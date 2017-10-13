[Hiawatha](https://www.hiawatha-webserver.org/) is an open source [web-server](https://en.wikipedia.org/wiki/Web_server "wikipedia:Web server") with security, ease of use and lightweight as its three key features. It supports among others [(Fast)](https://en.wikipedia.org/wiki/FastCGI "wikipedia:FastCGI")[CGI](https://en.wikipedia.org/wiki/Common_Gateway_Interface "wikipedia:Common Gateway Interface"), IPv6, URL rewriting and reverse proxy and has security features no other webserver has, like blocking [SQL injections](https://en.wikipedia.org/wiki/SQL_injection "wikipedia:SQL injection"), [XSS](https://en.wikipedia.org/wiki/Cross-site_scripting "wikipedia:Cross-site scripting"), [CSRF](https://en.wikipedia.org/wiki/Cross-site_scripting "wikipedia:Cross-site scripting") and exploit attempts.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Directory structure](#Directory_structure)
    *   [2.2 Basic webserver setup](#Basic_webserver_setup)
    *   [2.3 Normal CGI](#Normal_CGI)
        *   [2.3.1 Interpreters for CGI scripts](#Interpreters_for_CGI_scripts)
    *   [2.4 FastCGI](#FastCGI)
        *   [2.4.1 PHP via FastCGI](#PHP_via_FastCGI)
    *   [2.5 Reverse Proxy](#Reverse_Proxy)
    *   [2.6 SSL/TLS](#SSL.2FTLS)
*   [3 Let's Encrypt](#Let.27s_Encrypt)
    *   [3.1 Install](#Install)
    *   [3.2 Obtain a certificate](#Obtain_a_certificate)
    *   [3.3 Auto renewal](#Auto_renewal)
        *   [3.3.1 Automation with cron](#Automation_with_cron)
        *   [3.3.2 Automation with systemd/Timers](#Automation_with_systemd.2FTimers)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [hiawatha](https://www.archlinux.org/packages/?name=hiawatha) package.

## Configuration

### Directory structure

First, to give an overview of the overall directory structure of Hiawatha, the hierarchy suggested by the default configuration is shown below:

	`/etc/hiawatha`

	program configuration files

	`/etc/hiawatha/tls`

	website TLS certificate

	`/srv/http/hiawatha`

	root for the default blank website associated with the IP address

	`/var/log/hiawatha`

	log files for Hiawatha and for the default blank website associated with the IP address

	`/srv/http/*my-domain*/public`

	website root

	`/srv/http/*my-domain*/log`

	website log files

### Basic webserver setup

The Hiawatha configuration file is `/etc/hiawatha/hiawatha.conf`. A configuration file example `/etc/hiawatha/hiawatha.conf.sample` is provided.

In the sample setup, there is one default website attached to the IP address of the domain, it is a dummy one directing to a blank html page. This is the page IP scanning robots and hackers will face.

Then, the working webservers are defined with `VirtualHost` sections. Hiawatha can serve more than one webserver and each of these sections describes a different one. For initial testing purpose, you can create one `VirtualHost` for *my-domain* and save in its root directory `/srv/http/*my-domain*/public` a dummy `index.html` start file.

Next, [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `hiawatha.service` and point your browser to `http://*my-domain*`. At that stage you should be able to load the website start page.

For further details see the official [HowTo](https://www.hiawatha-webserver.org/howto).

**Note:** Hiawatha supports on-the-fly [gzip content encoding](https://en.wikipedia.org/wiki/HTTP_compression "wikipedia:HTTP compression"). It will gzip the requested file and cache it on disk in `/var/lib/hiawatha/gzipped`. Every time the file is requested again, the already gzipped version from disk will be used. It will notice (timestamp and size) file changes and the cache is cleared upon restart.

### Normal CGI

[Common Gateway Interface](https://en.wikipedia.org/wiki/Common_Gateway_Interface "wikipedia:Common Gateway Interface") (CGI) scripts work with Hiawatha out of the box, you just need to enable the CGI module in the `VirtualHost` section as follows:

 `/etc/hiawatha/hiawatha.conf` 
```
VirtualHost {
    ...
    ExecuteCGI = yes
}
```

#### Interpreters for CGI scripts

To use CGI scripts in your website, you have to specify where Hiawatha can find the binary that can run them. This is configured by associating the interpreter with the script extensions in the main body of the configuration file:

```
CGIhandler = /usr/bin/php5-cgi:php,php5
CGIhandler = /usr/bin/perl:pl
CGIhandler = /usr/bin/python:py

```

**Note:** The corresponding language interpreters should be installed. For *php* you need both [php](https://www.archlinux.org/packages/?name=php) and [php-cgi](https://www.archlinux.org/packages/?name=php-cgi), for *python* [python](https://www.archlinux.org/packages/?name=python).

For further details see the official [HowTo](https://www.hiawatha-webserver.org/howto/cgi_and_fastcgi).

### FastCGI

[Install](/index.php/Install "Install") [fcgi](https://www.archlinux.org/packages/?name=fcgi).

Hiawatha supports two different methods to send information to the FastCGI process: the webserver can communicate over either a *Unix domain socket* or a *TCP connection*. The communication type is defined in the `FastCGIServer` section via the field `ConnectTo`.

#### PHP via FastCGI

Install [php](https://www.archlinux.org/packages/?name=php), [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) and [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) (see also [PHP](/index.php/PHP "PHP") and [LAMP](/index.php/LAMP "LAMP")). [Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `php-fpm.service`. You can check that [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) is working properly by executing `$ php-cgi --version`.

To activate a FastCGI server with [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) using a *UNIX socket*, a `FastCGIserver` section is needed in the configuration file:

 `/etc/hiawatha/hiawatha.conf` 
```
FastCGIserver {
    FastCGIid = PHP7
    ConnectTo = /run/php-fpm/php-fpm.sock
    Extension = php
    SessionTimeout = 30
}
```

To connect to the FastCGI process in *TCP* mode, use instead `ConnectTo = 127.0.0.1:9000` in the `FastCGIserver` section above to indicate the IP-address and TCP port Hiawatha should use to reach the FastCGI server.

Eventually, to use the previously defined `FastCGIserver` with your webserver, just reference it as follows:

 `/etc/hiawatha/hiawatha.conf` 
```
VirtualHost {
    ...
    UseFastCGI = PHP7
}
```

Then [restart](/index.php/Restart "Restart") the `hiawatha.service`.

### Reverse Proxy

This example shows a reverse proxy configuration which forwards requests to `https://service.domain.net` to another local running web service on port `8181`:

 `/etc/hiawatha/hiawatha.conf` 
```
VirtualHost {
        Hostname = service.domain.net
        WebsiteRoot = /var/www/domain
        StartFile = index.html
        ReverseProxy .* http://127.0.0.1:8181/
        RequireTLS = yes
}

```

### SSL/TLS

First, you need a *X.509 SSL/TLS* certificate to use TLS. If you do not, you can obtain one for free from [#Let's Encrypt](#Let.27s_Encrypt) certificate authority.

The order of the items in the certificate file is important and has to be as follows:

 `serverkey.pem` 
```
-----BEGIN RSA PRIVATE KEY-----
[webserver private key]
-----END RSA PRIVATE KEY----- 

-----BEGIN CERTIFICATE-----
[webserver certificate]
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
[optional intermediate CA certificate]
-----END CERTIFICATE-----

```

For SSL/TLS support, the following `Binding` section that configures Hiawatha to use a certificate for HTTPS connections should be added:

 `/etc/hiawatha/hiawatha.conf` 
```
Binding {
    Port = 443
    TLScertFile = /etc/hiawatha/tls/serverkey.pem
}
```

Once it is done, [restart](/index.php/Restart "Restart") the `hiawatha.service`.

**Tip:** Hiawatha supports [Server Name Indication](https://en.wikipedia.org/wiki/Server_Name_Indication "wikipedia:Server Name Indication"), which allows to serve multiple certificates on the same IP address and hence multiple secure websites. To use this functionality, add a `TLScertFile` setting inside the `VirtualHost` block for each virtual host that has its own SSL/TLS certificate. The certificate specified in the `Binding` section is used whenever no virtual host has been defined for a website. `/etc/hiawatha/hiawatha.conf` 
```
VirtualHost {
    Hostname = www.website.org
    ...
    TLScertFile = website.pem
}

```

## Let's Encrypt

### Install

Hiawatha provides a script to obtain a [Let’s Encrypt](/index.php/Let%E2%80%99s_Encrypt "Let’s Encrypt") certificate in an automated fashion. Download it into your preferred location (for example `/root`):

```
$ curl [https://www.hiawatha-webserver.org/files/letsencrypt.tar.gz](https://www.hiawatha-webserver.org/files/letsencrypt.tar.gz) | tar -xz

```

Alternatively, the script is also available within the [source tarball](https://github.com/hsleisink/hiawatha/archive/master.zip) in `extra/letsencrypt`.

### Obtain a certificate

The detailed instructions are described in `README.txt` and the tool configuration is defined in `letsencrypt.conf`. In short, there are two steps to get a certificate:

1.  Register an account with the Let's Encrypt certificate authority (CA). An account key file will be created. `$ ./letsencrypt register` 
2.  Request a website certificate: *www.my-domain.org* must be the first hostname of a `VirtualHost`. Any following webserver's hostname will be used as an alternative hostname for the certificate. The file `www.my-domain.org.pem` will be created. `$ ./letsencrypt request www.my-domain.org` 

If the above succeeds, you can switch from the ***testing*** to the ***production*** CA by changing the `LE_CA_HOSTNAME` setting in the configuration file and go through the **two steps** above again.

### Auto renewal

The following command can be used to renew the certificate and restart the server upon renewal:

```
$ /path/to/letsencrypt renew restart

```

The certificate will be renewed whenever it has less than 7 days to go and written to the directory indicated in `HIAWATHA_CERT_DIR`. The number of days before renewal is controlled via the `RENEWAL_EXPIRE_THRESHOLD` setting if necessary.

A daily schedule of this script is appropriate as no action will be taken anyway before the threshold is reached. This daily automation can be achieved using either [cron](/index.php/Cron "Cron") or [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers"):

#### Automation with cron

In order to automate the renewal of the certificate, schedule a cronjob for the root user to run the command line above.

#### Automation with systemd/Timers

Both service and timer unit files need to be created:

 `/etc/systemd/system/letsencrypt-renew.service ` 
```
[Unit]
Description=Renew Let's Encrypt certificates

[Service]
Type=oneshot
ExecStart=/path/to/letsencrypt renew restart

```
 `/etc/systemd/system/letsencrypt-renew.timer ` 
```
[Unit]
Description=Daily renewal of Let's Encrypt's certificates

[Timer]
OnCalendar=daily
# Be kind to the Let's Encrypt servers: add a random delay of 0–3600 seconds
RandomizedDelaySec=3600
Persistent=true

[Install]
WantedBy=timers.target

```

[start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the newly created `letsencrypt-renew.timer`.

## See also

*   [Hiawatha Support page](https://www.hiawatha-webserver.org/support)