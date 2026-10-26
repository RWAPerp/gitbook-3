# Get user daily volume

`GET /v1/volume/user/daily`

**Authentication:** RWA

**Rate limit:** See platform limits

## Description

**Limit 10 requests per 60 seconds**

Returns the authenticated account's daily perpetual trading volume for the requested date range.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `start_date` | query | string | Yes | Start date in `YYYY-MM-DD` format. |
| `end_date` | query | string | Yes | End date in `YYYY-MM-DD` format. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}GET/v1/volume/user/daily{body}` → URL-safe Base64 without trailing `=` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | array<object> | Yes | Daily perpetual trading volume entries for the requested date range. |
| `data[].date` | string | Yes | Date of the reported volume in `YYYY-MM-DD` format. Example: `2024-01-01` |
| `data[].perp_volume` | number | Yes | Perpetual futures trading volume for the date. Example: `100.24` |
