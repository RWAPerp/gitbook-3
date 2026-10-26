# Get tradingview localized config info

`GET /v1/tv/config`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `locale` | query | string | Yes | — |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `s` | string | Yes | — |
| `d` | object | Yes | — |
| `d.accountSummaryRow` | array<object> | Yes | — |
| `d.accountSummaryRow[].id` | string | Yes | — |
| `d.accountSummaryRow[].title` | string | Yes | — |
| `d.accountManager` | array<object> | Yes | — |
| `d.accountManager[].id` | string | No | — |
| `d.accountManager[].title` | string | No | — |
| `d.accountManager[].columns` | array<object> | No | — |
| `d.accountManager[].columns[].id` | string | Yes | — |
| `d.accountManager[].columns[].title` | string | Yes | — |
| `d.durations` | array<object> | Yes | — |
| `d.durations[].id` | string | No | — |
| `d.durations[].title` | string | No | — |
| `d.durations[].hasDatePicker` | boolean | No | — |
| `d.durations[].hasTimePicker` | boolean | No | — |
| `d.durations[].default` | boolean | No | — |
| `d.durations[].supportedOrderTypes` | array<string> | No | — |
| `d.orderCustomFields` | array<object> | Yes | — |
| `d.orderCustomFields[].id` | string | No | — |
| `d.orderCustomFields[].title` | string | No | — |
| `d.orderCustomFields[].tooltip` | string | No | — |
| `d.orderCustomFields[].alignment` | string | No | — |
| `d.orderHistoryCustomFields` | array<object> | Yes | — |
| `d.orderHistoryCustomFields[].id` | string | No | — |
| `d.orderHistoryCustomFields[].title` | string | No | — |
| `d.orderHistoryCustomFields[].tooltip` | string | No | — |
| `d.orderHistoryCustomFields[].alignment` | string | No | — |
| `d.positionCustomFields` | array<object> | Yes | — |
| `d.positionCustomFields[].id` | string | Yes | — |
| `d.positionCustomFields[].title` | string | Yes | — |
| `d.positionCustomFields[].tooltip` | string | Yes | — |
| `d.positionCustomFields[].alignment` | string | Yes | — |
| `d.pullingInterval` | object | Yes | — |
| `d.pullingInterval.quotes` | integer | Yes | — |
| `d.pullingInterval.orders` | integer | Yes | — |
| `d.pullingInterval.positions` | integer | Yes | — |
| `d.pullingInterval.accountManager` | integer | Yes | — |
| `d.pullingInterval.balances` | integer | Yes | — |
