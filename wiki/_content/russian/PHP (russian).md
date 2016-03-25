[PHP](http://www.php.net/) — широко распространенный скриптовый язык программирования общего назначения, который ориентирован главным образом для использования в веб и также может быть встроен в HTML.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Запуск](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [4 Расширения](#.D0.A0.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [4.1 gd](#gd)
    *   [4.2 imagemagick](#imagemagick)
    *   [4.3 pthreads](#pthreads)
    *   [4.4 mcrypt](#mcrypt)
    *   [4.5 PCNTL](#PCNTL)
    *   [4.6 MySQL/MariaDB](#MySQL.2FMariaDB)
*   [5 Zend Core + Apache](#Zend_Core_.2B_Apache)
*   [6 Development tools](#Development_tools)
    *   [6.1 Komodo](#Komodo)
    *   [6.2 Netbeans](#Netbeans)
    *   [6.3 Eclipse PDT](#Eclipse_PDT)
    *   [6.4 Zend Studio](#Zend_Studio)
    *   [6.5 Aptana Studio](#Aptana_Studio)
    *   [6.6 Zend Code Analyzer](#Zend_Code_Analyzer)
        *   [6.6.1 Installation](#Installation)
        *   [6.6.2 Vim Integration](#Vim_Integration)
        *   [6.6.3 Eclipse Integration](#Eclipse_Integration)
        *   [6.6.4 Komodo Integration](#Komodo_Integration)
*   [7 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [7.1 PHP Fatal error: Class 'ZipArchive' not found](#PHP_Fatal_error:_Class_.27ZipArchive.27_not_found)
    *   [7.2 /etc/php/php.ini not parsed](#.2Fetc.2Fphp.2Fphp.ini_not_parsed)
*   [8 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [php](https://www.archlinux.org/packages/?name=php), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Обратите внимание, что для запуска скриптов из обычного CGI вам также понадобится пакет [php-cgi](https://www.archlinux.org/packages/?name=php-cgi).

## Запуск

Несмотря на то, что интерпретатор PHP можно запускать как самостоятельное приложение, обычно он используется в связке с одним из веб-серверов, например [Apache HTTP Server (Русский)](/index.php/Apache_HTTP_Server_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Apache HTTP Server (Русский)"), [nginx (Русский)](/index.php/Nginx_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nginx (Русский)") или [lighttpd (Русский)](/index.php/Lighttpd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Lighttpd (Русский)").

Для запуска в качестве самостоятельного приложения используйте команду `php -S localhost:8000 -t public_html/`. Смотрите подробнее в [документации](http://docs.php.net/manual/en/features.commandline.webserver.php).

## Настройка

Основной файл настроек PHP хорошо документирован и размещен в `/etc/php/php.ini`.

*   Рекомендуется установить часовой пояс ([список часовых поясов](http://www.php.net/manual/en/timezones.php)) в `/etc/php/php.ini`:

```
date.timezone = Europe/Moscow

```

*   Если для отладки вашего кода вы хотите, чтобы отображались ошибки, установите опции `display_errors` в `/etc/php/php.ini` значение `On`:

```
display_errors=On

```

*   Не забудьте добавить файл индекса с расширением *.phtml* (если вам это нужно) в `/etc/httpd/conf/extra/php5_module.conf`:

```
DirectoryIndex index.php index.phtml index.html

```

## Расширения

Вы сможете найти множество популярных расширений для PHP в официальных репозиториях:

```
$ pacman -Ss php-

```

### gd

Для [php-gd](https://www.archlinux.org/packages/?name=php-gd) раскомментируйте следующую строку в `/etc/php/php.ini`:

```
extension=gd.so

```

### imagemagick

Для [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) запустите `# pecl install imagick`. Утилита *pecl* доступна из пакета [php-pear](https://aur.archlinux.org/packages/php-pear/). Затем добавьте

```
extension=imagick.so

```

в `/etc/php/php.ini`.

### pthreads

Если вы хотите иметь поддержку POSIX-многопоточности, вам нужно добавить расширение pthreads. Для установки расширения ([http://pecl.php.net/package/pthreads](http://pecl.php.net/package/pthreads)) используя *pecl* вам нужно использовать потокобезопасную версию PHP (собранную с флагом `--enable-maintainer-zts`). В настоящий момент это проще всего сделать, пересобрав основной пакет с этим флагом.

Инструкцию по сборке вы найдете на странице [PHP pthreads extension](/index.php/PHP_pthreads_extension "PHP pthreads extension").

### mcrypt

Если вы хотите использовать модуль `mcrypt`, установите [php-mcrypt](https://www.archlinux.org/packages/?name=php-mcrypt) и раскомментируйте следующую строку в `/etc/php/php.ini`:

```
extension=mcrypt.so

```

### PCNTL

PCNTL позволяет создать процесс напрямую на сервере. Вам пожет показаться, что это то, что вам нужно, однако имейте ввиду, что оно также дает PHP возможность натворить бед. Поэтому это расширение нельзя подключить так же удобно, как другие: все из за большого количества привелегий, которое оно делает доступным для PHP-скриптов. Чтобы его включить, придется пересобрать PHP совместно с PCNTL.

### MySQL/MariaDB

Установите и настройте MySQL/MariaDB так, как описано в [MySQL](/index.php/MySQL_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MySQL (Русский)").

Раскомментируйте [хотя бы одну](http://www.php.net/manual/en/mysqlinfo.api.choosing.php) из следующих строчек в `/etc/php/php.ini`:

```
extension=pdo_mysql.so
extension=mysqli.so

```

**Важно:** Начиная с PHP 5.5, библиотека `mysql.so` считается [устаревшей](http://www.php.net/manual/de/migration55.deprecated.php) и ее использование не рекомендуется.

Теперь вы можете добавить в базу новых пользователей с ограниченными правами для доступа к базе из ваших веб-приложений. Вы также можете ограничить доступ к базе данных, разрешив подключаться только локально: для этого раскомментируйте опцию `skip-networking` в `/etc/mysql/my.cnf`. [Перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") `mysqld.service`, чтобы изменения вступили в силу.

**Совет:** Возможно, вы захотите установить инструменты для управления базой данных [PhpMyAdmin](/index.php/PhpMyAdmin_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PhpMyAdmin (Русский)"), [Adminer](/index.php/Adminer "Adminer") или [mysql-workbench](https://www.archlinux.org/packages/?name=mysql-workbench).

## Zend Core + Apache

Zend Core is the official PHP distribution provided by [zend.com](http://www.zend.com). It includes an installer/updater, zend optimizer, oracle support, and necessary libraries. However, it lacks support for postgresql, firebird, and odbc.

*   Install [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid), a FastCGI module for Apache (the official one sucks).
*   Install Zend Core (official PHP distribution)
    *   Uninstall the [php](https://www.archlinux.org/packages/?name=php) package.
    *   Download and install zend core from [[1]](http://www.zend.com/products/zend_core) ; **don't** install the bundle apache or tell it to setup your web server. It always installs to `/usr/local/Zend/Core` due to hard-coded path.
    *   Create a script `/usr/local/bin/zendcore` and create symlinks to *php*, *php-cgi*, *pear*, *phpize* under */usr/local/bin*
        `#!/bin/bash
        export LD_LIBRARY_PATH="/usr/local/Zend/Core/lib"
        exec /usr/local/Zend/Core/bin/`basename $0` "$@"`
*   Setup Apache:
    *   In `/etc/httpd/conf/httpd.conf`, add
        `LoadModule fcgid_module modules/mod_fcgid.so
        <Directory /srv/http>
        AddHandler fcgid-script .php
        FCGIWrapper /usr/local/bin/php-cgi .php
        Options ExecCGI
        Allow from all
        </Directory>
        SocketPath /tmp/fcgidsock
        SharememPath /tmp/fcgidshm`
    *   Remember to change the Directory path
*   Disable Zend Optimizer (so you can use cache):
    *   Edit `/etc/php.ini`, uncomment the following line near the end of file:
        `zend_extension_manager.optimizer="/usr/local/Zend/Core/lib/zend/optimizer"`

*   Install APC (Alternative PHP Cache):
    *   Run `pear install pecl.php.net/apc` as superuser.
    *   Edit `/etc/php.ini`, add the line after *"; Zend Core extensions..."* (line 1205):
        `extension=apc.so`
*   Update Zend Core and/or install other components
    *   Just run `/usr/local/Zend/Core/setup`

## Development tools

### Komodo

Good integration for PHP+HTML+JavaScript. Lacks code formatting and unicode support in doc comments.

[Komodo IDE](http://www.activestate.com/products/komodo_ide/) | [Komodo Edit (free)](http://www.activestate.com/products/komodo_edit/)

Add custom encodings:

*   Edit `*KOMODO_INSTALL_DIR*/lib/mozilla/components/koEncodingServices.py`, line 84, add:

```
 ('cp950', 'Chinese(CP-950/Big5)', 'CP950', '', 1,'cp950'),
 ('cp936', 'Chinese(CP-936/GB2312)', 'CP936', '', 1,'cp936'),
 ('GB2312', 'Chinese(GB-2312)', 'GB2312', '', 1,'GB2312'),
 ....

```

The format is (*encoding name in python*, *description*, *short description*, BOM, *is ASCII-superset?*, *font encoding*)

### Netbeans

A complete IDE for many languages including PHP. Includes features like debugging, refactoring, code tempalting, autocomplete, XML features, and web design and development functionalities (very good CSS autocomplete functionality and PHP/JavaScript code notifications/tips).

### Eclipse PDT

[Eclipse PDT](http://www.zend.com/pdt) is not very complete at the current stage (v0.7); for instance, it cannot pop-up class list automatically when you type, though you can add custom auto-activation trigger keys.

You would need other plugins for JavaScript support and DB query.

### Zend Studio

[Zend Studio](http://www.zend.com/products/studio/) is the official PHP IDE, based on eclipse. The IDE has autocomplete, advanced code formatting, WYSIWYG html editor, refactoring, and all the eclipse features such as db access and version control integration and whatever you can get from other eclipse plugins. You can install it through [zendstudio](https://aur.archlinux.org/packages/zendstudio/) package in AUR.

### Aptana Studio

A good IDE for programming in PHP and web development. The current version (3.2.2) does not have a PHP debugger.

### Zend Code Analyzer

A PHP code analyzer from Zend Studio. The program is indispensable for any serious PHP coding.

#### Installation

*   Download and install Zend Studio Neon
*   In the installation dir, run `find . -name "ZendCodeAnalyzer` to get the path.
*   Copy ZendCodeAnalyzer to `/usr/local/bin/zca`
*   Now you can remove zend studio; you won't need a key or anything.

#### Vim Integration

Add the following lines into your `.vimrc`:

```
autocmd FileType php setlocal makeprg=zca\ %<.php
autocmd FileType php setlocal errorformat=%f(line\ %l):\ %m

```

#### Eclipse Integration

*Error Link* plugin:

*   Symlink *zca* to *build.zca* (so Error Link can recognize it)
*   Install [Sunshade](http://sunshade.sourceforge.net/) plugin suite;
*   Preference -> Sunshade -> Error Link -> Add: *`^(.*\.php)\(line (\d+)\): ()(.*)`*
*   Run -> External Tools -> Open External Tools Dialog -> Select "Program" -> Clicn on "New":
    Name: Zend Code Analyzer
    Location: */usr/local/bin/build.zca*
    Working Directory: *${container_loc}*
    Arguments: *--recursive ${resource_name}*

#### Komodo Integration

Toolbox -> Add -> New Command:

*   Command: *zca --recursive %F*
*   Run in: Command Output Tab
*   Parse output with: *`^(?P<file>.+?)\(line (?P<line>\d+)\): (?P<content>.*)$`*
*   Select *Show parsed output as a list*

## Решение проблем

### PHP Fatal error: Class 'ZipArchive' not found

Ensure the zip extension is enabled.

 `$ grep zip /etc/php/php.ini`  `extension=zip.so` 

### /etc/php/php.ini not parsed

If your php.ini isn't parsed, the ini file is named after the sapi it's using. for instance if you're using uwsgi the file would be called /etc/php/php-uwsgi.ini or if you're using cli it's /etc/php/php-cli.ini

## Смотрите также

*   [PHP Official Website](http://www.php.net/)