# Edit algo order

`PUT /v1/algo/order`

**Authentication:** RWA

**Rate limit:** 5 requests per 1 second

| Base | URL |
|------|-----|
| Default REST | `https://api-trade.rwaperp.xyz` |
| VIP REST | `https://api-vip.rwaperp.xyz` |

Same path, same `RWA-*` signing on both hosts. Prefer VIP when your integration is provisioned for the dedicated REST endpoint. **To-B partners:** contact RWA Perp to obtain a dedicated Base URL before using `api-trade`, `api-vip`, or any custom host.

## Description

Edit a pending algo order by `order_id`. Only the price or quantity can be amended.

Note: This endpoint requires trading scope in API key.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `order_id` | body | string | Yes | — |
| `price` | body | number | No | — |
| `quantity` | body | number | No | — |
| `trigger_price` | body | number | No | — |
| `trigger_price_type` | body | string | No | — |
| `child_orders` | body | array<object> | No | Array of `EditAlgoOrderChildRequest` |
| `child_orders[].order_id` | body | string | No | — |
| `child_orders[].trigger_price` | body | number | No | — |
| `child_orders[].price` | body | number | No | — |
| `child_orders[].quantity` | body | number | No | — |
| `child_orders[].is_activated` | body | string | No | — |
| `child_orders[].trigger_price_type` | body | string | No | — |
| `child_orders[].child_orders` | body | array<object> | No | Array of `EditAlgoOrderChildRequest` |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}PUT/v1/algo/order{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.status` | string | No | Example: `EDIT_SENT` |
