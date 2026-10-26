# Get aggregate holding

`GET /v1/client/aggregate/holding`

**Authentication:** RWA

**Rate limit:** 1 request per 60 seconds

## Description

Only the main account is allowed to call this API.

## Parameters

No fields are defined in the published schema.

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/aggregate/holding{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | No | Example: `[{'account_id': '0x1111', 'updated_time': 1580794149000, 'token': 'BTC', 'holding': -28.000752, 'frozen': 0, 'pending_short': -2000, 'isolated_margin': 0, 'isolated_order_frozen': 0}, {'account_id': '0x2222', 'updated_time': 1580794149000, 'token': 'ETH', 'holding': -10.123456, 'frozen': 0, 'pending_short': -500, 'isolated_margin': 0, 'isolated_order_frozen': 0}]` |
| `data.rows` | array<object> | No | Aggregate asset balances for the main account and its sub accounts. |
| `data.rows[].account_id` | string | No | Account ID that owns the balance. |
| `data.rows[].updated_time` | number | No | Timestamp of the latest balance update in milliseconds. |
| `data.rows[].token` | string | No | Token symbol of the balance entry. |
| `data.rows[].holding` | number | No | Current balance held in the account. |
| `data.rows[].frozen` | number | No | Balance currently frozen by open orders or system processes. |
| `data.rows[].pending_short` | number | No | Balance reserved for pending short exposure. |
| `data.rows[].isolated_margin` | number | No | Balance allocated as isolated margin. |
| `data.rows[].isolated_order_frozen` | number | No | Balance frozen by open isolated-margin orders. |
