# Get builder's users' volumes

`GET /v1/volume/broker/daily`

**Authentication:** RWA

**Rate limit:** See platform limits

## Description

**Limit 10 requests per 60 seconds**

Get the daily historical breakdown of the user trading volume on specified builder.

The provided `start_date`/`end_date` has to be within a 90-day range.
Updated hourly

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `start_date` | query | string | Yes | Format YYYY-MM-DD |
| `end_date` | query | string | Yes | Format YYYY-MM-DD |
| `page` | query | number | No | start from 1 |
| `size` | query | number | No | — |
| `address` | query | string | No | — |
| `order_tag` | query | string | No | Filter by the full stored order tag, including a current-format `enum:<owning_broker_id>:<enum_id>` tag. |
| `aggregateBy` | query | string | No | Either by `DATE` or by `ACCOUNT` |
| `sort` | query | string | No | Allow sort by

`ascending_broker_fee`
`descending_broker_fee`
`ascending_perp_maker_volume`
`descending_perp_maker_volume`
`ascending_perp_taker_volume`
`descending_perp_taker_volume`
`ascending_perp_volume`
`descending_perp_volume`
`ascending_total_fee`
`descending_total_fee`
 |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/volume/broker/daily{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.snapshot_time` | number | No | Example: `1702989203989` |
| `data.rows` | array<object> | Yes | Daily account statistic snapshots for the requested date range. |
| `data.rows[].account_id` | string | No | Example: `0x58220761ade872c94f85e62f1b24a74eec792aaa3677b6201071fd05c1698e89` |
| `data.rows[].date` | string | No | Example: `2023-09-14` |
| `data.rows[].perp_volume` | number | No | Example: `451580.9523` |
| `data.rows[].perp_maker_volume` | number | No | Example: `123.456` |
| `data.rows[].perp_taker_volum` | number | No | Example: `123.456` |
| `data.rows[].total_fee` | number | No | Example: `123.456` |
| `data.rows[].broker_fee` | number | No | Example: `123.456` |
| `data.rows[].address` | string | No | Example: `0x0000000000` |
| `data.rows[].realized_pnl` | number | No | Example: `111.0` |
| `data.meta` | object | No | — |
| `data.meta.records_per_page` | integer | No | Example: `25` |
| `data.meta.current_page` | integer | No | start from 1 Example: `1` |
| `data.meta.total` | integer | No | Example: `50` |
