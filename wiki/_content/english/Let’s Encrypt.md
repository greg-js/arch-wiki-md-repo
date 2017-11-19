[Let’s Encrypt](https://letsencrypt.org/) is a free, automated, and open certificate authority utilizing the [ACME](https://en.wikipedia.org/wiki/Automated_Certificate_Management_Environment "wikipedia:Automated Certificate Management Environment") protocol.

The official client is called **Certbot**, which allows to request valid X.509 certificates straight from the command line. A minimal client with manual CSR creation is available at [acme-tiny](https://aur.archlinux.org/packages/acme-tiny/), clients suitable for scripts are [simp_le-git](https://aur.archlinux.org/packages/simp_le-git/) and [letsencrypt-cli](https://aur.archlinux.org/packages/letsencrypt-cli/).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Plugins](#Plugins)
        *   [2.1.1 Nginx](#Nginx)
    *   [2.2 Webroot](#Webroot)
        *   [2.2.1 Obtain certificate(s)](#Obtain_certificate.28s.29)
    *   [2.3 Manual](#Manual)
*   [3 Advanced Configuration](#Advanced_Configuration)
    *   [3.1 Webserver Configuration](#Webserver_Configuration)
        *   [3.1.1 nginx](#nginx_2)
    *   [3.2 Multiple domains](#Multiple_domains)
        *   [3.2.1 nginx](#nginx_3)
        *   [3.2.2 Apache](#Apache)
    *   [3.3 Automatic renewal](#Automatic_renewal)
        *   [3.3.1 systemd](#systemd)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [certbot](https://www.archlinux.org/packages/?name=certbot) package.

Plugins are available for automated configuration and installation of the issued certificates in web servers:

*   The experimental plugin for [Nginx](/index.php/Nginx "Nginx") is provided with the [certbot-nginx](https://www.archlinux.org/packages/?name=certbot-nginx) package.
*   Automated installation using the [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") is enabled via the [certbot-apache](https://www.archlinux.org/packages/?name=certbot-apache) package.

## Configuration

Consult the [Certbot documentation](https://certbot.eff.org/docs/) for more information about creation and usage of certificates.

### Plugins

#### Nginx

The plugin [certbot-nginx](https://www.archlinux.org/packages/?name=certbot-nginx) provides an automatic configuration for [nginx](/index.php/Nginx "Nginx") [server-blocks](/index.php/Nginx#Server_blocks "Nginx"):

```
# certbot --nginx

```

To renew certificates, simple run:

```
# certbot renew

```

See [#Automatic renewal](#Automatic_renewal) to keep installed certificates valid.

### Webroot

**Note:**

*   The Webroot method requires **HTTP on port 80** for Certbot to validate.
*   The Server Name must match that of it's corresponding DNS.
*   Permissions may need to be altered on the host to allow read-access to `[http://domain.tld/.well-known](http://domain.tld/.well-known)`.

When using the webroot method the Certbot client places a challenge response inside `/path/to/domain.tld/html/.well-known/acme-challenge/` which is used for validation.

The use of this method is recommend over a manual install; it offers automatic renewal and easier certificate management.

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

  # ACME challenge
  location ^~ /.well-known/acme-challenge/ {
    default_type "text/plain";
    root /var/lib/letsencrypt;
  }
}

```

#### Obtain certificate(s)

Request a certificate for `domain.tld` using `/var/lib/letsencrypt/` as public accessible path:

```
# certbot certonly --email **email@example.com** --webroot -w **/var/lib/letsencrypt/** -d **domain.tld**

```

To add a (sub)domain, include all registered domains used on the current setup:

```
# certbot certonly --email **email@example.com** --webroot -w **/var/lib/letsencrypt/** -d **domain.tld,sub.domain.tld**

```

To renew (all) the current certificate(s):

```
# certbot renew

```

See [#Automatic renewal](#Automatic_renewal) as alternative approach.

### Manual

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

*   Mozilla has a useful [SSL/TLS article](https://wiki.mozilla.org/Security/Server_Side_TLS) which includes an [automated tool](https://mozilla.github.io/server-side-tls/ssl-config-generator/) to help create a more secure configuration.
*   [Cipherli.st](https://cipherli.st) provides strong SSL implementation examples and tutorial for most modern webservers.

#### nginx

An example of the server `domain.tld` using the signed SSL-certificate of Let's Encrypt:

 `/etc/nginx/servers-available/domain.tld` 
```

server {
  listen 443 ssl http2;
  listen [::]:443 ssl http2;
  ssl_certificate /etc/letsencrypt/live/domain.tld/fullchain.pem;
  ssl_certificate_key /etc/letsencrypt/live/domain.tld/privkey.pem;
  ssl_trusted_certificate /etc/letsencrypt/live/domain.tld/chain.pem;
  server_name domain.tld;
  ..
}

```

### Multiple domains

Management of can be made easier by mapping all HTTP-requests for `/.well-known/acme-challenge/` to a single folder, e.g. `/var/lib/letsencrypt`.

The path has then to be writable for the Let's Encrypt client and the web server (e.g. [nginx](/index.php/Nginx "Nginx") or [Apache](/index.php/Apache "Apache") running as user *http*):

```
# mkdir -p /var/lib/letsencrypt/.well-known
# chgrp http /var/lib/letsencrypt
# chmod g+s /var/lib/letsencrypt

```

#### nginx

Create a file containing the location block and include this inside a server block:

 `/etc/nginx/conf.d/letsencrypt.conf` 
```

location ^~ /.well-known {
  allow all;
  alias /var/lib/letsencrypt/.well-known/;
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
  include conf.d/letsencrypt.conf;
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

You'll probably want your web server to reload the certificates after each time they're renewed. This can be done by adding `--post-hook "systemctl reload nginx.service"` to the `ExecStart` command [[1]](https://certbot.eff.org/docs/using.html#renewing-certificates). Of course use `httpd.service` instead of `nginx.service` if appropriate.

**Note:** Before adding a [timer](/index.php/Systemd/Timers "Systemd/Timers"), check that the service is working correctly and is not trying to prompt anything.

Add a timer to check for certificate renewal twice a day and include a randomized delay so that everyone's requests for renewal will be spread over the day to lighten the Let's Encrypt server load [[2]](https://certbot.eff.org/#arch-nginx):

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

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `certbot.timer`.

## See also

*   [EFF's Certbot documentation](https://certbot.eff.org/)
*   [List of ACME clients](https://letsencrypt.org/docs/client-options/)