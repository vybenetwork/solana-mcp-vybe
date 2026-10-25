---
name: vybe-wallet-analytics
description: Analyze Solana wallets with Vybe — balances, holdings, PnL, transfers, and counterparties. Use when the user asks about a wallet address, portfolio, realized/unrealized PnL, token accounts, or transfer history on Solana.
---

# Vybe wallet analytics

Call the one wallet tool that matches the question. Pass `ownerAddress` (and any filters) as arguments. Do not look up a path first.

## Tools

| Tool | Calls |
| --- | --- |
| `get-empty-accounts-batch` | POST `/v4/wallets/batch/empty-accounts` |
| `get-dust-accounts-batch` | POST `/v4/wallets/batch/dust-accounts` |
| `get-token-balance-history-batch` | POST `/v4/wallets/batch/token-balances-ts` |
| `get-token-balances-batch` | POST `/v4/wallets/batch/token-balances` |
| `list-top-traders` | GET `/v4/wallets/top-traders` |
| `get-wallet-counterparties` | GET `/v4/wallets/{ownerAddress}/counterparties` |
| `list-labeled-accounts` | GET `/v4/wallets/labeled-accounts` |
| `get-token-accounts-batch` | POST `/v4/wallets/batch/token-accounts-balance-ts` |
| `get-wallet-defi-positions` | GET `/v4/wallets/{ownerAddress}/defi-positions` |
| `get-wallet-empty-accounts` | GET `/v4/wallets/{ownerAddress}/empty-accounts` |
| `get-wallet-dust-accounts` | GET `/v4/wallets/{ownerAddress}/dust-accounts` |
| `get-wallet-token-account-history` | GET `/v4/wallets/{ownerAddress}/token-accounts-balance-ts` |
| `get-wallet-token-balances` | GET `/v4/wallets/{ownerAddress}/token-balance` |
| `get-wallet-pnl` | GET `/v4/wallets/{ownerAddress}/pnl` |
| `get-wallet-pnl-history` | GET `/v4/wallets/{ownerAddress}/pnl-ts` |
| `get-wallet-token-balance-history` | GET `/v4/wallets/{ownerAddress}/token-balance-ts` |
| `build-close-token-accounts` | POST `/v4/wallets/util/close-token-accounts` |
| `get-wallet-transfer-volume` | GET `/v4/wallets/{ownerAddress}/transfer-volume-usd` |
| `build-withdraw-mev` | POST `/v4/wallets/util/withdraw-mev` |

## When to use

- Wallet balances, holdings, or portfolio value → `get-wallet-token-balances`
- Realized / unrealized PnL → `get-wallet-pnl` or `get-wallet-pnl-history`
- Counterparties → `get-wallet-counterparties`
- Empty / dust token accounts → `get-wallet-empty-accounts` or `get-wallet-dust-accounts`
- Several wallets at once → the matching `*-batch` tool, with addresses in `body.ownerAddresses`

## Workflow

1. Confirm you have a Solana wallet address (base58 pubkey). If missing, ask for it.
2. Call the matching tool with `ownerAddress` and a small `limit` when the schema has one.
3. Summarize results: top holdings, USD values when present, PnL figures, notable counterparties. Name the tool used.
4. Offer one follow-up (deeper PnL window, specific mint, or transfer volume).

## Rules

- Never ask for or handle private keys or seed phrases.
- `build-close-token-accounts` and `build-withdraw-mev` return unsigned transactions. Use them only when the user explicitly asks, and tell them to sign in their own wallet.
- If OAuth is required, tell the user to connect the Vybe MCP connector and retry.
