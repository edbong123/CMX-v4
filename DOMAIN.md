# DOMAIN.md - Restacked Domain Model and Terminology

## Core Problem
AI coding assistants have no persistent, structured knowledge of the project they are working on. Every new session starts from zero. Users repeat themselves. Context degrades. Hallucinations increase. The AI makes decisions without knowing architecture, constraints, or prior decisions.

## Core Solution
Restacked generates and maintains a structured set of markdown files that live in GitHub. These files are served to any AI client via a single MCP endpoint. The AI always has accurate, curated, project-specific context before it writes a single line of code.

---

## Terminology

**Context System**
The full set of files generated for a project. Includes llms.txt, Layer 2 files, and one or more Layer 3 Intent files.

**Layer 2 Files**
Core context files. Stable. Project-specific. Generated once during bootstrap, updated only when the project changes or a gap is found. These are the files a senior developer would need to onboard without asking questions.

**Layer 3 / Intent File**
Specialized context for a specific task. References Layer 2 for depth. Regenerated when the task changes. Naming: INTENT-[PURPOSE].md.

**Layer 1 / RAG**
Optional retrieval layer. Not owned by Restacked. User plugs in their own vector store or MCP servers. Restacked documents this as an extension point.

**llms.txt**
Master index file. Lives at repo root. Read first. Points to the active Intent file. Lists all Layer 2 files. Contains fallback instructions for when no Intent file matches the current task.

**Bootstrap**
The one-time flow that generates all context files for a new project. Triggered via "make it so" in the AI client. Involves research, gap questions, and file generation.

**Self-Improvement Loop**
The ongoing process of detecting context gaps and updating files. Triggered by the user or the AI. Changes auto-commit to GitHub with user confirmation.

**"Make it so"**
The trigger phrase users type in their AI client to initiate MCP-guided setup, bootstrap, or session initialization. Without it, the MCP serves context passively.

**Gap**
A missing or outdated piece of context. When detected, the AI flags it explicitly, proposes a new or updated file, and waits for user confirmation before continuing.

**Default Repo**
A GitHub repo managed by Restacked on the backend. Used for users who have not connected their own GitHub account. Allows zero-friction onboarding.

**Session**
A single conversation in an AI client. At session start (triggered by "make it so"), the user selects which repo to use. The MCP reads llms.txt and serves the appropriate context for that session.

---

## User Types

**Vibe Coder**
Non-technical builder. Uses AI tools like Claude or Cursor to build software without deep programming knowledge. Needs the simplest possible onboarding. Triggered entirely through the chat interface. Cannot be expected to edit YAML, configure MCP manually, or understand file structures.

**Advanced AI User**
Has experience with MCP, AI clients, and prompt engineering. May already use Cursor Rules or llms.txt. Understands the value of structured context immediately. Wants control and portability.

---

## Business Rules

- Context files are the product. Not code, not a UI, not a dashboard.
- GitHub is the only source of truth. No Restacked database holds context.
- The MCP serves files. It does not store them.
- Claude decides the file structure for each project. No fixed template.
- Only generate files relevant to the project. No filler files.
- Never speculate in generated files. Only write what is known.
- Never skip the research phase during bootstrap.
- Never proceed past a phase without completing the current one.
- When a gap is detected, stop and flag it. Do not guess.
- Only regenerate affected files when updating context. Leave others unchanged.

---

## Non-Negotiables

- One MCP URL. No per-project config in the client.
- No dashboard at launch.
- No lock-in. Files are plain markdown in a GitHub repo. User owns them.
- Transparent. Users always see what is served and why.
- Minimal. Every feature must earn its place.
