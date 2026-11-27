# PostSyncer Plugin

Schedule, publish, and analyze social media posts from Claude Code, Claude Cowork, Cursor, Codex, Gemini CLI and Grok Build — across **12 platforms**: X (Twitter), Instagram, Facebook, LinkedIn, TikTok, YouTube, Threads, Bluesky, Mastodon, Pinterest, Telegram, and Google Business Profile.

The plugin bundles the official **PostSyncer MCP server** (`https://postsyncer.com/mcp`) plus a skill that teaches Claude the full PostSyncer workflow: workspaces, their settings and brand voice, connected accounts, posts (publish now / schedule / draft / repeat), threads, first comments, approvals, media library, saved snippets and hashtag groups, campaigns, labels, comments, Google reviews, webhooks, performance analytics, the team, notifications, blog-to-social feeds and products.

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
- *"Invite sam@example.com to my workspace as a Content Creator"*

## What's included

| Component | Description |
|---|---|
| MCP server | Remote HTTP server at `postsyncer.com/mcp` with PostSyncer's API v1 actions as tools (116 today) |
| `postsyncer` skill | Workflow guidance: brand voice first, discovery, media prep, posting rules, threads, first comments, scheduling, repeats, approvals, snippets, comments, Google reviews, webhooks, analytics, plans |

## AI features

A few tools pass your request to an AI model that writes the answer. These models are PostSyncer's, not the Claude you are chatting with: PostSyncer runs them on its own account, with Anthropic as its main provider.

- `analyze-twitter-post`: an AI model answers your question about a public X post and its replies.
- `analyze-video`: an AI model watches a video and returns its transcript, on-screen text, scenes and an answer to your question.
- `update-post-comment-moderation`: with AI checks or AI replies switched on, an AI model reads a post's new comments and writes the replies.
- `get-brand`: the brand profile and the weekly learnings it returns are written by an AI model.
- `create-blog-source` and `update-blog-source`: a blog feed's posts are written from each new article by an AI model, from the workspace owner's AI credits, on paid plans.

## What the tools can change

Most tools only read. These change things in PostSyncer or on your social accounts. The server tells Claude to confirm with you before publishing right away or deleting.

- **Publish and schedule:** `create-post` and `update-post` publish or schedule posts on your connected accounts. `approve-post` publishes or schedules a post that waits for approval. `put-back-account-posts` puts a reconnected account back on its scheduled posts.
- **Post in public:** `create-comment`, answering a comment from the network, posts a reply there. `reply-to-review` posts a public reply to a Google review and replaces any earlier one. `update-post-auto-plug` posts a follow-up reply once a post reaches a number you set.
- **Hide and delete:** `hide-comment` hides a comment on its network. Each `delete-*` tool removes what it names for good: posts, media, folders, labels, campaigns, snippets, comments, review replies, webhooks, workspaces (with their posts, accounts and analytics), API keys, notification channels, blog feeds, products, contacts, contact notes and contact lists. `delete-account` disconnects a social account, and `remove-team-member` takes someone out of a workspace.
- **Comments, brand and settings:** `update-post-comment-moderation` sets rules that hide or delete comments and AI replies. `update-post-contact-collection` adds a post's commenters to a contact list. `update-brand` and the other `update-*` tools change what they name.
- **Access and outside addresses:** `create-account-connect-link` makes a link where someone connects social accounts to your workspace without a PostSyncer login. `create-webhook`, `update-webhook` and `test-webhook` send events to an https address you choose. `create-media-upload-link` makes an upload page (below).
- **Team:** `invite-team-member` emails an invitation to the address you give and makes an account for it when there is none. `update-team-member` changes a role, or emails the invitation again.
- **Workspaces:** `create-workspace` makes a workspace you own. `update-workspace-settings` changes its name, time zone, posting times and what new posts start with.
- **Notifications:** `create-notification-connect-link` makes a link to connect Slack, Discord or Telegram. `create-notification-destination` sends the workspace's notifications to a Slack channel, and `test-notification-destination` sends a test message there. `delete-notification-destination` stops them; PostSyncer's Discord webhook then leaves the channel and its bot leaves a Telegram group.
- **Blog feeds:** `create-blog-source` turns a blog's new articles into posts on the accounts you pick, saved as drafts or scheduled on their own (`DAILY` or `AUTO_QUEUE`).
- **Contacts, products and your profile:** `update-contact` and `update-contact-lists` change the team's notes and lists, `create-product` and `update-product` change the products posts can promote, and `update-profile` changes your name.

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
- Docs: https://postsyncer.com/docs
- Support: support@postsyncer.com

## License

MIT
