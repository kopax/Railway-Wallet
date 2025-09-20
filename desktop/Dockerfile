FROM node:18 AS builder

RUN apt-get update && apt-get install -y git

ARG YARN_VERSION=4.5.1
RUN corepack enable && corepack prepare yarn@$YARN_VERSION --activate

WORKDIR /app

COPY . .

ENV NODE_OPTIONS="--max-old-space-size=4096"

RUN yarn install

RUN yarn run build-prod

FROM nginx:alpine

COPY --from=builder /app/build /usr/share/nginx/html

EXPOSE 80


