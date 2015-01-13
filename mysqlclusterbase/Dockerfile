FROM fedora:20
MAINTAINER Philipz <philipzheng@gmail.com>

ADD https://downloads.mariadb.com/files/mysql-cluster-gpl-7.3/mysql-cluster-gpl-7.3.7-linux-glibc2.5-x86_64.tar.gz /opt/
RUN mv /opt/mysql-cluster-gpl-7.2.17-linux2.6-x86_64 /opt/mysql

RUN yum -y install libaio
RUN groupadd mysql
RUN useradd -g mysql -s /sbin/nologin mysql
