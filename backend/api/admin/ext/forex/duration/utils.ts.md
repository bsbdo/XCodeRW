import {
  baseIntegerSchema,
  baseEnumSchema,
  baseStringSchema,
} from "@b/utils/schema";

const id = baseStringSchema("ID of the Forex Duration");
const duration = baseIntegerSchema("Duration in time units");
const timeframe = baseEnumSchema("Unit of time for duration", [
  "HOUR",
  "DAY",
  "WEEK",
  "MONTH",
]);

export const forexDurationSchema = {
  id,
  duration,
  timeframe,
};

export const baseForexDurationSchema = {
  id,
  duration,
  timeframe,
};

export const forexDurationUpdateSchema = {
  type: "object",
  properties: {
    duration,
    timeframe,
  },
  required: ["duration", "timeframe"],
};

export const forexDurationStoreSchema = {
  description: `Forex Duration created or updated successfully`,
  content: {
    "application/json": {
      schema: {
        type: "object",
        properties: baseForexDurationSchema,
      },
    },
  },
};
