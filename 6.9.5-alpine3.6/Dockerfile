FROM conchoid/docker-nodenv

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
  # "-D__USE_MISC" is necessary for building Nodejs 0.10.48 and it does not affect installation of other versions.
  && export CFLAGS="-D__USE_MISC" \
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
