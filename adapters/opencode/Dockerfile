# OpenCode CLI image. OpenCode runs on the base image's Node.js.
FROM node:24-bookworm-slim

ARG OPENCODE_VERSION=1.18.35

RUN apt-get update \
 && apt-get install -y --no-install-recommends ca-certificates curl git \
 && rm -rf /var/lib/apt/lists/*

RUN npm install -g "opencode-ai@${OPENCODE_VERSION}"

WORKDIR /workspace
ENTRYPOINT ["opencode"]
