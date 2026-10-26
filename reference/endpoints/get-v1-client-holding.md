# Get current holding

`GET /v1/client/holding`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 seconds

## Description

Get the current summary of user token holdings.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `all` | query | boolean | No | true/false. If true then will return all token even if balance is empty. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/holding{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.holding` | array<object> | Yes | — |
| `data.holding[].updated_time` | number | Yes | Unix epoch time in milliseconds Example: `1580794149000` |
| `data.holding[].token` | string | Yes | Example: `USDT` |
| `data.holding[].holding` | number | Yes | Example: `282485.071904` |
| `data.holding[].frozen` | number | Yes | Example: `0` |
| `data.holding[].pending_short` | number | Yes | Example: `-2000` |
| `data.holding[].isolated_margin` | number | No | Example: `0` |
| `data.holding[].isolated_order_frozen` | number | No | Example: `0` |
