# PHP (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Pdepend](/index.php/Pdepend "Pdepend")
*   [Php-codesniffer-drupal](/index.php/Php-codesniffer-drupal "Php-codesniffer-drupal")
*   [PhpMetrics](/index.php/PhpMetrics "PhpMetrics")
*   [PHPLOC](/index.php/PHPLOC "PHPLOC")
*   [PhpDox](/index.php/PhpDox "PhpDox")

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**本页面或部分需要翻译，部分内容可能已经与英文文章脱节。如果您希望贡献翻译，请访问[简体中文翻译组](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")。**

**附注:** please use the first argument of the template to provide more detailed indications.

[PHP](http://www.php.net/) is a widely-used general-purpose scripting language that is especially suited for Web development and can be embedded into HTML.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 运行](#.E8.BF.90.E8.A1.8C)
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
    *   [5.1 OPCache](#OPCache)
    *   [5.2 APCu](#APCu)
*   [6 Development tools](#Development_tools)
    *   [6.1 Aptana Studio](#Aptana_Studio)
    *   [6.2 Eclipse PDT](#Eclipse_PDT)
    *   [6.3 Komodo](#Komodo)
    *   [6.4 Netbeans](#Netbeans)
    *   [6.5 PhpStorm](#PhpStorm)
    *   [6.6 Zend Studio](#Zend_Studio)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 PHP Fatal error: Class 'ZipArchive' not found](#PHP_Fatal_error:_Class_.27ZipArchive.27_not_found)
    *   [7.2 /etc/php/php.ini not parsed](#.2Fetc.2Fphp.2Fphp.ini_not_parsed)
    *   [7.3 PHP Warning: PHP Startup: _<module>_: Unable to initialize module](#PHP_Warning:_PHP_Startup:_.3Cmodule.3E:_Unable_to_initialize_module)
*   [8 See also](#See_also)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 从[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")安装[php](https://www.archlinux.org/packages/?name=php) 。

注意：要想像纯CGI那样运行PHP，你需要安装 [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) 。

## 运行

While PHP can be run standalone, it is typically used with http servers such as [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server"), [nginx](/index.php/Nginx "Nginx") and [lighttpd](/index.php/Lighttpd "Lighttpd").

To run PHP standalone issue the `php -S localhost:8000 -t public_html/` command. See [documentation](https://secure.php.net/manual/en/features.commandline.webserver.php).

## Configuration

The main PHP configuration file is well-documented and located at `/etc/php/php.ini`.

*   It is recommended to set your timezone ([list of timezones](https://secure.php.net/manual/en/timezones.php)) in `/etc/php/php.ini` like so:

```
date.timezone = Europe/Berlin

```

*   If you want to display errors to debug your PHP code, change `display_errors` to `On` in `/etc/php/php.ini`:

```
display_errors=On

```

**Tip:** Prior to 22 November 2015, [php-composer](https://www.archlinux.org/packages/?name=php-composer) kept its settings in a separate file in `/usr/share/php-composer/php.ini`

## Extensions

A number of commonly used PHP extensions can also be found in the official repositories:

```
$ pacman -Ss php-

```

**Tip:** Instead of editing `/etc/php/php.ini`, a extension may be enabled/configured in the `/etc/php/conf.d` directory instead (e.g. `/etc/php/conf.d/gd.ini`)

### gd

For [php-gd](https://www.archlinux.org/packages/?name=php-gd) uncomment the line in `/etc/php/php.ini`:

```
extension=gd.so

```

### imagemagick

For [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) run `# pecl install imagick`. The _pecl_ binary is included in the [php-pear](https://aur.archlinux.org/packages/php-pear/)<sup><small>AUR</small></sup> package. Then add

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

Uncomment [the following lines](https://secure.php.net/manual/en/mysqlinfo.api.choosing.php) in `/etc/php/php.ini`:

```
extension=pdo_mysql.so
extension=mysqli.so

```

**Warning:** `mysql.so` was [removed](https://secure.php.net/manual/en/migration70.removed-exts-sapis.php) in PHP 7.0.

You can add minor privileged MySQL users for your web scripts. You might also want to edit `/etc/mysql/my.cnf` and uncomment the `skip-networking` line so the MySQL server is only accessible by the localhost. You have to restart MySQL for changes to take effect.

**Tip:** You may want to install a tool like [phpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin"), [Adminer](/index.php/Adminer "Adminer") or [mysql-workbench](https://www.archlinux.org/packages/?name=mysql-workbench) to work with your databases.

### PostgreSQL

Install and configure [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), then install the [php-pgsql](https://www.archlinux.org/packages/?name=php-pgsql) package and uncomment the following lines in `/etc/php/php.ini`:

```
extension=pdo_pgsql.so
extension=pgsql.so

```

### Sqlite

Install and configure [SQLite](/index.php/SQLite "SQLite"), then install the [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite) package and uncomment the following lines in `/etc/php/php.ini`:

```
extension=pdo_sqlite.so
extension=sqlite3.so

```

## Caching

There are two kinds of caching in PHP: _opcode_/_bytecode_ caching and _userland_/_user data_ caching. Both allow for substantial gains in applications speed, and therefore should be enabled wherever possible.

*   [Zend OPCache](https://en.wikipedia.org/wiki/Zend_Opcache "wikipedia:Zend Opcache") provides only _opcode_ caching.
*   [APCu](https://github.com/krakjoe/apcu/) provides only _userland_ caching.

For optimal caching, you should enable **both**. To do this, follow _both_ [#OPCache](#OPCache) _and_ [#APCu](#APCu).

### OPCache

OPCache comes bundled with the standard PHP distribution, therefore to enable it you simply have to add or uncomment the following line in your [PHP configuration file](#Configuration):

 `/etc/php/php.ini`  `zend_extension=opcache.so` 

A list of its options and suggested settings can be found in its [official entry](https://secure.php.net/manual/en/book.opcache.php) on the PHP website.

**Warning:** If you choose to apply the [suggested settings](https://secure.php.net/manual/en/opcache.installation.php#opcache.installation.recommended) its manual offers, be sure to read carefully [the first comment](https://secure.php.net/manual/en/opcache.installation.php#114567) below those instructions as well. In some configurations those settings result in errors such as `zend_mm_heap corrupted` being produced.

### APCu

APCu can be installed with the [php-apcu](https://www.archlinux.org/packages/?name=php-apcu) package. You can then enable it by uncommenting the following line in `/etc/php/conf.d/apcu.ini`, or adding it to your [PHP configuration file](#Configuration):

```
extension=apcu.so

```

Its author recommends a few [suggested settings](https://github.com/krakjoe/apcu/blob/master/INSTALL), among which:

*   `apc.enabled=1` and `apc.shm_size=32M` are not really required as they represent the [default values](https://secure.php.net/manual/en/apc.configuration.php);
*   `apc.ttl=7200` on the other hand seems [rather beneficial](https://secure.php.net/manual/en/apc.configuration.php#ini.apc.ttl);
*   finally, `apc.enable_cli=1`, which although [not recommended](https://secure.php.net/manual/en/apc.configuration.php#ini.apc.enable-cli) by the manual may be required by some software such as [ownCloud](https://github.com/owncloud/core/issues/17329#issuecomment-119248944).

**Tip:** You can add those settings either to APCu's own `/etc/php/conf.d/apcu.ini` **or** directly to your [PHP configuration file](#Configuration). Just make sure not to enable the extension twice as it will result in errors being diplayed in the system logs.

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

### PhpStorm

[JetBrains PhpStorm](https://en.wikipedia.org/wiki/PhpStorm "wikipedia:PhpStorm") is a commercial, cross-platform IDE for PHP built on JetBrains' IntelliJ IDEA platform. It can be installed with the [phpstorm](https://aur.archlinux.org/packages/phpstorm/)<sup><small>AUR</small></sup> package, or with [phpstorm-eap](https://aur.archlinux.org/packages/phpstorm-eap/)<sup><small>AUR</small></sup> for the 30-day trial version. You can get a free license for education from Jetbrains.[[1]](https://www.jetbrains.com/student/)

### Zend Studio

[Zend Studio](http://www.zend.com/products/studio/) is the official PHP IDE, based on eclipse. The IDE has autocomplete, advanced code formatting, WYSIWYG html editor, refactoring, and all the eclipse features such as db access and version control integration and whatever you can get from other eclipse plugins. You can install it with the [zendstudio](https://aur.archlinux.org/packages/zendstudio/)<sup><small>AUR</small></sup> package.

## Troubleshooting

### PHP Fatal error: Class 'ZipArchive' not found

Ensure the zip extension is enabled.

 `$ grep zip /etc/php/php.ini`  `extension=zip.so` 

### /etc/php/php.ini not parsed

If your `php.ini` is not parsed, the ini file is named after the sapi it is using. For instance, if you are using uwsgi, the file would be called `/etc/php/php-uwsgi.ini`. If you are using cli, it is `/etc/php/php-cli.ini`.

### PHP Warning: PHP Startup: _<module>_: Unable to initialize module

When running `php`, this error indicates that the aforementioned module is out of date. This will rarely happen in Arch Linux, since maintainers make sure core PHP and all modules be only available in compatible versions.

This might happen in conjunction with a module compiled from the [AUR](/index.php/AUR "AUR"). You usually could confirm this by looking at the dates of the files `/usr/lib/php/modules/`.

To fix, find a compatible update for your module, probably by looking up the [AUR](/index.php/AUR "AUR") using its common name.

If it applies, flag the outdated [AUR](/index.php/AUR "AUR") package as _outdated_.

## See also

*   [PHP Official Website](http://www.php.net/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PHP_(简体中文)&oldid=416319](https://wiki.archlinux.org/index.php?title=PHP_(简体中文)&oldid=416319)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [简体中文](/index.php/Category:%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87 "Category:简体中文")
*   [Programming languages（简体中文）](/index.php?title=Category:Programming_languages%EF%BC%88%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87%EF%BC%89&action=edit&redlink=1 "Category:Programming languages（简体中文） (page does not exist)")