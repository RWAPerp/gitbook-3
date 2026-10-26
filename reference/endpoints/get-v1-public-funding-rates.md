# Get predicted funding rates for all markets

`GET /v1/public/funding_rates`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Get predicted funding rates for all futures trading pairs.

Get the : 
* `last_funding_rate` : latest hourly funding rate for all the markets for the last funding period (dt = 8h)
* `est_funding_rate` : rolling average of all funding rates over the last 8 hours

## Parameters

No fields are defined in the published schema.

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
| `data.rows[].est_funding_rate` | integer | Yes | Example: `0` |
| `data.rows[].est_funding_rate_timestamp` | integer | Yes | Example: `1683880020000` |
| `data.rows[].last_funding_rate` | number | Yes | Example: `0.0001` |
| `data.rows[].last_funding_rate_timestamp` | integer | Yes | Example: `1683878400000` |
| `data.rows[].next_funding_time` | integer | Yes | Example: `1683907200000` |
| `data.rows[].sum_unitary_funding` | number | Yes | Example: `521.367` |
