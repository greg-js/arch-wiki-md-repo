[PowerDNS](https://www.powerdns.com/) is a DNS server, written in C++ and licensed under the GPL. PowerDNS features a large number of different backends ranging from simple BIND style zonefiles to relational databases and load balancing/failover algorithms.

## Contents

*   [1 Installation](#Installation)
*   [2 Backends](#Backends)
    *   [2.1 PostgreSQL backend](#PostgreSQL_backend)
    *   [2.2 MySQL backend](#MySQL_backend)
    *   [2.3 SQLite backend](#SQLite_backend)
*   [3 Startup](#Startup)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [powerdns](https://www.archlinux.org/packages/?name=powerdns) package.

Next you can review the configuration file located at `/etc/powerdns/pdns.conf`.

## Backends

To configure PowerDNS to use specific backend you will need to set then `launch` option in configuration file. Also depending on particular backend you use, you will have to configure it.

For [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), [MySQL](/index.php/MySQL "MySQL") and [SQLite](/index.php/SQLite "SQLite") you can find database table creation SQL files located at `/usr/share/doc/powerdns`.

### PostgreSQL backend

Firstly you will need to create a user and database where PowerDNS can store data.

Then execute "schema.pgsql.sql" file to create tables.

```
psql -U <user> -d <database name> -a -f /usr/share/doc/powerdns/schema.pgsql.sql

```

And finally update configuration file

```
launch=gpgsql
gpgsql-host=/run/postgresql # if PostgreSQL is listening to unix socket
# gpgsql-host=127.0.0.1
# gpgsql-port=5432
gpgsql-dbname=<database name>
gpgsql-user=<user to use>
gpgsql-password=

```

### MySQL backend

Install and run a [MySQL](/index.php/MySQL "MySQL") server. Create a new user, and a new database and import the schema into the db:

 `mysql -u root -p pdns < /usr/share/doc/powerdns/schema.mysql.sql` 

Then, configure Powerdns to use MySQL:

 `/etc/powerdns/pdns.conf` 
```
launch=gmysql
gmysql-host=127.0.0.1
gmysql-socket=/run/mysqld/mysqld.sock
gmysql-user=pdns
gmysql-password=Pa$$w0rd
gmysql-dbname=pdns
# Add this for dnssec support
# gmysql-dnssec=yes
```

You could also use localhost instead of 127.0.0.1, but this causes PowerDNS to use the socket file. As PowerDNS runs in a chroot by default, the socket file is not available.

### SQLite backend

## Startup

[Start/enable](/index.php/Start/enable "Start/enable") the `powerdns` service.

## See also

*   [PowerDNS manual](http://doc.powerdns.com/)