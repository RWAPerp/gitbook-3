# Get asset history

`GET /v1/asset/history`

**Authentication:** RWA

**Rate limit:** See platform limits

## Description

**Limit 10 requests per 60 seconds**

Returns asset transfer history for the authenticated account, including deposits and withdrawals.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `token` | query | string | No | Filter results to a specific token symbol. |
| `side` | query | string | No | Filter by transfer direction: `DEPOSIT` or `WITHDRAW`. |
| `status` | query | string | No | Filter by transfer status. Supported values: `NEW`, `CONFIRM`, `PROCESSING`, `COMPLETED`, `FAILED`, `PENDING_REBALANCE`. |
| `start_t` | query | number | No | Filter results created at or after this timestamp in milliseconds. |
| `end_t` | query | number | No | Filter results created at or before this timestamp in milliseconds. |
| `page` | query | number | No | Page number to return. Starts from 1. |
| `size` | query | number | No | Number of records to return per page. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/asset/history{body}` → URL-safe Base64 without trailing `=` |

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
| `data.rows[].id` | string | Yes | Example: `230707030600002` |
| `data.rows[].tx_id` | string | Yes | On-chain transaction hash associated with the transfer. Example: `0x4b0714c63cc7abae72bf68e84e25860b88ca651b7d27dad1e32bf4c027fa5326` |
| `data.rows[].side` | string | Yes | Transfer direction of the record. Example: `WITHDRAW` |
| `data.rows[].token` | string | Yes | Token symbol involved in the transfer. Example: `USDC` |
| `data.rows[].amount` | number | Yes | Transfer amount. Example: `555` |
| `data.rows[].fee` | number | Yes | Fee charged for the transfer. Example: `0` |
| `data.rows[].trans_status` | string | Yes | Current processing status of the transfer. Example: `FAILED` |
| `data.rows[].created_time` | number | Yes | Timestamp when the transfer request was created in milliseconds. Example: `1688699193034` |
| `data.rows[].updated_time` | number | Yes | Timestamp of the latest transfer update in milliseconds. Example: `1688699193096` |
| `data.rows[].chain_id` | string | Yes | Chain ID associated with the transfer. Example: `986532` |
