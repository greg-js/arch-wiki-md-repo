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
extension=pgsql

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

Make sure to set up [nginx#FastCGI](/index.php/Nginx#FastCGI "Nginx") with separate configuration file for PHP as shown in [nginx#PHP configuration file](/index.php/Nginx#PHP_configuration_file "Nginx").

Using this method, you will access PhpPgAdmin as `phpmyadmin.<domain>`.

You can setup a sub domain (or domain) with a server block such as:

```
server {
    server_name     phppgadmin.<domain.tld>;
    root    /usr/share/webapps/phppgadmin;
    index   index.php;
    include php.conf;
}

```

### phpPgAdmin configuration

phpPgAdmin's configuration file is located at `/etc/webapps/phppgadmin/config.inc.php`. If you have a local PostgreSQL server, it should be usable without making any modifications.

If your PostgreSQL server is not on the localhost, edit the following line:

```
$conf['servers'][0]['host'] = *;*

```

## Accessing your phpPgAdmin installation

Your phpPgAdmin installation is now complete. Before start using it you need to restart your apache server by following command:

```
# systemctl restart httpd.service

```

You can access your phpPgAdmin installation by going to [http://localhost/phppgadmin/](http://localhost/phppgadmin/)

## Troubleshooting

### Login disallowed for security reasons

If extra login security is true, then logins via phpPgAdmin with no password or certain usernames (*pgsql*, *postgres*, *root*, *administrator*) will be denied. Only set this to `false` once you have read the FAQ and understand how to change PostgreSQL's `pg_hba.conf` to enable passworded local connections.

Edit `/etc/webapps/phppgadmin/config.inc.php` and change the following line

```
 $conf['extra_login_security'] = true;

```

to

```
 $conf['extra_login_security'] = false;

```