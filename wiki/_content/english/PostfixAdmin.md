[PostfixAdmin](http://postfixadmin.sourceforge.net/) is a web interface for [Postfix](/index.php/Postfix "Postfix") used to manage mailboxes, virtual domains and aliases.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Hosting](#Hosting)
    *   [3.1 Apache](#Apache)
        *   [3.1.1 php-fpm](#php-fpm)
    *   [3.2 Nginx](#Nginx)
        *   [3.2.1 php-fpm](#php-fpm_2)
        *   [3.2.2 uWSGI](#uWSGI)
*   [4 Setup](#Setup)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Configuration not found](#Configuration_not_found)
    *   [5.2 Blank page on access](#Blank_page_on_access)

## Installation

To use PostfixAdmin, you need a working [web server](/index.php/Web_server "Web server") setup. You can either choose a web server, that can serve the web application directly (such as [Apache](/index.php/Apache "Apache")), or a setup in which a web server (e.g [Nginx](/index.php/Nginx "Nginx")) forwards requests to an application server (e.g. [UWSGI](/index.php/UWSGI "UWSGI") or [php-fpm](https://www.archlinux.org/packages/?name=php-fpm)).

For IMAP functionality, refer to [PHP#IMAP](/index.php/PHP#IMAP "PHP").

Next, [install](/index.php/Install "Install") the [postfixadmin](https://www.archlinux.org/packages/?name=postfixadmin) package.

**Note:** Postfixadmin should only be accessed over [TLS](/index.php/TLS "TLS") (unless accessed directly from the machine running it), as it otherwise exposes passwords and user data.

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
$CONF['default_aliases'] = array (
    'abuse' => 'abuse@change-this-to-your.domain.tld',
    'hostmaster' => 'hostmaster@change-this-to-your.domain.tld',
    'postmaster' => 'postmaster@change-this-to-your.domain.tld',
    'webmaster' => 'webmaster@change-this-to-your.domain.tld'
);

$CONF['vacation_domain'] = 'autoreply.change-this-to-your.domain.tld';

$CONF['footer_text'] = 'Return to change-this-to-your.domain.tld';
$CONF['footer_link'] = 'http://change-this-to-your.domain.tld';

```

If installing dovecot and you changed the password scheme in dovecot (to SHA512-CRYPT for example), reflect that with Postfix

 `/etc/webapps/postfixadmin/config.local.php` 
```
$CONF['encrypt'] = 'dovecot:SHA512-CRYPT';

```

As of dovecot 2, dovecotpw has been deprecated. You will also want to ensure that your config reflects the new binary name.

**Note:** As of postfixadmin 2.91 this is set correctly by default.
 `/etc/webapps/postfixadmin/config.local.php` 
```
$CONF['dovecotpw'] = "/usr/sbin/doveadm pw";

```

**Note:** For this to work it does not suffice to have dovecot installed, it also needs to be configured. See [Dovecot#Dovecot configuration](/index.php/Dovecot#Dovecot_configuration "Dovecot").

## Hosting

**Note:** PostfixAdmin needs to be run as its own user and group (i.e. `postfixadmin`). It's using `/etc/webapps/postfixadmin`, `/var/lib/postfixadmin` and `/run/postfixadmin` for configurations, template caches and (potentially) sockets (respectively)!

### Apache

The [apache](/index.php/Apache "Apache") [web server](/index.php/Web_server "Web server") can serve dynamic web applications with the help of modules, such as [mod_proxy_fcgi](https://httpd.apache.org/docs/current/mod/mod_proxy_fcgi.html) or [mod_proxy_uwsgi](https://httpd.apache.org/docs/current/mod/mod_proxy_uwsgi.html).

#### php-fpm

[Install](/index.php/Install "Install") and configure [apache](/index.php/Apache "Apache") with [php-fpm](/index.php/Apache_HTTP_Server#Using_php-fpm_and_mod_proxy_fcgi "Apache HTTP Server"). Use a [pool](https://www.php.net/manual/en/install.fpm.configuration.php) run as user and group `postfixadmin`. The socket file should be accessible by the `http` user and/or group.

Include the following configuration in your [apache](/index.php/Apache "Apache") configuration (i.e. `/etc/httpd/conf/httpd.conf`) and [restart](/index.php/Restart "Restart") the [web server](/index.php/Web_server "Web server"):

 `/etc/httpd/conf/postfixadmin.conf` 
```
Alias /postfixadmin "/usr/share/webapps/postfixadmin/public"
<Directory "/usr/share/webapps/postfixadmin/public">
    DirectoryIndex index.html index.php
    <FilesMatch \.php$>
        SetHandler "proxy:unix:/run/postfixadmin/postfixadmin.sock|fcgi://localhost/"
    </FilesMatch>
    AllowOverride All
    Options FollowSymlinks
    Require all granted
    SetEnv PHP_ADMIN_VALUE "open_basedir = /tmp/:/usr/share/webapps/postfixadmin:/etc/webapps/postfixadmin/:/var/cache/postfixadmin/templates_c"
</Directory>

```

Create a pool for postfixadmin and [restart](/index.php/Restart "Restart") php-fpm.service:

 `/etc/php/php-fpm.d/postfixadmin.conf` 
```
[postfixadmin]
user = postfixadmin
group = postfixadmin
listen = /run/postfixadmin/postfixadmin.sock
listen.owner = http
listen.group = http
pm = ondemand
pm.max_children = 4

```

To only allow localhost access to postfixadmin (for heightened security), add this to the previous `<Directory>` directive:

```
   Order Deny,Allow
   Deny from all
   Allow from 127.0.0.1

```

### Nginx

[Nginx](/index.php/Nginx "Nginx") can proxy application servers such as [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) and [uWSGI](/index.php/UWSGI "UWSGI"), that run a dynamic web application. The following examples describe a folder based setup over a non-default port (for simplicity).

**Note:** For server entry management in [nginx](/index.php/Nginx "Nginx") have a look at [Nginx#Managing server entries](/index.php/Nginx#Managing_server_entries "Nginx").

**Note:** Postfixadmin ships a configuration for [uWSGI](/index.php/UWSGI "UWSGI").

#### php-fpm

[Install](/index.php/Install "Install") [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) and [php-imap](https://www.archlinux.org/packages/?name=php-imap). Setup [nginx](/index.php/Nginx "Nginx") with [php-fpm](/index.php/Nginx#PHP_implementation "Nginx") and use a [pool](https://www.php.net/manual/en/install.fpm.configuration.php) run as user and group `postfixadmin`. The socket file should be accessible by the `http` user and/or group, but needs to be located below `/run/postfixadmin`. This can be achieved by adding the following lines.

 `/etc/php/php-fpm.d/postfixadmin.conf` 
```
[postfixadmin]
user = postfixadmin
group = postfixadmin
listen = /run/postfixadmin/postfixadmin.sock
listen.owner = http
listen.group = http
pm = ondemand
pm.max_children = 4

```

You will need to at least activate the `imap` and `mysqli` extensions in `/etc/php/php.ini`. Make sure you also add `/var/cache/postfixadmin` to [open_basedir](/index.php?title=Ic&action=edit&redlink=1 "Ic (page does not exist)") in your php.ini. Restart [php-fpm](/index.php?title=Php-fpm&action=edit&redlink=1 "Php-fpm (page does not exist)") for all these to take effect.

Add the following configuration for [nginx](/index.php/Nginx "Nginx") and [restart](/index.php/Restart "Restart") it.

 `/etc/nginx/sites-available/postfixadmin.conf` 
```
    server {
      listen 8081;
      server_name postfixadmin;
      root /usr/share/webapps/postfixadmin/public/;
      index index.php;
      charset utf-8;

      access_log /var/log/nginx/postfixadmin-access.log;
      error_log /var/log/nginx/postfixadmin-error.log;

      location / {
        try_files $uri $uri/ index.php;
      }

      location ~* \.php$ {
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        include fastcgi_params;
        fastcgi_pass unix:/run/postfixadmin/postfixadmin.sock;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_buffer_size 16k;
        fastcgi_buffers 4 16k;
      }
    }

```

#### uWSGI

[Install](/index.php/Install "Install") [uwsgi-plugin-php](https://www.archlinux.org/packages/?name=uwsgi-plugin-php), create a per-application socket for [uWSGI](/index.php/UWSGI "UWSGI") (see [UWSGI#Accessibility of uWSGI socket](/index.php/UWSGI#Accessibility_of_uWSGI_socket "UWSGI") for reference) and [activate](/index.php/Systemd#Using_units "Systemd") the `uwsgi-secure@postfixadmin.socket` unit.

Add the following configuration for nginx and [restart](/index.php/Restart "Restart") [nginx](/index.php/Nginx "Nginx").

 `/etc/nginx/sites-available/postfixadmin.conf` 
```
    server {
      listen 8081;
      server_name postfixadmin;
      root /usr/share/webapps/postfixadmin/public/;
      index index.php;
      charset utf-8;

      access_log /var/log/nginx/postfixadmin-access.log;
      error_log /var/log/nginx/postfixadmin-error.log;

      location / {
        try_files $uri $uri/ index.php;
      }

      # pass all .php or .php/path urls to uWSGI
      location ~ ^(.+\.php)(.*)$ {
        include uwsgi_params;
        uwsgi_modifier1 14;
        uwsgi_pass unix:/run/postfixadmin/postfixadmin.sock;
      }
    }

```

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