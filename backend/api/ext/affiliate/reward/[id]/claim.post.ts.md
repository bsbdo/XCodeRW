import { models, sequelize } from "@b/db";
import { createError } from "@b/utils/error";
import {
  notFoundMetadataResponse,
  serverErrorResponse,
  unauthorizedResponse,
} from "@b/utils/query";
import { getWalletByUserIdAndCurrency } from "@b/utils/eco/wallet"; // Ensure this import is correct

export const metadata: OperationObject = {
  summary: "Claims a specific referral reward",
  description: "Processes the claim of a specified referral reward.",
  operationId: "claimReward",
  tags: ["MLM", "Rewards"],
  parameters: [
    {
      name: "id",
      in: "path",
      required: true,
      schema: { type: "string", description: "Referral reward UUID" },
    },
  ],
  responses: {
    200: {
      description: "Reward claimed successfully",
      content: {
        "application/json": {
          schema: {
            type: "object",
            properties: {
              message: { type: "string", description: "Success message" },
            },
          },
        },
      },
    },
    401: unauthorizedResponse,
    404: notFoundMetadataResponse("Affiliate Reward"),
    500: serverErrorResponse,
  },
  requiresAuth: true,
};

export default async (data: Handler) => {
  const { params, user } = data;
  const { id } = params;

  if (!user?.id) {
    throw createError({ statusCode: 401, message: "Unauthorized" });
  }

  const reward = await models.mlmReferralReward.findOne({
    where: { id, isClaimed: false },
    include: [{ model: models.mlmReferralCondition, as: "condition" }],
  });

  if (!reward) throw new Error("Reward not found or already claimed");
  if (reward.referrerId !== user.id) throw new Error("Unauthorized");

  let updatedWallet: any;

  // Handle ECO wallet creation logic differently
  if (reward.condition.rewardWalletType === "ECO") {
    // Utilize ecosystem-specific wallet retrieval/creation logic
    updatedWallet = await getWalletByUserIdAndCurrency(
      user.id,
      reward.condition.rewardCurrency
    );
  } else {
    // For non-ECO wallets, just find or create normally
    const wallet = await models.wallet.findOne({
      where: {
        userId: user.id,
        currency: reward.condition.rewardCurrency,
        type: reward.condition.rewardWalletType,
      },
    });

    if (!wallet) {
      updatedWallet = await models.wallet.create({
        userId: user.id,
        currency: reward.condition.rewardCurrency,
        type: reward.condition.rewardWalletType,
        status: true,
      });
    } else {
      updatedWallet = wallet;
    }
  }

  if (!updatedWallet)
    throw new Error("Wallet not found or could not be created");

  await sequelize.transaction(async (transaction) => {
    const newBalance = updatedWallet.balance + reward.reward;
    await updatedWallet.update({ balance: newBalance }, { transaction });

    await reward.update({ isClaimed: true }, { transaction });

    await models.transaction.create(
      {
        userId: user.id,
        walletId: updatedWallet.id,
        type: "REFERRAL_REWARD",
        status: "COMPLETED",
        amount: reward.reward,
        description: `Claimed referral reward for ${reward.condition?.type}`,
        metadata: JSON.stringify({ rewardId: reward.id }),
      },
      { transaction }
    );
  });

  return { message: "Reward claimed successfully" };
};
