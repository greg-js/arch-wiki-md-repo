Related articles

*   [Pdepend](/index.php/Pdepend "Pdepend")
*   [Php-codesniffer-drupal](/index.php/Php-codesniffer-drupal "Php-codesniffer-drupal")
*   [PhpMetrics](/index.php/PhpMetrics "PhpMetrics")
*   [PHPLOC](/index.php/PHPLOC "PHPLOC")
*   [PhpDox](/index.php/PhpDox "PhpDox")

**翻译状态：** 本文是英文页面 [PHP](/index.php/PHP "PHP") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2020-02-14，点击[这里](https://wiki.archlinux.org/index.php?title=PHP&diff=0&oldid=594211)可以查看翻译后英文页面的改动。

[PHP](https://secure.php.net/)是一种广泛使用的通用脚本语言，特别适合于 Web 开发，可嵌入到 HTML 中。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 运行](#运行)
*   [3 配置](#配置)
*   [4 扩展](#扩展)
    *   [4.1 gd](#gd)
    *   [4.2 imagemagick](#imagemagick)
    *   [4.3 多线程](#多线程)
    *   [4.4 PCNTL](#PCNTL)
    *   [4.5 MySQL/MariaDB](#MySQL/MariaDB)
    *   [4.6 Redis](#Redis)
    *   [4.7 PostgreSQL](#PostgreSQL)
    *   [4.8 Sqlite](#Sqlite)
    *   [4.9 XDebug](#XDebug)
    *   [4.10 IMAP](#IMAP)
*   [5 缓存](#缓存)
    *   [5.1 OPCache](#OPCache)
    *   [5.2 APCu](#APCu)
*   [6 开发工具](#开发工具)
    *   [6.1 Aptana Studio](#Aptana_Studio)
    *   [6.2 Eclipse PDT](#Eclipse_PDT)
    *   [6.3 Komodo](#Komodo)
    *   [6.4 Netbeans](#Netbeans)
    *   [6.5 PhpStorm](#PhpStorm)
    *   [6.6 Zend Studio](#Zend_Studio)
*   [7 Commandline tools](#Commandline_tools)
    *   [7.1 Composer](#Composer)
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
*   [8 故障排除](#故障排除)
    *   [8.1 PHP Fatal error: Class 'ZipArchive' not found](#PHP_Fatal_error:_Class_'ZipArchive'_not_found)
    *   [8.2 /etc/php/php.ini not parsed](#/etc/php/php.ini_not_parsed)
    *   [8.3 PHP Warning: PHP Startup: *<module>*: Unable to initialize module](#PHP_Warning:_PHP_Startup:_<module>:_Unable_to_initialize_module)
*   [9 参见](#参见)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [php](https://www.archlinux.org/packages/?name=php)。AUR 中也提供了老的版本，包括 [php53](https://aur.archlinux.org/packages/php53/), [php55](https://aur.archlinux.org/packages/php55/), [php56](https://aur.archlinux.org/packages/php56/), [php70](https://aur.archlinux.org/packages/php70/), [php71](https://aur.archlinux.org/packages/php71/),[php72](https://aur.archlinux.org/packages/php72/) 和 [php73](https://aur.archlinux.org/packages/php73/).

注意：要想像纯CGI那样运行PHP，你需要安装 [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) 。

## 运行

虽然PHP可以独立运行，它通常用于HTTP服务器如： [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server")([LAMP](/index.php/LAMP "LAMP") 组合), [nginx](/index.php/Nginx "Nginx"), [lighttpd](/index.php/Lighttpd "Lighttpd") 和 [Hiawatha](/index.php/Hiawatha "Hiawatha").

使用命令：“`php -S localhost:8000 -t public_html/` ”可以独立运行PHP。 见 [documentation](https://secure.php.net/manual/en/features.commandline.webserver.php).

## 配置

主要PHP配置位于 `/etc/php/php.ini`.

*   建议在`/etc/php/php.ini` 中设置所在时区([list of timezones](https://secure.php.net/manual/en/timezones.php)) 。如下:

```
date.timezone = Europe/Berlin

```

*   如果你想调试PHP时显示错误，在`/etc/php/php.ini`中将`display_errors` 设为 `On`：

```
display_errors=On

```

*   [open_basedir](http://php.net/open-basedir) 限制 PHP 可以访问的目录，可以增加安全性，但是会影响程序的正常执行。从 PHP 7.0 开始，和上游一样默认不再设置，要使用的用户请手动设置。符号链接会被解析，所以无法通过符号链接跳过限制。某些软件的 Arch 软件包，例如 `nextcloud` 和 `phpmyadmin` 安装在 `/usr/share/webapps`，然后在 `/etc/webapps` 中创建了配置文件的符号链接。设置 `open_basedir` 时请加入这两个目录。例如：

```
open_basedir = /srv/http/:/var/www/:/home/:/tmp/:/var/tmp/:/var/cache/:/usr/share/pear/:/usr/share/webapps/:/etc/webapps/

```

## 扩展

一些常用的PHP扩展也可以在官方库发现：

```
$ pacman -Ss php-

```

**Tip:** 不要编辑`/etc/php/php.ini`，扩展的启停可在 `/etc/php/conf.d` 中设置，如： (e.g. `/etc/php/conf.d/gd.ini`)

要安装 PHP 的扩展，可以在 AUR 中搜索 php-* 或 php56-*, 例如 [php-imagick](https://www.archlinux.org/packages/?name=php-imagick), [php-redis](https://www.archlinux.org/packages/?name=php-redis) [php56-mcrypt](https://aur.archlinux.org/packages/php56-mcrypt/)。

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

### 多线程

要使用 POSIX 多线程，需要 pthreads 扩展 。用 `pecl` 安装 pthreads ([http://pecl.php.net/package/pthreads](http://pecl.php.net/package/pthreads)) 扩展，需要 PHP 在编译时启用线程安全选项`--enable-maintainer-zts`. 当前最简单的方式是用需要的选项重新编译.

可在 [PHP pthreads extension](/index.php/PHP_pthreads_extension "PHP pthreads extension") 页面找到指令介绍。

### PCNTL

利用 PCNTL 可以在服务器上直接创建进程。虽然这可能是你想要的，但是这样也会让 PHP 有能力把机器搞的一团糟。所以 PHP 不能和其他扩展一样加载，要启用此扩展，需要重新编译PHP。ArchLinux 的 PHP 已经加入 "--enable-pcntl"选项，默认已经启用。

### MySQL/MariaDB

根据 [MariaDB](/index.php/MariaDB "MariaDB") 页面安装并配置 MySQL/MariaDB.

取消 `/etc/php/php.ini` 中 [下面行](https://secure.php.net/manual/en/mysqlinfo.api.choosing.php)前面的注释 :

```
extension=pdo_mysql.so
extension=mysqli.so

```

**警告:** PHP 7.0 中 [删除了](https://secure.php.net/manual/en/migration70.removed-exts-sapis.php) `mysql.so`。

可以给网络脚本最低的 MySQL 用户权限，可以编辑 `/etc/mysql/my.cnf` 取消 `skip-networking` 行的注释，这样 MySQL 服务器就只能本地访问。设置之后需要重启 MySQL。

### Redis

安装并配置 [Redis](/index.php/Redis "Redis")，然后安装 [phpredis-git](https://aur.archlinux.org/packages/phpredis-git/).

在 `/etc/php/conf.d/redis.ini` 中取消 redis 扩展的注释。同时在 `/etc/php/conf.d/igbinary.ini` 中启用(取消注释) igbinary 扩展。

### PostgreSQL

安装并配置 [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")，然后安装 [php-pgsql](https://www.archlinux.org/packages/?name=php-pgsql) 软件包并取消 `/etc/php/php.ini` 中下面几行的注释:

```
extension=pdo_pgsql
extension=pgsql

```

### Sqlite

安装并配置 [SQLite](/index.php/SQLite "SQLite")，然后安装 [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite) 软件包并取消 `/etc/php/php.ini` 中下面几行的注释:

```
extension=pdo_sqlite
extension=sqlite3

```

### XDebug

用 XDebug 可以很容易的通过修改的 var_dump() 函数进行调试，安装 [xdebug](https://www.archlinux.org/packages/?name=xdebug) 并取消 `/etc/php/conf.d/xdebug.ini` 中如下行前面的注释：

```
zend_extension=xdebug
xdebug.remote_enable=on
xdebug.remote_host=127.0.0.1
xdebug.remote_port=9000
xdebug.remote_handler=dbgp

```

### IMAP

安装 [php-imap](https://www.archlinux.org/packages/?name=php-imap) 并取消 `/etc/php/conf.d/xdebug.ini` 中如下行前面的注释:

```
 extension=imap

```

## 缓存

PHP有两种缓存： *opcode*/*bytecode* 缓存和*userland*/*user data* 缓存，这两种缓存都大幅度提升性能，因此最好开启。

*   [Zend OPCache](https://en.wikipedia.org/wiki/Zend_Opcache "wikipedia:Zend Opcache")仅提供*opcode*缓存。
*   [APCu](https://github.com/krakjoe/apcu/)仅提供*userland*缓存

### OPCache

OPCache随PHP发布，因此在[PHP configuration file](#Configuration)中开启或添加此行即可：

 `/etc/php/php.ini`  `zend_extension=opcache` 

你可在[官网](https://secure.php.net/manual/en/book.opcache.php) 找到其他设置以及建议设置。

**警告:** 如果你使用[推荐设置](https://secure.php.net/manual/en/opcache.installation.php#opcache.installation.recommended)，要确保你一仔细看过[说明](https://secure.php.net/manual/en/opcache.installation.php#114567)，某些情况下可能导致如下错误：`zend_mm_heap corrupted`。

### APCu

通过 [php-apcu](https://www.archlinux.org/packages/?name=php-apcu) 软件包安装 APCu, 然后在 `/etc/php/conf.d/apcu.ini` 中取消下面行的注释：

```
extension=apcu.so

```

作者 [建议进行一些设置](https://github.com/krakjoe/apcu/blob/master/INSTALL):

*   `apc.enabled=1` 和 `apc.shm_size=32M` 并不是必须的，因为这已经是 [默认值](https://secure.php.net/manual/en/apc.configuration.php);
*   `apc.ttl=7200` 看上去 [很有效](https://secure.php.net/manual/en/apc.configuration.php#ini.apc.ttl);
*   最后, `apc.enable_cli=1`, 虽然手册上 [不建议启用](https://secure.php.net/manual/en/apc.configuration.php#ini.apc.enable-cli)，有些软件比如 [ownCloud](https://github.com/owncloud/core/issues/17329#issuecomment-119248944) 需要这个选项.

**Tip:** 可以将设置加入 APCu 自己的 `/etc/php/conf.d/apcu.ini` 或直接加到住配置文件，只需要注意不要同时加入。

## 开发工具

*   **Visual Studio Code** — 支持 PHP 等多种语言的开发编辑器。

	[https://code.visualstudio.com/](https://code.visualstudio.com/) || [visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/)

### Aptana Studio

[Aptana Studio](http://www.aptana.com/products/studio3.html) 是一个用于PHP和网页开发的IDE. 它能通过 [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/) 包来安装. 没有3.2.2版本的PHP调试器.

### Eclipse PDT

[Eclipse PDT](http://www.eclipse.org/pdt/) 是eclipse的PHP变种. 它能通过 [eclipse-php](https://www.archlinux.org/packages/?name=eclipse-php) 包来安装. 可阅览 [Eclipse](/index.php/Eclipse "Eclipse") 获取更多信息.

你可能需要其他插件来获取JavaScript支持和数据库查询.

### Komodo

[Komodo](http://komodoide.com/) 是一个集成了PHP+HTML+JavaScript的非常好的IDE. [Komodo Edit](http://komodoide.com/komodo-edit/) 是免费的只支持编辑的变种. 可以通过 [komodo-edit](https://aur.archlinux.org/packages/komodo-edit/) 安装。

### Netbeans

[NetBeans IDE](https://netbeans.org/) 是一个用于很多语言的IDE，包括PHP. 它的特性包括调试、重构、代码模板、自动补全、XML特性、网页设计和其他开发功能（包括很棒的CSS自动补全功能和PHP/JavaScript代码建议）。 可以通过 [netbeans](https://www.archlinux.org/packages/?name=netbeans) 来安装.

### PhpStorm

[JetBrains PhpStorm](https://en.wikipedia.org/wiki/PhpStorm "wikipedia:PhpStorm") 是一个商业的、跨平台PHP IDE，它基于jetbrains的intellij IDEA平台。它可以通过[phpstorm](https://aur.archlinux.org/packages/phpstorm/) 来安装, 或者通过 [phpstorm-eap](https://aur.archlinux.org/packages/phpstorm-eap/) 来进行30天免费试用 version. 你可以从jetbrains获取免费的教育许可.[[1]](https://www.jetbrains.com/student/)

### Zend Studio

[Zend Studio](http://www.zend.com/products/studio/) 是官方的基于Eclipse的PHP IDE. 这个IDE有自动补全、高级代码格式化、WYSIWYG HTML编辑器、重构和所有的Eclipse特性比如数据库访问和版本控制集成和你能从Eclipse获取的所有其他插件。你可以通过[zendstudio](https://aur.archlinux.org/packages/zendstudio/) 来安装.

## Commandline tools

### Composer

[Composer](https://getcomposer.org/) is a dependency manager for PHP. It can be installed with the [php-composer](https://www.archlinux.org/packages/?name=php-composer) package.

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

[Producer](http://getproducer.org/) is a command-line quality-assurance tool to validate, and then release, your PHP library package.

It can be installed with the [producer](https://aur.archlinux.org/packages/producer/) package.

## 故障排除

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

## 参见

*   [PHP 官方网站](http://www.php.net/)