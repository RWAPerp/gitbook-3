# Get PnL settlement history

`GET /v1/pnl_settlement/history`

**Authentication:** RWA

**Rate limit:** 20 requests per 1 second

## Description

Retrieve the historical PnL settlement history of the account.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `start_t` | query | integer | No | — |
| `end_t` | query | integer | No | — |
| `page` | query | integer | No | start from 1 |
| `size` | query | integer | No | — |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/pnl_settlement/history{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.meta` | object | Yes | — |
| `data.meta.total` | integer | Yes | Example: `9` |
| `data.meta.records_per_page` | integer | Yes | Example: `25` |
| `data.meta.current_page` | integer | Yes | start from 1 Example: `1` |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].id` | integer | No | Example: `10001` |
| `data.rows[].old_balance` | number | No | Example: `4050` |
| `data.rows[].new_balance` | number | No | Example: `3050` |
| `data.rows[].settled_amount` | number | No | Example: `-500` |
| `data.rows[].requested_time` | integer | No | Unix epoch time in ms Example: `1575014255089` |
| `data.rows[].settled_time` | integer | No | Unix epoch time in ms Example: `1575014255910` |
| `data.rows[].symbols` | array<object> | No | — |
| `data.rows[].symbols[].symbol` | string | Yes | Example: `PERP_BTC_USDC` |
| `data.rows[].symbols[].settled_amount` | integer | Yes | Example: `-500` |
