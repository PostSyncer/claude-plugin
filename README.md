# PostSyncer Plugin

Schedule, publish, and analyze social media posts from Claude Code, Claude Cowork, Cursor, and Grok Build — across **11 platforms**: X (Twitter), Instagram, Facebook, LinkedIn, TikTok, YouTube, Threads, Bluesky, Mastodon, Pinterest, and Telegram.

The plugin bundles the official **PostSyncer MCP server** (`https://postsyncer.com/mcp`) plus a skill that teaches Claude the full PostSyncer workflow: workspaces, connected accounts, posts (publish now / schedule / draft / repeat), threads, first comments, media library, campaigns, labels, comment moderation, and performance analytics.

## Install

From the Claude plugin directory:

```bash
claude plugin install postsyncer
```

Or directly from this repo:

```bash
claude plugin marketplace add PostSyncer/claude-plugin
claude plugin install postsyncer@postsyncer
```

### Cursor

Install from the [Cursor Marketplace](https://cursor.com/marketplace), or clone this repo into `~/.cursor/plugins/local/postsyncer` and run **Developer: Reload Window**. The manifest lives in `.cursor-plugin/plugin.json`.

### Codex

```bash
codex plugin marketplace add PostSyncer/claude-plugin
```

The Codex manifest lives in `.codex-plugin/plugin.json`; the plugin is also listed in the ChatGPT/Codex plugin directory as **PostSyncer**.

### Gemini CLI

```bash
gemini extensions install https://github.com/PostSyncer/claude-plugin
```

### Any MCP client

Point your client at `https://postsyncer.com/mcp` (Streamable HTTP). The server is published in the [official MCP Registry](https://registry.modelcontextprotocol.io) as `io.github.PostSyncer/postsyncer`.

### Grok Build

Install from the [xAI plugin marketplace](https://github.com/xai-org/plugin-marketplace) (`postsyncer`). The Claude-format manifest in `.claude-plugin/plugin.json` is used as-is.

## Authenticate

Sign in with OAuth: run `/mcp` inside Claude Code, select `postsyncer`, and click authenticate. You log in to PostSyncer once in the browser, and Claude stores and refreshes the session for you.

## Try it

- *"List my connected social accounts"*
- *"Schedule a post to LinkedIn and X for tomorrow at 9am announcing our new feature"*
- *"Upload these product shots and draft an Instagram carousel with the link in a first comment"*
- *"How did last week's posts perform across all my workspaces?"*
- *"Repeat this post every Monday for a month"*

## What's included

| Component | Description |
|---|---|
| MCP server | Remote HTTP server at `postsyncer.com/mcp` with ~50 tools mirroring PostSyncer REST API v1 |
| `postsyncer` skill | Workflow guidance: discovery, media prep, posting rules, threads, first comments, scheduling, repeats, analytics, moderation |

## Network and permissions

This plugin ships no scripts, hooks, or local binaries. Its only component besides the skill file is a remote MCP server:

| Endpoint | Purpose |
|---|---|
| `https://postsyncer.com/mcp` | The PostSyncer MCP server (Streamable HTTP). All tool calls go here. |
| `https://postsyncer.com/oauth/*` | OAuth 2.0 sign-in. |

Sign-in is OAuth only. The MCP server only accesses the PostSyncer workspaces the signed-in account can see.

Privacy policy: https://postsyncer.com/privacy-policy

## Links

- Website: https://postsyncer.com
- Docs: https://docs.postsyncer.com
- Support: support@postsyncer.com

## License

MIT
