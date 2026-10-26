# Get user statistics

`GET /v1/client/statistics`

**Authentication:** RWA

**Rate limit:** 10 requests per 60 seconds

## Description

Returns trading activity and fee statistics for the authenticated account.

## Parameters

No fields are defined in the published schema.

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/statistics{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.days_since_registration` | integer | Yes | Number of days since the account was registered. Example: `109` |
| `data.fees_paid_last_30_days` | number | Yes | Total fees paid across all markets during the last 30 days. Example: `0` |
| `data.perp_fees_paid_last_30_days` | number | Yes | Total perpetual futures fees paid during the last 30 days. Example: `0` |
| `data.perp_trading_volume_last_24_hours` | number | Yes | Perpetual futures trading volume during the last 24 hours. Example: `0` |
| `data.perp_trading_volume_last_7_days` | number | No | Perpetual futures trading volume during the last 7 days. Example: `0` |
| `data.perp_trading_volume_last_30_days` | number | Yes | Perpetual futures trading volume during the last 30 days. Example: `0` |
| `data.perp_trading_volume_ytd` | number | Yes | Perpetual futures trading volume year to date. Example: `0` |
| `data.perp_trading_volume_ltd` | number | No | Perpetual futures trading volume since account registration. Example: `0` |
| `data.trading_volume_last_24_hours` | number | Yes | Total trading volume during the last 24 hours. Example: `0` |
| `data.trading_volume_last_30_days` | number | Yes | Total trading volume during the last 30 days. Example: `0` |
| `data.trading_volume_ytd` | number | Yes | Total trading volume year to date. Example: `459.7436` |
