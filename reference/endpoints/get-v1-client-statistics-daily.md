# Get user daily statistics

`GET /v1/client/statistics/daily`

**Authentication:** RWA

**Rate limit:** See platform limits

## Description

**Limit 10 requests per 60 seconds**

Returns daily account snapshots for account value, PnL, and trading volume over the requested date range.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `start_date` | query | string | Yes | Start date in `YYYY-MM-DD` format. |
| `end_date` | query | string | Yes | End date in `YYYY-MM-DD` format. |
| `page` | query | number | No | Page number to return. Starts from 1. |
| `size` | query | number | No | Number of records to return per page. |
| `include_historical_data` | query | boolean | No | When set to `true`, the response also includes archived data and the rate limit becomes 1 request per 60 seconds. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/statistics/daily{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].account_value` | number | No | Total account value captured in the daily snapshot. Example: `456789.12` |
| `data.rows[].date` | string | No | Snapshot date in `YYYY-MM-DD` format. Example: `2023-09-14` |
| `data.rows[].perp_volume` | number | No | Perpetual futures trading volume for the day. Example: `451580.9523` |
| `data.rows[].pnl` | number | No | Profit and loss recorded for the day. Example: `123.45` |
| `data.rows[].snapshot_time` | number | No | Timestamp when the daily snapshot was generated in milliseconds. Example: `1722989203989` |
