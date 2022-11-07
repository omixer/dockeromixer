FROM node:16.13.0 AS node

LABEL description="Angular image"
LABEL maintainer="youssef.darzi@gmail.com"

RUN apt-get update \
 && apt-get install -y --no-install-recommends chromium \
 && rm -rf /var/lib/apt/lists/*

ENV CHROME_BIN=/usr/bin/chromium-browser
ARG NG_CLI_VERSION=14.2.8

RUN yarn global add @angular/cli@$NG_CLI_VERSION -T && rm -rf $(yarn cache dir)
RUN ng config -g cli.packageManager yarn

WORKDIR /app

ENTRYPOINT ["ng"]
