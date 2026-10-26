# Update margin mode

`POST /v1/client/margin_mode`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second per user

## Description

Update the default margin mode for a specific symbol. Switching a symbol's margin mode is only possible when you have no open positions or pending orders on that symbol in the current mode.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | body | string | Yes | Symbol to update margin mode for Example: `PERP_BTC_USDC` |
| `default_margin_mode` | body | string | Yes | Target margin mode Example: `ISOLATED` |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/client/margin_mode{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
