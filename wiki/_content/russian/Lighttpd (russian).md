**lighttpd** - веб-сервер, разрабатываемый с расчётом на быстроту и защищённость, а также соответствие стандартам. В lighttpd есть поддержка сжатия отдаваемого содержимого «на лету», HTTP-аутентификации, перезаписи URL, SSL и автоматической балансировки нагрузки (нагрузка может автоматически распределяться по нескольким запущенным серверам lighttpd). Веб-сервер также поддерживает интерфейсы CGI, SCGI, FastCGI.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [3 CGI](#CGI)
*   [4 FastCGI](#FastCGI)
    *   [4.1 PHP](#PHP)
        *   [4.1.1 php-fpm](#php-fpm)
*   [5 SSI](#SSI)
*   [6 SSL](#SSL)
    *   [6.1 Перенаправление HTTP на HTTPS](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BD.D0.B0.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_HTTP_.D0.BD.D0.B0_HTTPS)
*   [7 Сжатие исходящих данных](#.D0.A1.D0.B6.D0.B0.D1.82.D0.B8.D0.B5_.D0.B8.D1.81.D1.85.D0.BE.D0.B4.D1.8F.D1.89.D0.B8.D1.85_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85)
    *   [7.1 Сжатие динамического контента](#.D0.A1.D0.B6.D0.B0.D1.82.D0.B8.D0.B5_.D0.B4.D0.B8.D0.BD.D0.B0.D0.BC.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D0.BA.D0.BE.D0.BD.D1.82.D0.B5.D0.BD.D1.82.D0.B0)
*   [8 Управление кешем браузера пользователя](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.B5.D1.88.D0.B5.D0.BC_.D0.B1.D1.80.D0.B0.D1.83.D0.B7.D0.B5.D1.80.D0.B0_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F)
*   [9 Виртуальные хосты](#.D0.92.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.85.D0.BE.D1.81.D1.82.D1.8B)
    *   [9.1 Использование условий](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.83.D1.81.D0.BB.D0.BE.D0.B2.D0.B8.D0.B9)
    *   [9.2 mod_simple_vhost](#mod_simple_vhost)
    *   [9.3 mod_evhost](#mod_evhost)
*   [10 Листинг директорий](#.D0.9B.D0.B8.D1.81.D1.82.D0.B8.D0.BD.D0.B3_.D0.B4.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B9)
*   [11 Ограничение доступа](#.D0.9E.D0.B3.D1.80.D0.B0.D0.BD.D0.B8.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.B0)
*   [12 Аутентификация](#.D0.90.D1.83.D1.82.D0.B5.D0.BD.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.86.D0.B8.D1.8F)
    *   [12.1 Методы](#.D0.9C.D0.B5.D1.82.D0.BE.D0.B4.D1.8B)
    *   [12.2 Backends](#Backends)
        *   [12.2.1 plain](#plain)
        *   [12.2.2 htpasswd](#htpasswd)
        *   [12.2.3 htdigest](#htdigest)
        *   [12.2.4 ldap](#ldap)
    *   [12.3 Пример конфигурации](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8)
*   [13 Кодировка по умолчанию](#.D0.9A.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
*   [14 Проксирование](#.D0.9F.D1.80.D0.BE.D0.BA.D1.81.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [14.1 Lighttpd как reverse proxy для отдачи статики](#Lighttpd_.D0.BA.D0.B0.D0.BA_reverse_proxy_.D0.B4.D0.BB.D1.8F_.D0.BE.D1.82.D0.B4.D0.B0.D1.87.D0.B8_.D1.81.D1.82.D0.B0.D1.82.D0.B8.D0.BA.D0.B8)
    *   [14.2 Распределние нагрузки с помощью Lighttpd](#.D0.A0.D0.B0.D1.81.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_Lighttpd)
*   [15 Производительность](#.D0.9F.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
    *   [15.1 HTTP Keep-Alive](#HTTP_Keep-Alive)
    *   [15.2 Обработчик событий](#.D0.9E.D0.B1.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.87.D0.B8.D0.BA_.D1.81.D0.BE.D0.B1.D1.8B.D1.82.D0.B8.D0.B9)
    *   [15.3 Обработчик сетевых соединений](#.D0.9E.D0.B1.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.87.D0.B8.D0.BA_.D1.81.D0.B5.D1.82.D0.B5.D0.B2.D1.8B.D1.85_.D1.81.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [15.4 Максимальное количество соединений](#.D0.9C.D0.B0.D0.BA.D1.81.D0.B8.D0.BC.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B5_.D0.BA.D0.BE.D0.BB.D0.B8.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.BE_.D1.81.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D0.B9)
*   [16 Примеры настроек для различных CMS](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA_.D0.B4.D0.BB.D1.8F_.D1.80.D0.B0.D0.B7.D0.BB.D0.B8.D1.87.D0.BD.D1.8B.D1.85_CMS)
    *   [16.1 phpMyAdmin](#phpMyAdmin)
    *   [16.2 Mediawiki](#Mediawiki)
        *   [16.2.1 texvc](#texvc)
        *   [16.2.2 HTTPS login](#HTTPS_login)
    *   [16.3 Drupal](#Drupal)
        *   [16.3.1 Вариант 1: server.error-handler-404](#.D0.92.D0.B0.D1.80.D0.B8.D0.B0.D0.BD.D1.82_1:_server.error-handler-404)
        *   [16.3.2 Вариант 2: mod_rewrite](#.D0.92.D0.B0.D1.80.D0.B8.D0.B0.D0.BD.D1.82_2:_mod_rewrite)
    *   [16.4 MODX](#MODX)
*   [17 См. также](#.D0.A1.D0.BC._.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

lighttpd доступ в extra репозитории

 `# pacman -S lighttpd` 

## Настройка

Настройи lighttpd находятся в файле `/etc/lighttpd/lighttpd.conf`. Настройки по умолчанию позволяют проверить работоспособность сервера.

**Tip:** Проверить правильность настроек и выявить ошибки можно с помощью команды: `$ lighttpd -t -f /etc/lighttpd/lighttpd.conf` 

По умолчанию в качестве document-root сервера служит директория `/srv/http/`.

Проверяем, существует ли пользователь http:

 `# grep http /etc/passwd` 

Если такого пользователя нет в системе, добавляем его командой:

 `# useradd -d /srv/http -r -s /bin/false -U http` 

Проверим правильность установки

```
# rc.d start lighttpd
# echo 'It works!' > /srv/http/index.html
```

Затем откройте в своём браузере адрес [http://localhost](http://localhost) и вы должны увидеть тестовую страницу.

Вы также можете добавить lighttpd в секцию DAEMONS в `/etc/rc.conf`, чтобы он загружался при старте системы.

Примеры конфигурационных файлов вы можете найти в `/usr/share/doc/lighttpd/config/`.

**Tip:** Вы можете копировать текст из примеров прямо в `/etc/lighttpd/lighttpd.conf` или разместить настройки в отдельных файлах в `/etc/lighttpd/conf.d` (предварительно создав этот каталог). Чтобы включить файл с настройками из `/etc/lighttpd/conf.d` добавьте в `/etc/lighttpd/lighttpd.conf` следующую строку: `/etc/lighttpd/lighttpd.conf`  `include "conf.d/example.conf"` 

Вы также можете включить все файлы настроек из `/etc/lighttpd/conf.d/` одной командой:

 `/etc/lighttpd/lighttpd.conf`  `include_shell "cat /etc/lighttpd/conf.d/*.conf"` 

При этом файлы будут включаться в порядке их следования в каталоге, что может привести к непредсказуемым результатам. В качетсве решения можно перед названием файла ставить цифры, например, `10-auth.conf`, `20-fastcgi.conf`, `21-fastcgi-php.conf`.

**Tip:** Для корректной обработки различных типов файлов нужно определить mime-типы: `# cp /usr/share/doc/lighttpd/config/conf.d/mime.conf /etc/lighttpd/conf.d/` 

Теперь нужно включить эти настройки в `/etc/lighttpd/lighttpd.conf`:

 `/etc/lighttpd/lighttpd.conf` 
```
include "conf.d/mime.conf"

```

**Tip:** После изменения конфигурационных файлов не забудьте перезапустить сервер: `# rc.d retsrt lighttpd` 

## CGI

**Важно:** По умолчанию lighttpd будет запускать процессы от пользователя и группы "http".

Этот модуль позволяет выполнять различные CGI программы. Пример конфигурации CGI модуля приведён ниже:

 `/etc/lighttpd/conf.d/cgi.conf` 
```
server.modules += ( "mod_alias", "mod_cgi" )

alias.url += ( "/cgi-bin" => server_root + "/cgi-bin" )
$HTTP["url"] =~ "^/cgi-bin" {
   cgi.assign = ( ".pl"  => "/usr/bin/perl",
                  ".cgi" => "/usr/bin/perl",
                  ".rb"  => "/usr/bin/ruby",
                  ".erb" => "/usr/bin/eruby",
                  ".py"  => "/usr/bin/python",
                  ".sh"  => "/bin/sh"
   )
}
```

Включаем эти настройки в `/etc/lighttpd/lighttpd.conf`:

 `/etc/lighttpd/lighttpd.conf`  `include "conf.d/cgi.conf"` 
**Tip:** Чтобы файлы с некоторым расширением исполнялись безо всякой спец. программы, просто не указывайте никакую CGI-программу: `cgi.assign = ( ".sh" => "" )` 

Файл без расширения, но имеет определённую правую часть URL:

 `cgi.assign = ( "/testfile" => "" )` 

## FastCGI

Устанавливаем FastCGI командой:

 `# pacman -S fcgi` 

Теперь у вас есть lighttpd с поддержкой fcgi.

**Важно:** По умолчанию lighttpd будет запускать процессы от пользователя и группы "http".

Следующее содержимое нужно добавить в файл конфигурации

 `/etc/lighttpd/conf.d/fastcgi.conf` 
```
server.modules += ( "mod_fastcgi" )

server.indexfiles += ( "dispatch.fcgi" ) #dispatch.fcgi if rails specified

server.error-handler-404   = "/dispatch.fcgi" #too
fastcgi.server = (
   ".fcgi" => ((
      "socket" => "/var/run/lighttpd/rails-fastcgi.sock",
      "bin-path" => "/path/to/rails/application/public/dispatch.fcgi"
   ))
)
```

Включаем этот конфиг в `/etc/lighttpd/lighttpd.conf` строкой

 `/etc/lighttpd/lighttpd.conf`  `include "conf.d/fastcgi.conf"` 

### PHP

Устанавливаем php и php-cgi

 `# pacman -S php php-cgi` 

Проверяем, что php-cgi работает:

 `$ php-cgi --version` 
```
PHP 5.3.8 with Suhosin-Patch (cgi-fcgi) (built: Sep 11 2011 10:04:49)
Copyright (c) 1997-2011 The PHP Group
Zend Engine v2.3.0, Copyright (c) 1998-2011 Zend Technologies
```

Если вы увидели похожий вывод, значит всё установлено правильно.

**Примечание:** Если вы получаете ошибки, подобные этим "*No input file found*" при попытке получить доступ к вашему php файлу, убедитесь, что следующие директивы активированы в `/etc/php/php.ini`: `/etc/php.ini` 
```
cgi.fix_pathinfo=1
open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/another/path:/second/path
```

И что файлы доступны для чтения всем:

 `# chmod -R 644` 

Чтобы lighttpd мог работать с php в `/etc/lighttpd/conf.d/fastcgi-php.conf` добавляем

 `/etc/lighttpd/conf.d/fastcgi-php.conf` 
```
server.modules += ( "mod_fastcgi" )

index-file.names += ( "index.php" )

fastcgi.server = (
   ".php" => (( 
      "bin-path" => "/usr/bin/php-cgi",
      "socket" => "/var/run/lighttpd/php-fastcgi" + PID + ".sock",
      "max-procs" => 4, # значение по умолчанию
      "bin-environment" => (
         "PHP_FCGI_CHILDREN" => "1", # значение по умолчанию
         "PHP_FCGI_MAX_REQUESTS" => "10000"
      ),
      "broken-scriptfilename" => "enable"
   ))
)

fastcgi.map-extensions = ( ".php3" => ".php", ".php4" => ".php", ".php5" => ".php", "phtml" => "php" ) # если используете разные версии php

```

Включаем этот конфиг в `/etc/lighttpd/lighttpd.conf` строкой

 `/etc/lighttpd/lighttpd.conf`  `include "conf.d/fastcgi-php.conf"` 

Проверяем работу php:

 `# echo "<?php phpinfo() ?>" > /srv/http/phpinfo.php` 

Затем откройте в своём браузере адрес [http://localhost/phpinfo.php](http://localhost/phpinfo.php) и вы должны увидеть страницу, содержащую информацию о php.

**Tip:** Если вы хотите, чтобы в html файлах обрабатывался php-код, добавьте в `fastcgi-php.conf`: `fastcgi.map-extensions = ( ".html" => ".php" )` 

#### php-fpm

В качестве альтернативы php-cgi можно использовать php-fpm. Целесообразность использования php-fpm заключается в отсутствии в последних версиях lighttpd динамической регуляции количества php процессов.

Устанавливаем php-fpm и запускаем демон:

```
# pacman -S php-fpm
# rc.d start php-fpm
```

**Примечание:** Настройки php-fpm находятся в файле `/etc/php/php-fpm.conf`. [Подробнее о настройках php-fpm](http://php-fpm.org/wiki/Configuration_File).

В `/etc/lighttpd/conf.d/fastcgi-php.conf` добавляем:

 `/etc/lighttpd/conf.d/fastcgi-php.conf` 
```
server.modules += ( "mod_fastcgi" )

index-file.names += ( "index.php" ) 

fastcgi.server = (
   ".php" => ((
      "socket" => "/var/run/php-fpm/php-fpm.sock",
      "broken-scriptfilename" => "enable"
   ))
)
```

Аналогично предыдущему описанию включаем этот конфиг в `/etc/lighttpd/lighttpd.conf` строкой

 `/etc/lighttpd/lighttpd.conf`  `include "conf.d/fastcgi-php.conf"` 
**Примечание:** Демон php-fpm необходимо запускать до lighttpd, иначе php-скрипты не будут обрабатываться (будут выдаваться ошибки 500 или 503).

## SSI

SSI (Server Side Includes — включения на стороне сервера) — несложный язык для динамической «сборки» веб-страниц на сервере из отдельных составных частей и выдачи клиенту полученного HTML-документа.

**Важно:** Если вы используете одновременно mod_ssi и mod_compress, то mod_ssi должен быть загружен **до** mod_compress.

Чтобы добавить поддержку SSI в Lighttpd добавляем следующие настройки в `/etc/lighttpd/conf.d/ssi.conf`:

 `/etc/lighttpd/conf.d/ssi.conf` 
```
server.modules += ( "mod_ssi" )

ssi.extension              = ( ".html", ".shtml" )

```

Затем

 `/etc/lighttpd/lighttpd.conf`  `include "conf.d/ssi.conf"` 

## SSL

Создаем директорию для хранения сертификатов:

 `# mkdir /etc/lighttpd/certs` 

Генерируем самоподписанный сертификат (пример команды):

 `# openssl req -x509 -nodes -days 7300 -newkey rsa:2048 -keyout /etc/lighttpd/certs/www.example.com.pem -out /etc/lighttpd/certs/www.example.com.pem` 
**Примечание:** Подробнее о создании сертификатов смотрите отдельную [статью](/index.php/OpenSSL "OpenSSL").

Выставляем владельца и нужные права:

```
# chown http:http /etc/lighttpd/certs/www.example.com.pem
# chmod 600 /etc/lighttpd/certs/www.example.com.pem
```

Теперь нужно включить SSL в настройках lighttpd (в `/etc/lighttpd/lighttpd.conf`).

Чтобы включить SSL для всего HTTP-сервера (вам также нужно указать порт сервера 443):

 `/etc/lighttpd/lighttpd.conf` 
```
ssl.engine = "enable" 
ssl.pemfile = "/etc/lighttpd/certs/www.example.com.pemm"
```

Чтобы включить SSL в дополнение к HTTP:

 `/etc/lighttpd/lighttpd.conf` 
```
$SERVER["socket"] == ":443" {
   ssl.engine = "enable" 
   ssl.pemfile = "/etc/lighttpd/certs/www.example.com.pem" 
}
```

Если вы хотите использовать другой сайт при переходе на HTTPS, вам нужно указать другую директорию в качестве document-root используя сокет (в данном случае 443 порт) в качестве условия:

 `/etc/lighttpd/lighttpd.conf` 
```
$SERVER["socket"] == ":443" {
   server.document-root = "/srv/ssl" # use your ssl directory here
   ssl.engine                 = "enable"
   ssl.pemfile                = "/etc/lighttpd/certs/www.example.com.pem"  # use the path where you created your pem file
}
```

Вы также можете использовать named-based виртуальным хостинг, чтобы реализовать несколько SSL серверов:

 `/etc/lighttpd/lighttpd.conf` 
```
$HTTP["host"] == "www.example.org" {
   ssl.pemfile = "/etc/lighttpd/certs/www.example.org.pem" 
}
$HTTP["host"] == "mail.example.org" {
   ssl.pemfile = "/etc/lighttpd/certs/mail.example.org.pem" 
}
```

**Примечание:** [SNI](https://en.wikipedia.org/wiki/Server_Name_Indication "wikipedia:Server Name Indication") поддерживается не всеми браузерами. [Подробнее](https://en.wikipedia.org/wiki/Server_Name_Indication#Support "wikipedia:Server Name Indication"). IP-based виртуальный хостинг лишён этого недостатка.

**Tip:** Некоторые php-скрипты пытаются определить HTTPS, проверяя значение переменной $_SERVER['HTTPS']. Чтобы разрешить это, вам нужно подключить модуль setenv и передать соответствующую опцию. Пример настройки: `/etc/lighttpd/lighttpd.conf` 
```
server.modules = ( ... "mod_setenv", ... )

$SERVER["socket"] == ":443" {
   ssl.engine             = "enable" 
   ssl.pemfile            = "/etc/lighttpd/server.pem" 
   setenv.add-environment = (
     "HTTPS" => "on" 
   )
}
```

### Перенаправление HTTP на HTTPS

mod_redirect должен быть включён:

 `/etc/lighttpd/lighttpd.conf`  `server.modules              = ( ... "mod_redirect", ... )` 

Перенаправляем трафик для домена example.org:

 `/etc/lighttpd/lighttpd.conf` 
```
$SERVER["socket"] == ":80" {
   $HTTP["host"] =~ "example.org" {
      url.redirect = ( "^/(.*)" => "https://example.org/$1" )
      server.name                 = "example.org" 
   }
}
```

Перенаправляем запросы на HTTPS для части сайта (в примере ниже - `/secure`):

 `/etc/lighttpd/lighttpd.conf` 
```
$SERVER["socket"] == ":80" {
   $HTTP["url"] =~ "^/secure|^/phpmyadmin" {
      url.redirect = ( "^/(.*)" => "https://example.com/$1" )
   }
}
```

Перенаправляем весь трафик на HTTPS:

 `/etc/lighttpd/lighttpd.conf` 
```
$SERVER["socket"] == ":80" {
   $HTTP["host"] =~ "(.*)" {
      url.redirect = ( "^/(.*)" => "https://%1/$1" )
   }
}
```

## Сжатие исходящих данных

Сжатие исходящих данных уменьшает нагрузку на сеть и может улучшить общую пропускную способность веб-сервера.

На сегодня поддерживается только статичное содержимое.

Сервер автоматически договаривается какой метод сжатия использовать. Поддерживается gzip, deflate, bzip.

Ограничение на размер сжимаемых файлов: от 128 байт до 128 мегабайт.

Создаём нужную директорию и задаём владельца:

```
# mkdir /var/cache/lighttpd/compress/
# chown http:http /var/cache/lighttpd/compress/
```

В `/etc/lighttpd/conf.d/compress.conf` вносим:

 `/etc/lighttpd/conf.d/compress.conf` 
```
server.modules += ( "mod_compress" )

compress.cache-dir          = "/var/cache/lighttpd/compress/"
compress.allowed-encodings  = ("bzip2", "gzip", "deflate") # значение по умолчанию
compress.filetype           = ("text/plain", "text/html", "text/javascript", "text/css", "text/xml")
```

Включаем настройки `/etc/lighttpd/conf.d/compress.conf` в `/etc/lighttpd/lighttpd.conf`

 `/etc/lighttpd/lighttpd.conf`  `include "conf.d/compress.conf"` 
**Tip:** Чтобы каталог, в котором Lighttpd хранит сжатые файлы регулярно очищался от старых, неиспользуемых файлов, можно использовать следующий скрипт в качестве задания Cron: `/etc/cron.daily/lighttpd` 
```
#!/bin/bash

find /var/cache/lighttpd/compress -type f -mtime +10 | xargs -r rm

```

В данном примере будут удалены все файлы, которые старше 10 дней.

**Tip:** Вы также можете использовать условия (имя хоста или url), чтобы задать произвольный каталог для сжатых фавйлов. `/etc/lighttpd/lighttpd.conf` 
```
$HTTP["host"] == "docs.example.org" {
   compress.cache-dir = "/srv/http/cache/docs.example.org/" 
}
```

Не забудьте установить владельцем каталога пользователя http.

### Сжатие динамического контента

Для сжатия динамического контента (PHP) в `/etc/php/php.ini` нужно включить следующую директиву:

 `/etc/php/php.ini`  `zlib.output_compression = On` 
**Tip:** Вы также можете задать уровен сжатия с помощью директивы [zlib.output_compression_level](http://www.php.net/manual/en/zlib.configuration.php).

## Управление кешем браузера пользователя

Для ускорения загрузки статических файлов можно управлять кешем браузера пользователя через заголовки Expires и Cache-Control. Для этого в Lighttpd используется mod_expire.

 `/etc/lighttpd/lighttpd.conf` 
```
server.modules += ( "mod_expire" )

expire.url = (
   "/images/"  => "access plus 7 days",
   "/themes/" => "access plus 7 days",
   "/jquery/" => "access plus 2 weeks",
)

```

Можно также перечислить отдельные расширения файлов:

 `/etc/lighttpd/lighttpd.conf` 
```
server.modules += ( "mod_expire" )

expire.url = (
   ".css" => "access plus 7 days",
   ".js" => "access plus 2 weeks",
   ".png" => "access plus 7 days",
   ".gif" => "access plus 7 days",
   ".jpg" => "access plus 7 days",
)

```

Альтернативу предыдущему листингу:

 `/etc/lighttpd/lighttpd.conf` 
```
server.modules += ( "mod_expire" )

$HTTP["url"] =~ "\.(jpe?g|gif|png|css|js)$" {
     expire.url = ( "" => "access 7 days" )
}

```

## Виртуальные хосты

### Использование условий

Первый способ заключается в изменении server.document-root в зависимости от содержимого заголовка "host".

 `/etc/lighttpd/lighttpd.conf` 
```
$HTTP["host"] == "www.example1.com" {
   server.document-root = "/srv/vhosts/www.example1.com/http"
   accesslog.filename = "/srv/vhosts/www.example1.com/access.log"
   server.error-handler-404 = "/404.php"
}

$HTTP["host"] == "www.example2.com" {
   server.document-root = "/srv/vhosts/www.example2.com/http"
   accesslog.filename = "/srv/vhosts/www.example2.com/access.log"
   server.error-handler-404 = "/404.php"
}
```

**Примечание:** Не забудьте предварительно создать необходимые каталоги и назначить им соответствующих владельцев (http:http).
```
# mkdir -p /srv/vhosts/www.exmaple1.com/http
# mkdir -p /srv/vhosts/www.exmaple2.com/http
# chown -R http:http /srv/vhosts/
```

### mod_simple_vhost

Этот способ более прост и экономичен. В указанной директории хостинга имя каждого каталога соответствует аналогичному имени вируального хоста. Внутри каждого такого каталога находится dccroot вируального хоста.

Docroot для каждого вируального хоста строится из следующих трёх значений:

*   server-root
*   hostname
*   document-root

Абсолютный путь к docroot'у строится из:

```
server-root + hostname + document-root

```

в случае если путь не существует

```
server-root + default-host + document-root

```

**Tip:** Вы можете использовать символьные ссылки чтобы соотнести несколько имён хостов одной директории.

В качестве примера приведём следующий:

 `/etc/lighttpd/conf.d/simple_vhost.conf` 
```
server.modules += ( "mod_simple_vhost" )

simple-vhost.server-root = "/srv/vhosts/"
simple-vhost.default-host = "www.example.org"
simple-vhost.document-root = "http"

```

Включаем конфигурацию из `/etc/lighttpd/conf.d/simple_vhost.conf` в `/etc/lighttpd/lighttpd.conf`:

 `/etc/lighttpd/lighttpd.conf`  `include /etc/lighttpd/conf.d/simple_vhost.conf` 

Для создания виртуального хоста достаточно создать каталог в `/srv/vhosts/` и сделать владельцем http:http. Например:

```
# mkdir -p /srv/vhosts/www.exmaple1.com/http
# chown http:http /srv/vhosts/www.exmaple1.com/http
```

### mod_evhost

Модуль evhost создаёт document-root, основываясь на шаблнах. Эти шаблоны представляют различные части запроса "host":

*   %% => % sign
*   %0 => domain name + tld
*   %1 => tld
*   %2 => domain name without tld
*   %3 => subdomain 1 name
*   %4 => subdomain 2 name
*   %_ => full domain name

 `/etc/lighttpd/lighttpd.conf` 
```
server.modules = ( ... "mod_evhost", ... )
evhost.path-pattern = "/srv/vhosts/%0/http/"
```

С помощью этого моудля можно также организовать виртуальные хосты для поддоменов:

 `/etc/lighttpd/lighttpd.conf`  `evhost.path-pattern = "/srv/vhosts/%0/http/%3/"` 

## Листинг директорий

Чтобы включить листинг для всех каталогов в `/etc/lighttpd/lighttpd.conf` укажите следующую опцию:

 `/etc/lighttpd/lighttpd.conf`  `dir-listing.activate = "enable"` 

Листинг включается для всех каталогов, в корне которых нет файлов перечисленных в директиве *index-file.names*.

Чтобы включить листинг для отдельного каталога укажите следующее:

 `/etc/lighttpd/lighttpd.conf` 
```
$HTTP["url"] =~ "^/download($|/)" {
   dir-listing.activate = "enable" 
}
```

**Tip:** Для исключения из листинга скрытых файлов используется директива dir-listing.hide-dotfiles = "enable". Список исключений, основанный на регулярных выражениях, задаётся директивой dir-listing.exclude

## Ограничение доступа

Для использования ограничения доступа необходим включить mod_access:

 `/etc/lighttpd/lighttpd,conf`  `server.modules = ( ... "mod_access", ... )` 

Ограничиваем доступ к файлам, заканчивающимся на "~" и ".inc":

 `/etc/lighttpd/lighttpd,conf`  `url.access-deny = ( "~", ".inc")` 

Запрет доступа к сайту для определённого IP:

 `/etc/lighttpd/lighttpd,conf` 
```
$HTTP["remoteip"] == "202.54.1.1" {
   url.access-deny = ( "" )
}
```

Ограничение доступа к каталогу `/libraries`:

 `/etc/lighttpd/lighttpd,conf` 
```
$HTTP["url"] =~ "^/libraries/" {
   url.access-deny = ("")
}
```

Запрет доступа к каталогу `/stats` всех кроме IP адресов 200.19.1.5 и 210.45.2.7:

 `/etc/lighttpd/lighttpd,conf` 
```
$HTTP["remoteip"] !~ "200\.19\.1\.5|210\.45\.2\.7" {
   $HTTP["url"] =~ "^/stats/" {
      url.access-deny = ( "" )
   }
}
```

Запрет доступа к файлам jpg, jpeg, png если запрос приходит не с www.example.com (защита от прямых ссылок):

 `/etc/lighttpd/lighttpd,conf` 
```
$HTTP["referer"] !~ "^($|http://www\.example\.org)" {
   url.access-deny = ( ".jpg", ".jpeg", ".png" )
}
```

**Важно:** При совместном использовании директив url.access-deny и server.error-handler-404 при запросе запрещённого контента запросы будут направляться согласно директиве server.error-handler-404 ([Подробнее](http://redmine.lighttpd.net/issues/1727)).Чтобы этого избежать необходимо добавить server.error-handler-404 = "forbidden" внутрь условия, содержащего url.access-deny. Пример: `/etc/lighttpd/lighttpd.conf` 
```
$HTTP["host"] =~ "mysite\.com" {
   server.document-root = "/srv/http/mysite.com"
   server.error-handler-404 = "/index.php"
   $HTTP["url"] == "/cache/" {
      url.access-deny = ( "" )
      server.error-handler-404 = "forbidden"
   }
   $HTTP["url"] =~ "^/wiki/(.*/)?\.ht" {
      url.access-deny = ( "" )
      server.error-handler-404 = "forbidden"
   }
}
```

## Аутентификация

**Важно:** Если mod_fastcgi и mod_auth используются вместе, то mod_auth должен быть загружен **до** mod_fastcgi.

### Методы

lighttpd поддерживает два метода аутентификации:

*   **Basic** метод передаёт имя пользователя и пароль по сети в открытом виде(закодированными в base64), что способствует возникновению проблемы безопастности в случае если соединение между клиентом и сервером не шифруется.
*   **Digest** метод передаёт только хешированную информацию, что значительно повышает конфидециальность аутентификационных данных в незащищённых сетях.

**Важно:** Реализация digest метода в настоящий момент не полностью соответствует стандарту, позволяя осуществить replay attack.

### Backends

В зависимости от метода lighttpd позволяет использовать различные методы хранения данных необходимых для аутентификации. Для basic аутентификации:

*   plain
*   htpasswd (crypt only)
*   htdigest
*   ldap

Для digest аутентификации:

*   plain
*   htdigest

#### plain

Файл содержит строки с именами пользователей и паролями в открытом виде. Имя пользователя и пароль разделяются двоеточием. Например:

```
agent007:secret

```

#### htpasswd

Файл содержит строки с именами пользователей и зашифрованными с помощью crypt() паролями. Имя пользователя и пароль разделяются двоеточием.Например:

```
agent007:XWY5JwrAVBXsQ

```

#### htdigest

Файл содержит строки с именами пользователей, realm'ом и зашифрованными с помощью md5() паролями. Имя пользователя, realm и пароль разделяются двоеточием. Например:

```
agent007:download area:8364d0044ef57b3defcfa141e8f77b65

```

#### ldap

ldap backend обычно выполняет следующие действия для аутентификации пользователя

*   анонимное соединение (при загрузке plugin'а)
*   получение DN для фильтрации = username
*   аутентификация на ldap сервере
*   рассоединение

если четвёртый шаг проходит без ошибок, то пользователь считается авторизированным

**Tip:** Для создания файлов htpasswd и htdigest Вы можете воспользоваться утилитами, идущими в составе пакета [apache](https://www.archlinux.org/packages/?name=apache) или установить [apache-tools](https://aur.archlinux.org/packages/apache-tools/) из [AUR](/index.php/AUR "AUR").

Чтобы сгенерировать файл htpasswd введите команду:

 `$ htpasswd lighttpd.user.htpasswd username` 

Чтобы сгенерировать файл htdigest введите команду:

 `$ htdigest lighttpd.user.htdigest 'download area' username` 

### Пример конфигурации

 `/etc/lighttpd/conf.d/auth.conf` 
```
server.modules += ( "mod_auth" )
## отладка
# 0 для выключения, 1 для 'auth-ok' сообщений, 2 для подробных сообщений
auth.debug                 = 0

## тип backend'а
# plain, htpasswd, ldap или htdigest
auth.backend               = "htpasswd" 

# имя файла в котором хранится информация необходимая для plain аутентификации
auth.backend.plain.userfile = "lighttpd-plain.user" 

## для htpasswd
auth.backend.htpasswd.userfile = "/full/path/to/lighttpd-htpasswd.user" 

## для htdigest
auth.backend.htdigest.userfile = "lighttpd-htdigest.user" 

## ограничения
# установка ограничений:
#
# ( <left-part-of-the-url> =>
#   ( "method" => "digest"/"basic",
#     "realm" => <realm>,
#     "require" => "user=<username>" )
# )
#
# <realm> это значение которое будет показано в диалоговом окне
#     и также будет использоваться для digest-алгоритма и
#     должно совпадать с realm'ом в htdigest файле (если используется)
#

auth.require = ( "/download/" =>
                 (
                 # метод должен быть или basic или digest
                   "method"  => "digest",
                   "realm"   => "download archiv",
                   "require" => "user=agent007|user=agent008" 
                 ),
                 "/server-info" =>
                 (
                 # Ограничение доступа к информации о сервере
                   "method"  => "digest",
                   "realm"   => "download archiv",
                   "require" => "valid-user" 
                 )
                 "/protected-folder/" =>
                 (
                   "method"  => "digest",
                   "realm"   => "download archiv",
                   "require" => "valid-user" 
                 )
               )

# Использование регулярного выражения (как альтернатива):
$HTTP["url"] =~ "/server-info|/protected-folder/" {
  auth.require = ( "" =>
                   (
                     "method"  => "digest",
                     "realm"   => "download archiv",
                     "require" => "valid-user" 
                   )
                 )
}

```

## Кодировка по умолчанию

Чтобы установить кодировку для статических файлов, нужно добавить charset=utf-8 в директиве mimetype.assign. Например:

 `/etc/lighttpd/conf.d/mime.conf` 
```
mimetype.assign             = (
  ".css"          =>      "text/css; charset=utf-8",
  ".html"         =>      "text/html; charset=utf-8",
  ".htm"          =>      "text/html; charset=utf-8",
  ".js"           =>      "text/javascript; charset=utf-8",
  ".log"          =>      "text/plain; charset=utf-8",
  ".conf"         =>      "text/plain; charset=utf-8",
  ".text"         =>      "text/plain; charset=utf-8",
  ".txt"          =>      "text/plain; charset=utf-8",
  ".xml"          =>      "text/xml; charset=utf-8",
  ""              =>      "application/octet-stream",
)
```

**Важно:** Для файлов, указанных в директиве ssi.extension, добавление charset=utf-8 в mimetype.assign не работает. Единственный способ указать кодировку, это добавить в секцию <head> shtml файла строку: `<meta http-equiv="Content-Type" content="text/html; charset=utf-8">` 

Кодировка для листинга каталогов устанавливается директивой:

 `/etc/lighttpd/lighttpd.conf`  `dir-listing.encoding = "utf-8"` 

Кодировка для php файлов устанавливается в файле `/etc/php/php.ini`:

 `/etc/php/php.ini`  `default_charset = "utf-8"` 

## Проксирование

### Lighttpd как reverse proxy для отдачи статики

Пример конфигурации при использовании виртуальных хостов:

 `/etc/lighttpd/lighttpd.conf` 
```
server.modules = (
   ... "mod_proxy", ...
}

$HTTP["host"] =~ "example\.com" {
   setenv.add-request-header ( "Host" => "example.org" ) # добавляем HTTP заголовок
   $HTTP["url"] !~ "\.(js|css|gif|jpg|png|ico|txt|swf|html|htm)$" {
      proxy.server = ( "" => (( "host" => "127.0.0.1", "port" => 8080 )
   ))
   }
}
```

Можно также перенапрвлять только скрипты с определённым расширением:

 `/etc/lighttpd/lighttpd.conf` 
```
server.modules = (
   ... "mod_proxy", ...
}

$HTTP["host"] =~ "example\.com" {
   setenv.add-request-header ( "Host" => "example.org" ) # добавляем HTTP заголовок
   proxy.server = ( ".php" => (( "host" => "127.0.0.1", "port" => 8080 )),
                    ".cgi" => (( "host" => "127.0.0.1", "port" => 8080 )),
                    ".pl" => (( "host" => "127.0.0.1", "port" => 8080 ))
   )
}
```

В качестве альтернативы можно использовать условие $HTTP["url"]:

 `/etc/lighttpd/lighttpd.conf` 
```
server.modules = (
   ... "mod_proxy", ...
}

$HTTP["host"] =~ "example\.com" {
   setenv.add-request-header ( "Host" => "example.org" ) # добавляем HTTP заголовок
   $HTTP['url'] =~ "(.cgi|.pl|.php)$" {
      proxy.server = ( "" => ( host = "127.0.0.1", port = "8080" ))
   }
}
```

### Распределние нагрузки с помощью Lighttpd

Для распределения нагрузки можно использовать следующие настройки:

 `/etc/lighttpd/lighttpd.conf` 
```
server.modules = (
   ... "mod_proxy", ...
}
$SERVER["socket"] == ":80" {
   proxy.balance = "hash" 
   proxy.server  = ( "" => ( ( "host" => "10.0.0.10", "port" => "80" ),
                             ( "host" => "10.0.0.11", "port" => "80" ),
                             ( "host" => "10.0.0.12", "port" => "80" ),
                             ( "host" => "10.0.0.13", "port" => "80" ),
                             ( "host" => "10.0.0.14", "port" => "80" ),
                             ( "host" => "10.0.0.15", "port" => "80" ),
                             ( "host" => "10.0.0.16", "port" => "80" ),
                             ( "host" => "10.0.0.17", "port" => "80" )
   ))
}
```

Доступны следующие типы балансинга:

*   **fair** - запрос обрабатывается менее нагруженным сервером
*   **round-robin** - запросы обрабатывают сервера по очереди
*   **hash** - гарантировано один и тот же uri будет обрабатываться конкретным сервером

## Производительность

### HTTP Keep-Alive

Отключение Keep-Alive может помочь вашему серверу, если вы страдаете от большого количества дескрипторов файлов. Значения по умолчанию:

 `/etc/lighttpd/lighttpd.conf` 
```
server.max-keep-alive-requests = 16
server.max-keep-alive-idle = 5
server.max-read-idle = 60
server.max-write-idle = 360
```

Обработка 16 запросов на одно соединение, ожидание 5 секунд прежде, чем Lighttpd закроет соединение.

Если сервер обрабатывает несколько соединений сразу под высокой нагрузкой (предположим, 500 соединений одновременно в течение 24 часов), вы можете столкнуться с проблемой нехватки дескрипторов файлов

 `/etc/lighttpd/lighttpd.conf` 
```
server.max-keep-alive-requests = 4
server.max-keep-alive-idle = 4
```

Это позволит высвободить соединения ранее, и освободит дескриптор файлов без вредные потери производительности.

Отключение Keep-Alive полностью является крайним случаем, если вы все еще хватает файловых дескрипторов:

 `/etc/lighttpd/lighttpd.conf`  `server.max-keep-alive-requests = 0` 

### Обработчик событий

Для Linux с ядром 2.6 и выше рекомендуется следующее значение:

 `/etc/lighttpd/lighttpd.conf`  `server.event-handler = linux-sysepoll` 

Значение по умолчанию: poll (для Unix систем).

### Обработчик сетевых соединений

Основный интерфейс для всех платформ - это системные вызовы read() и write(). Современные операционные системы имеют свои собственные системные вызовы, помогающие серверам передавать файлы так быстро, как это возможно. Чтобы установить обработчик сетевых сеодиненй используется директива server.network-backend:

 `/etc/lighttpd/lighttpd.conf`  `server.network-backend = linux-sendfile` 

*   linux-sendfile рекомендуется для маленьких файлов.
*   writev рекомендуется для очень больших файлов.

### Максимальное количество соединений

Lighttpd - сервер, работающий в один поток. Его основной ресурс ограничивается количеством дескрипторов файлов, которые устанавливается 1024 по умолчанию в большинстве систем. Дескриптор файла — это просто число, которое представляет открытый файл или сокет. Каждый раз, когда процесс открывает новый файл или сокет, он определяет место для нового дескриптора файла. После закрытия файла или сокета эти дескрипторы используются повторно. Большая часть систем Unix накладывает ограничение на число одновременно открытых дескрипторов файлов. Эти ограничения касаются как одного процесса, так и всей системы.

Узнать ограничение дескрипторов файлов в вашей системе можно с помощью команды:

 `# ulimit -n` 

Если у вас сайт с большим трафиком, вы можете увеличить это ограничение:

 `/etc/lighttpd/lighttpd.conf`  `server.max-fds = 2048` 

## Примеры настроек для различных CMS

### phpMyAdmin

Устанавливаем необходимые пакеты:

 `# pacman -S lighttpd mysql php-cgi php-mcrypt phpmyadmin` 

Настройка поддержки php описана [выше](#PHP).

Раскоментируем следующие директивы в `/etc/php/php.ini`:

 `/etc/php/php.ini` 
```
extension=mcrypt.so
extension=mysql.so
```

Также убедитесь, что директории phpmyadmin указаны в директиве open_basedir в `/etc/php/php.ini`

 `/etc/php/php.ini`  `open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/:/etc/webapps/` 

Затем конфигурируем Lighttpd:

 `/etc/lighttpd/conf.d/phpmyadmin.conf` 
```
# Подкючаем необходимые модули, если этого не было сделано раньше
server.modules += ( "mod_alias", "mod_access", "mod_redirect", "mod_rewrite" )

alias.url = ( "/phpmyadmin" => "/usr/share/webapps/phpMyAdmin/")
url.rewrite = ( "^/phpMyAdmin(/.*)?$" => "/phpmyadmin$1" )
```

Если вы хотите, чтобы phpMyAdmin был доступен только по защищённому протоколу добавьте следюущие настройки:

 `/etc/lighttpd/conf.d/phpmyadmin.conf` 
```
$SERVER["socket"] == ":80" {
   $HTTP["url"] =~ "^/phpmyadmin" {
      url.redirect = ( "^/(.*)" => "https://example.com/$1" )
   }
}
```

Вы также можете ограничить доступ к phpMyAdmin для определённых IP адресов:

 `/etc/lighttpd/conf.d/phpmyadmin.conf` 
```
$HTTP["remoteip"] != "127.0.0.1" {
   $HTTP["url"] =~ "^/phpmyadmin" {
      url.access-deny = ( "" )
   }
}
```

Подключаем `/etc/lighttpd/conf.d/phpmyadmin.conf` к основному файлу настроек:

 `/etc/lighttpd/lighttpd.conf`  `include "conf.d/phpmyadmin.conf"` 

Запускаем сервер:

 `# rc.d start lighttpd` 

Теперь вы можете получить доступ к phpMyAdmin по адресу [http://localhost/phpmyadmin](http://localhost/phpmyadmin) или [http://localhost/phpMyAdmin](http://localhost/phpMyAdmin)

### Mediawiki

Устанавливаем необходимые пакеты:

 `# pacman -S lighttpd mysql php-cgi imagemagick ghostscript mediawiki` 

Настройка поддержки php описана [выше](#PHP). УБедитесь, что необходимые директории перечислены в директиве open_basedir в `/etc/php/php.ini`

 `/etc/php/php.ini`  `open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/:/etc/webapps/:/var/cache/mediawiki:/var/lib/mediawiki/` 

Задаём пароль для учётной записи root MySQL:

 `#mysqladmin -u root password пароль` 

Создаём базу данных для wiki:

 `# mysql -uroot -p${rootpasswd} --execute="create database wiki;"` 

Создаём пользователя для новой базы:

 `# mysql -uroot -p${rootpasswd} --execute="GRANT ALL PRIVILEGES ON wiki.* TO ${wiki_user}@localhost IDENTIFIED by '${userpasswd}'  WITH GRANT OPTION;"` 

*   ${rootpasswd} - пароль root MySQL.
*   ${wiki_user} - имя пользователя базы данных wiki.
*   ${userpasswd} - пароль пользователя базы данныз wiki.

**Tip:** Тоже самое Вы можете проделать через web-интерфейс [phpMyAdmin](#phpMyAdmin).

Настраиваем Lighttpd (согласно нижеприведённые настройки wiki будет доступна по адресу [http://mysite/wiki](http://mysite/wiki)):

 `/etc/lighttpd/conf.d/mediawiki.conf` 
```
# Подкючаем необходимые модули, если этого не было сделано раньше
server.modules += ( "mod_alias", "mod_access", "mod_redirect", "mod_rewrite" )
# Создаём alias
alias.url += ( "/wiki" => "/usr/share/webapps/mediawiki")
# Перенаправляем запросы на несуществующие файлы на index.php
$HTTP["url"] =~ "/wiki" {
   server.error-handler-404 = "/wiki/index.php"
}
# Запрещаем доступ к .htaccess файлам
$HTTP["url"] =~ "/\.ht" {
   url.access-deny = ( "" )
   server.error-handler-404 = "403"
}
# Запрещаем доступ к папкам (согласно расположению .htaccess)
$HTTP["url"] =~ "^/wiki/(cache|includes|maintenance|math|languages|serialized|images/deleted)/" {
   url.access-deny = ( "" )
   server.error-handler-404 = "403"
}
# Запрещаем выполнение html или php кода в каталоге images (http://www.mediawiki.org/wiki/Manual:Security#Upload_security)
$HTTP["url"] =~ "^/wiki/images/" {
   mimetype.assign = (
      ".html" => "text/plain",
      ".htm" => "text/plain",
      ".shtml" => "text/plain",
      ".phtml" => "text/plain",
      ".php5" => "text/plain",
      ".php" => "text/plain",
      "" => ""
   )
}
# Определяем mime-тип для файлов без расширения
$HTTP["url"] =~ "^/wiki/(.*/)?(README|FAQ|COPYING|CREDITS|HYSTORY|INSTALL|OBSOLETE|RELEASE-NOTES(.*)|TODO|UPGRADE)$" {
   mimetype.assign	= ( "" => "text/plain" )
}
# Определяем mime-тип для файлов в каталоге docs
$HTTP["url"] =~ "^/wiki/docs/" {
   mimetype.assign	= ( "" => "text/plain" )
}
```

Подключаем `/etc/lighttpd/conf.d/mediawiki.conf` к основному файлу настроек:

 `/etc/lighttpd/lighttpd.conf`  `include "conf.d/mediawiki.conf"` 

Запускаем сервер:

 `# rc.d start lighttpd` 

Теперь вы можете перейти по адресу [http://localhost/wiki](http://localhost/wiki) для утсановки.

**Tip:** Для получения коротких URL в `/usr/share/webapps/mediawiki/LocalSettings.php` нужно добавить: `/usr/share/webapps/mediawiki/LocalSettings.php` 
```
$wgArticlePath = "/wiki/$1";
$wgUsePathInfo = true;
```

**Tip:** Вместо директивы server.error-handler-404 = /wiki/index.php можно использовать следующие правила перезаписи: `/etc/lighttpd/conf.d/mediawiki.conf` 
```
url.rewrite-if-not-file = (
   "^/wiki/(mw-)?config(/.*)?$" => "$0",
   "^/wiki/([^?]*)(?:\?(.*))?" => "/wiki/index.php?title=$1&$2",
   "^/wiki/([^?]*)" => "/wiki/index.php?title=$1"
)

```

Если хотите использовать поддомен для wiki или Mediawiki будет единствуенной CMS на вашем сайте, то настройки Lighttpd будут выглядеть следующим образом:

 `/etc/lighttpd/conf.d/mediawiki.conf` 
```
# Подкючаем необходимые модули, если этого не было сделано раньше
server.modules += ( "mod_alias", "mod_access", "mod_redirect", "mod_rewrite" )

# Перенаправляем запросы на несуществующие файлы на index.php
$HTTP["host"] =~ "mysite\.com" { # для поддомена "wiki\.mysite\.com"
   server.document-root = "/usr/share/webapps/mediawiki"
   server.error-handler-404 = "/index.php")
# Запрещаем доступ к .htaccess файлам
   $HTTP["url"] =~ "/\.ht" {
# Предотвращаем перенапрвление запросов на запрещённый контент на /index.php (баг Lighttpd)
      url.access-deny = ( "" )
      server.error-handler-404 = "403"
   }
# Запрещаем доступ к папкам (согласно расположению .htaccess)
   $HTTP["url"] =~ "^/(cache|includes|maintenance|math|languages|serialized|images/deleted)/" {
# Предотвращаем перенапрвление запросов на запрещённый контент на /index.php (баг Lighttpd)
      url.access-deny = ( "" )
      server.error-handler-404 = "403"
   }
# Запрещаем выполнение html или php кода в каталоге images (http://www.mediawiki.org/wiki/Manual:Security#Upload_security)
   $HTTP["url"] =~ "^/images/" {
      mimetype.assign = (
         ".html" => "text/plain",
         ".htm" => "text/plain",
         ".shtml" => "text/plain",
         ".phtml" => "text/plain",
         ".php5" => "text/plain",
         ".php" => "text/plain",
         "" => ""
      )
   }
# Определяем mime-тип для файлов без расширения
   $HTTP["url"] =~ "^/(.*/)?(README|FAQ|COPYING|CREDITS|HYSTORY|INSTALL|OBSOLETE|RELEASE-NOTES(.*)|TODO|UPGRADE)$" {
      mimetype.assign	= ( "" => "text/plain" )
   }
# Определяем mime-тип для файлов в каталоге docs
   $HTTP["url"] =~ "^/docs/" {
      mimetype.assign	= ( "" => "text/plain" )
   }
}
```

**Tip:** Для получения коротких URL в `/usr/share/webapps/mediawiki/LocalSettings.php` нужно добавить: `/usr/share/webapps/mediawiki/LocalSettings.php` 
```
$wgArticlePath = "/$1";
$wgUsePathInfo = true;
```

**Tip:** Вместо директивы server.error-handler-404 = /index.php можно использовать следующие правила перезаписи: `/etc/lighttpd/conf.d/mediawiki.conf` 
```
url.rewrite-if-not-file = (
   "^/(mw-)?config(/.*)?$" => "$0",
   "^/([^?]*)(?:\?(.*))?" => "/index.php?title=$1&$2",
   "^/([^?]*)" => "/index.php?title=$1"
)

```

#### texvc

Устанавлиаем необходимые пакеты:

 `# pacman -S texvc` 

Затем в файле `/usr/share/webapps/mediawiki/LocalSettings.php` добавляем:

 `/usr/share/webapps/mediawiki/LocalSettings.php` 
```
$wgUseTeX           = true;
$wgMaxShellMemory = 8000000;
$wgMaxShellFileSize = 1000000;
$wgMaxShellTime = 300;
```

#### HTTPS login

Если MediaWiki Установлена в папку wiki, то конфиг будет выглядеть следующим образом:

 `/etc/lighttpd/conf.d/mediawiki.conf` 
```
$HTTP["scheme"] == "http" {
   $HTTP["url"] =~ "^/wiki/(.*)UserLogin" {
      url.redirect = ( "^/(.*)" => "https://unikum.dyndns.org/$1" )
   }
   $HTTP["url"] =~ "^/wiki/" {
      $HTTP["querystring"] =~ "UserLogin" {
         url.redirect = ( "^/(.*)" => "https://unikum.dyndns.org/$1" )
      }
   }
}
```

### Drupal

Устанавливаем Drupal:

 `# pacman -S drupal` 

УБедитесь, что необходимые директории перечислены в директиве open_basedir в `/etc/php/php.ini`

 `/etc/php/php.ini`  `open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/:/var/lib/drupal/` 

Настраиваем Lighttpd:

#### Вариант 1: server.error-handler-404

 `/etc/lighttpd/lighttpd.conf` 
```
$HTTP["host"] =~ "mysite\.com$" { # "drupal\.mysite\.com" для поддомена
   server.document-root = "/usr/share/webapps/drupal"
   server.error-handler-404 = "/index.php"
# Запрет доступа (согласно .htaccess)
   url.access-deny = ( ".engine", ".inc", "info", ".install", ".make", ".module", ".profile", ".test", ".po", ".sh", "sql", ".theme", ".tpl.php", ".xtmpl", "Entries", "Repository", "Root", "Tag", "Template" )
}
```

**Tip:** При возникновении проблем с доступом при изменении настроек попробуйте отключить "Чистые ссылки" (Главная » Администрирование » Конфигурация » Адреса и поиск).

#### Вариант 2: mod_rewrite

 `/etc/lighttpd/lighttpd.conf` 
```
$HTTP["host"] =~ "mysite\.com$" { # "drupal\.mysite\.com" для поддомена
   server.document-root = "/usr/share/webapps/drupal"
   url.rewrite-if-not-file += (
      "^/rss.xml" => "/index.php?q=rss.xml",
      "^/system/test/(.*)$" => "/index.php?q=system/test/$1",
      "^/([^.?]*)\?(.*)$" => "/index.php?q=$1&$2",
      "^/search/(.*)$" => "/index.php?q=search/$1",
      "^/([^.?]*)$" => "/index.php?q=$1",
      "^/([^.?]*\.html)$" => "/index.php?q=$1",
      "^/([^.?]*\.htm)$" => "/index.php?q=$1",
   )

   url.access-deny = ( ".engine", ".inc", "info", ".install", ".make", ".module", ".profile", ".test", ".po", ".sh", "sql", ".theme", ".tpl.php", ".xtmpl", "Entries", "Repository", "Root", "Tag", "Template" )
}

```

### MODX

Для того, чтобы в MODX заработали "Дружественные URL" в конфиг Lighttpd внесите следующие строки:

 `/etc/lighttpd/lighttpd.conf` 
```
url.rewrite-if-not-file += (
   "^/$" => "index.php",
   "^/(assets|manager|core|connectors)" => "$0",
   "^/(?!index(?:-ajax)?\.php)(.*)\?(.*)$" => "/index.php?q=$1&$2",
   "^/(?!index(?:-ajax)?\.php)(.*)$" => "/index.php?q=$1"
)

$HTTP["url"] =~ "^/core/" {
   url.access-deny = ( "" )
}

```

Также стоит запреттить доступ для всех в папку core.

## См. также

*   [Lighttpd wiki](http://redmine.lighttpd.net/projects/lighttpd/wiki) (англ.)
*   [Документация по web-серверу Lighttpd (version 1.3.16)](http://silinio.webhost.ru/lighttpd/index.html) (рус.)
*   [Перевод статьи «The lighttpd Web Server»](http://netsago.org/ru/docs/2/6/) (рус.)