# Get liquidated positions info

`GET /v1/public/liquidated_positions`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Returns a list of positions that have been fully liquidated. This includes historical data on positions that were closed by the liquidation engine after margin was exhausted.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | query | string | No | Filter results to a specific trading symbol, for example `PERP_ETH_USDC`. |
| `start_t` | query | string | No | Start time of the query range as a 13-digit Unix timestamp in milliseconds. |
| `end_t` | query | string | No | End time of the query range as a 13-digit Unix timestamp in milliseconds. |
| `page` | query | string | No | Page number to return. Starts from 1. |
| `size` | query | string | No | Number of records to return per page. |

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
| `data.rows[].timestamp` | integer | Yes | Example: `1683802462092` |
| `data.rows[].liquidation_id` | integer | Yes | Example: `29` |
| `data.rows[].transfer_amount_to_insurance_fund` | integer | Yes | Example: `0` |
| `data.rows[].type` | string | No | Example: `liquidated` |
| `data.rows[].positions_by_perp` | array<object> | Yes | — |
| `data.rows[].positions_by_perp[].symbol` | string | Yes | Example: `PERP_ETH_USDC` |
| `data.rows[].positions_by_perp[].seq` | number | No | Example: `1730181536341943600` |
| `data.rows[].positions_by_perp[].position_qty` | integer | Yes | Example: `0` |
| `data.rows[].positions_by_perp[].liquidator_fee` | number | Yes | Example: `0.015` |
| `data.rows[].positions_by_perp[].cost_position_transfer` | integer | Yes | Example: `0` |
| `data.rows[].positions_by_perp[].transfer_price` | integer | Yes | Example: `1860` |
| `data.rows[].positions_by_perp[].insurance_fund_fee` | number | Yes | Example: `0.011999` |
| `data.rows[].positions_by_perp[].abs_insurance_fund_fee` | integer | Yes | Example: `0` |
| `data.rows[].positions_by_perp[].abs_liquidator_fee` | integer | No | Example: `0` |
