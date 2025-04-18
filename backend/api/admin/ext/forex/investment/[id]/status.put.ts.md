import { updateStatus, updateRecordResponses } from "@b/utils/query";

export const metadata: OperationObject = {
  summary: "Updates the status of a Forex Investment",
  operationId: "updateForexInvestmentStatus",
  tags: ["Admin", "Forex Investments"],
  parameters: [
    {
      index: 0,
      name: "id",
      in: "path",
      required: true,
      description: "ID of the forex investment to update",
      schema: { type: "string" },
    },
  ],
  requestBody: {
    required: true,
    content: {
      "application/json": {
        schema: {
          type: "object",
          properties: {
            status: {
              type: "string",
              enum: ["ACTIVE", "COMPLETED", "CANCELLED", "REJECTED"],
              description: "New status to apply",
            },
          },
          required: ["status"],
        },
      },
    },
  },
  responses: updateRecordResponses("Forex Investment"),
  requiresAuth: true,
  permission: "Access Forex Investment Management",
};

export default async (data) => {
  const { body, params } = data;
  const { id } = params;
  const { status } = body;
  return updateStatus("forexInvestment", id, status);
};
