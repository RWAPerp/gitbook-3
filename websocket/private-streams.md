# Private streams

**Request** (build the URL with `private_ws_url()` from [Request signing](../authentication/request-signing.md))

```json
{"event":"subscribe","topic":"executionreport"}
```

**Response**

Subscription acknowledgment:

```json
{"event":"subscribe","success":true,"ts":1781628477334}
```

Execution report:

```json
{"topic":"executionreport","ts":1781628478000,"data":{"order_id":123456789,"status":"NEW","symbol":"PERP_ETH_USDC","side":"BUY","price":888.53,"quantity":0.0114}}
```

On receiving `{"event":"ping"}` you must reply `{"event":"pong"}`.
