[Tiny Tiny RSS](https://tt-rss.org/) is an open source web-based news feed (RSS/Atom) aggregator, designed to allow you to read news from any location, while feeling as close to a real desktop application as possible.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Set up php and database](#Set_up_php_and_database)
    *   [1.2 Pacman hook](#Pacman_hook)
    *   [1.3 Set up an update daemon](#Set_up_an_update_daemon)
    *   [1.4 Known issues](#Known_issues)
        *   [1.4.1 Integrity constraint violation: 1062 Duplicate entry '1' for key 'ttrss_feeds_feed_url_owner_uid_key'](#Integrity_constraint_violation:_1062_Duplicate_entry_'1'_for_key_'ttrss_feeds_feed_url_owner_uid_key')
        *   [1.4.2 PHP UConverter class is missing, it's provided by the Internationalization (intl) module.](#PHP_UConverter_class_is_missing,_it's_provided_by_the_Internationalization_(intl)_module.)

## Installation

Install [tt-rss](https://www.archlinux.org/packages/?name=tt-rss) from the [official repositories](/index.php/Official_repositories "Official repositories").

If you plan on using PostgreSQL, install [php-pgsql](https://www.archlinux.org/packages/?name=php-pgsql)

tt-rss is installed into `/usr/share/webapps/tt-rss/`; you'll need to make this directory available from your web server. The simplest way is to do :

*   With [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") :

	 `# ln -s /usr/share/webapps/tt-rss /srv/http/tt-rss` 

*   With [Nginx](/index.php/Nginx "Nginx") :

	 `# ln -s /usr/share/webapps/tt-rss /usr/share/nginx/html/tt-rss` 

You will need to recursively chown `/usr/share/webapps/tt-rss` to http:http.

### Set up php and database

You'll need to set up a database, either [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL").

Create a ttrss user and database, e.g. with mysql:

```
$ mysql -p -u root
mysql> CREATE USER 'ttrss'@'localhost' IDENTIFIED BY 'somepassword';
mysql> CREATE DATABASE ttrss;
mysql> GRANT ALL PRIVILEGES ON ttrss.* TO "ttrss"@"localhost" IDENTIFIED BY 'somepassword';

```

Or create a ttrss user and database in PostgreSQL, e.g.:

```
[postgres]$ createuser -P --interactive
[postgres]$ createdb -U ttrss ttrss

```

In `/etc/php/php.ini`, enable the following modules:

```
extension=curl
extension=iconv
extension=intl
extension=mysqli # for MySQL
extension=pdo_mysql # for MySQL
extension=pdo_pgsql # for PostgreSQL
extension=pgsql # for legacy PostgreSQL plugins (still required by default)
extension=soap

```

*If* `open_basedir` is set in `/etc/php/php.ini` (it isn't by default), add `/var/lib/tt-rss:/usr/share/webapps/tt-rss:/etc/webapps/tt-rss` to it.

Application initialization can be done either automatically or manually.

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

With PostgreSQL run:

```
$ psql ttrss -U ttrss -f /usr/share/webapps/tt-rss/schema/ttrss_schema_pgsql.sql

```

### Pacman hook

To do tt-rss database upgrades automatically you may set up pacman post upgrade hook based on following example:

```
[Trigger]
Operation = Install
Operation = Upgrade
Type = Package
Target = tt-rss

[Action]
Description = Updating TT-RSS Database
When = PostTransaction
Exec = /usr/bin/runuser -u http -- /usr/bin/php /usr/share/webapps/tt-rss/update.php --update-schema

```

You need to put it into /etc/pacman.d/hooks/tt-rss.hook if you did not customize HookDir in pacman.conf.

See also [Pacman#Hooks](/index.php/Pacman#Hooks "Pacman")

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

### Known issues

#### Integrity constraint violation: 1062 Duplicate entry '1' for key 'ttrss_feeds_feed_url_owner_uid_key'

If you update tt-rss database to schema 137 you might see the error *Duplicate entry '1' for key 'ttrss_feeds_feed_url_owner_uid_key'*. To fix the issue please start database shell, e.g.:

```
$ mysql -u ttrss -p
$ use tt-rss;

```

And then run [query from official forum](https://discourse.tt-rss.org/t/potential-problems-when-upgrading-to-schema-137/2122) that drops duplicated database entries.

#### PHP UConverter class is missing, it's provided by the Internationalization (intl) module.

If you see this error after tt-rss upgrade, please edit `/etc/php/php.ini`, enable 'extension=intl' module and then restart php-fpm systemctl service

```
# systemctl restart php-fpm.service

```