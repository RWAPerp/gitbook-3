# Get trade

`GET /v1/trade/{trade_id}`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second

## Description

Get specific transaction details by `trade_id`.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `trade_id` | path | number | Yes | id of the trade |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/trade/{trade_id}{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.id` | number | No | Example: `2` |
| `data.symbol` | string | No | Example: `PERP_BTC_USDC` |
| `data.fee` | number | No | Total per-execution fee, including `order_enum_fee` when present. Subtract `order_enum_fee` to derive the non-enum trade fee. Example: `0.0001` |
| `data.fee_asset` | string | No | fee. use Base as unit when BUY, use Quote as unit when SELL Example: `USDC` |
| `data.side` | string | No | Example: `BUY` |
| `data.order_id` | number | No | Example: `1` |
| `data.executed_price` | number | No | Example: `123` |
| `data.executed_quantity` | number | No | Example: `0.05` |
| `data.executed_timestamp` | number | No | Example: `1567382401000` |
| `data.is_maker` | number | No | Example: `1` |
| `data.realized_pnl` | number | No | Example: `0.0` |
| `data.match_id` | number | No | Example: `1773456866666462000` |
| `data.margin_token` | string | No | Example: `USDC` |
| `data.margin_change_qty` | number | No | Example: `0` |
| `data.margin_mode` | string | No | Example: `CROSS` |
| `data.order_enum_fee` | number | No | Additional per-execution fee paid in full to the fee-owning broker, in `fee_asset` units. Exclude this amount from executing-builder and affiliate fee-share calculations. Example: `0.05` |
| `data.order_enum_fee_rate` | number | No | Custom trading fee rate applied at execution time. Subtract this value from the trade fee rate to derive the effective rate excluding the custom fee. Example: `0.005` |
