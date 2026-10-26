# List order tags for a broker

`GET /v1/public/broker/order_enums`

**Authentication:** None

**Rate limit:** 10 requests per 1 second per IP address

## Description

`GET /v1/public/broker/order_enums?broker_id={broker_id}`

List custom trading fee configurations owned by `broker_id`. Returned `enum_id` values are unprefixed.

To submit a new enum-tagged order, combine the queried owner and returned ID as `enum:<broker_id>:<enum_id>`.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `broker_id` | query | string | Yes | Broker that owns the enum configurations |
| `symbol` | query | string | No | Filter by symbol |
| `enum_id` | query | string | No | Filter by unprefixed enum ID |
| `include_archived` | query | boolean | No | Include archived fee configurations |

## Responses

### HTTP 200

Success

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | array<object> | No | — |
| `data[].enum_id` | string | No | Unprefixed enum ID. Combine it with the enum owner's broker ID as `enum:<owner_broker_id>:<enum_id>` when submitting a new order. Example: `GRID_PRO` |
| `data[].name` | string | No | Example: `Grid Pro` |
| `data[].description` | string | No | Example: `Grid strategy orders` |
| `data[].status` | string | No | Example: `active` |
| `data[].default_fee_rate` | number | No | Default enum fee rate used when the order symbol has no pair override. Example: `0.005` |
| `data[].pair_overrides` | object | No | Symbol-specific enum fee rates that override `default_fee_rate`. Example: `{'PERP_BTC_USDC': 0.003}` |
| `data[].created_time` | number | No | Example: `1710300000000` |
| `data[].updated_time` | number | No | Example: `1710300000000` |
