FROM philipz/mysqlcluster73:base
MAINTAINER Philipz <philipzheng@gmail.com>

RUN mkdir -p /usr/local/mysql/data
VOLUME /usr/local/mysql/data
ENTRYPOINT /opt/mysql/bin/ndbmtd --nodaemon --initial --connect-string="host=192.168.0.1:1186"
