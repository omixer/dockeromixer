FROM node:10.16.0 AS node

LABEL description="Angular image"
LABEL maintainer="youssef.darzi@gmail.com"

ARG NG_CLI_VERSION=8.0.3

RUN yarn global add @angular/cli@$NG_CLI_VERSION -T && rm -rf $(yarn cache dir)
RUN ng config -g cli.packageManager yarn

WORKDIR /app

ENTRYPOINT ["ng"]
