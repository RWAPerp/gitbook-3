# Claim liquidated positions

`POST /v1/liquidation`

**Authentication:** RWA

**Rate limit:** 5 requests per 1 second

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `liquidation_id` | body | integer | Yes | — |
| `ratio_qty_request` | body | integer | Yes | — |
| `extra_liquidation_ratio` | body | integer | No | — |
| `limit_price` | body | object | Yes | Liquidator’s instruction to let the system reject the liquidation claim if the following condition applies: if position_qty > 0, reject if mark_price > limit_price; if position_qty < 0, reject if mark_price < limit_price |
| `limit_price.symbol` | body | number | Yes | The limit price for each symbol in the liquidation claim |
| `symbols` | body | object | No | For high risk tiers only |
| `symbols.ratio_qty_request` | body | number | Yes | Field dedicated to high risk symbols liquidations type only (symbols with liquidation tier = 2), where a liquidator can specific the ratio he wish to liquidates per symbol |
| `symbols.symbol` | body | string | Yes | Only relevant if this is a liquidation of type high tier (symbols with liquidation tier = 2) |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/liquidation{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.liquidation_id` | integer | Yes | — |
| `data.timestamp` | number | Yes | — |
| `data.type` | string | Yes | OR "claim" |
| `data.positions_by_perp` | array<object> | Yes | — |
| `data.positions_by_perp[].symbol` | string | No | Example: `PERP_BTC_USDC` |
| `data.positions_by_perp[].abs_liquidator_fee` | number | No | Example: `1.152279` |
| `data.positions_by_perp[].cost_position_transfer` | number | No | Example: `21.002786` |
| `data.positions_by_perp[].liquidator_fee` | number | No | Example: `0.006` |
| `data.positions_by_perp[].position_qty` | number | No | Example: `0.00017` |
| `data.positions_by_perp[].transfer_price` | number | No | Example: `123545.8` |
