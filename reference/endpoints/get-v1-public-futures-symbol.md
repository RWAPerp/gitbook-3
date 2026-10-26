# Get market info for one symbol

`GET /v1/public/futures/{symbol}`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Get basic market information for one trading pair.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | path | string | Yes | — |

## Responses

### HTTP 200

Success

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].symbol` | string | Yes | Example: `PERP_ETH_USDC` |
| `data.rows[].index_price` | number | Yes | Example: `1901.6` |
| `data.rows[].mark_price` | number | Yes | Example: `1950.1` |
| `data.rows[].sum_unitary_funding` | number | Yes | Example: `387.891` |
| `data.rows[].est_funding_rate` | number | Yes | Example: `0.00046875` |
| `data.rows[].last_funding_rate` | number | Yes | Example: `0.00046875` |
| `data.rows[].next_funding_time` | integer | Yes | Example: `1683270060000` |
| `data.rows[].open_interest` | number | Yes | Example: `815539` |
| `data.rows[].24h_open` | number | Yes | Example: `2115.1` |
| `data.rows[].24h_close` | number | Yes | Example: `2115.2` |
| `data.rows[].24h_high` | number | Yes | Example: `2115.3` |
| `data.rows[].24h_low` | number | Yes | Example: `2114.9` |
| `data.rows[].24h_amount` | number | Yes | Example: `449054.7636` |
| `data.rows[].24h_volume` | number | Yes | Example: `6716559` |
