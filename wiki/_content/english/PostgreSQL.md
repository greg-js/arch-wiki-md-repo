Related articles

*   [PhpPgAdmin](/index.php/PhpPgAdmin "PhpPgAdmin")

[PostgreSQL](https://www.postgresql.org/) is an open source, community driven, standard compliant object-relational database system.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Initial configuration](#Initial_configuration)
*   [3 Create your first database/user](#Create_your_first_database/user)
*   [4 Familiarize with PostgreSQL](#Familiarize_with_PostgreSQL)
    *   [4.1 Access the database shell](#Access_the_database_shell)
*   [5 Optional configuration](#Optional_configuration)
    *   [5.1 Restricts access rights to the database superuser by default](#Restricts_access_rights_to_the_database_superuser_by_default)
    *   [5.2 Configure PostgreSQL to be accessible exclusively through UNIX Sockets](#Configure_PostgreSQL_to_be_accessible_exclusively_through_UNIX_Sockets)
    *   [5.3 Configure PostgreSQL to be accessible from remote hosts](#Configure_PostgreSQL_to_be_accessible_from_remote_hosts)
    *   [5.4 Configure PostgreSQL authenticate against PAM](#Configure_PostgreSQL_authenticate_against_PAM)
    *   [5.5 Change default data directory](#Change_default_data_directory)
    *   [5.6 Change default encoding of new databases to UTF-8](#Change_default_encoding_of_new_databases_to_UTF-8)
*   [6 Graphical tools](#Graphical_tools)
*   [7 Upgrading PostgreSQL](#Upgrading_PostgreSQL)
    *   [7.1 pg_upgrade](#pg_upgrade)
    *   [7.2 Manual dump and reload](#Manual_dump_and_reload)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Improve performance of small transactions](#Improve_performance_of_small_transactions)
    *   [8.2 Prevent disk writes when idle](#Prevent_disk_writes_when_idle)
    *   [8.3 pgAdmin 4 issues after upgrade to PostgreSQL 12](#pgAdmin_4_issues_after_upgrade_to_PostgreSQL_12)

## Installation

[Install](/index.php/Install "Install") the [postgresql](https://www.archlinux.org/packages/?name=postgresql) package. It will also create a system user called *postgres*.

**Warning:** See [#Upgrading PostgreSQL](#Upgrading_PostgreSQL) for necessary steps before installing new versions of the PostgreSQL packages.

**Note:** Commands that should be run as the *postgres* user are prefixed by `[postgres]$` in this article.

You can switch to the PostgreSQL user by executing the following command:

*   If you have [sudo](/index.php/Sudo "Sudo") and are in [sudoers](/index.php/Sudoers "Sudoers"):

	 `$ sudo -iu postgres` 

*   Otherwise using [su](/index.php/Su "Su"):

```
$ su
# su -l postgres

```

See [sudo(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sudo.8) or [su(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/su.1) for their usage.

## Initial configuration

Before PostgreSQL can function correctly, the database cluster must be initialized:

```
[postgres]$ initdb -D /var/lib/postgres/data

```

Where `-D` is the default location where the database cluster must be stored (see [#Change default data directory](#Change_default_data_directory) if you want to use a different one).

Note that by default, the locale and the encoding for the database cluster are derived from your current environment (using [$LANG](/index.php/Locale#LANG:_default_locale "Locale") value). [[1]](https://www.postgresql.org/docs/current/static/locale.html) However, depending on your settings and use cases this might not be what you want, and you can override the defaults using:

*   `--locale=*locale*`, where *locale* is to be chosen amongst the system's [available locales](/index.php/Locale#Generating_locales "Locale");
*   `-E *encoding*` for the encoding (which must match the chosen locale);

Example:

```
[postgres]$ initdb --locale=en_US.UTF-8 -E UTF8 -D /var/lib/postgres/data

```

Many lines should now appear on the screen with several ending by `... ok`:

```
The files belonging to this database system will be owned by user "postgres".
This user must also own the server process.

The database cluster will be initialized with locale "en_US.UTF-8".
The default database encoding has accordingly been set to "UTF8".
The default text search configuration will be set to "english".

Data page checksums are disabled.

fixing permissions on existing directory /var/lib/postgres/data ... ok
creating subdirectories ... ok
selecting default max_connections ... 100
selecting default shared_buffers ... 128MB
selecting dynamic shared memory implementation ... posix
creating configuration files ... ok
running bootstrap script ... ok
performing post-bootstrap initialization ... ok
syncing data to disk ... ok

WARNING: enabling "trust" authentication for local connections
You can change this by editing pg_hba.conf or using the option -A, or
--auth-local and --auth-host, the next time you run initdb.

Success. You can now start the database server using:

    pg_ctl -D /var/lib/postgres/ -l logfile start

```

If these are the kind of lines you see, then the process succeeded. Return to the regular user using `exit`.

**Note:** To read more about this `WARNING`, see [#Restricts access rights to the database superuser by default](#Restricts_access_rights_to_the_database_superuser_by_default).

**Tip:** If you change the root to something other than `/var/lib/postgres`, you will have to [edit](/index.php/Edit "Edit") the service file. If the root is under `home`, make sure to set `ProtectHome` to false.

**Warning:**

*   If the database resides on a [Btrfs](/index.php/Btrfs "Btrfs") file system, you should consider disabling [Copy-on-Write](/index.php/Btrfs#Copy-on-Write_(CoW) "Btrfs") for the directory before creating any database.
*   If the database resides on a [ZFS](/index.php/ZFS "ZFS") file system, you should consult [ZFS#Databases](/index.php/ZFS#Databases "ZFS") before creating any database.

Finally, [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the `postgresql.service`.

## Create your first database/user

**Tip:** If you create a PostgreSQL user with the same name as your Linux username, it allows you to access the PostgreSQL database shell without having to specify a user to login (which makes it quite convenient).

Become the postgres user. Add a new database user using the [createuser](https://www.postgresql.org/docs/current/static/app-createuser.html) command:

```
[postgres]$ createuser --interactive

```

Create a new database over which the above user has read/write privileges using the [createdb](https://www.postgresql.org/docs/current/static/app-createdb.html) command (execute this command from your login shell if the database user has the same name as your Linux user, otherwise add `-O *database-username*` to the following command):

```
$ createdb myDatabaseName

```

**Tip:** If you did not grant your new user database creation privileges, add `-U postgres` to the previous command.

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

The PostgreSQL database server configuration file is `postgresql.conf`. This file is located in the data directory of the server, typically `/var/lib/postgres/data`. This folder also houses the other main configuration files, including the `pg_hba.conf` which defines authentication settings, for both [local users](#Restricts_access_rights_to_the_database_superuser_by_default) and [other hosts ones](#Configure_PostgreSQL_to_be_accessible_from_remote_hosts).

**Note:** By default, this folder will not be browsable or searchable by a regular user. This is why `find` and `locate` are not finding the configuration files.

### Restricts access rights to the database superuser by default

The defaults `pg_hba.conf` **allow any local user to connect as any database user**, including the database superuser. This is likely not what you want, so in order to restrict global access to the *postgres* user, change the following line:

 `/var/lib/postgres/data/pg_hba.conf` 
```
# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     trust
```

To:

 `/var/lib/postgres/data/pg_hba.conf` 
```
# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             postgres                                peer
```

You might later add additional lines depending on your needs or software ones.

### Configure PostgreSQL to be accessible exclusively through UNIX Sockets

In the connections and authentications section of your configuration, set:

 `/var/lib/postgres/data/postgresql.conf`  `listen_addresses = ''` 

This will disable network listening completely. After this you should [restart](/index.php/Restart "Restart") `postgresql.service` for the changes to take effect.

### Configure PostgreSQL to be accessible from remote hosts

In the connections and authentications section, set the `listen_addresses` line to your needs:

 `/var/lib/postgres/data/postgresql.conf`  `listen_addresses = 'localhost,*my_local_ip_address'*` 

You can use `'*'` to listen on all available addresses.

**Note:** PostgreSQL uses TCP port `5432` by default for remote connections. Make sure this port is open in your [firewall](/index.php/Firewall "Firewall") and able to receive incoming connections. You can also change it in the configuration file, right below `listen_addresses`

Then add a line like the following to the authentication config:

 `/var/lib/postgres/data/pg_hba.conf` 
```
# TYPE  DATABASE        USER            ADDRESS                 METHOD
# IPv4 local connections:
host    all             all             *ip_address*/32   md5
```

where `*ip_address*` is the IP address of the remote client.

See the documentation for [pg_hba.conf](https://www.postgresql.org/docs/current/static/auth-pg-hba-conf.html).

**Note:** Neither sending your plain password nor the md5 hash (used in the example above) over the Internet is secure if it is not done over an SSL-secured connection. See [Secure TCP/IP Connections with SSL](https://www.postgresql.org/docs/current/static/ssl-tcp.html) for how to configure PostgreSQL with SSL.

After this you should [restart](/index.php/Restart "Restart") `postgresql.service` for the changes to take effect.

For troubleshooting take a look in the server log file:

```
$ journalctl -u postgresql.service

```

### Configure PostgreSQL authenticate against PAM

PostgreSQL offers a number of authentication methods. If you would like to allow users to authenticate with their system password, additional steps are necessary. First you need to enable [PAM](/index.php/PAM "PAM") for the connection.

For example, the same configuration as above, but with PAM enabled:

 `/var/lib/postgres/data/pg_hba.conf` 
```
# IPv4 local connections:
host   all   all   *my_remote_client_ip_address*/32   pam
```

The PostgreSQL server is however running without root privileges and will not be able to access `/etc/shadow`. We can work around that by allowing the postgres group to access this file:

```
# setfacl -m g:postgres:r /etc/shadow

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

**Note:** If you ran `initdb` with `-E UTF8` or while using an UTF-8 locale, these steps are not required.

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

## Graphical tools

*   **[phpPgAdmin](/index.php/PhpPgAdmin "PhpPgAdmin")** — Web-based administration tool for PostgreSQL.

	[http://phppgadmin.sourceforge.net](http://phppgadmin.sourceforge.net) || [phppgadmin](https://www.archlinux.org/packages/?name=phppgadmin)

*   **pgAdmin** — Comprehensive design and management GUI for PostgreSQL.

	[https://www.pgadmin.org/](https://www.pgadmin.org/) || [pgadmin3](https://aur.archlinux.org/packages/pgadmin3/) or [pgadmin4](https://www.archlinux.org/packages/?name=pgadmin4)

*   **pgModeler** — Graphical schema designer for PostgreSQL.

	[https://pgmodeler.io/](https://pgmodeler.io/) || [pgmodeler](https://aur.archlinux.org/packages/pgmodeler/)

For tools supporting multiple DBMSs, see [List of applications/Documents#Database tools](/index.php/List_of_applications/Documents#Database_tools "List of applications/Documents").

## Upgrading PostgreSQL

Upgrading major PostgreSQL versions requires some extra maintenance.

**Note:**

*   Official PostgreSQL [upgrade documentation](https://www.postgresql.org/docs/current/static/upgrading.html) should be followed.
*   From version `10.0` onwards PostgreSQL [changed its versioning scheme](https://www.postgresql.org/about/news/1786/). Earlier upgrade from version `9.*x*` to `9.*y*` was considered as major upgrade. Now upgrade from version `10.*x*` to `10.*y*` is considered as minor upgrade and upgrade from version `10.*x*` to `11.*y*` is considered as major upgrade.

**Warning:** The following instructions could cause data loss. Do not run the commands below blindly, without understanding what they do. [Backup database](https://www.postgresql.org/docs/current/static/backup.html) first.

Get the currently used database version via

```
# cat /var/lib/postgres/data/PG_VERSION

```

To ensure you do not accidentally upgrade the database to an incompatible version, it is recommended to [skip updates](/index.php/Pacman#Skip_package_from_being_upgraded "Pacman") to the PostgreSQL packages:

 `/etc/pacman.conf` 
```
...
IgnorePkg = postgresql postgresql-libs
...
```

Minor version upgrades are safe to perform. However, if you do an accidental upgrade to a different major version, you might not be able to access any of your data. Always check the [PostgreSQL home page](https://www.postgresql.org/) to be sure of what steps are required for each upgrade. For a bit about why this is the case, see the [versioning policy](https://www.postgresql.org/support/versioning).

There are two main ways to upgrade your PostgreSQL database. Read the official documentation for details.

### pg_upgrade

For those wishing to use `pg_upgrade`, a [postgresql-old-upgrade](https://www.archlinux.org/packages/?name=postgresql-old-upgrade) package is available that will always run one major version behind the real PostgreSQL package. This can be installed side-by-side with the new version of PostgreSQL. To upgrade from older versions of PostgreSQL there are AUR packages available: [postgresql-96-upgrade](https://aur.archlinux.org/packages/postgresql-96-upgrade/), [postgresql-95-upgrade](https://aur.archlinux.org/packages/postgresql-95-upgrade/), [postgresql-94-upgrade](https://aur.archlinux.org/packages/postgresql-94-upgrade/), [postgresql-93-upgrade](https://aur.archlinux.org/packages/postgresql-93-upgrade/), [postgresql-92-upgrade](https://aur.archlinux.org/packages/postgresql-92-upgrade/). Read the [pg_upgrade(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pg_upgrade.1) man page to understand what actions it performs.

Note that the databases cluster directory does not change from version to version, so before running `pg_upgrade`, it is necessary to rename your existing data directory and migrate into a new directory. The new databases cluster must be initialized, as described in the [#Installation](#Installation) section.

When you are ready, stop the postgresql service, upgrade the following packages: [postgresql](https://www.archlinux.org/packages/?name=postgresql), [postgresql-libs](https://www.archlinux.org/packages/?name=postgresql-libs), and [postgresql-old-upgrade](https://www.archlinux.org/packages/?name=postgresql-old-upgrade). Finally upgrade the databases cluster.

Stop and make sure PostgreSQL is stopped:

```
# systemctl stop postgresql.service
# systemctl status postgresql.service

```

Upgrade the packages:

```
# pacman -S postgresql postgresql-libs postgresql-old-upgrade

```

Rename the databases cluster directory, and create an empty one:

```
# mv /var/lib/postgres/data /var/lib/postgres/olddata
# mkdir /var/lib/postgres/data /var/lib/postgres/tmp
# chown postgres:postgres /var/lib/postgres/data /var/lib/postgres/tmp
[postgres]$ cd /var/lib/postgres/tmp
[postgres]$ initdb -D /var/lib/postgres/data

```

Upgrade the cluster, replacing `*PG_VERSION*` below, with the old PostgreSQL version number (e.g. `11`):

```
[postgres]$ pg_upgrade -b /opt/pgsql-*PG_VERSION*/bin -B /usr/bin -d /var/lib/postgres/olddata -D /var/lib/postgres/data

```

`pg_upgrade` will perform the upgrade and create some scripts in `/var/lib/postgres/tmp/`. Follow the instructions given on screen and act accordingly. You may delete the `/var/lib/postgres/tmp` directory once the upgrade is completely over.

If necessary, adjust the configuration files of new cluster (e.g. `pg_hba.conf` and `postgresql.conf`) to match the old cluster.

Start the cluster:

```
# systemctl start postgresql.service

```

### Manual dump and reload

You could also do something like this (after the upgrade and install of [postgresql-old-upgrade](https://www.archlinux.org/packages/?name=postgresql-old-upgrade)).

**Note:**

*   Below are the commands for upgrading from PostgreSQL 11\. You can find similar commands in `/opt/` for your version of PostgreSQL cluster, provided you have matching version of [postgresql-old-upgrade](https://www.archlinux.org/packages/?name=postgresql-old-upgrade) package installed.
*   If you had customized your `pg_hba.conf` file, you may have to temporarily modify it to allow full access to old database cluster from local system. After upgrade is complete set your customization to new database cluster as well and [restart](/index.php/Restart "Restart") `postgresql.service`.

```
# systemctl stop postgresql.service
# mv /var/lib/postgres/data /var/lib/postgres/olddata
# mkdir /var/lib/postgres/data
# chown postgres:postgres /var/lib/postgres/data
[postgres]$ initdb -D /var/lib/postgres/data
[postgres]$ /opt/pgsql-11/bin/pg_ctl -D /var/lib/postgres/olddata/ start
[postgres]$ pg_dumpall -h /tmp -f /tmp/old_backup.sql
[postgres]$ /opt/pgsql-11/bin/pg_ctl -D /var/lib/postgres/olddata/ stop
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

### pgAdmin 4 issues after upgrade to PostgreSQL 12

If you see errors about `string indices must be integers` when navigating the tree on the left, or about `column rel.relhasoids does not exist` when viewing the data, remove the server from the connection list in pgAdmin and add a fresh server instance. pgAdmin will otherwise continue to treat the server as a PostgreSQL 11 server resulting in these issues.