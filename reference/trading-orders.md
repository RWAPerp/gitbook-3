# Trading and orders

| Method | Path | Auth |
|--------|------|------|
| DELETE | [`/v1/algo/client/order`](endpoints/delete-v1-algo-client-order.md) | RWA |
| GET | [`/v1/algo/client/order/{client_order_id}`](endpoints/get-v1-algo-client-order-client-order-id.md) | RWA |
| DELETE | [`/v1/algo/order`](endpoints/delete-v1-algo-order.md) | RWA |
| POST | [`/v1/algo/order`](endpoints/post-v1-algo-order.md) | RWA |
| PUT | [`/v1/algo/order`](endpoints/put-v1-algo-order.md) | RWA |
| GET | [`/v1/algo/order/{order_id}`](endpoints/get-v1-algo-order-order-id.md) | RWA |
| GET | [`/v1/algo/order/{order_id}/trades`](endpoints/get-v1-algo-order-order-id-trades.md) | RWA |
| DELETE | [`/v1/algo/orders`](endpoints/delete-v1-algo-orders.md) | RWA |
| GET | [`/v1/algo/orders`](endpoints/get-v1-algo-orders.md) | RWA |
| DELETE | [`/v1/batch-order`](endpoints/delete-v1-batch-order.md) | RWA (`trading` scope) |
| POST | [`/v1/batch-order`](endpoints/post-v1-batch-order.md) | RWA (`trading` scope) |
| DELETE | [`/v1/client/batch-order`](endpoints/delete-v1-client-batch-order.md) | RWA (`trading` scope) |
| DELETE | [`/v1/client/order`](endpoints/delete-v1-client-order.md) | RWA (`trading` scope) |
| GET | [`/v1/client/order/{client_order_id}`](endpoints/get-v1-client-order-client-order-id.md) | RWA |
| GET | [`/v1/client/orderly_key_ip_restriction`](endpoints/get-v1-client-orderly-key-ip-restriction.md) | RWA |
| POST | [`/v1/client/reset_orderly_key_ip_restriction`](endpoints/post-v1-client-reset-orderly-key-ip-restriction.md) | RWA |
| POST | [`/v1/client/set_orderly_key_ip_restriction`](endpoints/post-v1-client-set-orderly-key-ip-restriction.md) | RWA |
| DELETE | [`/v1/order`](endpoints/delete-v1-order.md) | RWA (`trading` scope) |
| POST | [`/v1/order`](endpoints/post-v1-order.md) | RWA (`trading` scope) |
| PUT | [`/v1/order`](endpoints/put-v1-order.md) | RWA (`trading` scope) |
| POST | [`/v1/order/cancel_all_after`](endpoints/post-v1-order-cancel-all-after.md) | RWA |
| GET | [`/v1/order/{order_id}`](endpoints/get-v1-order-order-id.md) | RWA |
| GET | [`/v1/order/{order_id}/trades`](endpoints/get-v1-order-order-id-trades.md) | RWA |
| GET | [`/v1/orderbook/{symbol}`](endpoints/get-v1-orderbook-symbol.md) | RWA |
| DELETE | [`/v1/orders`](endpoints/delete-v1-orders.md) | RWA (`trading` scope) |
| GET | [`/v1/orders`](endpoints/get-v1-orders.md) | RWA |
| GET | [`/v1/trade/{trade_id}`](endpoints/get-v1-trade-trade-id.md) | RWA |
| GET | [`/v1/trades`](endpoints/get-v1-trades.md) | RWA |
