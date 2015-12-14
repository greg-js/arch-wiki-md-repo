# Rtgui

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

rtGui is a web based front end for rTorrent - the Linux command line BitTorrent client. It is written in PHP and uses XML-RPC to communicate with the rTorrent client.

## Contents

*   [1 Set up](#Set_up)
    *   [1.1 Apache configuration](#Apache_configuration)
    *   [1.2 PHP configuration](#PHP_configuration)
    *   [1.3 rTorrent configuration](#rTorrent_configuration)
    *   [1.4 Restart Apache](#Restart_Apache)
    *   [1.5 rtGui installation](#rtGui_installation)

## Set up

First [install](/index.php/Install "Install") dependencies: [rtorrent](https://www.archlinux.org/packages/?name=rtorrent), [apache](https://www.archlinux.org/packages/?name=apache), [php](https://www.archlinux.org/packages/?name=php), [php-apache](https://www.archlinux.org/packages/?name=php-apache) and [mod_scgi](https://aur.archlinux.org/packages/mod_scgi/)<sup><small>AUR</small></sup>.

### Apache configuration

Add mod_scgi module to `/etc/httpd/conf/httpd.conf` in _LoadModule_ section:

```
LoadModule scgi_module modules/mod_scgi.so

```

Append at the end of the file:

```
LoadModule php5_module modules/libphp5.so
Include conf/extra/php5_module.conf
SCGIMount /RPC2 127.0.0.1:5000

```

### PHP configuration

Uncomment these extensions in `/etc/php/php.ini`:

```
extension=sockets.so
extension=xmlrpc.so

```

Change the value of these settings from off to on:

```
allow_url_fopen = On
allow_url_include = On

```

### rTorrent configuration

You need to adjust the `.rtorrent.rc` and add the following line:

```
scgi_port = localhost:5000

```

### Restart Apache

```
# systemctl restart httpd.service

```

### rtGui installation

Download and extract rtgui from source:

```
cd /srv/http/
tar xvzf rtgui-x.x.x.tgz
cd rtgui/
cp config.php.example config.php

```

Modify `config.php` to suit your needs

Retrieved from "[https://wiki.archlinux.org/index.php?title=Rtgui&oldid=412169](https://wiki.archlinux.org/index.php?title=Rtgui&oldid=412169)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet applications](/index.php/Category:Internet_applications "Category:Internet applications")