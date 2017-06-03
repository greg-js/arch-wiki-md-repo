[Icinga](https://www.icinga.org/) is an open source host, service and network monitoring program. It monitors specified hosts and services, alerting you to any developing issues, errors or improvements. This article describes the installation and configuration of Icinga.

## Contents

*   [1 Installation](#Installation)
*   [2 Icinga configuration](#Icinga_configuration)
*   [3 Icinga2 configuration](#Icinga2_configuration)
*   [4 Webserver configuration](#Webserver_configuration)
    *   [4.1 Additional Nginx configuration](#Additional_Nginx_configuration)
*   [5 Icinga-web](#Icinga-web)
    *   [5.1 Configure IDOUtils](#Configure_IDOUtils)
    *   [5.2 Configure web server](#Configure_web_server)
        *   [5.2.1 Configure PHP](#Configure_PHP)
        *   [5.2.2 Configure database](#Configure_database)
            *   [5.2.2.1 MySQL](#MySQL)
    *   [5.3 Finally](#Finally)
*   [6 Upgrade database](#Upgrade_database)
*   [7 See also](#See_also)

## Installation

Follow [Install Web Application Package](/index.php/Web_application_package_guidelines#Install_web_application_package "Web application package guidelines")

Before you install the package create the user `icinga:icinga` with these commands:

```
# groupadd -g 667 icinga
# useradd -u 667 -g icinga -G http -d /dev/null -s /bin/false icinga

```

Install [icinga](https://aur.archlinux.org/packages/icinga/) or [icinga2](https://aur.archlinux.org/packages/icinga2/) from the [AUR](/index.php/AUR "AUR").

Users may also want to install [monitoring-plugins](https://www.archlinux.org/packages/?name=monitoring-plugins) from the Community repositories.

## Icinga configuration

Copy the sample config files as root:

```
# cd /etc/icinga
# cp cgi.cfg.sample cgi.cfg
# cp resource.cfg.sample resource.cfg
# cp icinga.cfg.sample icinga.cfg
# cp objects/commands.cfg.sample objects/commands.cfg
# cp objects/contacts.cfg.sample objects/contacts.cfg
# cp objects/localhost.cfg.sample objects/localhost.cfg
# cp objects/templates.cfg.sample objects/templates.cfg
# cp objects/timeperiods.cfg.sample objects/timeperiods.cfg

```

Edit `/etc/icinga/resource.cfg`:

 `/etc/icinga/resource.cfg` 
```
# Default monitoring plugins
$USER1$=/usr/lib/monitoring-plugins
# or legacy Nagios plugins 
#$USER1$=/usr/share/nagios/libexec
```

## Icinga2 configuration

By default Icinga 2 uses the following files and directories:

```
# /etc/icinga2	                Contains Icinga 2 configuration files.
# /etc/init.d/icinga2	        The Icinga 2 init script.
# /usr/sbin/icinga2*	        The Icinga 2 binary.
# /usr/share/doc/icinga2	Documentation files that come with Icinga 2.
# /usr/share/icinga2/include	The Icinga Template Library and plugin command configuration.
# /var/run/icinga2	        PID file.
# /var/run/icinga2/cmd	        Command pipe and Livestatus socket.
# /var/cache/icinga2	        status.dat/objects.cache, icinga2.debug files
# /var/spool/icinga2	        Used for performance data spool files.
# /var/lib/icinga2	        Icinga 2 state file, cluster log, local CA and configuration files.
# /var/log/icinga2	        Log file location and compat/ directory for the CompatLogger feature.

```

## Webserver configuration

Create htpasswd.users file with a username and password.

```
# htpasswd -c /etc/icinga/htpasswd.users icingaadmin

```

If you define another user foo, you need grant access permission to that user. Edit /etc/icinga/cgi.cfg

```
authorized_for_system_information=icingaadmin,foo
authorized_...
...

```

### Additional Nginx configuration

Configure Authentication:

```
 location /icinga/ {
   alias                   /usr/share/webapps/icinga/;
   auth_basic              "Restricted";
   auth_basic_user_file    /etc/icinga/htpasswd.users;
 }

```

Configure CGI:

```
   location ~ ^/icinga/(.*)\.cgi$ {
     root           /usr/share/webapps/;
     fastcgi_pass   unix:/var/run/fcgiwrap.sock;
     include        fastcgi.conf;
     fastcgi_param  AUTH_USER          $remote_user;
     fastcgi_param  REMOTE_USER        $remote_user;
   }

```

## Icinga-web

Follow [Install Web Application Package](/index.php/Web_application_package_guidelines#Install_web_application_package "Web application package guidelines")

Install [icinga-web](https://aur.archlinux.org/packages/icinga-web/) from the [AUR](/index.php/AUR "AUR").

### Configure IDOUtils

```
 # cd /etc/icinga
 # mv idomod.cfg-sample idomod.cfg
 # mv ido2db.cfg-sample ido2db.cfg

 # cd /etc/icinga/modules
 # mv idoutils.cfg-sample idoutils.cfg

 ! Database Setup

 (Mysql)
 $ mysql -u root -p
 > CREATE USER 'icinga'@'localhost' IDENTIFIED BY 'icinga';
 > CREATE DATABASE icinga;
 > GRANT USAGE ON icinga.* TO 'icinga'@'localhost' WITH MAX_QUERIES_PER_HOUR 0 MAX_CONNECTIONS_PER_HOUR 0 MAX_UPDATES_PER_HOUR 0;
 > GRANT SELECT , INSERT , UPDATE , DELETE, DROP, CREATE VIEW, INDEX
  ON icinga.* TO 'icinga'@'localhost';
 > FLUSH PRIVILEGES;
 > quit

 $ mysql -u root -p icinga < /usr/share/icinga/idoutils/db/mysql/mysql.sql

```

### Configure web server

Example config files are located at

```
 /etc/icinga-web/apache.example.conf
 /etc/icinga-web/nginx.example.conf

```

If you get 503 'Access denied' errors, check in these configuration files to see if you're allowed to visit the page:

```
 Order allow,deny
 Allow from all

```

in sections *<Directory "/usr/local/icinga-web/lib/ext3/">* and *<Directory "/usr/local/icinga-web/pub/">*.

#### Configure PHP

Edit `/etc/php.ini`

```
 open_basedir = ...:/usr/share/icinga-web:/var/cache/icinga-web:/var/log/icinga
 extension=pdo_mysql.so
 extension=xsl.so
 extension=sockets.so

```

#### Configure database

##### MySQL

```
! Create database and grants.
# mysql -u root -p
> CREATE USER 'icinga_web'@'localhost' IDENTIFIED BY 'icinga_web';
> CREATE DATABASE icinga_web;
> GRANT USAGE ON icinga_web.* TO 'icinga_web'@'localhost' WITH MAX_QUERIES_PER_HOUR 0 MAX_CONNECTIONS_PER_HOUR 0 MAX_UPDATES_PER_HOUR 0;
> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, ALTER, INDEX ON icinga_web.* TO 'icinga_web'@'localhost';
> quit

 ! Import the schema.
# mysql -u root -p icinga_web < /usr/share/icinga-web/etc/schema/mysql.sql

```

### Finally

```
! Start IDOUtils
# systemctl start ido2db

! Start Icinga
# systemctl start icinga

! Start Mysql
# systemctl start mysqld

! Start Web Server
# systemctl start httpd or nginx

! goto [http://localhost/icinga-web](http://localhost/icinga-web)
> login with 'root' and 'password'

```

## Upgrade database

A new version usually requires an upgrade of the database. You find the SQL upgrade scripts in:

```
/usr/share/icinga/idoutils/db/mysql/upgrade
/usr/share/icinga-web/etc/schema/updates/mysql

```

Commands to upgrade with these scripts are:

```
# mysql -u root -p icinga < ./mysql-upgrade-1.8.0.sql 
# mysql -u root -p icinga_web < ./mysql_v1-7-2_to_v1-8-0.sql
# systemctl --system daemon-reload
# systemctl restart icinga

```

## See also

*   [icinga.org](https://www.icinga.org/) - Official website
*   [monitoring-plugins](https://www.monitoring-plugins.org/) - Default plugins for Icinga and other monitoring applications
*   [Nagios Plugins](https://nagios-plugins.org/) - The home of the legacy plugins
*   [Wikipedia article](https://en.wikipedia.org/wiki/Icinga "w:Icinga")
*   [NagiosExchange](https://exchange.nagios.org/) - Overview of plugins, addons, mailing lists for Icinga