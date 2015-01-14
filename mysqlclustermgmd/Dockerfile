FROM philipz/mysqlcluster73:base
MAINTAINER Philipz <philipzheng@gmail.com>

RUN mkdir -p /usr/local/mysql/mysql-cluster
RUN mkdir -p /var/lib/mysql-cluster
ADD config.ini /usr/local/mysql/mysql-cluster/

EXPOSE 1186
VOLUME /var/lib/mysql-cluster
ENTRYPOINT /opt/mysql/bin/ndb_mgmd -f /usr/local/mysql/mysql-cluster/config.ini --initial --nodaemon
