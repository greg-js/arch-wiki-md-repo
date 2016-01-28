# Sonerezh

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Don't show simple commands like cp or even how to reload systemctl. Instead write out the instructions in those cases and link to the relevant pages. (Discuss in [Talk:Sonerezh#](https://wiki.archlinux.org/index.php/Talk:Sonerezh))

[Sonerezh](https://www.sonerezh.bzh) is a self-hosted, web-based application for stream your music, everywhere.

## Installation

Install [sonerezh-git](https://aur.archlinux.org/packages/sonerezh-git/)<sup><small>AUR</small></sup>. Further you will need a database (e.g. [MariaDB](/index.php/MariaDB "MariaDB")), a web server (like [Nginx](/index.php/Nginx "Nginx")) with php-support. You may refer following sites:

*   [Apache](/index.php/Apache "Apache")
*   [Lighttpd](/index.php/Lighttpd "Lighttpd")
*   [Nginx](/index.php/Nginx "Nginx")

## Configuration

Make sure to adjust following variables to these minimal values in your `php.ini`:

 `/etc/php/php.ini` 

```
extension=gd.so

date.timezone = UTC
```

In this configuration, we will configure the [Nginx](/index.php/Nginx "Nginx") web server to serve Sonerezh on localhost in the root location without SSL enabled (even tough it's recommended to use it with SSL). First, place a copy of the Sonerezh Nginx configuration

```
cp /usr/share/doc/sonerezh/example_nginx_vhost.conf /etc/webapps/sonerezh/nginx.conf

```

replace the domain name

```
sed -i 's/pydio.example.com/localhost/g' /etc/webapps/pydio/nginx.conf

```

and reference this configuration file in the main nginx.conf:

 `/etc/nginx/nginx.conf` 

```

http {
    [...]
    include /etc/webapps/sonerezh/nginx.conf;
    [...]
 }

```

Here's an example on how you could setup a database for Sonerezh with [MariaDB](/index.php/MariaDB "MariaDB") called `sonerezh` for the user `sonerezh` identified by the password `sonerezh`:

```
CREATE DATABASE pydio;
GRANT ALL PRIVILEGES ON sonerezh.* TO sonerezh@'localhost' IDENTIFIED BY 'sonerezh';
FLUSH PRIVILEGES;

```

Do not forget to (re)start your services!

```
systemctl restart nginx php-fpm

```

Visit the installation wizard page at [http://sonerezh.localhost/install](http://sonerezh.localhost/install) and follow the instructions.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sonerezh&oldid=404049](https://wiki.archlinux.org/index.php?title=Sonerezh&oldid=404049)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet applications](/index.php/Category:Internet_applications "Category:Internet applications")

Hidden category:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")