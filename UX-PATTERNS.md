# UX-PATTERNS.md - Restacked UX Patterns and User Flows

## Design Constraint
Restacked cannot push UI to the AI client. All MCP interaction happens through tool calls and text responses inside the user's existing AI client (Claude, Cursor, etc.). The web UI (built in V0) handles onboarding and file management only.

---

## Trigger Pattern: "Make it so"

The single phrase that activates MCP-guided interaction.

Without it: MCP serves context passively whenever the AI client requests it.
With it: MCP initiates a guided flow - setup, bootstrap, or session initialization.

This pattern is critical for non-technical users who do not know how MCP works. They just type the phrase and the system takes over.

Design rule: The phrase must be prominently displayed during onboarding. It is the only thing the user needs to remember.

---

## User Flow 1: First-Time Vibe Coder

1. User lands on restacked.ai (V0-built marketing/onboarding site).
2. User sees: "Add one URL to Claude. Type three words. Your AI knows your project."
3. User copies mcp.restacked.ai into their AI client's MCP config.
4. User opens Claude (or any MCP client).
5. User types: "make it so"
6. MCP responds: "What are you building? Who is it for? What tools are you using?"
7. User answers in plain language.
8. Claude researches autonomously.
9. Claude asks max 5 follow-up questions.
10. Files generated, committed to default Restacked-managed repo.
11. MCP tells user: "Your context is ready. Start building."
12. User continues in the same chat. Claude now has full project context.

---

## User Flow 2: Advanced User with Existing Repo

1. User adds mcp.restacked.ai to their AI client MCP config.
2. User opens their AI client.
3. User types: "make it so"
4. MCP asks: "Connect your GitHub repo? Provide a token or use OAuth."
5. User provides token (prototype) or completes OAuth (launch).
6. MCP reads existing repo. If llms.txt exists, session is initialized.
7. If no llms.txt, bootstrap flow begins (same as Flow 1, step 6+).

---

## User Flow 3: Returning User (Session Start)

1. User opens AI client.
2. User types: "make it so"
3. MCP asks: "Which repo? [lists known repos for this user]"
4. User selects or types repo name.
5. MCP reads llms.txt, loads active Intent file, surfaces Layer 2 context.
6. MCP confirms: "Context loaded for [project name]. Ready."
7. User starts building.

---

## User Flow 4: Gap Detected Mid-Session

1. User is working. AI hits something not covered in context files.
2. AI flags explicitly: "I don't have context for [X]. This might cause errors."
3. AI proposes: "Should I add an INTENT-[X].md file to cover this?"
4. User confirms.
5. MCP generates file, commits to GitHub.
6. Session continues with updated context.

---

## Onboarding Site (V0)

The marketing and onboarding site built in V0. Purpose:
- Explain the product in plain language for vibe coders.
- Show the three-step setup (add URL, type "make it so", start building).
- Provide the MCP URL to copy.
- Link to GitHub for file management (prototype).
- Future: host the simplified file manager.

Copy direction: Plain, direct, no jargon. Target audience has never heard of MCP. Lead with the outcome ("Your AI knows your project") not the mechanism.

---

## File Manager (Post-Launch)

Simple web UI built in V0.
Shows all context files in the connected repo.
User can view, edit, and delete files.
No code editor. Plain text editing only.
Triggered from the onboarding site after auth.
Not in scope for MVP.

---

## Error States

**No repo connected:** MCP uses the default Restacked-managed repo. User is notified.
**Gap detected:** AI stops, flags explicitly, proposes solution, waits for confirmation.
**Bootstrap incomplete:** MCP stores partial state. User can resume with "make it so".
**Token expired:** MCP prompts user to re-authenticate via the onboarding site.

---

## Anti-Patterns (Do Not Do)

- Do not require users to open a dashboard to start a session.
- Do not require users to select a repo before entering the AI client.
- Do not show technical MCP output (JSON, tool call names) to vibe coders.
- Do not let the AI guess when it hits a gap. Always flag and ask.
- Do not regenerate all files when only one needs updating.
