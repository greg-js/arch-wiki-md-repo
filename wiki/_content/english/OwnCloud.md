From [Wikipedia](https://en.wikipedia.org/wiki/ownCloud "wikipedia:ownCloud"): "ownCloud is a software suite that provides a location-independent storage area for data (cloud storage)." The ownCloud installation and configuration mainly depends on what web server and database you decide to run. Currently the wiki discusses [Apache configuration](#Apache_configuration) and [Nginx configuration](#Nginx).

## Contents

*   [1 Prerequisites](#Prerequisites)
    *   [1.1 An all-in-one alternative with Docker](#An_all-in-one_alternative_with_Docker)
*   [2 Installation](#Installation)
    *   [2.1 Database support](#Database_support)
    *   [2.2 Caching](#Caching)
    *   [2.3 Exif support](#Exif_support)
    *   [2.4 Optional but recommended security hardening](#Optional_but_recommended_security_hardening)
        *   [2.4.1 Setting strong permissions for the filesystem](#Setting_strong_permissions_for_the_filesystem)
        *   [2.4.2 Protection from hacking with fail2ban](#Protection_from_hacking_with_fail2ban)
*   [3 Database Setup](#Database_Setup)
    *   [3.1 Mariadb](#Mariadb)
*   [4 Webserver Setup](#Webserver_Setup)
    *   [4.1 Apache configuration](#Apache_configuration)
        *   [4.1.1 WebDAV](#WebDAV)
        *   [4.1.2 Running ownCloud in a subdirectory](#Running_ownCloud_in_a_subdirectory)
    *   [4.2 Nginx](#Nginx)
        *   [4.2.1 php-fpm configuration](#php-fpm_configuration)
    *   [4.3 uWSGI configuration](#uWSGI_configuration)
        *   [4.3.1 Configuration](#Configuration)
        *   [4.3.2 Activation](#Activation)
*   [5 Synchronization](#Synchronization)
    *   [5.1 Desktop](#Desktop)
        *   [5.1.1 Calendar](#Calendar)
        *   [5.1.2 Contacts](#Contacts)
        *   [5.1.3 Mounting files with davfs2](#Mounting_files_with_davfs2)
    *   [5.2 Android](#Android)
*   [6 Important notes](#Important_notes)
    *   [6.1 SABnzbd](#SABnzbd)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Self-signed certificate not accepted](#Self-signed_certificate_not_accepted)
    *   [7.2 Self-signed certificate for Android devices](#Self-signed_certificate_for_Android_devices)
    *   [7.3 Cannot write into config directory!](#Cannot_write_into_config_directory.21)
    *   [7.4 Cannot create data directory (/path/to/dir)](#Cannot_create_data_directory_.28.2Fpath.2Fto.2Fdir.29)
    *   [7.5 CSync failed to find a specific file.](#CSync_failed_to_find_a_specific_file.)
    *   [7.6 Seeing white page after login](#Seeing_white_page_after_login)
    *   [7.7 GUI sync client fails to connect](#GUI_sync_client_fails_to_connect)
    *   [7.8 Some files upload, but give an error 'Integrity constraint violation...'](#Some_files_upload.2C_but_give_an_error_.27Integrity_constraint_violation....27)
    *   [7.9 "Cannot write into apps directory"](#.22Cannot_write_into_apps_directory.22)
    *   [7.10 Security warnings even though the recommended settings have been included in nginx.conf](#Security_warnings_even_though_the_recommended_settings_have_been_included_in_nginx.conf)
    *   [7.11 Password not saved](#Password_not_saved)
*   [8 Upload and Share from File Manager](#Upload_and_Share_from_File_Manager)
*   [9 See also](#See_also)

## Prerequisites

*ownCloud* needs a [web server](/index.php/Category:Web_server "Category:Web server"), [PHP](/index.php/PHP "PHP") and a [database](/index.php/Category:Database_management_systems "Category:Database management systems"). For instance, a classic [LAMP stack](/index.php/LAMP "LAMP") should work fine and is the [recommended configuration](https://doc.owncloud.org/server/8.2/admin_manual/installation/system_requirements.html#recommended-setup-for-running-owncloud).

### An all-in-one alternative with Docker

A alternative to installing and configuring your own *ownCloud* is to use a 3rd party supported [Docker](/index.php/Docker "Docker") image. You can find several images of fully working LAMP stack with pre-installed *ownCloud* in the [Docker repositories](https://index.docker.io/search?q=ownCloud). *Docker* containers are generally safer than a [chroot](/index.php/Chroot "Chroot") environment and the overhead is very low; *ownCloud* in Docker works smoothly even on quite old machines. The whole setup including installing *Docker* and *ownCloud* image is considerably easier and quicker than a native installation but you must trust the third party whom you have now given complete control to regarding the installation of your ownCloud instance.

**Note:** Docker images are not officially supported by ownCloud.

## Installation

[Install](/index.php/Install "Install") the [owncloud](https://www.archlinux.org/packages/?name=owncloud) package.

**Note:** When the Arch owncloud package is updated via pacman, it may become necessary to connect via the web interface to manually trigger an update of the associated files. Failure to do so will render the mobile app unable to connect.

Uncomment the following [required](https://doc.owncloud.org/server/8.2/admin_manual/installation/source_installation.html#prerequisites) extensions in `/etc/php/php.ini`:

```
gd.so
iconv.so
xmlrpc.so
zip.so

```

It is also [recommended](https://doc.owncloud.org/server/8.2/admin_manual/installation/source_installation.html#prerequisites) to install [php-intl](https://www.archlinux.org/packages/?name=php-intl), [php-mcrypt](https://www.archlinux.org/packages/?name=php-mcrypt) and uncomment the following extensions:

```
bz2.so
curl.so
intl.so
mcrypt.so

```

### Database support

Depending on which database backend you are going to use, uncomment the following extensions in `/etc/php/php.ini`:

*   For [MySQL](/index.php/MySQL "MySQL"), uncomment `pdo_mysql.so`.
*   For [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), uncomment `pdo_pgsql.so` and `pgsql.so`, and install [php-pgsql](https://www.archlinux.org/packages/?name=php-pgsql).
*   For [SQLite](/index.php/SQLite "SQLite"), uncomment `pdo_sqlite.so` and `sqlite3.so`, and install [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite).

### Caching

For enhanced performance, it is recommended to implement PHP caching using APCu, as described in [PHP#APCu](/index.php/PHP#APCu "PHP"). It is also beneficial to enable OPCache, as described in [PHP#OPCache](/index.php/PHP#OPCache "PHP").

Then, after enabling APCu, add the following directive to `/etc/webapps/owncloud/config/config.php`:

```
'memcache.local' => '\OC\Memcache\APCu',

```

**Note:** Make sure to add `apc.enable_cli=1` under the `[apc]` portion of your [PHP configuration](/index.php/PHP#Configuration "PHP") and uncomment `extension=apcu.so` in `/etc/php/conf.d/apcu.ini`. As of 2015-07-12, [several](https://github.com/owncloud/core/issues/17329#issuecomment-119248944) [things](https://github.com/owncloud/documentation/issues/1233#issuecomment-120664134) will not work properly without it.

See [the official documentation](https://doc.owncloud.org/server/8.1/admin_manual/configuration_server/config_sample_php_parameters.html#memory-caching-backend-configuration).

### Exif support

Additionally enable exif support by installing the [exiv2](https://www.archlinux.org/packages/?name=exiv2) package and uncommenting the `exif.so` extension in `php.ini`.

### Optional but recommended security hardening

#### Setting strong permissions for the filesystem

From the [official installation manual](https://doc.owncloud.org/server/8.2/admin_manual/installation/installation_wizard.html#setting-strong-directory-permissions):

	*For hardened security we recommend setting the permissions on your ownCloud directories as strictly as possible, and for proper server operations. This should be done immediately after the initial installation and before running the setup. Your HTTP user must own the `config/`, `data/` and `apps/` directories so that you can configure ownCloud, create, modify and delete your data files, and install apps via the ownCloud Web interface.*

 `oc-perms` 
```
#!/bin/bash
ocpath='/usr/share/webapps/owncloud'
htuser='http'
htgroup='http'
rootuser='root'

printf "Creating possible missing Directories
"
mkdir -p $ocpath/data
mkdir -p $ocpath/assets

printf "chmod Files and Directories
"
find ${ocpath}/ -type f -print0 | xargs -0 chmod 0640
find ${ocpath}/ -type d -print0 | xargs -0 chmod 0750

printf "chown Directories
"
chown -R ${rootuser}:${htgroup} ${ocpath}/
chown -R ${htuser}:${htgroup} ${ocpath}/apps/
chown -R ${htuser}:${htgroup} ${ocpath}/config/
chown -R ${htuser}:${htgroup} ${ocpath}/data/
chown -R ${htuser}:${htgroup} ${ocpath}/themes/
chown -R ${htuser}:${htgroup} ${ocpath}/assets/

chmod +x ${ocpath}/occ

printf "chmod/chown .htaccess
"
if [ -f ${ocpath}/.htaccess ]
 then
  chmod 0644 ${ocpath}/.htaccess
  chown ${rootuser}:${htgroup} ${ocpath}/.htaccess
fi
if [ -f ${ocpath}/data/.htaccess ]
 then
  chmod 0644 ${ocpath}/data/.htaccess
  chown ${rootuser}:${htgroup} ${ocpath}/data/.htaccess
fi

```

If you have customized your ownCloud installation and your filepaths are different than the standard installation, then modify this script accordingly.

#### Protection from hacking with fail2ban

Setting up [fail2ban](/index.php/Fail2ban "Fail2ban") is highly recommended. Once installed, create the following files:

 `/etc/fail2ban/filter.d/owncloud.conf` 
```
[Definition]
failregex={"reqId":".*","remoteAddr":".*","app":"core","message":"Login failed: '.*' \(Remote IP: '<HOST>'\)","level":2,"time":".*"}

ignoreregex =

```
 `/etc/fail2ban/jail.local` 
```
[owncloud]
enabled = true
filter  = owncloud
port    =  http,https
logpath = /usr/share/webapps/owncloud/data/owncloud.log
# optionally whitelist internal LAN IP addresses
ignoreip = 192.168.1.1/24

```

[Restart](/index.php/Restart "Restart") the `fail2ban` service. One can test the configuration by running the following:

```
fail2ban-regex /usr/share/webapps/owncloud/data/owncloud.log /etc/fail2ban/filter.d/owncloud.conf -v

```

## Database Setup

### Mariadb

After [MySQL#Installation](/index.php/MySQL#Installation "MySQL") and the initial setup described therein, a database and user for owncloud needs to be created within mariadb:

```
$ mysql -u root -p
create database owncloud;
create user ownclouduser@localhost identified by 'password';
grant all privileges on owncloud.* to ownclouduser@localhost identified by 'password';
flush privileges;
exit;

```

## Webserver Setup

### Apache configuration

**Note:** Make sure PHP is enabled, as described in [Apache HTTP Server#PHP](/index.php/Apache_HTTP_Server#PHP "Apache HTTP Server").

Copy the Apache configuration file to its configuration directory:

```
# cp /etc/webapps/owncloud/apache.example.conf /etc/httpd/conf/extra/owncloud.conf

```

And include it at the bottom of `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/owncloud.conf

```

Now restart Apache (`httpd.service`).

Open [http://localhost/owncloud](http://localhost/owncloud) in your browser. You should now be able to create a user account and follow the installation wizard.

**Note:** Moving your data folder to another location might conflict with the open_basedir option set in the default apache configuration file.

#### WebDAV

ownCloud comes with its own [WebDAV](/index.php/WebDAV "WebDAV") implementation enabled, which may conflict with the one shipped with Apache. If you have enabled WebDAV (not enabled by default with Apache), disable `mod_dav` and `mod_dav_fs` in `/etc/httpd/conf/httpd.conf`. See [https://forum.owncloud.org/viewtopic.php?f=17&t=7240](https://forum.owncloud.org/viewtopic.php?f=17&t=7240) for details.

#### Running ownCloud in a subdirectory

By including the default `owncloud.conf` in `httpd.conf`, ownCloud will take control of port 80 and your localhost domain.

If you would like to have ownCloud run in a subdirectory, then edit the `/etc/httpd/conf/extra/owncloud.conf` you included and comment out the `<VirtualHost *:80> ... </VirtualHost>` part of the include file.

### Nginx

#### php-fpm configuration

*ownCloud* official documentation uses [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) for [PHP](/index.php/PHP "PHP") and as such it is the best supported configuration. See [Nginx#PHP implementation](/index.php/Nginx#PHP_implementation "Nginx") to set up *php-fpm* and [Nginx#TLS/SSL](/index.php/Nginx#TLS.2FSSL "Nginx") to acquire and/or set up a TLS certificate.

By default, the only things you need to change from the [recommended server configuration](https://doc.owncloud.org/server/9.0/admin_manual/installation/nginx_configuration.html) for ownCloud to run on Arch Linux are the `server_name`, `ssl_certificate`, `ssl_certificate_key`, `root` and `fastcgi_pass` directives:

 `/etc/nginx/nginx.conf` 
```
server {
  listen 80;
  server_name cloud.example.com;
  # enforce https
  return 301 https://$server_name$request_uri;
}

server {
  listen 443 ssl;
  server_name cloud.example.com;

  ssl_certificate /path/to/domain-cert.crt;
  ssl_certificate_key /path/to/private-key.key;

  # Add headers to serve security related headers
  add_header Strict-Transport-Security "max-age=15768000; includeSubDomains; preload;";
  add_header X-Content-Type-Options nosniff;
  add_header X-Frame-Options "SAMEORIGIN";
  add_header X-XSS-Protection "1; mode=block";
  add_header X-Robots-Tag none;
  add_header X-Download-Options noopen;
  add_header X-Permitted-Cross-Domain-Policies none;

  # Path to the root of your installation
  root /usr/share/webapps/owncloud/;
  # set max upload size
  client_max_body_size 10G;
  fastcgi_buffers 64 4K;

  # Disable gzip to avoid the removal of the ETag header
  gzip off;

  # Uncomment if your server is build with the ngx_pagespeed module
  # This module is currently not supported.
  #pagespeed off;

  index index.php;
  error_page 403 /core/templates/403.php;
  error_page 404 /core/templates/404.php;

  rewrite ^/.well-known/carddav /remote.php/carddav/ permanent;
  rewrite ^/.well-known/caldav /remote.php/caldav/ permanent;

  # The following 2 rules are only needed for the user_webfinger app.
  # Uncomment it if you're planning to use this app.
  #rewrite ^/.well-known/host-meta /public.php?service=host-meta last;
  #rewrite ^/.well-known/host-meta.json /public.php?service=host-meta-json last;

  location = /robots.txt {
    allow all;
    log_not_found off;
    access_log off;
  }

  location ~ ^/(build|tests|config|lib|3rdparty|templates|data)/ {
    deny all;
  }

  location ~ ^/(?:\.|autotest|occ|issue|indie|db_|console) {
    deny all;
  }

  location / {
    rewrite ^/remote/(.*) /remote.php last;
    rewrite ^(/core/doc/[^\/]+/)$ $1/index.html;
    try_files $uri $uri/ =404;
  }

  location ~ \.php(?:$|/) {
    fastcgi_split_path_info ^(.+\.php)(/.+)$;
    include fastcgi_params;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    fastcgi_param PATH_INFO $fastcgi_path_info;
    fastcgi_param HTTPS on;
    fastcgi_param modHeadersAvailable true; #Avoid sending the security headers twice
    fastcgi_pass unix:/run/php-fpm/php-fpm.sock;
    fastcgi_intercept_errors on;
  }

  # Adding the cache control header for js and css files
  # Make sure it is BELOW the location ~ \.php(?:$|/) { block
  location ~* \.(?:css|js)$ {
    add_header Cache-Control "public, max-age=7200";
    # Add headers to serve security related headers
    add_header Strict-Transport-Security "max-age=15768000; includeSubDomains; preload;";
    add_header X-Content-Type-Options nosniff;
    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-XSS-Protection "1; mode=block";
    add_header X-Robots-Tag none;
    add_header X-Download-Options noopen;
    add_header X-Permitted-Cross-Domain-Policies none;
    # Optional: Don't log access to assets
    access_log off;
  }

  # Optional: Don't log access to other assets
  location ~* \.(?:jpg|jpeg|gif|bmp|ico|png|swf)$ {
    access_log off;
  }
}

```

*php-fpm* is already configured to run as the user `http`, so assuming you are using the permissions described above it should function fine. It is not recommended to manually copy the `config.example.php` in the ownCloud configuration, and instead let it be automatically generated on first run.

**Note:** Automatic configuration relies on the `data/` directory creation, as done in [#Setting strong permissions for the filesystem](#Setting_strong_permissions_for_the_filesystem).

### uWSGI configuration

You can run *ownCloud* in its own process and service by using the [uWSGI](/index.php/UWSGI "UWSGI") application server with [uwsgi-plugin-php](https://www.archlinux.org/packages/?name=uwsgi-plugin-php). This allows you to define a [PHP configuration](/index.php/PHP#Configuration "PHP") only for this instance of PHP, without the need to edit the global `php.ini` and thus keeping your web application configurations compartmentalized. *uWSGI* itself has a wealth of features to limit the resource use and to harden the security of the application, and by being a separate process it can run under its own user.

#### Configuration

The only part that differs from [#php-fpm configuration](#php-fpm_configuration) is the `location ~ \.php(?:$|/) {}` block:

```
  location ~ \.php(?:$|/) {
    include uwsgi_params;
    uwsgi_modifier1 14;
    # Avoid duplicate headers confusing OC checks
    uwsgi_hide_header X-Frame-Options;
    uwsgi_hide_header X-XSS-Protection;
    uwsgi_hide_header X-Content-Type-Options;
    uwsgi_hide_header X-Robots-Tag;
    uwsgi_pass unix:/run/uwsgi/owncloud.sock;
    }

```

Then create a config file for *uWSGI*:

 `/etc/uwsgi/owncloud.ini` 
```
[uwsgi]
; load the required plugins
plugins = php
; force the sapi name to 'apache', this will enable the opcode cache  
php-sapi-name = apache

; set master process name and socket
; '%n' refers to the name of this configuration file without extension
procname-master = uwsgi %n
master = true
socket = /run/uwsgi/%n.sock

; drop privileges
uid    = http
gid    = http
umask  = 027

; run with at least 1 process but increase up to 4 when needed
processes = 4
cheaper = 1

; reload whenever this config file changes
; %p is the full path of the current config file
touch-reload = %p

; disable uWSGI request logging
;disable-logging = true

; enforce a DOCUMENT_ROOT
php-docroot     = /usr/share/webapps/%n
; limit allowed extensions
php-allowed-ext = .php
; and search for index.php if required
php-index = index.php

; set php configuration for this instance of php, no need to edit global php.ini
php-set = date.timezone=Etc/UTC
;php-set = open_basedir=/tmp/:/usr/share/webapps/owncloud:/etc/webapps/owncloud:/dev/urandom
php-set = expose_php=false
; avoid security risk of leaving sessions in world-readable /tmp
php-set = session.save_path=/usr/share/webapps/owncloud/data

; port of php directives set upstream in /usr/share/webapps/owncloud/.user.ini for use with PHP-FPM
php-set = upload_max_filesize=513M
php-set = post_max_size=513M
php-set = memory_limit=512M
php-set = output_buffering=off

; load all extensions only in this instance of php, no need to edit global php.ini
;; required core modules
php-set = extension=gd.so
php-set = extension=iconv.so
;php-set = extension=zip.so     # enabled by default in global php.ini

;; database connectors
;; uncomment your selected driver
;php-set = extension=pdo_sqlite.so
;php-set = extension=pdo_mysql.so
;php-set = extension=pdo_pgsql.so

;; recommended extensions
;php-set = extension=curl.so    # enabled by default in global php.ini
php-set = extension=bz2.so
php-set = extension=intl.so
php-set = extension=mcrypt.so

;; required for specific apps
;php-set = extension=ldap.so    # for LDAP integration
;php-set = extension=ftp.so     # for FTP storage / external user authentication
;php-set = extension=imap.so    # for external user authentication, requires php-imap

;; recommended for specific apps
;php-set = extension=exif.so    # for image rotation in pictures app, requires exiv2
;php-set = extension=gmp.so     # for SFTP storage

;; for preview generation
;; provided by packages in AUR
; php-set = extension=imagick.so

; opcache
php-set = zend_extension=opcache.so

; user cache
; provided by php-acpu, to be enabled **either** here **or** in /etc/php/conf.d/apcu.ini
php-set = extension=apcu.so
; per https://github.com/krakjoe/apcu/blob/simplify/INSTALL
php-set = apc.ttl=7200
php-set = apc.enable_cli=1

cron2 = minute=-15,unique=1 /usr/bin/php -f /usr/share/webapps/owncloud/cron.php 1>/dev/null

```

**Note:**

*   Do not forget to set your timezone and uncomment the required database connector in the uWSGI config file
*   Starting with PHP 7, the [open_basedir](/index.php/PHP#Configuration "PHP") directive is [no longer set by default](https://www.archlinux.org/news/php-70-packages-released/) to keep in line with upstream. A commented out version functional until at least OC 8.2 has been left in the config for users wishing to harden security. Be aware that it may [occasionally break things](https://github.com/owncloud/core/search?q=open_basedir&type=Issues&utf8=%E2%9C%93).

**Warning:** The way the [ownCloud background job](https://doc.owncloud.org/server/9.0/admin_manual/configuration_server/background_jobs_configuration.html) is currently set up with [uWSGI cron](https://uwsgi-docs.readthedocs.org/en/latest/Cron.html) will make use of the default global configuration from `/etc/php/php.ini`. This means that none of the specific parameters defined (e.g. required modules) will be enabled, [leading to various issues](https://github.com/owncloud/core/issues/12678#issuecomment-66114448). One solution is to copy `/etc/php/php.ini` to e.g. `/etc/uwsgi/cron-php.ini`, make the required modifications there (mirroring `/etc/uwsgi/owncloud.ini` parameters) and referencing it in the cron directive by adding the `-c /etc/uwsgi/cron-php.ini` option to *php* invocation.

#### Activation

[uWSGI](/index.php/UWSGI "UWSGI") provides a [template unit](/index.php/Systemd#Using_units "Systemd") that allows to start and enable application using their configuration file name as instance identifier. For example:

```
# systemctl start uwsgi@owncloud.socket

```

would start it on demand referencing the configuration file `/etc/uwsgi/owncloud.ini`.

To enable the uwsgi service by default at start-up, run:

```
# systemctl enable uwsgi@owncloud.socket

```

**Note:** Here we make use of [systemd socket activation](http://0pointer.de/blog/projects/socket-activation.html) to prevent unnecessary resources consumption when no connections are made to the instance. If you would rather have it constantly active, simply remove the `.socket` part to start and enable the service instead.

See also [UWSGI#Starting service](/index.php/UWSGI#Starting_service "UWSGI").

## Synchronization

### Desktop

The official client can be installed with the [owncloud-client](https://www.archlinux.org/packages/?name=owncloud-client) package. Alternative versions are avaiable in the [AUR](/index.php/AUR "AUR"): [owncloud-client-beta](https://aur.archlinux.org/packages/owncloud-client-beta/), [owncloud-client-git](https://aur.archlinux.org/packages/owncloud-client-git/) and [owncloud-client-qt5](https://aur.archlinux.org/packages/owncloud-client-qt5/). Its use is described in [this page](http://doc.owncloud.org/server/7.0/user_manual/files/sync.html) of the documentation.

#### Calendar

To access your *ownCloud* calendars using Mozilla [Thunderbird](/index.php/Thunderbird "Thunderbird")'s [Lightning calendar](/index.php/Thunderbird#Lightning_-_Calendar "Thunderbird") you would use the following URL:

```
https://ADDRESS/remote.php/caldav/calendars/USERNAME/CALENDARNAME

```

To access your *ownCloud* calendars using CalDAV-compatible programs like Kontact or [Evolution](/index.php/Evolution "Evolution"), you would use the following URL:

```
https://ADDRESS/remote.php/caldav

```

For details see the [official documentation](http://doc.owncloud.org/server/7.0/user_manual/pim/calendar.html#synchronizing-calendars-using-caldav).

#### Contacts

To sync contacts with [Thunderbird](/index.php/Thunderbird "Thunderbird") you must install the [SOGo frontend](http://www.sogo.nu/downloads/frontends.html), [Lightning extension](/index.php/Thunderbird#Lightning_-_Calendar "Thunderbird") and follow [those instructions](http://doc.owncloud.org/server/7.0/user_manual/pim/sync_thunderbird.html) from the official doc.

#### Mounting files with davfs2

If you want to mount your ownCloud permanently install [davfs2](https://www.archlinux.org/packages/?name=davfs2) (as described in [Davfs](/index.php/Davfs "Davfs")) first.

Considering your ownCloud were at `[https://own.example.com](https://own.example.com)`, your WebDAV URL would be `[https://own.example.com/remote.php/webdav](https://own.example.com/remote.php/webdav)` (as of ownCloud 6.0).

To mount your ownCloud, use:

```
# mount -t davfs [https://own.example.com/remote.php/webdav](https://own.example.com/remote.php/webdav) /path/to/mount

```

You can also create an entry for this in `/etc/fstab`

 `/etc/fstab` 
```
[https://own.example.com/remote.php/webdav](https://own.example.com/remote.php/webdav) /path/to/mount davfs rw,user,noauto 0 0

```

**Tip:** In order to allow automount you can also store your username (and password if you like) in a file as described in [Davfs#Mounting as regular user](/index.php/Davfs#Mounting_as_regular_user "Davfs").

**Note:** If creating/copying files is not possible, while the same operations work on directories, see [Davfs#Creating/copying files not possible](/index.php/Davfs#Creating.2Fcopying_files_not_possible "Davfs").

### Android

There is an official Android app available for a [small donation on the Play Store](https://play.google.com/store/apps/details?id=at.bitfire.davdroid) and for free [on F-Droid](https://f-droid.org/app/at.bitfire.davdroid).

To enable contacts and calendar sync:

*   if using Android 4+:
    1.  download [[1]](https://davdroid.bitfire.at/) ([Play Store](https://play.google.com/store/apps/details?id=at.bitfire.davdroid), [F-Droid](https://f-droid.org/app/at.bitfire.davdroid))
    2.  Enable mod_rewrite.so in httpd.conf
    3.  create a new DAVdroid account in the *Account* settings, and specify your "short" server address and login/password couple, e.g. `https://cloud.example.com` (there is no need for the `/remote.php/{carddav,webdav}` part if you configured your web server with the proper redirections, as illustrated previously in the article; *DAVdroid* will find itself the right URLs)

	For an older version of the app but with still useful info, see [this article](http://www.slsmk.com/sync-android-contacts-calendar-and-files-to-owncloud/).

*   if using an Android version below 4.0 and favouring Free/Libre software solutions, give a try to [aCal](https://f-droid.org/repository/browse/?fdfilter=caldav&fdid=com.morphoss.acal) for calendar and contacts sync or CalDAV Sync Adapter ([F-Droid](https://f-droid.org/repository/browse/?fdfilter=caldav&fdid=org.gege.caldavsyncadapter)) for just calendar sync; if you are willing to use non-libre software, then the [recommended solution](http://doc.owncloud.org/server/7.0/user_manual/pim/contacts.html#synchronizing-with-android) is to use [CardDAV-Sync and CalDAV-Sync](http://dmfs.org/).

## Important notes

*   When using a subdomain (like cloud.example.net), make sure it is covered by your certificate. Otherwise, connection via the ownCloud client or webdav might fail.

*   If you are planning on using ownCloud's [sync-clients](http://owncloud.org/sync-clients/), make sure to have [ntpd](/index.php/Ntpd "Ntpd") installed and running on your ownCloud server, otherwise the sync-clients will fail.

*   Add some [SSL encryption](/index.php/LAMP#TLS.2FSSL "LAMP") to your connection!

(If adding SSL encryption as above, be sure to edit /etc/httpd/conf/extra/httpd-ssl.conf and change DocumentRoot "/srv/http" to DocumentRoot "/usr/share/webapps/owncloud" )

*   More Apps for ownCloud can be found [here](http://apps.owncloud.com/)

*   To install an new application, download the zip from the apps store, extract it into /srv/http/owncloud/apps/.

Afterwards restart httpd:

```
# systemctl restart httpd

```

log into your server go to the app sections you should see the new apps in there,

*   If you are protecting access to your ownCloud location with HTTP basic auth, the file "status.php" must be excluded from auth and be publicly accessible. [[2]](https://github.com/owncloud/mirall/issues/734)

### SABnzbd

When using [SABnzbd](/index.php/SABnzbd "SABnzbd"), you might want to set

```
folder_rename 0

```

in your sabnzbd.ini file, because ownCloud will scan the files as soon as they get uploaded, preventing SABnzbd from removing UNPACKING prefixes etc.

## Troubleshooting

### Self-signed certificate not accepted

ownCloud uses [Wikipedia:cURL](https://en.wikipedia.org/wiki/cURL "wikipedia:cURL") and [Wikipedia:SabreDAV](https://en.wikipedia.org/wiki/SabreDAV "wikipedia:SabreDAV") to check if WebDAV is enabled. If you use SSL/TLS with a self-signed certificate, e.g. as shown in [LAMP](/index.php/LAMP "LAMP"), and access ownCloud's admin panel, you will see the following error message:

```
Your web server is not yet properly setup to allow files synchronization because the WebDAV interface seems to be broken.

```

Assuming that you followed the [LAMP](/index.php/LAMP "LAMP") tutorial, execute the following steps:

Create a local directory for non-distribution certificates and copy [LAMPs](/index.php/LAMP "LAMP") certificate there. This will prevent `ca-certificates`-updates from overwriting it.

```
# cp /etc/httpd/conf/server.crt /usr/share/ca-certificates/*WWW.EXAMPLE.COM.crt*

```

Add *WWW.EXAMPLE.COM.crt* to `/etc/ca-certificates.conf`:

```
*WWW.EXAMPLE.COM.crt*

```

Now, regenerate your certificate store:

```
# update-ca-certificates

```

Restart the httpd service to activate your certificate.

Should this not work, consider disabling `mod_curl` in `/etc/php/php.ini`.

### Self-signed certificate for Android devices

Once you have followed the setup for SSL, as on [LAMP](/index.php/LAMP#TLS.2FSSL "LAMP") for example, early versions of DAVdroid will reject the connection because the certificate is not trusted. A certificate can be made as follows on your server:

```
 # openssl x509 -req -days 365 -in /etc/httpd/conf/server.csr -signkey /etc/httpd/conf/server.key -extfile android.txt -out CA.crt
 # openssl x509 -inform PEM -outform DER -in CA.crt -out CA.der.crt 

```

The file `android.txt` should contain the following:

```
 basicConstraints=CA:true

```

Then import `CA.der.crt` to your Android device:

Put the `CA.der.crt` file onto the sdcard of your Android device (usually to the internal one, e.g. save from a mail attachment). It should be in the root directory. Go to *Settings > Security > Credential storage* and select *Install from device storage*. The `.crt` file will be detected and you will be prompted to enter a certificate name. After importing the certificate, you will find it in *Settings > Security > Credential storage > Trusted credentials > User*.

Thanks to: [[3]](http://www.leftbrainthings.com/2013/10/13/creating-and-importing-self-signed-certificate-to-android-device/)

Another way is to import the certificate directly from your server via [CAdroid](https://play.google.com/store/apps/details?id=at.bitfire.cadroid) and follow the instructions there.

### Cannot write into config directory!

Check your httpd configuration file (like `owncloud.conf`). Add your configuration directory (`/etc/webapps` by default) to

```
php_admin_value open_basedir "/srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/:/path/to/dir/"

```

Restart the httpd or php-fpm service to activate the change.

### Cannot create data directory (/path/to/dir)

Check your httpd configuration file (like `owncloud.conf`). Add your data directory to

```
php_admin_value open_basedir "/srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/:/path/to/dir/"

```

Restart the httpd or php-fpm service to activate the change.

### CSync failed to find a specific file.

This is most likely a certificate issue. Recreate it, and do not leave the common name empty or you will see the error again.

```
# openssl req -new -x509 -nodes -newkey rsa:4096 -keyout server.key -out server.crt

```

### Seeing white page after login

The cause is probably a new app that you installed. To fix that, you can use the occ command as described [here](https://doc.owncloud.org/server/8.2/admin_manual/configuration_server/occ_command.html). So with

```
sudo -u http php /usr/share/webapps/owncloud/occ app:list

```

you can list all apps (if you installed owncloud in the standard directory), and with

```
sudo -u http php /usr/share/webapps/owncloud/occ app:disable <nameOfExtension>

```

you can disable the troubling app.

Alternatively, you can either use [phpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin") to edit the `oc_appconfig` table (if you got lucky and the table has an edit option), or do it by hand with mysql:

```
mysql -u root -p owncloud
MariaDB [owncloud]> **delete from** oc_appconfig **where** appid='<nameOfExtension>' **and** configkey='enabled' **and** configvalue='yes';
MariaDB [owncloud]> **insert into** oc_appconfig (appid,configkey,configvalue) **values** ('<nameOfExtension>','enabled','no');

```

This should delete the relevant configuration from the table and add it again.

### GUI sync client fails to connect

If using HTTP basic authentication, make sure to exclude "status.php", which must be publicly accessible. [[4]](https://github.com/owncloud/mirall/issues/734)

### Some files upload, but give an error 'Integrity constraint violation...'

You may see the following error in the ownCloud sync client:

```
   SQLSTATE[23000]: Integrity constraint violation: ... Duplicate entry '...' for key 'fs_storage_path_hash')...

```

This is caused by an issue with the File Locking app, which is often not sufficient to keep conflicts from occurring on some webserver configurations. A more complete [Transactional File Locking](https://doc.owncloud.org/server/8.1/admin_manual/configuration_files/files_locking_transactional.html) is available that rids these errors, but you must be using the Redis php-caching method. Install [redis](https://www.archlinux.org/packages/?name=redis) and [php-redis](https://aur.archlinux.org/packages/php-redis/), comment out your current php-cache mechanism, and then in `/etc/php/conf.d/redis.ini` uncomment `extension=redis.so`. Then in `config.php` make the following changes:

```
   'memcache.local' => '\OC\Memcache\Redis',
   'filelocking.enabled' => 'true',
   'memcache.locking' => '\OC\Memcache\Redis',
   'redis' => array(
        'host' => 'localhost',
        'port' => 6379,
        'timeout' => 0.0,
         ),

```

and start Redis:

```
   systemctl enable redis.service
   systemctl start redis.service

```

Finally, disable the File Locking App, as the Transational File Locking will take care of it (and would conflict).

If everything is working, you should see 'Transactional File Locking Enabled' under Server Status on the Admin page, and syncs should no longer cause issues.

### "Cannot write into apps directory"

As mentioned in the [official admin manual](http://doc.owncloud.org/server/6.0/admin_manual/configuration/configuration_apps.html), either you need an apps directory that is writable by the http user, or you need to set `appstoreenabled` to `false`.

*Also*, not mentioned there, the directory needs to be in the `open_basedir` line in `/etc/php/php.ini`.

One clean method is to have the package-installed directory at `/usr/share/webapps/owncloud/apps` stay owned by root, and have the user-installed apps go into e.g. `/var/www/owncloud/apps`, which is owned by http. Then you can set `appstoreenabled` to `true` and package upgrades of apps should work fine as well. Relevant lines from `/etc/webapps/owncloud/config/config.php`:

```
  'apps_paths' => 
  array (
    0 => 
    array (
      'path' => '/usr/share/webapps/owncloud/apps',
      'url' => '/apps',
      'writable' => false,
    ),
    1 => 
    array (
      'path' => '/var/www/owncloud/apps',
      'url' => '/wapps',
      'writable' => true,
    ),
  ),

```

Example `open_basedir` line from `/etc/php/php.ini` (you might have other directories in there as well):

```
open_basedir = /srv/http/:/usr/share/webapps/:/var/www/owncloud/apps/

```

Directory permissions:

 `$ ls -ld /usr/share/webapps/owncloud/apps /var/www/owncloud/apps/` 
```
 drwxr-xr-x 26 root root 4096 des.  14 20:48 /usr/share/webapps/owncloud/apps
 drwxr-xr-x  2 http http   48 jan.  20 20:01 /var/www/owncloud/apps/
```

### Security warnings even though the recommended settings have been included in nginx.conf

At the top of the admin page there might be a warning to set the `Strict-Transport-Security`, `X-Content-Type-Options`, `X-Frame-Options`, `X-XSS-Protection` and `X-Robots-Tag` according to [https://doc.owncloud.org/server/8.1/admin_manual/configuration_server/harden_server.html](https://doc.owncloud.org/server/8.1/admin_manual/configuration_server/harden_server.html) even though they are already set like that.

A possible cause could be that because owncloud sets those settings, uwsgi passed them along and nginx added them again:

 `$ curl -I [https://domain.tld](https://domain.tld)` 
```
...
X-XSS-Protection: 1; mode=block
X-Content-Type-Options: nosniff
X-Frame-Options: Sameorigin
X-Robots-Tag: none
Strict-Transport-Security: max-age=15768000; includeSubDomains; preload;
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
X-Robots-Tag: none
```

While the fast_cgi sample config has a parameter to avoid that ( `fastcgi_param modHeadersAvailable true; #Avoid sending the security headers twice` ), when using uwsgi and nginx the following modification of the uwsgi part in nginx.conf could help:

 ` /etc/nginx/nginx.conf` 
```
...
        # pass all .php or .php/path urls to uWSGI
        location ~ ^(.+\.php)(.*)$ {
            include uwsgi_params;
            uwsgi_modifier1 14;
            # hode following headers received from uwsgi, because otherwise we would send them twice since we already add them in nginx itself
            uwsgi_hide_header X-Frame-Options;
            uwsgi_hide_header X-XSS-Protection;
            uwsgi_hide_header X-Content-Type-Options;
            uwsgi_hide_header X-Robots-Tag;
            uwsgi_hide_header X-Frame-Options;
            #Uncomment line below if you get connection refused error. Remember to commet out line with "uwsgi_pass 127.0.0.1:3001;" below
            uwsgi_pass unix:/run/uwsgi/owncloud.sock;
            #uwsgi_pass 127.0.0.1:3001;
        }
...
```

### Password not saved

If the password are not saved and asked on every startup try to install [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring), helped under xfce4.

## Upload and Share from File Manager

You can use the following script to quickly upload and share files to your ownCloud installation from Thunar (and possibly other filemanagers): [https://github.com/schiesbn/shareLinkCreator](https://github.com/schiesbn/shareLinkCreator) You need to edit the file with the proper configuration settings. **Note: password is stored as plain text.**

## See also

*   [ownCloud official website](http://owncloud.org/)
*   [ownCloud 8.2 Admin Documentation](http://doc.owncloud.org/server/8.2/admin_manual/)