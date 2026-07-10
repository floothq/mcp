# Floot

**Build and host full-stack apps with your own AI.**

A Cursor plugin that connects your editor to the Floot remote MCP server, so you can scaffold, build, and host full-stack applications without leaving your workflow.

## Install

Add this plugin from the Cursor Marketplace, or point Cursor at this repository.

The plugin registers a single remote MCP server:

| Server | Transport | URL |
|--------|-----------|-----|
| `floot` | Streamable HTTP | `https://mcp.floot.com/mcp` |

No local install or API key is required to connect. If the server requires
authentication, Cursor will prompt you to sign in on first use.

## What's in this plugin

```
.cursor-plugin/plugin.json   Plugin manifest (name, version, author, logo)
mcp.json                     Remote MCP server definition
assets/logo.svg              Marketplace logo
```

## Configuration

The MCP server is defined in [`mcp.json`](mcp.json):

```json
{
  "mcpServers": {
    "floot": {
      "url": "https://mcp.floot.com/mcp"
    }
  }
}
```

To point at a different environment (e.g. staging), change the `url`.

## License

MIT
