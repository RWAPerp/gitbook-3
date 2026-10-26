# Quick start

Complete [account onboarding](../authentication/onboarding.md) before running the trading example. The onboarding process creates the trading account and returns the API credentials required below.

> **Production environment:** Default REST is `https://api-trade.rwaperp.xyz`. If your integration is provisioned for VIP, use `https://api-vip.rwaperp.xyz` (same paths and `RWA-*` signing). **To-B partners:** contact RWA Perp to obtain a dedicated Base URL before using either host. The default command performs read-only queries. The `--with-order` option submits and cancels a real order using real account funds.

```bash
pip install eth-account base58 cryptography pynacl websocket-client
export RWA_ACCOUNT_ID="0x..."
export RWA_API_KEY="ed25519:..."
export RWA_SECRET_B58="..."
# Optional VIP host (To-B: contact RWA Perp for a dedicated Base URL first):
# export B2B_API_BASE="https://api-vip.rwaperp.xyz"
# After saving the trading example as trading-mainline.py:
python3 trading-mainline.py
python3 trading-mainline.py --with-order   # submits and cancels a real order; requires sufficient USDC
```

**Chain restriction: X Layer only (`chainId = 196`). No other chain is supported.** Do not use Avalanche, Arbitrum, Base or any other `CHAIN_ID` when opening an account or binding a key.

| What you need | Section |
|---------------|---------|
| Trading workflow and sample script | [Trading workflow](../rest-api/trading-workflow.md) |
| RWA request signing | [Request signing](../authentication/request-signing.md) |
| Response format | [REST API overview](../rest-api/README.md) |
| Complete endpoint documentation | [REST API reference](../reference/README.md) |
| Withdrawals | [Withdrawals](../rest-api/withdrawals.md) |

Trading pairs: `PERP_{BASE}_{QUOTE}` (e.g. `PERP_ETH_USDC`).
