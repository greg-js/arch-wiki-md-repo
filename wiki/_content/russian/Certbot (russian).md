**Состояние перевода:** На этой странице представлен перевод статьи [Certbot](/index.php/Certbot "Certbot"). Дата последней синхронизации: 3 июня 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Certbot&diff=0&oldid=573839).

[Certbot](https://github.com/certbot/certbot) — [ACME](/index.php/ACME "ACME")-клиент от [Фонда Электронных Рубежей](https://www.eff.org/), написанный на Python и обеспечивающий такие удобства, как автоматическая настройка веб-сервера и встроенный веб-сервер для вызова HTTP. Certbot рекомендован [Let's Encrypt](https://letsencrypt.org/).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 Плагины](#Плагины)
        *   [2.1.1 Nginx](#Nginx)
            *   [2.1.1.1 Управление блоками server в Nginx](#Управление_блоками_server_в_Nginx)
        *   [2.1.2 Apache](#Apache)
            *   [2.1.2.1 Управление виртуальными хостами Apache](#Управление_виртуальными_хостами_Apache)
    *   [2.2 Webroot](#Webroot)
        *   [2.2.1 Mapping ACME-challenge requests](#Mapping_ACME-challenge_requests)
            *   [2.2.1.1 nginx](#nginx_2)
            *   [2.2.1.2 Apache](#Apache_2)
        *   [2.2.2 Получить сертификат(ы)](#Получить_сертификат(ы))
    *   [2.3 Вручную](#Вручную)
*   [3 Расширенная настройка](#Расширенная_настройка)
    *   [3.1 Автоматическое обновление](#Автоматическое_обновление)
        *   [3.1.1 systemd](#systemd)
    *   [3.2 Автоматическое обновление wildcard-сертификатов](#Автоматическое_обновление_wildcard-сертификатов)
        *   [3.2.1 Настройка BIND для rfc2136](#Настройка_BIND_для_rfc2136)
        *   [3.2.2 Настройка certbot для rfc2136](#Настройка_certbot_для_rfc2136)
*   [4 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [certbot](https://www.archlinux.org/packages/?name=certbot).

Также доступны плагины для автоматической настройки и установки выданных сертификатов на веб-серверах:

*   Плагин для [nginx](/index.php/Nginx_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nginx (Русский)") предоставляется пакетом [certbot-nginx](https://www.archlinux.org/packages/?name=certbot-nginx).
*   Плагин для [Apache HTTP Server](/index.php/Apache_HTTP_Server_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Apache HTTP Server (Русский)") предоставляется пакетом [certbot-apache](https://www.archlinux.org/packages/?name=certbot-apache).

## Настройка

Обратитесь к [документации Certbot](https://certbot.eff.org/docs/) для получения дополнительной информации о создании и использовании сертификатов.

### Плагины

**Важно:** Файлы конфигурации могут быть переписаны для добавления настроек и путей сертификатов Certbot при использовании плагина. Рекомендуется заблаговременно сделать **резервную копию**.

#### Nginx

Плагин [certbot-nginx](https://www.archlinux.org/packages/?name=certbot-nginx) предоставляет автоматическую настройку [Nginx (Русский)](/index.php/Nginx_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nginx (Русский)"). Он пытается найти конфигурацию каждого домена, а также добавляет рекомендованные для безопасности параметры, настройки использования сертификатов и пути к сертификатам Certbot. См. примеры в разделе [#Управление блоками server в Nginx](#Управление_блоками_server_в_Nginx).

Первоначальная настройка [блоков server](/index.php/Nginx_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Блоки_server "Nginx (Русский)"):

```
# certbot --nginx

```

Обновить сертификаты:

```
# certbot renew

```

Изменить сертификаты без изменения файлов конфигурации nginx:

```
# certbot --nginx certonly

```

См. статью [Certbot-Nginx on Arch Linux](https://certbot.eff.org/#arch-nginx) для получения дополнительной информации и раздел [#Автоматическое обновление](#Автоматическое_обновление).

##### Управление блоками server в Nginx

Следующий пример можно использовать в каждом [блоке server](/index.php/Nginx_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Блоки_server "Nginx (Русский)") при управлении этими файлами вручную:

 `/etc/nginx/sites-available/example` 
```
server {
  listen 443 ssl http2;
  listen [::]:443 ssl http2; # Cлушать IPv6
  ssl_certificate /etc/letsencrypt/live/*домен*/fullchain.pem; # Управляется Certbot'ом
  ssl_certificate_key /etc/letsencrypt/live/*домен*/privkey.pem; # Управляется Certbot'ом
  include /etc/letsencrypt/options-ssl-nginx.conf;
  ..
}
```

См. раздел [Nginx (Русский)#TLS/SSL](/index.php/Nginx_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#TLS/SSL "Nginx (Русский)") для получения более подробной информации.

Также можно создать отдельный конфигурационный файл и включать его в каждый блок server:

 `/etc/nginx/conf/001-certbot.conf` 
```
ssl_certificate /etc/letsencrypt/live/*домен*/fullchain.pem; # Управляется Certbot'ом
ssl_certificate_key /etc/letsencrypt/live/*домен*/privkey.pem; # Управляется Certbot'ом
include /etc/letsencrypt/options-ssl-nginx.conf;
```
 `/etc/nginx/sites-available/example` 
```
server {
  listen 443 ssl http2;
  listen [::]:443 ssl http2; # Слушать IPv6
  include conf/001-certbot.conf;
  ..
}

```

#### Apache

Плагин [certbot-apache](https://www.archlinux.org/packages/?name=certbot-apache) предоставляет автоматическую настройку [Apache HTTP Server (Русский)](/index.php/Apache_HTTP_Server_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Apache HTTP Server (Русский)"). Он пытается найти конфигурацию каждого домена, а также добавляет рекомендованные для безопасности параметры, настройки использования сертификатов и пути к сертификатам Certbot. См. примеры в разделе [#Управление виртуальными хостами Apache](#Управление_виртуальными_хостами_Apache).

Первоначальная настройка [виртуальных хостов](/index.php/Apache_HTTP_Server_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Виртуальные_хосты "Apache HTTP Server (Русский)"):

```
# certbot --apache

```

Обновить сертификаты:

```
# certbot renew

```

Изменить сертификаты без изменения файлов конфигурации apache:

```
# certbot --apache certonly

```

См. статью [Certbot-Apache on Arch Linux](https://certbot.eff.org/#arch-apache) для получения дополнительной информации и раздел [#Автоматическое обновление](#Автоматическое_обновление).

##### Управление виртуальными хостами Apache

Следующий пример можно использовать в каждом [виртуальном хосте](/index.php/Apache_HTTP_Server_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Виртуальные_хосты "Apache HTTP Server (Русский)") при управлении этими файлами вручную:

 `/etc/httpd/conf/extra/001-certbot.conf` 
```
<IfModule mod_ssl.c>
<VirtualHost *:443>

Include /etc/letsencrypt/options-ssl-apache.conf
SSLCertificateFile /etc/letsencrypt/live/*домен*/fullchain.pem
SSLCertificateKeyFile /etc/letsencrypt/live/*домен*/privkey.pem

</VirtualHost>
</IfModule>
```
 `/etc/httpd/conf/httpd.conf` 
```
  <IfModule mod_ssl.c>
  Listen 443
  </IfModule>

  Include conf/extra/001-certbot.conf
  ..

```

См. раздел [Apache HTTP Server (Русский)#TLS/SSL](/index.php/Apache_HTTP_Server_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#TLS/SSL "Apache HTTP Server (Русский)") для получения более подробной информации.

### Webroot

**Примечание:**

*   Метод Webroot требует HTTP на порт 80 для проверки Certbot.
*   Имя сервера должно соответствовать имени соответствующего DNS.
*   На хосте могут потребоваться разрешения, чтобы разрешить доступ для чтения к `[http://domain.tld/.well-known](http://domain.tld/.well-known)`.

При использовании метода webroot клиент Certbot размещает ответ на вызов (challenge response) по адресу `/путь/к/domain.tld/html/.well-known/acme-challenge/` который используется для проверки.

Использование этого метода более рекомендовано, чем полностью ручная установка (метод manual), так как он допускает автоматическое обновление сертификатов и упрощает управление ими. Однако использование [плагинов](#Плагины) может быть более предпочтительным, так как они обеспечивают полностью автоматическую настройку и установку.

#### Mapping ACME-challenge requests

Управление может быть упрощено путем сопоставления всех HTTP-запросов для `/.well-known/acme-challenge/` в одну папку, например. `/var/lib/letsencrypt`.

Этот каталог должен быть доступен для записи клиенту Certbot и веб-серверу ([nginx](/index.php/Nginx_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nginx (Русский)") или [apache](/index.php/Apache_HTTP_Server_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Apache HTTP Server (Русский)"), запущенными под пользователем *http*):

```
# mkdir -p /var/lib/letsencrypt/.well-known
# chgrp http /var/lib/letsencrypt
# chmod g+s /var/lib/letsencrypt

```

##### nginx

Создайте файл с блоком `location` и включите (include) его в блок `server`:

 `/etc/nginx/conf.d/letsencrypt.conf` 
```

location ^~ /.well-known/acme-challenge/ {
  allow all;
  root /var/lib/letsencrypt/;
  default_type "text/plain";
  try_files $uri =404;
}

```

Пример настройки блока `server`:

 `/etc/nginx/servers-available/domain.conf` 
```
server {
  server_name domain.tld
   ..
  include conf.d/letsencrypt.conf;
}

```

##### Apache

Создайте файл `/etc/httpd/conf/extra/httpd-acme.conf`:

 `/etc/httpd/conf/extra/httpd-acme.conf` 
```
Alias /.well-known/acme-challenge/ "/var/lib/letsencrypt/.well-known/acme-challenge/"
<Directory "/var/lib/letsencrypt/">
    AllowOverride None
    Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec
    Require method GET POST OPTIONS
</Directory>

```

Включив в `/etc/httpd/conf/httpd.conf`:

 `/etc/httpd/conf/httpd.conf` 
```
Include conf/extra/httpd-acme.conf

```

#### Получить сертификат(ы)

Запросить сертификат для `domain.tld` для `/var/lib/letsencrypt/` как общедоступный путь:

```
# certbot certonly --email **email@example.com** --webroot -w **/var/lib/letsencrypt/** -d **domain.tld**

```

Чтобы добавить (под)домен(ы), включите все зарегистрированные домены, используемые в текущей настройке:

```
# certbot certonly --email **email@example.com** --webroot -w **/var/lib/letsencrypt/** -d **domain.tld,sub.domain.tld**

```

Чтобы обновить (все) текущий сертификат (ы):

```
# certbot renew

```

Смотрите [#Автоматическое обновление](#Автоматическое_обновление) как альтернативный вариант

### Вручную

**Примечание:** Автоматическое обновление недоступно при выполнении ручной установки, см. [#Webroot](#Webroot).

Если для вашего веб-сервера нет плагина, используйте следующую команду:

```
# certbot certonly --manual

```

Если вы предпочитаете использовать DNS-запрос (запись TXT), используйте:

```
# certbot certonly --manual --preferred-challenges dns

```

Это автоматически проверяет ваш домен и создает закрытый ключ и пару сертификатов. Они будут размещены в `/etc/letsencrypt/archive/*ваш.домен*/`, а в каталоге `/etc/letsencrypt/live/*ваш.домен*/` будут созданы символические ссылки на них.

Затем вы можете вручную настроить веб-сервер для использования ключа и сертификата из каталога с символическими ссылками.

**Примечание:** Запуск этой команды несколько раз приведет к созданию нескольких наборов файлов в `/etc/letsencrypt/live/*your.domain*/` с произвольным числом в конце. При этом Certbot автоматически обновляет символические ссылки в каталоге `/etc/letsencrypt/live/*your.domain*/`, чтобы они ссылались на самые свежие сертификаты, так что при использовании этих символических ссылок вам не нужно менять конфигурацию веб-сервера, чтобы использовать обновлённые сертификаты.

## Расширенная настройка

### Автоматическое обновление

#### systemd

Создайте [systemd](/index.php/Systemd "Systemd") `certbot.service`:

 `/etc/systemd/system/certbot.service` 
```
[Unit]
Description=Let's Encrypt renewal

[Service]
Type=oneshot
ExecStart=/usr/bin/certbot renew --quiet --agree-tos
```

Если вы не используете плагин для управления веб-сервером, то его нужно будет перезагрузить вручную, чтобы применить обновлённые сертификаты. Это можно сделать добавлением `--deploy-hook "systemctl reload nginx.service"` к команде `ExecStart` [[1]](https://certbot.eff.org/docs/using.html#renewing-certificates). (Разумеется, используйте `httpd.service` вместо `nginx.service` если нужно.)

**Примечание:** Перед добавлением [timer](/index.php/Systemd/Timers_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd/Timers (Русский)"), убедитесь, что служба работает правильно и ничего не пытается запрашивать у пользователя. Имейте в виду, что для завершения работы службы может потребоваться до 480 секунд из-за задержки, добавленной в [v0.29.0](https://github.com/certbot/certbot/blob/master/CHANGELOG.md#0290---2018-12-05).

Добавьте таймер для проверки продления сертификата дважды в день и включите рандомизированную задержку, чтобы все запросы на продление были равномерно распределены в течение дня, чтобы облегчить загрузку сервера Let's Encrypt [[2]](https://certbot.eff.org/#arch-nginx):

 `/etc/systemd/system/certbot.timer` 
```
[Unit]
Description=Twice daily renewal of Let's Encrypt's certificates

[Timer]
OnCalendar=0/12:00:00
RandomizedDelaySec=1h
Persistent=true

[Install]
WantedBy=timers.target
```

[Включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") `certbot.timer`.

### Автоматическое обновление wildcard-сертификатов

Процесс довольно прост. Для выпуска wildcard-сертификата нужно выполнить DNS challenge request, [using the ACMEv2 protocol](https://community.letsencrypt.org/t/acme-v2-and-wildcard-certificate-support-is-live/55579).

В то время как выпуск wildcard-сертификата вручную прост, его не так просто автоматизировать. DNS challenge представляет собой запись TXT, предоставленную клиентом certbot, которую необходимо установить вручную в DNS.

Вам нужно будет обновлять DNS при каждом обновлении сертификатов. Чтобы не делать это вручную, вы можете использовать [rfc2136](https://tools.ietf.org/html/rfc2136), для которого в certbot есть плагин, упакованный в [certbot-dns-rfc2136](https://www.archlinux.org/packages/?name=certbot-dns-rfc2136). Вам также необходимо настроить DNS-сервер, чтобы разрешить динамическое обновление записей TXT.

#### Настройка BIND для rfc2136

Generate a TSIG secret key:

```
$ tsig-keygen -a HMAC-SHA512 **example-key**

```

and add it in the configuration file:

 `/etc/named.conf` 
```
...
zone "**domain.ltd**" IN {
        ...
        // this is for certbot
        update-policy {
                grant **example-key** name _acme-challenge.**domain.ltd**. txt;
        };
        ...
};

key "**example-key**" {
        algorithm hmac-sha512;
        secret "**a_secret_key**";
};
...
```

[Restart](/index.php/Restart "Restart") `named.service`.

#### Настройка certbot для rfc2136

Create a configuration file for the rfc2136 plugin.

 `/etc/letsencrypt/rfc2136.ini` 
```
dns_rfc2136_server = **IP.ADD.RE.SS**
dns_rfc2136_name = **example-key**
dns_rfc2136_secret = **INSERT_KEY_WITHOUT_QUOTES**
dns_rfc2136_algorithm = HMAC-SHA512
```

Since the file contains a copy of the secret key, secure it with [chmod](/index.php/Chmod "Chmod") by removing the group and others permissions.

Test what we did:

```
# certbot certonly --dns-rfc2136 --force-renewal --dns-rfc2136-credentials /etc/letsencrypt/rfc2136.ini --server [https://acme-v02.api.letsencrypt.org/directory](https://acme-v02.api.letsencrypt.org/directory) --email **example@domain.ltd** --agree-tos --no-eff-email -d '**domain.ltd'** -d '***.domain.ltd'**

```

If you pass the validation successfully and receive certificates, then you are good to go with automating certbot. Otherwise, something went wrong and you need to debug your setup. It basically boils down to running `certbot renew` from now on, see [#Автоматическое обновление](#Автоматическое_обновление).

## Смотрите также

*   [Transport Layer Security#ACME clients](/index.php/Transport_Layer_Security#ACME_clients "Transport Layer Security")
*   [Статья на Википедии](https://en.wikipedia.org/wiki/ru:Let%E2%80%99s_Encrypt "wikipedia:ru:Let’s Encrypt")
*   [Документация Certbot от EFF](https://certbot.eff.org/)
*   [Список ACME-клиентов](https://letsencrypt.org/docs/client-options/)