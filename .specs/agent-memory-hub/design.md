# Design Document: Agent Memory Hub (Central Docs + Version Alignment)

## Overview

The Graphiti memory integration spans multiple repos (Graphiti service, Copilot Chat, Codex). Each repo has its own `.specs/*` and implementation details. This hub repo provides:

- A single “home page” and index into all specs and PRs.
- A big-picture architecture diagram for the end-to-end memory loop.
- Operational guidance (deploy/redeploy Graphiti, healthcheck, debugging).
- Version alignment by pinning the participating repos as git submodules.

### Goals

- Make it easy to understand “what was built” across repos.
- Keep the docs aligned with code versions (submodule commit pins).
- Provide a stable reference for identity + scope semantics and shared-memory conventions.

### Non-goals

- Replace repo-local specs (this hub links to them; it does not duplicate them).
- Provide a production-grade release process (tracked as future work).

## Current Architecture

- Each repo tracks its own specs and PRs independently.
- Cross-repo drift risk exists (schema ids, group id derivation, recall behaviors).
- Reviewers/operators lack a single place to find the “system story”.

## Proposed Architecture

### Documentation hub

This repo contains curated docs:

- `docs/architecture.md`: system-level diagrams and data flow.
- `docs/spec-index.md`: index across repos/specs/PRs.
- `docs/ops.md`: redeploy/debug guidance.
- `docs/identity.md`: how clients derive stable identity keys and group ids.
- `docs/index.html`: GitHub Pages-friendly showcase/presentation of the end-to-end system.
- `docs/demos/e2e-shared-memory/README.md`: end-to-end demo guide across clients.
- `VERSIONS.md`: pinned commit matrix for aligned versions.

### Version alignment via submodules

Add the participating repos as submodules under `repos/` and pin them to the commits that correspond to the documented PRs/branches.

This ensures:

- Cross-repo doc links resolve in one checkout.
- The “system story” matches specific code revisions.

## Components

- `repos/graphiti` (submodule)
- `repos/vscode-copilot-chat` (submodule)
- `repos/codex` (submodule)
- `docs/*` (human-facing docs)
- `VERSIONS.md` (version matrix)

## Risks and Mitigations

- **Submodule friction:** include clear update commands in `VERSIONS.md`.
- **Repo access/size (codex):** use `--reference` locally when adding/updating submodules to avoid large re-clones.

## Future Enhancements

- Add a release checklist that validates all three repos + Graphiti service E2E.
- Add an automated “versions refresh” workflow to update `VERSIONS.md`.
