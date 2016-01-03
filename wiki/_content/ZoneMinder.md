# ZoneMinder

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

ZoneMinder is an integrated set of applications which provide a complete surveillance solution allowing capture, analysis, recording and monitoring of any CCTV or security cameras attached to a Linux based machine. It is designed to run on distributions which support the Video For Linux (V4L) interface and has been tested with video cameras attached to BTTV cards, various USB cameras and also supports most IP network cameras.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Apache configuration](#Apache_configuration)
        *   [2.1.1 Edit /etc/httpd/conf/httpd.conf](#Edit_.2Fetc.2Fhttpd.2Fconf.2Fhttpd.conf)
            *   [2.1.1.1 Enable PHP](#Enable_PHP)
            *   [2.1.1.2 Enable mod_cgi](#Enable_mod_cgi)
            *   [2.1.1.3 Load the httpd-zoneminder configuration file](#Load_the_httpd-zoneminder_configuration_file)
    *   [2.2 PHP](#PHP)
        *   [2.2.1 Edit /etc/php/php.ini](#Edit_.2Fetc.2Fphp.2Fphp.ini)
            *   [2.2.1.1 Ensure the following extensions are enabled by uncommenting these lines](#Ensure_the_following_extensions_are_enabled_by_uncommenting_these_lines)
            *   [2.2.1.2 Set your timezone](#Set_your_timezone)
    *   [2.3 MySQL](#MySQL)
    *   [2.4 Optional packages](#Optional_packages)
    *   [2.5 Starting](#Starting)
    *   [2.6 Flushing application data](#Flushing_application_data)
        *   [2.6.1 Dropping the database](#Dropping_the_database)
        *   [2.6.2 Reset the database and permissions](#Reset_the_database_and_permissions)
        *   [2.6.3 Flush the cache folders](#Flush_the_cache_folders)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Local video devices](#Local_video_devices)
    *   [3.2 Multiple local USB cameras](#Multiple_local_USB_cameras)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [zoneminder](https://aur.archlinux.org/packages/zoneminder/)<sup><small>AUR</small></sup> package. The development branch is also available with [zoneminder-git](https://aur.archlinux.org/packages/zoneminder-git/)<sup><small>AUR</small></sup>.

It is very important that [LAMP](/index.php/LAMP "LAMP") stack is installed and properly configured in order for ZoneMinder to work.

Once configuration below is completed and the system service started, the web interface will be accessible via [http://localhost/zm](http://localhost/zm).

## Configuration

### Apache configuration

#### Edit /etc/httpd/conf/httpd.conf

##### Enable PHP

1\. Comment out LoadModule mpm_event_module modules/mod_mpm_event.so:

```
 #LoadModule mpm_event_module modules/mod_mpm_event.so

```

2\. Uncomment LoadModule mpm_prefork_module modules/mod_mpm_prefork.so:

```
 LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

3\. Load mod_php at or near line 183:

```
 LoadModule php5_module modules/libphp5.so

```

4\. Place this at or near the end of the file:

```
 Include conf/extra/php5_module.conf

```

##### Enable mod_cgi

Uncomment the following line at or near line 170:

```
LoadModule cgi_module modules/mod_cgi.so

```

##### Load the httpd-zoneminder configuration file

Add this line at or near the end of httpd.conf:

```
Include conf/extra/httpd-zoneminder.conf

```

### PHP

#### Edit /etc/php/php.ini

##### Ensure the following extensions are enabled by uncommenting these lines

```
 extension=ftp.so
 extension=gd.so
 extension=gettext.so
 extension=mcrypt.so
 extension=pdo_mysql.so
 extension=sockets.so
 extension=zip.so

```

##### Set your timezone

For example:

```
date.timezone = "Australia/Sydney"

```

See [http://php.net/manual/en/timezones.php](http://php.net/manual/en/timezones.php) for a list of timezones.

### MySQL

Create the zm database and user with appropriate permissions and password :

 `$ mysql -u root -p` 

```
MariaDB> CREATE DATABASE zm;

MariaDB> CREATE USER 'zmuser'@'localhost' IDENTIFIED BY 'choose_password';

MariaDB> GRANT CREATE, INSERT, SELECT, DELETE, UPDATE ON zm.* TO zmuser@localhost;

MariaDB> exit
```

Import the preconfigured tables into your newly created zm database:

```
$ mysql -u root -p zm < /usr/share/zoneminder/db/zm_create.sql

```

Update the ZoneMinder config with your new parameters:

 `/etc/zm.conf` 

```
ZM_DB_HOST=localhost
ZM_DB_NAME=zm
ZM_DB_USER=zmuser
ZM_DB_PASS=chosen_password
```

### Optional packages

For thumbnail generation (used rarely), install the [netpbm](https://www.archlinux.org/packages/?name=netpbm) package.

### Starting

[Start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `httpd.service` and `zoneminder.service`.

### Flushing application data

This is useful for developers or users that need to wipe all ZoneMinder and start fresh.

#### Dropping the database

Drop the ZoneMinder MySQL database.

MySQL root user with a password:

```
$ echo 'delete from user where User="zoneminder";' | mysql --defaults-file=/etc/mysql/my.cnf -p mysql
$ echo 'delete from db where User="zoneminder";' | mysql --defaults-file=/etc/mysql/my.cnf -p mysql
$ mysqladmin --defaults-file=/etc/mysql/my.cnf -p -f drop zoneminder

```

Or, root without password:

```
$ echo 'delete from user where User="zoneminder";' | mysql --defaults-file=/etc/mysql/my.cnf mysql
$ echo 'delete from db where User="zoneminder";' | mysql --defaults-file=/etc/mysql/my.cnf mysql
$ mysqladmin --defaults-file=/etc/mysql/my.cnf -f drop zm

```

#### Reset the database and permissions

MySQL root user with a password:

```
$ mysqladmin --defaults-file=/etc/mysql/my.cnf -p -f reload
$ cat /usr/share/zoneminder/db/zm_create.sql | mysql --defaults-file=/etc/mysql/my.cnf -p
$ echo 'grant lock tables, alter,select,insert,update,delete on zm.* to 'zmuser'@localhost identified by "zoneminder";' | mysql --defaults-file=/etc/mysql/my.cnf -p mysql

```

Or, root without passsword:

```
$ mysqladmin --defaults-file=/etc/mysql/my.cnf -f reload
$ cat /usr/share/zoneminder/db/zm_create.sql | mysql --defaults-file=/etc/mysql/my.cnf
$ echo 'grant lock tables, alter,select,insert,update,delete on zm.* to 'zmuser'@localhost identified by "zoneminder";' | mysql --defaults-file=/etc/mysql/my.cnf mysql

```

#### Flush the cache folders

Note: this removes all images and events!

```
$ rm -Rf /var/cache/zoneminder/events/* /var/cache/zoneminder/images/* /var/cache/zoneminder/temp/*

```

## Troubleshooting

Logs by default are kept in **/var/log/zoneminder**. You can also inspect the log within the web interface.

See the upstream wiki page, [Troubleshooting](http://www.zoneminder.com/wiki/index.php/Troubleshooting).

### Local video devices

It is important that the user running httpd (usually **http**) can access your cameras, for example:

```
$ groups http
video http

```

```
$ ls -l /dev/video0
crw-rw----+ 1 root video 81, 0 Oct 28 21:54 /dev/video0

```

That is, add the **http** user to the **video** group.

### Multiple local USB cameras

If you observe an error like, **libv4l2: error turning on stream: No space left on device** when using multiple USB video devices (such as multiple webcams), you may need to increase the bandwidth on the bus.

Test first by stopping the **zoneminder** service, then:

```
$ rmmod uvcvideo
$ modprobe uvcvideo quirks=128

```

Start the **zoneminder** service and if the issue is resolved, perist the change by adding the module option to **/etc/modprobe.d/uvcvideo.conf**. for example:

```
options uvcvideo nodrop=1 quirks=128

```

([reference](http://renoirsrants.blogspot.com.au/2011/07/multiple-webcams-on-zoneminder.html))

## See also

*   [http://www.zoneminder.com/wiki/index.php/Arch_Linux](http://www.zoneminder.com/wiki/index.php/Arch_Linux) — Upstream project page.

Retrieved from "[https://wiki.archlinux.org/index.php?title=ZoneMinder&oldid=414216](https://wiki.archlinux.org/index.php?title=ZoneMinder&oldid=414216)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Security](/index.php/Category:Security "Category:Security")