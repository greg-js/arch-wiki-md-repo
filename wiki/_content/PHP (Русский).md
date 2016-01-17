# PHP (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта статья или раздел нуждается в [переводе](/index.php/ArchWiki:Contributing_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9F.D0.B5.D1.80.D0.B5.D0.B2.D0.BE.D0.B4 "ArchWiki:Contributing (Русский)")**

**Примечания:** Переведена только половина статьи. (обсуждение: [Talk:PHP (Русский)#](https://wiki.archlinux.org/index.php/Talk:PHP_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

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
date.timezone = Europe/Moskow

```

*   Если для отладки вашего кода вы хотите, чтобы отображались ошибки, установите опции `display_errors` в `/etc/php/php.ini` значение `On`:

```
display_errors=On

```

*   Не забудьте добавить файл индекса с расширением _.phtml_ (если вам это нужно) в `/etc/httpd/conf/extra/php5_module.conf`:

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

Для [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) запустите `# pecl install imagick`. Утилита _pecl_ доступна из пакета [php-pear](https://aur.archlinux.org/packages/php-pear/)<sup><small>AUR</small></sup>. Затем добавьте

```
extension=imagick.so

```

в `/etc/php/php.ini`.

### pthreads

Если вы хотите иметь поддержку POSIX-многопоточности, вам нужно добавить расширение pthreads. Для установки расширения ([http://pecl.php.net/package/pthreads](http://pecl.php.net/package/pthreads)) используя _pecl_ вам нужно использовать потокобезопасную версию PHP (собранную с флагом `--enable-maintainer-zts`). В настоящий момент это проще всего сделать, пересобрав основной пакет с этим флагом.

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

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Formatting and other style issues. (Discuss in [Talk:PHP (Русский)#](https://wiki.archlinux.org/index.php/Talk:PHP_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

Zend Core is the official PHP distribution provided by [zend.com](http://www.zend.com). It includes an installer/updater, zend optimizer, oracle support, and necessary libraries. However, it lacks support for postgresql, firebird, and odbc.

*   Install [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid), a FastCGI module for Apache (the official one sucks).
*   Install Zend Core (official PHP distribution)
    *   Uninstall the [php](https://www.archlinux.org/packages/?name=php) package.
    *   Download and install zend core from [[1]](http://www.zend.com/products/zend_core) ; **don't** install the bundle apache or tell it to setup your web server. It always installs to `/usr/local/Zend/Core` due to hard-coded path.
    *   Create a script `/usr/local/bin/zendcore` and create symlinks to _php_, _php-cgi_, _pear_, _phpize_ under _/usr/local/bin_  
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

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Use APCu/OPcache [https://www.archlinux.org/news/php-55-available-in-the-extra-repository/](https://www.archlinux.org/news/php-55-available-in-the-extra-repository/) (Discuss in [Talk:PHP (Русский)#](https://wiki.archlinux.org/index.php/Talk:PHP_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

*   Install APC (Alternative PHP Cache):
    *   Run `pear install pecl.php.net/apc` as superuser.
    *   Edit `/etc/php.ini`, add the line after _"; Zend Core extensions..."_ (line 1205):  
        `extension=apc.so`
*   Update Zend Core and/or install other components
    *   Just run `/usr/local/Zend/Core/setup`

## Development tools

### Komodo

Good integration for PHP+HTML+JavaScript. Lacks code formatting and unicode support in doc comments.

[Komodo IDE](http://www.activestate.com/products/komodo_ide/) | [Komodo Edit (free)](http://www.activestate.com/products/komodo_edit/)

Add custom encodings:

*   Edit `_KOMODO_INSTALL_DIR_/lib/mozilla/components/koEncodingServices.py`, line 84, add:

```
 ('cp950', 'Chinese(CP-950/Big5)', 'CP950', '', 1,'cp950'),
 ('cp936', 'Chinese(CP-936/GB2312)', 'CP936', '', 1,'cp936'),
 ('GB2312', 'Chinese(GB-2312)', 'GB2312', '', 1,'GB2312'),
 ....

```

The format is (_encoding name in python_, _description_, _short description_, BOM, _is ASCII-superset?_, _font encoding_)

### Netbeans

A complete IDE for many languages including PHP. Includes features like debugging, refactoring, code tempalting, autocomplete, XML features, and web design and development functionalities (very good CSS autocomplete functionality and PHP/JavaScript code notifications/tips).

### Eclipse PDT

[Eclipse PDT](http://www.zend.com/pdt) is not very complete at the current stage (v0.7); for instance, it cannot pop-up class list automatically when you type, though you can add custom auto-activation trigger keys.

You would need other plugins for JavaScript support and DB query.

### Zend Studio

[Zend Studio](http://www.zend.com/products/studio/) is the official PHP IDE, based on eclipse. The IDE has autocomplete, advanced code formatting, WYSIWYG html editor, refactoring, and all the eclipse features such as db access and version control integration and whatever you can get from other eclipse plugins. You can install it through [zendstudio](https://aur.archlinux.org/packages/zendstudio/)<sup><small>AUR</small></sup> package in AUR.

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

_Error Link_ plugin:

*   Symlink _zca_ to _build.zca_ (so Error Link can recognize it)
*   Install [Sunshade](http://sunshade.sourceforge.net/) plugin suite;
*   Preference -> Sunshade -> Error Link -> Add: _`^(.*\.php)\(line (\d+)\): ()(.*)`_
*   Run -> External Tools -> Open External Tools Dialog -> Select "Program" -> Clicn on "New":  
    Name: Zend Code Analyzer  
    Location: _/usr/local/bin/build.zca_  
    Working Directory: _${container_loc}_  
    Arguments: _--recursive ${resource_name}_

#### Komodo Integration

Toolbox -> Add -> New Command:

*   Command: _zca --recursive %F_
*   Run in: Command Output Tab
*   Parse output with: _`^(?P<file>.+?)\(line (?P<line>\d+)\): (?P<content>.*)$`_
*   Select _Show parsed output as a list_

## Решение проблем

### PHP Fatal error: Class 'ZipArchive' not found

Ensure the zip extension is enabled.

 `$ grep zip /etc/php/php.ini`  `extension=zip.so` 

### /etc/php/php.ini not parsed

If your php.ini isn't parsed, the ini file is named after the sapi it's using. for instance if you're using uwsgi the file would be called /etc/php/php-uwsgi.ini or if you're using cli it's /etc/php/php-cli.ini

## Смотрите также

*   [PHP Official Website](http://www.php.net/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PHP_(Русский)&oldid=415678](https://wiki.archlinux.org/index.php?title=PHP_(Русский)&oldid=415678)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Programming languages (Русский)](/index.php/Category:Programming_languages_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Programming languages (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")

Hidden categories:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")
*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")