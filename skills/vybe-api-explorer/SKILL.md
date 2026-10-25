---
name: vybe-api-explorer
description: Call one specific Vybe Solana API tool for wallets, tokens, markets, trades, or unsigned transactions. Use when the user wants live Vybe data or a signable Solana payload.
---

# Vybe API explorer

Each tool calls one Vybe endpoint. Pass that tool's arguments directly. Do not pass a path, URL, or HTTP method.

## Tools

| Tool | Calls |
| --- | --- |
| `list-pyth-price-feeds` | GET `/v4/oracle/pyth/pricefeeds` |
| `get-pyth-price-candles` | GET `/v4/oracle/pyth/pricefeeds/{priceFeedAddress}/candles` |
| `get-pyth-price` | GET `/v4/oracle/pyth/pricefeeds/{priceFeedAddress}/price` |
| `get-market` | GET `/v4/markets/{marketAddress}` |
| `list-markets` | GET `/v4/markets` |
| `get-market-candles` | GET `/v4/markets/{marketAddress}/candles` |
| `get-pyth-price-history` | GET `/v4/oracle/pyth/pricefeeds/{priceFeedAddress}/price-ts` |
| `get-pyth-product` | GET `/v4/oracle/pyth/products/{productAddress}` |
| `get-token-candles` | GET `/v4/tokens/{mintAddress}/candles` |
| `list-tokens` | GET `/v4/tokens` |
| `list-labeled-programs` | GET `/v4/programs/labeled-program-accounts` |
| `list-supported-dexes` | GET `/v4/reference/dexes` |
| `get-token-liquidity` | GET `/v4/tokens/{mintAddress}/liquidity` |
| `get-token` | GET `/v4/tokens/{mintAddress}` |
| `get-token-holder-count-history` | GET `/v4/tokens/{mintAddress}/holders-count-ts` |
| `list-instruction-names` | GET `/v4/reference/instruction-names` |
| `get-token-trader-activity` | GET `/v4/tokens/{mintAddress}/trader-activity` |
| `get-token-top-pnl-traders` | GET `/v4/tokens/{mintAddress}/top-pnl-traders` |
| `get-token-top-holders` | GET `/v4/tokens/{mintAddress}/top-holders` |
| `list-transfers` | GET `/v4/transfers` |
| `get-swap-quote` | GET `/v4/trading/swap-quote` |
| `get-token-trade-volume-history` | GET `/v4/tokens/{mintAddress}/trade-volume-ts` |
| `build-swap` | POST `/v4/trading/swap` |
| `list-trades` | GET `/v4/trades` |
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
| `get-x402-access-guide` | Static x402 pay-per-call guidance. Does not send a payment. |

## Workflow

1. Choose the one tool whose name matches the question.
2. Fill only the arguments in that tool's schema. Path values such as `ownerAddress` and `mintAddress` are arguments, not a URL.
3. For several wallets, use the matching `*-batch` tool and put the addresses in `body`.
4. Return the endpoint, the arguments used, and a compact result.
5. If the user wants pay-per-call access, call `get-x402-access-guide`. It returns guidance only and does not send a payment.

## Rules

- Never put API keys in repo files or chat logs when avoidable; prefer the OAuth MCP session.
- Do not invent a tool that is not in this list.
- `build-swap`, `build-close-token-accounts`, and `build-withdraw-mev` return an unsigned payload. Confirm intent, then tell the user to sign it in their own wallet.
- Prefer the smallest successful request (low `limit`) before large pulls.
