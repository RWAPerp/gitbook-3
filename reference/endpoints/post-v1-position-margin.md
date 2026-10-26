# Add or reduce position margin

`POST /v1/position_margin`

**Authentication:** RWA (`trading` scope)

**Rate limit:** 10 requests per 1 second per user

## Description

Add or reduce margin for an existing isolated margin position. This allows you to adjust the margin allocated to a specific isolated position after it has been opened.

- `ADD`: Transfer margin from your available balance to the isolated position, lowering the liquidation price.
- `REDUCE`: Transfer margin from the isolated position back to your available balance, raising the liquidation price.

**Prerequisites:** You must have an open isolated position on the specified symbol.

Note: This endpoint requires `trading` scope in API key.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | body | string | Yes | Symbol of the isolated position Example: `PERP_ETH_USDC` |
| `amount` | body | string | Yes | Amount of margin to add or reduce Example: `3` |
| `type` | body | string | Yes | Operation type Example: `ADD` |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/position_margin{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
