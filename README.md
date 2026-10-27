# Solana MCP by Vybe

Solana MCP by Vybe is a developer toolkit for live Solana data: wallets, trades, markets, transfers, and signable swaps. The public server publishes **44 tools**. Each tool calls one Vybe API endpoint.

`build-swap`, `build-close-token-accounts`, and `build-withdraw-mev` return an unsigned transaction to sign in your own wallet. The server does not take private keys, and it does not broadcast transactions. `get-x402-access-guide` returns x402 pay-per-call instructions and does not send a payment.

This repo is the directory listing, Claude plugin, and MCP registry metadata. The running server is [`vybenetwork/vybe-mcp-oauth-proxy`](https://github.com/vybenetwork/vybe-mcp-oauth-proxy). Its current version is **1.3.2**.

## Versions

| Piece | Version | Where |
| --- | --- | --- |
| Live MCP server | 1.3.2 | `initialize` on `https://mcp.vybenetwork.xyz/mcp` |
| Claude plugin | 1.3.0 | `.claude-plugin/plugin.json` |
| MCP registry metadata | 1.1.3 | `server.json` |

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

The public guide at [docs.vybenetwork.com/docs/mcp](https://docs.vybenetwork.com/docs/mcp) still describes the old tools `list-endpoints`, `search-endpoints`, `get-endpoint`, and `execute-request`. Those names are not in the published tool list.

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

Same snippet: [`.mcp.json`](.mcp.json).

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

### Claude Code / Cowork plugin

This repo is a Claude plugin (`/.claude-plugin/plugin.json`). Validate, then submit the public GitHub URL:

```bash
claude plugin validate .
```

- Claude.ai: https://claude.ai/admin-settings/directory/submissions/plugins/new
- Console: https://platform.claude.com/plugins/submit

Sign in with **OAuth** when the client asks. Use your Vybe email as the username and your API key as the password, then approve consent. Do not commit API keys or private keys into this repo.

Claude directory links from `.claude-plugin/plugin.json`:

- Homepage: https://docs.vybenetwork.com
- Documentation: https://docs.vybenetwork.com/docs/mcp
- Support: https://vybe.fyi/settings/api
- Privacy: https://vybe.fyi/privacy
- Terms: https://vybe.fyi/terms

Classification on that manifest: acts on `apis`, `finances`, `code`, and `databases`, department `engineering`, industry `software-saas`, subject `computing`. `claude plugin validate` on Claude Code 2.1.138 reports the directory-only fields (`displayName`, `icon`, links, `classification`) as unrecognized. The plugin directory accepts them.

## What this repository holds

- **`server.json`** — metadata published to the [official MCP Registry](https://registry.modelcontextprotocol.io) (GitHub Actions). Remote URL: `https://mcp.vybenetwork.xyz`.
- **`.mcp.json`** — MCP server URL for the Claude and Codex plugins. Native HTTP to `https://mcp.vybenetwork.xyz/mcp`. No secrets.
- **`.codex-plugin/plugin.json`** — Codex plugin metadata for local install against the same MCP URL.
- **`.claude-plugin/plugin.json`** — Claude Code / Cowork plugin manifest (skills, commands, remote MCP, directory links, and classification).
- **`skills/`** — `vybe-api-explorer`, `vybe-token-market-intel`, and `vybe-wallet-analytics`.
- **`commands/connect-vybe.md`** — Claude command for the OAuth sign-in steps.

## Available tools

Published `tools/list` has these 44 tools. Pass each tool's own arguments. Do not pass a URL, path, or HTTP method.

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
| `get-token-holder-count-history` | GET `/v4/tokens/{mintAddress}/holders-count-ts`. Requires `startTime` and `endTime` as unix seconds, at most 2592000 seconds (30 days) apart. `interval` is `hour` or `day`. |
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

`build-swap`, `build-close-token-accounts`, and `build-withdraw-mev` return an unsigned transaction. They do not sign or broadcast it. The five `*-batch` tools POST a list of wallet addresses and only read data.

## GitHub repository name

**`vybenetwork/solana-mcp-vybe`** (starts with `solana-mcp`, includes Vybe).

## Publish a new listing version

1. Clone or use this repo at `github.com/vybenetwork/solana-mcp-vybe`
2. Tag and push (the workflow sets `server.json` `version` from the tag):

   ```bash
   git tag vX.Y.Z
   git push origin vX.Y.Z
   ```

   `server.json` is currently **1.1.3**. The next registry tag should be newer than that. A tag push rewrites `server.json` `version` from the tag during the workflow.

   Or run **Actions → Publish to MCP Registry → Run workflow** (uses the version already in `server.json`).

Publishing uses **GitHub OIDC** in Actions; no personal token secret is required.

**If you use `mcp-publisher login github` locally** and get **403** for `io.github.vybenetwork/...`: Git apps like **Git Credential Manager** are unrelated. Open **GitHub → Settings → Applications → Authorized OAuth Apps**, choose the app you authorized during **`mcp-publisher login github`** (device flow), then under **Organization access** click **Grant** for **`vybenetwork`**. On SAML-enforced orgs, also complete **SSO** for that OAuth app. Then run **`mcp-publisher logout`**, **`mcp-publisher login github`**, and **`publish`** again.

3. Verify:

   ```bash
   curl -sS "https://registry.modelcontextprotocol.io/v0.1/servers?search=vybenetwork" | jq .
   ```

## Cursor and other directories

Use `.mcp.json` as the install snippet. For [Cursor Directory](https://cursor.directory), submit after the registry publish succeeds; use **OAuth** for `https://mcp.vybenetwork.xyz/mcp`.

## Registry catalog id

**`server.json` `name`:** **`io.github.vybenetwork/solana-mcp-vybe`**. **Display title:** **Solana MCP by Vybe**.

**Publish:** push `main`, then `git tag vX.Y.Z && git push origin vX.Y.Z`, or **Actions → Publish to MCP Registry**.
