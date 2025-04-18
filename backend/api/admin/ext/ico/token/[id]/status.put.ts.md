import { updateStatus, updateRecordResponses } from "@b/utils/query";

export const metadata = {
  summary: "Updates the status of an ICO Token",
  operationId: "updateIcoTokenStatus",
  tags: ["Admin", "ICO Tokens"],
  parameters: [
    {
      index: 0,
      name: "id",
      in: "path",
      required: true,
      description: "ID of the ICO token to update",
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
              enum: ["PENDING", "ACTIVE", "COMPLETED", "REJECTED", "CANCELLED"],
              description: "New status to apply",
            },
          },
          required: ["status"],
        },
      },
    },
  },
  responses: updateRecordResponses("ICO Token"),
  requiresAuth: true,
  permission: "Access ICO Token Management",
};

export default async (data) => {
  const { body, params } = data;
  const { id } = params;
  const { status } = body;
  return updateStatus("icoToken", id, status);
};
