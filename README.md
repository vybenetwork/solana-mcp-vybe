# solana-mcp-vybe

Public **Model Context Protocol (MCP) registry metadata** for **Solana MCP by Vybe** (hosted on ReadMe).

The live MCP endpoint is:

`https://docs.vybenetwork.com/mcp`

This repository holds:

- **`server.json`** — metadata published to the [official MCP Registry](https://registry.modelcontextprotocol.io) (GitHub Actions).
- **`.mcp.json` and `mcp.json`** — [Open Plugins](https://open-plugins.com)–style MCP config at the repo root so directory UIs (e.g. Cursor “Submit a Plugin” with Auto GitHub scan) can detect a plugin component. They use **`npx mcp-remote`** and the public MCP URL only — **no API key in the repo.** Add a **`X-API-KEY`** header (or env) in your client when you need **live Solana API calls** (not just schema browsing); keys come from [vybe.fyi](https://vybe.fyi).

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

Use `examples/cursor-mcp.json` as the install snippet. For [Cursor Directory](https://cursor.directory), submit after the registry publish succeeds; add `X-API-KEY` locally when you need **live API calls**.

## Registry catalog id

Target id in `server.json` **`name`**: **`io.github.vybenetwork/solana-mcp-vybe`** (matches this repo).

The [official registry](https://registry.modelcontextprotocol.io) does not offer self-service delete/unpublish ([FAQ](https://modelcontextprotocol.io/registry/faq)). The previous id **`io.github.vybenetwork/vybe-solana-api`** must be **removed by registry operators** before the same remote URL can be published under the new name.

- **Deletion / migration request:** [modelcontextprotocol/registry#1151](https://github.com/modelcontextprotocol/registry/issues/1151)

**After that issue is resolved**, publish by tagging (e.g. `v1.0.7`) or **Actions → Publish to MCP Registry**. Do **not** run a publish until then—the workflow will fail while the old entry still holds `https://docs.vybenetwork.com/mcp`.

**Display title** everywhere: **Solana MCP by Vybe** (`server.json` `title`).
