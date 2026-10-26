# Get receiver events

`GET /v1/client/asset/receiver_events`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second

## Description

Returns transfer events detected at the user's exclusive receiver address. Use this endpoint to poll for deposit status after a user transfers tokens to their receiver address.

## Parameters

No fields are defined in the published schema.

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/asset/receiver_events{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | No | — |
| `data.rows` | array<object> | No | — |
| `data.rows[].chain_id` | string | No | Chain ID where the transfer was detected. Example: `42161` |
| `data.rows[].tx_id` | string | No | Transaction hash of the user's token transfer. Example: `0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef` |
| `data.rows[].token` | string | No | Token symbol. Example: `USDC` |
| `data.rows[].amount` | number | No | Transfer amount. Example: `29.619521` |
| `data.rows[].created_time` | number | No | Timestamp when the transfer was detected (UNIX ms). Example: `1767848705855` |
| `data.rows[].updated_time` | number | No | Timestamp of last status update (UNIX ms). Example: `1767848724143` |
