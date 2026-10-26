# Get system maintenance status

`GET /v1/public/system_info`

**Authentication:** None

**Rate limit:** 1 request per 1 second per IP address

## Description

Returns the current system status for RWA Perp. `status = 0` indicates normal operation. `status = 2` indicates maintenance mode.

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
| `data.status` | number | Yes | System status code. `0` means normal operation and `2` means maintenance mode. Example: `0` |
| `data.scheduled_maintenance` | object | No | Scheduled maintenance window, when available. |
| `data.scheduled_maintenance.startTime` | number | No | Scheduled maintenance start time in milliseconds. Example: `1618822380000` |
| `data.scheduled_maintenance.endTime` | number | No | Scheduled maintenance end time in milliseconds. Example: `1618822440000` |
| `data.msg` | string | Yes | Human-readable status message. |
