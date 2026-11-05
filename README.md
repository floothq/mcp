<p align="center">
  <img src="assets/logo.svg" alt="Floot" width="128" height="128" />
</p>

<h1 align="center">Floot MCP Server</h1>

<p align="center">
  <strong>Build and deploy full-stack web and mobile apps from Claude, ChatGPT, Codex or Cursor.</strong>
</p>

<p align="center">
  Your AI assistant writes the code. Floot runs it: database, sign-in, file storage, email, payments, scheduled jobs, a live preview and hosting,<br/>
  plus native iOS and Android builds. The model runs on your existing Claude or ChatGPT subscription.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/protocol-MCP-000000?style=flat-square" alt="Model Context Protocol" />
  <img src="https://img.shields.io/badge/clients-Claude%20%C2%B7%20ChatGPT%20%C2%B7%20Codex%20%C2%B7%20Cursor-000000?style=flat-square" alt="Clients" />
  <img src="https://img.shields.io/badge/transport-Streamable%20HTTP%20%2B%20OAuth-000000?style=flat-square" alt="Transport" />
</p>

<p align="center">
  <a href="#-connect">Connect</a> ·
  <a href="#-what-floot-can-do">Capabilities</a> ·
  <a href="#-try-these-prompts">Prompts</a> ·
  <a href="#-what-it-costs">Cost</a> ·
  <a href="#️-troubleshooting--faq">FAQ</a>
</p>

---

## 🔗 Server URL

```
https://mcp.floot.com/mcp
```

> [!TIP]
> In Claude, ChatGPT and Cursor you don't need the URL: install Floot from their directories (below). For other clients, the URL must end in **`/mcp`**. It's an MCP endpoint, not a web page, so it won't open in a browser.

It connects over the [Model Context Protocol (MCP)](https://modelcontextprotocol.io), the open standard for giving AI assistants access to tools. Go from a conversation straight to a live app.

---

## ⚠️ Before you connect

> [!IMPORTANT]
> **A connected client acts with your Floot account.** Please read this first.

| | |
|---|---|
| 🔓 **Full account access** | Once connected, the client can read and modify **any** project in your Floot account, not just one. |
| 📊 **The model runs on your AI subscription** | Model usage comes from your Claude or ChatGPT plan. Floot counts tool calls as build actions (see [What it costs](#-what-it-costs)). |
| 🌐 **Publishing makes apps public** | Publishing returns a **live, public URL** that anyone with the link can open, unless you publish internally (sign-in required). |
| 🔒 **Secrets stay on Floot** | API keys and credentials are entered on **floot.com only**. They are never shown to the AI. |

---

## ✅ Prerequisites

| Requirement | Details |
|---|---|
| **Floot account** | Any Floot account, free or paid. Sign in with an emailed code, Google, GitHub or Microsoft. |
| **Claude** | Any Claude plan can add Floot, including Claude Free. A paid plan is recommended for real builds. |
| **ChatGPT / Codex** | A ChatGPT account. Codex uses the same account. |
| **Other clients** | Any client that supports remote MCP servers over Streamable HTTP with OAuth sign-in. |

---

## 🔌 Connect

### <picture><img src="https://img.shields.io/badge/-Claude-D97757?style=flat-square" alt="Claude" /></picture>

1. Open [Floot in the Claude connector directory](https://claude.ai/directory/connectors/floot-mcp-updated) and click **Connect**.
2. **Sign in to Floot** in the browser window that opens.
3. Mention Floot in a chat, for example: "build me a feedback hub with Floot".

> [!NOTE]
> **On Team or Enterprise?** An organization Owner enables Floot once (from the directory, or **Organization settings → Connectors**), then each member clicks **Connect**.
>
> For long builds in the Claude web app, use **Cowork** mode rather than Chat.

**Claude Code:**

```bash
claude mcp add --transport http floot https://mcp.floot.com/mcp
```

### <picture><img src="https://img.shields.io/badge/-ChatGPT-10A37F?style=flat-square" alt="ChatGPT" /></picture>

1. Open the [Floot app in the ChatGPT directory](https://chatgpt.com/plugins/plugin_asdk_app_6a500d350f8c819194e30335a7b134af) and click **Install**.
2. **Sign in to Floot** when prompted.
3. Add Floot from the **+** / tools menu, or start your message with **@Floot**.
4. Turn off per-action approval in Floot's app settings. ChatGPT asks before every action by default, and a build makes dozens.

**Codex** shares your ChatGPT account, so Floot is available there once ChatGPT has it. You can also search **Floot** in Codex's plugin registry.

### <picture><img src="https://img.shields.io/badge/-Cursor-000000?style=flat-square" alt="Cursor" /></picture>

Open [Floot in the Cursor Marketplace](https://cursor.com/marketplace/floot), add it, and sign in to Floot when prompted. Or add it by hand with [`clients/cursor.json`](clients/cursor.json):

```json
{ "mcpServers": { "floot": { "url": "https://mcp.floot.com/mcp" } } }
```

<details>
<summary><strong>Other MCP clients (VS Code, Windsurf, Gemini CLI, Raycast, …)</strong></summary>

<br/>

1. Add a remote MCP server and choose transport **Streamable HTTP**.
2. Enter `https://mcp.floot.com/mcp`. **Leave any bearer-token or header fields empty.** Floot signs you in with OAuth.
3. Sign in to Floot in the browser window that opens, then enable Floot's tools.

Ready-to-paste configs live in [`clients/`](clients/):

| Client | Config |
|---|---|
| VS Code (GitHub Copilot) | [`clients/vscode.json`](clients/vscode.json) → `.vscode/mcp.json` |
| Windsurf | [`clients/windsurf.json`](clients/windsurf.json) → `~/.codeium/windsurf/mcp_config.json` |
| Claude Desktop (config-file fallback) | [`clients/claude-desktop.json`](clients/claude-desktop.json) → `claude_desktop_config.json` |
| Any MCP client | [`clients/generic.json`](clients/generic.json) |

Full guide: [floot.com/docs/integrations/other-mcp-clients](https://floot.com/docs/integrations/other-mcp-clients).

</details>

---

## 🧰 What Floot can do

Your assistant builds the app with these tools, and the app you publish gets these services, with no extra accounts or API keys to set up.

**Building**

| | |
|---|---|
| 📁 **Projects & code** | Create projects, read, write and patch files, search the code, and add npm packages. |
| 👀 **Live preview** | A shareable preview link from the first edit, plus screenshots and in-browser checks. |
| 🐞 **Debug & verify** | Read server logs, run type checks and tests, and run code in the browser or a VM. |
| ⏪ **History** | Checkpoints and earlier versions of any file, so changes can be undone. |

**What your app gets**

| | |
|---|---|
| 🗄️ **Database** | Managed Postgres. Query it, run SQL and pull the schema from the chat. |
| 🔐 **Sign-in** | Email and password, plus Google and Microsoft sign-in. |
| 📦 **File storage** | Uploads and files served from your app. |
| ✉️ **Email** | Send and receive email, from your own domain on paid plans. |
| 🔔 **Push notifications** | For web apps and native mobile apps. |
| 💳 **Payments** | Stripe checkout and subscriptions. |
| ⏰ **Scheduled & background jobs** | Recurring jobs and queued tasks that run on their own. |
| ⚡ **Live updates** | Realtime data so screens update without polling. |
| 🤖 **AI features** | Text and image generation, transcription and more, inside your app. |
| 🔗 **Integrations** | Connect Google and Microsoft accounts, or any API with your own key. |

**Publishing**

| | |
|---|---|
| 🚀 **Web** | Publish to a floot.app address in one step, or your own domain on paid plans. Publish internally to limit an app to people you invite. |
| 📱 **iOS & Android** | Build native apps and submit them to the App Store and Google Play, with no Mac needed. |

---

## 💬 Try these prompts

> Use Floot to build a client portal where customers sign in and see their invoices, then publish it.

> Build a booking app for my coaching practice with Floot: clients pick a free slot and get an email confirmation.

> Add a database and user login to this app with Floot, and keep each user's notes private to them.

> Make my Floot app into an iPhone and Android app.

> Something's failing in my app. Read the Floot logs, fix it and republish.

---

## 💸 What it costs

- **Model usage** comes from your Claude or ChatGPT subscription. Floot charges no credits for it.
- **Build actions:** Floot counts one build action per tool call your assistant makes. Failed and cancelled calls don't count, and a few status tools are always free. Free accounts get **100 build actions a day**; paid plans raise the daily cap.
- **Image generation** is the one action that also spends Floot credits.
- **Publishing** to a floot.app address is free. Custom domains, code download and live payments are on paid plans; database export works on every plan.

Current plans: [floot.com/pricing](https://floot.com/pricing).

---

## 🛠️ Troubleshooting & FAQ

<details>
<summary><strong>"There was a problem connecting"</strong></summary>

<br/>

If you added Floot by URL, make sure it ends in **`/mcp`**: `https://mcp.floot.com/mcp`. Leave bearer-token and header fields empty. Floot accepts OAuth with PKCE `S256` only, so a client that offers no PKCE (or only `plain`) can't connect.

</details>

<details>
<summary><strong>The Floot tools don't appear</strong></summary>

<br/>

Confirm you finished the Floot **sign-in** step and that Floot is **enabled for the current chat** (Claude: **+ → Connectors**; ChatGPT: the **+** / tools menu). If the tool list looks stale, remove and re-add the connector.

</details>

<details>
<summary><strong>ChatGPT stops every few seconds to ask permission</strong></summary>

<br/>

Turn off per-action approval in Floot's app settings in ChatGPT. A build makes dozens of actions.

</details>

<details>
<summary><strong>Which clients are supported?</strong></summary>

<br/>

**Claude** (web, desktop and Claude Code), **ChatGPT**, **Codex** and **Cursor** have one-click installs. Any client that supports remote MCP servers with OAuth sign-in can connect by URL, including VS Code Copilot, Windsurf, Gemini CLI, Raycast and LM Studio.

</details>

<details>
<summary><strong>Can I take my app elsewhere?</strong></summary>

<br/>

Yes. Database export works on every plan, and paid plans can download the full project. See [Code, data and exports](https://floot.com/docs/faqs/code-data-and-exports).

</details>

---

## 📖 What is MCP?

The [Model Context Protocol](https://modelcontextprotocol.io) is an open standard that lets AI apps connect to external tools and data through a single interface. A Floot MCP connection gives your assistant the tools to build, run and publish full-stack apps directly from your chat.

Floot is listed in the [official MCP Registry](https://registry.modelcontextprotocol.io) as `com.floot/floot`.

## 📁 Repository layout

```
clients/                     Ready-to-paste config for MCP clients
mcp.json                     Generic MCP server definition
.cursor-plugin/plugin.json   Cursor Marketplace plugin manifest
assets/logo.svg              Logo
```

More: [floot.com/docs](https://floot.com/docs)
