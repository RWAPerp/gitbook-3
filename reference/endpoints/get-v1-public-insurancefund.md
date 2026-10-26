# Get insurance fund info

`GET /v1/public/insurancefund`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Returns the current balance and risk metrics for the RWA Perp insurance fund.

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
| `data.min_insurance_fund_initial_margin_ratio` | number | Yes | Minimum initial margin ratio configured for the insurance fund. Example: `0.3` |
| `data.min_insurance_fund_margin_ratio` | number | Yes | Minimum maintenance margin ratio configured for the insurance fund. Example: `0.25` |
| `data.margin_ratio` | integer | Yes | Current margin ratio of the insurance fund. Example: `10` |
| `data.total_collateral_value` | number | Yes | Total collateral value held by the insurance fund. Example: `1.0008662996861E7` |
| `data.balance` | number | Yes | Current balance of the insurance fund. Example: `1.0001908678983E7` |
| `data.free_collateral` | number | Yes | Collateral currently available for use. Example: `1.0008662996861E7` |
| `data.total_account_value` | number | Yes | Total account value of the insurance fund. Example: `1.0008662996861E7` |
| `data.total_pnl_24_h` | integer | Yes | Total profit and loss over the last 24 hours. Example: `0` |
| `data.rows` | array<object> | Yes | Open position details currently held by the insurance fund. |
| `data.rows[].symbol` | string | Yes | Example: `PERP_BTC_USDC` |
| `data.rows[].timestamp` | integer | Yes | Example: `1685262631606` |
| `data.rows[].position_qty` | integer | Yes | Example: `0` |
| `data.rows[].cost_position` | number | Yes | Example: `-617.672835` |
| `data.rows[].last_sum_unitary_funding` | number | Yes | Example: `100.56` |
| `data.rows[].settle_price` | integer | Yes | Example: `0` |
| `data.rows[].average_open_price` | integer | Yes | Example: `0` |
| `data.rows[].pnl_24_h` | integer | Yes | Example: `0` |
| `data.rows[].fee_24_h` | integer | Yes | Example: `0` |
| `data.rows[].mark_price` | number | Yes | Example: `27821.8` |
