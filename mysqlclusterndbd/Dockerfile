FROM philipz/mysqlcluster73:base
MAINTAINER Philipz <philipzheng@gmail.com>

RUN mkdir -p /usr/local/mysql/data
VOLUME /usr/local/mysql/data
ENTRYPOINT /opt/mysql/bin/ndbmtd --nodaemon --initial --connect-string="host=${MGM01_PORT_1186_TCP_ADDR}:1186"
