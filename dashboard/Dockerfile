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
  && pip3 install brozzler[dashboard] \
  && apk --no-cache del \
    build-base \
    jpeg-dev \
    python3-dev \
    zlib-dev
RUN adduser -S brozzler
USER brozzler
#ENV BROZZLER_RETHINKDB_SERVERS=db BROZZLER_RETHINKDB_DB=brozzler
CMD gunicorn --bind=0.0.0.0:8881 brozzler.dashboard:app
