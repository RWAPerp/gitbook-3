# Create order

`POST /v1/order`

**Authentication:** RWA (`trading` scope)

**Rate limit:** 10 requests per 1 second

| Base | URL |
|------|-----|
| Default REST | `https://api-trade.rwaperp.xyz` |
| VIP REST | `https://api-vip.rwaperp.xyz` |

Same path, same `RWA-*` signing on both hosts. Prefer VIP when your integration is provisioned for the dedicated REST endpoint. **To-B partners:** contact RWA Perp to obtain a dedicated Base URL before using `api-trade`, `api-vip`, or any custom host.

## Description

Place order maker/taker, the order executed information will be update from websocket stream.
will response immediately with an order created message.

`MARKET` type order behavior: it matches until the full size is executed. If the size is too large (larger than whole book) or the matching price exceeds the price limit (refer to `price_range`), then the remaining quantity will be cancelled.

`IOC` type order behavior: it matches as much as possible at the order_price. If not fully executed, then remaining quantity will be cancelled.

`FOK` type order behavior: if the order can be fully executed at the order_price then the order gets fully executed otherwise would be cancelled without any execution.

`POST_ONLY` type order behavior: if the order will be executed with any maker trades at the time of placement, then it will be cancelled without any execution. If a `POST_ONLY` order would match only with hidden quantity at the price level, the incoming `POST_ONLY` order is treated as the maker side for that execution and the resting hidden order is treated as the taker side.

`ASK` type order behavior: the order price is guranteed to be the best ask price of the orderbook at the time it gets accepted.

`BID` type order behavior: the order price is guranteed to be the best bid price of the orderbook at the time it gets accepted.

`visible_quantity` behavior: it sets the maximum quantity to be shown on orderbook. By default, it is equal to order_quantity, negative number and number larger than `order_quantity` is not allowed. If it sets to 0, the order would be hidden from the orderbook. It doesn't work for `MARKET`/`IOC`/`FOK` orders since orders with these types would be executed and cancelled immediately and not be shown on orderbook. For `LIMIT` order, as long as it's not complete, `visible_quantity` is the maximum quantity that shown on orderbook. When hidden quantity is matched by a new incoming order, the hidden side is marked as taker and charged the taker fee. If an order has both hidden and visible quantity, the hidden quantity is matched before the visible quantity.

`order_quantity` are provided. The precision of the number should be within 8 digits.

`client_order_id` behavior: customized order_id, a unique id among open orders. Orders with the same `client_order_id` can be accepted only when the previous one if completed, otherwise the order will be rejected.

Note: This endpoint requires `trading` scope in API key.

## Parameters

| Name | Location | Type | Required | Description |
|---|---|---|---|---|
| `x-recv-window` | header | number | No | Use this parameter to control the timeout threshold for placing order, unit in miliseconds |
| `symbol` | body | string | Yes | Example: `PERP_ETH_USDC` |
| `client_order_id` | body | string | No | 36 length, accepts hyphen but cannot be the first character, default: null |
| `order_type` | body | string | Yes | `LIMIT`/`MARKET`/`IOC`/`FOK`/`POST_ONLY`/`ASK`/`BID` |
| `order_price` | body | number | No | If order_type is MARKET/ASK/BID, then is not required, otherwise this parameter is required. |
| `order_quantity` | body | number | No | — |
| `order_amount` | body | number | No | For MARKET/ASK/BID order, the order size in terms of quote currency |
| `visible_quantity` | body | number | No | The order quantity shown on orderbook. (default: equal to order_quantity)
Visible quantity is not supported for post-only orders.
 |
| `side` | body | string | Yes | `SELL`/`BUY` |
| `reduce_only` | body | boolean | No | Default false |
| `slippage` | body | number | No | `MARKET` orders beyond this slippage will not be executed |
| `order_tag` | body | string | No | Optional tag for the order. Supports two formats:
- Referral code: plain string (e.g., `REFERRAL2026`) - overrides referral relationship
- Custom trading fee: `enum:<owning_broker_id>:<enum_id>` (e.g., `enum:broker_b:GRID_PRO`) - adds the custom fee and preserves the existing referral relationship
New custom-fee-tagged orders must use the current three-segment format. Legacy `enum:<enum_id>` tags are supported only on orders accepted before cutover.
Maximum length: 128 characters. Cannot be modified after order placement.
 Example: `enum:broker_b:GRID_PRO` |
| `level` | body | number | No | Integer value from `0` to `4`. This parameter controls wether to present the price of bid0 to bid4 or ask0 to ask4. Only allowed when `order_type` is `BID` or `ASK`. |
| `post_only_adjust` | body | boolean | No | If set to true, then price will be adjusted to 1 tick close to current best price. Only supported for `POST_ONLY` type orders |
| `margin_mode` | body | string | No | Margin mode for the order. Default: the symbol's current default margin mode. |

## Authentication headers

| Header | Required | Description |
|--------|----------|-------------|
| `RWA-Account-Id` | Yes | `account_id` |
| `RWA-Api-Key` | Yes | `ed25519:` + base58 public key |
| `RWA-Timestamp` | Yes | Millisecond timestamp |
| `RWA-Signature` | Yes | Ed25519 signature of `{timestamp}POST/v1/order{body}` → URL-safe Base64 without trailing `=` |
| `Content-Type` | Yes | `application/json` |

## Responses

### HTTP 200

OK

| Field | Type | Required | Description |
|---|---|---|---|
| `success` | boolean | Yes | Indicates whether the request was successful. Example: `True` |
| `timestamp` | integer | No | Server timestamp in milliseconds. Example: `1702989203989` |
| `data` | object | Yes | — |
| `data.order_id` | number | No | Example: `13` |
| `data.client_order_id` | string | No | Example: `testclientid` |
| `data.order_type` | string | No | Example: `LIMIT` |
| `data.order_price` | number | No | Example: `100.12` |
| `data.order_quantity` | number | No | Example: `0.987654` |
| `data.error_message` | string | No | Example: `none` |
