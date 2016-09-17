[Cacti](http://www.cacti.net/) is a web-based system monitoring and graphing solution.

## Contents

*   [1 Server Setup](#Server_Setup)
*   [2 Cacti Setup](#Cacti_Setup)
*   [3 MySQL setup](#MySQL_setup)
*   [4 Spine](#Spine)
*   [5 Systemd](#Systemd)
*   [6 Web Configuration](#Web_Configuration)
*   [7 External Links](#External_Links)

## Server Setup

This article assumes that you already have a working [LAMP](/index.php/LAMP "LAMP") (Linux, Apache, MySQL, PHP) server.

## Cacti Setup

[Install](/index.php/Install "Install") the [cacti](https://www.archlinux.org/packages/?name=cacti), [php-snmp](https://www.archlinux.org/packages/?name=php-snmp) and [net-snmp](https://www.archlinux.org/packages/?name=net-snmp) packages. Ensure LAMP services (`httpd`, `mysqld`) are [started](/index.php/Start "Start") and [enabled](/index.php/Enable "Enable"). If it is necessary for Cacti to monitor the machine that it is running on, configure [snmpd](/index.php/Snmpd "Snmpd").

Cacti uses PHP, an SQL database (MySQL or MariaDB) and SNMP, so enable the required PHP modules:

 `/etc/php/php.ini` 
```
extension=mysqli.so
extension=sockets.so
extension=pdo_mysql.so
extension=snmp.so
```

PHP scripts are, by default, permitted only to open files in specific directories. Configure (or comment out) `open_basedir` in `/etc/php/php.ini`. When misconfigured, errors such as `PHP Warning: include(): open_basedir restriction in effect.` will appear in the webserver log file.

In order to display dates and times in the correct timezone, configure `date.timezone` in `/etc/php/php.ini`. Values are in "Continent/City" notation, for example "America/New_York", "Asia/Tokyo".

Configure Apache to point to Cacti by adding the following in a `/etc/httpd/conf/extra/cacti.conf` (or in a vhost's config file):

```
Alias /cacti /usr/share/webapps/cacti
<Directory /usr/share/webapps/cacti>
  # PHP options
  AddType application/x-httpd-php .php
  <IfModule dir_module>
    DirectoryIndex index.php
  </IfModule>

  Require all granted
  Options +FollowSymLinks
  AllowOverride All

  # The following may be useful.
  #<IfModule mod_php5.c>
  #  php_flag magic_quotes_gpc Off
  #  php_flag short_open_tag On
  #  php_flag register_globals Off
  #  php_flag register_argc_argv On
  #  php_flag track_vars On
  #  # This setting is necessary for some locales.
  #  php_value mbstring.func_overload 0
  #  php_value include_path .
  #</IfModule>
</Directory>

```

If the Cacti config is in a separate file, remember to add `Include conf/extra/cacti.conf` to `/etc/httpd/conf/httpd.conf`.

The file `/usr/share/webapps/cacti/.htaccess` also controls access. Configure or remove it.

Cacti needs to have permission to write its gathered data and log messages to disk: `# chown -R http:http /usr/share/webapps/cacti/{rra,log}`

## MySQL setup

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

Add the database access details to `/usr/share/webapps/cacti/include/config.php`:

```
$database_default = "cactidb";
$database_username = "cactiuser";
$database_password = "some_password";
```

## Spine

Optionally, install [cacti-spine](https://aur.archlinux.org/packages/cacti-spine/), a faster poller for cacti, from the [AUR](/index.php/AUR "AUR"). configure it with database access details:

 `/etc/spine.conf` 
```
DB_User cactiuser
DB_Pass some_password
```

## Systemd

Cacti uses a poller to collect data, so create a [Systemd](/index.php/Systemd "Systemd") service to run poller.php, and a timer to run the service every 5 minutes:

 `/etc/systemd/system/cacti_poller.service` 
```
[Unit]
Description=Cacti Poller

[Service]
User=http
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

## Web Configuration

Open a browser and go to http://your_server/cacti/. You should be welcomed with the cacti installer.

*   Click Next
*   Select New Install and click Next
*   Ensure that all paths are ok. You need to specify versions of RRDTool and NET-SNMP. Get RRDTool Utility Version using 'rrdtool -v', and'net-snmp-config --version' for NET-SNMP. Click Finish.
    *   If any paths are invalid, you'll need to figure out why. Check the apache error logs for hints.
*   Login with username "admin" and password "admin".
*   Change the password as requested, click Save.
*   (Optional) If you chose to install spine, follow these instructions to set it up.
    *   Click on Settings, on the left panel of the Console tab.
    *   Select the Poller tab.
    *   Change Poller Type to spine.
    *   Adjust any other settings on the page as desired, then click Save.
    *   Select the Paths tab.
    *   Set Spine Poller File Path to /usr/bin/spine and click Save.

## External Links

*   [http://cacti.net](http://cacti.net)