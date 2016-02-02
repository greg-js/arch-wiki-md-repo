# MySQL

Related articles

*   [phpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin")
*   [Adminer](/index.php/Adminer "Adminer")

MySQL is a widely spread, multi-threaded, multi-user SQL database. For more information about features, see the [official homepage](http://www.mysql.com/).

**Note:** MariaDB is now officially Arch Linux's default implementation of MySQL. It is recommended for all users to [upgrade](#Upgrade_from_Oracle_MySQL_to_MariaDB) to MariaDB. Oracle MySQL was dropped to the [AUR](/index.php/AUR "AUR"). See [the announcement](https://www.archlinux.org/news/mariadb-replaces-mysql-in-repositories/).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Upgrade MariaDB](#Upgrade_MariaDB)
    *   [1.2 Upgrade from Oracle MySQL to MariaDB](#Upgrade_from_Oracle_MySQL_to_MariaDB)
*   [2 Configuration](#Configuration)
    *   [2.1 Add user](#Add_user)
    *   [2.2 Configuration files](#Configuration_files)
    *   [2.3 Grant remote access](#Grant_remote_access)
    *   [2.4 Disable remote access](#Disable_remote_access)
    *   [2.5 Enable auto-completion](#Enable_auto-completion)
    *   [2.6 Using UTF-8](#Using_UTF-8)
    *   [2.7 Using a TMPFS for tmpdir](#Using_a_TMPFS_for_tmpdir)
    *   [2.8 Time zone tables](#Time_zone_tables)
*   [3 Backup](#Backup)
    *   [3.1 Compression](#Compression)
    *   [3.2 Non-interactive](#Non-interactive)
        *   [3.2.1 Example script](#Example_script)
    *   [3.3 Holland Backup](#Holland_Backup)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 MySQL daemon cannot start](#MySQL_daemon_cannot_start)
    *   [4.2 Unable to run mysql_upgrade because MySQL cannot start](#Unable_to_run_mysql_upgrade_because_MySQL_cannot_start)
    *   [4.3 Reset the root password](#Reset_the_root_password)
    *   [4.4 Check and repair all tables](#Check_and_repair_all_tables)
    *   [4.5 Optimize all tables](#Optimize_all_tables)
    *   [4.6 OS error 22 when running on ZFS](#OS_error_22_when_running_on_ZFS)
    *   [4.7 Cannot login through CLI, but phpmyadmin works well](#Cannot_login_through_CLI.2C_but_phpmyadmin_works_well)
    *   [4.8 MySQL binary logs are taking up huge disk space](#MySQL_binary_logs_are_taking_up_huge_disk_space)
*   [5 See also](#See_also)

## Installation

[MariaDB](https://mariadb.org/) is the [default implementation](https://www.archlinux.org/news/mariadb-replaces-mysql-in-repositories/) of MySQL in Arch Linux, provided with the [mariadb](https://www.archlinux.org/packages/?name=mariadb) package.

Alternative implementations are:

*   **Oracle MySQL** — An implementation by Oracle Corporation.

	[https://www.mysql.com/](https://www.mysql.com/) || [mysql](https://aur.archlinux.org/packages/mysql/)<sup><small>AUR</small></sup>

*   **Percona Server** — An implementation by Percona LLC.

	[http://www.percona.com/software/percona-server/](http://www.percona.com/software/percona-server/) || [percona-server](https://www.archlinux.org/packages/?name=percona-server)

**Tip:**

*   If the database (in `/var/lib/mysql`) resides on a [Btrfs](/index.php/Btrfs "Btrfs") file system, you should consider disabling [Copy-on-Write](/index.php/Btrfs#Copy-On-Write_.28CoW.29 "Btrfs") for the directory before creating any database.
*   If the database resides on a [ZFS](/index.php/ZFS "ZFS") file system, you should consult [ZFS#Database](/index.php/ZFS#Database "ZFS") before creating any database.

Install [mariadb](https://www.archlinux.org/packages/?name=mariadb), afterwards run the following command **before starting** the `mysqld.service`:

```
# mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql

```

Now the `mysqld.service` can be started and/or enabled with [systemd](/index.php/Systemd#Using_units "Systemd").

It is recommended to secure the MySQL installation by running the following command:

```
# mysql_secure_installation

```

To simplify administration, you might want to install a front-end such as [mysql-workbench](https://www.archlinux.org/packages/?name=mysql-workbench) and/or [Adminer](/index.php/Adminer "Adminer").

### Upgrade MariaDB

You might consider running the following command after a (major) version upgrade (such as from 5.5 to 10.0, or from 10.0 to 10.1):

```
# mysql_upgrade -u root -p

```

### Upgrade from Oracle MySQL to MariaDB

**Note:** It could be necessary to remove the following files from `/var/lib/mysql` : `ib_logfile0`, `ib_logfile1` and `aria_log_control`, before restarting the daemon in the following procedure.

See [the announcement](https://www.archlinux.org/news/mariadb-replaces-mysql-in-repositories/) for the procedure to follow.

## Configuration

Once you have started the MySQL server and added a root account, you may want to change the default configuration.

To log in as `root` on the MySQL server, use the following command:

```
$ mysql -u root -p

```

### Add user

Creating a new user takes two steps: create the user; grant privileges. In the below example, the user _monty_ with _some_pass_ as password is being created, then granted full permissions to the database _mydb_:

 `$ mysql -u root -p` 

```
MariaDB> CREATE USER 'monty'@'localhost' IDENTIFIED BY 'some_pass';
MariaDB> GRANT ALL PRIVILEGES ON mydb.* TO 'monty'@'localhost';
MariaDB> FLUSH PRIVILEGES;
MariaDB> quit
```

### Configuration files

_MariaDB_ configuration options are read from the following files in the given order (according to `mysqld --help --verbose` output):

```
/etc/my.cnf /etc/mysql/my.cnf ~/.my.cnf

```

Depending on the scope of the changes you want to make (system-wide, user-only...), use the corresponding file. See [this entry](https://mariadb.com/kb/en/mariadb/documentation/getting-started/starting-and-stopping-mariadb/mysqld-configuration-files-and-groups/) of the KnowledgeBase for more information.

### Grant remote access

**Warning:** This is not considered as best practice and may cause security issues. Consider using [Secure Shell](/index.php/Secure_Shell "Secure Shell"), [VNC](/index.php/VNC "VNC") or [VPN](/index.php/Category:Virtual_Private_Network "Category:Virtual Private Network"), if you want to maintain the MySQL-server outside and/or inside your LAN.

If you want to access your MySQL server from other LAN hosts, you have to edit the following lines in `/etc/mysql/my.cnf`:

```
[mysqld]
   ...
   #skip-networking
   bind-address = <some ip-address>
   ...

```

Grant any MySQL user remote access (example for root):

```
$ mysql -u root -p

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

The MySQL server is accessible from the network by default. If MySQL is only needed for the localhost, you can improve security by not listening on TCP port 3306\. To refuse remote connections, uncomment the following line in `/etc/mysql/my.cnf`:

```
skip-networking

```

You will still be able to log in from the localhost.

### Enable auto-completion

**Note:** Enabling this feature can make the client initialization longer.

The MySQL client completion feature is disabled by default. To enable it system-wide edit `/etc/mysql/my.cnf`, and replace `no-auto-rehash` by `auto-rehash`. Completion will be enabled next time you run the MySQL client.

### Using UTF-8

In the `/etc/mysql/my.cnf` file section under the `mysqld` group, add:

```
[mysqld]
init_connect                = 'SET collation_connection = utf8_general_ci,NAMES utf8'
collation_server            = utf8_general_ci
character_set_client        = utf8
character_set_server        = utf8

```

### Using a TMPFS for tmpdir

The directory used by MySQL for storing temporary files is named _tmpdir_. For example, it is used to perform disk based large sorts, as well as for internal and explicit temporary tables.

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

## Backup

There are various [tools and strategies](https://mariadb.com/kb/en/mariadb/documentation/backing-up-and-restoring/) to back up your databases.

If you are using the default InnoDB storage engine, a [suggested](https://mariadb.com/kb/en/mariadb/documentation/clients-and-utilities/backup-restore-and-import/mysqldump/#examples) way of backing up all your bases online while provisioning for [point-in-time recovery](https://dev.mysql.com/doc/refman/5.6/en/password-security-user.html) (also known as “roll-forward,” when you need to restore an old backup and replay the changes that happened since that backup) is to execute the following command:

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
$ gunzip all_databases.sql.gz | mysql -u root -p

```

This will recreate and repopulate all the databases previously backed up (see [this](https://stackoverflow.com/questions/23180963/restore-all-mysql-database-from-a-all-database-sql-gz-file#comment35453351_23180977) or [this](http://www.linuxquestions.org/questions/linux-server-73/how-to-restore-mysqldump-all-databases-backup-892922/)).

### Non-interactive

If you want to setup non-interactive backup script for use in [cron](/index.php/Cron "Cron") jobs or [systemd timers](/index.php/Systemd/cron_functionality "Systemd/cron functionality"), see [option files](https://dev.mysql.com/doc/refman/5.6/en/option-files.html) and [this illustration](https://stackoverflow.com/a/9293090) for _mysqldump_.

Basically you should add the following section to the relevant [configuration file](#Configuration_files):

```
[mysqldump]
user=mysqluser
password=secret

```

Mentioning a user here is optional, but doing so will free you from having to mention it on the command line.

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

The main [holland](https://aur.archlinux.org/packages/holland/)<sup><small>AUR</small></sup> and [holland-common](https://aur.archlinux.org/packages/holland-common/)<sup><small>AUR</small></sup> packages provide the core framework; one of the sub-packages ([holland-mysqldump](https://aur.archlinux.org/packages/holland-mysqldump/)<sup><small>AUR</small></sup>, [holland-mysqllvm](https://aur.archlinux.org/packages/holland-mysqllvm/)<sup><small>AUR</small></sup> and/or [holland-xtrabackup](https://aur.archlinux.org/packages/holland-xtrabackup/)<sup><small>AUR</small></sup> must be installed for full operation. Example configurations for each method are in the `/usr/share/doc/holland/examples/` directory and can be copied to `/etc/holland/backupsets/`, as well as using the `holland mk-config` command to generate a base config for a named provider.

## Troubleshooting

### MySQL daemon cannot start

If MySQL fails to start and there is no entry in the log files, you might want to check the permissions of files in the directories `/var/lib/mysql` and `/var/lib/mysql/mysql`. If the owner of files in these directories is not `mysql:mysql`, you should do the following:

```
# chown mysql:mysql /var/lib/mysql -R

```

If you run into permission problems despite having followed the above, ensure that your `my.cnf` is copied to `/etc/`:

```
# cp /etc/mysql/my.cnf /etc/my.cnf

```

Now try and start the daemon.

If you get these messages in your `/var/lib/mysql/hostname.err`:

```
[ERROR] Can't start server : Bind on unix socket: Permission denied
[ERROR] Do you already have another mysqld server running on socket: /var/run/mysqld/mysqld.sock ?
[ERROR] Aborting

```

the permissions of `/var/run/mysqld` could be the culprit.

```
# chown mysql:mysql /var/run/mysqld -R

```

If you run mysqld and the following error appears:

```
Fatal error: Can’t open and lock privilege tables: Table ‘mysql.host’ doesn’t exist

```

Run the following command from the `/usr` directory to install the default tables:

```
# cd /usr
# mysql_install_db --user=mysql --ldata=/var/lib/mysql/

```

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

Stop `mysqld.service`. Issue the following command:

```
# mysqld_safe --skip-grant-tables &

```

Connect to the mysql server. Issue the following command:

```
# mysql -u root mysql

```

Change root password:

```
mysql> use mysql;
mysql> UPDATE mysql.user SET Password=PASSWORD('MyNewPass') WHERE User='root';
mysql> FLUSH PRIVILEGES;
mysql> exit

```

Start `mysqld.service`.

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

If you are using [ZFS](/index.php/ZFS "ZFS") and get the following error:

```
InnoDB: Operating system error number 22 in a file operation.

```

You need to disable aio_writes by adding a line to the mysqld-section in /etc/mysql/my.cnf

```
[mysqld]
...
innodb_use_native_aio = 0

```

However, if the post install scripts failed because of the above issue, MySQL/MariaDB might be in an invalid state. To recover from this state, execute the following:

```
rm -rf /var/lib/mysql/*
mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
chown -R mysql:mysql /var/lib/mysql &>/dev/null
/usr/bin/systemd-tmpfiles --create mysql.conf

```

After which MySQL/MariaDB should be installed correctly.

### Cannot login through CLI, but phpmyadmin works well

This may happen if you are using a long (>70-75) password. As for 5.5.36, for some reason, mysql CLI cannot handle that much characters in readline mode. So, if you are planning to use the recommended password input mode:

```
$ mysql -u <user> -p
Password:

```

consider changing the password to smaller one.

**Note:** You still can log in by specifying the password as an argument to mysql command.

**Warning:** This behavior is considered dangerous, because your password might leak, for example, to the logs. Use it only in case of emergency and do not forget to change password right afterwards.

```
$ mysql -u <user> -p"<some-veryveryveryveryveryveryveryveryveryveryveryveryveryveryvery-long-and-veryveryveryveryveryveryveryveryveryvery-strong-password>"

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

## See also

*   [MariaDB Official Website](https://mariadb.org/)
*   [MariaDB knowledge Base](https://mariadb.com/kb/en/)
*   [MySQL documentation](http://dev.mysql.com/doc/)
*   [LAMP](/index.php/LAMP "LAMP") - ArchWiki article covering the setup of a LAMP server (Linux Apache MySQL PHP)
*   [PhpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin") - ArchWiki article covering the web-based tool to help manage MySQL databases using an Apache/PHP front-end.
*   [PHP](/index.php/PHP "PHP") - ArchWiki article on PHP.
*   [MySQL Performance Tuning Scripts and Know-How](http://www.askapache.com/mysql/performance-tuning-mysql.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=MySQL&oldid=415037](https://wiki.archlinux.org/index.php?title=MySQL&oldid=415037)"