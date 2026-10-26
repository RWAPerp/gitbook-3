# Edit order

`PUT /v1/order`

**Authentication:** RWA (`trading` scope)

**Rate limit:** 10 request per 1 second

| Base | URL |
|------|-----|
| Default REST | `https://api-trade.rwaperp.xyz` |
| VIP REST | `https://api-vip.rwaperp.xyz` |

Same path, same `RWA-*` signing on both hosts. Prefer VIP when your integration is provisioned for the dedicated REST endpoint. **To-B partners:** contact RWA Perp to obtain a dedicated Base URL before using `api-trade`, `api-vip`, or any custom host.

## Description

Edit a pending order by `order_id`. Only the `order_price` or `order_quantity` can be amended.

Note: This endpoint requires `trading` scope in API key.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `order_id` | body | string | Yes | — |
| `symbol` | body | string | Yes | — |
| `client_order_id` | body | string | No | — |
| `order_type` | body | string | Yes | — |
| `order_price` | body | number | No | — |
| `order_quantity` | body | number | No | — |
| `order_amount` | body | number | No | — |
| `reduce_only` | body | boolean | No | — |
| `visible_quantity` | body | number | No | — |
| `side` | body | string | Yes | — |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}PUT/v1/order{body}` → URL-safe Base64 without trailing `=` |
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
