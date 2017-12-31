Related articles

*   [DAViCal](/index.php/DAViCal "DAViCal")
*   [Kcaldav](/index.php/Kcaldav "Kcaldav")
*   [Radicale](/index.php/Radicale "Radicale")

[AgenDAV](http://agendav.org/) is an open source multilanguage CalDAV web application, written in PHP, which features a rich AJAX interface with shared calendars support.

## Installation

[Install](/index.php/Install "Install") the [agendav](https://aur.archlinux.org/packages/agendav/) package.

### Database

You must provide a SQL database to AgenDAV. Here is a PostgreSQL example.

Install [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") according to the article. Create a `agendav` user and database:

```
# createuser agendav
# createdb -O agendav agendav

```

### Configuration

When the database is setup, you must manually populate it:

```
# psql -U agendav agendav < /usr/share/webapps/agendav/sql/pgsql.schema.sql
# bash /usr/share/webapps/agendav/bin/agendavcli dbupdate

```

Make sure you enable the **pgsql.so** (or whatever database you used) and **iconv.so** extension in php.ini.

Edit the configuration files `/etc/webapps/agendav/{config,caldav,database}.php` to your liking.

Serve the app via apache `/etc/webapps/agendav/apache.example.conf`, nginx/php-fpm `/etc/webapps/agendav/nginx.example.conf` or some other webserver.