[Cacti](https://www.cacti.net/) is a web-based system monitoring and graphing solution.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 PHP](#PHP)
    *   [2.2 SNMP](#SNMP)
    *   [2.3 MySQL](#MySQL)
*   [3 Hosting](#Hosting)
    *   [3.1 Apache](#Apache)
        *   [3.1.1 php-fpm](#php-fpm)
    *   [3.2 Nginx](#Nginx)
        *   [3.2.1 php-fpm](#php-fpm_2)
        *   [3.2.2 uWSGI](#uWSGI)
*   [4 Setup](#Setup)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Spine](#Spine)
    *   [5.2 Systemd](#Systemd)
*   [6 See also](#See_also)

## Installation

To use cacti, you need a working [web server](/index.php/Web_server "Web server") (e.g. [Nginx](/index.php/Nginx "Nginx") or [Apache](/index.php/Apache "Apache")) setup, that forwards requests to an application server (e.g. [uWSGI](/index.php/UWSGI "UWSGI") or [php-fpm](https://www.archlinux.org/packages/?name=php-fpm)).

Next, [install](/index.php/Install "Install") [cacti](https://www.archlinux.org/packages/?name=cacti) and configure [MariaDB](/index.php/MariaDB "MariaDB"), if a local MySQL server will be used.

**Note:** Cacti should only be accessed over [TLS](/index.php/TLS "TLS") (unless accessed directly from the machine running it), as it otherwise exposes passwords and user data.

## Configuration

To serve cacti top level instead of under `/cacti/` (i.e. [https://example.tld/](https://example.tld/) instead of [https://example.tld/cacti/](https://example.tld/cacti/)) use the `$url_path` configuration option:

 `/etc/webapps/cacti/config.php`  `$url_path = '/';` 

### PHP

**Note:** Due to an unresolved upstream issue, cacti is unable to stay in its own [PHP](/index.php/PHP "PHP") environment [[1]](https://github.com/Cacti/cacti/issues/2643). Required [PHP](/index.php/PHP "PHP") modules have to be activated in the system's global `/etc/php/php.ini`.

Cacti requires the following [PHP extensions](/index.php/PHP#Extensions "PHP") to be enabled:

 `/etc/php/php.ini` 
```
extension=gd
extension=gettext
extension=gmp
extension=ldap
extension=mysqli
extension=pdo_mysql
extension=snmp
extension=sockets
```

Cacti needs certain directories and executables in [PHP](/index.php/PHP "PHP")'s `open_basedir` [[2]](https://www.php.net/manual/en/ini.core.php#ini.open-basedir) to function properly: `/tmp/:/usr/share/webapps/cacti:/etc/webapps/cacti:/var/cache/cacti:/var/lib/cacti:/var/log/cacti:/proc/meminfo:/usr/bin/rrdtool:/usr/bin/snmpget:/usr/bin/snmpwalk:/usr/bin/snmpbulkwalk:/usr/bin/snmpgetnext:/usr/bin/snmptrap:/usr/bin/sendmail:/usr/bin/php:/usr/bin/spine:/usr/share/fonts/TTF/`.

Cacti requires `date.timezone` to be set in `/etc/php/php.ini`. Check upstream documentation [[3]](https://www.php.net/manual/en/datetime.configuration.php#ini.date.timezone) and [time zone](/index.php/Time_zone "Time zone") for reference.

### SNMP

If it is necessary for cacti to monitor the machine that it is running on, configure [snmpd](/index.php/Snmpd "Snmpd").

### MySQL

Cacti needs its own database in which to store its data, and a database user account to access the database.

Run the following commands as root:

```
# mysqladmin -u root -p create cactidb
# mysql -u root -p cactidb </usr/share/webapps/cacti/cacti.sql
# mysql -u root -p
mysql> GRANT ALL ON cactidb.* TO cactiuser@localhost IDENTIFIED BY 'some_password';
mysql> FLUSH PRIVILEGES;
mysql> exit

```

Alternatively, use [PhpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin") to achieve the same results:

*   Create an empty database called `cactidb`.
*   Import the file `/usr/share/webapps/cacti/cacti.sql` into the `cactidb` database.
*   Create a user `cactiuser`, and grant this user privileges to access the `cactidb` database.

Add the database details:

 `/etc/webapps/cacti/config.php` 
```
$database_type = "mysql";
$database_default = "cactidb";
$database_username = "cactiuser";
$database_password = "some_password";
```

## Hosting

**Note:** Cacti needs to be run as its own user and group (i.e. `cacti`). It's using `/etc/webapps/cacti`, `/var/lib/cacti`, `/var/log/cacti` and `/run/cacti` for configurations, caches, logs and (potentially) sockets (respectively)!

### Apache

The [apache](/index.php/Apache "Apache") [web server](/index.php/Web_server "Web server") can serve dynamic web applications with the help of modules, such as [mod_proxy_fcgi](https://httpd.apache.org/docs/current/mod/mod_proxy_fcgi.html) or [mod_proxy_uwsgi](https://httpd.apache.org/docs/current/mod/mod_proxy_uwsgi.html).

#### php-fpm

[Install](/index.php/Install "Install") and configure [apache](/index.php/Apache "Apache") with [php-fpm](/index.php/Apache_HTTP_Server#Using_php-fpm_and_mod_proxy_fcgi "Apache HTTP Server"). Use a [pool](https://www.php.net/manual/en/install.fpm.configuration.php) run as user and group `cacti`. The socket file should be accessible by the `http` user and/or group, but needs to be located below `/run/cacti`.

Include the following configuration in your [apache](/index.php/Apache "Apache") configuration (i.e. `/etc/httpd/conf/httpd.conf`) and [restart](/index.php/Restart "Restart") the [web server](/index.php/Web_server "Web server"):

 `/etc/httpd/conf/cacti.conf` 
```
Alias /cacti "/usr/share/webapps/cacti"
<Directory "/usr/share/webapps/cacti">
    DirectoryIndex index.html index.php
    <FilesMatch \.php$>
        SetHandler "proxy:unix:/run/cacti/cacti.sock|fcgi://localhost/"
    </FilesMatch>
    AllowOverride All
    Options FollowSymlinks
    Require all granted
</Directory>

```

The file `/usr/share/webapps/cacti/.htaccess` also controls access. Configure or remove it.

### Nginx

[Nginx](/index.php/Nginx "Nginx") can proxy application servers such as [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) and [uWSGI](/index.php/UWSGI "UWSGI"), that run a dynamic web application. The following examples describe a folder based setup over a non-default port (for simplicity).

**Tip:** For server entry management in [nginx](/index.php/Nginx "Nginx") have a look at [Nginx#Managing server entries](/index.php/Nginx#Managing_server_entries "Nginx").

**Note:** Postfixadmin ships a configuration for [uWSGI](/index.php/UWSGI "UWSGI").

#### php-fpm

[Install](/index.php/Install "Install") [php-fpm](https://www.archlinux.org/packages/?name=php-fpm). Setup [nginx](/index.php/Nginx "Nginx") with [php-fpm](/index.php/Nginx#PHP_implementation "Nginx") and use a [pool](https://www.php.net/manual/en/install.fpm.configuration.php) run as user and group `cacti`. The socket file should be accessible by the `http` user and/or group, but needs to be located below `/run/cacti`. This can be achieved by adding the following lines to the php-fpm configuration and [restarting](/index.php/Systemd#Using_units "Systemd") it.

 `/etc/php/php-fpm.d/www.conf` 
```

[cacti]
user = cacti
group = cacti
listen = /run/cacti/cacti.sock
listen.owner = http
listen.group = http
pm = ondemand
pm.max_children = 4

```

Add the following configuration for [nginx](/index.php/Nginx "Nginx") and [restart](/index.php/Restart "Restart") it.

 `/etc/nginx/sites-available/cacti.conf` 
```
server {
  listen 8081;
  server_name cacti;
  root /usr/share/webapps/cacti/;
  index index.php;
  charset utf-8;

  access_log /var/log/nginx/cacti-access.log;
  error_log /var/log/nginx/cacti-error.log;

  location / {
    try_files $uri $uri/ index.php;
  }

  location ~* \.php$ {
    fastcgi_split_path_info ^(.+\.php)(/.+)$;
    include fastcgi_params;
    fastcgi_pass unix:/run/cacti/cacti.sock;
    fastcgi_index index.php;
    include fastcgi_params;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    fastcgi_buffer_size 16k;
    fastcgi_buffers 4 16k;
  }
}

```

#### uWSGI

[Install](/index.php/Install "Install") [uwsgi-plugin-php](https://www.archlinux.org/packages/?name=uwsgi-plugin-php), create a per-application socket for [uWSGI](/index.php/UWSGI "UWSGI") (see [UWSGI#Accessibility of uWSGI socket](/index.php/UWSGI#Accessibility_of_uWSGI_socket "UWSGI") for reference) and [activate](/index.php/Systemd#Using_units "Systemd") the `cacti@uwsgi-secure.socket` unit.

Add the following configuration for nginx and [restart](/index.php/Restart "Restart") [nginx](/index.php/Nginx "Nginx").

 `/etc/nginx/sites-available/cacti.conf` 
```
    server {
      listen 8081;
      server_name cacti;
      root /usr/share/webapps/cacti/;
      index index.php;
      charset utf-8;

      access_log /var/log/nginx/cacti-access.log;
      error_log /var/log/nginx/cacti-error.log;

      location / {
        try_files $uri $uri/ index.php;
      }

      # pass all .php or .php/path urls to uWSGI
      location ~ ^(.+\.php)(.*)$ {
        include uwsgi_params;
        uwsgi_modifier1 14;
        uwsgi_pass unix:/run/cacti/cacti.sock;
      }
    }

```

## Setup

Open a browser and go to http://your_server/cacti/. You should be welcomed with the cacti installer.

*   Login with username "admin" and password "admin".
*   Change the password as requested, click *Save*.
*   Follow the remaining install steps and recommendations.
*   (Optional) If you chose to install spine, follow these instructions to set it up.
    *   Click on *Settings*, on the left panel of the Console tab.
    *   Select the *Poller* tab.
    *   Change Poller Type to spine.
    *   Adjust any other settings on the page as desired, then click *Save*.
    *   Select the *Paths* tab.
    *   Set Spine Poller File Path to `/usr/bin/spine` and click *Save*.

## Tips and tricks

### Spine

Optionally, install [cacti-spine](https://aur.archlinux.org/packages/cacti-spine/), a faster poller for cacti, from the [AUR](/index.php/AUR "AUR"). configure it with database access details:

 `/etc/spine.conf` 
```
DB_User cactiuser
DB_Pass some_password

```

### Systemd

**Tip:** The configuration for [uWSGI](/index.php/UWSGI "UWSGI") integrates a cron based approach, that makes a separate systemd unit not necessary.

Cacti uses a poller to collect data, so create a [Systemd](/index.php/Systemd "Systemd") service to run `poller.php`, and a timer to run the service every 5 minutes:

 `/etc/systemd/system/cacti_poller.service` 
```
[Unit]
Description=Cacti Poller

[Service]
User=cacti
Type=simple
ExecStart=/usr/bin/php /usr/share/webapps/cacti/poller.php

```
 `/etc/systemd/system/cacti_poller.timer` 
```
[Unit]
Description=Cacti Poller Timer

[Timer]
OnCalendar=*:0/5:0
Unit=cacti_poller.service
AccuracySec=1

[Install]
WantedBy=multi-user.target

```

**Note:** Do not start or enable `cacti_poller.service`. Instead, [start](/index.php/Start "Start") and enable `cacti_poller.timer` only, which calls the service every 5 minutes.

**Tip:** [journalctl](/index.php/Journalctl "Journalctl") can be used to watch for the poller's log messages, which will resemble the following:
```
Sep 27 15:50:00 hoom php[4072]: OK u:0.00 s:0.01 r:0.35
Sep 27 15:50:00 hoom php[4072]: OK u:0.00 s:0.01 r:0.38
Sep 27 15:50:00 hoom php[4072]: OK u:0.00 s:0.01 r:0.40
Sep 27 15:50:01 hoom php[4072]: 09/27/2015 03:50:01 PM - SYSTEM STATS: Time:0.6176 Method:cmd.php Processes:1 Threads:N/A Hosts:5 HostsPerProcess:5 DataSources:169 RRDsProcessed:15

```

## See also

*   [https://cacti.net](https://cacti.net)