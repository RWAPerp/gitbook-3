# Get funding rate for all markets

`GET /v1/public/market_info/funding_history`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

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
| `data.rows[].symbol` | string | No | Example: `PERP_BTC_USDC` |
| `data.rows[].data_start_time` | string | No | Example: `2022-01-01 00:00:00` |
| `data.rows[].funding` | object | No | — |
| `data.rows[].funding.last` | object | No | — |
| `data.rows[].funding.last.rate` | number | No | Example: `0.00234` |
| `data.rows[].funding.last.positive` | number | No | Example: `1` |
| `data.rows[].funding.last.negative` | number | No | Example: `0` |
| `data.rows[].funding.1d` | object | No | — |
| `data.rows[].funding.1d.rate` | number | No | Example: `-0.00828` |
| `data.rows[].funding.1d.positive` | number | No | Example: `10` |
| `data.rows[].funding.1d.negative` | number | No | Example: `10` |
| `data.rows[].funding.3d` | object | No | — |
| `data.rows[].funding.3d.rate` | number | No | Example: `-0.00412` |
| `data.rows[].funding.3d.positive` | number | No | Example: `9` |
| `data.rows[].funding.3d.negative` | number | No | Example: `11` |
| `data.rows[].funding.7d` | object | No | — |
| `data.rows[].funding.7d.rate` | number | No | Example: `0.00012` |
| `data.rows[].funding.7d.positive` | number | No | Example: `8` |
| `data.rows[].funding.7d.negative` | number | No | Example: `12` |
| `data.rows[].funding.14d` | object | No | — |
| `data.rows[].funding.14d.rate` | number | No | Example: `0.00156` |
| `data.rows[].funding.14d.positive` | number | No | Example: `7` |
| `data.rows[].funding.14d.negative` | number | No | Example: `13` |
| `data.rows[].funding.30d` | object | No | — |
| `data.rows[].funding.30d.rate` | number | No | Example: `0.00345` |
| `data.rows[].funding.30d.positive` | number | No | Example: `6` |
| `data.rows[].funding.30d.negative` | number | No | Example: `14` |
| `data.rows[].funding.90d` | object | No | — |
| `data.rows[].funding.90d.rate` | number | No | Example: `0.01023` |
| `data.rows[].funding.90d.positive` | number | No | Example: `5` |
| `data.rows[].funding.90d.negative` | number | No | Example: `15` |
| `data.rows[].funding.180d` | object | No | — |
| `data.rows[].funding.180d.rate` | number | No | Example: `0.01567` |
| `data.rows[].funding.180d.positive` | number | No | Example: `4` |
| `data.rows[].funding.180d.negative` | number | No | Example: `16` |
