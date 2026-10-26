# Get valor2 batch info

`GET /v1/staking/valor2/batch_info`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Parameters

No fields are defined in the published schema.

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | No | — |
| `data.rows` | array<object> | No | — |
| `data.rows[].batch_id` | number | No | Example: `1` |
| `data.rows[].batch_start_time` | number | No | Example: `1684502400000` |
| `data.rows[].batch_end_time` | number | No | Example: `1684588800000` |
