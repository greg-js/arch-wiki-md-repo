[Certbot](https://github.com/certbot/certbot) is [Electronic Frontier Foundation](https://www.eff.org/)'s [ACME](/index.php/ACME "ACME") client, which is written in Python and provides conveniences like automatic web server configuration and a built-in webserver for the HTTP challenge. Certbot is recommended by [Let's Encrypt](https://letsencrypt.org/).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Plugins](#Plugins)
        *   [2.1.1 Nginx](#Nginx)
            *   [2.1.1.1 Managing server blocks](#Managing_server_blocks)
    *   [2.2 Webroot](#Webroot)
        *   [2.2.1 Mapping ACME-challenge requests](#Mapping_ACME-challenge_requests)
            *   [2.2.1.1 nginx](#nginx_2)
            *   [2.2.1.2 Apache](#Apache)
        *   [2.2.2 Obtain certificate(s)](#Obtain_certificate.28s.29)
    *   [2.3 Manual](#Manual)
*   [3 Advanced Configuration](#Advanced_Configuration)
    *   [3.1 Automatic renewal](#Automatic_renewal)
        *   [3.1.1 systemd](#systemd)
    *   [3.2 Automatic renewal for wildcard certificates](#Automatic_renewal_for_wildcard_certificates)
        *   [3.2.1 Configure BIND for rfc2136](#Configure_BIND_for_rfc2136)
        *   [3.2.2 Configure certbot for rfc2136](#Configure_certbot_for_rfc2136)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [certbot](https://www.archlinux.org/packages/?name=certbot) package.

Plugins are available for automated configuration and installation of the issued certificates in web servers:

*   The [Nginx](/index.php/Nginx "Nginx") plugin can be installed with the [certbot-nginx](https://www.archlinux.org/packages/?name=certbot-nginx) package.
*   The [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") plugin can be installed with the [certbot-apache](https://www.archlinux.org/packages/?name=certbot-apache) package.

## Configuration

Consult the [Certbot documentation](https://certbot.eff.org/docs/) for more information about creation and usage of certificates.

### Plugins

**Warning:** Configuration files may be rewritten when using a plugin. Creating a **backup** first is recommended.

#### Nginx

The plugin [certbot-nginx](https://www.archlinux.org/packages/?name=certbot-nginx) provides an automatic configuration for [nginx](/index.php/Nginx "Nginx") [server-blocks](/index.php/Nginx#Server_blocks "Nginx"):

```
# certbot --nginx

```

To renew certificates:

```
# certbot renew

```

To change certificates without modifying nginx config files:

```
# certbot --nginx certonly

```

See [Nginx on Arch Linux](https://certbot.eff.org/#arch-nginx) for more information and [#Automatic renewal](#Automatic_renewal) to keep installed certificates valid.

##### Managing server blocks

The following example may be used in each [server-blocks](/index.php/Nginx#Server_blocks "Nginx") when managing these files manually:

 `/etc/nginx/sites-available/example` 
```
server {
  listen 443 ssl http2;
  listen [::]:443 ssl http2; # Listen on IPv6
  ssl_certificate /etc/letsencrypt/live/*domain*/fullchain.pem; # managed by Certbot
  ssl_certificate_key /etc/letsencrypt/live/*domain*/privkey.pem; # managed by Certbot
  include /etc/letsencrypt/options-ssl-nginx.conf;
  ..
}
```

See [nginx#TLS/SSL](/index.php/Nginx#TLS.2FSSL "Nginx") for more information.

It's also possible to create a separated config file and include it in each server block:

 `/etc/nginx/conf/001-certbot.conf` 
```
ssl_certificate /etc/letsencrypt/live/*domain*/fullchain.pem; # managed by Certbot
ssl_certificate_key /etc/letsencrypt/live/*domain*/privkey.pem; # managed by Certbot
include /etc/letsencrypt/options-ssl-nginx.conf;
```
 `/etc/nginx/sites-available/example` 
```
server {
  listen 443 ssl http2;
  listen [::]:443 ssl http2; # Listen on IPv6
  include conf/001-certbot.conf;
  ..
}

```

### Webroot

**Note:**

*   The Webroot method requires **HTTP on port 80** for Certbot to validate.
*   The Server Name must match that of its corresponding DNS.
*   Permissions may need to be altered on the host to allow read-access to `[http://domain.tld/.well-known](http://domain.tld/.well-known)`.

When using the webroot method the Certbot client places a challenge response inside `/path/to/domain.tld/html/.well-known/acme-challenge/` which is used for validation.

The use of this method is recommend over a manual install; it offers automatic renewal and easier certificate management. However the usage of [#Plugins](#Plugins) may be the preferred since it allows automatic configuration and installation.

#### Mapping ACME-challenge requests

Management of can be made easier by mapping all HTTP-requests for `.well-known/acme-challenge` to a single folder, e.g. `/var/lib/letsencrypt`.

The path has then to be writable for Cerbot and the web server (e.g. [nginx](/index.php/Nginx "Nginx") or [Apache](/index.php/Apache "Apache") running as user *http*):

```
# mkdir -p /var/lib/letsencrypt/.well-known
# chgrp http /var/lib/letsencrypt
# chmod g+s /var/lib/letsencrypt

```

##### nginx

Create a file containing the location block and include this inside a server block:

 `/etc/nginx/conf.d/letsencrypt.conf` 
```
location ^~ /.well-known/acme-challenge/ {
  allow all;
  root /var/lib/letsencrypt/;
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

##### Apache

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

This will automatically verify your domain and create a private key and certificate pair. These are placed in `/etc/letsencrypt/archive/*your.domain*/` and symlinked from `/etc/letsencrypt/live/*your.domain*/`.

You can then manually configure your web server to reference the private key, certificate and full certificate chain in the symlinked directory.

**Note:** Running this command multiple times, or renewing certificates will create multiple sets of files with a trailing number in `/etc/letsencrypt/archive/*your.domain*/`. Certbot automatically updates the symlinks in `/etc/letsencrypt/live/*your.domain*/` to point to the latest instances of files so there is no need to update your webserver to point to the new key material.

## Advanced Configuration

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

If you do not use a plugin to manage the web server configuration automatically, the web server has to be reloaded manually to reload the certificates each time they are renewed. This can be done by adding `--deploy-hook "systemctl reload nginx.service"` to the `ExecStart` command [[1]](https://certbot.eff.org/docs/using.html#renewing-certificates). Of course use `httpd.service` instead of `nginx.service` if appropriate.

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

### Automatic renewal for wildcard certificates

The process is fairly simple. To issue a wildcard certificate, you have to do it via a DNS challenge request, [using the ACMEv2 protocol](https://community.letsencrypt.org/t/acme-v2-and-wildcard-certificate-support-is-live/55579).

While issuing a certificate manually is easy, it's not straight forward for automation. The DNS challenge represents a TXT record, given by certbot, which has to be set manually in the domain zone file.

You will need to update the zone file upon every renew. To avoid doing that manually, you may use [rfc2136](https://tools.ietf.org/html/rfc2136) for which certbot has a plugin packaged in [certbot-dns-rfc2136](https://www.archlinux.org/packages/?name=certbot-dns-rfc2136). You will also need to configure your DNS server to allow dynamic updates for TXT records.

#### Configure BIND for rfc2136

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

#### Configure certbot for rfc2136

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

If you pass the validation successfully and receive certificates, then you are good to go with automating certbot. Otherwise, something went wrong and you need to debug your setup. It basically boils down to running `certbot renew` from now on, see [#Automatic renewal](#Automatic_renewal).

## See also

*   [Wikipedia article](https://en.wikipedia.org/wiki/Let%27s_Encrypt "wikipedia:Let's Encrypt")
*   [EFF's Certbot documentation](https://certbot.eff.org/)
*   [List of ACME clients](https://letsencrypt.org/docs/client-options/)