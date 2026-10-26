# Get internal transfer history

`GET /v1/internal_transfer_history`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second

## Description

Returns internal transfer history for the authenticated account.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `status` | query | string | No | `CREATED`/`PENDING`/`COMPLETED`/`FAILED` |
| `start_t` | query | string | No | — |
| `end_t` | query | string | No | — |
| `page` | query | number | No | start from 1 |
| `size` | query | number | No | — |
| `side` | query | string | Yes | `IN`/`OUT` |
| `from_account_id` | query | string | No | — |
| `to_account_id` | query | string | No | — |
| `main_sub_only` | query | boolean | No | If True, return only internal transfers between main account and sub accounts. 
If False, return only internal transfers between main account and other main accounts. 
If empty, return all transfer history.
 |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/internal_transfer_history{body}` → URL-safe Base64 without trailing `=` |

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
| `data.rows[].internal_transfer_request_id` | number | No | Example: `123` |
| `data.rows[].id` | string | No | Unique ID of the internal transfer record. Example: `230707030600002` |
| `data.rows[].token` | string | No | Example: `USDC` |
| `data.rows[].amount` | number | No | Example: `555` |
| `data.rows[].from_account_id` | string | No | Example: `0x000000` |
| `data.rows[].to_account_id` | string | No | Example: `0x000000` |
| `data.rows[].status` | string | No | Example: `FAILED` |
| `data.rows[].created_time` | number | No | Example: `1688699193034` |
| `data.rows[].updated_time` | number | No | Example: `1688699193034` |
