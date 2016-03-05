[Hiawatha](https://www.hiawatha-webserver.org/) is "an open source [web-server](https://en.wikipedia.org/wiki/Web_server "wikipedia:Web server") with security, easy to use and lightweight as the three key features. It supports among others [(Fast)](https://en.wikipedia.org/wiki/FastCGI "wikipedia:FastCGI")[CGI](https://en.wikipedia.org/wiki/Common_Gateway_Interface "wikipedia:Common Gateway Interface"), IPv6, URL rewriting and reverse proxy and has security features no other webserver has, like blocking [SQL injections](https://en.wikipedia.org/wiki/SQL_injection "wikipedia:SQL injection"), [XSS](https://en.wikipedia.org/wiki/Cross-site_scripting "wikipedia:Cross-site scripting"), [CSRF](https://en.wikipedia.org/wiki/Cross-site_scripting "wikipedia:Cross-site scripting") and exploit attempts."

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Basic Setup](#Basic_Setup)
    *   [2.2 CGI](#CGI)
    *   [2.3 FastCGI](#FastCGI)
        *   [2.3.1 PHP](#PHP)
        *   [2.3.2 Ruby on Rails](#Ruby_on_Rails)
        *   [2.3.3 Python FastCGI](#Python_FastCGI)
    *   [2.4 SSL](#SSL)
        *   [2.4.1 Let's Encrypt](#Let.27s_Encrypt)
        *   [2.4.2 Server Name Indication](#Server_Name_Indication)
    *   [2.5 Output Compression](#Output_Compression)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [hiawatha](https://www.archlinux.org/packages/?name=hiawatha) package.

## Configuration

### Basic Setup

The Hiawatha configuration file is: `/etc/hiawatha/hiawatha.conf`. By default it should produce a 404 page.

The default configuration file suggests `/srv/http/my-domain/public` as the document directory served. To test the installation, create a dummy file:

 `/srv/http/my-domain/public/index.html`  `Hello world!` 

Edit the VIRTUAL HOSTS section in the config file to fit your needs.

Then [start/enable](/index.php/Start/enable "Start/enable") the `hiawatha.service` and point your browser to `my-domain`, where you should see the test page.

A very good example configuration file is available at `/etc/hiawatha/hiawatha.conf.sample`.

For further details see the official [HowTo](https://www.hiawatha-webserver.org/howto).

### CGI

[Common Gateway Interface](https://en.wikipedia.org/wiki/Common_Gateway_Interface "wikipedia:Common Gateway Interface") (CGI) scripts work with Hiawatha out of box, you just need to enable the CGI module.

 `/etc/hiawatha/hiawatha.conf` 
```
VirtualHost {
    ...
    ExecuteCGI = yes
}
```

Make sure your chosen programming language interpreter is installed. (i.e. for python you would install [python](https://www.archlinux.org/packages/?name=python))

For further details see the official [HowTo](https://www.hiawatha-webserver.org/howto/cgi_and_fastcgi).

### FastCGI

Install [fcgi](https://www.archlinux.org/packages/?name=fcgi). Now you have Hiawatha with fcgi support.

**Note:** There are two kinds of FastCGI applications:

*   The first one runs as a daemon and listens to a port for incoming connections from a webserver.
*   The second one is started by the webserver and communicates with the webserver via pipes.

Hiawatha only supports the first kind!

#### PHP

Install [php](https://www.archlinux.org/packages/?name=php), [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) and [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) (see also [PHP](/index.php/PHP "PHP") and [LAMP](/index.php/LAMP "LAMP")). Do not forget to [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `php-fpm.service`.

Check that php-cgi is working `php-cgi --version`

```
PHP 7.0.2 (cgi-fcgi) (built: Jan  6 2016 11:51:03)
Copyright (c) 1997-2015 The PHP Group
Zend Engine v3.0.0, Copyright (c) 1998-2015 Zend Technologies

```

If you get a similar output then php is installed correctly.

Add one of this `FastCGIserver` sections to your config file.

 `/etc/hiawatha/hiawatha.conf` 
```
### The following fast CGI daemon requires php-fpm using a UNIX socket and TCP port, respectively.
# ACTIVATE a FastCGI server for php  (using UNIX socket)
FastCGIserver {
    FastCGIid = PHP7
    ConnectTo = /run/php-fpm/php-fpm.sock
    Extension = php
    SessionTimeout = 30
}

```
 `/etc/hiawatha/hiawatha.conf` 
```
### The following fast CGI daemon requires php-fpm using a UNIX socket and TCP port, respectively.
# ACTIVATE a FastCGI server for php (using IP-address and TCP port)
FastCGIserver {
    FastCGIid = PHP5
    ConnectTo = 127.0.0.1:9000
    Extension = php
    SessionTimeout = 30
}

```

To use the FastCGIserver ad the following to your config file

 `/etc/hiawatha/hiawatha.conf` 
```
VirtualHost {
    ...
    UseFastCGI = PHP7
}
```

Then [Reload](/index.php/Reload "Reload") the `hiawatha.service`.

#### Ruby on Rails

For some details see the FastCGI section of the [HowTo](https://www.hiawatha-webserver.org/howto/cgi_and_fastcgi).

#### Python FastCGI

For some details see the FastCGI section of the [HowTo](https://www.hiawatha-webserver.org/howto/cgi_and_fastcgi).

### SSL

For SSL/TLS support add the following `Binding` to your con fig file. Then [Reload](/index.php/Reload "Reload") the `hiawatha.service`.

 `/etc/hiawatha/hiawatha.conf` 
```
Binding {
    Port = 443
    TLScertFile = /etc/hiawatha/serverkey.pem
}

```

The order of the items in `serverkey.pem` is important. The order has to be as follows:

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

#### Let's Encrypt

If you want to use Let's Encrypt with Hiawatha follow [Let’s_Encrypt](/index.php/Let%E2%80%99s_Encrypt "Let’s Encrypt") (the manual way is recommended). Read Let's Encrypt [Getting Started](https://letsencrypt.org/getting-started/) for detailed instructions. Afterwards, create a Hiawatha certificate bundle:

```
# cd /etc/letsencrypt/live/domain.tld/
# cat privkey.pem cert.pem chain.pem > /etc/hiawatha/certs/domain.tld/hiawatha.pem

```

and secure it:

```
# chmod 400 /etc/hiawatha/certs/domain.tld/hiawatha.pem

```

Change your Hiawatha TLScertFile paths accordingly in hiawatha.conf:

```
   Binding {                                                      
      ...                                                         
      RequireTLS = yes                                           
      TLScertFile = /etc/hiawatha/certs/domain.tld/hiawatha.pem 
      ...                                                         
   }                                                              

   VirtualHost {                                                  
       ...                                                        
       RequireTLS = yes                                           
       TLScertFile = /etc/hiawatha/certs/domain.tld/hiawatha.pem
       ...                                                        
   }                                                              

```

Then restart Hiawatha:

```
   # systemctl restart hiawatha.service

```

For see this [forum post](https://www.hiawatha-webserver.org/forum/topic/2085).

For further details see the official [HowTo](https://www.hiawatha-webserver.org/howto/bindings).

#### Server Name Indication

Hiawatha has support for SNI, which allows you to serve multiple TLS websites via one IP address. Just configure a TLS binding as explained above. For each virtual host that has its own SSL/TLS certificate, simply use the `TLScertFile` option inside the virtual host block. The certificate specified via Binding{} is used when a website is requested for which no virtual host has been defined.

 `/etc/hiawatha/hiawatha.conf` 
```
VirtualHost {
    Hostname = www.website.org
    ...
    TLScertFile = website.pem
}

```

### Output Compression

Hiawatha has no support for on-the-fly GZip content encoding! But Hiawatha goes its own way with preziped contend.

For further details see the official [FAQ](https://www.hiawatha-webserver.org/faq).

## See also

*   [Hiawatha Support page](https://www.hiawatha-webserver.org/support)