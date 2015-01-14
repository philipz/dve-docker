FROM philipz/mysqlcluster73:base
MAINTAINER Philipz <philipzheng@gmail.com>

RUN mkdir -p /usr/local/mysql/mysql-cluster
RUN mkdir -p /var/lib/mysql-cluster

ENTRYPOINT /opt/mysql/bin/ndb_mgm 192.168.0.1
