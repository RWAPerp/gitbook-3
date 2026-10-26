# Get liquidated positions of account

`GET /v1/liquidations`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second per IP address

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | query | string | No | — |
| `start_t` | query | number | No | — |
| `end_t` | query | number | No | — |
| `page` | query | number | No | start from 1 |
| `size` | query | number | No | — |
| `sort_by` | query | string | No | `liquidation_id`/`time` |
| `liquidation_id` | query | number | No | return the designed liquidation_id only |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/liquidations{body}` → URL-safe Base64 without trailing `=` |

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
| `data.rows[].liquidation_id` | number | No | Example: `101` |
| `data.rows[].timestamp` | number | No | Example: `1663313562090` |
| `data.rows[].transfer_amount_to_insurance_fund` | number | No | Example: `0` |
| `data.rows[].margin_ratio` | number | No | Example: `0.10436069` |
| `data.rows[].account_mmr` | number | No | Example: `0.012` |
| `data.rows[].position_notional` | number | No | Example: `28.415534` |
| `data.rows[].collateral_value` | number | No | Example: `2.965465` |
| `data.rows[].positions_by_perp` | array<object> | No | — |
| `data.rows[].positions_by_perp[].total_position` | number | Yes | Example: `41.6` |
| `data.rows[].positions_by_perp[].mark_price` | number | No | Example: `123400` |
| `data.rows[].positions_by_perp[].symbol` | string | Yes | Example: `PERP_BTC_USDC` |
| `data.rows[].positions_by_perp[].position_qty` | number | Yes | Example: `0.00017` |
| `data.rows[].positions_by_perp[].liquidator_fee` | number | Yes | Example: `0.006` |
| `data.rows[].positions_by_perp[].cost_position_transfer` | number | Yes | Example: `21.002786` |
| `data.rows[].positions_by_perp[].transfer_price` | number | Yes | Example: `123545.8` |
| `data.rows[].positions_by_perp[].insurance_fund_fee` | number | Yes | Example: `0.006` |
| `data.rows[].positions_by_perp[].abs_insurance_fund_fee` | number | Yes | Absolute fee amount allocated to the insurance fund. Example: `0.126017` |
| `data.rows[].positions_by_perp[].abs_liquidation_fee` | number | Yes | Total absolute liquidation fee, equal to the liquidator fee plus the insurance fund fee. Example: `0.252034` |
