# Dokuwiki

"DokuWiki is a standards-compliant, simple-to-use wiki which allows users to create rich documentation repositories. It provides an environment for individuals, teams and companies to create and collaborate using a simple yet powerful syntax that ensures data files remain structured and readable outside the wiki."

"Unlimited page revisions allows restoration to any earlier page version, and with data stored in plain text files, no database is required. A powerful plugin architecture allows for extension and enhancement of the core system. See the features section for a full description of what DokuWiki has to offer."[[1]](http://wiki.splitbrain.org/wiki:dokuwiki)

In other words, DokuWiki is a wiki written in PHP and requires no database.

[Like to see a running example?](http://www.dokuwiki.org/)

## Contents

*   [1 Initial Notes](#Initial_Notes)
*   [2 Installation](#Installation)
*   [3 Configuration](#Configuration)
    *   [3.1 Apache](#Apache)
    *   [3.2 lighttpd Specific Configuration](#lighttpd_Specific_Configuration)
    *   [3.3 nginx](#nginx)
*   [4 Post Installation](#Post_Installation)
    *   [4.1 Cleaning Up](#Cleaning_Up)
    *   [4.2 Installing Plugins](#Installing_Plugins)
    *   [4.3 Backing Up](#Backing_Up)
*   [5 Further Reading](#Further_Reading)

## Initial Notes

DokuWiki should work on any web server which supports PHP 5.1.2 or later. As the requirements may change over time, you should consult the [requirements page](http://www.dokuwiki.org/requirements) for DokuWiki for additional details.

It is strongly recommend to read through the appropriate sections of [DokuWiki's security page](http://www.dokuwiki.org/security) for your web server. Most popular web servers are covered but there are generic instructions as well.

The package in [community] unpacks DokuWiki at `/usr/share/webapps/dokuwiki` with the configuration files in `/etc/webapps/dokuwiki` and the data files in `/var/lib/dokuwiki/data`. It also changes the ownership of the relevant files to the "http" user. This should work fine for most popular web servers as packaged for Arch.

## Installation

1.  Install your web server of choice (e.g. [Apache](/index.php/Apache "Apache"), [nginx](/index.php/Nginx "Nginx") or [lighttpd](/index.php/Lighttpd "Lighttpd")) and configure it for [PHP](/index.php/PHP "PHP"). As mentioned above, DokuWiki has no need for a database server so you may be able to skip those steps when setting up your web server.
2.  Install [dokuwiki](https://www.archlinux.org/packages/?name=dokuwiki) from [community] with [pacman](/index.php/Pacman "Pacman").
3.  Configure web server for dokuwiki (see section below)
4.  With your web browser of choice, open http://<your-server>/dokuwiki/install.php and continue the installation from there.

Alternatively, if you would like to install from tarball, you can read from [http://www.dokuwiki.org/Install](http://www.dokuwiki.org/Install). Generally the procedure is the same as above. Instead of using pacman, you will need to [download the tarball](http://www.splitbrain.org/projects/dokuwiki), unpack it to your server's document root (e.g. `/srv/http/dokuwiki`), and chown to the appropriate user (e.g. "http").

## Configuration

If you are using [lighttpd](/index.php/Lighttpd "Lighttpd") or [nginx](/index.php/Nginx "Nginx") you need to adjust the `open_basedir` in `/etc/php/php.ini` to include the dokuwiki directories (php forbids following symbolic links outside of the allowed scope):

 `/etc/php/php.ini` 

```
open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/:/etc/webapps/dokuwiki/:/var/lib/dokuwiki/

```

Also uncomment the following line.

 `/etc/php/php.ini` 

```
extension=gd.so

```

Dokuwiki needs this library for resizing images.

### Apache

The package should add the file `/etc/httpd/conf/extra/dokuwiki.conf` with the following contents:

```
Alias /dokuwiki /usr/share/webapps/dokuwiki
<Directory /usr/share/webapps/dokuwiki/>
    Options +FollowSymLinks
    AllowOverride All
    order allow,deny
    allow from all
    php_admin_value open_basedir "/tmp/:/usr/share/pear/:/usr/share/webapps/:/etc/webapps/dokuwiki/:/var/lib/dokuwiki/"
</Directory>

```

If you are running [Apache 2.4 or newer](https://httpd.apache.org/docs/2.4/upgrading.html), you will have to change the following lines:

```
    order allow,deny
    allow from all

```

to read:

```
    Require all granted

```

Include the newly created file in the Apache configuration by placing the following line at the end of `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/dokuwiki.conf

```

Make sure the folders `/etc/webapps/dokuwiki` and `/var/lib/dokuwiki` are owned by user and group "http". You may relocate these directories if you like as long as you update the references in `/etc/httpd/conf/extra/dokuwiki.conf` respectively.

Afterwards restart Apache:

```
 # systemctl restart httpd.service

```

Then finish the installation by running the _dokuwiki/install.php_ script in your browser.

### lighttpd Specific Configuration

Edit the `/etc/lighttpd/lighttpd.conf` file as per the [dokuwiki instructions](http://www.dokuwiki.org/install:lighttpd) (might contain updated information).

Make sure the modules `mod_access` and `mod_alias` are loaded. If not, load them by adding the following to `/etc/lighttpd/lighttpd.conf`:

```
server.modules += ("mod_access")
server.modules += ("mod_alias")
```

`mod_access` provides the `url.access-deny` command, which we are using from this point.

Under the line:

```
$HTTP["url"] =~ "\.pdf$" {
  server.range-requests = "disable"
}
```

add this:

```
# subdir of dokuwiki
# comprised of the subdir of the root dir where dokuwiki is installed
# in this case the root dir is the basedir plus /htdocs/
# Note: be careful with trailing slashes when uniting strings.
# all content on this example server is served from htdocs/ up.
#var.dokudir = var.basedir + "/dokuwiki"
var.dokudir = server.document-root + "/dokuwiki"

# make sure those are always served through fastcgi and never as static files
# deny access completly to these
$HTTP["url"] =~ "/(\.|_)ht" { url.access-deny = ( "" ) }
$HTTP["url"] =~ "^" + var.dokudir + "/(bin|data|inc|conf)/"  { url.access-deny = ( "" ) }
```

_These entries give some basic security to DokuWiki._ lighttpd does not use .htaccess files like Apache. You CAN install with out this, but I would NEVER recommend it.

Add alias somewhere in lighttpd or fastcgi conf file:

 `alias.url += ("/dokuwiki" => "/usr/share/webapps/dokuwiki/")` 

Restart lighttpd:

```
 # systemctl restart lighttpd

```

### nginx

Add the following location blocks to your `/etc/nginx/nginx.conf`.

```
#Assuming that the root is set to /usr/share/webapps.
#You may need to adjust your location blocks accordingly.
location ~^/dokuwiki/(data|conf|bin|inc)/ { deny all; } # secure DokuWiki
location ~^/dokuwiki/\.ht { deny all; } # also secure the Apache .htaccess files
location ~^/dokuwiki/lib/^((?!php).)*$ { expires 30d; } # no need to serve non .php files through fastcgi, so we catch those requests here.
location ~^/dokuwiki/.*\.php$ {
            include fastcgi.conf;
            fastcgi_pass unix:/run/php-fpm/php-fpm.sock;
        }

```

Restart nginx

```
 # systemctl restart nginx

```

## Post Installation

### Cleaning Up

**After configuring the server remove the install.php file!**

```
 # rm /srv/http/dokuwiki/install.php

```

### Installing Plugins

Many community created plugins can be found [here](http://www.dokuwiki.org/plugins)

They can be added through the web interface (as well as updated) through the Admin menu. Some plugins cannot be downloaded, if they go over ssl (e.g. git).

### Backing Up

It is very trivial to backup DokuWiki, since there is no database. All pages are in plain text, and require only a simple tar, or rsync.

A quick breakdown of the directories of interest in the current (2008-05-05) version:

```
 /dokuwiki/data/  =>  All User Created Data
 /dokuwiki/lib/plugins/  =>  All User Added Plugins

```

## Further Reading

The [DokuWiki main site](http://www.dokuwiki.org/) has all of the information and help that you could possibly need.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dokuwiki&oldid=414212](https://wiki.archlinux.org/index.php?title=Dokuwiki&oldid=414212)"