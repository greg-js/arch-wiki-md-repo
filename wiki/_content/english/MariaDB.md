Related articles

*   [phpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin")
*   [Adminer](/index.php/Adminer "Adminer")
*   [JDBC and MySQL](/index.php/JDBC_and_MySQL "JDBC and MySQL")
*   [Open Database Connectivity](/index.php/Open_Database_Connectivity "Open Database Connectivity")

[MariaDB](https://en.wikipedia.org/wiki/MariaDB "wikipedia:MariaDB") is a reliable, high performance and full-featured database server which aims to be an 'always Free, backward compatible, drop-in' replacement of [MySQL](/index.php/MySQL "MySQL"). Since 2013 MariaDB is Arch Linux's default implementation of MySQL.[[1]](https://www.archlinux.org/news/mariadb-replaces-mysql-in-repositories/)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Improve security](#Improve_security)
    *   [2.2 Add user](#Add_user)
    *   [2.3 Configuration files](#Configuration_files)
    *   [2.4 Grant remote access](#Grant_remote_access)
    *   [2.5 Disable remote access](#Disable_remote_access)
    *   [2.6 Enable auto-completion](#Enable_auto-completion)
    *   [2.7 Using UTF8MB4](#Using_UTF8MB4)
    *   [2.8 Increase character limit](#Increase_character_limit)
    *   [2.9 Using a TMPFS for tmpdir](#Using_a_TMPFS_for_tmpdir)
    *   [2.10 Time zone tables](#Time_zone_tables)
*   [3 Database maintenance](#Database_maintenance)
    *   [3.1 Upgrade databases on major releases](#Upgrade_databases_on_major_releases)
    *   [3.2 Checking, optimizing and repairing databases](#Checking,_optimizing_and_repairing_databases)
*   [4 Backup](#Backup)
    *   [4.1 Compression](#Compression)
    *   [4.2 Non-interactive](#Non-interactive)
        *   [4.2.1 Example script](#Example_script)
    *   [4.3 Holland Backup](#Holland_Backup)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Unable to run mysql_upgrade because MySQL cannot start](#Unable_to_run_mysql_upgrade_because_MySQL_cannot_start)
    *   [5.2 Reset the root password](#Reset_the_root_password)
    *   [5.3 Check and repair all tables](#Check_and_repair_all_tables)
    *   [5.4 Optimize all tables](#Optimize_all_tables)
    *   [5.5 OS error 22 when running on ZFS](#OS_error_22_when_running_on_ZFS)
    *   [5.6 Cannot login through CLI, but phpmyadmin works well](#Cannot_login_through_CLI,_but_phpmyadmin_works_well)
    *   [5.7 MySQL binary logs are taking up huge disk space](#MySQL_binary_logs_are_taking_up_huge_disk_space)
    *   [5.8 OpenRC fails to start MySQL](#OpenRC_fails_to_start_MySQL)
    *   [5.9 Specified key was too long](#Specified_key_was_too_long)
    *   [5.10 Changed limits warning on max_open_files/table_open_cache](#Changed_limits_warning_on_max_open_files/table_open_cache)
*   [6 See also](#See_also)

## Installation

[MariaDB](https://mariadb.com/) is the [default implementation](https://www.archlinux.org/news/mariadb-replaces-mysql-in-repositories/) of MySQL in Arch Linux, provided with the [mariadb](https://www.archlinux.org/packages/?name=mariadb) package.

**Tip:**

*   If the database (in `/var/lib/mysql`) resides on a [Btrfs](/index.php/Btrfs "Btrfs") file system, you should consider disabling [Copy-on-Write](/index.php/Btrfs#Copy-on-Write_(CoW) "Btrfs") for the directory before creating any database.
*   If the database resides on a [ZFS](/index.php/ZFS "ZFS") file system, you should consult [ZFS#Databases](/index.php/ZFS#Databases "ZFS") before creating any database.

Install [mariadb](https://www.archlinux.org/packages/?name=mariadb), afterwards run the following command **before starting** the `mariadb.service`:

```
# mariadb-install-db --user=mysql --basedir=/usr --datadir=/var/lib/mysql

```

**Note:** For security reasons, the systemd service file contains `ProtectHome=true`, which prevents MariaDB from accessing files under the `/home`, `/root` and `/run/user` hierarchies. The `datadir` has to be in an accessible location and [owned](/index.php/Chown "Chown") by the `mysql` user and group. You can modify this behavior by creating a supplementary service file as described here: [https://mariadb.com/kb/en/mariadb/systemd/](https://mariadb.com/kb/en/mariadb/systemd/)

Now the `mariadb.service` can be started and/or enabled with [systemd](/index.php/Systemd#Using_units "Systemd").

**Tip:** If you use something different from `/var/lib/mysql` for your data dir, you need to set `datadir=<YOUR_DATADIR>` under section `[mysqld]` of your `/etc/my.cnf.d/server.cnf`.

To simplify administration, you might want to install a [front-end](/index.php/MySQL#Graphical_tools "MySQL").

## Configuration

Once you have started the MySQL server and added a root account, you may want to change the default configuration.

To log in as `root` on the MySQL server, use the following command:

```
# mysql -u root -p

```

**Note:** The default password is empty. Press Enter to log in.

### Improve security

The `mysql_secure_installation` command will interactively guide you through a number of recommended security measures at the database level:

```
# mysql_secure_installation

```

### Add user

Creating a new user takes two steps: create the user; grant privileges. In the below example, the user *monty* with *some_pass* as password is being created, then granted full permissions to the database *mydb*:

 `$ mysql -u root -p` 
```
MariaDB> CREATE USER 'monty'@'localhost' IDENTIFIED BY 'some_pass';
MariaDB> GRANT ALL PRIVILEGES ON mydb.* TO 'monty'@'localhost';
MariaDB> FLUSH PRIVILEGES;
MariaDB> quit
```

### Configuration files

*MariaDB* configuration options are read from the following files in the given order (according to `mysqld --help --verbose` output):

```
/etc/my.cnf /etc/my.cnf.d/ ~/.my.cnf

```

Depending on the scope of the changes you want to make (system-wide, user-only...), use the corresponding file. See [this entry](https://mariadb.com/kb/en/library/configuring-mariadb-with-option-files/) of the Knowledge Base for more information.

### Grant remote access

**Warning:** This is not considered as best practice and may cause security issues. Consider using [Secure Shell](/index.php/Secure_Shell "Secure Shell"), [VNC](/index.php/VNC "VNC") or [VPN](/index.php/VPN "VPN"), if you want to maintain the MySQL-server outside and/or inside your LAN.

If you want to access your MySQL server from other LAN hosts, you have to edit the following lines in `/etc/my.cnf.d/server.cnf`:

```
[mysqld]
   ...
   #skip-networking
   bind-address = <some ip-address>
   ...

```

Grant any MySQL user remote access (example for root):

```
# mysql -u root -p

```

Check current users with remote access privileged:

```
SELECT User, Host FROM mysql.user WHERE Host <> 'localhost';

```

Now grant remote access for your user (here root)::

```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'192.168.1.%' IDENTIFIED BY 'my_optional_remote_password' WITH GRANT OPTION;

```

You can change the '%' wildcard to a specific host if you like. The password can be different from user's main password.

### Disable remote access

The MySQL server is accessible from the network by default. If MySQL is only needed for the localhost, you can improve security by not listening on TCP port 3306\. To refuse remote connections, uncomment the following line in `/etc/my.cnf.d/server.cnf`:

```
skip-networking

```

You will still be able to log in from the localhost.

### Enable auto-completion

**Note:** Enabling this feature can make the client initialization longer.

The MySQL client completion feature is disabled by default. To enable it system-wide edit `/etc/mysql/my.cnf`, and replace `no-auto-rehash` by `auto-rehash` (or add if it doesn't exist). Note that this must be placed under `mysql` and not `mysqld`. Completion will be enabled next time you run the MySQL client.

### Using UTF8MB4

**Warning:** Before changing the character set be sure to create a backup first.

**Note:**

*   The [mariadb](https://www.archlinux.org/packages/?name=mariadb) package already uses `utf8mb4` as charset and `utf8mb4_unicode_ci` as collation. Users using the default (character) settings may want to skip this section.
*   UTF8MB4 is recommended over UTF-8 since it allows full Unicode support [[2]](https://mathiasbynens.be/notes/mysql-utf8mb4) [[3]](https://stackoverflow.com/questions/30074492/what-is-the-difference-between-utf8mb4-and-utf8-charsets-in-mysql).

[Append](/index.php/Append "Append") the following values to the main configuration file located at `/etc/mysql/my.cnf`:

```
[client]
default-character-set = utf8mb4

[mysqld]
collation_server = utf8mb4_unicode_ci
character_set_server = utf8mb4

[mysql]
default-character-set = utf8mb4

```

[Restart](/index.php/Restart "Restart") `mariadb.service` to apply the changes.

See [#Database maintenance](#Database_maintenance) to optimize and check the database health.

### Increase character limit

**Note:** The character-limit depends on the character-set in use [[4]](http://mechanics.flite.com/blog/2014/07/29/using-innodb-large-prefix-to-avoid-error-1071/) [[5]](https://dev.mysql.com/doc/refman/5.5/en/innodb-parameters.html#sysvar_innodb_large_prefix) [[6]](https://easyengine.io/tutorials/mysql/enable-innodb-file-per-table/).

For InnoDB execute the following commands to support a higher character-limit:

```
mysql> set global innodb_file_format = BARRACUDA;
Query OK, 0 rows affected (0.00 sec)

```

```
mysql> set global innodb_file_per_table = ON;
Query OK, 0 rows affected (0.00 sec)

```

```
mysql> set global innodb_large_prefix = ON;
Query OK, 0 rows affected (0.00 sec)

```

[Append](/index.php/Append "Append") the following lines in `/etc/mysql/my.cnf` to always use a higher character-limit:

```
[mysqld]
innodb_file_format = barracuda
innodb_file_per_table = 1
innodb_large_prefix = 1

```

[Restart](/index.php/Restart "Restart") `mariadb.service` to apply the changes.

On table creating append the `ROW_FORMAT` as seen in the example:

```
mysql> create table if not exists products (
   ->   day date not null,
   ->   product_id int not null,
   ->   dimension1 varchar(500) not null,
   ->   dimension2 varchar(500) not null,
   ->   unique index unique_index (day, product_id, dimension1, dimension2)
   -> ) ENGINE=InnoDB ROW_FORMAT=DYNAMIC;
Query OK, 0 rows affected (0.02 sec)

```

### Using a TMPFS for tmpdir

The directory used by MySQL for storing temporary files is named *tmpdir*. For example, it is used to perform disk based large sorts, as well as for internal and explicit temporary tables.

Create the directory with appropriate permissions:

```
# mkdir -pv /var/lib/mysqltmp
# chown mysql:mysql /var/lib/mysqltmp

```

Find the id and gid of the `mysql` user and group:

```
$ id mysql
uid=27(mysql) gid=27(mysql) groups=27(mysql)

```

Add to your `/etc/fstab` file.

```
 tmpfs   /var/lib/mysqltmp   tmpfs   rw,gid=27,uid=27,size=100M,mode=0750,noatime   0 0

```

Add to your `/etc/mysql/my.cnf` file under the `mysqld` group:

```
 tmpdir      = /var/lib/mysqltmp

```

Then reboot or ( shutdown mysql, mount the tmpdir, start mysql ).

### Time zone tables

Although time zone tables are created during the installation, they are not automatically populated. They need to be populated if you are planning on using CONVERT_TZ() in SQL queries.

To populate the time zone tables with all the time zones:

```
$ mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -u root -p mysql

```

Optionally, you may populate the table with specific time zone files:

```
$ mysql_tzinfo_to_sql <timezone_file> <timezone_name> | mysql -u root -p mysql

```

## Database maintenance

### Upgrade databases on major releases

Upon a major version release of [mariadb](https://www.archlinux.org/packages/?name=mariadb) (for example mariadb-10.1.10-1 to mariadb-10.1.18-1), it is wise to upgrade databases:

```
# mysql_upgrade -u root -p

```

To upgrade from 10.1.x to 10.3.x:

*   keep the 10.1.x database daemon running
*   upgrade the package
*   run `mysql_upgrade` (from the new package version) against the old still-running daemon. This will produce some error messages; however, the upgrade will succeed.
*   restart the daemon, so the 10.3.x daemon runs.

Alternatively, stop the (old) daemon, run the (new) daemon in safe mode, run `mysql_upgrade` against that, and then start the (new) daemon as described below in [troubleshooting](#Unable_to_run_mysql_upgrade_because_MySQL_cannot_start).

### Checking, optimizing and repairing databases

[mariadb](https://www.archlinux.org/packages/?name=mariadb) ships with `mysqlcheck` which can be used to check, repair, and optimize tables within databases from the shell. See the mysqlcheck man page for more. Several command tasks are shown:

To check all tables in all databases:

```
$ mysqlcheck --all-databases -u root -p -c

```

To analyze all tables in all databases:

```
$ mysqlcheck --all-databases -u root -p -a

```

To repair all tables in all databases:

```
$ mysqlcheck --all-databases -u root -p -r

```

To optimize all tables in all databases:

```
$ mysqlcheck --all-databases -u root -p -o

```

## Backup

There are various [tools and strategies](https://mariadb.com/kb/en/mariadb/documentation/backing-up-and-restoring/) to back up your databases.

If you are using the default InnoDB storage engine, a [suggested](https://mariadb.com/kb/en/mariadb/documentation/clients-and-utilities/backup-restore-and-import/mysqldump/#examples) way of backing up all your bases online while provisioning for [point-in-time recovery](https://dev.mysql.com/doc/refman/5.6/en/point-in-time-recovery.html) (also known as “roll-forward,” when you need to restore an old backup and replay the changes that happened since that backup) is to execute the following command:

```
$ mysqldump --single-transaction --flush-logs --master-data=2 --all-databases -u root -p > all_databases.sql

```

This will prompt for **MariaDB's** root user's password, which was defined during database [#Configuration](#Configuration).

Specifying the password on the command line is [strongly discouraged](https://dev.mysql.com/doc/refman/5.6/en/password-security-user.html), as it exposes it to discovery by other users through the use of `ps aux` or other techniques. Instead, the aforementioned command will prompt for the specified user's password, concealing it away.

### Compression

As SQL tables can get pretty large, it is recommended to pipe the output of the aforementioned command in a compression utility like [gzip](https://www.archlinux.org/packages/?name=gzip):

```
$ mysqldump --single-transaction --flush-logs --master-data=2 --all-databases -u root -p | gzip > all_databases.sql.gz

```

Decompressing the backup thus created and reloading it in the server is achieved by doing:

```
$ zcat all_databases.sql.gz | mysql -u root -p

```

This will recreate and repopulate all the databases previously backed up (see [this](https://stackoverflow.com/questions/23180963/restore-all-mysql-database-from-a-all-database-sql-gz-file#comment35453351_23180977) or [this](http://www.linuxquestions.org/questions/linux-server-73/how-to-restore-mysqldump-all-databases-backup-892922/)).

### Non-interactive

If you want to setup non-interactive backup script for use in [cron](/index.php/Cron "Cron") jobs or [systemd timers](/index.php/Systemd/cron_functionality "Systemd/cron functionality"), see [option files](https://dev.mysql.com/doc/refman/5.6/en/option-files.html) and [this illustration](https://stackoverflow.com/a/9293090) for *mysqldump*.

Basically you should add the following section to the relevant [configuration file](#Configuration_files):

```
[mysqldump]
user=mysqluser
password=secret
```

Mentioning a user here is optional, but doing so will free you from having to mention it on the command line. If you want to set this for all tools, including `mysql`, use the `[client]` group.

#### Example script

The database can be dumped to a file for easy backup. The following shell script will do this for you, creating a `db_backup.gz` file in the same directory as the script, containing your database dump:

```
#!/bin/bash

THISDIR=$(dirname $(readlink -f "$0"))

mysqldump --single-transaction --flush-logs --master-data=2 --all-databases \
 | gzip > $THISDIR/db_backup.gz
echo 'purge master logs before date_sub(now(), interval 7 day);' | mysql

```

See also the official `mysqldump` page in the [MySQL](http://dev.mysql.com/doc/refman/5.6/en/mysqldump.html) and [MariaDB](https://mariadb.com/kb/en/mariadb/documentation/clients-and-utilities/backup-restore-and-import/mysqldump) manuals.

### Holland Backup

A python-based software package named [Holland Backup](http://hollandbackup.org/) is available in [AUR](/index.php/AUR "AUR") to automate all of the backup work. It supports direct mysqldump, LVM snapshots to tar files (mysqllvm), LVM snapshots with mysqldump (mysqldump-lvm), and [xtrabackup](https://www.archlinux.org/packages/?name=xtrabackup) methods to extract the data. The Holland framework supports a multitude of options and is highly configurable to address almost any backup situation.

The main [holland](https://aur.archlinux.org/packages/holland/) and [holland-common](https://aur.archlinux.org/packages/holland-common/) packages provide the core framework; one of the sub-packages ([holland-mysqldump](https://aur.archlinux.org/packages/holland-mysqldump/), [holland-mysqllvm](https://aur.archlinux.org/packages/holland-mysqllvm/) and/or [holland-xtrabackup](https://aur.archlinux.org/packages/holland-xtrabackup/) must be installed for full operation. Example configurations for each method are in the `/usr/share/doc/holland/examples/` directory and can be copied to `/etc/holland/backupsets/`, as well as using the `holland mk-config` command to generate a base config for a named provider.

## Troubleshooting

### Unable to run mysql_upgrade because MySQL cannot start

Try run MySQL in safemode:

```
# mysqld_safe --datadir=/var/lib/mysql/

```

And then run:

```
# mysql_upgrade -u root -p

```

### Reset the root password

Stop `mariadb.service`. Issue the following command:

```
# mysqld_safe --skip-grant-tables &

```

Connect to the mysql server. Issue the following command:

```
# mysql -u root

```

Change root password:

```
mysql> use mysql;
mysql> FLUSH PRIVILEGES;
mysql> SET PASSWORD FOR 'root'@'localhost' = PASSWORD('MyNewPass');
mysql> exit

```

Then kill currently running mysql server:

```
# killall -9 mysqld

```

And finally start `mariadb.service`:

Start `mariadb.service`.

### Check and repair all tables

Check and auto repair all tables in all databases, [see more](http://dev.mysql.com/doc/refman/5.7/en/mysqlcheck.html):

```
# mysqlcheck -A --auto-repair -u root -p

```

### Optimize all tables

Forcefully optimize all tables, automatically fixing table errors that may come up.

```
# mysqlcheck -A --auto-repair -f -o -u root -p

```

### OS error 22 when running on ZFS

If using MySQL databases on [ZFS](/index.php/ZFS "ZFS"), the error **InnoDB: Operating system error number 22 in a file operation** may occur.

A workaround is to disable *aio_writes* in `/etc/mysql/my.cnf`:

 `/etc/mysql/my.cnf` 
```
[mysqld]
innodb_use_native_aio = 0
```

### Cannot login through CLI, but phpmyadmin works well

This may happen if you are using a long (>70-75) password. As for 5.5.36, for some reason, mysql CLI cannot handle that many characters in readline mode. So, if you are planning to use the recommended password input mode:

```
$ mysql -u <user> -p
Password:

```

Consider changing the password to smaller one.

**Note:** You still can log in by specifying the password as an argument to mysql command.
**Warning:** This behavior is considered dangerous, because your password might leak, for example, to the logs. Use it only in case of emergency and do not forget to change password right afterwards.

```
$ mysql -u <user> -p"<some-very-strong-password>"

```

### MySQL binary logs are taking up huge disk space

By default, mysqld creates binary log files in `/var/lib/mysql`. This is useful for replication master server or data recovery. But these binary logs can eat up your disk space. If you do not plan to use replication or data recovery features, you may disable binary logging by commenting out these lines in `/etc/mysql/my.cnf`:

```
#log-bin=mysql-bin
#binlog_format=mixed

```

Or you could limit the size of the logfile like this:

```
expire_logs_days = 10
max_binlog_size  = 100M

```

Alternatively, you can purge some binary logs in `/var/lib/mysql` to free up disk space with this command:

```
# mysql -u root -p"PASSWORD" -e "PURGE BINARY LOGS TO 'mysql-bin.0000xx';"

```

**Warning:** This may decrease the chances of successful data recovery when trying to repair database tables (i.e. on database corruption).

### OpenRC fails to start MySQL

To use MySQL with [OpenRC](/index.php/OpenRC "OpenRC") you need to add the following lines to the `[mysqld]` section in the MySQL config file, located at `/etc/mysql/my.cnf`.

```
user = mysql
basedir = /usr
datadir = /var/lib/mysql
pid-file = /run/mysqld/mysql.pid

```

You should now be able to start MySQL using:

```
# rc-service mysql start

```

### Specified key was too long

See [#Increase character limit](#Increase_character_limit).

### Changed limits warning on max_open_files/table_open_cache

Increase the number of file descriptors by creating a [systemd drop-in](/index.php/Systemd#Drop-in_files "Systemd"), e.g.:

 `/etc/systemd/system/mysqld.service.d/limit_nofile.conf` 
```
[Service]
LimitNOFILE=8192
```

## See also

*   [MariaDB Official Website](https://mariadb.com/)
*   [MariaDB knowledge Base](https://mariadb.com/kb/en/)
*   [MySQL Performance Tuning Scripts and Know-How](https://www.askapache.com/mysql/performance-tuning-mysql/)