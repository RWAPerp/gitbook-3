# Get esorder vesting list

`GET /v1/staking/esorder/vesting_list`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second per IP address

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `address` | query | string | Yes | — |
| `is_vesting` | query | boolean | Yes | — |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/staking/esorder/vesting_list{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | No | — |
| `data.rows` | array<object> | No | — |
| `data.rows[].vest_request_id` | number | No | Example: `1` |
| `data.rows[].vest_start_time` | number | No | `unlockTimestamp` - 15days Example: `1685600000000` |
| `data.rows[].vest_end_time` | number | No | `unlockTimestamp` + 75days Example: `1691200000000` |
| `data.rows[].total_vest_amount` | number | No | Example: `1500000.0` |
| `data.rows[].status` | string | No | `claimed` / `canceled` / `vesting` Example: `claimed` |
