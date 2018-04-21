[Hiawatha](https://www.hiawatha-webserver.org/) is an open source [web-server](https://en.wikipedia.org/wiki/Web_server "wikipedia:Web server") with security, ease of use and lightweight as its three key features. It supports among others [CGI](https://en.wikipedia.org/wiki/Common_Gateway_Interface "wikipedia:Common Gateway Interface"), [FastCGI](https://en.wikipedia.org/wiki/FastCGI "wikipedia:FastCGI"), IPv6, URL rewriting and reverse proxy and has security features no other webserver has, like blocking [SQL injections](https://en.wikipedia.org/wiki/SQL_injection "wikipedia:SQL injection"), [XSS](https://en.wikipedia.org/wiki/Cross-site_scripting "wikipedia:Cross-site scripting"), [CSRF](https://en.wikipedia.org/wiki/Cross-site_scripting "wikipedia:Cross-site scripting") and exploit attempts.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Directory structure](#Directory_structure)
    *   [2.2 Basic webserver setup](#Basic_webserver_setup)
    *   [2.3 CGI](#CGI)
        *   [2.3.1 Interpreters for CGI scripts](#Interpreters_for_CGI_scripts)
    *   [2.4 FastCGI](#FastCGI)
    *   [2.5 Enable SSL/TLS](#Enable_SSL.2FTLS)
    *   [2.6 Reverse proxy](#Reverse_proxy)
*   [3 Certificates](#Certificates)
    *   [3.1 Self-signed certificate](#Self-signed_certificate)
    *   [3.2 Let's Encrypt certificate](#Let.27s_Encrypt_certificate)
        *   [3.2.1 Install](#Install)
        *   [3.2.2 Obtain a certificate](#Obtain_a_certificate)
        *   [3.2.3 Auto renewal](#Auto_renewal)
            *   [3.2.3.1 Automation with cron](#Automation_with_cron)
            *   [3.2.3.2 Automation with a systemd timer](#Automation_with_a_systemd_timer)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [hiawatha](https://www.archlinux.org/packages/?name=hiawatha) package.

## Configuration

### Directory structure

First, to give an overview of the overall directory structure of Hiawatha, the hierarchy suggested by the default configuration is shown below:

*   `/etc/hiawatha` - program configuration files
*   `/etc/hiawatha/tls` - website TLS certificate
*   `/srv/http/hiawatha` - root for the default blank website associated with the IP address
*   `/var/lib/hiawatha` - cache for http compression and uploads
*   `/var/log/hiawatha` - log files for the program and the default website
*   `/srv/http/*my-domain*/public` - website root
*   `/srv/http/*my-domain*/log` - website log files

### Basic webserver setup

The Hiawatha configuration file is `/etc/hiawatha/hiawatha.conf`. A configuration file example `/etc/hiawatha/hiawatha.conf.sample` is provided.

In the sample setup, there is one default website attached to the IP address of the domain, it is a dummy one directing to a blank html page. This is the page IP scanning robots and hackers will face.

Then, the working webservers are defined with `VirtualHost` sections. Hiawatha can serve more than one webserver and each of these sections describes a different one. For initial testing purpose, you can create one `VirtualHost` for *my-domain* and save in its root directory `/srv/http/*my-domain*/public` a dummy `index.html` start file.

Next, [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `hiawatha.service` and point your browser to `http://*my-domain*`. At that stage you should be able to load the website start page.

For further details see the official [how to](https://www.hiawatha-webserver.org/howto) and the [hiawatha(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hiawatha.1) manual page.

**Note:** Hiawatha supports on-the-fly [gzip content encoding](https://en.wikipedia.org/wiki/HTTP_compression "wikipedia:HTTP compression"). It will gzip the requested file and cache it on disk in `/var/lib/hiawatha/gzipped`. Every time the file is requested again, the already gzipped version from disk will be used. It will notice (timestamp and size) file changes and the cache is cleared upon restart.

### CGI

[Common Gateway Interface](https://en.wikipedia.org/wiki/Common_Gateway_Interface "wikipedia:Common Gateway Interface") (*CGI*) scripts work with Hiawatha out of the box, the CGI module in the `VirtualHost` section just needs to be enabled as follows:

 `/etc/hiawatha/hiawatha.conf` 
```
VirtualHost {
    ...
    ExecuteCGI = yes
}
```

#### Interpreters for CGI scripts

To use CGI scripts in your website, you have to specify the common script file extension and the location of the binary that can run them. This is indicated in the main body of the configuration file:

```
CGIhandler = /usr/bin/php5-cgi:php,php5
CGIhandler = /usr/bin/perl:pl
CGIhandler = /usr/bin/python:py

```

**Note:** The corresponding language interpreters should be installed: for *php* both [php](https://www.archlinux.org/packages/?name=php) and [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) are needed, for *python* [python](https://www.archlinux.org/packages/?name=python) is required.

For further details see the official [HowTo](https://www.hiawatha-webserver.org/howto/cgi_and_fastcgi).

### FastCGI

[Install](/index.php/Install "Install") [fcgi](https://www.archlinux.org/packages/?name=fcgi).

Hiawatha supports two different methods to send information to the FastCGI process: the webserver can communicate over either a *Unix domain socket* or a *TCP connection*. The communication type is defined in the `FastCGIServer` section via the field `ConnectTo`.

### Enable SSL/TLS

First, a *X.509 SSL/TLS* certificate is required to use TLS. If you do not have one, you can use a [#Self-signed certificate](#Self-signed_certificate) or use one for free from [#Let's Encrypt certificate](#Let.27s_Encrypt_certificate) authority.

The order of the items in the certificate file must be as follows:

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

Once it is done, [restart](/index.php/Restart "Restart") `hiawatha.service`.

**Tip:** Hiawatha supports [Server Name Indication](https://en.wikipedia.org/wiki/Server_Name_Indication "wikipedia:Server Name Indication"), which allows to serve multiple certificates on the same IP address and hence multiple secure websites. To use this functionality, add a `TLScertFile` setting inside the `VirtualHost` block for each virtual host that has its own SSL/TLS certificate. The certificate specified in the `Binding` section is used whenever no virtual host has been defined for a website. `/etc/hiawatha/hiawatha.conf` 
```
VirtualHost {
    Hostname = www.website.org
    ...
    TLScertFile = website.pem
}

```

### Reverse proxy

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

## Certificates

### Self-signed certificate

To get a local self-signed certificate for personal use, testing or web development, the procedure in [OpenSSL#Self-signed certificate](/index.php/OpenSSL#Self-signed_certificate "OpenSSL") to create both a private key and a self-signed certificate can be followed.

Make sure you did add the SSL bundle path to your `hiawatha.conf` as stated in [#Enable SSL/TLS](#Enable_SSL.2FTLS).

As this solution does not use an official certificate authority (CA), a security exception will need to be added the first time the website is visited.

### Let's Encrypt certificate

#### Install

Hiawatha provides a script to obtain a [Let’s Encrypt](/index.php/Let%E2%80%99s_Encrypt "Let’s Encrypt") certificate in an automated fashion. The script and the [systemd](/index.php/Systemd "Systemd") *.service* and *.timer* files are available in `/usr/share/hiawatha/letsencrypt.tar.gz` and should be unarchived into your preferred location, for example `/root`.

#### Obtain a certificate

The detailed instructions are described in `README.txt` and the tool configuration is defined in `letsencrypt.conf`. In short, there are two steps to get a certificate:

1.  Register an account with the Let's Encrypt certificate authority (CA). An account key file will be created. `$ ./letsencrypt register` 
2.  Request a website certificate: *www.my-domain.org* must be the first hostname of a `VirtualHost`. Any following webserver's hostname will be used as an alternative hostname for the certificate. The file `www.my-domain.org.pem` will be created. `# ./letsencrypt request www.my-domain.org` 

If the above succeeds, you can switch from the ***testing*** to the ***production*** CA by changing the `LE_CA_HOSTNAME` setting in the configuration file and go through the **two steps** above again.

#### Auto renewal

The following command can be used to renew the certificate and restart the server upon renewal:

```
# */path/to*/letsencrypt renew restart

```

By default, the certificate will be renewed whenever it has less than 7 days to go and it will be written in the directory indicated in `HIAWATHA_CERT_DIR`. The number of days before renewal can be controlled via the `RENEWAL_EXPIRE_THRESHOLD` setting.

A daily schedule of this script is appropriate as no action will be taken anyway before the threshold is reached. This daily automation can be achieved using either [cron](/index.php/Cron "Cron") or [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers"):

##### Automation with cron

In order to automate the renewal of the certificate, schedule a cronjob for the root user to run the command line above.

##### Automation with a systemd timer

A [systemd timer](/index.php/Systemd/Timers "Systemd/Timers") can be used for the repetition of the renewal process, both service and timer unit files are provided in the package:

 `/etc/systemd/system/letsencrypt-renew.service ` 
```
[Unit]
Description=Renew Let's Encrypt certificates
Wants=network-online.target
After=network-online.target

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
# Be kind to the Let's Encrypt servers: add a random delay of 12 hours
RandomizedDelaySec=12h
Persistent=true

[Install]
WantedBy=timers.target

```

[start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the `letsencrypt-renew.timer`.

**Note:** The service waits for the network to be up and online, for more information on the implementation of the network dependency, see [Systemd#Running services after the network is up](/index.php/Systemd#Running_services_after_the_network_is_up "Systemd").

## See also

*   [Hiawatha Support page](https://www.hiawatha-webserver.org/support)