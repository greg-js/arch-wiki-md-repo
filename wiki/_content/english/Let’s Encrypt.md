[Let’s Encrypt](https://letsencrypt.org/) is a free, automated, and open certificate authority utilizing the ACME protocol. It provides tools to request valid SSL certificates straight from the command line.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Manual](#Manual)
    *   [2.2 Webroot](#Webroot)
        *   [2.2.1 Automatic renewal](#Automatic_renewal)
*   [3 See also](#See_also)

## Installation

To obtain the official client [install](/index.php/Install "Install") the [letsencrypt](https://www.archlinux.org/packages/?name=letsencrypt) package.

A minimal client with manual CSR creation is available at [acme-tiny](https://aur.archlinux.org/packages/acme-tiny/). More integrated clients suitable for scripts are e.g. [simp_le-git](https://aur.archlinux.org/packages/simp_le-git/) and [letsencrypt-cli](https://aur.archlinux.org/packages/letsencrypt-cli/).

The official client provides plugins for automated configuration and installation of the issued certificates in web servers:

*   The experimental plugin for [Nginx](/index.php/Nginx "Nginx") is provided with the [letsencrypt-nginx](https://www.archlinux.org/packages/?name=letsencrypt-nginx) package.
*   Although a package [letsencrypt-apache](https://www.archlinux.org/packages/?name=letsencrypt-apache) exists, automated installation using the [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") is currently only supported on Debian and derivatives.

## Configuration

Please consult the [Let’s Encrypt client documentation](https://letsencrypt.readthedocs.org/en/latest/) on how to create and install certificates. This wiki will be expanded as soon as certificate installation methods have been crystallized out.

### Manual

**Note:** With this method, you must temporarily stop your web server. You can also run the verification through your already running web server with the [#Webroot](#Webroot) method.

If there is no plugin for your web server, use the following command:

```
# letsencrypt certonly --manual

```

This will automatically verify your domain and create a private key and certificate pair. These are placed in `/etc/letsencrypt/live/*your.domain*/`.

You can then manually configure your web server to use the key and certificate in that directory.

### Webroot

The webroot method lets the client place a challenge response at `yourdomain.tld/.well-known/acme-challenge/`. You can use it to get/renew certificates with a running webserver (e.g. Apache/nginx).

```
# letsencrypt certonly --email *email@example.com* --webroot -w */path/to/html/* -d *your.domain*

```

Make sure the server configuration for the certificates points to `/etc/letsencrypt/live/*your.domain*/`.

If you use more than one domain or subdomains, the webroot has to be given for every domain. If no new webroot is given, the previous is taken.

Management of this can be made much easier, if you instruct you map all http requests for `/.well-known/acme-challenge/` to a single folder, e.g. `/var/lib/letsencrypt`. For nginx you can achieve this with a location block, placed e.g. in `ssl.conf`:

 `ssl.conf` 
```
location /.well-known/acme-challenge {
  alias /var/lib/letsencrypt;
  default_type "text/plain";
  try_files $uri =404;
}
```

For apache you can achieve this by creating the file `httpd-acme.conf`:

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

The chosen path has then to be writable for the chosen letsencrypt client. It also has to be readable by the web server; you can achieve this thereby : `chgrp http /val/lib/letsencrypt && chmod g+s /var/lib/letsencrypt`.

#### Automatic renewal

When running `letsencrypt certonly`, letsencrypt stores the domains and webroot directories in `/etc/letsencrypt/renewal`, so the certificates can be renewed later automatically by running `letsencrypt renew`.

You can fully automate this by creating the following systemd service file:

 `/etc/systemd/system/letsencrypt.service` 
```
[Unit]
Description=Let's Encrypt renewal

[Service]
Type=oneshot
ExecStart=/usr/bin/letsencrypt renew
```

Before adding a [timer](/index.php/Systemd/Timers "Systemd/Timers"), check that the service is working correctly and is not trying to prompt anything.

Then, you can add a timer to renew the certificates monthly.

 `/etc/systemd/system/letsencrypt.timer` 
```
[Unit]
Description=Monthly renewal of Let's Encrypt's certificates

[Timer]
OnCalendar=monthly
Persistent=true

[Install]
WantedBy=timers.target
```

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `letsencrypt.timer`.

You'll probably want your web server to be restarted after each certificate renewal. You can realize that by adding one of these lines to the `letsencrypt.service` file:

*   Apache: `ExecStartPost=/bin/systemctl reload httpd.service`
*   nginx: `ExecStartPost=/bin/systemctl restart nginx.service`

## See also

*   [List of ACME clients](https://community.letsencrypt.org/t/list-of-client-implementations/2103)