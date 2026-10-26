# Get order rules per symbol

`GET /v1/public/info/{symbol}`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

This endpoint provides all the values for the rules that an order need
to fulfil in order for it to be placed successfully. The rules are
defined as follows:


Price filter


- `price` >= `quote_min`

- `price` =< `quote_max`

- `(price - quote_min) % quote_tick` should equal to zero

- `price` =< `mark_price * (1 + price_range)` when BUY

- `price` >= `mark_price * (1 - price_range)` when SELL


Size filter


- `base_min` =< `quantity` =< `base_max`

- `(quantity - base_min) % base_tick` should equal to zero


Min Notional filter


- `price * quantity` should greater than `min_notional`


Risk Exposure filer


- Order size should be within holding threshold. See
[account_info](/docs/build-on-omnichain/restful-api/private/get-account-information)

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | path | string | Yes | — |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.symbol` | string | Yes | Example: `PERP_BTC_USDC` |
| `data.quote_min` | integer | Yes | Example: `0` |
| `data.quote_max` | integer | Yes | Example: `100000` |
| `data.quote_tick` | number | Yes | Example: `0.1` |
| `data.base_min` | number | Yes | Example: `1e-05` |
| `data.base_max` | integer | Yes | Example: `20` |
| `data.base_tick` | number | Yes | Example: `1e-05` |
| `data.min_notional` | integer | Yes | Example: `1` |
| `data.price_range` | number | Yes | Example: `0.02` |
| `data.price_scope` | number | Yes | Example: `0.4` |
| `data.std_liquidation_fee` | number | Yes | Example: `0.03` |
| `data.liquidator_fee` | number | Yes | Example: `0.015` |
| `data.claim_insurance_fund_discount` | number | Yes | Example: `0.0075` |
| `data.funding_period` | integer | Yes | Example: `8` |
| `data.cap_funding` | number | Yes | Example: `0.000375` |
| `data.floor_funding` | number | Yes | Example: `-0.000375` |
| `data.cap_ir` | number | No | Example: `0.0003` |
| `data.floor_ir` | number | No | Example: `-0.0003` |
| `data.interest_rate` | number | Yes | Example: `0.0001` |
| `data.imr_factor` | number | No | Example: `0.025` |
| `data.created_time` | integer | Yes | Example: `1684140107326` |
| `data.updated_time` | integer | Yes | Example: `1685345968053` |
| `data.base_mmr` | number | Yes | Example: `0.05` |
| `data.base_imr` | number | Yes | Example: `0.1` |
| `data.liquidation_tier` | number | No | Example: `1` |
| `data.global_max_oi_cap` | number | No | Example: `11111` |
