[Gitea](https://gitea.io/) is a community managed fork of [Gogs](/index.php/Gogs "Gogs"), lightweight code hosting solution written in Go and published under the MIT license.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 MariaDB](#MariaDB)
*   [2 Running](#Running)
*   [3 Configuration](#Configuration)

## Installation

**Note:** At the time of writing, there are no official Gitea release yet. Developers are working on 1.0.0 that should allow seamless upgrades of existing Gogs deploys.

Install the [gitea-git](https://aur.archlinux.org/packages/gitea-git/) package.

Gitea requires the use of a database backend, the following are supported:

*   [MariaDB](/index.php/MariaDB "MariaDB")
*   [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")

The following database backends are consider experimental [[1]](https://gogs.io/docs/installation/install_from_source.html#build-with-tags), thus not included in [gitea-git](https://aur.archlinux.org/packages/gitea-git/):

*   [SQLite](/index.php/SQLite "SQLite")
*   [TiDB](https://github.com/pingcap/tidb)

### MariaDB

The following is an example of setting up [MariaDB](/index.php/MariaDB "MariaDB"):

 `$ mysql -u root -p` 
```
mysql> CREATE DATABASE `gitea` DEFAULT CHARACTER SET `utf8` COLLATE `utf8_unicode_ci`;
mysql> CREATE USER **gitea**@'localhost' IDENTIFIED BY '**password'**;
mysql> GRANT ALL ON `gitea`.* TO 'gitea'@'localhost';
mysql> \q
```

Try connecting to the new database with the new user:

```
$ mysql -u **gitea** -p -D gitea

```

It is possible to install Gitea using a MySQL socket by using `/var/run/mysqld/mysqld.sock` as the listen address.

## Running

[Start/enable](/index.php/Start/enable "Start/enable") `gitea.service`, the webinterface should listen on `[http://localhost:3000](http://localhost:3000)`.

When running Gitea for the first time it should redirect to `[http://localhost:3000/install](http://localhost:3000/install)`.

## Configuration

The configuration file is located at `/var/lib/gitea/custom/conf/app.ini`. Do **not** edit the main configuration file at `conf/app.ini`, since this file is included in the binary and will be overwritten on each update.