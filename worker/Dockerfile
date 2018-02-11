FROM alpine
RUN apk --no-cache add \
    build-base \
    chromium \
    jpeg \
    jpeg-dev \
    py3-cryptography \
    py3-pip \
    python3 \
    python3-dev \
    xvfb \
    zlib \
    zlib-dev \
  && pip3 install brozzler \
  && apk --no-cache del \
    build-base \
    jpeg-dev \
    python3-dev \
    zlib-dev
RUN echo '#!/bin/sh' > /bin/chrome-wrapper && \
  echo 'exec chromium-browser --no-sandbox "$@"' >> /bin/chrome-wrapper && \
  chmod +x /bin/chrome-wrapper && \
  adduser -S brozzler
RUN apk --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing/ add x11vnc
USER brozzler
ENV DISPLAY=:1
CMD trap 'kill $(jobs -p)' SIGINT SIGTERM EXIT && \
  Xvfb :1 & \
  x11vnc -nopw -shared -forever -ncache 10 -ncache_cr -quiet & \
  brozzler-worker -e chrome-wrapper --warcprox-auto --max-browsers=1
