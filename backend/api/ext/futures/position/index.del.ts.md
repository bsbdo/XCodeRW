import { createError } from "@b/utils/error";
import { fromBigInt } from "@b/utils/eco/blockchain";
import { updateWalletBalance } from "@b/utils/eco/wallet";
import {
  notFoundMetadataResponse,
  serverErrorResponse,
  unauthorizedResponse,
} from "@b/utils/query";
import {
  getPosition,
  updatePositionStatus,
} from "@b/utils/futures/queries/positions";
import { getWallet } from "@b/api/finance/wallet/utils";

export const metadata: OperationObject = {
  summary: "Closes an open futures position",
  description: "Closes an open futures position for the logged-in user.",
  operationId: "closeFuturesPosition",
  tags: ["Futures", "Positions"],
  parameters: [
    {
      name: "id",
      in: "path",
      required: true,
      schema: {
        type: "string",
        description: "ID of the position to close",
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
            currency: {
              type: "string",
              description: "Currency symbol (e.g., BTC)",
            },
            pair: { type: "string", description: "Pair symbol (e.g., USDT)" },
            side: {
              type: "string",
              description: "Position side, either buy or sell",
            },
          },
          required: ["currency", "pair", "side"],
        },
      },
    },
  },
  responses: {
    200: {
      description: "Position closed successfully",
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
    404: notFoundMetadataResponse("Position"),
    500: serverErrorResponse,
  },
  requiresAuth: true,
};

export default async (data: Handler) => {
  const { body, user } = data;
  if (!user?.id) {
    throw createError({ statusCode: 401, message: "Unauthorized" });
  }

  const { currency, pair, side } = body;

  if (!currency || !pair || !side) {
    throw createError({
      statusCode: 400,
      message: "Invalid request parameters",
    });
  }
  const symbol = `${currency}/${pair}`;

  try {
    const position = await getPosition(user.id, symbol, side);
    if (!position) {
      throw createError({
        statusCode: 404,
        message: "Position not found",
      });
    }

    if (position.status !== "OPEN") {
      throw createError({
        statusCode: 400,
        message: "Position is not open",
      });
    }

    const finalBalanceChange = calculateFinalBalanceChange(position);

    const wallet = await getWallet(
      position.userId,
      "FUTURES",
      symbol.split("/")[1]
    );

    if (wallet) {
      if (finalBalanceChange > 0) {
        await updateWalletBalance(wallet, finalBalanceChange, "add");
      } else {
        await updateWalletBalance(
          wallet,
          Math.abs(finalBalanceChange),
          "subtract"
        );
      }
    }

    await updatePositionStatus(position.userId, position.id, "CLOSED");

    return { message: "Position closed and balance updated successfully" };
  } catch (error) {
    throw createError({
      statusCode: 500,
      message: `Failed to close position: ${error.message}`,
    });
  }
};

const calculateFinalBalanceChange = (position) => {
  const entryPrice = fromBigInt(position.entryPrice);
  const amount = fromBigInt(position.amount);
  const unrealizedPnl = fromBigInt(position.unrealizedPnl); // Ensure PnL is a number
  const investedAmount = entryPrice * amount;
  const finalBalanceChange = investedAmount + unrealizedPnl;
  return finalBalanceChange;
};
