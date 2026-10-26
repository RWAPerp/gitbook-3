# Update leverage setting

`POST /v1/client/leverages`

**Authentication:** RWA

**Rate limit:** 5 requests per 60 second per user

## Description

Update leverage settings. This endpoint supports two modes:

**Single symbol mode:** When `symbol` is provided, update leverage for that specific symbol.

**Batch mode:** When `symbol` is omitted, set leverage for all symbols in a single atomic operation. Each symbol's new leverage will be adjusted to `min(requested_leverage, symbol_max_leverage)`.

For example, if BTC max leverage is 100, ETH max leverage is 100, and NEAR max leverage is 10, and the user requests leverage = 20, the result will be: BTC = 20, ETH = 20, NEAR = 10.

Batch update behavior with margin modes:
- **Cross margin symbols:** A margin check is performed assuming all cross-margin symbols are updated to the new leverage. Either all cross-margin symbol leverages are updated successfully, or none are updated.
- **Isolated margin symbols:** The leverage update will only apply to symbols with no active isolated positions or pending orders. The update for isolated margin symbols will always go through for eligible symbols.

Validation Logic:

1. Check the leverage range is eligible

2. Check if the position notional under the updated leverage is acceptable
   - `max_notional = (1 / (symbol_leverage * imr_factor)) ^ (1/0.8)`
   - `symbol_leverage_max = round down to int → min(1 / (imr_factor * notional ^ 0.8), 1/base_imr)`

3. Check if the margin is enough

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `symbol` | body | string | No | Example: `PERP_BTC_USDC` |
| `leverage` | body | integer | Yes | Integer between 1 to 100 |
| `margin_mode` | body | string | No | Default: `CROSS`. Margin mode for the leverage update. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/client/leverages{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | No | — |
| `data.symbol` | string | No | Trading symbol for the leverage setting. Example: `PERP_BTC_USDC` |
| `data.margin_mode` | string | No | Margin mode for the returned leverage setting. Example: `ISOLATED` |
| `data.leverage` | integer | No | Configured leverage value for the symbol. Example: `19` |
