# Get valor redeem info

`GET /v1/staking/valor/redeem`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second per IP address

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `address` | query | string | Yes | — |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/staking/valor/redeem{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | No | — |
| `data.redeeming_valor_amount` | number | No | Example: `1000` |
| `data.chain_details` | array<object> | No | — |
| `data.chain_details[].chain_id` | number | No | Example: `1` |
| `data.chain_details[].pending_usdc` | number | No | Example: `5000` |
| `data.chain_details[].available_usdc` | number | No | Example: `1500` |
