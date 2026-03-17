# ARCHITECTURE.md - Restacked System Architecture

## Overview
Restacked is a layered context delivery system. It serves structured markdown files from GitHub to any MCP-compatible AI client via a single hosted MCP endpoint. Context is generated through a bootstrap flow, stored in GitHub, and improved over time through a self-improvement loop.

---

## Three-Layer Context Model

### Layer 1 - RAG (Not Owned by Restacked)
Optional retrieval layer. User brings their own vector store, embedding pipeline, or additional MCP servers. Restacked does not build or maintain this. It is documented as a pluggable extension point.

### Layer 2 - Core Context Files (Always Served)
Curated, stable markdown files stored in the user's GitHub repo.
Generated during bootstrap. Claude decides the file structure based on project type.
Examples: STACK.md, SCHEMA.md, AUTH.md, ARCHITECTURE.md, DOMAIN.md, COMPETITORS.md.
These files change infrequently. Updated when the project changes or a gap is detected.

### Layer 3 - Intent Files (Served Per Use Case)
Specialized context for a specific task or goal.
File naming convention: INTENT-[PURPOSE].md (e.g., INTENT-AUTH-FLOW.md).
References Layer 2 files for depth.
Regenerated when the task changes or a gap is detected.
Multiple intent files can exist in one repo simultaneously.

---

## Entry Point: llms.txt
Master index file at repo root.
Read first by any AI working on the project.
Points to the active Intent file and lists all Layer 2 files with one-line descriptions.
Contains fallback instructions: if no Intent file fits the current task, generate a new one.

---

## MCP Layer

### Single Endpoint
One URL: mcp.restacked.ai
Added once to any AI client's MCP config.
No per-project config required in the client.

### Session Initialization
Restacked cannot push UI or prompts to the AI client.
User triggers session setup by typing "make it so" in their AI client.
The MCP server responds with guided setup: which repo to use, what context is available.
Without the trigger, the MCP server serves context passively when the AI requests it.

### Repo Selection
At session start (triggered by "make it so"), the MCP asks the user which GitHub repo to connect.
This selection persists for the session.
The MCP then reads llms.txt from that repo and serves the appropriate context files.

### Auth Flow
Prototype: User provides a GitHub Personal Access Token. Restacked uses it to read/write to the repo.
Launch: GitHub OAuth. Token stored server-side, scoped to repo read/write.
Default: Restacked maintains a backend-managed GitHub repo for users who have not connected their own.

---

## Bootstrap Flow (New Project)

1. User adds mcp.restacked.ai to their AI client.
2. User types "make it so" in the client.
3. MCP asks: what are you building, who is it for, what stack?
4. Claude researches autonomously (competitors, patterns, best practices).
5. Claude asks max 5 gap-filling questions.
6. Layer 2 files generated and committed to GitHub repo.
7. Layer 3 Intent file generated and committed.
8. llms.txt generated and committed.
9. User is told: your context is ready. Start building.

---

## Self-Improvement Loop

Trigger 1: User detects a gap and requests an update.
Trigger 2: AI detects a gap mid-session and proposes a new or updated file.

Flow:
1. Gap identified.
2. MCP proposes updated or new file.
3. User confirms.
4. File updated and auto-committed to GitHub.
5. Context improves. Loop repeats.

Only affected files are regenerated. Unaffected files are not touched.

---

## File Ownership

Prototype: User edits generated MD files directly in GitHub.
Launch: Simplified web-based file manager (built in V0, served from Vercel).
MCP can also propose and commit file changes directly via GitHub API (with user confirmation).

---

## Design Constraints

- No dashboard at launch.
- No editor at launch.
- No project management features.
- GitHub is the only persistence layer.
- One MCP URL. Everything else happens in the AI client.
- Transparent: users always see what files exist and what is being served.
- Portable: works with any MCP-compatible client (Claude, Cursor, etc.).
