# Cursor agent CLI image. The CLI ships as a tarball and runs on the base
# image's Node.js.
FROM node:20-bookworm-slim

ARG CURSOR_VERSION=2026.06.04-5fd875e
ARG TARGETARCH=x64

RUN apt-get update \
 && apt-get install -y --no-install-recommends ca-certificates curl git \
 && rm -rf /var/lib/apt/lists/* \
 && mkdir -p /opt/cursor \
 && curl -fsSL "https://downloads.cursor.com/lab/${CURSOR_VERSION}/linux/${TARGETARCH}/agent-cli-package.tar.gz" \
    | tar -xz -C /opt/cursor

ENV PATH="/opt/cursor:${PATH}"
WORKDIR /workspace
ENTRYPOINT ["cursor-agent"]
