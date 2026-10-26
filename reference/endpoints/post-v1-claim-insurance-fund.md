# Claim insurance fund

`POST /v1/claim_insurance_fund`

**Authentication:** RWA

**Rate limit:** 5 requests per 1 second

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `claim_id` | body | number | Yes | — |
| `symbol` | body | string | Yes | — |
| `qty_request` | body | number | Yes | Quantity to be claimed from insurance fund |
| `limit_price` | body | object | No | Liquidator’s instruction to let the system reject the liquidation claim if the following condition applies: if position_qty > 0, reject if mark_price > limit_price; if position_qty < 0, reject if mark_price < limit_price |
| `limit_price.symbol` | body | number | Yes | The limit price for each symbol in the liquidation claim |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/claim_insurance_fund{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.liquidation_id` | integer | Yes | Example: `101` |
| `data.timestamp` | integer | Yes | Example: `1663313562090` |
| `data.positions_by_perp` | array<object> | Yes | — |
| `data.positions_by_perp[].symbol` | string | No | Example: `PERP_BTC_USDC` |
| `data.positions_by_perp[].abs_liquidator_fee` | number | No | Example: `1.152279` |
| `data.positions_by_perp[].cost_position_transfer` | number | No | Example: `21.002786` |
| `data.positions_by_perp[].liquidator_fee` | number | No | Example: `0.006` |
| `data.positions_by_perp[].position_qty` | number | No | Example: `0.00017` |
| `data.positions_by_perp[].transfer_price` | number | No | Example: `123545.8` |
