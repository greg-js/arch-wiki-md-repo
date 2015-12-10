# PHP

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Pdepend](/index.php/Pdepend "Pdepend")
*   [Php-codesniffer-drupal](/index.php/Php-codesniffer-drupal "Php-codesniffer-drupal")
*   [PhpMetrics](/index.php/PhpMetrics "PhpMetrics")
*   [PHPLOC](/index.php/PHPLOC "PHPLOC")
*   [PhpDox](/index.php/PhpDox "PhpDox")

[PHP](http://www.php.net/) is a widely-used general-purpose scripting language that is especially suited for Web development and can be embedded into HTML.

## Contents

*   [1 Installation](#Installation)
*   [2 Running](#Running)
*   [3 Configuration](#Configuration)
*   [4 Extensions](#Extensions)
    *   [4.1 gd](#gd)
    *   [4.2 imagemagick](#imagemagick)
    *   [4.3 pthreads](#pthreads)
    *   [4.4 mcrypt](#mcrypt)
    *   [4.5 PCNTL](#PCNTL)
    *   [4.6 MySQL/MariaDB](#MySQL.2FMariaDB)
    *   [4.7 PostgreSQL](#PostgreSQL)
    *   [4.8 Sqlite](#Sqlite)
*   [5 Caching](#Caching)
    *   [5.1 OPCache + APCu](#OPCache_.2B_APCu)
    *   [5.2 XCache](#XCache)
*   [6 Development tools](#Development_tools)
    *   [6.1 Aptana Studio](#Aptana_Studio)
    *   [6.2 Eclipse PDT](#Eclipse_PDT)
    *   [6.3 Komodo](#Komodo)
    *   [6.4 Netbeans](#Netbeans)
    *   [6.5 Zend Studio](#Zend_Studio)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 PHP Fatal error: Class 'ZipArchive' not found](#PHP_Fatal_error:_Class_.27ZipArchive.27_not_found)
    *   [7.2 /etc/php/php.ini not parsed](#.2Fetc.2Fphp.2Fphp.ini_not_parsed)
*   [8 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [php](https://www.archlinux.org/packages/?name=php) package from the [official repositories](/index.php/Official_repositories "Official repositories").

Note that to run PHP scripts as plain CGI, you need the [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) package.

## Running

While PHP can be run standalone, it is typically used with http servers such as [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server"), [nginx](/index.php/Nginx "Nginx") and [lighttpd](/index.php/Lighttpd "Lighttpd").

To run PHP standalone issue the `php -S localhost:8000 -t public_html/` command. See [documentation](http://docs.php.net/manual/en/features.commandline.webserver.php).

## Configuration

The main PHP configuration file is well-documented and located at `/etc/php/php.ini`.

*   It is recommended to set your timezone ([list of timezones](http://www.php.net/manual/en/timezones.php)) in `/etc/php/php.ini` like so:

```
date.timezone = Europe/Berlin

```

*   If you want to display errors to debug your PHP code, change `display_errors` to `On` in `/etc/php/php.ini`:

```
display_errors=On

```

*   Remember to add a file handler for _.phtml_, if you need it, in `/etc/httpd/conf/extra/php5_module.conf`:

```
DirectoryIndex index.php index.phtml index.html

```

**Tip:** Prior to 22 November 2015, [php-composer](https://www.archlinux.org/packages/?name=php-composer) kept its settings in a separate file in `/usr/share/php-composer/php.ini`

## Extensions

A number of commonly used PHP extensions can also be found in the official repositories:

```
$ pacman -Ss php-

```

### gd

For [php-gd](https://www.archlinux.org/packages/?name=php-gd) uncomment the line in `/etc/php/php.ini`:

```
extension=gd.so

```

### imagemagick

For [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) run `# pecl install imagick`. The _pecl_ binary is included in the [php-pear](https://www.archlinux.org/packages/?name=php-pear) package. Then add

```
extension=imagick.so

```

to `/etc/php/php.ini`.

### pthreads

If you wish to have POSIX multi-threading you will need the pthreads extension. To install the pthreads ([http://pecl.php.net/package/pthreads](http://pecl.php.net/package/pthreads)) extension using `pecl` you are required to use a compiled version of PHP with the the thread safety support flag `--enable-maintainer-zts`. Currently the most clean way to do this would be to rebuild the original package with the flag.

Instruction can be found on the [PHP pthreads extension](/index.php/PHP_pthreads_extension "PHP pthreads extension") page.

### mcrypt

If you want the `mcrypt` module, install [php-mcrypt](https://www.archlinux.org/packages/?name=php-mcrypt) and uncomment the line in `/etc/php/php.ini`:

```
extension=mcrypt.so

```

### PCNTL

PCNTL allows you to create process directly into the server side machine. While this may seen as something you would want, it also gives the power to PHP to mess things up really bad. So it is a PHP extension that cannot be loaded like other more convenient extension. This is because of the great power it gives to PHP. To enable it (by default it is disabled) PCNTL has to be compiled into PHP.

### MySQL/MariaDB

Install and configure MySQL/MariaDB as described in [MariaDB](/index.php/MariaDB "MariaDB").

Uncomment [at least one](http://www.php.net/manual/en/mysqlinfo.api.choosing.php) of the following lines in `/etc/php/php.ini`:

```
extension=pdo_mysql.so
extension=mysqli.so

```

**Warning:** As of PHP 5.5, `mysql.so` is [deprecated](http://www.php.net/manual/de/migration55.deprecated.php) and will fill up your log files with error messages. It is no longer available in PHP 7.0.

You can add minor privileged MySQL users for your web scripts. You might also want to edit `/etc/mysql/my.cnf` and uncomment the `skip-networking` line so the MySQL server is only accessible by the localhost. You have to restart MySQL for changes to take effect.

**Tip:** You may want to install a tool like [phpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin"), [Adminer](/index.php/Adminer "Adminer") or [mysql-workbench](https://www.archlinux.org/packages/?name=mysql-workbench) to work with your databases.

### PostgreSQL

Install and configure [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), then install the [php-pgsql](https://www.archlinux.org/packages/?name=php-pgsql) package and uncomment the following lines in `/etc/php/php.ini`:

```
extension=pdo_pgsql.so
extension=pgsql.so

```

### Sqlite

Install and configure [Sqlite](/index.php/Sqlite "Sqlite"), then install the [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite) package and uncomment the following lines in `/etc/php/php.ini`:

```
extension=pdo_sqlite.so
extension=sqlite3.so

```

## Caching

There are two kinds of caching in PHP: _opcode_/_bytecode_ caching and _userland_/_user data_ caching. Both allow for substantial gains in applications speed, and therefore should be enabled wherever possible.

While traditionally users turned to the [Alternative PHP Cache](https://en.wikipedia.org/wiki/Alternative_PHP_Cache "wikipedia:Alternative PHP Cache") (APC) for both needs, starting with PHP 5.5 [APC was deprecated](https://www.archlinux.org/news/php-55-available-in-the-extra-repository/) in favor of [Zend OPCache](https://en.wikipedia.org/wiki/Zend_Opcache "wikipedia:Zend Opcache"), a more efficient opcode accelerator integrated to the core PHP distribution thanks to Zend releasing it as Libre software.[[1]](https://wiki.php.net/rfc/optimizerplus)

However as OPCache provides only _opcode_ caching, [APCu](https://github.com/krakjoe/apcu/) was forked from the APC codebase to provide only _userland_ caching while taking advantage of the many years of testing that had gone into it. For a combination of those two solutions, see [OPCache + APCu](#OPCache_.2B_APCu).

Another notable contender is the actively maintained [XCache](https://en.wikipedia.org/wiki/XCache "wikipedia:XCache"), developed by one of [Lighttpd](/index.php/Lighttpd "Lighttpd") authors and which provides both opcode and userland caching. See [XCache](#XCache).

### OPCache + APCu

OPCache comes bundled with the standard PHP distribution, therefore to enable it you simply have to add or uncomment the following line in your [PHP configuration file](#Configuration):

 `/etc/php/php.ini`  `zend_extension=opcache.so` 

A list of its options and suggested settings can be found in its [official entry](https://php.net/opcache) on the PHP website.

**Warning:** If you choose to apply the [suggested settings](https://secure.php.net/manual/en/opcache.installation.php#opcache.installation.recommended) its manual offers, be sure to read carefully [the first comment](https://secure.php.net/manual/en/opcache.installation.php#114567) below those instructions as well. In some configurations those settings result in errors such as `zend_mm_heap corrupted` being produced.

APCu can be installed with the [php-apcu](https://www.archlinux.org/packages/?name=php-apcu) package. You can then enable it by uncommenting the following line in `/etc/php/conf.d/apcu.ini`, or adding it to your [PHP configuration file](#Configuration):

```
extension=apcu.so

```

Its author recommends a few [suggested settings](https://github.com/krakjoe/apcu/blob/master/INSTALL), among which:

*   `apc.enabled=1` and `apc.shm_size=32M` are not really required as they represent the [default values](https://secure.php.net/manual/en/apc.configuration.php);
*   `apc.ttl=7200` on the other hand seems [rather beneficial](https://secure.php.net/manual/en/apc.configuration.php#ini.apc.ttl);
*   finally, `apc.enable_cli=1`, which although [not recommended](https://secure.php.net/manual/en/apc.configuration.php#ini.apc.enable-cli) by the manual may be required by some software such as [ownCloud](https://github.com/owncloud/core/issues/17329#issuecomment-119248944).

**Tip:** You can add those settings either to APCu's own `/etc/php/conf.d/apcu.ini` **or** directly to your [PHP configuration file](#Configuration). Just make sure not to enable the extension twice as it will result in errors being diplayed in the system logs.

### XCache

[XCache](http://xcache.lighttpd.net/) can be installed with the [php-xcache](https://www.archlinux.org/packages/?name=php-xcache) package.

It may be enabled like APCu, by uncommenting its line in `/etc/php/conf.d/xcache.ini` or by directly adding it to the [PHP configuration file](#Configuration).

## Development tools

### Aptana Studio

[Aptana Studio](http://www.aptana.com/products/studio3.html) is an IDE for programming in PHP and web development. It can be installed with the [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/)<sup><small>AUR</small></sup> package. Does not have a PHP debugger as of version 3.2.2.

### Eclipse PDT

[Eclipse PDT](http://www.eclipse.org/pdt/) is the PHP variant of Eclipse. It can be installed with the [eclipse-php](https://www.archlinux.org/packages/?name=eclipse-php) package. See [Eclipse](/index.php/Eclipse "Eclipse") for more information.

You would need other plugins for JavaScript support and DB query.

### Komodo

[Komodo](http://komodoide.com/) is an IDE with good integration for PHP+HTML+JavaScript. [Komodo Edit](http://komodoide.com/komodo-edit/) is a free editor-only variant.

### Netbeans

A complete IDE for many languages including PHP. Includes features like debugging, refactoring, code tempalting, autocomplete, XML features, and web design and development functionalities (very good CSS autocomplete functionality and PHP/JavaScript code notifications/tips). Install it with the [netbeans](https://www.archlinux.org/packages/?name=netbeans) package.

### Zend Studio

[Zend Studio](http://www.zend.com/products/studio/) is the official PHP IDE, based on eclipse. The IDE has autocomplete, advanced code formatting, WYSIWYG html editor, refactoring, and all the eclipse features such as db access and version control integration and whatever you can get from other eclipse plugins. You can install it with the [zendstudio](https://aur.archlinux.org/packages/zendstudio/)<sup><small>AUR</small></sup> package.

## Troubleshooting

### PHP Fatal error: Class 'ZipArchive' not found

Ensure the zip extension is enabled.

 `$ grep zip /etc/php/php.ini`  `extension=zip.so` 

### /etc/php/php.ini not parsed

If your `php.ini` is not parsed, the ini file is named after the sapi it is using. For instance, if you are using uwsgi, the file would be called `/etc/php/php-uwsgi.ini`. If you are using cli, it is `/etc/php/php-cli.ini`.

## See also

*   [PHP Official Website](http://www.php.net/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PHP&oldid=410888](https://wiki.archlinux.org/index.php?title=PHP&oldid=410888)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Programming languages](/index.php/Category:Programming_languages "Category:Programming languages")