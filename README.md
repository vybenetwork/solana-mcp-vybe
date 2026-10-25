# Solana MCP by Vybe

Solana MCP by Vybe lets Cursor, Claude, Codex, and other MCP clients browse schemas or make live Solana API calls through one public MCP server.

Public **Model Context Protocol (MCP) registry metadata** for **Solana MCP by Vybe**.

## MCP endpoint

Use the streamable HTTP endpoint:

```text
https://mcp.vybenetwork.xyz/mcp
```

Registry metadata (`server.json`) publishes the remote as:

```text
https://mcp.vybenetwork.xyz
```

Clients that require an explicit MCP path (ChatGPT Developer Mode, Codex, Cursor HTTP) should use **`https://mcp.vybenetwork.xyz/mcp`**.

Copy-paste setup for the public docs site: [`docs/mcp.md`](docs/mcp.md). Live product guides: [docs.vybenetwork.com/docs/mcp](https://docs.vybenetwork.com/docs/mcp) (still may show the old `.com` host until that site is updated).

## Quick setup

### Cursor / Windsurf / Codex-style HTTP

```json
{
  "mcpServers": {
    "solana-mcp-vybe": {
      "type": "http",
      "url": "https://mcp.vybenetwork.xyz/mcp"
    }
  }
}
```

Same snippet: [`examples/cursor-mcp.json`](examples/cursor-mcp.json).

### Claude Desktop via `mcp-remote`

```json
{
  "mcpServers": {
    "solana-mcp-vybe": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.vybenetwork.xyz/mcp"]
    }
  }
}
```

### Claude.ai custom connector or Connectors Directory

```text
Name: Solana MCP by Vybe
URL:  https://mcp.vybenetwork.xyz/mcp
```

Portal copy for the official directory: [`claude-connector-submission.json`](claude-connector-submission.json).

### Claude Code / Cowork plugin

This repo is a Claude plugin (`/.claude-plugin/plugin.json`). Validate, then submit the public GitHub URL:

```bash
claude plugin validate .
```

- Claude.ai: https://claude.ai/admin-settings/directory/submissions/plugins/new
- Console: https://platform.claude.com/plugins/submit

Authenticate with **OAuth** when the client prompts. Do not commit API keys into this repo.

## What this repository holds

- **`server.json`** — metadata published to the [official MCP Registry](https://registry.modelcontextprotocol.io) (GitHub Actions). Remote URL: `https://mcp.vybenetwork.xyz`.
- **`.mcp.json` and `mcp.json`** — root MCP/plugin configs for directory UIs (e.g. Cursor “Submit a Plugin”). Native HTTP to `https://mcp.vybenetwork.xyz/mcp` — **no secrets**.
- **`.codex-plugin/plugin.json`** — Codex plugin metadata for local install/refresh against the same MCP URL.
- **`.claude-plugin/plugin.json`** — Claude Code / Cowork plugin manifest (skills + remote MCP).
- **`claude-connector-submission.json`** — field-by-field copy for the Claude Connectors Directory portal.
- **`chatgpt-app-submission.json`** — draft ChatGPT Apps submission fields.

## Available tools

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

## GitHub repository name

**`vybenetwork/solana-mcp-vybe`** (starts with `solana-mcp`, includes Vybe).

## Publish a new listing version

1. Clone or use this repo at `github.com/vybenetwork/solana-mcp-vybe`
2. Tag and push (the workflow sets `server.json` `version` from the tag):

   ```bash
   git tag v1.0.0
   git push origin v1.0.0
   ```

   Or run **Actions → Publish to MCP Registry → Run workflow** (uses the version already in `server.json`).

Publishing uses **GitHub OIDC** in Actions; no personal token secret is required.

**If you use `mcp-publisher login github` locally** and get **403** for `io.github.vybenetwork/...`: Git apps like **Git Credential Manager** are unrelated. Open **GitHub → Settings → Applications → Authorized OAuth Apps**, choose the app you authorized during **`mcp-publisher login github`** (device flow), then under **Organization access** click **Grant** for **`vybenetwork`**. On SAML-enforced orgs, also complete **SSO** for that OAuth app. Then run **`mcp-publisher logout`**, **`mcp-publisher login github`**, and **`publish`** again.

3. Verify:

   ```bash
   curl -sS "https://registry.modelcontextprotocol.io/v0.1/servers?search=vybenetwork" | jq .
   ```

## Cursor and other directories

Use `examples/cursor-mcp.json` as the install snippet. For [Cursor Directory](https://cursor.directory), submit after the registry publish succeeds; use **OAuth** for `https://mcp.vybenetwork.xyz/mcp`.

## Registry catalog id

**`server.json` `name`:** **`io.github.vybenetwork/solana-mcp-vybe`**. **Display title:** **Solana MCP by Vybe**.

**Publish:** push `main`, then `git tag vX.Y.Z && git push origin vX.Y.Z`, or **Actions → Publish to MCP Registry**.
