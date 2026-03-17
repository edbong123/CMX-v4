# Restacked - AI Context System

This repository contains the context system for Restacked. It gives any AI client accurate, structured knowledge about this project before a single line of code is written.

---

## How It Works

Add `mcp.restacked.ai` to your AI client's MCP config once. Type `make it so` to start. Your AI knows the project.

All context lives here as plain markdown files. GitHub is the source of truth. No dashboard, no editor, no lock-in.

---

## Start Here

If you are an AI working on this project, read `INTENT-BUILD-RESTACKED.md` first. Always.

If you are a human, the file structure is:

| File | Purpose |
|------|---------|
| `llms.txt` | Master index. Entry point for every AI session. |
| `INTENT-BUILD-RESTACKED.md` | Full project context in one file. Read first. |
| `STACK.md` | Tools, frameworks, deployment, what is not in scope. |
| `ARCHITECTURE.md` | Three-layer model, session flows, bootstrap, self-improvement loop. |
| `DOMAIN.md` | Terminology, business rules, user types, non-negotiables. |
| `UX-PATTERNS.md` | User flows, "make it so" trigger, anti-patterns. |
| `AUTH.md` | GitHub auth model, prototype vs launch. |
| `COMPETITORS.md` | Market context, what exists, what to learn from. |

---

## Setup

1. Add the MCP server to your AI client:

```
mcp.restacked.ai
```

2. Open your AI client (Claude, Cursor, or any MCP-compatible tool).

3. Type:

```
make it so
```

4. Follow the prompts. Your context will be loaded automatically.

---

## Updating Context

If the AI detects a gap mid-session, it will flag it and propose an updated file. Confirm and the file is committed here automatically.

To manually trigger an update, type `make it so` and ask to regenerate a specific file.

Only the affected file is updated. Others are left unchanged.

---

## File Ownership

Files in this repo are generated and maintained by Restacked via MCP. You can edit them directly in GitHub at any time. Changes take effect in the next session.

---

## About Restacked

Restacked is an AI context and orchestration platform. One MCP URL. Structured context. Self-improving. Built for vibe coders and advanced AI users alike.

restacked.ai
