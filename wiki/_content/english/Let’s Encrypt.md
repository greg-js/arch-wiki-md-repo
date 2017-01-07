[Let’s Encrypt](https://letsencrypt.org/) is a free, automated, and open certificate authority utilizing the [ACME](https://en.wikipedia.org/wiki/Automated_Certificate_Management_Environment "wikipedia:Automated Certificate Management Environment") protocol.

The official client is called **Certbot**, which allows to request valid X.509 certificates straight from the command line. A minimal client with manual CSR creation is available at [acme-tiny](https://aur.archlinux.org/packages/acme-tiny/), clients suitable for scripts are [simp_le-git](https://aur.archlinux.org/packages/simp_le-git/) and [letsencrypt-cli](https://aur.archlinux.org/packages/letsencrypt-cli/).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Webroot](#Webroot)
        *   [2.1.1 Obtain certificate(s)](#Obtain_certificate.28s.29)
    *   [2.2 Manual](#Manual)
*   [3 Advanced Configuration](#Advanced_Configuration)
    *   [3.1 Webserver Configuration](#Webserver_Configuration)
        *   [3.1.1 nginx](#nginx)
    *   [3.2 Multiple domains](#Multiple_domains)
        *   [3.2.1 nginx](#nginx_2)
        *   [3.2.2 Apache](#Apache)
    *   [3.3 Automatic renewal](#Automatic_renewal)
        *   [3.3.1 systemd](#systemd)
            *   [3.3.1.1 Alternative services](#Alternative_services)
                *   [3.3.1.1.1 nginx](#nginx_3)
                *   [3.3.1.1.2 Apache](#Apache_2)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [certbot](https://www.archlinux.org/packages/?name=certbot) package.

Plugins are available for automated configuration and installation of the issued certificates in web servers:

*   The experimental plugin for [Nginx](/index.php/Nginx "Nginx") is provided with the [certbot-nginx](https://www.archlinux.org/packages/?name=certbot-nginx) package.
*   Although a package [certbot-apache](https://www.archlinux.org/packages/?name=certbot-apache) exists, automated installation using the [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") is currently only supported on Debian and derivatives.

## Configuration

Consult the [Certbot documentation](https://certbot.eff.org/docs/) for more information about creating and usage of certificates.

### Webroot

**Note:**

*   For Apache use --apache or --nginx for Nginx **instead** of --webroot.
*   The webserver should be accessible over HTTP on first-time setup and the DNS-records should be working correctly.
*   Permissions may need to be altered on the host to allow read-access to `[http://domain.tld/.well-know](http://domain.tld/.well-know)`.

When using the webroot method the Certbot client places a challenge response inside `/path/to/domain.tld/html/.well-known/acme-challenge/` which is used for validation.

The use of this method is recommend over a manual install; it offers automatically renewal and easier certificate management.

#### Obtain certificate(s)

Request a certificate for `domain.tld` using `/path/to/domain.tld/html/` as public accessible path:

```
# certbot certonly --email **email@example.com** --webroot -w **/path/to/domain.tld/html/** -d **domain.tld**

```

To add a (sub)domain, include all registered domains used on the current setup:

```
# certbot certonly --email **email@example.com** --webroot -w **/path/to/sub.domain.tld/html/** -d **domain.tld,sub.domain.tld**

```

To renew (all) the current certificate(s):

```
# certbot renew

```

See [#Automatic renewal](#Automatic_renewal) as alternative approach.

### Manual

**Note:**

*   The running webserver has to temporarily stopped.
*   Automatically renewal is not available when performing manual install, see [#Webroot](#Webroot) instead.

If there is no plugin for your web server, use the following command:

```
# certbot certonly --manual

```

When preferring to use DNS challenge (TXT record) use:

```
# certbot certonly --manual --preferred-challenges dns

```

This will automatically verify your domain and create a private key and certificate pair. These are placed in `/etc/letsencrypt/live/*your.domain*/`.

You can then manually configure your web server to use the key and certificate in that directory.

**Note:** Running this command multiple times will create multiple sets of files with a trailing number in `/etc/letsencrypt/live/*your.domain*/` so take care to rename them in that directory or in the webserver config file.

## Advanced Configuration

### Webserver Configuration

Instead of using plugins for automatic configuration, it may be preferred to enable SSL for a server manually.

**Tip:**

*   Mozilla has a useful [SSL/TLS article](https://wiki.mozilla.org/Security/Server_Side_TLS) which includes [nginx specific](https://wiki.mozilla.org/Security/Server_Side_TLS#Nginx) configuration guidelines as well as an [automated tool](https://mozilla.github.io/server-side-tls/ssl-config-generator/) to help create a more secure configuration.
*   [Cipherli.st](https://cipherli.st) provides strong SSL implementation examples and tutorial for most modern webservers.

#### nginx

An example of the server `domain.tld` using the signed SSL-certificate of Let's Encrypt:

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
  ssl_protocols TLSv1.2;
  ssl_ciphers 'ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256';
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

```

### Multiple domains

Management of can be made easier by mapping all HTTP-requests for `/.well-known/acme-challenge/` to a single folder, e.g. `/var/lib/letsencrypt`.

The path has then to be writable for the Let's Encrypt client and the web server (e.g. [nginx](/index.php/Nginx "Nginx") or [Apache](/index.php/Apache "Apache") running as user *http*):

```
# chgrp http /var/lib/letsencrypt
# chmod g+s /var/lib/letsencrypt

```

#### nginx

Create a file containing the location block and include this inside a server block:

 `/etc/nginx/conf/letsencrypt.conf` 
```

location ^~ /.well-known/acme-challenge {
  alias /var/lib/letsencrypt/.well-known/acme-challenge;
  default_type "text/plain";
  try_files $uri =404;
}

```

Example of a server configuration:

 `/etc/nginx/servers-available/domain.conf` 
```
server {
  server_name domain.tld
   ..
  include conf/letsencrypt.conf;
}

```

#### Apache

Create the file `/etc/httpd/conf/extra/httpd-acme.conf`:

 `/etc/httpd/conf/extra/httpd-acme.conf` 
```
Alias /.well-known/acme-challenge/ "/var/lib/letsencrypt/.well-known/acme-challenge/"
<Directory "/var/lib/letsencrypt/">
    AllowOverride None
    Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec
    Require method GET POST OPTIONS
</Directory>

```

Including this in `/etc/httpd/conf/httpd.conf`:

 `/etc/httpd/conf/httpd.conf` 
```
Include conf/extra/httpd-acme.conf

```

### Automatic renewal

#### systemd

Create a [systemd](/index.php/Systemd "Systemd") `certbot.service`:

 `/etc/systemd/system/certbot.service` 
```
[Unit]
Description=Let's Encrypt renewal

[Service]
Type=oneshot
ExecStart=/usr/bin/certbot renew --quiet --agree-tos
```

You'll probably want your web server to reload the certificates after each time they're renewed. You can realize that by adding one of these lines to the `certbot.service` file:

*   Apache: `ExecStartPost=/bin/systemctl reload httpd.service`
*   nginx: `ExecStartPost=/bin/systemctl reload nginx.service`

**Note:** Before adding a [timer](/index.php/Systemd/Timers "Systemd/Timers"), check that the service is working correctly and is not trying to prompt anything.

Add a timer to renew the certificates daily, including a randomized delay so that everyone's requests for renewal will be evenly spread over the day to lighten the Let's Encrypt server load:

 `/etc/systemd/system/certbot.timer` 
```
[Unit]
Description=Daily renewal of Let's Encrypt's certificates

[Timer]
OnCalendar=daily
RandomizedDelaySec=1day
Persistent=true

[Install]
WantedBy=timers.target
```

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `certbot.timer`.

##### Alternative services

When using the standalone method you should stop your webserver before executing the renew request, and start your webserver when Certbot is finished. Certbot provides hooks to automatically stop and restart a web server.

###### nginx

 `/etc/systemd/system/certbot.service` 
```
[Unit]
Description=Let's Encrypt renewal

[Service]
Type=oneshot
ExecStart=/usr/bin/certbot renew --pre-hook "/usr/bin/systemctl stop nginx.service" --post-hook "/usr/bin/systemctl start nginx.service" --quiet --agree-tos
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

## See also

*   [List of ACME clients](https://letsencrypt.org/docs/client-options/)