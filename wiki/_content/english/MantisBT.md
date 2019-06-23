[MantisBT](https://mantisbt.org) (Mantis Bug Tracker) is a bug tracker written in [PHP](/index.php/PHP "PHP"). For a list of features, visit its website.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 PHP extensions](#PHP_extensions)
    *   [2.2 TTF fonts](#TTF_fonts)
    *   [2.3 Web server](#Web_server)
        *   [2.3.1 nginx + uwsgi](#nginx_+_uwsgi)
    *   [2.4 Database](#Database)
    *   [2.5 Administrator](#Administrator)
*   [3 Usage](#Usage)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [mantisbt](https://aur.archlinux.org/packages/mantisbt/) package.

Choose your favorite [web server](/index.php/Web_server "Web server") and/or application server (such as [UWSGI](/index.php/UWSGI "UWSGI")) for making the application available.

## Configuration

*mantisbt* has a decent [administration guide](https://mantisbt.org/docs/master/en-US/Admin_Guide/html-desktop/), that can be followed for setting it up.

All configuration is exposed in `/etc/webapps/mantisbt/config_inc.php`.

*   Setup a compatible [DBMS](/index.php/DBMS "DBMS") and use the 'Database Configuration' section to connect mantisbt with it.
*   The 'Anonymous Access / Signup' section needs special attention, if you are not planning on disabling CAPTCHAs for new signups (see [#PHP extensions](#PHP_extensions) and [#TTF fonts](#TTF_fonts)).
*   If you want to use [SMTP](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol "wikipedia:Simple Mail Transfer Protocol") you can set it up in the 'Email Configuration' section. mantisbt defaults to a phpmailer setup, which has the downside of not reaching mail servers that use [grey listing](/index.php/Postgrey "Postgrey").

In any case, you will need to meet some requirements for *mantisbt* to work properly:

### PHP extensions

*   **mysqli** (if you are using [MySQL](/index.php/MySQL "MySQL")/[MariaDB](/index.php/MariaDB "MariaDB"))
*   **gd** (if you plan on using [CAPTCHA](https://en.wikipedia.org/wiki/CAPTCHA "wikipedia:CAPTCHA") for user signup)

### TTF fonts

*   make sure to [install a TrueTypeFont](/index.php/Fonts#Pacman "Fonts"), that you would like to use for the creation of CAPTCHAs
*   setup the paths and names of the fonts, you would like to use:

 `/etc/webapps/mantisbt/config_inc.php` 
```
# trailing slash is important!
$g_system_font_folder = '/usr/share/fonts/TTF/';

# here DroidSans.ttf from the package [ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid) is used for illustration
$g_font_per_captcha = 'DroidSans.ttf';
```

**Note:** Make sure to also include the TTF path (e.g. `/usr/share/fonts/TTF`) in the [open_basedir](http://www.php.net/manual/en/features.safe-mode.php#ini.open-basedir) of your PHP instance!

### Web server

#### nginx + uwsgi

This example shows a basic setup using a subdomain for the bug tracker, with some handson redirects. The below mentioned file needs of course to be sourced within `/etc/nginx/nginx.conf`. For a subfolder-based setup for *mantisbt*, some modifications are needed.

 `/etc/nginx/nginx.conf` 
```
server {
  listen 80;
  listen [::]:80;
  server_name bugs.mydomain.org www.mydomain.org;
  return 301 https://bugs.mydomain.org$request_uri;
}
server {
  listen 443 ssl;
  listen [::]:443 ssl;
  server_name www.bugs.mydomain.org;
  return 301 https://bugs.mydomain.org$request_uri;
}
server {
  listen 443 ssl;
  listen [::]:443 ssl;
  server_name bugs.mydomain.org;
  include tls.conf;
  root /usr/share/webapps/mantisbt;
  access_log /var/log/nginx/access.bugs.mydomain.log;
  error_log /var/log/nginx/error.bugs.mydomain.log;
  include letsencrypt-challenge.conf;

  location ~ ^/(admin|core|doc|lang) {
    deny all;
  }

  location / {
    index index.php;
    try_files $uri $uri/ @mantisbt;
  }

  location @mantisbt {
    include uwsgi_params;
    uwsgi_modifier1 14;
    uwsgi_pass unix:/run/uwsgi/mantisbt.sock;
  }

  location ~  \.php?$ {
    include uwsgi_params;
    uwsgi_modifier1 14;
    uwsgi_pass unix:/run/uwsgi/mantisbt.sock;
  }

  # Deny serving files beginning with a dot, but allow letsencrypt acme-challenge
  location ~ /\.(?!well-known/acme-challenge) {
    access_log off;
    log_not_found off;
    deny all;
  }
}

```

[UWSGI](/index.php/UWSGI "UWSGI") can be used to achieve a resource preserving setup with dedicated PHP settings.

 `/etc/uwsgi/mantisbt.ini` 
```
[uwsgi]
procname-master = mantisbt
plugins = php
master = true
socket = /run/uwsgi/%n.sock
uid = http
gid = http
processes = 10
cheaper = 2
cheaper-step = 1
idle = 600
die-on-idle = true

php-allowed-ext = .php
php-docroot = /usr/share/webapps/mantisbt
php-index = index.php
php-set = date.timezone=Europe/Berlin
php-set = open_basedir=/tmp/:/usr/share/fonts/TTF:/usr/share/webapps/mantisbt:/usr/share/webapps/mantisbt/core:/etc/webapps/mantisbt
php-set = session.save_path=/tmp
php-set = session.gc_maxlifetime  21600
php-set = session.gc_divisor      500
php-set = session.gc_probability  1
php-set = post_max_size=64M
php-set = upload_max_filesize=64M
php-set = always_populate_raw_post_data=-1
php-set = extension=curl
php-set = extension=gd
php-set = extension=imagick
php-set = extension=intl
php-set = extension=mysqli

```

If your (modified) versions of these files are in place, you should restart your [nginx](/index.php/Nginx "Nginx") and start/enable a uwsgi socket for *mantisbt* [using systemd](/index.php/Systemd#Using_units "Systemd").

### Database

After making the application available, go to [/admin/install.php](https://bugs.mydomain.org/admin/install.php) to setup the database. Follow the instructions on that page and let *mantisbt* generate the tables.

**Note:** You have to modify your [#Web server](#Web_server) settings temporarily to be able to visit that page. Here this is shown according to the example of using [#nginx + uwsgi](#nginx_+_uwsgi). `/etc/nginx/nginx.conf` 
```
  location ~ ^/(core|doc|lang) {
    deny all;
  }

```

### Administrator

The initial account generated by *mantisbt* is called *administrator* and has the password *root*.

**Warning:** Make sure to change the password for the *administrator* user and set it up properly, right after logging in for the first time!

**Note:** Modify your [#Web server](#Web_server) settings again, to make the *admin* settings unavailable again. The example of using [#nginx + uwsgi](#nginx_+_uwsgi) shows you how.

## Usage

*mantisbt* should be all setup now. The *administrator* user is able to create new projects and give user rights to signed up users.

## See also

*   [Official website](https://mantisbt.org)
*   [Official wiki](https://mantisbt.org/wiki/doku.php)
*   [Official documentation](https://mantisbt.org/documentation.php)
*   [Official bug tracker](https://www.mantisbt.org/bugs)
*   [Official forums](https://mantisbt.org/forums/)
*   [Official mailing lists](https://mantisbt.org/mailinglists.php)
*   [MantisBT on github](https://github.com/mantisbt)
*   [#mantisbt on freenode.net](irc://irc.freenode.net/mantisbt)