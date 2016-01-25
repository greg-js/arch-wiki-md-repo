# Let’s Encrypt

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[Let’s Encrypt](https://letsencrypt.org/) is a free, automated, and open certificate authority. It provides tools to request valid ssl certificates straight from the command line.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Manual](#Manual)
    *   [2.2 Webroot](#Webroot)

## Installation

[Install](/index.php/Install "Install") the [letsencrypt](https://www.archlinux.org/packages/?name=letsencrypt) package.

Automated configuration and installation of the issued certificates in web servers is provided by plugins:

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

This will automatically verify your domain and create a private key and certificate pair. These are placed in `/etc/letsencrypt/live/_your.domain_/`.

You can then manually configure your web server to use the key and certificate in that directory.

### Webroot

You can use the webroot method to get/renew certificates with a running webserver (e.g. Apache/nginx).

 `/etc/systemd/system/letsencrypt.service` 

```
[Unit]
Description=Let's Encrypt renewal

[Service]
Type=oneshot
ExecStart=/usr/bin/letsencrypt certonly --agree-tos --renew-by-default --email _email@example.com_ --webroot -w _/path/to/html/_ -d _your.domain_
```

Make sure the server configuration for the certificates points to `/etc/letsencrypt/live/_your.domain_/`.

Before adding a [timer](/index.php/Systemd/Timers "Systemd/Timers"), check that the service is working correctly and not trying to prompt anything.

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

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `letsencrypt.timer`. Also [start](/index.php/Start "Start") `letsencrypt.service` if you want to renew the certificates right now.

If the new certificate is not visible to your web server, you might have to also restart it (e.g. `nginx.service` or `httpd.service`).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Let’s_Encrypt&oldid=417027](https://wiki.archlinux.org/index.php?title=Let’s_Encrypt&oldid=417027)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Networking](/index.php/Category:Networking "Category:Networking")
*   [Encryption](/index.php/Category:Encryption "Category:Encryption")