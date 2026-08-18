# Vybe Solana API MCP

Connect Vybe’s Solana API to Cursor, Codex, Windsurf, Claude, or ChatGPT via MCP.

## MCP server URL

Use the streamable HTTP endpoint for all clients:

```text
https://mcp.vybenetwork.xyz/mcp
```

Registry remote (without path): `https://mcp.vybenetwork.xyz`

## Setup

### Cursor / Windsurf / Codex

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

### Claude.ai custom connector

```text
Name: Solana MCP by Vybe
URL:  https://mcp.vybenetwork.xyz/mcp
```

### Claude Desktop (`mcp-remote`)

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

Authenticate with OAuth when prompted. Do not put API keys in git.

## Available MCP tools

| Tool | Description |
| --- | --- |
| `list-endpoints` | Browse all API paths with methods and summaries |
| `search-endpoints` | Deep search across paths, operations, and schemas |
| `get-endpoint` | Full OpenAPI spec for a specific endpoint |
| `execute-request` | Live API calls |
| `pay-with-x402` | x402 pay-per-call integration guidance |

## Test prompts

- List all available Vybe API endpoints
- Show the parameters for the Wallet PnL endpoint
- Find all endpoints related to token holders
- Get the top 3 Solana traders by realized PnL today
