# Apache HTTP Server (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Ссылки по теме

*   [PHP](/index.php/PHP "PHP")
*   [MySQL (Русский)](/index.php/MySQL_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MySQL (Русский)")
*   [PhpMyAdmin (Русский)](/index.php/PhpMyAdmin_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PhpMyAdmin (Русский)")
*   [Adminer](/index.php/Adminer "Adminer")
*   [Xampp (Русский)](/index.php/Xampp_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xampp (Русский)")
*   [mod_perl](/index.php/Mod_perl "Mod perl")

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**Информация в этой статье или разделе устарела**

**Причина:** в английской версии накопилось много изменений ([Обсудить](https://wiki.archlinux.org/index.php/Talk:Apache_HTTP_Server_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

[Apache HTTP Server](https://en.wikipedia.org/wiki/ru:Apache "wikipedia:ru:Apache"), или сокращенно Apache — популярный веб-сервер, разработанный Apache Software Foundation.

Apache часто используется вместе с языком сценариев PHP и СУБД MySQL. Такую комбинацию обычно называют [LAMP](https://en.wikipedia.org/wiki/ru:LAMP "wikipedia:ru:LAMP") (**L**inux, **A**pache, **M**ySQL, **P**HP). Эта статья объясняет, как настроить Apache и как интегрировать с ним [PHP](/index.php/PHP "PHP") и [MySQL](/index.php/MySQL "MySQL").

Если вам нужно быстро создать окружение для разработки и тестирования, то можете просто установить [Xampp](/index.php/Xampp_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xampp (Русский)").

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Дополнительные опции](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BE.D0.BF.D1.86.D0.B8.D0.B8)
    *   [2.2 Пользовательские каталоги](#.D0.9F.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D0.BA.D0.B8.D0.B5_.D0.BA.D0.B0.D1.82.D0.B0.D0.BB.D0.BE.D0.B3.D0.B8)
    *   [2.3 TLS/SSL](#TLS.2FSSL)
    *   [2.4 Виртуальные хосты](#.D0.92.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.85.D0.BE.D1.81.D1.82.D1.8B)
        *   [2.4.1 Управление большим количеством виртуальных хостов](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B1.D0.BE.D0.BB.D1.8C.D1.88.D0.B8.D0.BC_.D0.BA.D0.BE.D0.BB.D0.B8.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.BE.D0.BC_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D1.85.D0.BE.D1.81.D1.82.D0.BE.D0.B2)
*   [3 Расширения](#.D0.A0.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [3.1 PHP](#PHP)
        *   [3.1.1 Дополнительные параметры](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D1.8B)
        *   [3.1.2 Использование php5 c php-fpm и mod_proxy_fcgi](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_php5_c_php-fpm_.D0.B8_mod_proxy_fcgi)
        *   [3.1.3 Использование php5 c apache2-mpm-worker и mod_fcgid](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_php5_c_apache2-mpm-worker_.D0.B8_mod_fcgid)
        *   [3.1.4 MySQL/MariaDB](#MySQL.2FMariaDB)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Просмотр журнала и текущего состояния Apache](#.D0.9F.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_.D0.B6.D1.83.D1.80.D0.BD.D0.B0.D0.BB.D0.B0_.D0.B8_.D1.82.D0.B5.D0.BA.D1.83.D1.89.D0.B5.D0.B3.D0.BE_.D1.81.D0.BE.D1.81.D1.82.D0.BE.D1.8F.D0.BD.D0.B8.D1.8F_Apache)
    *   [4.2 PID file /run/httpd/httpd.pid not readable (yet?) after start](#PID_file_.2Frun.2Fhttpd.2Fhttpd.pid_not_readable_.28yet.3F.29_after_start)
    *   [4.3 Обновление с Apache 2.2 до 2.4](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81_Apache_2.2_.D0.B4.D0.BE_2.4)
    *   [4.4 Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe](#Apache_is_running_a_threaded_MPM.2C_but_your_PHP_Module_is_not_compiled_to_be_threadsafe)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [apache](https://www.archlinux.org/packages/?name=apache), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

## Настройка

Файлы настроек Apache находятся в `/etc/httpd/conf`. Основным файлом является `/etc/httpd/conf/httpd.conf`, который может по ссылкам включать в себя дополнительные файлы с настройками. В большинстве случаев, будет достаточно стандартных настроек из этого файла. По умолчанию, корневым каталогом веб-сервера является `/srv/http`.

Для старта Apache, [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `httpd.service`.

После этих действий Apache должен запуститься. Проверьте, работает ли он, набрав в адресной строке браузера `[http://localhost/](http://localhost/)`. Веб-сервер должен отправить вам простую тестовую страничку.

При необходимости дальнейшей настройки сервера смотрите следующие разделы.

### Дополнительные опции

Следующие опции (_директивы_) в `/etc/httpd/conf/httpd.conf` могут быть вам интересны:

```
User http
Group http

```

По соображениям безопасности, при запуске сервера Apache от имени суперпользователя (напрямую или через скрипт инициализации) происходит смена идентификаторов группы и пользователя (UID), от имени которых выполняется процесс сервера. По умолчанию, используется группа `http` и пользователь `http`, которые не имеют привилегированных полномочий в системе.

```
Listen 80

```

Это порт, на котором Apache принимает входящие соединения. Если сервер имеет выход в интернет через маршрутизатор, необходимо будет настроить перенаправление этого порта.

Если вы используете Apache для разработки и тестирования, вы можете разрешить только локальный доступ к нему. Для этого укажите `Listen 127.0.0.1:80`.

```
ServerAdmin you@example.com

```

Страница ошибки Apache может содержать указанный почтовый адрес администратора веб-сервера.

```
DocumentRoot "/srv/http"

```

Это корневая директория Apache, в которой можно разместить ваши веб-страницы.

Измените ее, если нужно, но не забудьте также поменять путь в директиве `<Directory "/srv/http">` на новое расположение `DocumentRoot`, иначе вы, скорее всего, получите сообщение об ошибке **403 Error** (недостаточно полномочий) при попытке получить доступ к новому корневому каталогу Apache. Также не забудьте изменить строку `Require all denied`, иначе снова получите ошибку **403 Error**.

```
AllowOverride None

```

Запрещает переопределение настроек. Если в секции `<Directory>` указана эта директива, Apache будет полностью игнорировать файлы `.htaccess` в каталоге. Если вы собираетесь использовать `mod_rewrite` или указывать какие-то дополнительные настройки в файлах `.htaccess`, вы можете разрешить только определенные директивы, которые могут изменять конфигурацию сервера. Для получения дополнительной информации обратитесь к [документации Apache](http://httpd.apache.org/docs/current/mod/core.html#allowoverride).

**Совет:** Вы можете проверить корректность настроек Apache без запуска самого сервера командой `apachectl configtest`.

Дополнительные настройки можно найти в `/etc/httpd/conf/extra/httpd-default.conf`:

Чтобы отключить вывод версии Apache в генерируемых сервером страницах, укажите:

```
ServerSignature Off

```

Чтобы убрать вывод версий Apache и подключенных модулей в HTTP-заголовках ответов, добавьте:

```
ServerTokens Prod

```

### Пользовательские каталоги

По умолчанию, доступ к каталогам пользователей возможен по адресу `http://localhost/~''user''/`, который показывает содержимое каталога `~/public_html` (его имя и расположение задается в файле `/etc/httpd/conf/extra/httpd-userdir.conf`).

Если вы не хотите, чтобы пользовательские каталоги были доступны через web, закомментируйте следующую строку в `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/httpd-userdir.conf

```

Убедитесь, что права доступа к вашему домашнему каталогу и `~/public_html` позволяют получать доступ к файлам в них **всем** другим пользователям:

```
$ chmod o+x ~
$ chmod o+x ~/public_html

```

Однако с точки зрения безопасности вышеприведенное решение слишком фривольно. Правильнее поступить по-другому. Сначала добавьте пользователя **http** в группу, которой принадлежит ваша домашняя папка. Например, если ваша домашняя папка и все ее подкаталоги принадлежат группе **piter**, можно проделать следующее:

```
# usermod -aG piter http

```

или

```
# gpasswd -a http piter

```

После этого назначьте права на _чтение_ и _исполнение_ для каталогов `~/`, `~/public_html` и, рекурсивно, на остальные подкаталоги для `~/public_html` для членов группы (в нашем примере для членов группы **piter**). Опираясь на нижеприведенный шаблон, осуществите эти мероприятия:

```
$ chmod g+xr-w /home/_yourusername_
$ chmod -R g+xr-w /home/_yourusername_/public_html

```

**Обратите внимание:** Таким образом, только пользователь **http** и все потенциальные пользователи группы **piter** будут иметь разделяемый доступ к вашему домашнему каталогу.

[Перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") службу `httpd.service`, чтобы изменения вступили в силу.

### TLS/SSL

Для использования TLS/SSL необходимо установить [openssl](https://www.archlinux.org/packages/?name=openssl).

Создайте закрытый ключ и запрос на получение сертификата (CSR). Также вы можете [самозаверить](https://en.wikipedia.org/wiki/ru:%D0%A1%D0%B0%D0%BC%D0%BE%D0%B7%D0%B0%D0%B2%D0%B5%D1%80%D0%B5%D0%BD%D0%BD%D1%8B%D0%B9_%D1%81%D0%B5%D1%80%D1%82%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%82 "wikipedia:ru:Самозаверенный сертификат") CSR (который создаст сертификат):

**Обратите внимание:** Вы можете настроить длину ключа в битах (`rsa_keygen_bits:2048`). Также вы можете убрать опцию `-sha256` для использования SHA-1 вместо SHA-2 или изменить время его действия в днях (`-days 365`).

```
# cd /etc/httpd/conf
# openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:2048 -out server.key
# chmod 600 server.key
# openssl req -new -sha256 -key server.key -out server.csr
# openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt

```

Теперь раскомментируйте следующие строки в `/etc/httpd/conf/httpd.conf`:

```
LoadModule ssl_module modules/mod_ssl.so
LoadModule socache_shmcb_module modules/mod_socache_shmcb.so
Include conf/extra/httpd-ssl.conf

```

[Перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") службу `httpd.service`, чтобы изменения вступили в силу.

### Виртуальные хосты

**Обратите внимание:** Вам нужно будет добавить отдельную секцию `<VirtualHost dommainame:443>` для поддержки SSL на виртуальном хосте. Пример файла можно посмотреть ниже: [#Управление большим количеством виртуальных хостов](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B1.D0.BE.D0.BB.D1.8C.D1.88.D0.B8.D0.BC_.D0.BA.D0.BE.D0.BB.D0.B8.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.BE.D0.BC_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D1.85.D0.BE.D1.81.D1.82.D0.BE.D0.B2).

Если вы хотите, чтобы Apache обслуживал не один, а несколько хостов, раскомментируйте следующую строку в файле `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/httpd-vhosts.conf

```

Укажите свои виртуальные хосты в `/etc/httpd/conf/extra/httpd-vhosts.conf`. По умолчанию, файл уже содержит подробно разобранный пример.

Для проверки виртуальных хостов на локальной машине, добавьте их виртуальные имена в ваш файл `/etc/hosts`:

```
127.0.0.1 domainname1.dom 
127.0.0.1 domainname2.dom

```

[Перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") `httpd.service`, чтобы изменения вступили в силу.

#### Управление большим количеством виртуальных хостов

Если Apache используется для обслуживания очень большого количества виртуальных хостов, вам может быть полезна возможность их легко включать и отключать. Для этого рекомендуется создавать собственный файл настроек на каждый хост и хранить все эти файлы в одном каталоге, например `/etc/httpd/conf/vhosts`.

Создайте каталог:

```
# mkdir /etc/httpd/conf/vhosts

```

Теперь создайте в нем отдельные конфигурационные файлы:

```
# nano /etc/httpd/conf/vhosts/domainname1.dom
# nano /etc/httpd/conf/vhosts/domainname2.dom
...

```

И включите эти файлы в основной файл настроек `/etc/httpd/conf/httpd.conf`:

```
#Enabled Vhosts:
Include conf/vhosts/domainname1.dom
Include conf/vhosts/domainname2.dom
...

```

Теперь можно быстро включать/отключать требуемые виртуальные хосты, просто закомментировав или раскомментировав соответствующие директивы `Include` в основном файле настроек.

Очень простой файл виртуального хоста будет выглядеть следующим образом:

 `/etc/httpd/conf/vhosts/domainname1.dom` 

```
<VirtualHost domainname1.dom:80>
    ServerAdmin webmaster@domainname1.dom
    DocumentRoot "/home/user/http/domainname1.dom"
    ServerName domainname1.dom
    ServerAlias domainname1.dom
    ErrorLog "/var/log/httpd/domainname1.dom-error_log"
    CustomLog "/var/log/httpd/domainname1.dom-access_log" common

    <Directory "/home/user/http/domainname1.dom">
        Require all granted
    </Directory>
</VirtualHost>

<VirtualHost domainname1.dom:443>
    ServerAdmin webmaster@domainname1.dom
    DocumentRoot "/home/user/http/domainname1.dom"
    ServerName domainname1.dom:443
    ServerAlias domainname1.dom:443
    ErrorLog "/var/log/httpd/domainname1.dom-error_log"
    CustomLog "/var/log/httpd/domainname1.dom-access_log" common

    <Directory "/home/user/http/domainname1.dom">
        Require all granted
    </Directory>

    SSLEngine on
    SSLCertificateFile "/etc/httpd/conf/server.crt"
    SSLCertificateKeyFile "/etc/httpd/conf/server.key"
</VirtualHost>
```

## Расширения

### PHP

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [PHP](/index.php/PHP "PHP") с пакетами [php](https://www.archlinux.org/packages/?name=php) и [php-apache](https://www.archlinux.org/packages/?name=php-apache), доступными в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

**Обратите внимание:** `libphp5.so` входящий в [php-apache](https://www.archlinux.org/packages/?name=php-apache), не работает с `mod_mpm_event` ([FS#39218](https://bugs.archlinux.org/task/39218)). Вместо него следует использовать `mod_mpm_prefork`. В противном случае, вы получите следующее сообщение об ошибке:

```
Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.  You need to recompile PHP.
AH00013: Pre-configuration failed
httpd.service: control process exited, code=exited status=1
```

Для использования `mod_mpm_prefork`, откройте `/etc/httpd/conf/httpd.conf` и поменяйте строку

 `LoadModule mpm_event_module modules/mod_mpm_event.so` 

на

 `LoadModule mpm_prefork_module modules/mod_mpm_prefork.so` Также вы можете просто использовать `mod_proxy_fcgi` (смотрите [#Использование php5 c php-fpm и mod_proxy_fcgi](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_php5_c_php-fpm_.D0.B8_mod_proxy_fcgi)).

Чтобы включить модуль PHP, добавьте следующие строки в `/etc/httpd/conf/httpd.conf`:

*   Поместите эту строку в любом месте после строки `LoadModule dir_module modules/mod_dir.so`:

```
 LoadModule php7_module modules/libphp7.so

```

*   Разместите эту строку в конце списка `Include`:

```
 Include conf/extra/php7_module.conf

```

**Обратите внимание:** Если вы не обнаружите библиотеку `libphp5.so` в каталоге (`/etc/httpd/modules`), то вероятнее всего, что вы не установили [php-apache](https://www.archlinux.org/packages/?name=php-apache).

Если ваш корневой каталог `DocumentRoot` не `/srv/http`, добавьте его в список `open_basedir` в `/etc/php/php.ini`:

```
 open_basedir=/srv/http/:/home/:/tmp/:/usr/share/pear/:_/путь/до/корневого/каталога_

```

[Перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") службу `httpd.service`, чтобы изменения вступили в силу.

Чтобы убедиться в том, что PHP настроен корректно, создайте файл `test.php` в каталоге `DocumentRoot` (то есть в `/srv/http/` или `~/public_html`) и поместите в него следующий код:

```
<?php phpinfo(); ?>

```

По адресу http://localhost/test.php или http://localhost/''~пользователь''/test.php вы должны увидеть информационную страницу PHP.

Если PHP-код не исполняется, а на странице браузера вы увидите содержимое `test.php`, проверьте добавили ли вы `Includes` в строку `Options` для вашего корневого каталога в `/etc/httpd/conf/httpd.conf`. Кроме того, убедитесь, что `TypesConfig conf/mime.types` раскомментирован в секции <IfModule mime_module>. Также можно попробовать добавить нижеследующую строку в секцию `<IfModule mime_module>` файла `httpd.conf`:

```
AddHandler application/x-httpd-php .php

```

Дополнительную информацию вы можете получить на странице [PHP](/index.php/PHP "PHP").

#### Дополнительные параметры

Рекомендуется правильно настроить вашу временную зону ([список временных зон](http://www.php.net/manual/en/timezones.php)) в `/etc/php/php.ini` по примеру:

 `date.timezone = Europe/Moscow` 

По желанию включите режим показа ошибок при отладке PHP-кода, для этого измените значение опции `display_errors` на `On` в файле `/etc/php/php.ini`:

```
display_errors=On

```

Ежели вы хотите использовать модуль `libGD`, установите [php-gd](https://www.archlinux.org/packages/?name=php-gd) и раскомментируйте `extension=gd.so` в `/etc/php/php.ini`:

**Обратите внимание:** Пакет [php-gd](https://www.archlinux.org/packages/?name=php-gd) требует [libpng](https://www.archlinux.org/packages/?name=libpng), [libjpeg-turbo](https://www.archlinux.org/packages/?name=libjpeg-turbo) и [freetype2](https://www.archlinux.org/packages/?name=freetype2).

```
extension=gd.so

```

**Обратите внимание:** Проверьте, какие расширения PHP вы раскомментируете. Подключайте только те расширения, которые необходимы и достаточны для работы.

Для использования модуля `mcrypt` установите [php-mcrypt](https://www.archlinux.org/packages/?name=php-mcrypt) и раскомментируйте `extension=mcrypt.so` в `/etc/php/php.ini`:

```
extension=mcrypt.so

```

Не забудьте добавить индексные файлы `/etc/httpd/conf/extra/php5_module.conf`, если это необходимо:

```
DirectoryIndex index.php index.phtml index.html

```

Для дополнительной настройки, пожалуйста прочтите [PHP](/index.php/PHP "PHP").

#### Использование php5 c php-fpm и mod_proxy_fcgi

**Обратите внимание:** В отличие от широко распространенной установки с ProxyPass, конфигурация прокси с SetHandler использует директивы DirectoryIndex. Это обеспечивает лучшую совместимость с программным обеспечением, разработанным для libphp5, mod_fastcgi и mod_fcgid. Если вы хотите попробовать ProxyPass, используйте такую строку: `ProxyPassMatch ^/(.*\.php(/.*)?)$ unix:/run/php-fpm/php-fpm.sock|fcgi://localhost/srv/http/$1` 

*   [Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [php-fpm](https://www.archlinux.org/packages/?name=php-fpm)

*   Задайте `listen` в `/etc/php/php-fpm.conf` следующим образом:

```
;listen = 127.0.0.1:9000
listen = /run/php-fpm/php-fpm.sock
listen.owner = http
listen.group = http

```

*   Добавьте следующие строки в `/etc/httpd/conf/httpd.conf`:

```
<FilesMatch \.php$>
    SetHandler "proxy:unix:/run/php-fpm/php-fpm.sock|fcgi://localhost/"
</FilesMatch>
<IfModule dir_module>
    DirectoryIndex index.php index.html
</IfModule>

```

*   Если у вас добавлен модуль php, уберите его, так как он больше не нужен:

```
#LoadModule php5_module modules/libphp5.so

```

*   [Перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") демон apache php-fpm:

```
# systemctl restart httpd.service php-fpm.service

```

#### Использование php5 c apache2-mpm-worker и mod_fcgid

*   Раскомментируйте следующую строку в `/etc/conf.d/apache`:

```
HTTPD=/usr/sbin/httpd.worker

```

*   Раскомментируйте следующую строку в `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/httpd-mpm.conf

```

*   [Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакеты [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid) и [php-cgi](https://www.archlinux.org/packages/?name=php-cgi), доступные в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

*   Создайте файл `/etc/httpd/conf/extra/php5_fcgid.conf` со следующим содержимым:

 `/etc/httpd/conf/extra/php5_fcgid.conf` 

```
# Required modules: fcgid_module

<IfModule fcgid_module>
	AddHandler php-fcgid .php
	AddType application/x-httpd-php .php
	Action php-fcgid /fcgid-bin/php-fcgid-wrapper
	ScriptAlias /fcgid-bin/ /srv/http/fcgid-bin/
	SocketPath /var/run/httpd/fcgidsock
	SharememPath /var/run/httpd/fcgid_shm
        # If you don't allow bigger requests many applications may fail (such as WordPress login)
        FcgidMaxRequestLen 536870912
        PHP_Fix_Pathinfo_Enable 1
        # Path to php.ini – defaults to /etc/phpX/cgi
        DefaultInitEnv PHPRC=/etc/php/
        # Number of PHP childs that will be launched. Leave undefined to let PHP decide.
        #DefaultInitEnv PHP_FCGI_CHILDREN 3
        # Maximum requests before a process is stopped and a new one is launched
        #DefaultInitEnv PHP_FCGI_MAX_REQUESTS 5000
        <Location /fcgid-bin/>
		SetHandler fcgid-script
		Options +ExecCGI
	</Location>
</IfModule>

```

*   Создайте каталог и символическую ссылку в нем на _php-cgi_:

```
# mkdir /srv/http/fcgid-bin
# ln -s /usr/bin/php-cgi /srv/http/fcgid-bin/php-fcgid-wrapper

```

*   Отредактируйте `/etc/httpd/conf/httpd.conf`:

```
#LoadModule php5_module modules/libphp5.so
LoadModule fcgid_module modules/mod_fcgid.so
Include conf/extra/php5_fcgid.conf

```

и [перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") службу `httpd.service`.

**Обратите внимание:** Так же как и в Apache 2.4 вы можете использовать [mod_proxy_fcgi](http://httpd.apache.org/docs/2.4/mod/mod_proxy_fcgi.html) вместе с PHP-FPM. Пример конфигурации вы можете найти на странице [[1]](http://wiki.apache.org/httpd/PHP-FPM).

#### MySQL/MariaDB

Следуйте инструкциям на странице [PHP (Русский)#MySQL/MariaDB](/index.php/PHP_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#MySQL.2FMariaDB "PHP (Русский)").

После выполнения настройки, [перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") службу `mysqld`, чтобы изменения вступили в силу.

## Решение проблем

### Просмотр журнала и текущего состояния Apache

Текущее состояние службы `httpd` вы можете вывести командой `systemctl status httpd`.

Лог-файлы Apache вы найдете в каталоге `/var/log/httpd`.

### PID file /run/httpd/httpd.pid not readable (yet?) after start

Если вы получаете такую ошибку, закомментируйте строку:

```
LoadModule unique_id_module modules/mod_unique_id.so

```

в файле настроек Apache.

### Обновление с Apache 2.2 до 2.4

Если вы используете `php-apache`, посмотрите инструкции к [Apache с PHP](#PHP) выше.

Управление доступом было изменено. Приведите все директивы `Order`, `Allow`, `Deny` и `Satisfy` к новому синтаксису с `Require`. [mod_access_compat](http://httpd.apache.org/docs/2.4/mod/mod_access_compat.html) позволит использовать устаревший формат на время этапа перехода.

Подробную информацию вы найдете на странице [Upgrading to 2.4 from 2.2](http://httpd.apache.org/docs/2.4/upgrading.html).

### Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe

Если не удалось запустить `php5_module` при старте `httpd.service` и вы получаете следующее сообщение об ошибке:

```
Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.  You need to recompile PHP.

```

Это значит, что Apache работает c поточным MPM, но используется не потокобезопасная версия PHP. В этом случае, следует заменить `mpm_event_module` на `mpm_prefork_module`:

 `/etc/httpd/conf/httpd.conf` 

```
# LoadModule mpm_event_module modules/mod_mpm_event.so
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

и перезапустить `httpd.service`.

*   [Официальный сайт веб-сервера Apache](http://www.apache.org/)
*   [Руководство по созданию самозаверенных сертификатов](http://www.akadia.com/services/ssh_test_certificate.html)
*   [Поиск и устранение неисправностей при настройке Apache](http://wiki.apache.org/httpd/CommonMisconfigurations)
*   [Официальный сайт MariaDB](https://mariadb.org/)
*   [Официальный сайт PHP](http://www.php.net/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Apache_HTTP_Server_(Русский)&oldid=414990](https://wiki.archlinux.org/index.php?title=Apache_HTTP_Server_(Русский)&oldid=414990)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Web server (Русский)](/index.php/Category:Web_server_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Web server (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")