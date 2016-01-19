# Hiawatha

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

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
        *   [2.4.1 Server Name Indication](#Server_Name_Indication)
    *   [2.5 Output Compression](#Output_Compression)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [hiawatha](https://www.archlinux.org/packages/?name=hiawatha) package.

## Configuration

### Basic Setup

The Hiawatha configuration file is: `/etc/hiawatha/hiawatha.conf` By default it should produce a 404 page.

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

Install [php](https://www.archlinux.org/packages/?name=php), [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) and [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) (see also [PHP](/index.php/PHP "PHP") and [LAMP](/index.php/LAMP "LAMP")). Don't forget to [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `php-fpm.service`.

Check that php-cgi is working `php-cgi --version`

```
PHP 7.0.2 (cgi-fcgi) (built: Jan  6 2016 11:51:03)
Copyright (c) 1997-2015 The PHP Group
Zend Engine v3.0.0, Copyright (c) 1998-2015 Zend Technologies

```

If you get a similar output then php is installed correctly.

Add one this FastCGIserver sections to your con fig file.

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

To use the FastCGIserver ad the following to your con fig file

 `/etc/hiawatha/hiawatha.conf` 

```
VirtualHost {
    ...
    UseFastCGI = PHP7
}
```

The [Reload](/index.php/Reload "Reload") the `hiawatha.service`.

#### Ruby on Rails

**Note:** If you use it please fill this section!

For some details see the FastCGI section of the [HowTo](https://www.hiawatha-webserver.org/howto/cgi_and_fastcgi).

#### Python FastCGI

**Note:** If you use it please fill this section!

For some details see the FastCGI section of the [HowTo](https://www.hiawatha-webserver.org/howto/cgi_and_fastcgi).

### SSL

**Note:** Coming soon ...

For further details see the official [HowTo](https://www.hiawatha-webserver.org/howto/bindings).

##### Server Name Indication

**Note:** Coming soon ...

### Output Compression

Output Compression is not supported!

For further details see the official [FAQ](https://www.hiawatha-webserver.org/faq).

## See also

*   [Hiawatha Support page](https://www.hiawatha-webserver.org/support)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Hiawatha&oldid=416076](https://wiki.archlinux.org/index.php?title=Hiawatha&oldid=416076)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")