Tiny Tiny RSS is an open source web-based news feed (RSS/Atom) aggregator, designed to allow you to read news from any location, while feeling as close to a real desktop application as possible.

## Installation

Install [tt-rss](https://www.archlinux.org/packages/?name=tt-rss) from the [official repositories](/index.php/Official_repositories "Official repositories").

tt-rss is installed into `/usr/share/webapps/tt-rss/`; you'll need to make this directory available from your web server. The simplest way is to do

```
# ln -s /usr/share/webapps/tt-rss /srv/http/tt-rss 

```

### Set up php and database

You'll need to set up a database, either [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"). Create a user and database, e.g. with mysql:

```
$ mysql -p -u root
mysql> CREATE USER 'ttrss'@'localhost' IDENTIFIED BY 'somepassword';
mysql> CREATE DATABASE ttrss;
mysql> GRANT ALL PRIVILEGES ON ttrss.* TO "ttrss"@"localhost" IDENTIFIED BY 'somepassword';

```

You also need to add some paths to /etc/php/php.ini:

```
...
open_basedir = ... :/usr/share/webapps/:/etc/webapps/:/var/lib/tt-rss
...

```

In the same file, enable the following modules:

```
extension=curl.so
extension=iconv.so
extension=mysqli.so # extension=pdo_mysql.so might be an alternative
extension=soap.so

```

Application initialization can done either automatically or manually.

Automatic way:

*   remove default config file `/etc/webapps/tt-rss/config.php`, without this file tt-rss webapp enters installation wizard.
*   navigate to (your-servers-root)/tt-rss/ and proceed with the installer.
*   save generated config file to `/etc/webapps/tt-rss/config.php`.

Manual way:

*   edit tt-rss config file`/etc/webapps/tt-rss/config.php` and update database settings.
*   re-create database from `/usr/share/webapps/tt-rss/schema/ttrss_schema_TYPE.sql`. With MySQL run:

```
$ mysql --user ttrss --password=<PASSWORD> ttrss < /usr/share/webapps/tt-rss/schema/ttrss_schema_mysql.sql

```

### Set up an update daemon

See [https://tt-rss.org/gitlab/fox/tt-rss/wikis/UpdatingFeeds](https://tt-rss.org/gitlab/fox/tt-rss/wikis/UpdatingFeeds) – but you should be able to simply

```
# systemctl enable tt-rss

```

Do

```
$ systemctl status tt-rss

```

to check that it's running fine.