# PostSyncer Claude Plugin

Schedule, publish, and analyze social media posts from Claude Code and Claude Cowork — across **11 platforms**: X (Twitter), Instagram, Facebook, LinkedIn, TikTok, YouTube, Threads, Bluesky, Mastodon, Pinterest, and Telegram.

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

## Authenticate

Two options:

1. **OAuth (recommended)** — run `/mcp` inside Claude Code, select `postsyncer`, and click authenticate. You log in to PostSyncer once in the browser; no token to paste.
2. **API token** — create a token in the PostSyncer app (Settings → API) with the abilities you need (`workspaces`, `accounts`, `labels`, `campaigns`, `posts`) and configure it as a Bearer token for the `postsyncer` MCP server.

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

## Links

- Website: https://postsyncer.com
- Docs: https://docs.postsyncer.com
- Support: support@postsyncer.com

## License

MIT
