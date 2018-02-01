FROM conchoid/docker-nodenv-builtins:v1.1.2-node0.10.48-1-6.9.5-alpine3.6 AS node0.10.48
FROM conchoid/docker-nodenv-builtins:v1.1.2-node0.12.18-1-6.9.5-alpine3.6 AS node0.12.18
FROM conchoid/docker-nodenv-builtins:v1.1.2-node4.8.7-1-6.9.5-alpine3.6   AS node4.8.7
FROM conchoid/docker-nodenv-builtins:v1.1.2-node5.12.0-1-6.9.5-alpine3.6  AS node5.12.0
FROM conchoid/docker-nodenv-builtins:v1.1.2-node6.9.5-1-6.9.5-alpine3.6   AS node6.9.5
FROM conchoid/docker-nodenv-builtins:v1.1.2-node7.10.1-1-6.9.5-alpine3.6  AS node7.12.18
FROM conchoid/docker-nodenv-builtins:v1.1.2-node8.9.4-1-6.9.5-alpine3.6   AS node8.9.4
FROM conchoid/docker-nodenv-builtins:v1.1.2-node9.4.0-1-6.9.5-alpine3.6   AS node9.4.0

FROM conchoid/docker-nodenv:v1.1.2-1-6.9.5-alpine3.6

COPY --from=node0.10.48 $NODENV_ROOT/versions $NODENV_ROOT/versions
COPY --from=node0.12.18 $NODENV_ROOT/versions $NODENV_ROOT/versions
COPY --from=node4.8.7   $NODENV_ROOT/versions $NODENV_ROOT/versions
COPY --from=node5.12.0  $NODENV_ROOT/versions $NODENV_ROOT/versions
COPY --from=node6.9.5   $NODENV_ROOT/versions $NODENV_ROOT/versions
COPY --from=node7.12.18 $NODENV_ROOT/versions $NODENV_ROOT/versions
COPY --from=node8.9.4   $NODENV_ROOT/versions $NODENV_ROOT/versions
COPY --from=node9.4.0   $NODENV_ROOT/versions $NODENV_ROOT/versions

ENV PREINSTALLED_VERSIONS  "\
0.10.48\n\
0.12.18\n\
4.8.7\n\
5.12.0\n\
6.9.5\n\
7.10.1\n\
8.9.4\n\
9.4.0"

RUN set -x \
  # To disable showing progress may improve performance of npm install:
  # https://github.com/npm/npm/issues/11283
  && nodenv global system \
  && npm set progress false --global --quiet
