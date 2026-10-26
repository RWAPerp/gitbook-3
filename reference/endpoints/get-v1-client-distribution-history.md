# Get distribution history

`GET /v1/client/distribution_history`

**Authentication:** RWA

**Rate limit:** 10 requests per second

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `status` | query | string | No | One of `CREATED`/`SPLIT`/`COMPLETED` |
| `type` | query | string | No | One of `BROKER_FEE`/`REFEREE_REBATE`/`REFERRER_REBATE` |
| `start_t` | query | string | No | — |
| `end_t` | query | string | No | — |
| `page` | query | integer | No | start from 1 |
| `size` | query | integer | No | — |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/distribution_history{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].id` | integer | No | Example: `12345` |
| `data.rows[].token` | string | No | Example: `USDC` |
| `data.rows[].type` | string | No | `REFERRAL_REBATE`/`REFEREE_REBATE`/`BROKER_FEE` Example: `REFERRAL_REBATE` |
| `data.rows[].amount` | number | No | Example: `12.12` |
| `data.rows[].status` | string | No | Example: `COMPLETED` |
| `data.rows[].created_time` | number | No | Example: `1703511545867` |
| `data.rows[].updated_time` | number | No | Example: `1703511545867` |
| `data.meta` | object | No | — |
| `data.meta.records_per_page` | integer | No | Example: `25` |
| `data.meta.current_page` | integer | No | start from 1 Example: `1` |
| `data.meta.total` | integer | No | Example: `50` |
