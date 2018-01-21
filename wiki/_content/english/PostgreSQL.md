Related articles

*   [PhpPgAdmin](/index.php/PhpPgAdmin "PhpPgAdmin")

[PostgreSQL](https://www.postgresql.org/) is an open source, community driven, standard compliant object-relational database system.

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
    *   [7.1 Manual dump and reload](#Manual_dump_and_reload)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Improve performance of small transactions](#Improve_performance_of_small_transactions)
    *   [8.2 Prevent disk writes when idle](#Prevent_disk_writes_when_idle)
    *   [8.3 Cannot connect to database through pg_connect()](#Cannot_connect_to_database_through_pg_connect.28.29)

## Installing PostgreSQL

[Install](/index.php/Install "Install") the [postgresql](https://www.archlinux.org/packages/?name=postgresql) package. Then [set a password](/index.php/Users_and_groups#Example_adding_a_user "Users and groups") for the newly created *postgres* user.

Then, switch to the default PostgreSQL user *postgres* by executing the following command:

*   If you have [sudo](/index.php/Sudo "Sudo") and your username is in `sudoers`:

	 `$ sudo -u postgres -i` 

*   Otherwise use [su](/index.php/Su "Su"):

```
$ su
# su -l postgres

```

See [sudo(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sudo.8) or [su(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/su.1) for their usage.

**Note:** Commands that should be run as the postgres user are prefixed by `[postgres]$` in this article.

Before PostgreSQL can function correctly, the database cluster must be initialized:

```
[postgres]$ initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data'

```

Where:

*   the `--locale` is the one defined in the file `/etc/locale.conf`;
*   the `-E` is the default encoding of the database that will be created in the future;
*   and `-D` is the default location where the database cluster must be stored.

Many lines should now appear on the screen with several ending by `... ok`:

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

If these are the kind of lines you see, then the process succeeded. Return to the regular user using `exit`.

As root, [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `postgresql.service`. See [#Upgrading PostgreSQL](#Upgrading_PostgreSQL) for necessary steps before installing new versions of the PostgreSQL packages.

**Tip:** If you change the root to something other than `/var/lib/postgres`, you will have to [edit](/index.php/Edit "Edit") the service file. If the root is under `home`, make sure to set `ProtectHome` to false.

**Warning:** If the database resides on a [Btrfs](/index.php/Btrfs "Btrfs") file system, you should consider disabling [Copy-on-Write](/index.php/Btrfs#Copy-on-Write_.28CoW.29 "Btrfs") for the directory before creating any database. If the database resides on a [ZFS](/index.php/ZFS "ZFS") file system, you should consult [ZFS#Database](/index.php/ZFS#Database "ZFS") before creating any database.

## Create your first database/user

**Tip:** If you create a PostgreSQL user with the same name as your Linux username, it allows you to access the PostgreSQL database shell without having to specify a user to login (which makes it quite convenient).

Become the postgres user. Add a new database user using the [createuser](https://www.postgresql.org/docs/current/static/app-createuser.html) command:

```
[postgres]$ createuser --interactive

```

Create a new database over which the above user has read/write privileges using the [createdb](https://www.postgresql.org/docs/current/static/app-createdb.html) command (execute this command from your login shell if the database user has the same name as your Linux user, otherwise add `-U *database-username*` to the following command):

```
$ createdb myDatabaseName

```

## Familiarize with PostgreSQL

### Access the database shell

Become the postgres user. Start the primary database shell, [psql](https://www.postgresql.org/docs/current/static/app-psql.html), where you can do all your creation of databases/tables, deletion, set permissions, and run raw SQL commands. Use the `-d` option to connect to the database you created (without specifying a database, `psql` will try to access a database that matches your username).

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
listen_addresses = 'localhost,*my_local_ip_address'*
#You can use '*' to listen on all local addresses

```

Take a careful look at the other lines.

Host-based authentication is configured in `/var/lib/postgres/data/pg_hba.conf`. This file controls which hosts are allowed to connect. Note that the defaults **allow any local user to connect as any database user**, including the database superuser. Add a line like the following:

```
# IPv4 local connections:
host   all   all   *my_remote_client_ip_address*/32   md5

```

where `my_remote_client_ip_address` is the IP address of the client.

See the documentation for [pg_hba.conf](https://www.postgresql.org/docs/current/static/auth-pg-hba-conf.html).

**Note:** Neither sending your plain password nor the md5 hash (used in the example above) over the Internet is secure if it is not done over an SSL-secured connection. See [Secure TCP/IP Connections with SSL](https://www.postgresql.org/docs/current/static/ssl-tcp.html) for how to configure PostgreSQL with SSL.

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

[Edit](/index.php/Edit "Edit") `postgresql.service` to create a drop-in file and override the `Environment` and `PIDFile` settings. For example:

```
[Service]
Environment=PGROOT=*/pathto/pgroot*
PIDFile=*/pathto/pgroot/*data/postmaster.pid

```

If you want to use `/home` directory for default directory or for tablespaces, add one more line in this file:

```
ProtectHome=false

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

 `\l` 
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

*   **[Adminer](/index.php/Adminer "Adminer")** — Web-based database management tool for multiple database systems.

	[https://www.adminer.org](https://www.adminer.org) || [adminer](https://aur.archlinux.org/packages/adminer/)

*   **[phpPgAdmin](/index.php/PhpPgAdmin "PhpPgAdmin")** — Web-based administration tool for PostgreSQL.

	[http://phppgadmin.sourceforge.net](http://phppgadmin.sourceforge.net) || [phppgadmin](https://www.archlinux.org/packages/?name=phppgadmin)

*   **pgAdmin** — GUI-based administration tool for PostgreSQL.

	[https://www.pgadmin.org/](https://www.pgadmin.org/) || [pgadmin4](https://www.archlinux.org/packages/?name=pgadmin4)

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

Upgrading major PostgreSQL versions requires some extra maintenance.

**Note:**

*   Official PostgreSQL [upgrade documentation](https://www.postgresql.org/docs/current/static/upgrading.html) should be followed.
*   From version `10.0` onwards PostgreSQL [changed its versioning scheme](https://www.postgresql.org/about/news/1786/). Earlier upgrade from version `9.*x*` to `9.*y*` was considered as major upgrade. Now upgrade from version `10.*x*` to `10.*y*` is considered as minor upgrade and upgrade from version `10.*x*` to `11.*y*` is considered as major upgrade.

**Warning:** The following instructions could cause data loss. **Use at your own risk**.

It is recommended to add the following to your `/etc/pacman.conf` file:

```
IgnorePkg = postgresql postgresql-libs

```

This will ensure you do not accidentally upgrade the database to an incompatible version. When an upgrade is available, pacman will notify you that it is skipping the upgrade because of the entry in `pacman.conf`. Minor version upgrades are safe to perform. However, if you do an accidental upgrade to a different major version, you might not be able to access any of your data. Always check the [PostgreSQL home page](https://www.postgresql.org/) to be sure of what steps are required for each upgrade. For a bit about why this is the case, see the [versioning policy](https://www.postgresql.org/support/versioning).

There are two main ways to upgrade your PostgreSQL database. Read the official documentation for details.

For those wishing to use `pg_upgrade`, a [postgresql-old-upgrade](https://www.archlinux.org/packages/?name=postgresql-old-upgrade) package is available that will always run one major version behind the real PostgreSQL package. This can be installed side-by-side with the new version of PostgreSQL.

When you are ready, upgrade the following packages: [postgresql](https://www.archlinux.org/packages/?name=postgresql), [postgresql-libs](https://www.archlinux.org/packages/?name=postgresql-libs), and [postgresql-old-upgrade](https://www.archlinux.org/packages/?name=postgresql-old-upgrade). Note that the data directory does not change from version to version, so before running `pg_upgrade`, it is necessary to rename your existing data directory and migrate into a new directory. The new database must be initialized, as described near the top of this page.

```
# systemctl stop postgresql.service
# mv /var/lib/postgres/data /var/lib/postgres/olddata
# mkdir /var/lib/postgres/data /var/lib/postgres/tmp
# chown postgres:postgres /var/lib/postgres/data /var/lib/postgres/tmp
[postgres]$ initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data'

```

The upgrade invocation will likely look something like the following. **Do not run this command blindly without understanding what it does!** Reference the [upstream pg_upgrade documentation](https://www.postgresql.org/docs/current/static/pgupgrade.html) for details.

```
[postgres]$ cd /var/lib/postgres/tmp
[postgres]$ pg_upgrade -b /opt/pgsql-9.6/bin -B /usr/bin -d /var/lib/postgres/olddata -D /var/lib/postgres/data

```

pg_upgrade will perform the upgrade and create some scripts in `/var/lib/postgres/tmp`. Follow the instructions given on screen and act accordingly. You may delete `/var/lib/postgres/tmp` directory once the upgrade is completely over.

### Manual dump and reload

You could also do something like this (after the upgrade and install of [postgresql-old-upgrade](https://www.archlinux.org/packages/?name=postgresql-old-upgrade)).

**Note:**

*   Below are the commands for PostgreSQL 9.6\. You can find similar commands in `/opt/` for PostgreSQL 9.2.
*   If you had customized your `pg_hba.conf` file, you may have to temporarily modify it to allow full access to old database cluster from local system. After upgrade is complete set your customization to new database cluster as well and [restart](/index.php/Restart "Restart") `postgresql.service`.

```
# systemctl stop postgresql.service
# mv /var/lib/postgres/data /var/lib/postgres/olddata
# mkdir /var/lib/postgres/data
# chown postgres:postgres /var/lib/postgres/data
[postgres]$ initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data'
[postgres]$ /opt/pgsql-9.6/bin/pg_ctl -D /var/lib/postgres/olddata/ start
[postgres]$ pg_dumpall -f /tmp/old_backup.sql
[postgres]$ /opt/pgsql-9.6/bin/pg_ctl -D /var/lib/postgres/olddata/ stop
# systemctl start postgresql.service
[postgres]$ psql -f /tmp/old_backup.sql postgres

```

## Troubleshooting

### Improve performance of small transactions

If you are using PostgresSQL on a local machine for development and it seems slow, you could try turning [synchronous_commit off](https://www.postgresql.org/docs/current/static/runtime-config-wal.html#GUC-SYNCHRONOUS-COMMIT) in the configuration. Beware of the [caveats](https://www.postgresql.org/docs/current/static/runtime-config-wal.html#GUC-SYNCHRONOUS-COMMIT), however.

 `/var/lib/postgres/data/postgresql.conf`  `synchronous_commit = off` 

### Prevent disk writes when idle

PostgreSQL periodically updates its internal "statistics" file. By default, this file is stored on disk, which prevents disks from spinning down on laptops and causes hard drive seek noise. It is simple and safe to relocate this file to a memory-only file system with the following configuration option:

 `/var/lib/postgres/data/postgresql.conf`  `stats_temp_directory = '/run/postgresql'` 

### Cannot connect to database through pg_connect()

Install [php-pgsql](https://www.archlinux.org/packages/?name=php-pgsql) and edit the `php.ini` file uncommenting the lines `extension=pdo_pgsql.so` and `extension=pgsql.so`, then restart `httpd`.