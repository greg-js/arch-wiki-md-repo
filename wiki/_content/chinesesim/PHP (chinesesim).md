**翻译状态：** 本文是英文页面 [PHP](/index.php/PHP "PHP") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-02-27，点击[这里](https://wiki.archlinux.org/index.php?title=PHP&diff=0&oldid=421404)可以查看翻译后英文页面的改动。

[PHP](http://www.php.net/)是一种广泛使用的通用脚本语言，特别适合于Web开发，可嵌入到HTML。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 运行](#.E8.BF.90.E8.A1.8C)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
*   [4 扩展](#.E6.89.A9.E5.B1.95)
    *   [4.1 gd](#gd)
    *   [4.2 imagemagick](#imagemagick)
    *   [4.3 pthreads](#pthreads)
    *   [4.4 mcrypt](#mcrypt)
    *   [4.5 PCNTL](#PCNTL)
    *   [4.6 MySQL/MariaDB](#MySQL.2FMariaDB)
    *   [4.7 PostgreSQL](#PostgreSQL)
    *   [4.8 Sqlite](#Sqlite)
    *   [4.9 XDebug](#XDebug)
*   [5 缓存](#.E7.BC.93.E5.AD.98)
    *   [5.1 OPCache](#OPCache)
    *   [5.2 APCu](#APCu)
*   [6 开发工具](#.E5.BC.80.E5.8F.91.E5.B7.A5.E5.85.B7)
    *   [6.1 Aptana Studio](#Aptana_Studio)
    *   [6.2 Eclipse PDT](#Eclipse_PDT)
    *   [6.3 Komodo](#Komodo)
    *   [6.4 Netbeans](#Netbeans)
    *   [6.5 PhpStorm](#PhpStorm)
    *   [6.6 Zend Studio](#Zend_Studio)
*   [7 Commandline tools](#Commandline_tools)
    *   [7.1 Box](#Box)
    *   [7.2 Composer](#Composer)
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
*   [8 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [8.1 PHP Fatal error: Class 'ZipArchive' not found](#PHP_Fatal_error:_Class_.27ZipArchive.27_not_found)
    *   [8.2 /etc/php/php.ini not parsed](#.2Fetc.2Fphp.2Fphp.ini_not_parsed)
    *   [8.3 PHP Warning: PHP Startup: *<module>*: Unable to initialize module](#PHP_Warning:_PHP_Startup:_.3Cmodule.3E:_Unable_to_initialize_module)
*   [9 参见](#.E5.8F.82.E8.A7.81)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 从[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")安装[php](https://www.archlinux.org/packages/?name=php) 。

注意：要想像纯CGI那样运行PHP，你需要安装 [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) 。

## 运行

虽然PHP可以独立运行，它通常用于HTTP服务器如： [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server"), [nginx](/index.php/Nginx "Nginx"), [lighttpd](/index.php/Lighttpd "Lighttpd") 和 [Hiawatha](/index.php/Hiawatha "Hiawatha").

使用命令：“`php -S localhost:8000 -t public_html/` ”可以独立运行PHP。 见 [documentation](https://secure.php.net/manual/en/features.commandline.webserver.php).

## 配置

主要PHP配置位于 `/etc/php/php.ini`.

*   I建议在`/etc/php/php.ini` 中设置所在时区([list of timezones](https://secure.php.net/manual/en/timezones.php)) 。如下:

```
date.timezone = Europe/Berlin

```

*   如果你想调试PHP时显示错误，在`/etc/php/php.ini`中将`display_errors` 设为 `On`：

```
display_errors=On

```

**Tip:** 2015-11-22 前，[php-composer](https://www.archlinux.org/packages/?name=php-composer) 的配置文件在`/usr/share/php-composer/php.ini`

*   [open_basedir](http://php.net/open-basedir) 限制 PHP 可以访问的目录，可以增加安全性。从 PHP 7.0 开始，和上游一样默认不再设置，要使用的用户请手动设置，例如：

```
open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/

```

## 扩展

一些常用的PHP扩展也可以在官方库发现：

```
$ pacman -Ss php-

```

**Tip:** 不要编辑`/etc/php/php.ini`，扩展的启停可在 `/etc/php/conf.d` 中设置，如： (e.g. `/etc/php/conf.d/gd.ini`)

### gd

欲使用 [php-gd](https://www.archlinux.org/packages/?name=php-gd) 在 `/etc/php/php.ini`中取消下列内容的注释:

```
extension=gd.so

```

### imagemagick

运行`# pecl install imagick`安装[imagemagick](https://www.archlinux.org/packages/?name=imagemagick) . *pecl* 包含于[php-pear](https://aur.archlinux.org/packages/php-pear/) 包. 在 `/etc/php/php.ini`中加入

```
extension=imagick.so

```

### pthreads

要使用POSIX多线程，需要pthreads扩展 。要使用 `pecl` 安装 pthreads ([http://pecl.php.net/package/pthreads](http://pecl.php.net/package/pthreads)) 扩展，需要 PHP 在编译时启用线程安全选项 `--enable-maintainer-zts`. 当前最简单的方式是用需要的选项重新编译.

可在 [PHP pthreads extension](/index.php/PHP_pthreads_extension "PHP pthreads extension") 页面找到指令介绍。

### mcrypt

如果想用 `mcrypt` 模块， 安装 [php-mcrypt](https://www.archlinux.org/packages/?name=php-mcrypt) 以及在`/etc/php/php.ini`中取消下面这行的注释：

```
extension=mcrypt.so

```

### PCNTL

利用 PCNTL 可以在服务器上直接创建进程。虽然这可能是你想要的，但是这样也会让 PHP 有能力把机器搞的一团糟。所以 PHP 不能和其他扩展一样加载，要启用此扩展，需要重新编译PHP。

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

### XDebug

XDebug allows you to easily debug php code using modified var_dump() function. Install [xdebug](https://www.archlinux.org/packages/?name=xdebug) and add the line at `/etc/php/php.ini`:

```
extension=xdebug.so

```

## 缓存

PHP有两种缓存： *opcode*/*bytecode* 缓存和*userland*/*user data* 缓存，这两种缓存都大幅度提升性能，因此最好开启。

*   [Zend OPCache](https://en.wikipedia.org/wiki/Zend_Opcache "wikipedia:Zend Opcache")仅提供*opcode*缓存。
*   [APCu](https://github.com/krakjoe/apcu/)仅提供*userland*缓存

要获得最佳性能，应当开启两种缓存。按照下面[#OPCache](#OPCache)和[#APCu](#APCu)的步骤操作即可。

### OPCache

OPCache随PHP发布，因此在[PHP configuration file](#Configuration)中开启或添加下面两行即可：

 `/etc/php/php.ini`  `zend_extension=opcache.so` 

你可在[官网](https://secure.php.net/manual/en/book.opcache.php) 找到其他设置以及建议设置。

**警告:** 如果你使用[推荐设置](https://secure.php.net/manual/en/opcache.installation.php#opcache.installation.recommended)，要确保你一仔细看过[说明](https://secure.php.net/manual/en/opcache.installation.php#114567)，某些情况下可能导致如下错误：`zend_mm_heap corrupted`。

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

## 开发工具

### Aptana Studio

[Aptana Studio](http://www.aptana.com/products/studio3.html) is an IDE for programming in PHP and web development. It can be installed with the [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/) package. Does not have a PHP debugger as of version 3.2.2.

### Eclipse PDT

[Eclipse PDT](http://www.eclipse.org/pdt/) is the PHP variant of Eclipse. It can be installed with the [eclipse-php](https://www.archlinux.org/packages/?name=eclipse-php) package. See [Eclipse](/index.php/Eclipse "Eclipse") for more information.

You would need other plugins for JavaScript support and DB query.

### Komodo

[Komodo](http://komodoide.com/) is an IDE with good integration for PHP+HTML+JavaScript. [Komodo Edit](http://komodoide.com/komodo-edit/) is a free editor-only variant.

### Netbeans

[NetBeans IDE](https://netbeans.org/) is a complete IDE for many languages including PHP. Includes features like debugging, refactoring, code templating, autocomplete, XML features, and web design and development functionalities (very good CSS autocomplete functionality and PHP/JavaScript code notifications/tips). Install it with the [netbeans](https://www.archlinux.org/packages/?name=netbeans) package.

### PhpStorm

[JetBrains PhpStorm](https://en.wikipedia.org/wiki/PhpStorm "wikipedia:PhpStorm") is a commercial, cross-platform IDE for PHP built on JetBrains' IntelliJ IDEA platform. It can be installed with the [phpstorm](https://aur.archlinux.org/packages/phpstorm/) package, or with [phpstorm-eap](https://aur.archlinux.org/packages/phpstorm-eap/) for the 30-day trial version. You can get a free license for education from Jetbrains.[[1]](https://www.jetbrains.com/student/)

### Zend Studio

[Zend Studio](http://www.zend.com/products/studio/) is the official PHP IDE, based on eclipse. The IDE has autocomplete, advanced code formatting, WYSIWYG html editor, refactoring, and all the eclipse features such as db access and version control integration and whatever you can get from other eclipse plugins. You can install it with the [zendstudio](https://aur.archlinux.org/packages/zendstudio/) package.

## Commandline tools

### Box

[Box](http://box-project.github.io/box2/) is an application for building and managing Phars. It can be installed with the [php-box](https://aur.archlinux.org/packages/php-box/) package.

### Composer

[Composer](https://getcomposer.org/) is a dependency manager for PHP. It can be installed with the [php-composer](https://www.archlinux.org/packages/?name=php-composer) package.

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

## 故障排除

### PHP Fatal error: Class 'ZipArchive' not found

Ensure the zip extension is enabled.

 `$ grep zip /etc/php/php.ini`  `extension=zip.so` 

### /etc/php/php.ini not parsed

If your `php.ini` is not parsed, the ini file is named after the sapi it is using. For instance, if you are using uwsgi, the file would be called `/etc/php/php-uwsgi.ini`. If you are using cli, it is `/etc/php/php-cli.ini`.

### PHP Warning: PHP Startup: *<module>*: Unable to initialize module

When running `php`, this error indicates that the aforementioned module is out of date. This will rarely happen in Arch Linux, since maintainers make sure core PHP and all modules be only available in compatible versions.

This might happen in conjunction with a module compiled from the [AUR](/index.php/AUR "AUR"). You usually could confirm this by looking at the dates of the files `/usr/lib/php/modules/`.

To fix, find a compatible update for your module, probably by looking up the [AUR](/index.php/AUR "AUR") using its common name.

If it applies, flag the outdated [AUR](/index.php/AUR "AUR") package as *outdated*.

## 参见

*   [PHP Official Website](http://www.php.net/)