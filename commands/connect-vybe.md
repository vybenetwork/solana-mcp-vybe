---
name: connect-vybe
description: Connect and authenticate the Vybe Solana MCP server over OAuth.
---

The plugin already declares the remote MCP server at `https://mcp.vybenetwork.xyz/mcp`.

1. Open Claude Code's MCP panel (`/mcp`) and select **solana-mcp-vybe**.
2. Choose **Authenticate**. The browser opens `https://mcp.vybenetwork.xyz/authorize`.
3. On the Vybe login popup, enter the account email as the username and the API key as the password. Approve `openid`, `email`, `mcp:read`, and `mcp:write`.
4. Return here and confirm a tool such as `get-wallet-pnl` or `get-token` is available.
5. Never paste a private key. `build-swap`, `build-close-token-accounts`, and `build-withdraw-mev` return an unsigned payload only.

If auth fails, retry `/mcp` rather than putting an API key in chat or in this repo.
