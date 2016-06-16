[InvoicePlane](http://invoiceplane.com) is a self-hosted open source application for managing your quotes, invoices, clients and payments.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Database](#Database)
    *   [2.2 Web Server](#Web_Server)
        *   [2.2.1 Apache](#Apache)
        *   [2.2.2 Lighttpd](#Lighttpd)
        *   [2.2.3 Nginx](#Nginx)
    *   [2.3 Installation wizard](#Installation_wizard)
*   [3 Localization](#Localization)
*   [4 See also](#See_also)

## Installation

Install the [invoiceplane](https://aur.archlinux.org/packages/invoiceplane/) package.

## Configuration

### Database

Here is an example on how you could setup a database for Invoiceplane with [MariaDB](/index.php/MariaDB "MariaDB") called `invoiceplane` for the user `invoiceplane` identified by the password `password`:

```
CREATE DATABASE invoiceplane;
GRANT ALL PRIVILEGES ON invoiceplane.* TO invoiceplane@'localhost' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;

```

### Web Server

#### Apache

Create the [Apache](/index.php/Apache "Apache") configuration file:

 `/etc/httpd/conf/extra/invoiceplane.conf` 
```
Alias /invoiceplane "/usr/share/webapps/invoiceplane"
<Directory "/usr/share/webapps/invoiceplane">
    DirectoryIndex index.php
    AllowOverride All
    Options FollowSymlinks
    Require all granted
</Directory>

```

And include it in `/etc/httpd/conf/httpd.conf`:

```
# InvoicePlane configuration
Include conf/extra/invoiceplane.conf

```

#### Lighttpd

Make an alias for invoiceplane in your [Lighttpd](/index.php/Lighttpd "Lighttpd") configuration.

```
 alias.url = ( "/invoiceplane" => "/usr/share/webapps/invoiceplane/")

```

Then enable mod_alias, mod_fastcgi and mod_cgi in your config ( server.modules section )

#### Nginx

To get invoiceplane working with your [nginx](/index.php/Nginx "Nginx") setup, first take note of the root of the server you want to use. Supposing it is `/srv/http`, now create a symlink:

```
 # ln -s /usr/share/webapps/invoiceplane/ /srv/http/invoiceplane

```

### Installation wizard

Once database and webserver have been setup, visit the installation wizard page at [http://your-invoiceplane-domain.com/index.php/setup](http://your-invoiceplane-domain.com/index.php/setup) and follow the instructions.

## Localization

If you want to choose a different language than English visit [Translation / Localization](https://wiki.invoiceplane.com/en/1.0/system/translation-localization).

## See also

*   [Offical web page](http://invoiceplane.com)
*   [Documentation](https://github.com/InvoicePlane/InvoicePlane/wiki)