**Note:** If you are using xampp, instead of [LAMP](/index.php/LAMP "LAMP"), there are different steps you need to take after installing. More info [here](https://www.mediawiki.org/wiki/Manual:Running_MediaWiki_on_XAMPP#381)

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 PHP](#PHP)
    *   [2.2 Web server](#Web_server)
        *   [2.2.1 Apache](#Apache)
        *   [2.2.2 Nginx](#Nginx)
        *   [2.2.3 Lighttpd](#Lighttpd)
    *   [2.3 Database](#Database)
    *   [2.4 LocalSettings.php](#LocalSettings.php)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Mathematics (texvc)](#Mathematics_.28texvc.29)
    *   [3.2 Unicode](#Unicode)
    *   [3.3 VisualEditor](#VisualEditor)

## Installation

You need to have a web server, such as [Apache](/index.php/Apache "Apache") installed, configured to be able to use [PHP](/index.php/PHP "PHP").

[Install](/index.php/Install "Install") the [php-gd](https://www.archlinux.org/packages/?name=php-gd), [php-intl](https://www.archlinux.org/packages/?name=php-intl) and [mediawiki](https://www.archlinux.org/packages/?name=mediawiki) packages.

You will also need a database system, such as [MySQL](/index.php/MySQL "MySQL"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") or [SQLite](/index.php/SQLite "SQLite").

## Configuration

The steps to achieve a working MediaWiki configuration involve editing the PHP settings and adding the MediaWiki configuration snippets.

### PHP

First, adjust the `open_basedir` in `/etc/php/php.ini` to include the mediawiki data directory (`/var/lib/mediawiki` by default):

 `/etc/php/php.ini`  `open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/:/var/lib/mediawiki/` 

Then, also in `/etc/php/php.ini`, uncomment the following lines: (in the `Dynamic Extensions` section)

```
extension=gd.so
extension=intl.so
extension=iconv.so

```

**Note:**

*   If you would like to use SQLite as database, also uncomment `extension=pdo_sqlite.so`.
*   If you would like to use MariaDB as database, also uncomment `extension=mysqli.so`.

Second, tweak the session handling or you might get a fatal error (`PHP Fatal error: session_start(): Failed to initialize storage module[...]`) by finding the `session.save_path` path. A good choice can be `/var/lib/php/sessions` or `/tmp/`.

 `/etc/php/php.ini`  `session.save_path = "/var/lib/php/sessions"` 

You will need to create the directory if it doesn't exist and then restrict its permissions:

```
# mkdir -p /var/lib/php/sessions/
# chown http:http /var/lib/php/sessions
# chmod go-rwx /var/lib/php/sessions

```

### Web server

#### Apache

Copy `/etc/webapps/mediawiki/apache.example.conf` to `/etc/httpd/conf/extra/mediawiki.conf` and edit it as needed.

Add the following lines to `/etc/httpd/conf/httpd.conf`

```
Include conf/extra/mediawiki.conf

```

[Restart](/index.php/Restart "Restart") the `httpd.service` daemon.

**Note:** The default file from `/etc/webapps/mediawiki/apache.example.conf` will overwrite the PHP open_basedir setting, possibally conflicting with other pages. This behavior can be changed by moving line starting with `php_admin_value` between the `<Directory>` tags. Further, if you are running multiple applications that depend on the same server, this value could also be added to the open_basedir value in `/etc/php/php.ini` instead of `/etc/httpd/conf/extra/mediawiki.conf`

#### Nginx

To get MediaWiki working with [Nginx](/index.php/Nginx "Nginx"), create the following file:

 `/etc/nginx/mediawiki.conf` 
```

location / {
   index index.php;
   try_files $uri $uri/ @mediawiki;
}
location @mediawiki {
   rewrite ^/(.*)$ /index.php?title=$1&$args;
}
location ~ \.php5?$ {
   include /etc/nginx/fastcgi_params;
   fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
   fastcgi_index index.php5;
   fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
   try_files $uri @mediawiki;
}
location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
   try_files $uri /index.php;
   expires max;
   log_not_found off;
}
# Restrictions based on the .htaccess files
location ^~ ^/(cache|includes|maintenance|languages|serialized|tests|images/deleted)/ {
   deny all;
}
location ^~ ^/(bin|docs|extensions|includes|maintenance|mw-config|resources|serialized|tests)/ {
   internal;
}
location ^~ /images/ {
   try_files $uri /index.php;
}
location ~ /\. {
   access_log off;
   log_not_found off; 
   deny all;
}

```

Ensure that [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) is installed and [started](/index.php/Start "Start").

Include a server directive, similar to this

 `/etc/nginx/nginx.conf` 
```
server {
  listen 80;
  server_name mediawiki;
  root /usr/share/webapps/mediawiki;
  index index.php;
  charset utf-8;
# For correct file uploads
  client_max_body_size    100m; # Equal or more than upload_max_filesize in /etc/php/php.ini
  client_body_timeout     60;
  include mediawiki.conf;

}

```

Finally, [restart](/index.php/Restart "Restart") `nginx.service` and `php-fpm.service` daemons.

#### Lighttpd

You should have [Lighttpd](/index.php/Lighttpd "Lighttpd") installed and configured. "mod_alias" and "mod_rewrite" in server.modules array of lighttpd is required. Append to the lighttpd configuration file the following lines

 `/etc/lighttpd/lighttpd.conf` 
```
alias.url += ("/mediawiki" => "/usr/share/webapps/mediawiki/")
url.rewrite-once += (
                "^/mediawiki/wiki/upload/(.+)" => "/mediawiki/wiki/upload/$1",
                "^/mediawiki/wiki/$" => "/mediawiki/index.php",
                "^/mediawiki/wiki/([^?]*)(?:\?(.*))?" => "/mediawiki/index.php?title=$1&$2"
)

```

[Restart](/index.php/Restart "Restart") the `lighttpd.service` daemon.

### Database

If the database server is already set up, MediaWiki can automatically create the database (provided that the database root password is supplied) during the [next step](#LocalSettings.php). Otherwise the database needs to be created manually, see [upstream instructions](https://www.mediawiki.org/wiki/Manual:Installing_MediaWiki#Create_a_database "mw:Manual:Installing MediaWiki").

### LocalSettings.php

Open the wiki url (usually `http://*your_server*/mediawiki/`) in a browser and do the initial configuration. Follow [upstream instructions](https://www.mediawiki.org/wiki/Manual:Config_script "mw:Manual:Config script").

The generated `LocalSettings.php` file is offered for download, save it to `/usr/share/webapps/mediawiki/LocalSettings.php`. This file defines the specific settings of your wiki. Whenever you upgrade the [mediawiki](https://www.archlinux.org/packages/?name=mediawiki) package, it is not replaced.

## Tips and tricks

### Mathematics (texvc)

Usually installing [texvc](https://www.archlinux.org/packages/?name=texvc) and enabling it in the config are enough:

```
$wgUseTeX = true;

```

If you get problems, try to increase limits for shell commands:

```
$wgMaxShellMemory = 8000000;
$wgMaxShellFileSize = 1000000;
$wgMaxShellTime = 300;
```

### Unicode

Check that php, apache and mysql uses UTF-8\. Otherwise you may face strange bugs because of encoding mismatch.

### VisualEditor

After following [this instruction](https://www.mediawiki.org/wiki/Extension:VisualEditor) on how to install the VisualEditor, you need a backend nodejs application on your server, called [Parsoid](https://www.mediawiki.org/wiki/Parsoid), to get it finally working.

Simply install [parsoid-git](https://aur.archlinux.org/packages/parsoid-git/) from the [AUR](/index.php/AUR "AUR") and adjust the path to your MediaWiki in following file:

 `/usr/share/webapps/parsoid/api/localsettings.js` 
```
parsoidConfig.setInterwiki( 'localhost', 'http://localhost/mediawiki/api.php' );

```

After that simply [enable](/index.php/Enable "Enable") and start `parsoid.service`.