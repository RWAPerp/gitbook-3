# Get positions under liquidation

`GET /v1/public/liquidation`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Returns a list of positions that are currently being liquidated. These are positions where the margin has dropped below the maintenance margin requirement and are in the process of being closed by the liquidation engine.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `start_t` | query | number | No | start time range that you wish to query, noted that the time stamp is a 13-digits timestamp. |
| `end_t` | query | number | No | end time range that you wish to query, noted that the time stamp is a 13-digits timestamp. |
| `page` | query | integer | No | the page you wish to query. start from 1 |
| `size` | query | integer | No | Default: 60 |

## Responses

### HTTP 200

Success

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
| `data.rows[].timestamp` | integer | No | Example: `1685298157704` |
| `data.rows[].type` | string | No | Example: `liquidated` |
| `data.rows[].liquidation_id` | integer | No | Example: `1730` |
| `data.rows[].positions_by_perp` | array<object> | No | — |
| `data.rows[].positions_by_perp[].symbol` | string | No | Example: `PERP_BTC_USDC` |
| `data.rows[].positions_by_perp[].position_qty` | number | No | Example: `-0.22457` |
| `data.rows[].positions_by_perp[].liquidator_fee` | number | No | Example: `0.015` |
