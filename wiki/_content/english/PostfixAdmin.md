[PostfixAdmin](http://postfixadmin.sourceforge.net/) is a web interface for [Postfix](/index.php/Postfix "Postfix") used to manage mailboxes, virtual domains and aliases.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Hosting](#Hosting)
    *   [3.1 Apache](#Apache)
    *   [3.2 Nginx](#Nginx)
*   [4 Setup](#Setup)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Configuration not found](#Configuration_not_found)
    *   [5.2 Blank page on access](#Blank_page_on_access)

## Installation

To use PostfixAdmin, you need a working [web server](/index.php/Web_server "Web server") setup. You can either choose a web server, that can serve the web application directly (such as [Apache](/index.php/Apache "Apache")), or a setup in which a web server (e.g [Nginx](/index.php/Nginx "Nginx")) forwards requests to an application server (e.g. [UWSGI](/index.php/UWSGI "UWSGI") or [php-fpm](https://www.archlinux.org/packages/?name=php-fpm)).

For IMAP functionality, refer to [PHP#IMAP](/index.php/PHP#IMAP "PHP").

Next, [install](/index.php/Install "Install") [postfixadmin](https://www.archlinux.org/packages/?name=postfixadmin).

## Configuration

Edit the PostfixAdmin configuration file:

 `/etc/webapps/postfixadmin/config.local.php` 
```
$CONF['configured'] = true;
// correspond to dovecot maildir path /home/vmail/%d/%u 
$CONF['domain_path'] = 'YES';
$CONF['domain_in_mailbox'] = 'NO';
$CONF['database_type'] = 'mysqli';
$CONF['database_host'] = 'localhost';
$CONF['database_user'] = 'postfix_user';
$CONF['database_password'] = 'hunter2';
$CONF['database_name'] = 'postfix_db';

// globally change all instances of ''change-this-to-your.domain.tld'' 
// to an appropriate value

```

If installing dovecot and you changed the password scheme in dovecot (to SHA512-CRYPT for example), reflect that with Postfix

 `/etc/webapps/postfixadmin/config.local.php` 
```
$CONF['encrypt'] = 'dovecot:SHA512-CRYPT';

```

As of dovecot 2, dovecotpw has been deprecated. You will also want to ensure that your config reflects the new binary name.

 `/etc/webapps/postfixadmin/config.local.php` 
```
$CONF['dovecotpw'] = "/usr/sbin/doveadm pw";

```

**Note:** For this to work it does not suffice to have dovecot installed, it also needs to be configured. See [Dovecot#Dovecot configuration](/index.php/Dovecot#Dovecot_configuration "Dovecot").

## Hosting

**Note:** PostfixAdmin needs to be run as its own user and group (i.e. `postfixadmin`). It's using `/etc/webapps/postfixadmin`, `/var/lib/postfixadmin` and `/run/postfixadmin` for configurations, template caches and (potentially) sockets (respectively)! As such, granting the webserver user permission to read, write and execute the config files may be needed. To do so, follow the instruction here [Access Control Lists](/index.php/Access_Control_Lists "Access Control Lists") in section: Granting execution permissions for private files to a web server. An example is provided here:

```
 #setfacl -m "u:http:rwx" /etc/webapps/postfixadmin/config.inc.php

```

### Apache

Create an Apache configuration file:

 `/etc/httpd/conf/extra/httpd-postfixadmin.conf` 
```
Alias /postfixadmin "/usr/share/webapps/postfixadmin/public"
<Directory "/usr/share/webapps/postfixadmin/public">
    DirectoryIndex index.html index.php
    AllowOverride All
    Options FollowSymlinks
    Require all granted
</Directory>

```

To only allow localhost access to postfixadmin (for heightened security), add this to the previous <Directory> directive:

```
   Order Deny,Allow
   Deny from all
   Allow from 127.0.0.1

```

Now, include httpd-postfixadmin.conf to `/etc/httpd/conf/httpd.conf`:

```
# PostfixAdmin configuration
Include conf/extra/httpd-postfixadmin.conf

```

### Nginx

Keep im mind that this is a minimal example without TLS encryption. Accessing postfixadmin from anywhere else than the machine running it will expose passwords and user data.

Install [nginx](https://www.archlinux.org/packages/?name=nginx), [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) and [php-imap](https://www.archlinux.org/packages/?name=php-imap). Setup [nginx](/index.php/Nginx "Nginx") with [php-fpm](/index.php/Nginx#PHP_implementation "Nginx").

You will need to at least activate the `imap` and `mysqli` extensions in `/etc/php/php.ini`

Create nginx config file

 `/etc/nginx/sites-available/postfixadmin.conf` 
```
    server {
      listen 8081;
      server_name postfixadmin;
      root            /usr/share/webapps/postfixadmin/public/;
      index           index.php;
      charset         utf-8;

      access_log /var/log/nginx/postfixadmin-access.log;
      error_log /var/log/nginx/postfixadmin-error.log;

      location / {
        try_files $uri $uri/ index.php;
      }

      location ~* \.php$ {
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        include       fastcgi_params;
        fastcgi_pass  unix:/run/php-fpm/php-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_buffer_size 16k;
        fastcgi_buffers 4 16k;
      }
    }

```

Enable the config as described [here](/index.php/Nginx#Managing_server_entries "Nginx").

## Setup

Finally, navigate to [http://127.0.0.1:80/postfixadmin/setup.php](http://127.0.0.1:80/postfixadmin/setup.php) to finish the setup. Generate your setup password hash at the bottom of the page once it is done. Write the hash to the config file

 `/etc/webapps/postfixadmin/config.local.php` 
```
$CONF['setup_password'] = 'yourhashhere';

```

Now you can create a superadmin account at [http://127.0.0.1:80/postfixadmin/setup.php](http://127.0.0.1:80/postfixadmin/setup.php)

## Troubleshooting

### Configuration not found

If you go to yourdomain/postfixadmin/setup.php and the application states, that it is unable to find config.inc.php, add `/etc/webapps/postfixadmin` to the `open_basedir` line in `/etc/php/php.ini` (see [PHP#Configuration](/index.php/PHP#Configuration "PHP") for reference).

### Blank page on access

If you get a blank page check the syntax of the configuration with `php -l /etc/webapps/postfixadmin/config.inc.php`.