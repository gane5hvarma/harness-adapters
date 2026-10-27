# Codex CLI image.
FROM ubuntu:24.04

ARG NODE_MAJOR=20
ARG CODEX_NPM_VERSION=0.161.0

RUN apt-get update \
 && apt-get install -y --no-install-recommends ca-certificates curl git \
 && curl -fsSL "https://deb.nodesource.com/setup_${NODE_MAJOR}.x" | bash - \
 && apt-get install -y --no-install-recommends nodejs \
 && rm -rf /var/lib/apt/lists/*

RUN npm install -g "@openai/codex@${CODEX_NPM_VERSION}"

WORKDIR /workspace
ENTRYPOINT ["codex"]
