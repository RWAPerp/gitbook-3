# Get valor2 pool info

`GET /v1/staking/valor2/pool_info`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Parameters

No fields are defined in the published schema.

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | No | — |
| `data.revenue_rate` | number | No | Example: `0.6` |
| `data.valor_price_esorder` | number | No | Example: `0.018128737338881` |
| `data.treasury_pool_value` | number | No | esorder Example: `741510.854264` |
| `data.est_treasury_inflow` | number | No | total accumulated USDC pending buyback (usdc) Example: `1502.490346` |
| `data.order_price_usdc` | number | No | Example: `0.2` |
| `data.total_redeemed_amount` | number | No | Example: `1594502.182669` |
| `data.current_batch_id` | number | No | Example: `13` |
| `data.next_settlement_date` | string | No | Example: `2025-10-06` |
