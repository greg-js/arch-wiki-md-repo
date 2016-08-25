Galera is a synchronous multi-master cluster for MySQL/InnoDB databases. For more information about the product and its features, please visit the [official webpage](http://codership.com/content/using-galera-cluster).

**Note:** Currently replication is supported only for InnoDB tables.

## Contents

*   [1 Installation](#Installation)
*   [2 Installation MariaDB](#Installation_MariaDB)
*   [3 Configuration](#Configuration)
*   [4 Compile Galera](#Compile_Galera)
*   [5 See also](#See_also)

## Installation

The two components Galera cluster comprised of are Galera plugin itself and a patched version of MySQL server which connect using wsrep API.

Install the [mysql-wsrep](https://aur.archlinux.org/packages/mysql-wsrep/) and [galera](https://aur.archlinux.org/packages/galera/) packages from the [AUR](/index.php/AUR "AUR").

[Start/Enable](/index.php/Systemd#Using_units "Systemd") the `mysqld.service` daemon.

## Installation [MariaDB](/index.php/MariaDB "MariaDB")

MariaDB V>10.1 is ready to use galera / wsrep out of the box. [[1]](https://mariadb.org/mariadb-10-1-1-galera-support/)

[Install](/index.php/Install "Install") these packages:

*   [mariadb](https://www.archlinux.org/packages/?name=mariadb) — Standard MariaDB Package
*   [galera](https://aur.archlinux.org/packages/galera/) — ATM this package does not install the galera library to the right place so you should [Galera#Compile Galera](/index.php/Galera#Compile_Galera "Galera") yourself.

## Configuration

Once you have installed the [galera](https://aur.archlinux.org/packages/galera/) and [mysql-wsrep](https://aur.archlinux.org/packages/mysql-wsrep/) packages, you need to configure the cluster.

On each node edit `/etc/mysql/my.cnf` and update the wsrep_cluster_address variable so it contains the list of all nodes in the cluster:

```
wsrep_cluster_address="gcomm://192.168.1.4,192.168.1.5,192.168.1.6"

```

Change the variables wsrep_node_address and wsrep_node_name to the IP address/hostname and name(this doesn't need to be unique) for each node, e.g.:

```
wsrep_node_address='192.168.1.4'
wsrep_node_name='node1'

```

The wsrep_cluster_name variable should contain the same name for all cluster nodes:

```
wsrep_cluster_name='my_galera_cluster'

```

Also, set wsrep_sst_method to the desired state snapshot transfer method, the preferred one is rsync.

```
wsrep_sst_method=rsync

```

When you have finished with `/etc/mysql/my.cnf`, start the mysqld service on the first node:

```
# systemctl start mysqld-bootstrap.service

```

This will bootstrap the cluster. Use MySQL's command line tool to log in as root into your MySQL server:

```
$ mysql -p -u root

```

Check the status of the cluster:

```
mysql> SHOW STATUS LIKE 'wsrep_%';

```

This will show you wsrep-related status variables:

```
...
| wsrep_local_state          | 4                                    |
| wsrep_local_state_comment  | Synced                               |
| wsrep_cert_index_size      | 0                                    |
| wsrep_causal_reads         | 0                                    |
| wsrep_incoming_addresses   | 192.168.1.4:3306                     |
| wsrep_cluster_conf_id      | 1                                    |
| wsrep_cluster_size         | 1                                    |
| wsrep_cluster_state_uuid   | 6cd96745-2ea8-11e3-bbc8-d666651b51ef |
| wsrep_cluster_status       | Primary                              |
| wsrep_connected            | ON                                   |
| wsrep_local_index          | 0                                    |
| wsrep_provider_name        | Galera                               |
...

```

If you use xtrabackup or mysqldump SST method, you will need to create a MySQL user for sst transfers.

Once you configured the first node, you should be able to start all other nodes with:

```
# systemctl start mysqld.service

```

## Compile Galera

*   Download galera from github [Galera Releases](https://github.com/codership/galera/releases)
*   Extract content and run scons in root directory

```
$ tar xvfz release_*.tar.gz && cd galera_release_* && scons

```

*   Copy lib to `/usr/lib/galera/libgalera_smm.so`

```
$ sudo mkdir /usr/lib/galera && sudo cp libgalera_smm.so /usr/lib/galera/

```

## See also

[Galera Wiki](http://www.codership.com/wiki/doku.php?id=galera_wiki) [Percona XtraDB Cluster’s documentation](http://www.percona.com/doc/percona-xtradb-cluster/index.html)