FROM alpine
RUN apk --no-cache add \
    build-base \
    jpeg \
    jpeg-dev \
    py3-cryptography \
    py3-pip \
    python3 \
    python3-dev \
    zlib \
    zlib-dev \
  && pip3 install brozzler pywb==0.33.2 \
  && apk --no-cache del \
    build-base \
    jpeg-dev \
    python3-dev \
    zlib-dev
RUN adduser -S brozzler
VOLUME /warcs
USER brozzler
COPY pywb.yml /etc/pywb.yml
ENV PYWB_CONFIG_FILE=/etc/pywb.yml
CMD brozzler-wayback
