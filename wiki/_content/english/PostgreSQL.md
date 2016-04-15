[PostgreSQL](http://www.postgresql.org/) is an open source, community driven, standard compliant object-relational database system.

This document describes how to set up PostgreSQL. It also describes how to configure PostgreSQL to be accessible from a remote client. Among other applications, PostgreSQL can be substituted for MySQL as part of the [LAMP](/index.php/LAMP "LAMP") web stack.

## Contents

*   [1 Installing PostgreSQL](#Installing_PostgreSQL)
*   [2 Create your first database/user](#Create_your_first_database.2Fuser)
*   [3 Familiarize with PostgreSQL](#Familiarize_with_PostgreSQL)
    *   [3.1 Access the database shell](#Access_the_database_shell)
*   [4 Optional configuration](#Optional_configuration)
    *   [4.1 Configure PostgreSQL to be accessible from remote hosts](#Configure_PostgreSQL_to_be_accessible_from_remote_hosts)
    *   [4.2 Configure PostgreSQL authenticate against PAM](#Configure_PostgreSQL_authenticate_against_PAM)
    *   [4.3 Change default data directory](#Change_default_data_directory)
    *   [4.4 Change default encoding of new databases to UTF-8](#Change_default_encoding_of_new_databases_to_UTF-8)
*   [5 Administration tools](#Administration_tools)
*   [6 Setup HHVM to work with PostgreSQL](#Setup_HHVM_to_work_with_PostgreSQL)
*   [7 Upgrading PostgreSQL](#Upgrading_PostgreSQL)
    *   [7.1 Quick guide](#Quick_guide)
        *   [7.1.1 Troubleshooting](#Troubleshooting)
    *   [7.2 Detailed instructions](#Detailed_instructions)
        *   [7.2.1 Manual dump and reload](#Manual_dump_and_reload)
*   [8 Troubleshooting](#Troubleshooting_2)
    *   [8.1 Improve performance of small transactions](#Improve_performance_of_small_transactions)
    *   [8.2 Prevent disk writes when idle](#Prevent_disk_writes_when_idle)
    *   [8.3 Cannot connect to database through pg_connect()](#Cannot_connect_to_database_through_pg_connect.28.29)

## Installing PostgreSQL

[Install](/index.php/Install "Install") the [postgresql](https://www.archlinux.org/packages/?name=postgresql) package. Then [set a password](/index.php/Users_and_groups#Other_examples_of_user_management "Users and groups") for the newly created *postgres* user.

Then, switch to the default PostgreSQL user *postgres* by executing the following command:

*   If you have [sudo](https://www.archlinux.org/packages/?name=sudo) and your username is in `sudoers`:

	 `$ sudo -i -u postgres` 

*   Otherwise:

```
$ su
# su - postgres

```

**Note:** Commands that should be run as the postgres user are prefixed by `[postgres]$` in this article.

Before PostgreSQL can function correctly, the database cluster must be initialized:

```
[postgres]$ initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data'

```

Where:

*   the *--locale* is the one defined in the file `/etc/locale.conf`;
*   the *-E* is the default encoding of the database that will be created in the future;
*   and *-D* is the default location where the database cluster must be stored.

A bunch of lines should now appear on the screen with several ending by *... ok*:

```
The files belonging to this database system will be owned by user "postgres".
This user must also own the server process.

The database cluster will be initialized with locale "en_GB.UTF-8".
The default text search configuration will be set to "english".

Data page checksums are disabled.

fixing permissions on existing directory /var/lib/postgres/data ... ok
creating subdirectories ... ok
selecting default max_connections ... 100
selecting default shared_buffers ... 128MB
selecting dynamic shared memory implementation ... posix
creating configuration files ... ok
creating template1 database in /var/lib/postgres/data/base/1 ... ok
initializing pg_authid ... ok
[...]
```

If this is the kind of lines you see, then the process succeeded. In that case return to the regular user using `exit`.

Then as root, [start](/index.php/Start "Start") and enable `postgresql.service`.

**Warning:** If the database resides on a [Btrfs](/index.php/Btrfs "Btrfs") file system, you should consider disabling [Copy-on-Write](/index.php/Btrfs#Copy-On-Write_.28CoW.29 "Btrfs") for the directory before creating any database. If the database resides on a [ZFS](/index.php/ZFS "ZFS") file system, you should consult [ZFS#Database](/index.php/ZFS#Database "ZFS") before creating any database.

## Create your first database/user

**Tip:** If you create a PostgreSQL user with the same name as your Linux username, it allows you to access the PostgreSQL database shell without having to specify a user to login (which makes it quite convenient).

Become the postgres user. Add a new database user using the [createuser](http://www.postgresql.org/docs/current/static/app-createuser.html) command:

```
[postgres]$ createuser --interactive

```

Create a new database over which the above user has read/write privileges using the [createdb](http://www.postgresql.org/docs/current/static/app-createdb.html) command (execute this command from your login shell if the database user has the same name as your Linux user, otherwise add `-U *database-username*` to the following command):

```
$ createdb myDatabaseName

```

## Familiarize with PostgreSQL

### Access the database shell

Become the postgres user. Start the primary database shell, [psql](http://www.postgresql.org/docs/current/static/app-psql.html), where you can do all your creation of databases/tables, deletion, set permissions, and run raw SQL commands. Use the `-d` option to connect to the database you created (without specifying a database, `psql` will try to access a database that matches your username).

```
[postgres]$ psql -d myDatabaseName

```

Some helpful commands:

Get help:

```
=> \help

```

Connect to a particular database:

```
=> \c <database>

```

List all users and their permission levels:

```
=> \du

```

Show summary information about all tables in the current database:

```
=> \dt

```

Exit/quit the `psql` shell:

```
=> \q or CTRL+d

```

There are of course many more meta-commands, but these should help you get started. To see all meta-commands run:

```
=> \?

```

## Optional configuration

### Configure PostgreSQL to be accessible from remote hosts

The PostgreSQL database server configuration file is `postgresql.conf`. This file is located in the data directory of the server, typically `/var/lib/postgres/data`. This folder also houses the other main configuration files, including the `pg_hba.conf`.

**Note:** By default, this folder will not be browsable or searchable by a regular user. This is why `find` and `locate` are not finding the configuration files.

Edit the file `/var/lib/postgres/data/postgresql.conf`. In the connections and authentications section, add the `listen_addresses` line to your needs:

```
listen_addresses = 'localhost,my_remote_server_ip_address'

```

Take a careful look at the other lines.

Host-based authentication is configured in `/var/lib/postgres/data/pg_hba.conf`. This file controls which hosts are allowed to connect. Note that the defaults **allow any local user to connect as any database user**, including the database superuser. Add a line like the following:

```
# IPv4 local connections:
host   all   all   *my_remote_client_ip_address*/32   md5

```

where `your_desired_ip_address` is the IP address of the client.

See the documentation for [pg_hba.conf](http://www.postgresql.org/docs/current/static/auth-pg-hba-conf.html).

After this you should [restart](/index.php/Restart "Restart") `postgresql.service` for the changes to take effect.

**Note:** PostgreSQL uses port `5432` by default for remote connections. Make sure this port is open and able to receive incoming connections.

For troubleshooting take a look in the server log file:

```
$ journalctl -u postgresql

```

### Configure PostgreSQL authenticate against PAM

PostgreSQL offers a number of authentication methods. If you would like to allow users to authenticate with their system password, additional steps are necessary. First you need to enable [PAM](/index.php/PAM "PAM") for the connection.

For example, the same configuration as above, but with PAM enabled:

```
# IPv4 local connections:
host   all   all   *my_remote_client_ip_address*/32   pam

```

The PostgreSQL server is however running without root privileges and will not be able to access `/etc/shadow`. We can work around that by allowing the postgres group to access this file:

```
setfacl -m g:postgres:r /etc/shadow

```

### Change default data directory

The default directory where all your newly created databases will be stored is `/var/lib/postgres/data`. To change this, follow these steps:

Create the new directory and make the postgres user its owner:

```
# mkdir -p /pathto/pgroot/data
# chown -R postgres:postgres /pathto/pgroot

```

Become the postgres user, and initialize the new cluster:

```
[postgres]$ initdb -D /pathto/pgroot/data

```

If enabled, disable `postgresql.service`. Copy `/usr/lib/systemd/system/postgresql.service` to `/etc/systemd/system/postgresql.service` and edit it to change the default `PGROOT` and `PIDFile` paths.

```
Environment=PGROOT=*/pathto/pgroot/*
...
PIDFile=*/pathto/pgroot/*data/postmaster.pid

```

Alternatively, the variables can be overridden by a custom configuration, as described in [Systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd"):

1.  create the directory */etc/systemd/system/postgresql.service.d*
2.  create a file *start.conf*:

```
[Service]
Environment=PGROOT=*/pathto/pgroot/*
PIDFile=*/pathto/pgroot/*data/postmaster.pid

```

### Change default encoding of new databases to UTF-8

**Note:** If you ran `initdb` with `-E UTF8` these steps are not required.

When creating a new database (e.g. with `createdb blog`) PostgreSQL actually copies a template database. There are two predefined templates: `template0` is vanilla, while `template1` is meant as an on-site template changeable by the administrator and is used by default. In order to change the encoding of a new database, one of the options is to change on-site `template1`. To do this, log into PostgreSQL shell (`psql`) and execute the following:

First, we need to drop `template1`. Templates cannot be dropped, so we first modify it so it is an ordinary database:

```
UPDATE pg_database SET datistemplate = FALSE WHERE datname = 'template1';

```

Now we can drop it:

```
DROP DATABASE template1;

```

The next step is to create a new database from `template0`, with a new default encoding:

```
CREATE DATABASE template1 WITH TEMPLATE = template0 ENCODING = 'UNICODE';

```

Now modify `template1` so it is actually a template:

```
UPDATE pg_database SET datistemplate = TRUE WHERE datname = 'template1';

```

Optionally, if you do not want anyone connecting to this template, set `datallowconn` to `FALSE`:

```
UPDATE pg_database SET datallowconn = FALSE WHERE datname = 'template1';

```

**Note:** This last step can create problems when upgrading via `pg_upgrade`.

Now you can create a new database:

```
[postgres]$ createdb blog

```

If you log back in to `psql` and check the databases, you should see the proper encoding of your new database:

```
\l

```

returns

```
                              List of databases
  Name    |  Owner   | Encoding  | Collation | Ctype |   Access privileges
-----------+----------+-----------+-----------+-------+----------------------
blog      | postgres | UTF8      | C         | C     |
postgres  | postgres | SQL_ASCII | C         | C     |
template0 | postgres | SQL_ASCII | C         | C     | =c/postgres
                                                     : postgres=CTc/postgres
template1 | postgres | UTF8      | C         | C     |

```

## Administration tools

*   **[phpPgAdmin](/index.php/PhpPgAdmin "PhpPgAdmin")** — Web-based administration tool for PostgreSQL.

	[http://phppgadmin.sourceforge.net](http://phppgadmin.sourceforge.net) || [phppgadmin](https://www.archlinux.org/packages/?name=phppgadmin)

*   **pgAdmin** — GUI-based administration tool for PostgreSQL.

	[http://www.pgadmin.org/](http://www.pgadmin.org/) || [pgadmin3](https://www.archlinux.org/packages/?name=pgadmin3)

## Setup HHVM to work with PostgreSQL

```
$ git clone [https://github.com/PocketRent/hhvm-pgsql.git](https://github.com/PocketRent/hhvm-pgsql.git)
$ cd hhvm-pgsql

```

If you do not use a nightly build, then run this command (verified on HHVM 3.6.1) to avoid compile errors:

```
$ git checkout tags/3.6.0

```

Then build the extension (if you do not need an improved support for Hack language, then remove -DHACK_FRIENDLY=ON):

```
$ hphpize
$ cmake -DHACK_FRIENDLY=ON .
$ make

```

Then copy the built extension:

```
# cp pgsql.so /etc/hhvm/

```

Add to /etc/hhvm/server.ini:

```
extension_dir = /etc/hhvm
hhvm.extensions[pgsql] = pgsql.so
```

## Upgrading PostgreSQL

Upgrading minor PostgreSQL versions (i.e. `9.2, 9.3, 9.4, 9.5`) requires some extra maintenance.

**Tip:** If you already migrated from 9.2 to 9.3 and you want to migrate from 9.3 to 9.4, change versions before executing commands. If `/var/lib/postgres/data-9.2` already exists and you just copy-paste all commands, `pg_upgrade` will complain about the wrong version of the database, because your version 9.3 database will be stored in `/var/lib/postgres/data-9.2/data/`.

### Quick guide

If you had custom settings in configuration files like `pg_hba.conf` and `postgresql.conf`, merge them into the new ones.

```
upgrade_pg.sh

```

```
## Set the old version that we want to upgrade from.
export FROM_VERSION=9.4

pacman -S --needed postgresql-old-upgrade
chown postgres:postgres /var/lib/postgres/
su - postgres -c "mv /var/lib/postgres/data /var/lib/postgres/data-${FROM_VERSION}"
su - postgres -c 'mkdir /var/lib/postgres/data'
su - postgres -c 'initdb --locale en_US.UTF-8 -E UTF8 -D /var/lib/postgres/data'
su - postgres -c "pg_upgrade -b /opt/pgsql-${FROM_VERSION}/bin/ -B /usr/bin/ -d /var/lib/postgres/data-${FROM_VERSION} -D /var/lib/postgres/data"

```

#### Troubleshooting

If the `pg_upgrade` step fails with the following messages,

	cannot write to log file pg_upgrade_internal.log

	Failure, exiting

	Make sure you are in a directory that the postgres user has enough rights to write the log file to (`/tmp` for example), or use `su - postgres` instead of `sudo -u postgres`.

	If you are in a directory that postgres user has enough rights to write the log file to however you still get this error then make sure `/var/lib/postgres` is owned by postgres

	LC_COLLATE error that says that old and new values are different

	Figure out what the old locale was, `C` or `en_US.UTF-8` for example, and force it when calling `initdb`.

	 `sudo -u postgres LC_ALL=C initdb -D /var/lib/postgres/data` 

	There seems to be a postmaster servicing the old cluster.

	Please shutdown that postmaster and try again.

	Make sure postgres is not running. If you still get the error, then chances are there is an old PID file you need to clear out.

	Find the old pid in old pg data,

```
  $ sudo -u postgres ls -l /var/lib/postgres/data-9.X
  total 88
  -rw------- 1 postgres postgres     4 Mar 25  2012 PG_VERSION
  drwx------ 8 postgres postgres  4096 Jul 17 00:36 base
  drwx------ 2 postgres postgres  4096 Jul 17 00:38 global
  drwx------ 2 postgres postgres  4096 Mar 25  2012 pg_clog
  -rw------- 1 postgres postgres  4476 Mar 25  2012 pg_hba.conf
  -rw------- 1 postgres postgres  1636 Mar 25  2012 pg_ident.conf
  drwx------ 4 postgres postgres  4096 Mar 25  2012 pg_multixact
  drwx------ 2 postgres postgres  4096 Jul 17 00:05 pg_notify
  drwx------ 2 postgres postgres  4096 Mar 25  2012 pg_serial
  drwx------ 2 postgres postgres  4096 Jul 17 00:53 pg_stat_tmp
  drwx------ 2 postgres postgres  4096 Mar 25  2012 pg_subtrans
  drwx------ 2 postgres postgres  4096 Mar 25  2012 pg_tblspc
  drwx------ 2 postgres postgres  4096 Mar 25  2012 pg_twophase
  drwx------ 3 postgres postgres  4096 Mar 25  2012 pg_xlog
  -rw------- 1 postgres postgres 19169 Mar 25  2012 postgresql.conf
  -rw------- 1 postgres postgres    48 Jul 17 00:05 postmaster.opts
  -rw------- 1 postgres postgres    80 Jul 17 00:05 postmaster.pid   # <-- This is the problem

```

	Move the old pid to temporary directory,

```
$ sudo -u postgres mv /var/lib/postgres/data-9.X/postmaster.pid /tmp

```

	ERROR: could not access file "$libdir/postgis-2.0": No such file or directory

	Retrieve `postgis-2.0.so` from [postgis](https://www.archlinux.org/packages/?name=postgis) for version postgresql 9.X () and copy it to `/opt/pgsql-9.X/lib` and make sure the privileges are readable by postgres user.

	Your installation references loadable libraries that are missing from the new installation.

	You can add these libraries to the new installation, or remove the functions using them from the old installation.

	A list of problem libraries is in the file

	loadable_libraries.txt

	Could not load library "$libdir/pg_upgrade_support"

	ERROR: could not access file "$libdir/pg_upgrade_support": No such file or directory

	It means you have leftovers from old failed pg_upgrade attempts that you never completed. So you'll need to start postgres with old data and

	in each database execute `DROP SCHEMA IF EXISTS binary_upgrade CASCADE;`

### Detailed instructions

**Note:** Official PostgreSQL [upgrade documentation](http://www.postgresql.org/docs/current/static/upgrading.html) should be followed.

**Warning:** The following instructions could cause data loss. **Use at your own risk**.

It is recommended to add the following to your `/etc/pacman.conf` file:

```
IgnorePkg = postgresql postgresql-libs

```

This will ensure you do not accidentally upgrade the database to an incompatible version. When an upgrade is available, pacman will notify you that it is skipping the upgrade because of the entry in `pacman.conf`. Minor version upgrades (e.g. 9.0.3 to 9.0.4) are safe to perform. However, if you do an accidental upgrade to a different major version (e.g. 9.0.x to 9.1.x), you might not be able to access any of your data. Always check the PostgreSQL home page ([http://www.postgresql.org/](http://www.postgresql.org/)) to be sure of what steps are required for each upgrade. For a bit about why this is the case, see the [versioning policy](http://www.postgresql.org/support/versioning).

There are two main ways to upgrade your PostgreSQL database. Read the official documentation for details.

For those wishing to use `pg_upgrade`, a [postgresql-old-upgrade](https://www.archlinux.org/packages/?name=postgresql-old-upgrade) package is available in the [official repositories](/index.php/Official_repositories "Official repositories") that will always run one major version behind the real PostgreSQL package. This can be installed side-by-side with the new version of PostgreSQL.

When you are ready, upgrade the following packages: [postgresql](https://www.archlinux.org/packages/?name=postgresql), [postgresql-libs](https://www.archlinux.org/packages/?name=postgresql-libs), and [postgresql-old-upgrade](https://www.archlinux.org/packages/?name=postgresql-old-upgrade). Note that the data directory does not change from version to version, so before running `pg_upgrade`, it is necessary to rename your existing data directory and migrate into a new directory. The new database must be initialized, as described near the top of this page.

```
# systemctl stop postgresql
# su - postgres -c 'mv /var/lib/postgres/data /var/lib/postgres/olddata'
# su - postgres -c 'initdb --locale en_US.UTF-8 -E UTF8 -D /var/lib/postgres/data'

```

The upgrade invocation will likely look something like the following. **Do not run this command blindly without understanding what it does!** Reference the [upstream pg_upgrade documentation](http://www.postgresql.org/docs/current/static/pgupgrade.html) for details.

```
# su - postgres -c 'pg_upgrade -d /var/lib/postgres/olddata/ -D /var/lib/postgres/data/ -b /opt/pgsql-9.4/bin/ -B /usr/bin/'

```

#### Manual dump and reload

You could also do something like this (after the upgrade and install of [postgresql-old-upgrade](https://www.archlinux.org/packages/?name=postgresql-old-upgrade)).

**Note:** Below are the commands for PostgreSQL 9.4\. You can find similar commands in `/opt/` for PostgreSQL 9.2.

```
# systemctl stop postgresql
# /opt/pgsql-9.4/bin/pg_ctl -D /var/lib/postgres/olddata/ start
# /opt/pgsql-9.4/bin/pg_dumpall >> old_backup.sql
# /opt/pgsql-9.4/bin/pg_ctl -D /var/lib/postgres/olddata/ stop
# systemctl start postgresql
# psql -f old_backup.sql postgres

```

## Troubleshooting

### Improve performance of small transactions

If you are using PostgresSQL on a local machine for development and it seems slow, you could try turning [synchronous_commit off](http://www.postgresql.org/docs/current/static/runtime-config-wal.html#GUC-SYNCHRONOUS-COMMIT) in the configuration. Beware of the [caveats](http://www.postgresql.org/docs/current/static/runtime-config-wal.html#GUC-SYNCHRONOUS-COMMIT), however.

 `/var/lib/postgres/data/postgresql.conf`  `synchronous_commit = off` 

### Prevent disk writes when idle

PostgreSQL periodically updates its internal "statistics" file. By default, this file is stored on disk, which prevents disks from spinning down on laptops and causes hard drive seek noise. It is simple and safe to relocate this file to a memory-only file system with the following configuration option:

 `/var/lib/postgres/data/postgresql.conf`  `stats_temp_directory = '/run/postgresql'` 

### Cannot connect to database through pg_connect()

Install [php-pgsql](https://www.archlinux.org/packages/?name=php-pgsql) and edit the `php.ini` file uncommenting the lines `extension=pdo_pgsql.so` and `extension=pgsql.so`, then restart `httpd`.