# Claude Code CLI image.
FROM ubuntu:24.04

ARG CLAUDE_NPM_VERSION=2.1.289

RUN apt-get update \
 && apt-get install -y --no-install-recommends ca-certificates curl git \
 && curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
 && apt-get install -y --no-install-recommends nodejs \
 && rm -rf /var/lib/apt/lists/*

RUN npm install -g "@anthropic-ai/claude-code@${CLAUDE_NPM_VERSION}"

WORKDIR /workspace
ENTRYPOINT ["claude"]
