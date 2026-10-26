# Cancel order by client_order_id

`DELETE /v1/client/order`

**Authentication:** RWA (`trading` scope)

**Rate limit:** 10 requests per 1 second

## Description

`DELETE /v1/client/order?client_order_id={client_order_id}&symbol={symbol}`

Cancel an order by `client_order_id`.

Note: This endpoint requires `trading` scope in API key.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | query | string | Yes | — |
| `client_order_id` | query | string | Yes | — |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}DELETE/v1/client/order{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.status` | string | Yes | Example: `CANCEL_SENT` |
