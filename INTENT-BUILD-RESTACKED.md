# Intent: AI Context System for Software Projects

## Summary
Restacked is a layered context delivery platform that generates, stores, and serves structured markdown files to any MCP-compatible AI client via a single hosted endpoint (mcp.restacked.ai). It solves the core failure mode of AI-assisted development: the AI has no persistent, structured knowledge of the project it is working on. Every session starts from zero. Restacked fixes this by bootstrapping a curated set of context files through a research-backed flow, committing them to GitHub, and serving them on demand. The system improves over time through a self-improvement loop triggered by detected gaps. Target users are two distinct groups: non-technical vibe coders who trigger everything through a single phrase ("make it so") in their AI client, and advanced AI users who understand MCP and want portable, structured context that works across tools. Built with V0 (frontend) and a custom MCP server. GitHub is the only persistence layer. No dashboard, no editor, no project management - just context files that work.

---

## Key Context

- The system uses three layers: Layer 2 (core context files, always served), Layer 3 (intent files, served per task), Layer 1 (RAG, optional, user-supplied).
- llms.txt is the master index. Every AI working on a project reads it first.
- Bootstrap is triggered by "make it so" in the AI client. The MCP guides the user through a research-backed flow and generates all files.
- Files live in GitHub. Restacked manages a default repo for users without their own. Users with GitHub accounts connect via PAT (prototype) or OAuth (launch).
- The MCP cannot push UI to the client. All interaction is via text and tool calls within the existing AI client conversation.
- Restacked cannot know which repo a user wants at session start without asking. "Make it so" is the initialization trigger.
- File edits in prototype: directly in GitHub. Post-launch: V0-built web file manager.
- Self-improvement loop: AI flags gap, proposes file, user confirms, MCP commits to GitHub.
- Pricing: free at launch, usage-based later.

---

## References

- Stack and tooling: see STACK.md
- System architecture and flows: see ARCHITECTURE.md
- Business rules and terminology: see DOMAIN.md
- User flows and UX patterns: see UX-PATTERNS.md
- Auth model: see AUTH.md
- Competitive landscape: see COMPETITORS.md

---

## Constraints

- One MCP URL. No per-project config required in the client.
- Restacked cannot push UI to the AI client. Text and tool calls only.
- GitHub is the only source of truth. No Restacked database holds context.
- No dashboard at launch.
- No team or org accounts at launch.
- No billing at launch.
- Bootstrap must include autonomous research. Never generate files without researching the space first.
- Never speculate in generated files. Only write what is known.
- When a gap is detected, stop and flag it. Do not guess.
- Only regenerate affected files when updating. Leave others unchanged.
- V0 is the build tool for all frontend. No custom React outside V0 at launch.

---

## Market Context
The AI context tooling space is early and mostly free. GitMCP serves raw docs passively. ContextStream builds a local knowledge graph. Context7 injects library docs. Cursor Rules are manually written. None of them generate structured, layered, research-backed context files through a bootstrap flow and serve them via a single MCP endpoint with a self-improvement loop. The closest behavior to Restacked is developers manually maintaining .cursorrules files - Restacked automates and formalizes that pattern. See COMPETITORS.md for full analysis.

---

## Current State

**Built:**
- System architecture defined.
- Three-layer model designed.
- Bootstrap flow designed.
- "Make it so" trigger pattern defined.
- Context file structure and naming conventions defined.
- Competitive research complete.

**In progress:**
- V0 marketing and onboarding site.
- MCP server implementation.
- GitHub integration (PAT-based prototype).
- Bootstrap flow implementation in MCP.

**Not yet built:**
- GitHub OAuth for launch.
- Web-based file manager.
- Self-improvement loop (gap detection and auto-commit).
- Usage-based pricing system.
- Multi-user account system.
