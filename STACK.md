# STACK.md - Restacked Tech Stack

## Primary Build Tool
**V0 (vercel.com/v0)**
Used to build the marketing site, onboarding flow, and bootstrap UI.
Target users include non-technical vibe coders, so the UI must work without developer knowledge.
V0 generates React/Next.js. Deploy target: Vercel.

## MCP Server
**Protocol:** Model Context Protocol (MCP) - open standard by Anthropic, now under Linux Foundation.
**Transport:** Streamable HTTP (not SSE - deprecated).
**Endpoint:** Single public URL - mcp.restacked.ai
**Auth at session level:** Token passed per user session. No per-tool auth prompts.
**Implementation language:** To be determined. TypeScript preferred for MCP server work given ecosystem maturity.

## GitHub Integration
**Source of truth:** All context files live in GitHub repos.
**Prototype auth:** Personal Access Token (PAT) provided by user.
**Launch auth:** GitHub OAuth.
**Default repo:** Restacked maintains a backend-managed default GitHub repo for users who have not connected their own.
**File operations at launch:** User edits MD files directly in GitHub.
**File operations post-launch:** Simplified web-based file manager (V0-built).

## Context Files
**Format:** Markdown (.md)
**Structure:** Flat files at repo root.
**Entry point:** llms.txt (master index).
**Layer 2:** Core context files (STACK.md, SCHEMA.md, etc.) - stable, project-specific.
**Layer 3:** Intent files (INTENT-*.md) - task-specific, regenerated on demand.
**Layer 1:** RAG - user-supplied, Restacked does not own this layer.

## AI Client Compatibility
Target clients at launch: Claude (claude.ai), Cursor, any MCP-compatible client.
No client-side UI control. Restacked cannot push UI to the client.
All interaction happens through MCP tool calls triggered by user prompts.

## Trigger Mechanism
User types "make it so" in their AI client to initiate MCP-guided setup and bootstrap.
Without the trigger, the MCP server serves context passively.

## Deployment
**Frontend:** Vercel (via V0 export).
**MCP server:** To be hosted separately. Domain: mcp.restacked.ai.
**GitHub:** All context stored in user repos or Restacked-managed default repo.

## Not In Stack At Launch
- No RAG layer (user brings their own)
- No billing system
- No team/org accounts
- No analytics
- No custom domain per user
