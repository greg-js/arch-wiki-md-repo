# phpPgAdmin

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")

[phpPgAdmin](http://phppgadmin.sourceforge.net/) is a web-based tool to help manage PostgreSQL databases using an PHP frontend.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 PHP](#PHP)
    *   [2.2 Web server](#Web_server)
        *   [2.2.1 Apache](#Apache)
        *   [2.2.2 Lighttpd](#Lighttpd)
        *   [2.2.3 Nginx](#Nginx)
    *   [2.3 phpPgAdmin configuration](#phpPgAdmin_configuration)
*   [3 Accessing your phpPgAdmin installation](#Accessing_your_phpPgAdmin_installation)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Login disallowed for security reasons](#Login_disallowed_for_security_reasons)

## Installation

PhpPgAdmin requires a web server with PHP, such as Apache. To set it up, see [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") and [Apache HTTP Server#PHP](/index.php/Apache_HTTP_Server#PHP "Apache HTTP Server").

Install the [phppgadmin](https://www.archlinux.org/packages/?name=phppgadmin) package.

## Configuration

### PHP

You need to enable the `pgsql` extension in PHP by editing `/etc/php/php.ini` and uncommenting the following line:

```
extension=pgsql.so

```

You need to make sure that PHP can access `/etc/webapps`. Add it to `open_basedir` in `/etc/php/php.ini` if necessary:

```
open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/:/etc/webapps

```

### Web server

#### Apache

Create the Apache configuration file:

 `/etc/httpd/conf/extra/phppgadmin.conf` 

```
Alias /phppgadmin "/usr/share/webapps/phppgadmin"
<Directory "/usr/share/webapps/phppgadmin">
    DirectoryIndex index.php
    AllowOverride All
    Options FollowSymlinks
    Require all granted
</Directory>

```

And include it in `/etc/httpd/conf/httpd.conf`:

```
# phpPgAdmin configuration
Include conf/extra/phppgadmin.conf

```

By default, everyone can see the phpPgAdmin page, to change this, edit `/etc/httpd/conf/extra/phppgadmin.conf` to your liking. For example, if you only want to be able to access it from the same machine, replace `Require all granted` by `Require local`.

#### Lighttpd

The php setup for lighttpd is exactly the same as for apache. Make an alias for phppgadmin in your lighttpd config.

```
 alias.url = ( "/phppgadmin" => "/usr/share/webapps/phppgadmin/")

```

Then enable mod_alias, mod_fastcgi and mod_cgi in your config ( server.modules section )

Make sure lighttpd is setup to serve php files, [Lighttpd#FastCGI](/index.php/Lighttpd#FastCGI "Lighttpd")

Restart lighttpd and browse to [http://localhost/phppgadmin/index.php](http://localhost/phppgadmin/index.php)

#### Nginx

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Grammar, punctuation, style issues, see also [Help:Style](/index.php/Help:Style "Help:Style") and related. (Discuss in [Talk:PhpPgAdmin#](https://wiki.archlinux.org/index.php/Talk:PhpPgAdmin))

Create a symbolic link to the /usr/share/webapps/phppgadmin directory from whichever directory your vhost is serving files from, e.g. /srv/http/<domain>/public_html/

```
 sudo ln -s /usr/share/webapps/phppgadmin /srv/http/<domain>/public_html/phppgadmin

```

You can also setup a sub domain with a server block like so (if using php-fpm):

Also, you need to use at less php-fpm (you need it), you have to make it running first (if you not do it, you will have a "502 bad gateway" error instead of the phpPgadmin first page).

For make it running after install the package, make a "systemctl start php-fpm" (and enable it if you want to use it all the time and/or after reboot, by "systemctl enable php-fpm)

```
 server {
         server_name     phppgadmin.<domain.tld>;
         access_log      /srv/http/<domain>/logs/phppgadmin.access.log;
         error_log       /srv/http/<domain.tld>/logs/phppgadmin.error.log;

         location / {
                 root    /srv/http/<domain.tld>/public_html/phppgadmin;
                 index   index.html index.htm index.php;
         }

         location ~ \.php$ {
                 root            /srv/http/<domain.tld>/public_html/phppgadmin;
                 fastcgi_pass    unix:/var/run/php-fpm/php-fpm.sock;
                 fastcgi_index   index.php;
                 fastcgi_param   SCRIPT_FILENAME  /srv/http/<domain.tld>/public_html/phppgadmin/$fastcgi_script_name;
                 include         fastcgi_params;
         }
 }

```

but there is an other simple way to do it running (also, if you need some other web apps, it would be easy more after):

```
 server {
     listen 80;
     server_name localhost default_server;
     root /srv/http/www/public_html;
     index index.html index.html index.php;
     location ~ \.php$ {
         try_files $uri =404;
         include fastcgi_params;
         fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
         fastcgi_index index.php;
         fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name; } }

```

with this config, your phppgadmin will be accessible at [http://localhost/phppgadmin](http://localhost/phppgadmin) directly and you will be able also to add some other web apps easy in the same way

(just have to paste/link them under public_html directory and find it at localhost/your_webapps)

this config make working all php file inside your localhost directly

(also it is a good idea to allow a user http http in the top of this nginx file and make directory srv/http/ under http owner/group)

the "server" serve only if you want to create some other server name designed only for this...

also, make a root inside the location of php is not a simple way to do and make the config file in trouble...

### phpPgAdmin configuration

phpPgAdmin's configuration file is located at `/etc/webapps/phppgadmin/config.inc.php`. If you have a local PostgreSQL server, it should be usable without making any modifications.

If your PostgreSQL server is not on the localhost, edit the following line:

```
$conf['servers'][0]['host'] = _;_

```

## Accessing your phpPgAdmin installation

Your phpPgAdmin installation is now complete. Before start using it you need to restart your apache server by following command:

```
# systemctl restart httpd.service

```

You can access your phpPgAdmin installation by going to [http://localhost/phppgadmin/](http://localhost/phppgadmin/)

## Troubleshooting

### Login disallowed for security reasons

If extra login security is true, then logins via phpPgAdmin with no password or certain usernames (_pgsql_, _postgres_, _root_, _administrator_) will be denied. Only set this to `false` once you have read the FAQ and understand how to change PostgreSQL's `pg_hba.conf` to enable passworded local connections.

Edit `/etc/webapps/phppgadmin/config.inc.php` and change the following line

```
 $conf['extra_login_security'] = true;

```

to

```
 $conf['extra_login_security'] = false;

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=PhpPgAdmin&oldid=413725](https://wiki.archlinux.org/index.php?title=PhpPgAdmin&oldid=413725)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")

Hidden category:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")