# AUTH.md - Restacked Authentication Model

## Prototype (Current)

**User account:** Single account - Tim's personal GitHub account and token.
No multi-user auth system in prototype.

**GitHub access:** Personal Access Token (PAT) provided manually.
Token scoped to: repo read, repo write (for auto-commit of generated files).
Token stored server-side in the MCP backend during the session.

**Default repo:** Restacked maintains a backend-managed GitHub repo.
Users who have not connected their own repo use this by default.
No auth required to use the default repo.

---

## Launch (Planned)

**User account:** Restacked account created via GitHub OAuth.
GitHub is the primary identity layer. No separate username/password system.

**GitHub OAuth flow:**
1. User clicks "Connect GitHub" on restacked.ai.
2. Redirected to GitHub OAuth.
3. Grants Restacked read/write access to selected repos.
4. Token stored server-side. Refreshed automatically.
5. User returns to the onboarding site. Repo selection available.

**Scopes required:**
- repo (read and write for private repos)
- user:email (for account identification)

**Session auth:**
The MCP server identifies the user via a session token passed at connection time.
The AI client does not handle auth directly. Auth happens at the MCP config level.

---

## Permission Model

**Prototype:** Single user, full access, no restrictions.

**Launch:**
- Users can only access their own connected repos.
- No team or org accounts at launch.
- No shared repos between users at launch.
- Restacked-managed default repo is read/write for all users (sandboxed per user).

---

## What Restacked Does Not Own

- The user's GitHub account.
- The user's repo content beyond the context files.
- Any RAG or vector store the user connects (Layer 1).

---

## Security Notes

- PAT stored server-side, never exposed to client or AI client.
- Auto-commit of generated files requires write scope. User is informed during onboarding.
- User can revoke access at any time via GitHub settings.
- No context file content is logged or stored beyond the GitHub repo.
