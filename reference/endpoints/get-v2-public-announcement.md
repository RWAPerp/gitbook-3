# Get announcements (v2)

`GET /v2/public/announcement`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

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
| `timestamp` | integer | Yes | Time the response was generated, as a Unix timestamp in milliseconds. Example: `1789430400000` |
| `data` | object | Yes | — |
| `data.last_updated_time` | integer | Yes | Latest announcement update time retrieved by the backend, as a Unix timestamp in milliseconds. Not necessarily the maximum updated_time in the returned rows. Example: `1789426800000` |
| `data.rows` | array<object> | Yes | Currently active announcements. Returns an empty array when there are no active announcements. |
| `data.rows[].announcement_id` | integer | Yes | Unique ID of the announcement. Example: `12345` |
| `data.rows[].message` | string | Yes | Main announcement text in any language. Use as a fallback in its provided language when a translation is missing. Example: `Community voting is now open.` |
| `data.rows[].url` | string | Yes | Destination link for the announcement, or null. Example: `https://example.com/vote` |
| `data.rows[].i18n` | object | Yes | Translations for five fixed locales only (zh, es, fr, jp, ko). Values can be null. The Japanese key is jp. |
| `data.rows[].i18n.zh` | string | Yes | Chinese translation. Example: `社群投票現已開放。` |
| `data.rows[].i18n.es` | string | Yes | Spanish translation. |
| `data.rows[].i18n.fr` | string | Yes | French translation. |
| `data.rows[].i18n.jp` | string | Yes | Japanese translation. |
| `data.rows[].i18n.ko` | string | Yes | Korean translation. |
| `data.rows[].type` | string | Yes | Announcement category, or null. Example: `VOTE` |
| `data.rows[].updated_time` | integer | Yes | Time the announcement was updated, as a Unix timestamp in milliseconds. Example: `1789426800000` |
