FROM node:26.5.0 AS node

LABEL description="Angular image"
LABEL maintainer="youssef.darzi@omixer.io"

RUN apt-get update \
 && apt-get install -y --no-install-recommends chromium \
 && rm -rf /var/lib/apt/lists/*

ENV CHROME_BIN=/usr/bin/chromium-browser
ARG PNPM_VERSION=10
ARG NG_CLI_VERSION=22.0.6
RUN npm install -g pnpm@$PNPM_VERSION @angular/cli@$NG_CLI_VERSION

RUN ng config -g cli.packageManager pnpm

WORKDIR /app
ENTRYPOINT ["ng"]
