---
name: vybe-token-market-intel
description: Solana token and market intelligence via Vybe — prices, holders, liquidity, candles, DEX trades, and top traders. Use when the user asks about a mint, token price, holders, markets, volume, OHLCV, or trader leaderboards.
---

# Vybe token and market intel

Call the one token, market, or trade tool that matches the question. Pass `mintAddress` or `marketAddress` as an argument. Do not look up a path first.

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

## When to use

- Token details, price, or metadata → `get-token`
- Holders → `get-token-top-holders` or `get-token-holder-count-history`
- Liquidity → `get-token-liquidity`
- Candles → `get-token-candles` or `get-market-candles`
- Trades or transfers → `list-trades` or `list-transfers`
- Leaderboard → `list-top-traders`
- A price quote without a transaction → `get-swap-quote`
- An unsigned swap → `build-swap`

## Workflow

1. Identify the mint, market, or leaderboard. If only a ticker is given, call `list-tokens` before a mint-specific tool.
2. Call the matching tool with the required address and a small `limit` when the schema has one.
3. Present a tight briefing: price, liquidity, or volume when available; holder concentration; recent trades or candles.
4. Suggest one next tool (holders, another timeframe, or a quote).

## Rules

- Prefer mint addresses over ambiguous ticker symbols when both exist.
- Call out incomplete data instead of inventing figures.
- `build-swap` returns an unsigned transaction. Use it only when the user asks for a swap, and tell them to sign it in their own wallet.
- Auth failures → ask the user to reconnect OAuth on `mcp.vybenetwork.xyz`.
