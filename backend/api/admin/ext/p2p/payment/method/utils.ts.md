import {
  baseStringSchema,
  baseBooleanSchema,
  baseDateTimeSchema,
  baseEnumSchema,
} from "@b/utils/schema";

const id = baseStringSchema("ID of the P2P Payment Method");
const userId = baseStringSchema("ID of the User who owns the payment method");
const name = baseStringSchema("Name of the payment method");
const instructions = baseStringSchema(
  "Instructions for using the payment method"
);
const walletType = baseEnumSchema("Type of wallet used in the offer", [
  "FIAT",
  "SPOT",
  "ECO",
]);
const currency = baseStringSchema("Currency of the offer");
const chain = baseStringSchema("Blockchain chain used, if any", 191, 0, true);
const image = baseStringSchema("URL to an image of the payment method");
const status = baseBooleanSchema("Active status of the payment method");
const createdAt = baseDateTimeSchema("Creation date of the payment method");
const updatedAt = baseDateTimeSchema("Last update date of the payment method");

export const baseP2pPaymentMethodSchema = {
  id,
  userId,
  name,
  instructions,
  walletType,
  chain,
  currency,
  image,
  status,
  createdAt,
  updatedAt,
  deletedAt: baseDateTimeSchema("Deletion date of the payment method, if any"),
};

export const p2pPaymentMethodUpdateSchema = {
  type: "object",
  properties: {
    name,
    instructions,
    walletType,
    chain,
    currency,
    image,
    status,
  },
  required: ["name", "instructions", "walletType", "currency", "status"],
};

export const p2pPaymentMethodStoreSchema = {
  description: `P2P Payment Method created or updated successfully`,
  content: {
    "application/json": {
      schema: {
        type: "object",
        properties: baseP2pPaymentMethodSchema,
      },
    },
  },
};
