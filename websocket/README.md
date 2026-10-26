# WebSocket overview

Use public streams for live market data and private streams for account and order updates.

| Type | Address |
|------|---------|
| Public WS | `wss://api-trade.rwaperp.xyz/ws/public/ws/stream/{account_id}` |
| Private WS | `wss://api-trade.rwaperp.xyz/ws/private/v2/ws/private/stream/{account_id}` |
| Same streams via VIP host | `wss://api-vip.rwaperp.xyz/ws/public/...` and `wss://api-vip.rwaperp.xyz/ws/private/...` |

The public WebSocket path parameter must be an `account_id` returned by `GET /v1/get_account`. Arbitrary session identifiers are not accepted. VIP and default hosts expose the same public and private streams. **To-B partners:** contact RWA Perp to obtain a dedicated Base URL before using these hosts.

## Subscribe

```json
{"event": "subscribe", "topic": "PERP_ETH_USDC@ticker"}
```

## Message formats

| Direction | Example |
|-----------|---------|
| Subscription acknowledgment | `{"event":"subscribe","success":true,"ts":...}` |
| Data push | `{"topic":"PERP_ETH_USDC@ticker","ts":...,"data":{...}}` |
| Heartbeat | On `{"event":"ping"}` → reply `{"event":"pong"}` |

## Public streams

Example ticker `data`:

```json
{"symbol":"PERP_ETH_USDC","open":1840.86,"close":1777.67,"high":1844.78,"low":1758.29,"volume":15117.5,"count":16769}
```

## Private streams

Build the connection URL with `private_ws_url()` from [Request signing](../authentication/request-signing.md).

| Topic | `data` highlights |
|-------|-------------------|
| `balance` / `position` / `account` | Balance, positions, account summary |
| `executionreport` | Order status updates; clients that place orders should subscribe to this topic and reconcile updates with REST queries. Fields include `order_id`, `status`, `side`, `price`, and `quantity` |
| `algoexecutionreportv2` | Algo order reports |
| `wallettransaction` / `pnlsettlement` | Deposits/withdrawals, settlement |

| Topic | Description |
|-------|-------------|
| `{symbol}@ticker` / `tickers` | Last price, 24h volume |
| `{symbol}@orderbook` | Full depth |
| `{symbol}@orderbookupdate` | Incremental depth |
| `{symbol}@trade` | Tick-by-tick trades |
| `{symbol}@markprice` / `{symbol}@indexprice` | Mark price / index price |
| `{symbol}@kline_{interval}` | Candles |
| `maintenance_status` | Maintenance status |
