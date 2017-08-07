[Let’s Encrypt](https://letsencrypt.org/) бесплатный, автоматизированный, и открытый центр сертификации использующий [ACME](https://en.wikipedia.org/wiki/Automated_Certificate_Management_Environment "wikipedia:Automated Certificate Management Environment") протокол.

Официальный клиент называется 'Certbot', который позволяет запрашивать действительные сертификаты X.509 прямо из командной строки. Минимальный клиент с ручным созданием CSR доступен в [acme-tiny](https://aur.archlinux.org/packages/acme-tiny/), клиенты, подходящие для скриптов, - это [simp_le-git](https://aur.archlinux.org/packages/simp_le-git/) и [letsencrypt-cli](https://aur.archlinux.org/packages/letsencrypt-cli/).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
    *   [2.1 Webroot](#Webroot)
        *   [2.1.1 Получить сертификат](#.D0.9F.D0.BE.D0.BB.D1.83.D1.87.D0.B8.D1.82.D1.8C_.D1.81.D0.B5.D1.80.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82)
    *   [2.2 Вручную](#.D0.92.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
*   [3 Расширенная настройка](#.D0.A0.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.BD.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)

## Установка

[Установить](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C "Установить") пакет [certbot](https://www.archlinux.org/packages/?name=certbot).

Плагины доступны для автоматической настройки и установки выданных сертификатов на веб-серверах:

*   Экспериментальный плагин для [Nginx](/index.php/Nginx "Nginx") предоставляется пакетом [certbot-nginx](https://www.archlinux.org/packages/?name=certbot-nginx).
*   Автоматическая установка с использованием [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") включена через пакет [certbot-apache](https://www.archlinux.org/packages/?name=certbot-apache).

## Конфигурация

Для получения дополнительной информации об создании и использовании сертификатов обращайтесь в документацию [Certbot documentation](https://certbot.eff.org/docs/)

### Webroot

**Note:**

*   Метод Webroot требует HTTP на порт 80 для проверки Certbot.
    *   Чтобы Certbot проверял использование HTTPS на порту 443, вместо Webroot следует использовать плагин Nginx (--nginx) или Apache ( --apache) (--webroot).
*   Имя сервера должно соответствовать имени соответствующего DNS.
*   На хосте могут потребоваться разрешения, чтобы разрешить доступ для чтения к `[http://domain.tld/.well-known](http://domain.tld/.well-known)`.

При использовании метода webroot клиент Certbot отправляет запрос вызова внутри `/path/to/domain.tld/html/.well-known/acme-challenge/` который используется для проверки.

Использование этого метода рекомендуется для ручной установки; Он предлагает автоматическое обновление и упрощение управления сертификатами.

**Tip:** The following initial [nginx server](/index.php/Nginx#Server_blocks "Nginx") configuration may be helpful to obtain a first-time certificate: `/etc/nginx/servers-available/domain.tld` 
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

#### Получить сертификат

Запросить сертификат для `domain.tld` с помощью `/var/lib/letsencrypt/`

```
# certbot certonly --email **email@example.com** --webroot -w **/var/lib/letsencrypt/** -d **domain.tld**

```

Чтобы добавить (дополнительный) домен, включите все зарегистрированные домены, используемые в текущей настройке:

```
# certbot certonly --email **email@example.com** --webroot -w **/var/lib/letsencrypt/** -d **domain.tld,sub.domain.tld**

```

Чтобы обновить (все) текущий сертификат (ы):

```
# certbot renew

```

Смотрите [#Automatic renewal](#Automatic_renewal) как альтернативный вариант

### Вручную

**Note:**

*   Управляемый веб-сервер нужно временно приостановить.
*   Автоматическое обновление недоступно при ручной установке, см. [#Webroot](#Webroot).

Если для вашего веб-сервера нет плагина, используйте следующую команду:

```
# certbot certonly --manual

```

Если вы предпочитаете использовать DNS-вызов (запись TXT), используйте:

```
# certbot certonly --manual --preferred-challenges dns

```

Это автоматически проверяет ваш домен и создает закрытый ключ и пару сертификатов. Они размещены в `/etc/letsencrypt/live/*your.domain*/`.

Затем вы можете вручную настроить веб-сервер для использования ключа и сертификата в этом каталоге.

**Note:** Running this command multiple times will create multiple sets of files with a trailing number in `/etc/letsencrypt/live/*your.domain*/` so take care to rename them in that directory or in the webserver config file.

## Расширенная настройка