# Authentication overview

> Default REST: `https://api-trade.rwaperp.xyz` · VIP REST: `https://api-vip.rwaperp.xyz` (same paths and `RWA-*` signing)  
> **To-B partners:** Contact RWA Perp to obtain a dedicated Base URL before using `api-trade`, `api-vip`, or any custom host.  
> **X Layer only** (`chainId = 196`). No other chain is supported.  
> Follow [Account onboarding](onboarding.md) to open an account and bind a key. Then use the [sample trading script](../rest-api/mainline-script.md) to exercise the primary trading operations.

REST uses **`RWA-*` headers**; the private WebSocket uses **`rwa_*` query parameters**.

---

## Authentication layers

| Layer | Algorithm | Purpose | Stored by |
|-------|-----------|---------|---------|
| Account binding | EVM EIP-712 | Open account, bind API public key | Wallet private key (one-time) |
| API requests | Ed25519 | REST / private WebSocket | Client application (long-lived) |

`/v1/public/*` requires no API key. **The wallet private key is not the API secret.** Generate a separate Ed25519 key pair, then bind its public key with an EIP-712 signature from your wallet.

---

## Credentials and endpoints

| Name | Sent as | Notes |
|------|------------------|-------|
| `account_id` | `RWA-Account-Id` / WS path | `0x`-prefixed value containing 64 hexadecimal characters |
| API public key | `RWA-Api-Key` | `ed25519:` + base58 |
| API private key | Never transmitted | base58 seed, signs locally |
| Timestamp | `RWA-Timestamp` | Milliseconds |
| Signature | `RWA-Signature` | Ed25519 signature encoded as URL-safe Base64, without trailing `=` |

| Type | URL |
|------|-----|
| REST (default) | `https://api-trade.rwaperp.xyz` |
| REST (VIP) | `https://api-vip.rwaperp.xyz` |
| Public WS | `wss://api-trade.rwaperp.xyz/ws/public/ws/stream/{account_id}` (or `wss://api-vip.rwaperp.xyz/...`) |
| Private WS | `wss://api-trade.rwaperp.xyz/ws/private/v2/ws/private/stream/{account_id}` (or `wss://api-vip.rwaperp.xyz/...`) |

VIP REST uses the same paths and `RWA-*` signing as the default host. WebSocket streams on `api-vip` are the same market and private feeds. **To-B partners must contact RWA Perp to obtain a dedicated Base URL** before calling these hosts.

**Supported chain: X Layer only.** The EIP-712 domain `chainId` used for opening an account or binding a key must be `196`. Arbitrum, Base, Avalanche, Ethereum and every other chain are unsupported; passing any other `chainId` will fail signature verification.

| Chain | chainId | Supported |
|-------|---------|-----------|
| **X Layer** | `196` | **Yes (only)** |

---

## Authentication by endpoint

| Authentication | Typical endpoints |
|----------------|-------------------|
| None | `/v1/public/*`, `/v1/get_account` |
| RWA signature | `/v1/order`, `/v1/positions`, `/v1/client/holding` |
| Wallet EIP-712 | Account opening and key binding: `register_dex_account`, `dex_api_key` (off-chain domain) |
| Wallet EIP-712 + RWA | Withdrawals: `withdraw_request` ([on-chain domain](../rest-api/withdrawals.md)) |
