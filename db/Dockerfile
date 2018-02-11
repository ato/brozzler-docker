FROM alpine
RUN apk --no-cache add rethinkdb
VOLUME /rethinkdb_data
#USER rethinkdb
CMD exec rethinkdb --bind all
