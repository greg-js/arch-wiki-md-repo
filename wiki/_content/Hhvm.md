# Hhvm

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** This document is a stub, please help to extend it. (Discuss in [Talk:Hhvm#](https://wiki.archlinux.org/index.php/Talk:Hhvm))

HHVM, as authors declare, is an open-source virtual machine designed for executing programs written in Hack and PHP. HHVM uses a just-in-time (JIT) compilation approach to achieve superior performance while maintaining the development flexibility that PHP provides.

HHVM runs much of the world’s existing PHP. Developers and hosts are adopting HHVM. We are aware of minor incompatibilities (please open issues when you find them), but we can run the top 20 Github PHP frameworks out of the box. The HHVM team, along with many wonderful community members, has made it a stated, high priority goal to run all existing PHP code existing out in the wild.

## Contents

*   [1 Installation](#Installation)
*   [2 Running](#Running)
*   [3 Making it work with a web server](#Making_it_work_with_a_web_server)
    *   [3.1 Nginx](#Nginx)
    *   [3.2 Lighttpd](#Lighttpd)

## Installation

[Install](/index.php/Install "Install") package [hhvm](https://www.archlinux.org/packages/?name=hhvm) in the [official repositories](/index.php/Official_repositories "Official repositories").

## Running

To enable the HHVM service by default at start-up, run:

```
# systemctl enable hhvm

```

To start the HHVM service, run:

```
# systemctl start hhvm

```

With default configuration, HHVM serves fastcgi at localhost port 9000.

## Making it work with a web server

### Nginx

Edit `/etc/nginx/nginx.conf` to serve `.php` files through HHVM via fastcgi:

 `/etc/nginx/nginx.conf` 

```
..
location ~ \.php$ {
   fastcgi_pass   127.0.0.1:9000;
   fastcgi_index  index.php;
   include        fastcgi.conf;
}
..

```

### Lighttpd

 `/etc/lighttpd/lighttpd.conf` 

```
..
fastcgi.server = (
  ".php" => (
     "localhost" => (
       "host" => "127.0.0.1",
       "port" => "9000",
       "broken-scriptfilename" => "enable",
    )
  )
)
..

```

Restart `lighttpd.service` to apply any changes.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Hhvm&oldid=412097](https://wiki.archlinux.org/index.php?title=Hhvm&oldid=412097)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Programming languages](/index.php/Category:Programming_languages "Category:Programming languages")