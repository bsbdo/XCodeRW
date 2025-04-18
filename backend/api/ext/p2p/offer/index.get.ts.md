// /server/api/p2p/offers/index.get.ts

import { models } from "@b/db";

import { crudParameters, paginationSchema } from "@b/utils/constants";
import {
  getFiltered,
  notFoundMetadataResponse,
  serverErrorResponse,
  unauthorizedResponse,
} from "@b/utils/query";
import { p2pOfferSchema } from "./utils";

export const metadata: OperationObject = {
  summary: "Lists P2P offers with pagination and optional filtering",
  operationId: "listP2POffers",
  tags: ["P2P", "Offers"],
  parameters: crudParameters,
  responses: {
    200: {
      description: "List of P2P offers with pagination information",
      content: {
        "application/json": {
          schema: {
            type: "object",
            properties: {
              data: {
                type: "array",
                items: {
                  type: "object",
                  properties: p2pOfferSchema,
                },
              },
              pagination: paginationSchema,
            },
          },
        },
      },
    },
    401: unauthorizedResponse,
    404: notFoundMetadataResponse("P2P Offers"),
    500: serverErrorResponse,
  },
};

export default async (data: Handler) => {
  const { query } = data;

  // Call the generic fetch function
  return getFiltered({
    model: models.p2pOffer,
    query,
    where: { status: "ACTIVE" },
    sortField: query.sortField || "createdAt",
    includeModels: [
      {
        model: models.p2pTrade,
        as: "p2pTrades",
        attributes: ["id", "status"],
      },
      {
        model: models.user,
        as: "user",
        attributes: ["firstName", "lastName", "avatar"],
      },
      {
        model: models.p2pPaymentMethod,
        as: "paymentMethod",
        attributes: ["id", "name", "image", "currency"],
      },
      {
        model: models.p2pReview,
        as: "p2pReviews",
        attributes: ["id", "rating"],
      },
    ],
    numericFields: ["amount", "price", "rating"],
  });
};
