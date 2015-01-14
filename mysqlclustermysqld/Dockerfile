FROM philipz/mysqlcluster73:base
MAINTAINER Philipz <philipzheng@gmail.com>

RUN cd /opt/mysql; ./scripts/mysql_install_db --user=mysql --datadir=/usr/local/mysql/data
ADD my.cnf /etc/
EXPOSE 3306
ENTRYPOINT /opt/mysql/bin/mysqld_safe --skip-grant-tables --ledir=/opt/mysql/bin --ndb-connectstring=192.168.0.1
