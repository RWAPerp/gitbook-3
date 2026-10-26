# Get staking overview

`GET /v1/staking/overview`

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
| `data.total_stake` | number | No | Example: `845599630.06` |
| `data.rows` | array<object> | No | — |
| `data.rows[].date` | string | No | Example: `2023-05-20` |
| `data.rows[].usd_reward` | number | No | Example: `1268.34` |
| `data.rows[].total_staked_usd` | number | No | Example: `117654321.99` |
