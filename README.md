<p align="center">
  <img src="assets/logo.svg" alt="Floot" width="120" height="120" />
</p>

<h1 align="center">Floot MCP</h1>

<p align="center">
  <strong>Build and host full-stack apps with your own AI.</strong><br/>
  A remote <a href="https://modelcontextprotocol.io">Model Context Protocol</a> server you can connect from any MCP-compatible client — Cursor, Claude, ChatGPT, VS Code, and more.
</p>

---

## The server

| | |
|---|---|
| **URL** | `https://mcp.floot.com/mcp` |
| **Transport** | Streamable HTTP |
| **Auth** | None required — if the server needs it, your client will prompt you to sign in on connect |

> **Official one-click connectors for Claude, ChatGPT, and Cursor are in review.**
> Until they land, add the server manually with the instructions below — it already works in **any** MCP client today.

Every client boils down to the same thing: point it at `https://mcp.floot.com/mcp` over Streamable HTTP. Ready-to-paste config files live in [`clients/`](clients/).

---

## Connect

### Cursor

> **Temporary OAuth workaround.** A direct remote connection currently fails during login (see [Troubleshooting](#troubleshooting)). Until the server-side fix lands, connect through the [`mcp-remote`](https://www.npmjs.com/package/mcp-remote) bridge, which authenticates over `http://localhost`.

Add [`clients/cursor-mcp-remote.json`](clients/cursor-mcp-remote.json) to `~/.cursor/mcp.json` (global) or `.cursor/mcp.json` (per-project):

```json
{ "mcpServers": { "floot": { "command": "npx", "args": ["-y", "mcp-remote", "https://mcp.floot.com/mcp"] } } }
```

Once the server-side OAuth fix ships, you can switch to the native remote config in [`clients/cursor.json`](clients/cursor.json) (and the one-click install below):

[![Add to Cursor](https://img.shields.io/badge/Add%20to-Cursor-000000?style=for-the-badge&logo=cursor)](https://cursor.com/install-mcp?name=floot&config=eyJ1cmwiOiJodHRwczovL21jcC5mbG9vdC5jb20vbWNwIn0=)

```json
{ "mcpServers": { "floot": { "url": "https://mcp.floot.com/mcp" } } }
```

### Claude Code (CLI)

```bash
claude mcp add --transport http floot https://mcp.floot.com/mcp
```

### Claude Desktop

**Recommended (Pro/Max/Team/Enterprise):** Settings → **Connectors** → **Add custom connector** → paste `https://mcp.floot.com/mcp`.

**Config-file fallback** (bridges the remote server through [`mcp-remote`](https://www.npmjs.com/package/mcp-remote)) — add [`clients/claude-desktop.json`](clients/claude-desktop.json) to `claude_desktop_config.json`:

```json
{ "mcpServers": { "floot": { "command": "npx", "args": ["-y", "mcp-remote", "https://mcp.floot.com/mcp"] } } }
```

### Claude.ai (web)

Settings → **Connectors** → **Add custom connector** → enter `https://mcp.floot.com/mcp`.

### ChatGPT

Enable connectors/developer mode, then add a remote MCP server pointing at `https://mcp.floot.com/mcp`. Via the API:

```json
{
  "type": "mcp",
  "server_label": "floot",
  "server_url": "https://mcp.floot.com/mcp",
  "require_approval": "never"
}
```

### VS Code (GitHub Copilot)

Add [`clients/vscode.json`](clients/vscode.json) to `.vscode/mcp.json`:

```json
{ "servers": { "floot": { "type": "http", "url": "https://mcp.floot.com/mcp" } } }
```

### Windsurf

Add [`clients/windsurf.json`](clients/windsurf.json) to `~/.codeium/windsurf/mcp_config.json`:

```json
{ "mcpServers": { "floot": { "serverUrl": "https://mcp.floot.com/mcp" } } }
```

### Any other MCP client

Point it at `https://mcp.floot.com/mcp` using **Streamable HTTP** transport. The generic config in [`clients/generic.json`](clients/generic.json) works for most:

```json
{ "mcpServers": { "floot": { "url": "https://mcp.floot.com/mcp" } } }
```

> Client UIs and config keys change over time. If a snippet here drifts from your client's current format, check that client's MCP docs — the server URL and transport above stay the same.

---

## Troubleshooting

### `invalid redirect_uri: must be https (or http://localhost)`

The server requires OAuth, and its authorization server currently rejects the
custom callback URIs that desktop MCP clients use (e.g. Cursor's
`cursor://…/oauth/callback`), accepting only `https://` or `http://localhost`.

**Who's affected and what to do:**

| Client | Connects via | Workaround |
|--------|--------------|------------|
| Cursor | Local process | ✅ Use the `mcp-remote` config (localhost callback) |
| Claude Desktop | Local process | ✅ Use the `mcp-remote` config (localhost callback) |
| Claude.ai / native connector | Anthropic-hosted (https) | Not affected by this error; depends on server DCR |
| ChatGPT | OpenAI-hosted (https) | ⚠️ No client-side workaround — needs the server fix |

The `mcp-remote` bridge unblocks **local** clients because it runs its OAuth
callback on `http://localhost`, which the server accepts. **Hosted** clients
(ChatGPT, Claude.ai web) connect server-to-server, so no local bridge is
possible — they need the server-side fix below.

**Server-side fix (for `mcp.floot.com`):**

1. Relax `redirect_uri` validation to allow private-use URI schemes (RFC 8252),
   not just `https`/`localhost`.
2. Support Dynamic Client Registration (RFC 7591) so clients can register their
   redirect URI on the fly.
3. If auth is delegated to a third-party IdP that forbids custom schemes, front
   it with an MCP auth layer that accepts the client callback and proxies to the
   upstream provider.

Once this ships, every client can use the native remote config and the
`mcp-remote` workaround is no longer needed.

---

## What is MCP?

The [Model Context Protocol](https://modelcontextprotocol.io) is an open standard that lets AI apps connect to external tools and data through a single interface. A Floot MCP connection gives your assistant the tools to scaffold, build, and host full-stack apps directly from your chat.

## Repository layout

```
clients/                     Ready-to-paste config for each MCP client
mcp.json                     Generic MCP server definition
.cursor-plugin/plugin.json   Cursor Marketplace plugin manifest
assets/logo.svg              Logo
LICENSE                      MIT
```

## License

[MIT](LICENSE)
