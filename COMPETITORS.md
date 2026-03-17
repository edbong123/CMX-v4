# COMPETITORS.md - Market Context and Competitive Landscape

## The Gap Restacked Fills

Every existing tool either reads raw code passively, serves library documentation, or requires manual writing. None generate structured, curated, layered context files through a research-backed bootstrap flow, serve them via a single MCP URL, or have a self-improvement loop. Restacked is the only product treating project context as a first-class artifact worth building and maintaining.

---

## Direct Competitors / Adjacent Tools

### 1. GitMCP (gitmcp.io)
**What it does:** Transforms any public GitHub repo into a remote MCP endpoint. AI can read llms.txt, README, and code. Zero setup - swap github.com for gitmcp.io in the URL.
**Pricing:** Free, open-source.
**What it does well:** Frictionless setup. No auth. Instant. Good onboarding model.
**What it misses:** No context generation. No bootstrap. No structured MD files. No self-improvement. Read-only pass-through of whatever is already in the repo. Public repos only.
**Lesson:** The "change one word" onboarding pattern is worth emulating. But they are serving raw docs, not curated context.

### 2. ContextStream (contextstream.io)
**What it does:** MCP server that indexes codebase locally, builds a knowledge graph, surfaces context across sessions and tools. Persistent memory, decision tracking, semantic search.
**Pricing:** Free tier, paid tier unknown.
**What it does well:** Cross-session persistence. "Your AI remembers your architecture" is a strong value prop. Works across Claude, Cursor, Copilot.
**What it misses:** Developer-only. No bootstrap flow. No structured file generation. No non-technical user path. Local setup required (npx). Not portable without their infrastructure.
**Lesson:** Cross-session memory is a real pain point. Restacked solves this differently - via files in GitHub rather than a proprietary knowledge graph.

### 3. Context7 (upstash/context7)
**What it does:** Injects live library documentation into AI prompts via MCP. Say "use context7" and it fetches up-to-date docs for the library you are using.
**Pricing:** Free (1,000 req/month since Jan 2026), $10/month paid.
**What it does well:** The two-word trigger ("use context7") is excellent UX for non-technical users. Live docs prevent hallucinations on fast-moving libraries.
**What it misses:** Library docs only. Zero project-specific context. No GitHub integration. No structured file generation. Cannot tell the AI anything about your project, only about external libraries.
**Lesson:** Simple trigger phrases work for non-technical users. Pricing at $10/month for a context tool is validated.

### 4. DeepWiki by Devin (Cognition)
**What it does:** Free, no-auth remote MCP server. Answers questions about any public GitHub repo using AI.
**Pricing:** Free.
**What it does well:** No auth required. Remote URL. Works instantly. Good for open-source library questions.
**What it misses:** Read-only. No structured context generation. No curated files. No self-improvement. Public repos only. Answers questions about existing code but does not generate or maintain context.
**Lesson:** No-auth remote MCP is the right default for early adoption. Lower the barrier to zero.

### 5. Cursor Rules (.cursorrules / .cursor/rules)
**What it does:** Project-level instruction files stored in the repo. Claude and Cursor read them as persistent instructions. Community-maintained templates exist on GitHub.
**Pricing:** Free, built into Cursor.
**What it does well:** Developers already accept repo-based instruction files. The pattern is proven. Many teams maintain these manually.
**What it misses:** Manual only. Cursor-specific (limited portability). No AI generation. No bootstrap. No layered structure. No MCP. No self-improvement loop.
**Lesson:** The behavior Restacked is formalizing already exists informally. Developers maintain context files by hand. Restacked automates and structures this.

---

## Open Source / Alternative Approaches

**llms.txt standard (llmstxt.org):** Proposed by Jeremy Howard (Answer.AI) in September 2024. Plain markdown file at site root for AI context. Adopted by Anthropic, Cursor, Stripe, Cloudflare, others. Growing standard. Restacked uses this as the entry point file format. Not a competitor - it is the substrate.

**Cursor Rules community templates (github.com/PatrickJS/awesome-cursorrules):** Large collection of manually written .cursorrules files for different stacks. Shows demand for project context templates. Restacked generates these dynamically through research.

---

## What to Avoid

- Do not build a dashboard. ContextStream and others do this. It adds friction.
- Do not require local setup. ContextStream requires npx. Kills non-technical adoption.
- Do not make the user manage multiple MCP URLs per project. One URL is the constraint.
- Do not build library documentation indexing. Context7 owns that space.
- Do not require public repos only. Private repo support via auth is a meaningful differentiator.

---

## Pricing Reference Points

- Context7: $10/month for documentation injection.
- ContextStream: Free tier, paid unknown.
- GitMCP: Free, open-source.
- Cursor Rules: Free (built into tool).

Market is mostly free tools right now. Paid context tooling at $10-$20/month is the emerging range. Usage-based pricing (per bootstrap, per regeneration) is unexplored and likely the right model for Restacked.
