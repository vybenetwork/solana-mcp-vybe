---
name: vybe-wallet-analytics
description: Analyze Solana wallets with Vybe MCP — balances, holdings, PnL, transfers, and counterparties. Use when the user asks about a wallet address, portfolio, realized/unrealized PnL, token accounts, or transfer history on Solana.
---

# Vybe wallet analytics

Use the **Solana MCP by Vybe** tools (`list-endpoints`, `search-endpoints`, `get-endpoint`, `query-vybe-api`, `query-vybe-api-batch`) to answer wallet questions with live data.

## When to use

- Wallet balances, holdings, or portfolio value
- Realized / unrealized PnL for a wallet
- Transfer history or counterparties
- Empty / dust token accounts

## Workflow

1. Confirm you have a Solana wallet address (base58 pubkey). If missing, ask for it.
2. Discover the right route:
   - Prefer `search-endpoints` with keywords like `wallet`, `pnl`, `transfer`, `token-balance`.
   - Or `list-endpoints` then pick the matching path.
3. Call `get-endpoint` for the chosen path + method to learn required params, auth, and response shape.
4. Call `query-vybe-api` with the `path` and `query` params, or `query-vybe-api-batch` when covering several wallets in one call.
5. Summarize results for the user: top holdings, USD values when present, PnL figures, notable counterparties. Cite the endpoint used.
6. Offer a clear follow-up (e.g. deeper PnL window, specific mint, transfer filters).

## Rules

- Never ask for or handle private keys / seed phrases.
- Do not broadcast transactions; if a route returns an unsigned tx, say the user must sign in their own wallet.
- If OAuth / auth is required, tell the user to connect the Vybe MCP connector and retry.
- Prefer read-only endpoints for analytics. Use `build-vybe-transaction` only when the user explicitly asks for a transaction payload.
