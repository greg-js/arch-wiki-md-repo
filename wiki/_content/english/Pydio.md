[Pydio](https://pydio.com/) (formerly AjaXplorer) is an open source web application, written in PHP, for file sharing and synchronization.

## Installation

[Install](/index.php/Install "Install") the [pydio](https://aur.archlinux.org/packages/pydio/) package. Further you will need a database (e.g. [MariaDB](/index.php/MariaDB "MariaDB")), a web server ([Apache](/index.php/Apache "Apache"), [Lighttpd](/index.php/Lighttpd "Lighttpd") or [Nginx](/index.php/Nginx "Nginx")) with [PHP](/index.php/PHP "PHP")-support. You may refer following sites:

## Configuration

Make sure to adjust following variables to these minimal values in your `php.ini`:

 `/etc/php/php.ini` 
```
extension=exif.so
extension=gd.so
extension=mcrypt.so
extension=iconv.so
extension=mysqli.so
session.save_path = "/tmp"
output_buffering = Off

file_uploads = On
post_max_size = 20G
upload_max_filesize = 20G
max_file_uploads = 20000

```

In this configuration, we will configure the [Nginx](/index.php/Nginx "Nginx") web server to serve Pydio on localhost in the root location without SSL enabled (even though it's recommended to use it with SSL). First, place a copy of the Pydio Nginx configuration

```
# cp /usr/share/doc/pydio/nginx.conf.sample /etc/webapps/pydio/nginx.conf

```

replace the domain name

```
# sed -i 's/pydio.example.com/localhost/g' /etc/webapps/pydio/nginx.conf

```

and reference this configuration file in the main nginx.conf:

 `/etc/nginx/nginx.conf` 
```

http {
    [...]
    include /etc/webapps/pydio/nginx.conf;
    [...]
 }

```

Here's an example on how you could setup a database for Pydio with [MariaDB](/index.php/MariaDB "MariaDB") called `pydio` for the user `pydio` identified by the password `password`:

```
CREATE DATABASE pydio;
GRANT ALL PRIVILEGES ON pydio.* TO pydio@'localhost' IDENTIFIED BY 'pydio';
FLUSH PRIVILEGES;

```

Do not forget to (re)start your services (e.g. `nginx.service` and `php-fpm.service`)!

Visit the installation wizard page at [http://127.0.0.1/](http://127.0.0.1/) and follow the instructions.

## See also

*   [Official ArchLinux installation manual](https://pyd.io/archlinux/)