# Get builder volume

`GET /v1/public/volume/stats`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Returns the latest trading volume statistics for RWA Perp and its associated builders. For a specific builder, volume is calculated as maker volume plus taker volume. Platform-wide volume counts each matched trade once.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `broker_id` | query | string | No | Filter results to a specific broker ID. |

## Responses

### HTTP 200

Success

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
