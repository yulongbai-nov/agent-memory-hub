# Version Matrix

This repo pins the participating repos as submodules under `repos/`. The recorded commits are the “aligned” versions for the architecture and docs here.

| Repo | Submodule | Branch | Commit | PR |
|---|---|---|---|---|
| Graphiti | `repos/graphiti` | `feature/agent-memory-ontology` | `a957a1da8d2940765cae5cf70b2151955ce417c3` | https://github.com/yulongbai-nov/graphiti/pull/2 |
| Copilot Chat | `repos/vscode-copilot-chat` | `feature/graphiti-memory-integration` | `3222b2299dd481966e0c656cef622dcae2681b7a` | https://github.com/yulongbai-nov/vscode-copilot-chat/pull/51 |
| Codex | `repos/codex` | `feature/graphiti-memory-integration` | `b39c1f1f87d16f04a8e2ecb19892d4376ac1b0f0` | https://github.com/yulongbai-nov/codex/pull/1 |

## Submodule update

```bash
git submodule update --init --recursive
```

To move submodules to newer commits, update each submodule and commit the new pointers in this repo.
