FROM conchoid/docker-nodenv:v1.1.2-5-8.9.4-stretch

RUN set -x \
  && version="0.10.48" \
  # To avoid standard library version warnings, use '-c' option (Force compilation even if a matching binary exists).
  && nodenv install -c ${version} \
  && nodenv rehash \
  && nodenv global ${version} \
  # To disable showing progress may improve performance of npm install:
  # https://github.com/npm/npm/issues/11283
  && npm set progress false --global --quiet \
  && nodenv global system