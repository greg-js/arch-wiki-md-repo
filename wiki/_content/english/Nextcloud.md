Related articles

*   [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server")
*   [Nginx](/index.php/Nginx "Nginx")
*   [OpenSSL](/index.php/OpenSSL "OpenSSL")
*   [WebDAV](/index.php/WebDAV "WebDAV")

From [Wikipedia:Nextcloud](https://en.wikipedia.org/wiki/Nextcloud "wikipedia:Nextcloud"):

	Nextcloud is a suite of client-server software for creating and using file hosting services. It is functionally similar to Dropbox, although Nextcloud is free and open-source, allowing anyone to install and operate it on a private server. In contrast to proprietary services like Dropbox, the open architecture allows adding additional functionality to the server in form of applications.

Nextcloud is a fork of ownCloud. For differences between the two, see [wikipedia:Nextcloud#Differences to ownCloud](https://en.wikipedia.org/wiki/Nextcloud#Differences_to_ownCloud "wikipedia:Nextcloud").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Prerequisites](#Prerequisites)
*   [2 Installation](#Installation)
    *   [2.1 Pacman hook](#Pacman_hook)
*   [3 Setup](#Setup)
    *   [3.1 PHP setup](#PHP_setup)
    *   [3.2 Database setup](#Database_setup)
        *   [3.2.1 MariaDB](#MariaDB)
        *   [3.2.2 PostgreSQL](#PostgreSQL)
    *   [3.3 Web server setup](#Web_server_setup)
        *   [3.3.1 Apache](#Apache)
            *   [3.3.1.1 WebDAV](#WebDAV)
        *   [3.3.2 Nginx](#Nginx)
        *   [3.3.3 lighttpd](#lighttpd)
    *   [3.4 Create data storage directory](#Create_data_storage_directory)
    *   [3.5 Fix apps directory permissions](#Fix_apps_directory_permissions)
*   [4 Initialize](#Initialize)
    *   [4.1 Configure caching](#Configure_caching)
*   [5 Security Hardening](#Security_Hardening)
    *   [5.1 uWSGI](#uWSGI)
        *   [5.1.1 Activation](#Activation)
    *   [5.2 Setting strong permissions for the filesystem](#Setting_strong_permissions_for_the_filesystem)
*   [6 Synchronization](#Synchronization)
    *   [6.1 Desktop](#Desktop)
        *   [6.1.1 Calendar](#Calendar)
        *   [6.1.2 Contacts](#Contacts)
        *   [6.1.3 Mounting files with davfs2](#Mounting_files_with_davfs2)
    *   [6.2 Mounting files in GNOME Files (Nautilus)](#Mounting_files_in_GNOME_Files_(Nautilus))
    *   [6.3 Android](#Android)
    *   [6.4 iOS](#iOS)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Environment variables not available](#Environment_variables_not_available)
    *   [7.2 Self-signed certificate not accepted](#Self-signed_certificate_not_accepted)
    *   [7.3 Self-signed certificate for Android devices](#Self-signed_certificate_for_Android_devices)
    *   [7.4 Cannot write into config directory!](#Cannot_write_into_config_directory!)
    *   [7.5 Cannot create data directory](#Cannot_create_data_directory)
    *   [7.6 CSync failed to find a specific file.](#CSync_failed_to_find_a_specific_file.)
    *   [7.7 Seeing white page after login](#Seeing_white_page_after_login)
    *   [7.8 GUI sync client fails to connect](#GUI_sync_client_fails_to_connect)
    *   [7.9 GUI tray icon disappears, but client still running in the background](#GUI_tray_icon_disappears,_but_client_still_running_in_the_background)
    *   [7.10 Some files upload, but give an error 'Integrity constraint violation...'](#Some_files_upload,_but_give_an_error_'Integrity_constraint_violation...')
    *   [7.11 "Cannot write into apps directory"](#"Cannot_write_into_apps_directory")
    *   [7.12 Installed apps get blocked because of MIME type error](#Installed_apps_get_blocked_because_of_MIME_type_error)
    *   [7.13 Security warnings even though the recommended settings have been included in nginx.conf](#Security_warnings_even_though_the_recommended_settings_have_been_included_in_nginx.conf)
    *   [7.14 "Reading from keychain failed with error: 'No keychain service available'"](#"Reading_from_keychain_failed_with_error:_'No_keychain_service_available'")
    *   [7.15 FolderSync: "Method Not Allowed"](#FolderSync:_"Method_Not_Allowed")
*   [8 Tips and tricks](#Tips_and_tricks)
    *   [8.1 Running NextCloud in a subdirectory](#Running_NextCloud_in_a_subdirectory)
    *   [8.2 Docker](#Docker)
    *   [8.3 Upload and share from File Manager](#Upload_and_share_from_File_Manager)
    *   [8.4 Defining Background Jobs](#Defining_Background_Jobs)
        *   [8.4.1 Manual install](#Manual_install)
        *   [8.4.2 Activate timer](#Activate_timer)
        *   [8.4.3 AUR package](#AUR_package)
    *   [8.5 Collabora Online Office integration](#Collabora_Online_Office_integration)
*   [9 See also](#See_also)

## Prerequisites

Nextcloud requires several components:[[1]](https://docs.nextcloud.com/server/latest/admin_manual/installation/system_requirements.html#server)

*   A web server: [Apache](/index.php/Apache "Apache") or [nginx](/index.php/Nginx "Nginx")
*   A database: [MariaDB](/index.php/MariaDB "MariaDB")/MySQL, [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), [SQLite](/index.php/SQLite "SQLite") or [Oracle](/index.php/Oracle "Oracle")
*   [PHP](/index.php/PHP "PHP") with [additional modules](#PHP_setup)

These will be configured in [#Setup](#Setup).

Make sure the required components are installed before proceeding.

## Installation

[Install](/index.php/Install "Install") the [nextcloud](https://www.archlinux.org/packages/?name=nextcloud) package.

### Pacman hook

To upgrade the Nextcloud database automatically on updates, you may want to create a [pacman hook](/index.php/Pacman_hook "Pacman hook"):

 `/etc/pacman.d/hooks/nextcloud.hook` 
```
[Trigger]
Operation = Install
Operation = Upgrade
Type = Package
Target = nextcloud
Target = nextcloud-app-*

[Action]
Description = Update Nextcloud installation
When = PostTransaction
Exec = /usr/bin/runuser -u http -- /usr/bin/php /usr/share/webapps/nextcloud/occ upgrade
```

## Setup

As stated above, in order to setup Nextcloud, you must set up the appropriate PHP requirements; additionally, you must configure a database and a webserver.

### PHP setup

**Tip:** For all prerequisite PHP modules, see [upstream documentation](https://docs.nextcloud.com/server/latest/admin_manual/installation/source_installation.html#prerequisites-label).

Install [PHP#gd](/index.php/PHP#gd "PHP") and [php-intl](https://www.archlinux.org/packages/?name=php-intl) as additional modules. Configure [OPcache](/index.php/PHP#OPCache "PHP") as recommended by [the documentation](https://docs.nextcloud.com/server/latest/admin_manual/installation/server_tuning.html#enable-php-opcache).

Some apps (*News* for example) require the `iconv` extension, if you wish to use these apps, uncomment the extension in `/etc/php/php.ini`.

Depending on which database backend will be used:

*   For [MySQL](/index.php/MySQL "MySQL"), see [PHP#MySQL/MariaDB](/index.php/PHP#MySQL/MariaDB "PHP").
*   For [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), see [PHP#PostgreSQL](/index.php/PHP#PostgreSQL "PHP").
*   For [SQLite](/index.php/SQLite "SQLite"), see [PHP#Sqlite](/index.php/PHP#Sqlite "PHP").

Performance may be improved through the implementation of [caching](/index.php/PHP#Caching "PHP"), see [Configuring Memory Caching](https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/caching_configuration.html) on the official documentation for details.

### Database setup

An SQL database must be setup and used for your Nextcloud installation. After setting up the database here, you will be prompted for its information when you first create an administrator account.

#### MariaDB

It is recommended to set up an own database and user when using [MariaDB](/index.php/MariaDB "MariaDB"):

 `$ mysql -u root -p` 
```
mysql> CREATE DATABASE **nextcloud** DEFAULT CHARACTER SET 'utf8' COLLATE 'utf8_unicode_ci';
mysql> GRANT ALL PRIVILEGES ON **nextcloud**.* TO '**nextcloud'**@'localhost' IDENTIFIED BY '**password'**;
mysql> FLUSH PRIVILEGES;
mysql> \q
```

**Note:** Create or convert the database with MySQL 4-byte support in order to use Emojis (textbased smilies) on your Nextcloud server [[2]](https://docs.nextcloud.com/server/latest/admin_manual/configuration_database/mysql_4byte_support.html).

#### PostgreSQL

The following is an example of setting up a [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") user and database:

 `[postgres]$ createuser -h localhost -P nextcloud` 
```
Enter password for new role:
Enter it again:
```

```
[postgres]$ createdb -O nextcloud nextcloud

```

### Web server setup

**Warning:** It is recommended to use HTTPS instead of plain HTTP, see [Apache#TLS](/index.php/Apache#TLS "Apache") or [Nginx#TLS](/index.php/Nginx#TLS "Nginx") for examples and implement this in the examples given below.

Depending on which [web server](/index.php/Web_server "Web server") you are using, further setup is required, indicated below.

#### Apache

If you have not already, install [Apache](/index.php/Apache "Apache") and install and enable [Apache's PHP module](/index.php/Apache#PHP "Apache")

Copy the Apache configuration file to the configuration directory:

```
# cp /etc/webapps/nextcloud/apache.example.conf /etc/httpd/conf/extra/nextcloud.conf

```

Modify the file according to your preferences. By default it includes an alias for `/nextcloud` pointing to `/usr/share/webapps/nextcloud`.

And include it in `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/nextcloud.conf

```

Ensure that the root location of your Nextcloud installation (e.g., `/usr/share/webapps/nextcloud`) is accessible by the webserver's user `http`.

Now restart Apache (`httpd.service`).

##### WebDAV

Nextcloud comes with its own [WebDAV](/index.php/WebDAV "WebDAV") implementation enabled, which may conflict with the one shipped with Apache. If you have enabled WebDAV in Apache (not enabled by default), disable the modules `mod_dav` and `mod_dav_fs` in `/etc/httpd/conf/httpd.conf`. See [[3]](https://forum.owncloud.org/viewtopic.php?f=17&t=7240) for details.

#### Nginx

Make sure PHP-FPM has been configured correctly as described in [Nginx#FastCGI](/index.php/Nginx#FastCGI "Nginx"). Uncomment `env[PATH]` in `/etc/php/php-fpm.d/www.conf` as it is required by Nextcloud.

Create a [server block](/index.php/Nginx#Server_blocks "Nginx") and add the content according to the [Nextcloud documentation](https://docs.nextcloud.com/server/latest/admin_manual/installation/nginx.html):

**Note:** Use `/usr/share/webapps/nextcloud` as `root` location when using [nextcloud](https://www.archlinux.org/packages/?name=nextcloud).

**Tip:** See the [following template](https://github.com/graysky2/configs/blob/master/nginx/nextcloud-initial.conf) as initial configuration when setting up [Let's Encrypt](/index.php/Let%27s_Encrypt "Let's Encrypt").
 `/etc/nginx/sites-available/owncloud.conf` 
```
upstream php-handler {
    server unix:/run/php-fpm/php-fpm.sock;
}

server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name cloud.example.com;

    ssl_certificate /etc/ssl/nginx/cloud.example.com.crt;
    ssl_certificate_key /etc/ssl/nginx/cloud.example.com.key;

    ..

    # Path to the root of your installation
    root /usr/share/webapps/nextcloud/;

    ..

    location ~ ^/(?:index|remote|public|cron|core/ajax/update|status|ocs/v[12]|updater/.+|ocs-provider/.+)\.php(?:$|/) {
        fastcgi_split_path_info ^(.+\.php)(/.*)$;
        try_files $fastcgi_script_name =404;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
        fastcgi_param HTTPS on;
        #Avoid sending the security headers twice
        fastcgi_param modHeadersAvailable true;
        fastcgi_param front_controller_active true;
        fastcgi_pass php-handler;
        fastcgi_intercept_errors on;
        fastcgi_request_buffering off;
    }
}

```

#### lighttpd

Enable [lighttpd#FastCGI](/index.php/Lighttpd#FastCGI "Lighttpd"), e.g. by adding `server.modules += ( "mod_fastcgi" )` to `/etc/lighttpd/lighttpd.conf`.

Create a link to `/usr/share/webapps/nextcloud` in your `/srv/http/` directory (or configured root).

### Create data storage directory

Nextcloud needs a directory to store all user files, which has to be writable for the web server. It is recommended to put this directory somewhere outside of `/usr`, e.g. `/var/nextcloud`.

**Note:** Replace `http` when using a different [user](/index.php/User "User")/[user group](/index.php/User_group "User group") for the web server.

```
# mkdir /var/nextcloud
# chown http:http /var/nextcloud
# chmod 750 /var/nextcloud

```

### Fix apps directory permissions

To give the web server read/write access to the *apps* directory (e.g. on "Cannot write into "apps" directory"), setup the correct permissions:

**Note:** Replace `http` when using a different [user](/index.php/User "User")/[user group](/index.php/User_group "User group") for the web server.

```
# chown -R http:http /usr/share/webapps/nextcloud/apps
# chmod 750 /usr/share/webapps/nextcloud/apps

```

## Initialize

Open the address where you have installed Nextcloud in a web browser (e.g., [https://www.example.com/nextcloud](https://www.example.com/nextcloud)). Enter the database details and the location of the data directory (e.g. `/var/nextcloud`) set up above.

If you get the error message "Cannot write into "apps" directory", make sure you followed [#Fix apps directory permissions](#Fix_apps_directory_permissions) above.

### Configure caching

It is recommended to [enable caching](https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/caching_configuration.html). The Nextcloud documentation provides instructions on [Redis](/index.php/Redis "Redis"), Memcached and [APCu](/index.php/PHP#APCu "PHP").

## Security Hardening

See the [Nextcloud documentation](https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/harden_server.html) and [Security](/index.php/Security "Security"). Nextcloud additionally provides a [Security scanner](https://scan.nextcloud.com/).

### uWSGI

You can run Nextcloud in its own process and service by using the [uWSGI](/index.php/UWSGI "UWSGI") application server with [uwsgi-plugin-php](https://www.archlinux.org/packages/?name=uwsgi-plugin-php). This allows you to define a [PHP configuration](/index.php/PHP#Configuration "PHP") only for this instance of PHP, without the need to edit the global `php.ini` and thus keeping your web application configurations compartmentalized. *uWSGI* itself has a wealth of features to limit the resource use and to harden the security of the application, and by being a separate process it can run under its own user.

The only part that differs from [#Nginx](#Nginx) is the `location ~ \.php(?:$|/) {}` block:

```
  location ~ \.php(?:$|/) {
    include uwsgi_params;
    uwsgi_modifier1 14;
    # Avoid duplicate headers confusing OC checks
    uwsgi_hide_header X-Frame-Options;
    uwsgi_hide_header X-XSS-Protection;
    uwsgi_hide_header X-Content-Type-Options;
    uwsgi_hide_header X-Robots-Tag;
    uwsgi_pass unix:/run/uwsgi/nextcloud.sock;
    }

```

Then create a config file for *uWSGI*:

 `/etc/uwsgi/nextcloud.ini` 
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
;php-set = open_basedir=/tmp/:/usr/share/webapps/nextcloud:/etc/webapps/nextcloud:/dev/urandom
php-set = expose_php=false
; avoid security risk of leaving sessions in world-readable /tmp
php-set = session.save_path=/usr/share/webapps/nextcloud/data

; port of php directives set upstream in /usr/share/webapps/nextcloud/.user.ini for use with PHP-FPM
php-set = upload_max_filesize=513M
php-set = post_max_size=513M
php-set = memory_limit=512M
php-set = output_buffering=off

; load all extensions only in this instance of php, no need to edit global php.ini
;; required core modules
php-set = extension=gd
php-set = extension=iconv
;php-set = extension=zip     # enabled by default in global php.ini

;; database connectors
;; uncomment your selected driver
;php-set = extension=pdo_sqlite
;php-set = extension=pdo_mysql
;php-set = extension=pdo_pgsql

;; recommended extensions
;php-set = extension=curl    # enabled by default in global php.ini
php-set = extension=bz2
php-set = extension=intl

;; required for specific apps
;php-set = extension=ldap    # for LDAP integration
;php-set = extension=ftp     # for FTP storage / external user authentication
;php-set = extension=imap    # for external user authentication, requires php-imap

;; recommended for specific apps
;php-set = extension=exif    # for image rotation in pictures app, requires exiv2
;php-set = extension=gmp     # for SFTP storage

;; for preview generation
;; provided by packages in AUR
; php-set = extension=imagick

; opcache
php-set = zend_extension=opcache

; user cache
; provided by php-acpu, to be enabled **either** here **or** in /etc/php/conf.d/apcu.ini
php-set = extension=apcu
; per https://github.com/krakjoe/apcu/blob/simplify/INSTALL
php-set = apc.ttl=7200
php-set = apc.enable_cli=1

; web server is already handling URL rewriting, so tell NextCloud not to repeat this
env = front_controller_active=true

cron2 = minute=-15,unique=1 /usr/bin/php -f /usr/share/webapps/nextcloud/cron.php 1>/dev/null

```

**Note:** * Do not forget to set your timezone and uncomment the required database connector in the uWSGI config file

*   The [open_basedir](/index.php/PHP#Configuration "PHP") directive is optional and commented out. You can uncomment to harden security. Be aware that it may [occasionally break things](https://github.com/owncloud/core/search?q=open_basedir&type=Issues).
*   Use `php-docroot = /usr/share/webapps` if placing nextcloud in /nextcloud subdirectory.

**Warning:** The way the [Nextcloud background job](https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/background_jobs_configuration.html) is currently set up with [uWSGI cron](https://uwsgi-docs.readthedocs.org/en/latest/Cron.html) will make use of the default global configuration from `/etc/php/php.ini`. This means that none of the specific parameters defined (e.g. required modules) will be enabled, [leading to various issues](https://github.com/owncloud/core/issues/12678#issuecomment-66114448). One solution is to copy `/etc/php/php.ini` to e.g. `/etc/uwsgi/cron-php.ini`, make the required modifications there (mirroring `/etc/uwsgi/nextcloud.ini` parameters) and referencing it in the cron directive by adding the `-c /etc/uwsgi/cron-php.ini` option to *php* invocation.

#### Activation

[uWSGI](/index.php/UWSGI "UWSGI") provides a [template unit](/index.php/Systemd#Using_units "Systemd") that allows to start and enable application using their configuration file name as instance identifier. For example, [starting](/index.php/Start "Start") `uwsgi@nextcloud.socket` would start it on demand referencing the configuration file `/etc/uwsgi/nextcloud.ini`.

To enable the uwsgi service by default at start-up, [enable](/index.php/Enable "Enable") `uwsgi@nextcloud.socket`.

**Note:** Here we make use of [systemd socket activation](http://0pointer.de/blog/projects/socket-activation.html) to prevent unnecessary resources consumption when no connections are made to the instance. If you would rather have it constantly active, simply remove the `.socket` part to start and enable the service instead.

See also [UWSGI#Running uWSGI](/index.php/UWSGI#Running_uWSGI "UWSGI").

### Setting strong permissions for the filesystem

You should set the permissions for `config/`, `data/` and `apps/` as strict possible. That means that your HTTP user (*http* in case of [apache](https://www.archlinux.org/packages/?name=apache)) should own them, and the should have `700` permissions. You can use the following script to achieve this.

 `oc-perms` 
```
#!/bin/bash
ocpath='/usr/share/webapps/nextcloud'
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
chown -R ${htuser}:${htgroup} ${ocpath}/assets/
chown -R ${htuser}:${htgroup} ${ocpath}/config/
chown -R ${htuser}:${htgroup} ${ocpath}/data/
chown -R ${htuser}:${htgroup} ${ocpath}/themes/
chown -R ${htuser}:${htgroup} ${ocpath}/updater/

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

If you have customized your Nextcloud installation and your filepaths are different than the standard installation, then modify this script accordingly.

## Synchronization

### Desktop

The official client can be installed with the [owncloud-client](https://www.archlinux.org/packages/?name=owncloud-client) or [nextcloud-client](https://www.archlinux.org/packages/?name=nextcloud-client) package. Alternative versions are available in the [AUR](/index.php/AUR "AUR"): [owncloud-client-git](https://aur.archlinux.org/packages/owncloud-client-git/).

#### Calendar

To access your Nextcloud calendars using Mozilla [Thunderbird](/index.php/Thunderbird "Thunderbird")'s Lightning calendar you would use the following URL:

```
https://ADDRESS/remote.php/caldav/calendars/USERNAME/CALENDARNAME

```

To access your Nextcloud calendars using CalDAV-compatible programs like Kontact or [Evolution](/index.php/Evolution "Evolution"), you would use the following URL:

```
https://ADDRESS/remote.php/caldav

```

For details see the [official documentation](https://docs.nextcloud.com/server/latest/user_manual/pim/index.html).

#### Contacts

To sync contacts with [Thunderbird](/index.php/Thunderbird "Thunderbird"), see [these instructions](https://docs.nextcloud.com/server/latest/user_manual/pim/sync_thunderbird.html) from the official doc.

#### Mounting files with davfs2

If you want to mount your ownCloud permanently install [davfs2](https://www.archlinux.org/packages/?name=davfs2) (as described in [davfs2](/index.php/Davfs2 "Davfs2")) first.

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

**Tip:** In order to allow automount you can also store your username (and password if you like) in a file as described in [davfs2#Storing credentials](/index.php/Davfs2#Storing_credentials "Davfs2").

**Note:** If creating/copying files is not possible, while the same operations work on directories, see [davfs2#Creating/copying files not possible and/or freezes](/index.php/Davfs2#Creating/copying_files_not_possible_and/or_freezes "Davfs2").

### Mounting files in GNOME Files (Nautilus)

You can access the files directly in Nautilus ('+ Other Locations') through WebDAV protocol - use the link as shown in your Nextcloud installation Web GUI (typically: [https://example.org/remote.php/webdav/](https://example.org/remote.php/webdav/)) but replace the protocol name from 'https' to 'davs'. Nautilus will ask for user name and password when trying to connect.

### Android

Download the official Nextcloud app from [Google Play](https://play.google.com/store/apps/details?id=com.nextcloud.client) or [F-Droid](https://f-droid.org/packages/com.nextcloud.client/).

To enable contacts and calendar sync (Android 4+):

1.  download [DAVx](https://www.davx5.com/) ([Play Store](https://play.google.com/store/apps/details?id=at.bitfire.davdroid), [F-Droid](https://f-droid.org/app/at.bitfire.davdroid))
2.  Enable mod_rewrite.so in httpd.conf
3.  create a new DAVdroid account in the *Account* settings, and specify your "short" server address and login/password couple, e.g. `https://cloud.example.com` (there is no need for the `/remote.php/{carddav,webdav}` part if you configured your web server with the proper redirections, as illustrated previously in the article; *DAVdroid* will find itself the right URLs)

### iOS

Download the official Nextcloud app from the [App Store](https://itunes.apple.com/us/app/nextcloud/id1125420102).

## Troubleshooting

### Environment variables not available

Uncomment the line in `/etc/php/php-fpm.d/www.conf` as per [Nextcloud documentation](https://docs.nextcloud.com/server/latest/admin_manual/installation/source_installation.html#php-fpm-tips-label):

```
 env[PATH] = /usr/local/bin:/usr/bin:/bin

```

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

### Self-signed certificate for Android devices

Once you have followed the setup for SSL, as on [Apache HTTP Server#TLS](/index.php/Apache_HTTP_Server#TLS "Apache HTTP Server") for example, early versions of DAVdroid will reject the connection because the certificate is not trusted. A certificate can be made as follows on your server:

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

Thanks to: [[4]](http://www.leftbrainthings.com/2013/10/13/creating-and-importing-self-signed-certificate-to-android-device/)

Another way is to import the certificate directly from your server via [CAdroid](https://play.google.com/store/apps/details?id=at.bitfire.cadroid) and follow the instructions there.

### Cannot write into config directory!

If you have set `open_basedir` in your PHP/web server configuration file (e.g. `/etc/httpd/conf/extra/nextcloud.conf`), make sure that it includes `/etc/webapps`.

Restart the web server to apply the change.

### Cannot create data directory

If you have set `open_basedir` in your PHP/web server configuration file (e.g. `/etc/httpd/conf/extra/nextcloud.conf`), make sure that it includes the data directory.

Restart the web server to apply the change.

### CSync failed to find a specific file.

This is most likely a certificate issue. Recreate it, and do not leave the common name empty or you will see the error again.

```
# openssl req -new -x509 -nodes -newkey rsa:4096 -keyout server.key -out server.crt

```

### Seeing white page after login

The cause is probably a new app that you installed. To fix that, you can use the occ command as described [here](https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/occ_command.html). So with

```
sudo -u http php /usr/share/webapps/nextcloud/occ app:list

```

you can list all apps (if you installed nextcloud in the standard directory), and with

```
sudo -u http php /usr/share/webapps/nextcloud/occ app:disable <nameOfExtension>

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

If using HTTP basic authentication, make sure to exclude "status.php", which must be publicly accessible. [[5]](https://github.com/owncloud/mirall/issues/734)

### GUI tray icon disappears, but client still running in the background

After waking up from a suspended state, the Nextcloud client tray icon may disappear from the system tray. A workaround is to delay the startup of the client, as noted [here](https://github.com/nextcloud/desktop/issues/203#issuecomment-463957811). This can be done with the .desktop file, for example:

 `.local/share/applications/nextcloud.desktop` 
```
...
Exec=bash -c 'sleep 5 && nextcloud'
...

```

### Some files upload, but give an error 'Integrity constraint violation...'

You may see the following error in the ownCloud sync client:

```
   SQLSTATE[23000]: Integrity constraint violation: ... Duplicate entry '...' for key 'fs_storage_path_hash')...

```

This is caused by an issue with the File Locking app, which is often not sufficient to keep conflicts from occurring on some webserver configurations. A more complete [Transactional File Locking](https://docs.nextcloud.com/server/latest/admin_manual/configuration_files/files_locking_transactional.html) is available that rids these errors, but you must be using the Redis php-caching method. Install [redis](https://www.archlinux.org/packages/?name=redis) and [php-redis](https://www.archlinux.org/packages/?name=php-redis), comment out your current php-cache mechanism, and then in `/etc/php/conf.d/redis.ini` uncomment `extension=redis`. Then in `config.php` make the following changes:

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

and [start/enable](/index.php/Start/enable "Start/enable") `redis.service`.

Finally, disable the File Locking App, as the Transational File Locking will take care of it (and would conflict).

If everything is working, you should see 'Transactional File Locking Enabled' under Server Status on the Admin page, and syncs should no longer cause issues.

### "Cannot write into apps directory"

As mentioned in the [official admin manual](https://docs.nextcloud.com/server/latest/admin_manual/apps_management.html), either you need an apps directory that is writable by the http user, or you need to set `appstoreenabled` to `false`.

If you have set `open_basedir` in your PHP/web server configuration file (e.g. `/etc/httpd/conf/extra/nextcloud.conf`), it may be necessary to add your */path/to/data* directory to the string on the line starting with `php_admin_value open_basedir` :

 `/etc/httpd/conf/extra/nextcloud.conf`  `php_admin_value open_basedir "*/path/to/data/*:/srv/http/:/dev/urandom:/tmp/:/usr/share/pear/:/usr/share/webapps/nextcloud/:/etc/webapps/nextcloud"` 

### Installed apps get blocked because of MIME type error

If you are putting your apps folder outside of the nextcloud installation directory make sure your webserver serves it properly.

In nginx this is accomplished by adding a location block to the nginx configuration as the folder will not be included in it by default.

```
location ~ /apps2/(.*)$ {
    alias /var/www/nextcloud/apps/$1;
}

```

### Security warnings even though the recommended settings have been included in nginx.conf

At the top of the admin page there might be a warning to set the `Strict-Transport-Security`, `X-Content-Type-Options`, `X-Frame-Options`, `X-XSS-Protection` and `X-Robots-Tag` according to [https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/harden_server.html](https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/harden_server.html) even though they are already set like that.

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

### "Reading from keychain failed with error: 'No keychain service available'"

Can be fixed for Gnome by installing the following 2 packages, [libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring) and [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring). Or the following for KDE, [libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring) and [qtkeychain](https://www.archlinux.org/packages/?name=qtkeychain).

### FolderSync: "Method Not Allowed"

FolderSync needs access to `/owncloud/remote.php/webdav`, so you could create another alias for owncloud in your `/etc/httpd/conf/extra/nextcloud.conf`

```
  <IfModule mod_alias.c>
    Alias /nextcloud /usr/share/webapps/nextcloud/
    Alias /owncloud /usr/share/webapps/nextcloud/
  </IfModule>

```

## Tips and tricks

### Running NextCloud in a subdirectory

By including the default `nextcloud.conf` in `httpd.conf`, nextCloud will take control of port 80 and your localhost domain.

If you would like to have nextCloud run in a subdirectory, then

For apache,edit the `/etc/httpd/conf/extra/nextcloud.conf` you included and comment out the `<VirtualHost *:80> ... </VirtualHost>` part of the include file.

For nginx, you can use the following config when using nextcloud with uwsgi:

 `/etc/nginx/conf.d/nextcloud.conf` 
```
location = /.well-known/carddav {
  return 301 $scheme://$host/nextcloud/remote.php/dav;
}

location = /.well-known/caldav {
  return 301 $scheme://$host/nextcloud/remote.php/dav;
}

location /.well-known/acme-challenge { }

location ^~ /nextcloud {

  root /usr/share/webapps;

  # set max upload size
  client_max_body_size 512M;
  fastcgi_buffers 64 4K;

  # Disable gzip to avoid the removal of the ETag header
  gzip off;

  # Uncomment if your server is build with the ngx_pagespeed module
  # This module is currently not supported.
  #pagespeed off;

  location /nextcloud {
    rewrite ^ /nextcloud/index.php$uri;
  }

  location ~ ^/nextcloud/(?:build|tests|config|lib|3rdparty|templates|data)/ {
    deny all;
  }

  location ~ ^/nextcloud/(?:\.|autotest|occ|issue|indie|db_|console) {
    deny all;
  }

  location ~ ^/nextcloud/(?:updater|ocs-provider)(?:$|/) {
    try_files $uri/ =404;
    index index.php;
  }

  location ~ ^/nextcloud/(?:index|remote|public|cron|core/ajax/update|status|ocs/v[12]|updater/.+|ocs-provider/.+|core/templates/40[34])\.php(?:$|/) {
    include uwsgi_params;
    uwsgi_modifier1 14;
    # Avoid duplicate headers confusing OC checks
    uwsgi_hide_header X-Frame-Options;
    uwsgi_hide_header X-XSS-Protection;
    uwsgi_hide_header X-Content-Type-Options;
    uwsgi_hide_header X-Robots-Tag;
    uwsgi_pass unix:/run/uwsgi/owncloud.sock;
  }

  # Adding the cache control header for js and css files
  # Make sure it is BELOW the PHP block
  location ~* \.(?:css|js) {
    try_files $uri /nextcloud/index.php$uri$is_args$args;
    add_header Cache-Control "public, max-age=7200";
    # Add headers to serve security related headers  (It is intended
    # to have those duplicated to the ones above)
    # Before enabling Strict-Transport-Security headers please read
    # into this topic first.
    # add_header Strict-Transport-Security "max-age=15768000;
    # includeSubDomains; preload;";
    add_header X-Content-Type-Options nosniff;
    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-XSS-Protection "1; mode=block";
    add_header X-Robots-Tag none;
    add_header X-Download-Options noopen;
    add_header X-Permitted-Cross-Domain-Policies none;
    # Optional: Do not log access to assets
    access_log off;
  }

  location ~* \.(?:svg|gif|png|html|ttf|woff|ico|jpg|jpeg) {
    try_files $uri /nextcloud/index.php$uri$is_args$args;
    # Optional: Do not log access to other assets
    access_log off;
  }
}

```

### Docker

See the [ownCloud](https://hub.docker.com/_/owncloud/) or [Nextcloud](https://github.com/nextcloud/docker) repository for [Docker](/index.php/Docker "Docker").

### Upload and share from File Manager

[shareLinkCreator](https://github.com/schiesbn/shareLinkCreator) provides the ability to upload a file to OwnCloud via a supported file manager and receive a link to the uploaded file which can then be emailed or shared in another way.

### Defining Background Jobs

Nextcloud requires scheduled execution of some tasks, and by default it achieves this by using AJAX, however AJAX is the least reliable method, and it is recommended to use [Cron](/index.php/Cron "Cron") instead. However, ArchLinux ships with [systemd](https://www.archlinux.org/packages/?name=systemd), so the preferred way of executing scheduled tasks is a [systemd timer](/index.php/Systemd#Timers "Systemd").

#### Manual install

First create a service:

 `/etc/systemd/system/nextcloudcron.service` 
```
[Unit]
Description=Nextcloud cron.php job

[Service]
User=http
ExecStart=/usr/bin/php -f /usr/share/webapps/nextcloud/cron.php

[Install]
WantedBy=basic.target

```

Then create a timer for that service:

 `/etc/systemd/system/nextcloudcron.timer` 
```
[Unit]
Description=Run Nextcloud cron.php every 15 minutes

[Timer]
OnBootSec=5min
OnUnitActiveSec=15min
Unit=nextcloudcron.service

[Install]
WantedBy=timers.target

```

#### Activate timer

[Start/enable](/index.php/Start/enable "Start/enable") `nextcloudcron.timer`.

Confirm that it is running by running

```
# systemctl list-timers

```

#### AUR package

Install [nextcloud-systemd-timers](https://aur.archlinux.org/packages/nextcloud-systemd-timers/).

Provided services can be checked with:

```
$ pacman -Ql nextcloud-systemd-timers

```

For instance, to run the `cron.php` script every 15 minutes:

```
# systemctl start nextcloud-cron.timer
# systemctl enable nextcloud-cron.timer

```

### Collabora Online Office integration

**Solution with Docker: *CODE backend using the official Docker image***

The first, install a [docker](https://www.archlinux.org/packages/?name=docker) package to provide collabora files and setup a Collabora server.

[Start/enable](/index.php/Start/enable "Start/enable") `docker.service`.

Then, download the required binares :

```
# docker pull collabora/code

```

And, installing a Collabora server. Make sure `cloud//.example//.com` is your nextcloud's domain, not a collabora :

```
# docker run -t -d -p 127.0.0.1:9980:9980 -e 'domain=cloud\\.example\\.com' --restart always --cap-add MKNOD collabora/code

```

Also make sure to escape all dots with double backslashes (\), since this string will be evaluated as a regular expression (and your bash 'eats' the first backslash.) If you want to use the docker container with more than one Nextcloud, you will need to use 'domain=cloud\\.example\\.com\|second\\.example\\.com' instead. (All hosts are separated by \|.) When using `localhost` as domain for testing you need to add `--net host` to ensure the docker container can access your Nextcloud server.

If you need to delete or reinstall Collabora server use:

For recognition CONTAINER_ID of server

```
# docker ps

```

Stop and delete

```
# docker stop CONTAINER_ID
# docker rm CONTAINER_ID

```

Futher, follow the instruction of webserver you are using:

**Nginx setup example:**

Add following to your nextcloud domain config or add new config file in /etc/nginx/conf.d/ directory, (Do not forget to change `office.example.com` and `ssl_certificate` to the right values. If you are using docker image, change `http` to `https`.)

 `/etc/nginx/conf.d/example.conf` 
```
 upstream office.example.com {
    server 127.0.0.1:9980;
}

server {
    listen 443 ssl;
    server_name office.example.com;

    ssl_certificate /etc/letsencrypt/live/office.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/office.example.com/privkey.pem;

    # static files
    location ^~ /loleaflet {
        proxy_pass http://127.0.0.1:9980;
        proxy_set_header Host $host;
    }

    # WOPI discovery URL
    location ^~ /hosting/discovery {
        proxy_pass http://127.0.0.1:9980;
        proxy_set_header Host $host;
    }

    # Main websocket
    location ~ /lool/(.*)/ws$ {
        proxy_pass http://127.0.0.1:9980;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";
        proxy_set_header Host $host;
        proxy_read_timeout 36000s;
    }

    # Admin Console websocket
    location ^~ /lool/adminws {
	proxy_buffering off;
        proxy_pass http://127.0.0.1:9980;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";
        proxy_set_header Host $host;
        proxy_read_timeout 36000s;
    }

    # download, presentation and image upload
    location ~ /lool {
        proxy_pass http://127.0.0.1:9980;
        proxy_set_header Host $host;
    }
}

```

Restart a nginx:

```
# nginx -s reload

```

or [restart](/index.php/Restart "Restart") `nginx.service`.

**Apache setup example:**

Add following to nextcloud config file. Do not forget to change to the right values

 `/etc/httpd/conf/extra/nextcloud.conf` 
```
<VirtualHost *:443>
ServerName office.nextcloud.com:443

# SSL configuration, you may want to take the easy route instead and use Lets Encrypt!
SSLEngine on
SSLCertificateFile /path/to/signed_certificate
SSLCertificateChainFile /path/to/intermediate_certificate
SSLCertificateKeyFile /path/to/private/key
SSLProtocol             all -SSLv2 -SSLv3
SSLCipherSuite ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES256-SHA:ECDHE-ECDSA-DES-CBC3-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:DES-CBC3-SHA:!DSS
SSLHonorCipherOrder     on

# Encoded slashes need to be allowed
AllowEncodedSlashes NoDecode

# Container uses a unique non-signed certificate
SSLProxyEngine On
SSLProxyVerify None
SSLProxyCheckPeerCN Off
SSLProxyCheckPeerName Off

# keep the host
ProxyPreserveHost On

# static html, js, images, etc. served from loolwsd
# loleaflet is the client part of LibreOffice Online
ProxyPass           /loleaflet https://127.0.0.1:9980/loleaflet retry=0
ProxyPassReverse    /loleaflet https://127.0.0.1:9980/loleaflet

# WOPI discovery URL
ProxyPass           /hosting/discovery https://127.0.0.1:9980/hosting/discovery retry=0
ProxyPassReverse    /hosting/discovery https://127.0.0.1:9980/hosting/discovery

# Main websocket
ProxyPassMatch "/lool/(.*)/ws$" wss://127.0.0.1:9980/lool/$1/ws nocanon

# Admin Console websocket
ProxyPass   /lool/adminws wss://127.0.0.1:9980/lool/adminws

# Download as, Fullscreen presentation and Image upload operations
ProxyPass           /lool https://127.0.0.1:9980/lool
ProxyPassReverse    /lool https://127.0.0.1:9980/lool
</VirtualHost>

```

After configuring these do restart your apache by [restarting](/index.php/Restart "Restart") `httpd.service`.

**Install the Nextcloud app**

Go to the Apps section and choose “Office & Text”, install the “Collabora Online” app. In admin panel select Collabora Online tab and specific the server's domain you have setup before.

**Solution without Docker: *CODE backend using an Archlinux package***

The [collabora-online-server-nodocker](https://aur.archlinux.org/packages/collabora-online-server-nodocker/) package brings to your Archlinux installation 1º Collabora Office (the desktop suite), and 2º the “CODE” (Collabora Online Development Edition) server, which is based on “lool” (LibreOffice OnLine).

Alter the `/etc/loolwsd/loolwsd.xml` file, so that:

*   `config > server_name` contains the host and port of the public Nextcloud address, separated by a colon (eg. `example.org:443`),
*   `config > ssl > enable` is false (ie. web browser —HTTPS→ proxy —HTTP→ loolwsd),
*   `config > ssl > termination` is true (I suppose you’ll manage TLS at the proxy level),
*   `config > storage > wopi > host` reflects the actual hostname (or pattern) of the proxy server (eg. `(?:.*\.)?example\.org`),
*   `config > admin_console > username` and `config > admin_console > password` are set to values of your choice.

Then:

*   [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `loolwsd.service`;
*   configure Nginx as showed in `/usr/share/doc/loolwsd/example.nginx.conf`, and restart it.

## See also

*   [Nextcloud Documentation Overview](https://docs.nextcloud.com/)
*   [Nextcloud Admin Manual](https://docs.nextcloud.com/server/latest/admin_manual/)