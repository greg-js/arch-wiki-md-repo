[ZoneMinder](https://www.zoneminder.com/) is an integrated set of applications which provide a complete surveillance solution allowing capture, analysis, recording and monitoring of any CCTV or security cameras attached to a Linux based machine. It is designed to run on distributions which support the Video For Linux (V4L) interface and has been tested with video cameras attached to BTTV cards, various USB cameras and also supports most IP network cameras.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Apache](#Apache)
    *   [2.2 PHP](#PHP)
    *   [2.3 MySQL](#MySQL)
        *   [2.3.1 Security](#Security)
    *   [2.4 Starting](#Starting)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Flushing application data](#Flushing_application_data)
        *   [3.1.1 Recreate the database](#Recreate_the_database)
        *   [3.1.2 Flush the cache folders](#Flush_the_cache_folders)
    *   [3.2 Local video devices](#Local_video_devices)
    *   [3.3 Multiple local USB cameras](#Multiple_local_USB_cameras)
*   [4 See also](#See_also)

## Installation

**Note:** It is very important that a [LAMP](/index.php/LAMP "LAMP") stack is installed and properly configured in order for ZoneMinder to work.

[Install](/index.php/Install "Install") the [zoneminder](https://aur.archlinux.org/packages/zoneminder/) package. The development branch is also available with [zoneminder-git](https://aur.archlinux.org/packages/zoneminder-git/).

For thumbnail generation (used rarely), install the [netpbm](https://www.archlinux.org/packages/?name=netpbm) package.

Once configuration below is completed and the system service started, the web interface will be accessible via [http://localhost/zoneminder/](http://localhost/zoneminder/).

## Configuration

### Apache

Enable PHP as described in [Apache HTTP Server#PHP](/index.php/Apache_HTTP_Server#PHP "Apache HTTP Server").

Uncomment the following line in `/etc/httpd/conf/httpd.conf`:

```
LoadModule cgi_module modules/mod_cgi.so

```

Include the `httpd-zoneminder` configuration file, by adding this line at or near the end of `httpd.conf`:

```
Include conf/extra/httpd-zoneminder.conf

```

### PHP

Edit `/etc/php/php.ini`. Ensure the following extensions are enabled by uncommenting these lines:

```
extension=apcu
extension=ftp
extension=gd
extension=gettext
extension=pdo_mysql
extension=sockets
extension=zip

```

Also set your timezone, for example:

```
date.timezone = "Australia/Sydney"

```

See [http://php.net/manual/en/timezones.php](http://php.net/manual/en/timezones.php) for a list of timezones.

Sometimes, the /etc/php/conf.d/zoneminder.ini file may appear:

```
 extension = apcu
 extension = ftp
 extension = gd
 extension = gettext
 extension = pdo_mysql
 extension = sockets
 extension = zip

```

```
 date.timezone = PLACEHOLDER

```

if the zone is not logged, run:

```
 sed -i 's | PLACEHOLDER |' `timedatectl | grep "Time zone" | tr -s * | cut -f4 -d * `'| g' /etc/php/conf.d/zoneminder.ini

```

### MySQL

Create the zm database and user with appropriate permissions and password :

 `$ mysql -u root -p` 
```
CREATE DATABASE zm;
CREATE USER 'zmuser'@'localhost' IDENTIFIED BY 'zmpass';
GRANT ALL ON zm.* TO 'zmuser'@'localhost';
exit
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
ZM_DB_PASS=zmpass
```

Set up sql mode, otherwise strange sql-related errors will occur when saving various parts of configuration

 `/etc/mysql/my.cnf.d/zoneminder.cnf` 
```
[mysqld]
sql_mode=NO_ENGINE_SUBSTITUTION
```

#### Security

To increase security, you need to set a password for the root user:

```
/usr/bin/mysqladmin' -u root password 'new-password'
/usr/bin/mysqladmin' -u root -h lilya-x64 password 'new-password'

```

In addition, you can run:

```
 /usr/bin/mysql_secure_installation

```

### Starting

[Start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `httpd.service`, `zoneminder.service`, `fcgiwrap-multiwatch` and `php-fpm.service`.

## Troubleshooting

Logs by default are kept in `/var/log/zoneminder`. You can also inspect the log within the web interface.

See the upstream wiki page: [Troubleshooting](http://www.zoneminder.com/wiki/index.php/Troubleshooting).

### Flushing application data

This is useful for developers or users that need to wipe all ZoneMinder and start fresh.

#### Recreate the database

Drop the ZoneMinder MySQL database and delete the MySQL user:

 `$ mysql -u root -p` 
```
DROP DATABASE zm;
DROP USER 'zmuser'@'localhost';

```

Recreate the database and user:

 `$ mysql -u root -p` 
```
CREATE DATABASE zm;
CREATE USER 'zmuser'@'localhost' IDENTIFIED BY 'zmpass';
GRANT CREATE, INSERT, SELECT, DELETE, UPDATE ON zm.* TO 'zmuser'@'localhost';
exit
```

Import the preconfigured tables into your newly created zm database:

```
$ mysql -u root -p zm < /usr/share/zoneminder/db/zm_create.sql

```

#### Flush the cache folders

**Warning:** This removes all images and events.

```
$ rm -Rf /var/cache/zoneminder/events/* /var/cache/zoneminder/images/* /var/cache/zoneminder/temp/*

```

### Local video devices

It is important that the user running httpd (usually **http**) can access your cameras, for example:

 `$ groups http`  `video http`  `$ ls -l /dev/video0`  `crw-rw----+ 1 root video 81, 0 Oct 28 21:54 /dev/video0` 

That is, add the **http** user to the **video** group.

To add a user to the group run the command:

```
usermod -aG video http

```

### Multiple local USB cameras

If you observe an error like, **libv4l2: error turning on stream: No space left on device** when using multiple USB video devices (such as multiple webcams), you may need to increase the bandwidth on the bus.

Test first by stopping `zoneminder.service`, then:

```
$ rmmod uvcvideo
$ modprobe uvcvideo quirks=128

```

Start `zoneminder.service` and if the issue is resolved, persist the change by adding the module option to `/etc/modprobe.d/uvcvideo.conf`. For example:

```
options uvcvideo nodrop=1 quirks=128

```

([reference](http://renoirsrants.blogspot.com.au/2011/07/multiple-webcams-on-zoneminder.html))

## See also

*   [http://www.zoneminder.com/wiki/index.php/Arch_Linux](http://www.zoneminder.com/wiki/index.php/Arch_Linux) — Upstream project page.