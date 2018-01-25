# TODO: Use docker-nodenv image
FROM baseImage

ENV PREINSTALLED_VERSIONS  "\
0.10.48\n\
0.12.18\n\
4.8.6\n\
5.12.0\n\
6.9.5\n\
7.10.1\n\
8.9.1\n\
9.2.0"

RUN set -x \
  && echo -e ${PREINSTALLED_VERSIONS} \
    | while read -r version; do \
    # To avoid standard library version warnings, use '-c' option (Force compilation even if a matching binary exists).
        nodenv install -c ${version} \
        && nodenv rehash \
        && nodenv global ${version} \
        # To disable showing progress may improve performance of npm install:
        # https://github.com/npm/npm/issues/11283
        && npm set progress false --global --quiet; done \
  && nodenv global system \
  && npm set progress false --global --quiet
