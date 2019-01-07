[PHP](https://secure.php.net/) is a widely-used general-purpose scripting language that is especially suited for Web development and can be embedded into HTML.

## Contents

*   [1 Installation](#Installation)
*   [2 Running](#Running)
*   [3 Configuration](#Configuration)
*   [4 Extensions](#Extensions)
    *   [4.1 gd](#gd)
    *   [4.2 Imagemagick](#Imagemagick)
        *   [4.2.1 PECL](#PECL)
    *   [4.3 pthreads](#pthreads)
    *   [4.4 PCNTL](#PCNTL)
    *   [4.5 MySQL/MariaDB](#MySQL/MariaDB)
    *   [4.6 Redis](#Redis)
    *   [4.7 PostgreSQL](#PostgreSQL)
    *   [4.8 Sqlite](#Sqlite)
    *   [4.9 XDebug](#XDebug)
    *   [4.10 IMAP](#IMAP)
*   [5 Caching](#Caching)
    *   [5.1 OPCache](#OPCache)
    *   [5.2 APCu](#APCu)
*   [6 Development tools](#Development_tools)
*   [7 Commandline tools](#Commandline_tools)
    *   [7.1 Composer](#Composer)
        *   [7.1.1 Allow user-wide installations](#Allow_user-wide_installations)
    *   [7.2 Box](#Box)
    *   [7.3 PDepend](#PDepend)
    *   [7.4 PHP Coding Standards Fixer](#PHP_Coding_Standards_Fixer)
    *   [7.5 PHP-CodeSniffer](#PHP-CodeSniffer)
    *   [7.6 phpcov](#phpcov)
    *   [7.7 phpDox](#phpDox)
    *   [7.8 PHPLoc](#PHPLoc)
    *   [7.9 PhpMetrics](#PhpMetrics)
    *   [7.10 phptok](#phptok)
    *   [7.11 PHPUnit](#PHPUnit)
    *   [7.12 PHPUnit Skeleton Generator](#PHPUnit_Skeleton_Generator)
    *   [7.13 Producer](#Producer)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 PHP Fatal error: Class 'ZipArchive' not found](#PHP_Fatal_error:_Class_'ZipArchive'_not_found)
    *   [8.2 /etc/php/php.ini not parsed](#/etc/php/php.ini_not_parsed)
    *   [8.3 PHP Warning: PHP Startup: *<module>*: Unable to initialize module](#PHP_Warning:_PHP_Startup:_<module>:_Unable_to_initialize_module)
*   [9 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [php](https://www.archlinux.org/packages/?name=php) package from the [official repositories](/index.php/Official_repositories "Official repositories").

You can find older versions of PHP in the AUR including [php53](https://aur.archlinux.org/packages/php53/), [php55](https://aur.archlinux.org/packages/php55/), [php56](https://aur.archlinux.org/packages/php56/), [php70](https://aur.archlinux.org/packages/php70/), and [php71](https://aur.archlinux.org/packages/php71/).

Note that to run PHP scripts as plain CGI, you need the [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) package.

## Running

While PHP can be run standalone, it is typically used with http servers such as [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") (this is frequently called [LAMP](/index.php/LAMP "LAMP") setup), [nginx](/index.php/Nginx "Nginx"), [lighttpd](/index.php/Lighttpd "Lighttpd") and [Hiawatha](/index.php/Hiawatha "Hiawatha").

To run PHP standalone issue the `php -S localhost:8000 -t public_html/` command. See [documentation](https://secure.php.net/manual/en/features.commandline.webserver.php).

## Configuration

The main PHP configuration file is well-documented and located at `/etc/php/php.ini`.

*   It is recommended to set your timezone ([list of timezones](https://secure.php.net/manual/en/timezones.php)) in `/etc/php/php.ini` like so:

```
date.timezone = Europe/Berlin

```

*   If you want to display errors to debug your PHP code, change `display_errors` to `On` in `/etc/php/php.ini`:

```
display_errors = On

```

*   The [open_basedir](http://php.net/open-basedir) directive limits the paths that can be accessed by PHP, thus increasing security at the expense of potentially interfering with normal program execution. Starting with PHP 7.0, it is [no longer set by default](https://www.archlinux.org/news/php-70-packages-released/) to more closely match upstream so users who wish to use it must configure it manually. Example:

```
open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/

```

## Extensions

A number of commonly used PHP extensions can also be found in the official repositories:

```
$ pacman -Ss php-

```

**Tip:** Instead of editing `/etc/php/php.ini`, an extension may be enabled/configured in the `/etc/php/conf.d` directory instead (e.g. `/etc/php/conf.d/gd.ini`)

Extensions for current and older versions of PHP are also available in [AUR](/index.php/AUR "AUR") under the prefix php-* and php56-*, e.g. [php-imagick](https://aur.archlinux.org/packages/php-imagick/), [php-redis](https://aur.archlinux.org/packages/php-redis/), [php56-mcrypt](https://aur.archlinux.org/packages/php56-mcrypt/).

### gd

For [php-gd](https://www.archlinux.org/packages/?name=php-gd) uncomment the line in `/etc/php/php.ini`:

```
extension=gd

```

### Imagemagick

[Install](/index.php/Install "Install") the [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) package and install one of the listed PHP extension library.

Install [php-imagick](https://aur.archlinux.org/packages/php-imagick/), it will create the file `/etc/php/conf.d/imagick.ini` to configure the extension.

#### PECL

Make sure the [php-pear](https://aur.archlinux.org/packages/php-pear/) package has been installed:

```
 # pecl install imagick

```

Create a `/etc/php/conf.d/imagick.ini` and enable the extension:

 `/etc/php/conf.d/imagick.ini`  `extension=imagick` 

### pthreads

If you wish to have POSIX multi-threading you will need the pthreads extension. To install the pthreads ([http://pecl.php.net/package/pthreads](http://pecl.php.net/package/pthreads)) extension using `pecl` you are required to use a compiled version of PHP with the the thread safety support flag `--enable-maintainer-zts`. Currently the most clean way to do this would be to rebuild the original package with the flag.

Instruction can be found on the [PHP pthreads extension](/index.php/PHP_pthreads_extension "PHP pthreads extension") page.

### PCNTL

PCNTL allows you to create process directly into the server side machine. While this may seen as something you would want, it also gives PHP the power to mess things up really badly. So it is a PHP extension that cannot be loaded like other more convenient extension. This is because of the great power it gives to PHP. To enable it PCNTL has to be compiled into PHP.

The php package on Arch Linux is currently built with "--enable-pcntl", so that it should be available by default.

### MySQL/MariaDB

Install and configure MySQL/MariaDB as described in [MariaDB](/index.php/MariaDB "MariaDB").

Uncomment [the following lines](https://secure.php.net/manual/en/mysqlinfo.api.choosing.php) in `/etc/php/php.ini`:

```
extension=pdo_mysql
extension=mysqli

```

**Note:** `extension=mysql` was [removed](https://secure.php.net/manual/en/migration70.removed-exts-sapis.php) in PHP 7.0.

You can add minor privileged MySQL users for your web scripts. You might also want to edit `/etc/mysql/my.cnf` and uncomment the `skip-networking` line so the MySQL server is only accessible by the localhost. You have to restart MySQL for changes to take effect.

### Redis

Install and configure [Redis](/index.php/Redis "Redis"), then install [phpredis-git](https://aur.archlinux.org/packages/phpredis-git/).

Uncomment the line of the package, e.g. `/etc/php/conf.d/redis.ini`.

### PostgreSQL

Install and configure [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), then install the [php-pgsql](https://www.archlinux.org/packages/?name=php-pgsql) package and uncomment the following lines in `/etc/php/php.ini`:

```
extension=pdo_pgsql
extension=pgsql

```

### Sqlite

Install and configure [SQLite](/index.php/SQLite "SQLite"), then install the [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite) package and uncomment the following lines in `/etc/php/php.ini`:

```
extension=pdo_sqlite
extension=sqlite3

```

### XDebug

XDebug allows you to easily debug php code using modified var_dump() function. Install [xdebug](https://www.archlinux.org/packages/?name=xdebug) and uncomment the lines at `/etc/php/conf.d/xdebug.ini`:

```
zend_extension=xdebug
xdebug.remote_enable=on
xdebug.remote_host=127.0.0.1
xdebug.remote_port=9000
xdebug.remote_handler=dbgp

```

**Note:** To always attempt to start a remote debugging session and connect to a debugging client it is also necessary to set `xdebug.remote_autostart=on`.

### IMAP

Install [php-imap](https://www.archlinux.org/packages/?name=php-imap) and uncomment the line at `/etc/php/php.ini`:

```
extension=imap

```

## Caching

There are two kinds of caching in PHP: *opcode*/*bytecode* caching and *userland*/*user data* caching. Both allow for substantial gains in applications speed, and therefore should be enabled wherever possible.

*   [Zend OPCache](https://en.wikipedia.org/wiki/Zend_Opcache "wikipedia:Zend Opcache") provides only *opcode* caching.
*   [APCu](https://github.com/krakjoe/apcu/) provides only *userland* caching.

### OPCache

OPCache comes bundled with the standard PHP distribution, therefore to enable it you simply have to add or uncomment the following line in your [PHP configuration file](#Configuration):

 `/etc/php/php.ini`  `zend_extension=opcache` 

A list of its options and suggested settings can be found in its [official entry](https://secure.php.net/manual/en/book.opcache.php) on the PHP website.

**Warning:** If you choose to apply the [suggested settings](https://secure.php.net/manual/en/opcache.installation.php#opcache.installation.recommended) its manual offers, be sure to read carefully [the first comment](https://secure.php.net/manual/en/opcache.installation.php#114567) below those instructions as well. In some configurations those settings result in errors such as `zend_mm_heap corrupted` being produced.

### APCu

APCu can be installed with the [php-apcu](https://www.archlinux.org/packages/?name=php-apcu) package. You can then enable it by uncommenting the following line in `/etc/php/conf.d/apcu.ini`, or adding it to your [PHP configuration file](#Configuration):

```
extension=apcu

```

Its author recommends a few [suggested settings](https://github.com/krakjoe/apcu/blob/master/INSTALL), among which:

*   `apc.enabled=1` and `apc.shm_size=32M` are not really required as they represent the [default values](https://secure.php.net/manual/en/apc.configuration.php);
*   `apc.ttl=7200` on the other hand seems [rather beneficial](https://secure.php.net/manual/en/apc.configuration.php#ini.apc.ttl);
*   finally, `apc.enable_cli=1`, which although [not recommended](https://secure.php.net/manual/en/apc.configuration.php#ini.apc.enable-cli) by the manual may be required by some software such as [ownCloud](https://github.com/owncloud/core/issues/17329#issuecomment-119248944).

**Tip:** You can add those settings either to APCu's own `/etc/php/conf.d/apcu.ini` **or** directly to your [PHP configuration file](#Configuration). Just make sure not to enable the extension twice as it will result in errors being diplayed in the system logs.

## Development tools

*   **Aptana Studio** — IDE for programming in PHP and web development. Does not have a PHP debugger.

	[http://www.aptana.com/products/studio3.html](http://www.aptana.com/products/studio3.html) || [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/)

*   **[Eclipse](/index.php/Eclipse "Eclipse") PDT** — The PHP variant of Eclipse.

	[http://www.eclipse.org/pdt/](http://www.eclipse.org/pdt/) || [eclipse-php](https://www.archlinux.org/packages/?name=eclipse-php)

*   **Komodo** — IDE with good integration for PHP+HTML+JavaScript.

	[http://komodoide.com/](http://komodoide.com/) || [komodo-ide](https://aur.archlinux.org/packages/komodo-ide/), editor only: [komodo-edit](https://aur.archlinux.org/packages/komodo-edit/)

*   **[Netbeans](/index.php/Netbeans "Netbeans")** — IDE for many languages including PHP. Includes features like debugging, refactoring, code templating, autocomplete, XML features, and web design and development functionalities.

	[https://netbeans.org/](https://netbeans.org/) || [netbeans](https://www.archlinux.org/packages/?name=netbeans)

*   **[JetBrains PhpStorm](https://en.wikipedia.org/wiki/PhpStorm "wikipedia:PhpStorm")** — Commercial, cross-platform IDE for PHP built on JetBrains' IntelliJ IDEA platform. You can get a free license for education from Jetbrains.[[1]](https://www.jetbrains.com/student/).

	[https://www.jetbrains.com/phpstorm/](https://www.jetbrains.com/phpstorm/) || [phpstorm](https://aur.archlinux.org/packages/phpstorm/), 30-day trial: [phpstorm-eap](https://aur.archlinux.org/packages/phpstorm-eap/)

*   **Zend Studio** — Official PHP IDE, based on eclipse. The IDE has autocomplete, advanced code formatting, WYSIWYG html editor, refactoring, and all the eclipse features such as db access and version control integration and whatever you can get from other eclipse plugins.

	[http://www.zend.com/products/studio/](http://www.zend.com/products/studio/) || [zendstudio](https://aur.archlinux.org/packages/zendstudio/)

## Commandline tools

### Composer

[Composer](https://getcomposer.org/) is a dependency manager for PHP. It can be installed with the [composer](https://www.archlinux.org/packages/?name=composer) package.

#### Allow user-wide installations

To allow global package installations for the current [user](/index.php/User "User") (e.g. `$ composer global require "package/name"`), you may want to specify a default location by using an [environment variable](/index.php/Environment_variable "Environment variable"):

```
PATH="$HOME/.config/composer/vendor/bin:$PATH"

```

### Box

[Box](http://box-project.github.io/box2/) is an application for building and managing Phars. It can be installed with the [php-box](https://aur.archlinux.org/packages/php-box/) package.

### PDepend

[PHP Depend](http://pdepend.org/) (pdepend) is software metrics tool for php. It can be installed with the [pdepend](https://aur.archlinux.org/packages/pdepend/) package.

### PHP Coding Standards Fixer

[PHP Coding Standards Fixer](http://cs.sensiolabs.org/) a is PSR-1 and PSR-2 Coding Standards fixer for your code. It can be installed with the [php-cs-fixer](https://aur.archlinux.org/packages/php-cs-fixer/) package.

### PHP-CodeSniffer

[PHP CodeSniffer](http://pear.php.net/package/PHP_CodeSniffer/) tokenizes PHP, JavaScript and CSS files and detects violations of a defined set of coding standards. It can be installed with the [php-codesniffer](https://aur.archlinux.org/packages/php-codesniffer/) package.

### phpcov

[phpcov](https://github.com/sebastianbergmann/phpcov) is a command-line frontend for the PHP_CodeCoverage library. It can be installed with the [phpcov](https://aur.archlinux.org/packages/phpcov/) package.

### phpDox

[phpDox](http://phpdox.de/) is the documentation generator for PHP projects. This includes, but is not limited to, API documentation. It can be installed with the [phpdox](https://aur.archlinux.org/packages/phpdox/) package.

### PHPLoc

[PHPLoc](https://github.com/sebastianbergmann/phploc/) is a tool for quickly measuring the size of a PHP project. It can be installed with the [phploc](https://aur.archlinux.org/packages/phploc/) package.

### PhpMetrics

[PhpMetrics](http://www.phpmetrics.org/) provides various metrics about PHP projects. It can be installed with the [phpmetrics](https://aur.archlinux.org/packages/phpmetrics/) package.

### phptok

[phptok](https://github.com/sebastianbergmann/phptok) is a tool for quickly dumping the tokens of a PHP sourcecode file. It can be installed with the [phptok](https://aur.archlinux.org/packages/phptok/) package.

### PHPUnit

[PHPUnit](https://phpunit.de) is a programmer-oriented testing framework for PHP. It can be installed with the [phpunit](https://aur.archlinux.org/packages/phpunit/) package.

### PHPUnit Skeleton Generator

[PHPUnit Skeleton Generator](https://github.com/sebastianbergmann/phpunit-skeleton-generator) is a tool that can generate skeleton test classes from production code classes and vice versa. It can be installed with the [phpunit-skeleton-generator](https://aur.archlinux.org/packages/phpunit-skeleton-generator/) package.

### Producer

[Producer](http://getproducer.org/) is a command-line quality-assurance tool to validate, and then release, your PHP library package. It can be installed with the [producer](https://aur.archlinux.org/packages/producer/) package.

## Troubleshooting

### PHP Fatal error: Class 'ZipArchive' not found

Ensure the zip extension is enabled.

 `/etc/php/php.ini`  `extension=zip` 

### /etc/php/php.ini not parsed

If your `php.ini` is not parsed, the ini file is named after the sapi it is using. For instance, if you are using uwsgi, the file would be called `/etc/php/php-uwsgi.ini`. If you are using cli, it is `/etc/php/php-cli.ini`.

### PHP Warning: PHP Startup: *<module>*: Unable to initialize module

When running `php`, this error indicates that the aforementioned module is out of date. This will rarely happen in Arch Linux, since maintainers make sure core PHP and all modules be only available in compatible versions.

This might happen in conjunction with a module compiled from the [AUR](/index.php/AUR "AUR"). You usually could confirm this by looking at the dates of the files `/usr/lib/php/modules/`.

To fix, find a compatible update for your module, probably by looking up the [AUR](/index.php/AUR "AUR") using its common name.

If it applies, flag the outdated [AUR](/index.php/AUR "AUR") package as *outdated*.

## See also

*   [PHP Official Website](http://www.php.net/)