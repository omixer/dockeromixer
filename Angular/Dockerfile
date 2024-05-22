FROM node:18.20.3 AS node

LABEL description="Angular image"
LABEL maintainer="youssef.darzi@omixer.io"

RUN apt-get update \
 && apt-get install -y --no-install-recommends chromium \
 && rm -rf /var/lib/apt/lists/*

ENV CHROME_BIN=/usr/bin/chromium-browser
ARG NG_CLI_VERSION=17.1.0

RUN yarn global add @angular/cli@$NG_CLI_VERSION -T && rm -rf $(yarn cache dir)
RUN ng config -g cli.packageManager yarn

WORKDIR /app

ENTRYPOINT ["ng"]
