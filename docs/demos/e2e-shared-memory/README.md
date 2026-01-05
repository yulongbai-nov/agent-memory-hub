# Demo: Cross-client Shared Memory (Copilot Chat + Codex)

This demo proves that **Copilot Chat** and **Codex CLI** can share the same Graphiti-backed memories (user + workspace scope), instead of storing them in per-client silos.

## What’s “new” vs “old”

- Old: each client used its own group id namespace, so memories learned in one tool were not recalled by the other.
- New: both clients use canonical `graphiti_*` group ids derived from stable keys (identity + repo), and both also query legacy per-client ids during migration.

## Prereqs

- Graphiti is reachable:
  - `curl -fsS http://graph:8000/healthcheck`
- Both clients use the same endpoint:
  - Copilot Chat setting: `http://graph:8000`
  - Codex config: `graphiti.endpoint = "http://graph:8000"`
- Shared identity:
  - VS Code: logged into GitHub (Copilot Chat uses the GitHub auth session label).
  - Codex: `gh auth status` shows the same login, or set `graphiti.user_scope_key = "github_login:<login>"`.
- Shared workspace identity:
  - Repo has a GitHub remote (e.g. `origin`) so workspace key resolves to `github_repo:<host>/<org>/<repo>`.

## Step 1 — Copilot Chat → Codex recall (user scope)

1. In VS Code, enable Graphiti + consent (see `repos/vscode-copilot-chat/docs/demos/graphiti-memory-integration/README.md`).
2. Send a promoted memory in Copilot Chat (user scope):
   - `preference (user): I prefer rg over grep for searches. marker: shared-memory-<timestamp>`
3. In the same repo, run Codex with Graphiti enabled and Global enabled, then ask:
   - `What is my preference for searching in this repo?`
4. Confirm Codex injects `<graphiti_memory>` containing the preference (or observe the answer referencing it).

## Step 2 — Codex → Copilot Chat recall (user scope)

1. In Codex, send:
   - `preference (global): Keep diffs small and avoid inline comments. marker: shared-memory-<timestamp>`
2. In Copilot Chat, ask:
   - `What is my preference for diffs and comments?`
3. Confirm `<graphiti_memory>` contains the preference (Request Logger recommended).

## Troubleshooting

- **Graphiti is slow**: ingestion is async; wait ~5–15s and retry queries.
- **Identity mismatch**: ensure VS Code GitHub login matches `gh auth status`, or set `graphiti.user_scope_key = "github_login:<login>"`.
- **Workspace mismatch**: ensure both are operating in the same GitHub repo and that `origin` remote is present/consistent.
- **`POST /groups/resolve` returns 404**: older Graphiti build; clients still work via deterministic canonical ids (`graphiti_<scope>_<sha256(key)[:32]>`).

