# Get announcements

`GET /v1/public/announcement`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

**Legacy endpoint.** For the current announcement format, use [Get announcements (v2)](/build-on-omnichain/restful-api/public/get-announcements-v2).

Returns active platform announcements published by RWA Perp.

## Parameters

No fields are defined in the published schema.

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.rows` | array<object> | Yes | Active platform announcements. |
| `data.rows[].announcement_id` | number | No | Unique ID of the announcement. Example: `1` |
| `data.rows[].message` | string | No | Announcement message shown to users. Example: `Position information is incorrect due to a 1-minute delay.` |
| `data.rows[].url` | string | No | Optional link with more details about the announcement. Example: `https://api-trade.rwaperp.xyz |
