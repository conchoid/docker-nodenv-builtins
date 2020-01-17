FROM node:6.17.1-slim AS node6
FROM node:8.17.0-slim AS node8
FROM node:10.18.1-slim AS node10
FROM node:11.15.0-slim AS node11
FROM node:12.14.1-slim AS node12
FROM node:13.6.0-slim AS node13

FROM conchoid/docker-nodenv:v1.3.1-9-12.14.1-stretch

# Install all latest major Nodejs versions excludes older than one year since EOL.
# https://github.com/nodejs/Release#end-of-life-releases

ENV NODE6 "6.17.1"
ENV NODE8 "8.17.0"
ENV NODE10 "10.18.1"
ENV NODE11 "11.15.0"
ENV NODE12 "12.14.1"
ENV NODE13 "13.6.0"
ENV PREINSTALLED_VERSIONS  "\
${NODE6}\n\
${NODE8}\n\
${NODE10}\n\
${NODE11}\n\
${NODE12}\n\
${NODE13}"

COPY --from=node6 "/usr/local/bin/node" "${NODENV_ROOT}/versions/${NODE6}/bin/"
COPY --from=node8 "/usr/local/bin/node" "${NODENV_ROOT}/versions/${NODE8}/bin/"
COPY --from=node10 "/usr/local/bin/node" "${NODENV_ROOT}/versions/${NODE10}/bin/"
COPY --from=node11 "/usr/local/bin/node" "${NODENV_ROOT}/versions/${NODE11}/bin/"
COPY --from=node13 "/usr/local/bin/node" "${NODENV_ROOT}/versions/${NODE13}/bin/"
COPY --from=node6 "/usr/local/lib/node_modules" "${NODENV_ROOT}/versions/${NODE6}/lib/node_modules"
COPY --from=node8 "/usr/local/lib/node_modules" "${NODENV_ROOT}/versions/${NODE8}/lib/node_modules"
COPY --from=node10 "/usr/local/lib/node_modules" "${NODENV_ROOT}/versions/${NODE10}/lib/node_modules"
COPY --from=node11 "/usr/local/lib/node_modules" "${NODENV_ROOT}/versions/${NODE11}/lib/node_modules"
COPY --from=node13 "/usr/local/lib/node_modules" "${NODENV_ROOT}/versions/${NODE13}/lib/node_modules"

RUN mkdir -p "${NODENV_ROOT}/versions/${NODE12}/bin/" "${NODENV_ROOT}/versions/${NODE12}/lib/" \
    && cp "$(nodenv which node)" "${NODENV_ROOT}/versions/${NODE12}/bin/" \
    && cp -R "/usr/local/lib/node_modules" "${NODENV_ROOT}/versions/${NODE12}/lib/" \
    && echo ${PREINSTALLED_VERSIONS} | while read version;do \
      NPM_SRC="${NODENV_ROOT}/versions/${version}/lib/node_modules/npm/bin/npm-cli.js" \
      && NPM_DST="${NODENV_ROOT}/versions/${version}/bin/npm" \
      # Override the shebang line of npm-cli.js to use the "node" path dynamically.
      && sed -i -E "1s/#.+/#!\/usr\/bin\/env node/" "${NPM_SRC}" \
      && ln -s -f "${NPM_SRC}" "${NPM_DST}";done \
    && nodenv rehash \
    && npm set progress false --global --quiet \
    && [ "$(nodenv versions --bare | xargs)" = "$NODE6 $NODE8 $NODE10 $NODE11 $NODE12 $NODE13" ]
