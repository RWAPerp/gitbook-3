# Cancel all pending algo orders

`DELETE /v1/algo/orders`

**Authentication:** RWA

**Rate limit:** 5 requests per 1 second

## Description

`DELETE /v1/algo/orders?symbol={symbol}`

Cancel all pending algo orders.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | query | string | No | — |
| `algo_type` | query | string | No | Note: `STOP` will cancel both `TAKE_PROFIT` and `STOP_LOSS` |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}DELETE/v1/algo/orders{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.status` | string | Yes | Example: `CANCEL_ALL_SENT` |
