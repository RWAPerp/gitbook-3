# Get all trades of specific order

`GET /v1/order/{order_id}/trades`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second

| Base | URL |
|------|-----|
| Default REST | `https://api-trade.rwaperp.xyz` |
| VIP REST | `https://api-vip.rwaperp.xyz` |

Same path, same `RWA-*` signing on both hosts. Prefer VIP when your integration is provisioned for the dedicated REST endpoint. **To-B partners:** contact RWA Perp to obtain a dedicated Base URL before using `api-trade`, `api-vip`, or any custom host.

## Description

Get specific trades of an order by `order_id`.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `order_id` | path | number | Yes | — |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/order/{order_id}/trades{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | — |
| `data.rows[].id` | number | No | Example: `2` |
| `data.rows[].symbol` | string | No | Example: `PERP_BTC_USDC` |
| `data.rows[].fee` | number | No | Total per-execution fee, including `order_enum_fee` when present. Subtract `order_enum_fee` to derive the non-enum trade fee. Example: `0.0001` |
| `data.rows[].fee_asset` | string | No | fee. use Base as unit when BUY, use Quote as unit when SELL Example: `USDC` |
| `data.rows[].side` | string | No | Example: `BUY` |
| `data.rows[].order_id` | number | No | Example: `1` |
| `data.rows[].executed_price` | number | No | Example: `123` |
| `data.rows[].executed_quantity` | number | No | Example: `0.05` |
| `data.rows[].executed_timestamp` | number | No | Example: `1567382401000` |
| `data.rows[].is_maker` | number | No | Example: `1` |
| `data.rows[].realized_pnl` | number | No | Example: `0.0` |
| `data.rows[].match_id` | number | No | Example: `1773456866666462000` |
| `data.rows[].margin_token` | string | No | Example: `USDC` |
| `data.rows[].margin_change_qty` | number | No | Example: `0` |
| `data.rows[].margin_mode` | string | No | Example: `CROSS` |
| `data.rows[].order_enum_fee` | number | No | Additional per-execution fee paid in full to the fee-owning broker, in `fee_asset` units. Exclude this amount from executing-builder and affiliate fee-share calculations. Example: `0.05` |
| `data.rows[].order_enum_fee_rate` | number | No | Custom trading fee rate applied at execution time. Subtract this value from the trade fee rate to derive the effective rate excluding the custom fee. Example: `0.005` |
