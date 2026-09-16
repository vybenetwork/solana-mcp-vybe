---
name: vybe-token-market-intel
description: Solana token and market intelligence via Vybe MCP — prices, holders, liquidity, candles, DEX trades, and top traders. Use when the user asks about a mint, token price, holders, markets, volume, OHLCV, or trader leaderboards.
---

# Vybe token & market intel

Use **Solana MCP by Vybe** tools to pull live token and market data.

## When to use

- Token price, metadata, supply, or holder distribution
- Market / pool liquidity and DEX activity
- Trade history or OHLCV candles
- Top traders or labeled accounts

## Workflow

1. Identify the subject: mint address, market/pool address, or symbol. If only a symbol is given, search endpoints that resolve symbols/mints first.
2. Use `search-endpoints` with focused keywords (`token`, `holders`, `ohlc`, `trades`, `markets`, `top-traders`).
3. Inspect the chosen route with `get-endpoint` (params, pagination, sorting).
4. Run `query-vybe-api` with the `path` and `query` params, using sensible defaults (small `limit`, explicit sort fields when required).
5. Present a tight briefing:
   - Price / liquidity / volume when available
   - Top holders or concentration notes
   - Recent trade or candle highlights
   - Caveats (pagination, delayed fields, unlabeled wallets)
6. Suggest one concrete next query (e.g. expand holders, switch timeframe, compare markets).

## Rules

- Prefer mint addresses over ambiguous ticker symbols when both exist.
- Call out incomplete data instead of inventing figures.
- Keep responses scannable; use short tables for holders/trades when helpful.
- Auth failures → ask the user to reconnect OAuth on `mcp.vybenetwork.xyz`.
