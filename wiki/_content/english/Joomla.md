[Joomla!](https://www.joomla.org/) is a free and open-source content management system (CMS) for publishing web content. It is written in PHP, uses OOP techniques and software design patterns. The data can be stored in [MySQL](/index.php/MySQL "MySQL"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") and MS SQL databases.

Among the supported features are page caching, RSS feeds, printable versions of pages, news flashes, blogs, search, and support for language internationalization.

## Contents

*   [1 Introduction](#Introduction)
*   [2 Installation](#Installation)
    *   [2.1 In place of a PHP server](#In_place_of_a_PHP_server)
    *   [2.2 From scratch](#From_scratch)
*   [3 Configuration](#Configuration)
    *   [3.1 Apache](#Apache)
    *   [3.2 MySQL](#MySQL)
    *   [3.3 PHP](#PHP)
    *   [3.4 Joomla](#Joomla)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 The file Cache Storage is not supported on this platform](#The_file_Cache_Storage_is_not_supported_on_this_platform)
*   [5 Extra](#Extra)
    *   [5.1 Choosing between MySQL and PostgreSQL](#Choosing_between_MySQL_and_PostgreSQL)

## Introduction

In order for Joomla to function one will need the following components installed and configured:

*   An HTTP server with support for PHP(in the following example [Apache](/index.php/Apache "Apache") will be used)
*   Actual PHP libraries
*   An SQL engine(PostgreSQL, MySQL)

However don't be discouraged. It is the scope of this article: to simplify the installation & configuration to get you underway as soon as possible.

## Installation

### In place of a PHP server

[Install](/index.php/Install "Install") the [joomla](https://aur.archlinux.org/packages/joomla/) package.

### From scratch

Start by [installing](/index.php/Installing "Installing") all of the necessary packages: [apache](https://www.archlinux.org/packages/?name=apache) [php](https://www.archlinux.org/packages/?name=php) [php-apache](https://www.archlinux.org/packages/?name=php-apache) [mariadb](https://www.archlinux.org/packages/?name=mariadb)

For MySQL(MariaDB) or PostgreSQL see [#Choosing between MySQL and PostgreSQL](#Choosing_between_MySQL_and_PostgreSQL)

## Configuration

### Apache

See [Apache HTTP Server#Configuration](/index.php/Apache_HTTP_Server#Configuration "Apache HTTP Server")

After following the instructions you should have a running copy of Apache.

Now to enable PHP support we need to get back to editing `/etc/httpd/conf/httpd.conf`: PHP is known not to work with `mod_mpm_event.so` module. So we need to disable it in favor of `mod_mpm_prefork.so` like this:

```
#LoadModule mpm_event_module modules/mod_mpm_event.so
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

Now we need to add(uncomment) the following line after the `mod_dir.so` module:

```
LoadModule php7_module modules/libphp7.so

```

Add the handler:

```
AddHandler php7-script php

```

Append at the end of the `Include` list:

```
Include conf/extra/php7_module.conf

```

And we're done!

### MySQL

See [MySQL#Installation](/index.php/MySQL#Installation "MySQL")

After the base installation and configuration has been completed, it is time to perform some more detailed setup.

First, create the database for your future website:

```
$ mysqladmin -u root -p create joomla

```

The naming convention is optional, but for the sake of clarity the database will be called 'joomla'

It is recommended to avoid using root MySQL account for everyday tasks. In order to create another user one must first invoke mysql interface with:

```
$ mysql -u root -p

```

It will prompt you for MySQL's root password. If everything went OK and MySQL server is running, you sould end up with MariaDB prompt akin to this one:

```
MariaDB [(none)]>

```

In order to create a privileged user issue a following command:

```
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, \
LOCK TABLES ON joomla.* TO '$USER'@'localhost' IDENTIFIED BY '$PASSWD';

```

If you are setting up a personal server feel free to experiment with the $USER and $PASSWD values.

**Warning:**

*   The password you enter here will be saved in ~/.mysql_history;
*   It is impromptu that you get rid of the lines containing your password from that file;

Now, to apply these settings:

```
FLUSH PRIVILEGES;
quit

```

### PHP

Now to setup our PHP server. We will be running it using Apache. Edit `/etc/php/php.ini`:

A minimal config goes as follows:

*   Comment out

```
;output_buffering = 4096

```

*   Edit the following value for a more verbose error reporting

```
error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT
display_errors = On

```

*   Optional: enable logging

```
log_errors = On

```

*   Enable MySQL support(uncomment the following options):

```
extension=pdo_mysql.so
extension=mysqli.so

```

To test whether PHP was configured properly add this line somewhere in the body of a simple html page file:

<?php echo '

Hello World

'; ?>

Save this as some_page.php

Now restart httpd and navigate to [http://localhost/some_page.php](http://localhost/some_page.php)

### Joomla

By now you should have a working instance of Apache with PHP and MySQL up and running.

Now to get started with joomla, copy the contents of /usr/share/webapps/joomla to your document root.

Navigate to your [localhost](http://localhost/)

You should be presented with the Joomla! installation screen.

## Troubleshooting

**Note:** This section is intended for troubleshooting joomla-related issues. For generic issues see: [Apache#Troubleshooting](/index.php/Apache#Troubleshooting "Apache") and [MySQL#Troubleshooting](/index.php/MySQL#Troubleshooting "MySQL")

### The file Cache Storage is not supported on this platform

It is most likely that Apache doesn't have write permissions on $DocumentRoot/cache

Since by default Apache is ran as 'http' user, those must be tweaked accordingly for `$DocumentRoot/cache` and `$DocumentRoot/administrator/cache`

## Extra

### Choosing between MySQL and PostgreSQL

When choosing between [MySQL](https://en.wikipedia.org/wiki/MySQL "wikipedia:MySQL")(MariaDB) and [PostgreSQL](https://en.wikipedia.org/wiki/PostgreSQL "wikipedia:PostgreSQL") one should consider that MySQL's design is supposed to be fast and light vs more solid all-in-one PostgreSQL approach. For the purpose of this article MySQL was chosen because:

*   it is more lightweight
*   it is licensed under GPL(vs MIT)