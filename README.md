# PostSyncer Plugin

Schedule, publish, and analyze social media posts from Claude Code, Claude Cowork, Cursor, and Grok Build — across **12 platforms**: X (Twitter), Instagram, Facebook, LinkedIn, TikTok, YouTube, Threads, Bluesky, Mastodon, Pinterest, Telegram, and Google Business Profile.

The plugin bundles the official **PostSyncer MCP server** (`https://postsyncer.com/mcp`) plus a skill that teaches Claude the full PostSyncer workflow: workspaces and their brand voice, connected accounts, posts (publish now / schedule / draft / repeat), threads, first comments, approvals, media library, saved snippets and hashtag groups, campaigns, labels, comments, Google reviews, webhooks, and performance analytics.

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

Clone this repo into `~/.cursor/plugins/local/postsyncer` and run **Developer: Reload Window**. The manifest lives in `.cursor-plugin/plugin.json`.

To add only the MCP server, open this one-click link in your browser. It opens Cursor's install screen with PostSyncer filled in:

```text
cursor://anysphere.cursor-deeplink/mcp/install?name=PostSyncer&config=eyJ1cmwiOiJodHRwczovL3Bvc3RzeW5jZXIuY29tL21jcCJ9
```

### Codex

```bash
codex plugin marketplace add PostSyncer/claude-plugin
```

The Codex manifest lives in `.codex-plugin/plugin.json`. PostSyncer is also in the [plugin directory](https://chatgpt.com/plugins/plugin_asdk_app_6a632759aaf08191bf66f22649ac22cd) that ChatGPT and Codex share.

### Gemini CLI

```bash
gemini extensions install https://github.com/PostSyncer/claude-plugin
```

### Any MCP client

Point your client at `https://postsyncer.com/mcp` (Streamable HTTP). The server is published in the [official MCP Registry](https://registry.modelcontextprotocol.io) as `io.github.PostSyncer/postsyncer`.

### Grok Build

Pending in the [xAI plugin marketplace](https://github.com/xai-org/plugin-marketplace) (`postsyncer`). The Claude-format manifest in `.claude-plugin/plugin.json` is used as-is.

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
| MCP server | Remote HTTP server at `postsyncer.com/mcp` with every PostSyncer API v1 action as a tool (79 today) |
| `postsyncer` skill | Workflow guidance: brand voice first, discovery, media prep, posting rules, threads, first comments, scheduling, repeats, approvals, snippets, comments, Google reviews, webhooks, analytics, plans |

## Network and permissions

This plugin ships no scripts, hooks, or local binaries. Its only component besides the skill file is a remote MCP server. These are the addresses it uses:

| Endpoint | Purpose |
|---|---|
| `https://postsyncer.com/mcp` | The PostSyncer MCP server (Streamable HTTP). All tool calls go here. |
| `https://postsyncer.com/oauth/*` | OAuth 2.0 sign-in. |
| `https://app.postsyncer.com/upload/*` | An upload link's page, made by the `create-media-upload-link` tool for a file Claude can't pass to PostSyncer. The user opens it in their browser and picks the files to add to their PostSyncer media library. It needs no PostSyncer sign-in, only uploads, and works for 1 hour and up to 10 files. `*` is the link's code. |
| `https://postsyncer.com/api/media-upload-links/*/files` | Where an upload link takes files. Only in an app that can run commands, like Claude Code, the skill may send the file the user chose here with `curl`, instead of the user opening the page. The file goes to the user's PostSyncer media library and nowhere else. It needs no PostSyncer sign-in; `*` is the link's code. |

Sign-in is OAuth only. The MCP server only accesses the PostSyncer workspaces the signed-in account can see.

Privacy policy: https://postsyncer.com/privacy-policy

## Links

- Website: https://postsyncer.com
- Docs: https://docs.postsyncer.com
- Support: support@postsyncer.com

## License

MIT
