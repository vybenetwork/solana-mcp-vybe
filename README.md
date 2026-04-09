# solana-mcp-vybe

Public **Model Context Protocol (MCP) registry metadata** for **Vybe Solana MCP** (hosted on ReadMe).

The live MCP endpoint is:

`https://docs.vybenetwork.com/mcp`

This repository holds:

- **`server.json`** — metadata published to the [official MCP Registry](https://registry.modelcontextprotocol.io) (GitHub Actions).
- **`.mcp.json` and `mcp.json`** — [Open Plugins](https://open-plugins.com)–style MCP config at the repo root so directory UIs (e.g. Cursor “Submit a Plugin” with Auto GitHub scan) can detect a plugin component. They use **`npx mcp-remote`** and the public MCP URL only — **no API key in the repo.** Add a **`X-API-KEY`** header (or env) in your client when you need tools that call the Vybe API (e.g. `execute-request`); keys come from [vybe.fyi](https://vybe.fyi).

`examples/cursor-mcp.json` is the same idea for native **`url`** config: URL only, optional headers in the client when needed.

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

Registry id: **`io.github.vybenetwork/vybe-solana-api`** (`server.json` `name`; display title is **Vybe Solana MCP**).
