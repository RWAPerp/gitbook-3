# Get account overview info

`GET /v1/account_info`

**Authentication:** RWA

**Rate limit:** 10 requests per 1 second per user

## Description

Returns account-level collateral, margin, and PnL overview metrics for the authenticated account.

## Parameters

No fields are defined in the published schema.

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/account_info{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.current_margin_ratio_with_orders` | number | Yes | Current margin ratio after accounting for open orders. Example: `1.2385` |
| `data.free_collateral` | number | Yes | Collateral currently available under the current account state. Example: `450315.09115` |
| `data.initial_margin_ratio` | number | Yes | Current initial margin ratio of the account. Example: `0.1` |
| `data.initial_margin_ratio_with_orders` | number | Yes | Initial margin ratio after accounting for open orders. Example: `0.1` |
| `data.maintenance_margin_ratio` | number | Yes | Current maintenance margin ratio of the account. Example: `0.05` |
| `data.maintenance_margin_ratio_with_orders` | number | Yes | Maintenance margin ratio after accounting for open orders. Example: `0.05` |
| `data.margin_ratio` | number | Yes | Current account margin ratio. Example: `1.2385` |
| `data.open_margin_ratio` | number | Yes | Margin ratio based on open positions only. Example: `1.2102` |
| `data.total_collateral_value` | number | Yes | Total collateral value across the account. Example: `489865.71329` |
| `data.account_value` | number | Yes | Total account value including collateral and PnL. Example: `500000` |
| `data.total_pnl_24h` | number | Yes | Total profit and loss over the last 24 hours. Example: `0` |
