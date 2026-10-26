# Get valor2 revenue buyback

`GET /v1/staking/valor2/revenue_buyback`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

Order by batch_id. Display the amount after the batch is claimable.

## Parameters

No fields are defined in the published schema.

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | array<object> | No | Order by batch_id. Display the amount after the batch is claimable. |
| `data[].batch_id` | number | No | Example: `13` |
| `data[].usdc_revenue` | number | No | Example: `19090` |
| `data[].esorder_amount` | number | No | Example: `90000000` |
