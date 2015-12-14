# WTorrent

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** The project homepage and the SF page too time out on 6.4.14\. Similar was noted in [wtorrent-svn](https://aur.archlinux.org/packages/wtorrent-svn/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/wtorrent-svn)]</sup> comments two weeks ago. Is the project still existant? (Discuss in [Talk:WTorrent#](https://wiki.archlinux.org/index.php/Talk:WTorrent))

**[wTorrent](http://www.wtorrent-project.org/)** is a web interface to rTorrent, a high performance console based BitTorrent client. It uses rTorrent's built-in XMLRPC server to communicate with it.

wTorrent is programmed in PHP using Smarty templates and XMLRPC for PHP library. wTorrent also uses javascript for rendering the page with AJAX, Scriptaculous and ShadedBorders.

## Contents

*   [1 wTorrent with Apache](#wTorrent_with_Apache)
    *   [1.1 Installation](#Installation)
    *   [1.2 Configuration](#Configuration)
        *   [1.2.1 Adding mod_scgi to httpd.conf](#Adding_mod_scgi_to_httpd.conf)
        *   [1.2.2 Enabling SQLite in php.ini](#Enabling_SQLite_in_php.ini)
        *   [1.2.3 Final steps](#Final_steps)
*   [2 wTorrent with lighttpd](#wTorrent_with_lighttpd)
    *   [2.1 Installation](#Installation_2)
    *   [2.2 Configuration](#Configuration_2)
*   [3 FAQ](#FAQ)
    *   [3.1 Why, when I turn to http://localhost/wtorrent/install.php, it returns not the wTorrent setup page but a plain text page?](#Why.2C_when_I_turn_to_http:.2F.2Flocalhost.2Fwtorrent.2Finstall.php.2C_it_returns_not_the_wTorrent_setup_page_but_a_plain_text_page.3F)

## wTorrent with Apache

See also [Apache](/index.php/Apache "Apache").

### Installation

[Install](/index.php/Install "Install") [wtorrent-svn](https://aur.archlinux.org/packages/wtorrent-svn/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/wtorrent-svn)]</sup> and its the dependencies: [rtorrent](https://www.archlinux.org/packages/?name=rtorrent), [apache](https://www.archlinux.org/packages/?name=apache), [php](https://www.archlinux.org/packages/?name=php), [php-apache](https://www.archlinux.org/packages/?name=php-apache), [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite), [mod_scgi](https://aur.archlinux.org/packages/mod_scgi/)<sup><small>AUR</small></sup>.

### Configuration

#### Adding mod_scgi to httpd.conf

Edit `/etc/httpd/conf/httpd.conf`.

Locate the `LoadModule` lines and add:

```
LoadModule scgi_module modules/mod_scgi.so

```

Add to the end of the file:

```
SCGIMount /RPC2 127.0.0.1:5000

```

Save the file and quit.

#### Enabling SQLite in php.ini

Edit `/etc/php/php.ini`.

Locate and uncomment the following:

```
extension=pdo.so
extension=pdo_sqlite.so
extension=curl.so
extension=xmlrpc.so
extension=sqlite.so
extension=sqlite3.so

```

PHP

PHP is practically available out of the box now.

*   Add these lines in `/etc/httpd/conf/httpd.conf`:

**Note:** Place them at the end of "LoadModule" list or bottom of the file.

```
LoadModule php5_module modules/libphp5.so
Include conf/extra/php5_module.conf

```

*   Restart the Apache service to make changes take effect.

#### Final steps

Add the following to your `~/.rtorrent.rc`:

```
scgi_port = localhost:5000

```

Get the latest version of wTorrent and install to your web directory:

```
# cd /srv/http
# git clone [https://github.com/wtorrent/wtorrent.git](https://github.com/wtorrent/wtorrent.git)
# mv wtorrent wtorrent.git
# mv wtorrent.git/wtorrent/ .
# rm -rf wtorrent.git/
# chmod -R 777 wtorrent

```

Start rTorrent (most common to open a screen and type `rtorrent`)

Point your browser to [http://localhost/wtorrent/install.php](http://localhost/wtorrent/install.php) and add a username & password. After you click the "Try configuration" and it gives you no errors click the "Save configuration"

## wTorrent with lighttpd

See also [Lighttpd](/index.php/Lighttpd "Lighttpd").

### Installation

Install [rtorrent](https://www.archlinux.org/packages/?name=rtorrent), [lighttpd](https://www.archlinux.org/packages/?name=lighttpd), [php](https://www.archlinux.org/packages/?name=php), [sqlite](https://www.archlinux.org/packages/?name=sqlite).

### Configuration

[https://github.com/wtorrent/wtorrent/wiki/InstallGuide#using-lighttpd](https://github.com/wtorrent/wtorrent/wiki/InstallGuide#using-lighttpd)

## FAQ

### Why, when I turn to [http://localhost/wtorrent/install.php](http://localhost/wtorrent/install.php), it returns not the wTorrent setup page but a plain text page?

You should check whether or not PHP is working on your Apache. Add following lines to `/etc/httpd/conf/httpd.conf`: In LoadModule Section, add:

```
LoadModule php5_module modules/libphp5.so

```

In Supplemental configuration section add:

```
# php5
Include conf/extra/php5_module.conf

```

And make sure that `SCGIMount /RPC2 127.0.0.1:5000` is added after the Supplemental configuration section.

Retrieved from "[https://wiki.archlinux.org/index.php?title=WTorrent&oldid=412209](https://wiki.archlinux.org/index.php?title=WTorrent&oldid=412209)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet applications](/index.php/Category:Internet_applications "Category:Internet applications")