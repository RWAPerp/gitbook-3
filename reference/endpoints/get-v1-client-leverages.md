# Get all leverage settings

`GET /v1/client/leverages`

**Authentication:** RWA

**Rate limit:** See platform limits

## Description

Get leverage settings for all symbols.

## Parameters

No fields are defined in the published schema.

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/leverages{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | No | — |
| `data.rows` | array<object> | No | Leverage settings for the authenticated account. |
| `data.rows[].symbol` | string | No | Example: `PERP_BTC_USDC` |
| `data.rows[].margin_mode` | string | No | Example: `CROSS` |
| `data.rows[].leverage` | integer | No | Example: `10` |
