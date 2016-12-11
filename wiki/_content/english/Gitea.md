[Gitea](https://gitea.io/) is a community managed fork of [Gogs](/index.php/Gogs "Gogs"), lightweight code hosting solution written in Go and published under the MIT license.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 MariaDB](#MariaDB)
*   [2 Running](#Running)
*   [3 Configuration](#Configuration)
    *   [3.1 Disable HTTP protocol](#Disable_HTTP_protocol)
*   [4 Advanced Configuration](#Advanced_Configuration)
    *   [4.1 Configure nginx as reverse proxy](#Configure_nginx_as_reverse_proxy)
*   [5 See also](#See_also)

## Installation

**Note:** At the time of writing, there are no official upgrade release yet. Developers are working on 1.0.0 that should allow seamless upgrades of existing Gogs deploys.

Install the [gitea-git](https://aur.archlinux.org/packages/gitea-git/) package.

Gitea requires the use of a database backend, the following are supported:

*   [MariaDB](/index.php/MariaDB "MariaDB")
*   [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")
*   [SQLite](/index.php/SQLite "SQLite")
*   [TiDB](https://github.com/pingcap/tidb)

### MariaDB

**Note:** MySQL socket support can be enabled by using `/var/run/mysqld/mysqld.sock` as the listen address.

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

Configure MariaDB on first run or by updating `app.ini`:

 `/var/lib/gitea/custom/conf/app.ini` 
```
DB_TYPE  = mysql
HOST     = /var/run/mysqld/mysqld.sock ; or 127.0.0.1:3306
NAME     = gitea
USER     = gitea
PASSWD   = **password**
```

## Running

[Start/enable](/index.php/Start/enable "Start/enable") `gitea.service`, the webinterface should listen on `[http://localhost:3000](http://localhost:3000)`.

When running Gitea for the first time it should redirect to `[http://localhost:3000/install](http://localhost:3000/install)`.

## Configuration

The user configuration file is located at `/var/lib/gitea/custom/conf/app.ini`. Do **not** edit the main configuration file at `/var/lib/gitea/conf/app.ini`, since this file is included in the binary and will be overwritten on each update.

Gitea application and repository data will be saved into */var/lib/gitea*, however it is possible to set custom locations in `/var/lib/gitea/custom/conf/app.ini`.

### Disable HTTP protocol

By default, the ability to interact with repositories by HTTP protocol is enabled. You may want to disable support by setting `DISABLE_HTTP_GIT` to **false**.

## Advanced Configuration

See the [Gogs FAQ's](https://gogs.io/docs/intro/faqs) for more configuration examples.

### Configure nginx as reverse proxy

An example of using [nginx](/index.php/Nginx "Nginx") as reverse proxy including [OpenSSL](/index.php/OpenSSL "OpenSSL"):

 `/etc/nginx/servers-available/git` 
```
# redirect to ssl
server {
  listen 80;
  server_name git.domain.tld;
  return 301 [https://$server_name$request_uri](https://$server_name$request_uri);
}

server {
  listen 443 ssl http2;
  server_name git.domain.tld;
  ssl_certificate ssl/**cert.crt**;
  ssl_certificate_key ssl/**cert.key**;

  location / {
    proxy_set_header X-Real-IP $remote_addr;
    proxy_pass [http://localhost:3000](http://localhost:3000);
  }
}
```

Update the *server* section of `app.ini`:

 `/var/lib/gitea/custom/conf/app.ini` 
```
[server]
PROTOCOL               = http
DOMAIN                 = git.domain.tld
ROOT_URL               = [https://git.domain.tld/](https://git.domain.tld/)
HTTP_ADDR              = 0.0.0.0
HTTP_PORT              = 3000
```

**Note:** You don't need to activate any SSL certificate options in `app.ini`.

## See also

*   [Gitea Documentation](https://docs.gitea.io/)
*   [Gogs Documentation](https://gogs.io/docs)