# Security and troubleshooting

## Key scope and lifetime

The default scope used by the onboarding example is `read,trading`. Add `asset` when the key also needs to authorize withdrawals and transfers. The example sets the key expiration to 365 days; bind a new key before the configured expiration time.

## Security

Deploy only the API private key to your trading processes; never deploy the wallet private key. If an API key is exposed, bind a replacement, update the affected processes, and stop using the old credential.

## Common issues

| Symptom | Resolution |
|---------|------------|
| `address and signature do not match` | Use `register_dex_account`; add `chainType: "EVM"` to the body; `chainId` must be `196` (X Layer) |
| Opened an account / bound a key on Avalanche, Arbitrum, Base, etc. | This environment **supports X Layer only** (`CHAIN_ID=196`); correct it and repeat account opening / key binding |
| `must not be blank` when binding a key | Use `dex_api_key` + `AddDexApiKey`; the public-key field is **`key`** |
| `nonce is invalid` | Take the account-opening `timestamp` from the server time in the `registration_nonce` response |
| `401` on REST | Check that the account_id and key belong to the same account, and that the path/body match what was signed |
| `Verify contract is invalid` on withdrawal | Do not use the account-opening `0xCcCC` address or a vault address; see [Withdrawals](../rest-api/withdrawals.md) |
| Public WS disconnects immediately after connecting | Use the `account_id` returned by `GET /v1/get_account`; arbitrary session identifiers are not accepted |
| `401` on private WS | `rwa_sign` signs the timestamp only; do not apply the REST signing rule |
