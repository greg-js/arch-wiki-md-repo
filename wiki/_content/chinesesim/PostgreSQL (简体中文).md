PostgreSQL是一个开源的，社区驱动的，符合标准的 对象-关系型 数据库系统。

本文档介绍如何安装PostgreSql。同时，也介绍了如何配置PostgreSql，使远程客户端能够操作之。在某些应用中，PostgreSQL可以代替MySQL作为LAMP网络栈的一部分。

## Contents

*   [1 安装PostgreSQL](#.E5.AE.89.E8.A3.85PostgreSQL)
*   [2 创建第一个数据库/用户](#.E5.88.9B.E5.BB.BA.E7.AC.AC.E4.B8.80.E4.B8.AA.E6.95.B0.E6.8D.AE.E5.BA.93.2F.E7.94.A8.E6.88.B7)
*   [3 熟悉PostgreSQL](#.E7.86.9F.E6.82.89PostgreSQL)
    *   [3.1 连接数据库shell](#.E8.BF.9E.E6.8E.A5.E6.95.B0.E6.8D.AE.E5.BA.93shell)
*   [4 选择配置](#.E9.80.89.E6.8B.A9.E9.85.8D.E7.BD.AE)
    *   [4.1 配置 PostgreSQL 被远程访问](#.E9.85.8D.E7.BD.AE_PostgreSQL_.E8.A2.AB.E8.BF.9C.E7.A8.8B.E8.AE.BF.E9.97.AE)
    *   [4.2 Configure PostgreSQL to work with PHP](#Configure_PostgreSQL_to_work_with_PHP)
    *   [4.3 Change default data dir (optional)](#Change_default_data_dir_.28optional.29)
    *   [4.4 Change default encoding of new databases to UTF-8](#Change_default_encoding_of_new_databases_to_UTF-8)
*   [5 管理工具](#.E7.AE.A1.E7.90.86.E5.B7.A5.E5.85.B7)
*   [6 Postgresql升级配置](#Postgresql.E5.8D.87.E7.BA.A7.E9.85.8D.E7.BD.AE)
    *   [6.1 快速指南](#.E5.BF.AB.E9.80.9F.E6.8C.87.E5.8D.97)
    *   [6.2 详细说明](#.E8.AF.A6.E7.BB.86.E8.AF.B4.E6.98.8E)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Improve performance of small transactions](#Improve_performance_of_small_transactions)
    *   [7.2 空闲时防止磁盘写入](#.E7.A9.BA.E9.97.B2.E6.97.B6.E9.98.B2.E6.AD.A2.E7.A3.81.E7.9B.98.E5.86.99.E5.85.A5)
*   [8 See also](#See_also)

## 安装PostgreSQL

[安装](/index.php/Pacman "Pacman") [postgresql](https://www.archlinux.org/packages/?name=postgresql)，并为新用户*postgres*[设置一个密码](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.85.B6.E5.AE.83.E7.94.A8.E6.88.B7.E7.AE.A1.E7.90.86.E7.A4.BA.E4.BE.8B "Users and groups (简体中文)") 。

**注意:** 在本篇文章中需要以postgres用户运行的命令以`[postgres]$`作为前置符号。你可以以root用户执行`su - postgres`登陆postgres用户。如果你使用[sudo](/index.php/Sudo "Sudo")，可以以普通用户执行`sudo -i -u postgres`。

在PostgreSQL可以正确使用之前，数据库集群必须被初始化:

```
# sudo su - postgres -c "initdb --locale en_US.UTF-8 -E UTF8 -D '/var/lib/postgres/data'"

```

启动PostgreSQL，(可选)，添加 PostgreSQL 到daemons列表里作为守护进程同时启动：

```
# systemctl start postgresql.service
# systemctl enable postgresql.service

```

**警告:** 如果数据库位于[Btrfs](/index.php/Btrfs "Btrfs")文件系统上，你应该在创建数据库前禁用数据库目录的[Copy-on-Write](/index.php/Btrfs_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.86.99.E6.97.B6.E5.A4.8D.E5.88.B6_.EF.BC.88Copy-On-Write_.28CoW.29.EF.BC.89 "Btrfs (简体中文)")。

## 创建第一个数据库/用户

**提示:** 如果创建一个与你的 Arch 用户 ($USER) 同名的数据库用户，并允许其访问 PostgreSQL 数据库的 shell，那么在使用PostgreSQL 数据库 shell 的时候无需指定用户登录（这样做会比较方便）。

以 postgres 用户身份, 添加一个新的数据库用户使用 [createuser](http://www.postgresql.org/docs/9.0/static/app-createuser.html) 命令

 `[postgres]$ createuser --interactive`  `输入要增加的角色名称: 我登录 Arch 的用户名` 

以具备读写权限的用户身份，创建一个新的数据库,使用[createdb](http://www.postgresql.org/docs/9.0/static/app-createdb.html) 命令。

从你的 shell (**不是** 以 postrgres 用户的身份)

```
$ createdb myDatabaseName

```

## 熟悉PostgreSQL

### 连接数据库shell

登陆为postgres用户，启动主要数据库shell [psql](http://www.postgresql.org/docs/current/static/app-psql.html)，你可以创建数据库或表、设计权限和运行原始的SQL命令。使用`-d`选项连接你创建的数据库（如果没有指定数据库，`psql`会尝试连接与你用户名同名的数据库）。

```
[postgres]$ psql -d myDatabaseName

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

## 选择配置

#### 配置 PostgreSQL 被远程访问

PostgreSQL Server 的配置文件是 `postgresql.conf`。此文件在数据库数据目录中，通常在 `/var/lib/postgres/data`。这个目录也包含其他主要的配置文件，包括 `pg_hba.conf`。

**注意:** 默认情况下这个目录不能被普通用户访问，这就是 `find` 或 `locate` 没有找到这些配置文件的原因。

编辑文件`/var/lib/postgres/data/postgresql.conf`。在*connections and authentications*选项中，按照你的需要添加`listen_addresses`行:

```
listen_addresses = 'localhost,my_remote_server_ip_address'

```

仔细检查其他行。

`/var/lib/postgres/data/pg_hba.conf`配置基于主机的认证。这个文件控制哪些主机允许连接。要注意默认情况下**允许所有本地用户连接任何数据库用户**，包括数据库的超级用户。根据下面的描述添加一行:

```
# IPv4 local connections:
host   all   all   *my_remote_client_ip_address*/32   md5

```

`my_remote_client_ip_address`是客户端的IP地址。

如需更多帮助请查看[pg_hba.conf](http://www.postgresql.org/docs/current/static/auth-pg-hba-conf.html)的文档。

在完成编辑后你需要[重启](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)") `postgresql.service`服务使你的配置生效。

**注意:** PostgreSQL默认使用`5432`端口作为远程连接。确保打开这个端口并可以接受入口连接

如果遇到麻烦，使用下面的命令查看服务器日志:

```
$ journalctl -u postgresql

```

#### Configure PostgreSQL to work with PHP

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

#### Change default data dir (optional)

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
PGROOT="*/pathto/pgroot/*"

```

If using systemd, edit `/etc/systemd/system/multi-user.target.wants/postgresql.service`, which links to `/usr/lib/systemd/system/postgresql.service`, and change the default PGROOT path.

```
#Environment=PGROOT=/var/lib/postgres/
Environment=PGROOT=*/pathto/pgroot/*

```

You will also need to change the default PIDFile path.

```
PIDFile=/pathto/pgroot/data/postmaster.pid

```

#### Change default encoding of new databases to UTF-8

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

*   *cannot write to log file pg_upgrade_internal.log
    Failure, exiting*
    Make sure you're in a directory that the "postgres" user has enough rights to write the log file to (`/tmp` for example). Or use "su - postgres" instead of "sudo -u postgres".
*   *LC_COLLATE error that says that old and new values are different*
    Figure out what the old locale was, C or en_US.UTF-8 for example, and force it when calling initdb.

```
 sudo -u postgres LC_ALL=C initdb -D /var/lib/postgres/data

```

*   *There seems to be a postmaster servicing the old cluster.
    Please shutdown that postmaster and try again.*
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

*   *ERROR: could not access file "$libdir/postgis-2.0": No such file or directory*
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