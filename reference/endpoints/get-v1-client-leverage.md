# Get leverage setting

`GET /v1/client/leverage`

**Authentication:** RWA

**Rate limit:** 1 requests per 1 second per IP address

## Description

Get account's leverage setting for a specific symbol.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | query | string | Yes | — |
| `margin_mode` | query | string | No | Default: `CROSS`. Supported values: `CROSS`/`ISOLATED` |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/leverage{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | No | — |
| `data.symbol` | string | No | Trading symbol for the leverage setting. Example: `PERP_BTC_USDC` |
| `data.margin_mode` | string | No | Margin mode for the returned leverage setting. Example: `ISOLATED` |
| `data.leverage` | integer | No | Configured leverage value for the symbol. Example: `19` |
