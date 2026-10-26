# Get funding fee history

`GET /v1/funding_fee/history`

**Authentication:** RWA

**Rate limit:** 20 requests per 60 second per user

## Description

Get funding fee history.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | query | string | No | omit to get funding fee history for all symbols |
| `start_t` | query | string | No | start time range that you wish to query, noted that the time stamp is a 13-digits timestamp. |
| `end_t` | query | string | No | end time range that you wish to query, noted that the time stamp is a 13-digits timestamp. |
| `page` | query | string | No | the page you wish to query. start from 1 |
| `size` | query | string | No | Default: 60 |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/funding_fee/history{body}` → URL-safe Base64 without trailing `=` |

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
| `data.rows[].symbol` | string | No | Example: `PERP_ETH_USDC` |
| `data.rows[].funding_rate` | number | No | Example: `0.00046875` |
| `data.rows[].mark_price` | number | No | Example: `2100` |
| `data.rows[].funding_fee` | number | No | Example: `1.6e-05` |
| `data.rows[].payment_type` | string | No | `Receive`/`Pay` Example: `Pay` |
| `data.rows[].status` | string | No | `Accrued`/`Settled` Example: `Accrued` |
| `data.rows[].created_time` | number | No | Example: `1682235722003` |
| `data.rows[].updated_time` | number | No | Example: `1682235722003` |
| `data.rows[].margin_mode` | string | No | Example: `CROSS` |
