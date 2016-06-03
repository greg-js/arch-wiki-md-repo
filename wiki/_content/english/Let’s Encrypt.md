[Let’s Encrypt](https://letsencrypt.org/) is a free, automated, and open certificate authority utilizing the [ACME](https://en.wikipedia.org/wiki/Automated_Certificate_Management_Environment "wikipedia:Automated Certificate Management Environment") protocol.

The official client is called **Certbot**, which allows to request valid SSL certificates straight from the command line. A minimal client with manual CSR creation is available at [acme-tiny](https://aur.archlinux.org/packages/acme-tiny/). More integrated clients suitable for scripts are e.g. [simp_le-git](https://aur.archlinux.org/packages/simp_le-git/) and [letsencrypt-cli](https://aur.archlinux.org/packages/letsencrypt-cli/).

**Note:** The official client, which was previously called *the Let’s Encrypt client*, is now called *Certbot*.

## Contents

*   [1 Certbot](#Certbot)
    *   [1.1 Installation](#Installation)
    *   [1.2 Configuration](#Configuration)
        *   [1.2.1 Manual](#Manual)
        *   [1.2.2 Webroot](#Webroot)
            *   [1.2.2.1 Multiple domains](#Multiple_domains)
            *   [1.2.2.2 Automatic renewal](#Automatic_renewal)
*   [2 See also](#See_also)

## Certbot

*Certbot*, previously called *the Let’s Encrypt client*, is the official reference client. It is written in Python and provides a command-line tool to obtain certificates.

### Installation

[Install](/index.php/Install "Install") the [certbot](https://www.archlinux.org/packages/?name=certbot) package.

Plugins are available for automated configuration and installation of the issued certificates in web servers:

*   The experimental plugin for [Nginx](/index.php/Nginx "Nginx") is provided with the [certbot-nginx](https://www.archlinux.org/packages/?name=certbot-nginx) package.
*   Although a package [certbot-apache](https://www.archlinux.org/packages/?name=certbot-apache) exists, automated installation using the [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") is currently only supported on Debian and derivatives.

### Configuration

Please consult the [Certbot documentation](https://certbot.eff.org/docs/) on how to create and install certificates.

#### Manual

**Note:** With this method, you must temporarily stop your web server. You can also run the verification through your already running web server with the [#Webroot](#Webroot) method.

If there is no plugin for your web server, use the following command:

```
# certbot certonly --manual

```

This will automatically verify your domain and create a private key and certificate pair. These are placed in `/etc/letsencrypt/live/*your.domain*/`.

You can then manually configure your web server to use the key and certificate in that directory.

#### Webroot

The webroot method lets the client place a challenge response at `yourdomain.tld/.well-known/acme-challenge/`. You can use it to get/renew certificates with a running webserver (e.g. Apache/nginx).

```
# certbot certonly --email *email@example.com* --webroot -w */path/to/html/* -d *your.domain*

```

Make sure the server configuration for the certificates points to `/etc/letsencrypt/live/*your.domain*/`.

##### Multiple domains

If you use more than one domain or subdomains, the webroot has to be given for every domain. If no new webroot is given, the previous is taken.

Management of this can be made much easier, if you map all http requests for `/.well-known/acme-challenge/` to a single folder, e.g. `/var/lib/letsencrypt`. For nginx you can achieve this by placing this location block within server blocks of sites you want to request certificates for:

```
location /.well-known/acme-challenge {
    root /var/lib/letsencrypt;
    default_type "text/plain";
    try_files $uri =404;
}

```

For Apache you can achieve this by creating the file `httpd-acme.conf`:

 `/etc/httpd/conf/extra/httpd-acme.conf` 
```
Alias /.well-known/acme-challenge/ "/var/lib/letsencrypt/.well-known/acme-challenge/"
<Directory "/var/lib/letsencrypt/">
    AllowOverride None
    Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec
    Require method GET POST OPTIONS
</Directory>

```

and including it in `httpd.conf`:

 `/etc/httpd/conf/httpd.conf` 
```
Include conf/extra/httpd-acme.conf

```

The chosen path has then to be writable for the chosen letsencrypt client. It also has to be readable by the web server; you can achieve this thereby : `chgrp http /var/lib/letsencrypt && chmod g+s /var/lib/letsencrypt`.

##### Automatic renewal

When running `certbot certonly`, Cerbot stores the domains and webroot directories in `/etc/letsencrypt/renewal`, so the certificates can be renewed later automatically by running `certbot renew`.

You can fully automate this by creating the following systemd service file:

 `/etc/systemd/system/certbot.service` 
```
[Unit]
Description=Let's Encrypt renewal

[Service]
Type=oneshot
ExecStart=/usr/bin/certbot renew
```

Before adding a [timer](/index.php/Systemd/Timers "Systemd/Timers"), check that the service is working correctly and is not trying to prompt anything.

Then, you can add a timer to renew the certificates [daily](https://letsencrypt.org/getting-started/#writing-your-own-renewal-script). (The script will automatically skip certificates not due to renewal yet.)

 `/etc/systemd/system/certbot.timer` 
```
[Unit]
Description=Daily renewal of Let's Encrypt's certificates

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target
```

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `certbot.timer`.

You'll probably want your web server to be restarted after each certificate renewal. You can realize that by adding one of these lines to the `certbot.service` file:

*   Apache: `ExecStartPost=/bin/systemctl reload httpd.service`
*   nginx: `ExecStartPost=/bin/systemctl reload nginx.service`

## See also

*   [List of ACME clients](https://github.com/certbot/certbot/wiki/Links#other-lets-encrypt--acme-clients)