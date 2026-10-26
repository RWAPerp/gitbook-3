# Get one position info

`GET /v1/position/{symbol}`

**Authentication:** RWA

**Rate limit:** 30 requests per 10 second per user

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | path | string | Yes | — |
| `margin_mode` | query | string | No | Default: `CROSS`. Supported values: `CROSS`/`ISOLATED` |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/position/{symbol}{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.IMR_withdraw_orders` | number | No | Example: `0.1` |
| `data.MMR_with_orders` | number | No | Example: `0.05` |
| `data.average_open_price` | number | No | Example: `27908.14386047` |
| `data.cost_position` | number | No | Example: `-139329.358492` |
| `data.est_liq_price` | number | No | Example: `117335.92899428` |
| `data.fee_24_h` | number | No | Example: `0` |
| `data.imr` | number | No | Example: `0.1` |
| `data.last_sum_unitary_funding` | number | No | Example: `70.38` |
| `data.mark_price` | number | No | Example: `27794.9` |
| `data.mmr` | number | No | Example: `0.05` |
| `data.pending_long_qty` | number | No | Example: `0` |
| `data.pending_short_qty` | number | No | Example: `0` |
| `data.pnl_24_h` | number | No | Example: `0` |
| `data.position_qty` | number | No | Example: `-5` |
| `data.settle_price` | number | No | Example: `27865.8716984` |
| `data.symbol` | string | No | Example: `PERP_BTC_USDC` |
| `data.seq` | number | No | Example: `1730181536341943600` |
| `data.timestamp` | number | No | The timestamp when the position is created for the entry Example: `1685429350571` |
| `data.updated_time` | number | No | Example: `1685429350571` |
| `data.unsettled_pnl` | number | No | Example: `354.858492` |
| `data.leverage` | integer | No | Example: `10` |
| `data.margin_mode` | string | No | Example: `CROSS` |
| `data.margin` | number | No | Example: `0` |
| `data.accrued_funding_fee` | number | No | Example: `0.005202` |
