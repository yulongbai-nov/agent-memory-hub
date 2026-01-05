# Version Matrix

This repo pins the participating repos as submodules under `repos/`. The recorded commits are the “aligned” versions for the architecture and docs here.

| Repo | Submodule | Branch | Commit | PR |
|---|---|---|---|---|
| Graphiti | `repos/graphiti` | `feature/agent-memory-ontology` | `a957a1da8d2940765cae5cf70b2151955ce417c3` | https://github.com/yulongbai-nov/graphiti/pull/2 |
| Copilot Chat | `repos/vscode-copilot-chat` | `feature/graphiti-memory-integration` | `a2d2a1f689fef0765d9c0c0f1188178fc68211af` | https://github.com/yulongbai-nov/vscode-copilot-chat/pull/51 |
| Codex | `repos/codex` | `feature/graphiti-memory-integration` | `8a091d0a612a0df154e4ae1c93592f19a2e66893` | https://github.com/yulongbai-nov/codex/pull/1 |

## Submodule update

```bash
git submodule update --init --recursive
```

To move submodules to newer commits, update each submodule and commit the new pointers in this repo.
