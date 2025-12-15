# Requirements Document

## Introduction

This repo provides central documentation for the Graphiti-based agent memory system across multiple client repos, and aligns versions via submodules.

## Glossary

- **Hub Repo**: This repository (`agent-memory-hub`) which indexes cross-repo specs/PRs.
- **Pinned Version**: A specific commit recorded for each submodule in this repo.

## Requirements

### Requirement 1: Spec Index

**User Story:** As a contributor, I want one page that links to all relevant specs and PRs, so that I can quickly orient myself.

#### Acceptance Criteria

1.1 THE Hub Repo SHALL provide an index linking to specs and PRs across Graphiti, Copilot Chat, and Codex.
1.2 THE index SHALL reference repo-local `.specs/*` documents via relative links through submodules.

### Requirement 2: Architecture Documentation

**User Story:** As a reviewer/operator, I want a big-picture architecture diagram, so that I can understand the end-to-end memory flow.

#### Acceptance Criteria

2.1 THE Hub Repo SHALL include an architecture document that explains ingest, recall, and scope semantics.
2.2 The document SHALL include at least one diagram (Mermaid or ASCII).

### Requirement 3: Operational Guidance

**User Story:** As an operator, I want redeploy and debugging guidance for Graphiti, so that I can diagnose “202 but no memory” issues quickly.

#### Acceptance Criteria

3.1 THE Hub Repo SHALL document Graphiti health endpoints and redeploy steps.
3.2 The document SHALL include common failure modes and mitigations.

### Requirement 4: Version Alignment

**User Story:** As a maintainer, I want the docs to be pinned to specific code versions, so that references don’t drift.

#### Acceptance Criteria

4.1 THE Hub Repo SHALL include the participating repos as git submodules under `repos/`.
4.2 THE Hub Repo SHALL include a version matrix file listing the pinned commits and related PRs.

