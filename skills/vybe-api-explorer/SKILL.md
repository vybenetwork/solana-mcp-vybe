---
name: vybe-api-explorer
description: Explore and call the Vybe Solana API catalog through MCP — discover endpoints, inspect OpenAPI params, then run authenticated live requests. Use when the user wants to browse APIs, find a specific route, understand parameters, or execute a Vybe HTTP call.
---

# Vybe API explorer

Guide developers through the Vybe OpenAPI catalog with MCP tools.

## Tools

| Tool | Use for |
|------|---------|
| `list-endpoints` | Full path/method catalog |
| `search-endpoints` | Keyword search across paths, ops, schemas |
| `get-endpoint` | Full params, security, servers for one route |
| `query-vybe-api` | Live GET read of any `/v4` path |
| `query-vybe-api-batch` | Live read across many wallets at once |
| `build-vybe-transaction` | Unsigned swap / close-account / withdraw-MEV payload |
| `pay-with-x402` | Pay-per-call integration guidance only |

## Workflow

1. Clarify the goal (discover, inspect, or execute).
2. Discovery:
   - Broad browse → `list-endpoints`
   - Targeted → `search-endpoints` with 1–3 keywords
3. Before any live call, run `get-endpoint` for the path + HTTP method.
4. Pick the matching call tool and fill it from the schema — required query/path/body fields only; omit unknowns:
   - GET route → `query-vybe-api` with `path` and `query`
   - `/v4/wallets/batch/*` → `query-vybe-api-batch` with `path` and `body`
   - swap, close token accounts, withdraw MEV → `build-vybe-transaction`
5. Return:
   - Endpoint path + method
   - Key request params used
   - Compact result summary (or error body)
6. If the user wants paid / metered access patterns, call `pay-with-x402` and explain — do not invent payment flows.

## Rules

- Never put API keys in repo files or chat logs when avoidable; prefer the OAuth MCP session.
- Do not invent endpoints that are not in the catalog.
- For `build-vybe-transaction` (swaps, close accounts, withdraws), confirm intent, then return the unsigned payload only — the user signs in their own wallet.
- Prefer the smallest successful request (low `limit`) before large pulls.
