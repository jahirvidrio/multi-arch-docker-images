ARG MONGOSH_VERSION=latest


FROM node:lts-alpine AS builder

ARG MONGOSH_VERSION

WORKDIR /opt/mongosh

RUN \
    apk add --no-cache python3 make g++ \
    && wget -qO- https://gobinaries.com/tj/node-prune | sh \
    && npm --silent view "mongosh@$MONGOSH_VERSION" dist.tarball | xargs wget -qO- | tar -xz --strip-components=1 \
    && npm install --omit=dev --no-audit --no-fund \
    && node-prune ./node_modules/ 


FROM node:lts-alpine

COPY --from=builder /opt/mongosh /opt/mongosh
RUN ln -s /opt/mongosh/bin/mongosh.js /usr/local/bin/mongosh

ENTRYPOINT []
