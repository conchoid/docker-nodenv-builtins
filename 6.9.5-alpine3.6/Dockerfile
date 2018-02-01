FROM node:9.4.0-alpine AS node9.4.0-alpine

FROM conchoid/docker-nodenv:v1.1.2-1-6.9.5-alpine3.6

ENV NODE_VERSION "9.4.0"
ENV NODE940_DIR "$NODENV_ROOT/versions/$NODE_VERSION"
RUN mkdir -p "$NODE940_DIR/lib/node_modules" "$NODE940_DIR/bin"
COPY --from=node9.4.0-alpine "/usr/local/bin/node" "$NODE940_DIR/bin/"
COPY --from=node9.4.0-alpine "/usr/local/lib/node_modules" "$NODE940_DIR/lib/node_modules"
RUN set -x \
    && ln -s "$NODE940_DIR/lib/node_modules/npm/bin/npm-cli.js" "$NODE940_DIR/bin/npm" \
    && nodenv rehash \
    && nodenv global $NODE_VERSION \
    # To disable showing progress may improve performance of npm install:
    # https://github.com/npm/npm/issues/11283
    && npm set progress false --global --quiet \
    && nodenv global system
