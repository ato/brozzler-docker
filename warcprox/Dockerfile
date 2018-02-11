FROM alpine
RUN apk --no-cache add \
    build-base \
    py3-pip \
    python3 \
    python3-dev \
    libffi \
    libffi-dev \
    openssl \
    openssl-dev \
  && pip3 install warcprox \
  && apk --no-cache del \
    build-base \
    libffi-dev \
    openssl-dev \
    python3-dev \
  && adduser -S warcprox
RUN mkdir /warcprox && chown warcprox /warcprox
VOLUME /warcs
USER warcprox
CMD cd /warcprox && exec warcprox \
    -d /warcs \
    --address=0.0.0.0 \
    --base32 \
    --gzip \
    --rollover-idle-time=180 \
    --rethinkdb-services-url=rethinkdb://db/brozzler/services \
    --rethinkdb-stats-url=rethinkdb://db/brozzler/stats \
    --rethinkdb-big-table-url=rethinkdb://db/brozzler/captures \
    --method-filter=GET \
    --method-filter=POST
