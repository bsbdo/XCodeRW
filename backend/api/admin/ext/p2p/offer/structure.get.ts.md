// /api/p2pOffers/structure.get.ts

import { models } from "@b/db";
import { structureSchema } from "@b/utils/constants";
import {
  userAvatarSchema,
  userFullNameSchema,
} from "@b/utils/schema/structure";
import { CacheManager } from "@b/utils/cache";
import { getCurrencyConditions } from "@b/utils/currency";

export const metadata = {
  summary: "Get form structure for P2P Offers",
  operationId: "getP2pOfferStructure",
  tags: ["Admin", "P2P Offers"],
  responses: {
    200: {
      description: "Form structure for managing P2P Offers",
      content: structureSchema,
    },
  },
  permission: "Access P2P Offer Management",
};

export const p2pOfferStructure = async () => {
  const paymentMethods = await models.p2pPaymentMethod.findAll({
    where: { status: true },
  });
  const userId = {
    type: "input",
    label: "User",
    name: "userId",
    placeholder: "Enter the user ID",
    icon: "lets-icons:user-duotone",
  };

  const paymentMethodId = {
    type: "select",
    label: "Payment Method ID",
    name: "paymentMethodId",
    options: paymentMethods.map((method) => ({
      value: method.id,
      label: method.name,
    })),
    placeholder: "Select payment method",
  };

  const walletType = {
    type: "select",
    label: "Wallet Type",
    name: "walletType",
    options: [
      { value: "FIAT", label: "Fiat" },
      { value: "SPOT", label: "Spot" },
    ],
    placeholder: "Select wallet type",
  };

  const currencyConditions = await getCurrencyConditions();
  const cacheManager = CacheManager.getInstance();
  const extensions = await cacheManager.getExtensions();
  if (extensions.has("ecosystem")) {
    walletType.options.push({ value: "ECO", label: "Funding" });
  }
  const currency = {
    type: "select",
    label: "Currency",
    name: "currency",
    options: [],
    conditions: {
      walletType: currencyConditions,
    },
  };

  const chain = {
    type: "input",
    label: "Chain",
    name: "chain",
    placeholder: "Blockchain network (optional)",
    condition: { walletType: "ECO" },
  };

  const amount = {
    type: "input",
    label: "Total Amount",
    name: "amount",
    placeholder: "Total amount for the offer",
    ts: "number",
  };

  const minAmount = {
    type: "input",
    label: "Minimum Amount",
    name: "minAmount",
    placeholder: "Minimum transaction amount",
    ts: "number",
  };

  const maxAmount = {
    type: "input",
    label: "Maximum Amount",
    name: "maxAmount",
    placeholder: "Maximum transaction amount",
    ts: "number",
  };

  const inOrder = {
    type: "input",
    label: "In Order",
    name: "inOrder",
    placeholder: "Amount currently in order",
    ts: "number",
  };

  const price = {
    type: "input",
    label: "Price per Unit",
    name: "price",
    placeholder: "Set price per unit of currency",
    ts: "number",
  };

  const status = {
    type: "select",
    label: "Status",
    name: "status",
    options: [
      { value: "PENDING", label: "Pending" },
      { value: "ACTIVE", label: "Active" },
      { value: "COMPLETED", label: "Completed" },
      { value: "CANCELLED", label: "Cancelled" },
    ],
    placeholder: "Select the offer status",
  };

  return {
    userId,
    walletType,
    currency,
    chain,
    amount,
    minAmount,
    maxAmount,
    inOrder,
    price,
    paymentMethodId,
    status,
  };
};

export default async () => {
  const {
    userId,
    walletType,
    currency,
    chain,
    amount,
    minAmount,
    maxAmount,
    inOrder,
    price,
    paymentMethodId,
    status,
  } = await p2pOfferStructure();

  return {
    get: [
      {
        fields: [
          userAvatarSchema,
          {
            fields: [
              userFullNameSchema,
              {
                type: "input",
                component: "InfoBlock",
                label: "Payment Method",
                name: "paymentMethod.name",
                icon: "ph:wallet-light",
              },
            ],
            grid: "column",
          },
        ],
        className: "card-dashed mb-5 items-center",
      },
      [walletType, currency, chain],
      [amount, price],
      [minAmount, maxAmount],
      inOrder,
      status,
    ],
    set: [
      [userId, paymentMethodId],
      [walletType, currency, chain],
      [amount, price],
      [minAmount, maxAmount],
      inOrder,
      status,
    ],
  };
};
