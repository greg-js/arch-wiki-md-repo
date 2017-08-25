[Let’s Encrypt](https://letsencrypt.org/) бесплатный, автоматизированный, открытый центр сертификации использующий [ACME](https://en.wikipedia.org/wiki/Automated_Certificate_Management_Environment "wikipedia:Automated Certificate Management Environment") протокол.

Официальный клиент называется 'Certbot', который позволяет запрашивать действительные сертификаты X.509 прямо из командной строки. Минимальный клиент с ручным созданием CSR доступен в [acme-tiny](https://aur.archlinux.org/packages/acme-tiny/), клиенты, подходящие для скриптов, - это [simp_le-git](https://aur.archlinux.org/packages/simp_le-git/) и [letsencrypt-cli](https://aur.archlinux.org/packages/letsencrypt-cli/).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
    *   [2.1 Webroot](#Webroot)
        *   [2.1.1 Получить сертификат(ы)](#.D0.9F.D0.BE.D0.BB.D1.83.D1.87.D0.B8.D1.82.D1.8C_.D1.81.D0.B5.D1.80.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.28.D1.8B.29)
    *   [2.2 Вручную](#.D0.92.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
*   [3 Расширенная настройка](#.D0.A0.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.BD.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 Конфигурация веб-сервера](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D0.B2.D0.B5.D0.B1-.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0)
        *   [3.1.1 nginx](#nginx)
    *   [3.2 Несколько доменов](#.D0.9D.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.B4.D0.BE.D0.BC.D0.B5.D0.BD.D0.BE.D0.B2)
        *   [3.2.1 nginx](#nginx_2)
        *   [3.2.2 Apache](#Apache)
    *   [3.3 Автоматическое обновление](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5)
        *   [3.3.1 systemd](#systemd)
            *   [3.3.1.1 Альтернативные услуги](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D1.8B.D0.B5_.D1.83.D1.81.D0.BB.D1.83.D0.B3.D0.B8)
                *   [3.3.1.1.1 nginx](#nginx_3)
                *   [3.3.1.1.2 Apache](#Apache_2)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установить](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C "Установить") пакет [certbot](https://www.archlinux.org/packages/?name=certbot).

Плагины доступны для автоматической настройки и установки выданных сертификатов на веб-серверах:

*   Экспериментальный плагин для [Nginx](/index.php/Nginx "Nginx") предоставляется пакетом [certbot-nginx](https://www.archlinux.org/packages/?name=certbot-nginx).
*   Автоматическая установка с использованием [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") включена через пакет [certbot-apache](https://www.archlinux.org/packages/?name=certbot-apache).

## Конфигурация

Для получения дополнительной информации об создании и использовании сертификатов обращайтесь в документацию [Certbot documentation](https://certbot.eff.org/docs/)

### Webroot

**Примечание:**

*   Метод Webroot требует HTTP на порт 80 для проверки Certbot.
    *   Чтобы Certbot проверял использование HTTPS на порту 443, вместо Webroot следует использовать плагин Nginx (--nginx) или Apache ( --apache) (--webroot).
*   Имя сервера должно соответствовать имени соответствующего DNS.
*   На хосте могут потребоваться разрешения, чтобы разрешить доступ для чтения к `[http://domain.tld/.well-known](http://domain.tld/.well-known)`.

При использовании метода webroot клиент Certbot отправляет запрос вызова внутри `/path/to/domain.tld/html/.well-known/acme-challenge/` который используется для проверки.

Использование этого метода рекомендуется для ручной установки; Он предлагает автоматическое обновление и упрощение управления сертификатами.

**Совет:** Следующая первоначальная конфигурация сервера [nginx server](/index.php/Nginx#Server_blocks "Nginx") может оказаться полезной для получения первого сертификата: `/etc/nginx/servers-available/domain.tld` 
```

server {
  listen 80;
  listen [::]:80;
  server_name domain.tld;
  root /usr/share/nginx/html;
  location / {
    index index.htm index.html;
  }
}

# ACME challenge
location ^~ /.well-known {
  allow all;
  auth_basic off;
  alias /var/lib/letsencrypt/.well-known/;
  default_type "text/plain";
  try_files $uri =404;
}

```

#### Получить сертификат(ы)

Запросить сертификат для `domain.tld` для `/var/lib/letsencrypt/` как общедоступный путь:

```
# certbot certonly --email **email@example.com** --webroot -w **/var/lib/letsencrypt/** -d **domain.tld**

```

Чтобы добавить (дополнительный) домен(ы), включите все зарегистрированные домены, используемые в текущей настройке:

```
# certbot certonly --email **email@example.com** --webroot -w **/var/lib/letsencrypt/** -d **domain.tld,sub.domain.tld**

```

Чтобы обновить (все) текущий сертификат (ы):

```
# certbot renew

```

Смотрите [#Автоматическое обновление](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5) как альтернативный вариант

### Вручную

**Note:**

*   Запускаемый веб-сервер должен быть временно остановлен.
*   Автоматическое обновление недоступно при выполнении ручной установки, см. [#Webroot](#Webroot).

Если для вашего веб-сервера нет плагина, используйте следующую команду:

```
# certbot certonly --manual

```

Если вы предпочитаете использовать DNS-запрос (запись TXT), используйте:

```
# certbot certonly --manual --preferred-challenges dns

```

Это автоматически проверяет ваш домен и создает закрытый ключ и пару сертификатов. Они будут размещены в `/etc/letsencrypt/live/*your.domain*/`.

Затем вы можете вручную настроить веб-сервер для использования ключа и сертификата в этом каталоге.

**Note:** Запуск этой команды несколько раз приведет к созданию нескольких наборов файлов в в `/etc/letsencrypt/live/*your.domain*/` с произвольным числом в конце, поэтому позаботьтесь о том, чтобы переименовать их в этом каталоге или в файле конфигурации веб-сервера.

## Расширенная настройка

### Конфигурация веб-сервера

Вместо использования плагинов для автоматической настройки может быть предпочтительнее включить SSL для сервера вручную.

**Tip:**

*   Mozilla имеет полезную статью [SSL/TLS article](https://wiki.mozilla.org/Security/Server_Side_TLS), которая включает в себя [automated tool](https://mozilla.github.io/server-side-tls/ssl-config-generator/) чтобы создать более безопасную конфигурацию.
*   [Cipherli.st](https://cipherli.st) обеспечивает надежные примеры внедрения SSL и руководство для большинства современных веб-серверов.

#### nginx

Пример сервера `domain.tld` с использованием подписанного SSL-сертификата Let's Encrypt:

 `/etc/nginx/servers-available/domain.tld` 
```

# redirect to https
server {
  listen 80;
  listen [::]:80;
  server_name domain.tld;
  return 301 https://$host$request_uri;
}

server {
  listen 443 ssl http2;
  listen [::]:443 ssl http2;
  ssl_certificate /etc/letsencrypt/live/domain.tld/fullchain.pem;
  ssl_certificate_key /etc/letsencrypt/live/domain.tld/privkey.pem;
  ssl_trusted_certificate /etc/letsencrypt/live/domain.tld/chain.pem;
  ssl_session_timeout 1d;
  ssl_session_cache shared:SSL:50m;
  ssl_session_tickets off;
  ssl_prefer_server_ciphers on;
  add_header Strict-Transport-Security max-age=15768000;
  ssl_stapling on;
  ssl_stapling_verify on;
  server_name domain.tld;
  ..
}

# A subdomain uses the same SSL-certifcate:
server {
  listen 443 ssl http2;
  listen [::]:443 ssl http2;
  ssl_certificate /etc/letsencrypt/live/domain.tld/fullchain.pem;
  ssl_certificate_key /etc/letsencrypt/live/domain.tld/privkey.pem;
  ssl_trusted_certificate /etc/letsencrypt/live/domain.tld/chain.pem;
  ..
  server_name sub.domain.tld;
  ..
}

# ACME challenge
location ^~ /.well-known {
  allow all;
  alias /var/lib/letsencrypt/.well-known/;
  default_type "text/plain";
  try_files $uri =404;
}

```

### Несколько доменов

Управление может быть упрощено путем сопоставления всех HTTP-запросов для `/.well-known/acme-challenge/` в одну папку, например. `/var/lib/letsencrypt`.

Затем путь должен быть доступен для записи клиенту Let's Encrypt и веб-серверу (например, [nginx](/index.php/Nginx "Nginx") или [Apache](/index.php/Apache "Apache"), запущенному под пользователем *http*):

```
# mkdir -p /var/lib/letsencrypt/.well-known
# chgrp http /var/lib/letsencrypt
# chmod g+s /var/lib/letsencrypt

```

#### nginx

Создайте файл, содержащий блок местоположения, и включите его внутри блока сервера:

 `/etc/nginx/conf.d/letsencrypt.conf` 
```

location ^~ /.well-known {
  allow all;
  alias /var/lib/letsencrypt/.well-known/;
  default_type "text/plain";
  try_files $uri =404;
}

```

Пример конфигурации сервера:

 `/etc/nginx/servers-available/domain.conf` 
```
server {
  server_name domain.tld
   ..
  include conf.d/letsencrypt.conf;
}

```

#### Apache

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

Вероятно, вы захотите, чтобы ваш веб-сервер перезагружал сертификаты после каждого обновления. Добавте одну из этих строк в файл `certbot.service`:

*   Apache: `ExecStartPost=/bin/systemctl reload httpd.service`
*   nginx: `ExecStartPost=/bin/systemctl reload nginx.service`

**Примечание:** Перед добавлением [timer](/index.php/Systemd/Timers "Systemd/Timers") убедитесь, что служба работает правильно и ничего не пытается запросить.

Добавьте таймер для проверки продления сертификата дважды в день и включите рандомизированную задержку, чтобы все запросы на продление были равномерно распределены в течение дня, чтобы облегчить загрузку сервера Let's Encrypt [[1]](https://certbot.eff.org/#arch-nginx):

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

[enable](/index.php/Enable "Enable") и [start](/index.php/Start "Start") `certbot.timer`.

##### Альтернативные услуги

При использовании автономного метода, перед выполнением запроса на обновление, вы должны остановить свой веб-сервер и запустить веб-сервер, когда работа Certbot будет завершена. Certbot предоставляет hooks для автоматического остановки и перезапуска веб-сервера.

###### nginx

 `/etc/systemd/system/certbot.service` 
```
[Unit]
Description=Let's Encrypt renewal

[Service]
Type=oneshot
ExecStart=/usr/bin/certbot renew --post-hook "/usr/bin/systemctl restart nginx.service" --agree-tos
```

###### Apache

 `/etc/systemd/system/certbot.service` 
```
[Unit]
Description=Let's Encrypt renewal

[Service]
Type=oneshot
ExecStart=/usr/bin/certbot renew --pre-hook "/usr/bin/systemctl stop httpd.service" --post-hook "/usr/bin/systemctl start httpd.service" --quiet --agree-tos
```

## Смотрите также

*   [EFF's Certbot documentation](https://certbot.eff.org/)
*   [List of ACME clients](https://letsencrypt.org/docs/client-options/)