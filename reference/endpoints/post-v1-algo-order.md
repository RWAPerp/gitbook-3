# Create algo order

`POST /v1/algo/order`

**Authentication:** RWA

**Rate limit:** 1 request per 1 second

| Base | URL |
|------|-----|
| Default REST | `https://api-trade.rwaperp.xyz` |
| VIP REST | `https://api-vip.rwaperp.xyz` |

Same path, same `RWA-*` signing on both hosts. Prefer VIP when your integration is provisioned for the dedicated REST endpoint. **To-B partners:** contact RWA Perp to obtain a dedicated Base URL before using `api-trade`, `api-vip`, or any custom host.

## Description

Place maker/taker order that requires an additional trigger for order execution such as stop orders.

`STOP` type order bahavior: an order to buy or sell at the market/limit price once the asset has traded at or through a specified price (the "stop price"). If the asset reaches the stop price, the order becomes a market order and is filled at the next available market price.

To place `Positional TP/SL` order, the input fields is 2 layer and includes an array of the objects named childOrder. The take-profit or stop-loss order should be the objects in the array. For the sub-order in childOrder, please input `CLOSE_POSITION` as type, and `TAKE_PROFIT` or `STOP_LOSS` in algoType field.
To place `Trailing Stop` order, please use `TRAILING_STOP` as algoType and `MARKET` as type. Please also input your trailing rate setting in callbackRate field.

Sample request can be found [here](/docs/build-on-omnichain/user-flows/algo-order-samples)

Note: This endpoint requires trading scope in API key.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `x-recv-window` | header | number | No | Use this parameter to control the timeout threshold for placing order, unit in miliseconds |
| `symbol` | body | string | Yes | — |
| `algo_type` | body | string | Yes | `STOP`/`TP_SL`/`POSITIONAL_TP_SL`/`BRACKET`/`BRACKET + TP_SL`/`TRAILING_STOP` |
| `client_order_id` | body | string | No | 36 length, accepts hyphen but cannot be the first character, default: null |
| `type` | body | string | Yes | `LIMIT` / `MARKET`, required if `algo_type` = `STOP` |
| `price` | body | number | No | Optional for `TP_SL` and `POSTIONAL_TP_SL` |
| `quantity` | body | number | Yes | For `MARKET`/`ASK`/`BID` order, if order_amount is given, it is not required. Not required if type is `POSITIONAL_TP_SL`. |
| `trigger_price_type` | body | string | No | Only `MARK_PRICE` is available for now. |
| `trigger_price` | body | number | No | — |
| `reduce_only` | body | boolean | No | — |
| `visible_quantity` | body | boolean | No | Default false |
| `side` | body | string | Yes | `SELL`/`BUY`, required if `STOP` type |
| `order_tag` | body | string | No | Optional tag for the order. Supports two formats:
- Referral code: plain string (e.g., `REFERRAL2026`) - overrides referral relationship
- Custom trading fee: `enum:<owning_broker_id>:<enum_id>` (e.g., `enum:broker_b:GRID_PRO`) - adds the custom fee and preserves the existing referral relationship
New custom-fee-tagged orders must use the current three-segment format. Legacy `enum:<enum_id>` tags are supported only on orders accepted before cutover.
Maximum length: 128 characters. Cannot be modified after order placement.
 Example: `enum:broker_b:GRID_PRO` |
| `child_orders` | body | array<object> | Yes | — |
| `child_orders[].symbol` | body | string | No | — |
| `child_orders[].algo_type` | body | string | No | — |
| `child_orders[].child_orders` | body | array<object> | No | Array of `CreateAlgoOrderChildRequest` |
| `child_orders[].child_orders[].symbol` | body | string | No | — |
| `child_orders[].child_orders[].algo_type` | body | string | No | — |
| `child_orders[].child_orders[].side` | body | string | No | — |
| `child_orders[].child_orders[].type` | body | string | No | — |
| `child_orders[].child_orders[].trigger_price` | body | number | No | — |
| `child_orders[].child_orders[].price` | body | number | No | — |
| `child_orders[].child_orders[].reduce_only` | body | boolean | No | — |
| `child_orders[].child_orders[].trigger_price_type` | body | string | No | — |
| `activatedPrice` | body | string | No | Activated price for algoType=`TRAILING_STOP` |
| `callbackRate` | body | string | No | Callback rate, only for algoType=`TRAILING_STOP`, i.e. the value = 0.1 represent to 10%. |
| `callbackValue` | body | string | No | Callback value, only for algoType=`TRAILING_STOP`, i.e. the value = 100 |
| `margin_mode` | body | string | No | Margin mode for the order. Default: the symbol's current default margin mode. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/algo/order{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.order_id` | number | Yes | Example: `13` |
| `data.client_order_id` | string | Yes | Example: `testclientid` |
| `data.algo_type` | string | Yes | Example: `STOP` |
| `data.quantity` | number | Yes | Example: `100.12` |
