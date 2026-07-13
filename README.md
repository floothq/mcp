<p align="center">
  <img src="assets/logo.svg" alt="Floot" width="128" height="128" />
</p>

<h1 align="center">Floot MCP Connector</h1>

<p align="center">
  <strong>Build full-stack Floot apps from Claude &amp; ChatGPT.</strong>
</p>

<p align="center">
  Create, edit, and publish full-stack apps — with a real database, authentication, and email —<br/>
  without leaving your AI chat. Runs on your existing Claude or ChatGPT subscription, not Floot credits.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/protocol-MCP-000000?style=flat-square" alt="Model Context Protocol" />
  <img src="https://img.shields.io/badge/clients-Claude%20%C2%B7%20ChatGPT-000000?style=flat-square" alt="Clients" />
  <img src="https://img.shields.io/badge/status-beta-e8a33d?style=flat-square" alt="Beta" />
</p>

<p align="center">
  <a href="#-connect">Connect</a> ·
  <a href="#-what-floot-can-do">Capabilities</a> ·
  <a href="#-try-these-prompts">Prompts</a> ·
  <a href="#️-troubleshooting--faq">FAQ</a>
</p>

---

## 🔗 Server URL

```
https://mcp.floot.com/mcp
```

> [!TIP]
> The URL must end in **`/mcp`**. The root domain will not connect.

It connects over the [Model Context Protocol (MCP)](https://modelcontextprotocol.io) — the open standard for giving AI assistants access to tools. Go from a design conversation straight to a live app.

---

## ⚠️ Before you connect

> [!IMPORTANT]
> **A connected client acts with your Floot account.** Please read this first.

| | |
|---|---|
| 🔓 **Full account access** | Once connected, the client can read and modify **any** project in your Floot account — not just a single project. |
| 📊 **Runs on your Claude or ChatGPT usage** | Building, editing, and publishing count against your Claude or ChatGPT subscription — **not** Floot credits. Only image generation uses a small amount of Floot credits. |
| 🌐 **Publishing makes apps public** | Publishing returns a **live, public URL** that anyone with the link can open. |
| 🔒 **Secrets stay on Floot** | API keys and credentials are entered on **floot.com only** — they are never shown to the AI. |

---

## ✅ Prerequisites

| Requirement | Details |
|---|---|
| **Floot account** | Any Floot account works — free or paid. |
| **Claude** | A **Pro, Max, Team, or Enterprise** plan (required to add a custom connector). |
| **ChatGPT** | A plan with **connectors / developer mode** available. |

---

## 🔌 Connect

Add Floot as a custom connector by pasting the server URL. Pick your client below.

### <picture><img src="https://img.shields.io/badge/-Claude-D97757?style=flat-square" alt="Claude" /></picture>

1. In Claude, open **Settings → Customize → Connectors**.
   _(Pro, Max, Team, or Enterprise plan required to add a custom connector.)_
2. Click **+** and choose **Add custom connector**.
3. Paste the Floot server URL `https://mcp.floot.com/mcp` and click **Add**.
4. Claude opens a browser window — **sign in to Floot** to authorize the connection.
5. In any chat, click **+ → Connectors** and enable **Floot**.

> [!NOTE]
> Floot uses **OAuth 2.0** — your Floot credentials are never shared with Claude.
>
> **On Team or Enterprise?** An organization Owner adds Floot once under **Organization settings → Connectors → Add → Custom → Web**, then each member clicks **Connect**.

### <picture><img src="https://img.shields.io/badge/-ChatGPT-10A37F?style=flat-square" alt="ChatGPT" /></picture>

1. In ChatGPT, open **Settings → Connectors** (enable **developer mode** if your plan requires it).
2. Choose **Add** / **Create** → **custom connector (MCP server)**.
3. Paste the Floot server URL `https://mcp.floot.com/mcp` and confirm.
4. A browser window opens — **sign in to Floot** to authorize the connection (OAuth 2.0).
5. In a chat, enable the **Floot** connector and start building.

> [!NOTE]
> Once Floot is listed in the Claude and ChatGPT directories, you'll be able to add it in **one click** by searching "Floot" — no URL needed.

<details>
<summary><strong>Other MCP clients (Cursor, VS Code, Windsurf, …)</strong></summary>

<br/>

Floot is a standard remote MCP server, so any MCP-capable client can connect. Claude and ChatGPT are officially supported today; support for more clients is on the way.

**Cursor** currently needs the [`mcp-remote`](https://www.npmjs.com/package/mcp-remote) bridge, because its OAuth callback uses a custom URI scheme the server doesn't accept yet. The bridge authenticates over `http://localhost` instead. Add [`clients/cursor-mcp-remote.json`](clients/cursor-mcp-remote.json) to `~/.cursor/mcp.json` (global) or `.cursor/mcp.json` (per-project):

```json
{ "mcpServers": { "floot": { "command": "npx", "args": ["-y", "mcp-remote", "https://mcp.floot.com/mcp"] } } }
```

Once native remote OAuth is supported everywhere, you'll be able to use the direct config in [`clients/cursor.json`](clients/cursor.json) and this one-click install:

[![Add to Cursor](https://img.shields.io/badge/Add%20to-Cursor-000000?style=for-the-badge&logo=cursor)](https://cursor.com/install-mcp?name=floot&config=eyJ1cmwiOiJodHRwczovL21jcC5mbG9vdC5jb20vbWNwIn0=)

Ready-to-paste configs for other clients live in [`clients/`](clients/):

| Client | Config |
|---|---|
| VS Code (GitHub Copilot) | [`clients/vscode.json`](clients/vscode.json) → `.vscode/mcp.json` |
| Windsurf | [`clients/windsurf.json`](clients/windsurf.json) → `~/.codeium/windsurf/mcp_config.json` |
| Claude Desktop (config-file fallback) | [`clients/claude-desktop.json`](clients/claude-desktop.json) → `claude_desktop_config.json` |
| Any MCP client | [`clients/generic.json`](clients/generic.json) |

</details>

---

## 🧰 What Floot can do

Once connected, your AI assistant can use these tools on your behalf.

| | |
|---|---|
| 📁 **Projects & code** | Create projects, read and edit files, search the codebase, and manage dependencies. |
| 🗄️ **Database** | Provision Postgres, run SQL, inspect the schema, and query your app's data. |
| 🚀 **Preview & publish** | Get a live preview URL, publish to a public URL, and check publish status. |
| 🐞 **Debug & verify** | Read logs, run type checks and tests, and inspect the running app in the browser. |
| 🖼️ **Assets** | Generate images and upload files into a project. |
| 📚 **Guides** | Built-in guides teach the assistant Floot's design system and primitives for higher-quality output. |

---

## 💬 Try these prompts

> Create a Floot app called **"Feedback Hub"** with a form that saves responses to a database.

> Add a login page to my Floot project.

> Publish my project and give me the live URL.

> Something's failing in my app — read the logs and fix it.

---

## 🛠️ Troubleshooting & FAQ

<details>
<summary><strong>"There was a problem connecting"</strong></summary>

<br/>

Make sure the URL ends in **`/mcp`** — the full address is `https://mcp.floot.com/mcp`. The root domain will not connect correctly.

</details>

<details>
<summary><strong>The Floot tools don't appear</strong></summary>

<br/>

Confirm you finished the Floot **sign-in** step, and that the connector is **enabled for the current chat** (Claude: **+ → Connectors**). If needed, remove and re-add the connector to re-authorize.

</details>

<details>
<summary><strong>Does it use Floot credits?</strong></summary>

<br/>

No — the AI work runs on your own Claude or ChatGPT subscription, so building and editing don't spend Floot credits. The one exception is **image generation**, which uses a small amount of credits. _(Limits for free accounts are still being finalized.)_

</details>

<details>
<summary><strong>Which clients are supported?</strong></summary>

<br/>

**Claude** (Desktop on macOS/Windows and claude.ai) and **ChatGPT**. Other MCP clients such as **Cursor** can connect via the [bridge above](#-connect); broader native support is on the way.

</details>

<details>
<summary><strong>Is it stable?</strong></summary>

<br/>

The connector is in **beta**. Tool names, parameters, and behavior may change while we iterate.

</details>

---

## 📖 What is MCP?

The [Model Context Protocol](https://modelcontextprotocol.io) is an open standard that lets AI apps connect to external tools and data through a single interface. A Floot MCP connection gives your assistant the tools to scaffold, build, and host full-stack apps directly from your chat.

## 📁 Repository layout

```
clients/                     Ready-to-paste config for MCP clients
mcp.json                     Generic MCP server definition
.cursor-plugin/plugin.json   Cursor Marketplace plugin manifest
assets/logo.svg              Logo
```
