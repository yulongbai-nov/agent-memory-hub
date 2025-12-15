# Identity + Shared Memory

## Goal

Copilot Chat and Codex should share the same durable “user memory”. This requires both clients to use the same user-scope `group_id`.

## Recommended approach: GitHub login

Use a stable key derived from GitHub login:

- `github_login:<login>`

Then resolve the canonical group id:

```bash
curl -sS http://graph:8000/groups/resolve \
  -H 'content-type: application/json' \
  -d '{"scope":"user","key":"github_login:<login>"}'
```

### Where to get `<login>`

- CLI: parse from `gh auth status`
- VS Code: the GitHub auth session account label is typically the same login

## Why not email?

Email is often unavailable, sensitive, or inconsistent across providers. Prefer non-PII stable identifiers when possible.

