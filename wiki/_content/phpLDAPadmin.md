# phpLDAPadmin

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[phpLDAPadmin](http://phpldapadmin.sourceforge.net/) is an web-based [LDAP](/index.php/LDAP "LDAP") adminstration interface.

## Contents

*   [1 Pre-Installation](#Pre-Installation)
*   [2 Installation](#Installation)
*   [3 Configuration](#Configuration)
    *   [3.1 Apache](#Apache)
    *   [3.2 PHP](#PHP)
    *   [3.3 phpLDAPadmin configuration](#phpLDAPadmin_configuration)
*   [4 Accessing your phpLDAPadmin installation](#Accessing_your_phpLDAPadmin_installation)

## Pre-Installation

See [LAMP](/index.php/LAMP "LAMP") for a guide to setting up Apache, MySQL, and PHP.

## Installation

Install the package [phpldapadmin](https://www.archlinux.org/packages/?name=phpldapadmin) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

### Apache

Create the Apache configuration file:

 `/etc/httpd/conf/extra/phpldapadmin.conf` 

```
Alias /phpldapadmin "/usr/share/webapps/phpldapadmin"
<Directory "/usr/share/webapps/phpldapadmin">
    DirectoryIndex index.php
    AllowOverride All
    Options FollowSymlinks
    Require all granted
</Directory>

```

And include it in `/etc/httpd/conf/httpd.conf`:

```
# phpLDAPadmin configuration
Include conf/extra/phpldapadmin.conf

```

By default, everyone can see the phpLDAPadmin page, to change this, edit `/etc/httpd/conf/extra/phpldapadmin.conf` to your liking. For example, if you only want to be able to access it from the same machine, replace `Require all granted` by `Require local`.

### PHP

You need to enable the `php-ldap` extension in PHP by editing `/etc/php/php.ini` and uncommenting the line

```
;extension=ldap.so

```

You need to make sure that PHP can access `/usr/share/webapps` and `/etc/webapps`. Add them to `open_basedir` in `/etc/php/php.ini` :

```
open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/:/etc/webapps

```

### phpLDAPadmin configuration

phpLDAPadmin's configuration file is located at `/etc/webapps/phpldapadmin/config.php`. If you have a local LDAP server, it should be usable without making any modifications.

If your LDAP server is not on the localhost, uncomment and edit the following line:

```
$servers->setValue('server','host','127.0.0.1');

```

Although not strictly necessary you can name your server by editing the following line:

```
$servers->setValue('server','name','My LDAP server');

```

## Accessing your phpLDAPadmin installation

Your phpLDAPadmin installation is now complete. Before start using it you need to restart Apache.

You can access your phpLDAPadmin installation by going to [http://localhost/phpldapadmin/](http://localhost/phpldapadmin/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PhpLDAPadmin&oldid=388048](https://wiki.archlinux.org/index.php?title=PhpLDAPadmin&oldid=388048)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")