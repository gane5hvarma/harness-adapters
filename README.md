# harness-adapters

Container images for three AI coding-agent CLIs, one folder per adapter.

| Adapter | Agent CLI | Built on | Node.js |
|---|---|---|---|
| [`claude-code`](adapters/claude-code/Dockerfile) | Claude Code (`@anthropic-ai/claude-code`) | `ubuntu:24.04` + NodeSource | 20 |
| [`codex`](adapters/codex/Dockerfile) | Codex CLI (`@openai/codex`) | `ubuntu:24.04` + NodeSource, major set by the `NODE_MAJOR` build arg | 20 |
| [`opencode`](adapters/opencode/Dockerfile) | OpenCode (`opencode-ai`) | the `node:20-bookworm-slim` base image | 20 |

Each adapter gets Node.js in a different way, so the same Node.js upgrade
lands as a different change in each Dockerfile.

## Build

```sh
docker build -t claude-code adapters/claude-code
docker build -t codex       adapters/codex
docker build -t opencode    adapters/opencode
```

The agent CLI versions are build args with pinned defaults, for example:

```sh
docker build --build-arg CLAUDE_NPM_VERSION=2.1.289 -t claude-code adapters/claude-code
```

## Conventions

- **One adapter per pull request.** A change touches `adapters/<name>/` only,
  so fixes to different adapters can land in parallel without conflicting.
- Pull request titles follow `<adapter>: <summary> (<advisory id>)`.

## About this repository

This repo is the fixture for a video demo of an **agent swarm**. One coding
agent works through a security advisory across every adapter: it reads the
advisory, inspects each Dockerfile and plans a fix for each. That session is
then checkpointed and forked, one copy of the agent per adapter. Each copy
starts already knowing the plan, fixes only its own adapter, has its change
checked by an independent verifier, and opens its own pull request.

The pull requests you see here were opened by those agents.
