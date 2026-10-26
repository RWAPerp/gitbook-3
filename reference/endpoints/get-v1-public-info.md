# Get available symbols

`GET /v1/public/info`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Get available symbols that RWA Perp supports, and also send order rules for each symbol. The definition of rules can be found at [Get Order Rules per Market](/docs/build-on-omnichain/restful-api/public/get-order-rules-per-symbol)

## Parameters

No fields are defined in the published schema.

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].symbol` | string | Yes | Example: `PERP_BTC_USDC` |
| `data.rows[].quote_min` | integer | Yes | Example: `0` |
| `data.rows[].quote_max` | integer | Yes | Example: `100000` |
| `data.rows[].quote_tick` | number | Yes | Example: `0.1` |
| `data.rows[].base_min` | number | Yes | Example: `1e-05` |
| `data.rows[].base_max` | integer | Yes | Example: `20` |
| `data.rows[].base_tick` | number | Yes | Example: `1e-05` |
| `data.rows[].min_notional` | integer | Yes | Example: `1` |
| `data.rows[].price_range` | number | Yes | Example: `0.02` |
| `data.rows[].price_scope` | number | Yes | Example: `0.4` |
| `data.rows[].std_liquidation_fee` | number | Yes | Example: `0.03` |
| `data.rows[].liquidator_fee` | number | Yes | Example: `0.015` |
| `data.rows[].claim_insurance_fund_discount` | number | Yes | Example: `0.0075` |
| `data.rows[].funding_period` | integer | Yes | Example: `8` |
| `data.rows[].cap_funding` | number | Yes | Example: `0.000375` |
| `data.rows[].floor_funding` | number | Yes | Example: `-0.000375` |
| `data.rows[].cap_ir` | number | No | Example: `0.0003` |
| `data.rows[].floor_ir` | number | No | Example: `-0.0003` |
| `data.rows[].interest_rate` | number | Yes | Example: `0.0001` |
| `data.rows[].imr_factor` | number | No | Example: `0.025` |
| `data.rows[].created_time` | integer | Yes | Example: `1684140107326` |
| `data.rows[].updated_time` | integer | Yes | Example: `1685345968053` |
| `data.rows[].base_mmr` | number | Yes | Example: `0.05` |
| `data.rows[].base_imr` | number | Yes | Example: `0.1` |
| `data.rows[].liquidation_tier` | number | No | Example: `1` |
| `data.rows[].global_max_oi_cap` | number | No | Example: `11111` |
