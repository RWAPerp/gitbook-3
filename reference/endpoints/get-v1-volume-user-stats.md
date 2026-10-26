# Get user volume statistics

`GET /v1/volume/user/stats`

**Authentication:** RWA

**Rate limit:** See platform limits

## Description

**Limit 10 requests per 60 seconds**

Returns cumulative trading volume statistics for the authenticated account.

## Parameters

No fields are defined in the published schema.

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/volume/user/stats{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.perp_volume_ytd` | number | No | Perpetual trading volume year to date for the selected scope. Example: `274148.0364` |
| `data.perp_volume_ltd` | number | No | Perpetual trading volume since launch for the selected scope. Example: `274148.0364` |
| `data.perp_volume_today` | number | No | Perpetual trading volume since 00:00 UTC for the selected scope. Example: `120272.7674` |
| `data.perp_volume_last_1_day` | number | No | Perpetual trading volume over the last 24 hours for the selected scope. Example: `120272.7674` |
| `data.perp_volume_last_7_days` | number | No | Perpetual trading volume over the last 7 days for the selected scope. Example: `120272.7674` |
| `data.perp_volume_last_30_days` | number | No | Perpetual trading volume over the last 30 days for the selected scope. Example: `300730.5454` |
