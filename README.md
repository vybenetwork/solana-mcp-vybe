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

### Claude.ai custom connector

```text
Name: Solana MCP by Vybe
URL:  https://mcp.vybenetwork.xyz/mcp
```

Authenticate with **OAuth** when the client prompts. Do not commit API keys into this repo.

## What this repository holds

- **`server.json`** — metadata published to the [official MCP Registry](https://registry.modelcontextprotocol.io) (GitHub Actions). Remote URL: `https://mcp.vybenetwork.xyz`.
- **`.mcp.json` and `mcp.json`** — root MCP/plugin configs for directory UIs (e.g. Cursor “Submit a Plugin”). Native HTTP to `https://mcp.vybenetwork.xyz/mcp` — **no secrets**.
- **`.codex-plugin/plugin.json`** — Codex plugin metadata for local install/refresh against the same MCP URL.
- **`chatgpt-app-submission.json`** — draft ChatGPT Apps submission fields.

## Available tools

| Tool | Description |
| --- | --- |
| `list-endpoints` | Browse API paths with methods and summaries |
| `search-endpoints` | Search paths, operations, and schemas by keyword |
| `get-endpoint` | Full OpenAPI details for one path and method |
| `execute-request` | Live authenticated API calls |
| `pay-with-x402` | x402 pay-per-call integration guidance |

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
