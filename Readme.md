Description
===========

 - infobright: For building containers with Infobright Community Edition
 - mysqlcluster*: For building MySQL Cluster containers

Some are prebuild at https://registry.hub.docker.com/repos/dveeden/

## Detail
http://dev.mysql.com/doc/refman/5.6/en/mysql-cluster-installation.html

To get more familiar with docker and to create a test setup for MySQL Cluster I created docker images for the various components of MySQL Cluster (a.k.a. NDB Cluster)

At first I created a Fedora 20 container and ran all components in one container. That worked and is quite easy to setup. But that's not how one is supposed to use docker.

So I created Dockerfile's for all components and one base image.

The base image:

* contains the MySQL Cluster software
* has libaio installed
* has a mysql user and group 
* serves as a base for the other images

The management node (ndb_mgmd) image:

* Has ndb_mgmd as entrypoint
* Has a config.ini for the cluster config
* Should be started with "--name=mymgm01"

The data node (ndbmtd) image:

* Has ndbmtd as entrypoint
* Uses the connect string: "host=${MGM01_PORT_1186_TCP_ADDR}:1186"
* Should be started with "--link mymgm01:mgm01" to allow it to connect to the management node.
* You should create 2 containers of this type to create a nodegroup of 2 nodes.

The API node (mysqld) image:

* has a my.cnf
* Runs mysqld_safe
* Should be started with "--link mymgm01:mgm01" to allow it to connect to the management node.
* The ndb-connectstring is given as parameter to mysqld_safe as it comes from an environment variable. It's not possible to use environment variables from within my.cnf. Docker is supposed to also update /etc/hosts but that didn't work for me.
* You should expose port 3306 for your application

The management client (ndb_mgm) image:
* Runs ndb_mgm as entrypoint
* Should be started with "--link mymgm01:mgm01" to allow it to connect to the management node.
* Running the ndb_mgm in a container removes the need to publish port 1186 on the management server. More info here.
* You can override the entrypoint to run other NDB utilities like ndb_desc or ndb_select_all

The images can be found on https://registry.hub.docker.com/u/dveeden/mysqlcluster72/
The Dockerfiles can be found on https://github.com/dveeden/dve-docker   

Possible improvements

* Use hostnames in the config.ini instead of IPv4 addresses. This makes it more dynamic. But that means updating /etc/hosts or fideling with DNS.
* Using VOLUMES in the Dockerfiles to make working with data easier.
