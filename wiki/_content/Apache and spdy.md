# Apache and spdy

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

**This article or section is being considered for deletion.**

**Reason:** SPDY is deprecated in favour of HTTP/2, which is supported natively by Apache (Discuss in [Talk:Apache and spdy#](https://wiki.archlinux.org/index.php/Talk:Apache_and_spdy))

mod_spdy is a SPDY module for Apache 2.2 that allows your web server to take advantage of SPDY features like stream multiplexing and header compression.

*   [mod_spdy](http://code.google.com/p/mod-spdy/) dev site
*   References: [1](http://blog.chromium.org/2009/11/2x-faster-web.html) [2](http://news.cnet.com/8301-30684_3-10396574-265.html) [3](http://alex.dojotoolkit.org/2009/11/spdy-the-web-only-faster/)

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Configure mod_spdy](#Configure_mod_spdy)
    *   [2.2 Configure SPDY](#Configure_SPDY)
    *   [2.3 Module Directives](#Module_Directives)

## Installation

[Install](/index.php/Install "Install") the [mod_spdy](https://aur.archlinux.org/packages/mod_spdy/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/mod_spdy)]</sup> package.

## Configuration

### Configure mod_spdy

In `/etc/httpd/conf/httpd.conf` comment lines

```
#LoadModule ssl_module modules/mod_ssl.so

#Include conf/extra/httpd-ssl.conf

```

In `/etc/httpd/conf/httpd.conf` add Include

```
Include conf/extra/spdy.conf

```

Create self-signed certificate:

```
# cd /etc/httpd/conf
# openssl req -new -x509 -nodes -newkey rsa:4096 -keyout server.key -out server.crt

```

Restart apache

```
# systemctl restart httpd

```

### Configure SPDY

In `/etc/httpd/conf/extra/spdy.conf`

### Module Directives

```
SpdyEnabled - Enable SPDY support
SpdyMaxStreamsPerConnection - Maxiumum number of simultaneous SPDY streams per connection
SpdyMinThreadsPerProcess - Miniumum number of worker threads to spawn per child process
SpdyMaxThreadsPerProcess - Maxiumum number of worker threads to spawn per child process
SpdyDebugLoggingVerbosity - Set the verbosity of mod_spdy logging
SpdyDebugUseSpdyForNonSslConnections - Use SPDY even over non-SSL connections; DO NOT USE IN PRODUCTION

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Apache_and_spdy&oldid=413075](https://wiki.archlinux.org/index.php?title=Apache_and_spdy&oldid=413075)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")