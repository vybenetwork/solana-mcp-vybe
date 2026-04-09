# solana-mcp-vybe

Public **Model Context Protocol (MCP) registry metadata** for the Vybe Solana API MCP hosted on ReadMe.

The live MCP endpoint is:

`https://docs.vybenetwork.com/mcp`

This repository holds:

- **`server.json`** — metadata published to the [official MCP Registry](https://registry.modelcontextprotocol.io) (GitHub Actions).
- **`.mcp.json` and `mcp.json`** — [Open Plugins](https://open-plugins.com)–style MCP config at the repo root so directory UIs (e.g. Cursor “Submit a Plugin” with Auto GitHub scan) can detect a plugin component. The [Open Plugins MCP spec](https://open-plugins.com/agent-builders/components/mcp-servers) expects a **`command`** (not only a remote `url`), so these files use **`npx mcp-remote`** to connect to the hosted MCP URL. Set **`VYBE_API_KEY`** in your environment (see [Vybe API keys](https://vybe.fyi)).

For native remote URL + headers (no `npx`), use `examples/cursor-mcp.json` in Cursor’s user config instead.

## GitHub repository name

**`vybenetwork/solana-mcp-vybe`** (starts with `solana-mcp`, includes Vybe).

## Publish a new listing version

1. Clone or use this repo at `github.com/vybenetwork/solana-mcp-vybe`.
2. Tag and push (the workflow sets `server.json` `version` from the tag):

   ```bash
   git tag v1.0.0
   git push origin v1.0.0
   ```

   Or run **Actions → Publish to MCP Registry → Run workflow** (uses the version already in `server.json`).

Publishing uses **GitHub OIDC** in Actions; no personal token secret is required.

3. Verify:

   ```bash
   curl -sS "https://registry.modelcontextprotocol.io/v0.1/servers?search=vybenetwork" | jq .
   ```

## Cursor and other directories

Use `examples/cursor-mcp.json` as the install snippet (users set their own `X-API-KEY`). For [Cursor Directory](https://cursor.directory), submit the same URL and snippet after the registry publish succeeds.

## Registry server id

Listed as **`io.github.vybenetwork/vybe-solana-api`** (set in `server.json` `name`).
