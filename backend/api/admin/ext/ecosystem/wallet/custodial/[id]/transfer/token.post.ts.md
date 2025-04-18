// /api/admin/ecosystem/custodialWallets/transferTokens.post.ts

import { models } from "@b/db";
import { getCustodialWalletContract } from "@b/utils/eco/custodialWallet";
import { getProvider } from "@b/utils/eco/provider";
import { ethers } from "ethers";
import { decrypt } from "@b/utils/encrypt";
import {
  notFoundMetadataResponse,
  serverErrorResponse,
  unauthorizedResponse,
} from "@b/utils/query";

export const metadata: OperationObject = {
  summary: "Transfer ERC-20 tokens from Ecosystem Custodial Wallet",
  operationId: "transferTokensEcosystemCustodialWallet",
  tags: ["Admin", "Ecosystem Custodial Wallets"],
  parameters: [
    {
      index: 0,
      name: "id",
      in: "path",
      description: "Ecosystem Custodial Wallet ID",
      required: true,
      schema: {
        type: "string",
      },
    },
  ],
  requestBody: {
    required: true,
    content: {
      "application/json": {
        schema: {
          type: "object",
          properties: {
            tokenAddress: {
              type: "string",
              description: "ERC-20 token contract address",
            },
            recipient: {
              type: "string",
              description: "Recipient address",
            },
            amount: {
              type: "string",
              description: "Amount to transfer (in wei)",
            },
          },
          required: ["id", "tokenAddress", "recipient", "amount"],
        },
      },
    },
  },
  responses: {
    200: {
      description: "ERC-20 tokens transferred successfully",
      content: {
        "application/json": {
          schema: {
            type: "object",
            properties: {
              transactionHash: {
                type: "string",
                description: "Transaction hash",
              },
            },
          },
        },
      },
    },
    401: unauthorizedResponse,
    404: notFoundMetadataResponse("Custodial Wallet"),
    500: serverErrorResponse,
  },
  requiresAuth: true,
  permission: "Access Ecosystem Custodial Wallet Management",
};

export default async (data: Handler) => {
  const { user, body, params } = data;
  if (!user) {
    throw new Error("Authentication required to transfer tokens");
  }
  const { id } = params;
  const { tokenAddress, recipient, amount } = body;

  try {
    const custodialWallet = await models.ecosystemCustodialWallet.findByPk(id);
    if (!custodialWallet) {
      throw new Error(`Custodial wallet not found`);
    }

    const masterWallet = await models.ecosystemMasterWallet.findByPk(
      custodialWallet.masterWalletId
    );
    if (!masterWallet) {
      throw new Error(`Master wallet not found`);
    }

    if (!masterWallet.data) {
      throw new Error("Master wallet data not found");
    }

    const decryptedData = JSON.parse(decrypt(masterWallet.data));
    const { privateKey } = decryptedData;

    const provider = await getProvider(custodialWallet.chain);
    const signer = new ethers.Wallet(privateKey).connect(provider);
    const contract = await getCustodialWalletContract(
      custodialWallet.address,
      signer
    );

    const transaction = await contract.transferTokens(
      tokenAddress,
      recipient,
      amount
    );
    await transaction.wait();

    return {
      message: "ERC-20 tokens transferred successfully",
    };
  } catch (error) {
    console.error(`Failed to transfer ERC-20 tokens: ${error.message}`);
    throw new Error(error.message);
  }
};
