# Get account information

`GET /v1/client/info`

**Authentication:** RWA

**Rate limit:** 10 requests per 60 seconds

## Description

Returns account configuration details for the authenticated account, including fee rates and leverage settings.

## Parameters

No fields are defined in the published schema.

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/client/info{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.account_id` | string | Yes | Account ID of the authenticated account. |
| `data.email` | string | Yes | Email address bound to the account, when available. Example: `test@test.com` |
| `data.account_mode` | string | Yes | Account mode enabled for the account. Example: `FUTURES` |
| `data.max_leverage` | number | Yes | Maximum leverage available to the account. Example: `20` |
| `data.taker_fee_rate` | number | Yes | Taker fee rate applied to standard markets. Example: `0` |
| `data.maker_fee_rate` | number | Yes | Maker fee rate applied to standard markets. Example: `0` |
| `data.rwa_taker_fee_rate` | number | No | Taker fee rate applied to RWA markets. Example: `0` |
| `data.rwa_maker_fee_rate` | number | No | Maker fee rate applied to RWA markets. Example: `0` |
| `data.futures_taker_fee_rate` | number | Yes | Taker fee rate applied to perpetual futures markets. Example: `0` |
| `data.futures_maker_fee_rate` | number | Yes | Maker fee rate applied to perpetual futures markets. Example: `0` |
| `data.maintenance_cancel_orders` | boolean | Yes | Whether pending orders are automatically canceled during maintenance. Example: `True` |
| `data.imr_factor` | object | Yes | Initial margin ratio factor configured for each symbol. Example: `{'PERP_BTC_USDC': 9.1e-08, 'PERP_ETH_USDC': 1.2345e-06}` |
| `data.max_notional` | object | No | Maximum notional value allowed for each symbol. Example: `{'PERP_BTC_USDC': 10000000, 'PERP_ETH_USDC': 2000000}` |
