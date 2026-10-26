# Get valor pool info

`GET /v1/staking/valor/pool_info`

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
| `data.valor_price_usdc` | number | No | Example: `50` |
| `data.treasury_pool_value` | number | No | Example: `20000` |
| `data.next_settlement_date` | string | No | Example: `2024-06-15` |
| `data.revenue_rate` | number | No | Example: `0.6` |
| `data.est_treasury_inflow` | number | No | Example: `30000` |
| `data.total_redeemed_amount` | number | No | Example: `2000` |
