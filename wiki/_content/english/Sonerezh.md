[Sonerezh](https://www.sonerezh.bzh) is a self-hosted, web-based application for streaming your music everywhere.

## Installation

Install [sonerezh](https://aur.archlinux.org/packages/sonerezh/). You will need a database (e.g. [MariaDB](/index.php/MariaDB "MariaDB")) and a web server (like [Nginx](/index.php/Nginx "Nginx")) with PHP support. You may refer following sites:

*   [Apache](/index.php/Apache "Apache")
*   [Lighttpd](/index.php/Lighttpd "Lighttpd")
*   [Nginx](/index.php/Nginx "Nginx")

## Configuration

In `/etc/php/php.ini`, uncomment `extension=gd` and set your timezone as described in [PHP#Configuration](/index.php/PHP#Configuration "PHP").

In this configuration, we will configure the [Nginx](/index.php/Nginx "Nginx") web server to serve Sonerezh on localhost in the root location without SSL enabled (even though it's recommended to use it with SSL). First, place a copy of the Sonerezh Nginx configuration.

Copy `/usr/share/doc/sonerezh/example_nginx_vhost.conf` to `/etc/webapps/sonerezh/nginx.conf`.

Replace the domain name and reference this configuration file in the main nginx.conf:

 `/etc/nginx/nginx.conf` 
```

http {
    [...]
    include /etc/webapps/sonerezh/nginx.conf;
    [...]
 }

```

Here's an example on how you could setup a database for Sonerezh with [MariaDB](/index.php/MariaDB "MariaDB") called `sonerezh` for the user `sonerezh` identified by the password `sonerezh`:

```
CREATE DATABASE sonerezh;
GRANT ALL PRIVILEGES ON sonerezh.* TO sonerezh@'localhost' IDENTIFIED BY 'sonerezh';
FLUSH PRIVILEGES;

```

Do not forget to [restart](/index.php/Restart "Restart") your services (`nginx.service` and `php-fpm.service`).

Visit the installation wizard page at [http://sonerezh.localhost/install](http://sonerezh.localhost/install) and follow the instructions.