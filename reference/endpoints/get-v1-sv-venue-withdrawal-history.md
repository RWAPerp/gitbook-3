# Get fund outflow allocation

`GET /v1/sv/venue_withdrawal_history`

**Authentication:** None

**Rate limit:** 10 requests per second per account

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `period_number` | query | number | No | — |
| `page` | query | number | No | the page you wish to query start from 1 |
| `size` | query | number | No | the page size you wish to query (max: 500) |

## Responses

### HTTP 200

Success

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | No | — |
| `data.meta` | object | No | — |
| `data.meta.total` | number | No | Example: `2` |
| `data.meta.records_per_page` | number | No | Example: `25` |
| `data.meta.current_page` | number | No | start from 1 Example: `1` |
| `data.rows` | array<object> | No | — |
| `data.rows[].created_time` | number | No | Example: `1739257260000` |
| `data.rows[].period_number` | number | No | Example: `2` |
| `data.rows[].plan_id` | number | No | Example: `4` |
| `data.rows[].schedule_time` | number | No | Example: `1739268000000` |
| `data.rows[].executed_time` | number | No | — |
| `data.rows[].trigger_by` | number | No | — |
| `data.rows[].amount` | number | No | Example: `13633.532389` |
| `data.rows[].status` | string | No | Example: `pending` |
