# Batch create order

`POST /v1/batch-order`

**Authentication:** RWA (`trading` scope)

**Rate limit:** 1 request per 1 second

| Base | URL |
|------|-----|
| Default REST | `https://api-trade.rwaperp.xyz` |
| VIP REST | `https://api-vip.rwaperp.xyz` |

Same path, same `RWA-*` signing on both hosts. Prefer VIP when your integration is provisioned for the dedicated REST endpoint. **To-B partners:** contact RWA Perp to obtain a dedicated Base URL before using `api-trade`, `api-vip`, or any custom host.

## Description

Creates up to 10 orders in one request. Send the orders in the `orders` JSON array. Each order in the request counts as one order toward the overall create order rate limit.

Supports reduce-only orders. Set `reduce_only: true` on an individual item in the `orders` array to restrict that order to reducing an existing position. Configure this flag independently for each order in the batch.

Note: This endpoint requires `trading` scope in API key.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `x-recv-window` | header | number | No | Use this parameter to control the timeout threshold for placing order, unit in miliseconds |
| `orders` | body | array<object> | No | — |
| `orders[].symbol` | body | string | Yes | — |
| `orders[].client_order_id` | body | string | No | — |
| `orders[].order_type` | body | string | Yes | — |
| `orders[].order_price` | body | number | No | — |
| `orders[].order_quantity` | body | number | No | — |
| `orders[].order_amount` | body | number | No | — |
| `orders[].reduce_only` | body | boolean | No | When true, this order can only reduce an existing position and cannot increase or open a position. Set independently for each item in the orders array. Example: `True` |
| `orders[].visible_quantity` | body | number | No | — |
| `orders[].side` | body | string | Yes | — |
| `orders[].order_tag` | body | string | No | Optional tag for the order. Supports two formats:
- Referral code: plain string (e.g., `REFERRAL2026`) - overrides referral relationship
- Custom trading fee: `enum:<owning_broker_id>:<enum_id>` (e.g., `enum:broker_b:GRID_PRO`) - adds the custom fee and preserves the existing referral relationship
New custom-fee-tagged orders must use the current three-segment format. Legacy `enum:<enum_id>` tags are supported only on orders accepted before cutover.
Maximum length: 128 characters. Cannot be modified after order placement.
 Example: `enum:broker_b:GRID_PRO` |
| `orders[].margin_mode` | body | string | No | Margin mode for the order. Default: the symbol's current default margin mode. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/batch-order{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].order_id` | number | No | Example: `13` |
| `data.rows[].client_order_id` | string | No | Example: `testclientid` |
| `data.rows[].order_type` | string | No | Example: `LIMIT` |
| `data.rows[].order_price` | number | No | Example: `100.12` |
| `data.rows[].order_quantity` | number | No | Example: `0.987654` |
| `data.rows[].error_message` | string | No | Example: `none` |
