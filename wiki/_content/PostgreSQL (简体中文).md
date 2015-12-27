# PostgreSQL (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**本页面或部分需要翻译，部分内容可能已经与英文文章脱节。如果您希望贡献翻译，请访问[简体中文翻译组](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")。**

**附注:** please use the first argument of the template to provide more detailed indications.

PostgreSQL是一个开源的，社区驱动的，符合标准的 对象-关系型 数据库系统。

本文档介绍如何安装PostgreSql。同时，也介绍了如何配置PostgreSql，使远程客户端能够操作之。在某些应用中，PostgreSQL可以代替MySQL作为LAMP网络栈的一部分。

## Contents

*   [1 安装PostgreSQL](#.E5.AE.89.E8.A3.85PostgreSQL)
*   [2 创建第一个数据库/用户](#.E5.88.9B.E5.BB.BA.E7.AC.AC.E4.B8.80.E4.B8.AA.E6.95.B0.E6.8D.AE.E5.BA.93.2F.E7.94.A8.E6.88.B7)
*   [3 熟悉PostgreSQL](#.E7.86.9F.E6.82.89PostgreSQL)
    *   [3.1 Access the database shell](#Access_the_database_shell)
*   [4 配置 PostgreSQL 被远程访问](#.E9.85.8D.E7.BD.AE_PostgreSQL_.E8.A2.AB.E8.BF.9C.E7.A8.8B.E8.AE.BF.E9.97.AE)
*   [5 Configure PostgreSQL to work with PHP](#Configure_PostgreSQL_to_work_with_PHP)
*   [6 Change default data dir (optional)](#Change_default_data_dir_.28optional.29)
*   [7 Change default encoding of new databases to UTF-8 (optional)](#Change_default_encoding_of_new_databases_to_UTF-8_.28optional.29)
*   [8 管理工具](#.E7.AE.A1.E7.90.86.E5.B7.A5.E5.85.B7)
*   [9 Postgresql升级配置](#Postgresql.E5.8D.87.E7.BA.A7.E9.85.8D.E7.BD.AE)
    *   [9.1 快速指南](#.E5.BF.AB.E9.80.9F.E6.8C.87.E5.8D.97)
    *   [9.2 详细说明](#.E8.AF.A6.E7.BB.86.E8.AF.B4.E6.98.8E)
*   [10 Troubleshooting](#Troubleshooting)
    *   [10.1 Improve performance of small transactions](#Improve_performance_of_small_transactions)
    *   [10.2 空闲时防止磁盘写入](#.E7.A9.BA.E9.97.B2.E6.97.B6.E9.98.B2.E6.AD.A2.E7.A3.81.E7.9B.98.E5.86.99.E5.85.A5)
*   [11 See also](#See_also)

## 安装PostgreSQL

[安装](/index.php/Pacman "Pacman") [postgresql](https://www.archlinux.org/packages/?name=postgresql)，并为新用户_postgres_[设置一个密码](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.85.B6.E5.AE.83.E7.94.A8.E6.88.B7.E7.AE.A1.E7.90.86.E7.A4.BA.E4.BE.8B "Users and groups (简体中文)") 。

在PostgreSQL可以正确使用之前，数据库集群必须被初始化:

```
# sudo su - postgres -c "initdb --locale en_US.UTF-8 -E UTF8 -D '/var/lib/postgres/data'"

```

启动PostgreSQL，(可选)，添加 PostgreSQL 到daemons列表里作为守护进程同时启动：

```
# systemctl start postgresql
# systemctl enable postgresql

```

**警告:** 如果数据库位于[Btrfs](/index.php/Btrfs "Btrfs")文件系统上，你应该在创建数据库前禁用数据库目录的[Copy-on-Write](/index.php/Btrfs_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.86.99.E6.97.B6.E5.A4.8D.E5.88.B6_.EF.BC.88Copy-On-Write_.28CoW.29.EF.BC.89 "Btrfs (简体中文)")。

## 创建第一个数据库/用户

以postgres用户身份, 添加一个新的数据库用户使用[createuser](http://www.postgresql.org/docs/9.0/static/app-createuser.html) 命令

如果一个创建与你的Arch用户($USER)同名的数据库用户，并允许访问PostgreSQL数据库的shell，那么在使用PostgreSQL数据库shell的时候无需指定用户登录（这样做会比较方便）。

例如:创建一个超级用户

 `$ createuser -s -U postgres --interactive`  `输入要增加的角色名称: 我登录Arch的用户名` 

以具备读写权限的用户身份，创建一个新的数据库,使用[createdb](http://www.postgresql.org/docs/9.0/static/app-createdb.html) 命令。

从你的shell (**不是** 以postrgres用户的身份)

```
$ createdb myDatabaseName

```

## 熟悉PostgreSQL

### Access the database shell

Become the postgres user. Start the primary db shell, [psql](http://www.postgresql.org/docs/8.3/static/app-psql.html), where you can do all your creation of databases/tables, deletion, set permissions, and run raw SQL commands. Use the "-d" option to connect to the database you created (without specifying a database, psql will try to access a database that matches your username)

```
$ psql -d myDatabaseName

```

一些有用的命令：

*   帮助

```
=> \help

```

*   连接到数据库<database>

```
=> \c <database>

```

*   列出所有用户以及他们的权限

```
=> \du

```

*   展示当前数据库中所有的表相关的汇总信息

```
=> \dt

```

*   退出psql

```
=> \q or CTRL+d

```

当然也有更多元命令，但这些应该能够帮助您开始。

## 配置 PostgreSQL 被远程访问

PostgreSQL Server 的配置文件是 `postgresql.conf`。此文件在数据库数据目录中，通常在 `/var/lib/postgres/data`. 这个目录也包含其他主要的配置文件，包括 `pg_hba.conf`。

**Note:** 默认这个目录不能被普通用户浏览或进入，这就是 `find` 或 `locate` 没有找到这些配置文件的原因。

As root user edit the file `/var/lib/postgres/data/postgresql.conf`. In the connections and authentications section uncomment or edit the `listen_addresses` line to your needs:

```
listen_addresses = '*'

```

Take a careful look at the other lines. Hereafter insert the following line in the host-based authentication file `/var/lib/postgres/data/pg_hba.conf`. This file controls which hosts are allowed to connect, so **be careful**.

```
# IPv4 local connections:
host   all   all   your_desired_ip_address/32   trust

```

where `your_desired_ip_address` is the IP address of the client. After this you should restart the daemon process for the changes to take effect with:

```
# systemctl restart postgresql

```

**Note:** Postgresql uses port 5432 by default for remote connections. So make sure this port is open and able to receive incoming connections.

For troubleshooting take a look in the server log file

```
tail /var/log/postgresql.log

```

## Configure PostgreSQL to work with PHP

Install the PHP-PostgreSQL modules [php-pgsql](https://www.archlinux.org/packages/?name=php-pgsql). Edit the file `/etc/php/php.ini`. Find the line that starts with:

```
;extension=pgsql.so

```

Change it to:

```
extension=pgsql.so

```

If you need PDO, do the same thing with `;extension=pdo.so` and `;extension=pdo_pgsql.so`. If these lines are not present, add them. These lines may be in the "Dynamic Extensions" section of the file, or toward the very end of the file. Restart the Apache web server:

1.  systemctl restart httpd

## Change default data dir (optional)

The default directory where all your newly created databases will be stored is `/var/lib/postgres/data`. To change this, follow these steps:

Create the new directory and assign it to user `postgres` (you eventually have to become root):

```
mkdir -p /pathto/pgroot/data
chown -R postgres:postgres /pathto/pgroot

```

Become the postgres user(change to root, then postgres user), and initialize the new cluster:

```
initdb -D /pathto/pgroot/data

```

If not using systemd, edit `/etc/conf.d/postgresql` and change the PGROOT variable(optionally PGLOG) to point to your new pgroot directory:

```
#PGROOT="/var/lib/postgres/"
PGROOT="_/pathto/pgroot/_"

```

If using systemd, edit `/etc/systemd/system/multi-user.target.wants/postgresql.service`, which links to `/usr/lib/systemd/system/postgresql.service`, and change the default PGROOT path.

```
#Environment=PGROOT=/var/lib/postgres/
Environment=PGROOT=_/pathto/pgroot/_

```

You will also need to change the default PIDFile path.

```
PIDFile=/pathto/pgroot/data/postmaster.pid

```

## Change default encoding of new databases to UTF-8 (optional)

**Note:** If you ran initdb with -E UTF8 these steps are not required

When creating a new database (e.g. with `createdb blog`) PostgreSQL actually copies a template database. There are two predefined templates: template0 is vanilla, while template1 is meant as an on-site template changeable by the administrator and is used by default. In order to change the encoding of new database, one of the options is to change on-site template1\. To do this, log into PostgresSQL shell (psql) and execute the following:

First, we need to drop template1\. Templates cannot be dropped, so we first modify it so it is an ordinary database:

```
UPDATE pg_database SET datistemplate = FALSE WHERE datname = 'template1';

```

Now we can drop it:

```
DROP DATABASE template1;

```

The next step is to create a new database from template0, with a new default encoding:

```
CREATE DATABASE template1 WITH TEMPLATE = template0 ENCODING = 'UNICODE';

```

Now modify template1 so it is actually a template:

```
UPDATE pg_database SET datistemplate = TRUE WHERE datname = 'template1';

```

(OPTIONAL) If you do not want anyone connecting to this template, set datallowconn to FALSE:

```
UPDATE pg_database SET datallowconn = FALSE WHERE datname = 'template1';

```

**Note:** this last step can create problems when upgrading via `pg_upgrade`.

Now you can create a new database by running from regular shell:

```
su -
su - postgres
createdb blog;

```

If you log in back to psql and check the databases, you should see the proper encoding of your new database:

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

## 管理工具

*   **[phpPgAdmin](/index.php/PhpPgAdmin "PhpPgAdmin")** — Web-based administration tool for PostgreSQL.

[http://phppgadmin.sourceforge.net](http://phppgadmin.sourceforge.net) || [phppgadmin](https://www.archlinux.org/packages/?name=phppgadmin)

*   **pgAdmin** — GUI-based administration tool for PostgreSQL.

[http://www.pgadmin.org/](http://www.pgadmin.org/) || [pgadmin3](https://www.archlinux.org/packages/?name=pgadmin3)

## Postgresql升级配置

### 快速指南

This is for upgrading from 9.2 to 9.3.

```
 pacman -S --needed postgresql-old-upgrade
 su -
 su - postgres -c 'mv /var/lib/postgres/data /var/lib/postgres/data-9.2'
 su - postgres -c 'mkdir /var/lib/postgres/data'
 su - postgres -c 'initdb --locale en_US.UTF-8 -E UTF8 -D /var/lib/postgres/data'

```

If you had custom settings in configuration files like pg_hba.conf and postgresql.conf, merge them into the new ones. Then:

```
 su - postgres -c 'pg_upgrade -b /opt/pgsql-9.2/bin/ -B /usr/bin/ -d /var/lib/postgres/data-9.2 -D /var/lib/postgres/data'

```

If the "pg_upgrade" step fails with:

*   _cannot write to log file pg_upgrade_internal.log  
    Failure, exiting_  
    Make sure you're in a directory that the "postgres" user has enough rights to write the log file to (`/tmp` for example). Or use "su - postgres" instead of "sudo -u postgres".
*   _LC_COLLATE error that says that old and new values are different_  
    Figure out what the old locale was, C or en_US.UTF-8 for example, and force it when calling initdb.

```
 sudo -u postgres LC_ALL=C initdb -D /var/lib/postgres/data

```

*   _There seems to be a postmaster servicing the old cluster.  
    Please shutdown that postmaster and try again._  
    Make sure postgres isn't running. If you still get the error then chances are these an old PID file you need to clear out.

```
 > sudo -u postgres ls -l /var/lib/postgres/data-9.2
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

 > sudo -u postgres mv /var/lib/postgres/data-9.2/postmaster.pid /tmp

```

*   _ERROR: could not access file "$libdir/postgis-2.0": No such file or directory_  
    Retrieve postgis-2.0.so from postgis package for version postgresql 9.2 () and copy it to /opt/pgsql-9.2/lib (make sure the privileges are right)

### 详细说明

**Note:** Official PostgreSQL [upgrade documentation](http://www.postgresql.org/docs/current/static/upgrading.html) should be followed.

需要注意的是，这些指令可能会导致数据丢失。 **后果自负**.

推荐把下面的加入你的 `/etc/pacman.conf` 文件中:

```
IgnorePkg = postgresql postgresql-libs

```

这将确保你不会不小心将数据库升级到不兼容的版本中。当一个升级可用时，pacman将通知你，因为在pacman.conf中的设置，它跳过了升级。小版本升级 (e.g., 9.0.3 to 9.0.4) 可以被安全地执行。不过，当如果你突然做一个不同的主版本升级时，(e.g., 9.0.X to 9.1.X), 您可能无法访问你的任何数据。请务必检查PostgreSQL的主页 ([http://www.postgresql.org/](http://www.postgresql.org/)) ，以确认每次升级所需要的步骤。对于为什么是这种情况见 [versioning policy](http://www.postgresql.org/support/versioning)。

主要有两种方式来升级您的PostgreSQL数据库。阅读官方文档细节。

For those wishing to use `pg_upgrade`, a [postgresql-old-upgrade](https://www.archlinux.org/packages/?name=postgresql-old-upgrade) package is available in the repositories that will always run one major version behind the real PostgreSQL package. This can be installed side by side with the new version of PostgreSQL. When you are ready to perform the upgrade, you can do

```
pacman -Syu postgresql postgresql-libs postgresql-old-upgrade

```

Note also that the data directory does not change from version to version, so before running pg_upgrade it is necessary to rename your existing data directory and migrate into a new directory. The new database must be initialized by starting the server, as described near the top of this page. The server then needs to be stopped before running pg_upgrade.

```
# systemctl stop postgresql
# su - postgres -c 'mv /var/lib/postgres/data /var/lib/postgres/olddata'
# systemctl start postgresql
# systemctl stop postgresql

```

Reference the [upstream pg_upgrade documentation](http://www.postgresql.org/docs/current/static/pgupgrade.html) for details.

The upgrade invocation will likely look something like the following (run as the postgres user). **Do not run this command blindly without understanding what it does!**

```
# su - postgres -c 'pg_upgrade -d /var/lib/postgres/olddata/ -D /var/lib/postgres/data/ -b /opt/pgsql-8.4/bin/ -B /usr/bin/'

```

You could also do something like this (after the upgrade and install of postgresql-old-upgrade) (NB: these instructions DON'T seem to work for 9.2 -> 9.3 upgrades)

```
# systemctl stop postgresql
# /opt/pgsql-8.4/bin/pg_ctl -D /var/lib/postgres/olddata/ start
# pg_dumpall >> old_backup.sql
# /opt/pgsql-8.4/bin/pg_ctl -D /var/lib/postgres/olddata/ stop
# systemctl start postgresql
# psql -f old_backup.sql postgres

```

## Troubleshooting

### Improve performance of small transactions

If you are using PostgresSQL on a local machine for development and it seems slow, you could try turning [synchronous_commit off](http://www.postgresql.org/docs/current/static/runtime-config-wal.html#GUC-SYNCHRONOUS-COMMIT) in the configuration (`/var/lib/postgres/data/postgresql.conf`). Beware of the [caveats](http://www.postgresql.org/docs/current/static/runtime-config-wal.html#GUC-SYNCHRONOUS-COMMIT), however.

```
synchronous_commit = off

```

### 空闲时防止磁盘写入

PostgreSQL periodically updates its internal "statistics" file. By default, this file is stored on disk, which prevents disks spinning down on laptops and causes hard drive seek noise. It's simple and safe to relocate this file to a memory-only file system with the following configuration option:

```
stats_temp_directory = '/run/postgresql'

```

## See also

*   [Official PostgreSQL Homepage](http://www.postgresql.org/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PostgreSQL_(简体中文)&oldid=413551](https://wiki.archlinux.org/index.php?title=PostgreSQL_(简体中文)&oldid=413551)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [简体中文](/index.php/Category:%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87 "Category:简体中文")
*   [Networking (简体中文)](/index.php/Category:Networking_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Networking (简体中文)")
*   [Database management systems (简体中文)](/index.php/Category:Database_management_systems_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Database management systems (简体中文)")