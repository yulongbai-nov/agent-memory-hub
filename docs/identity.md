# Identity + Shared Memory

## Goal

Copilot Chat and Codex should share the same durable “user memory”. This requires both clients to use the same user-scope `group_id`.

## Recommended approach: GitHub login

Use a stable key derived from GitHub login:

- `github_login:<login>`

Canonical group ids are deterministic:

- `graphiti_user_<sha256(key)[:32]>` for user scope
- `graphiti_workspace_<sha256(key)[:32]>` for workspace scope

If the connected Graphiti build supports `POST /groups/resolve`, you can use it to verify the canonical mapping. Older Graphiti builds may return 404; clients fall back to the deterministic formula locally.

### Where to get `<login>`

- CLI: parse from `gh auth status`
- VS Code: the GitHub auth session account label is typically the same login

## Why not email?

Email is often unavailable, sensitive, or inconsistent across providers. Prefer non-PII stable identifiers when possible.
