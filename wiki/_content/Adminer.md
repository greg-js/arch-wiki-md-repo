# Adminer

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[Adminer](http://www.adminer.org/) is a simple tool for database management. It's possible to manage [MySQL](/index.php/MySQL "MySQL"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), [Sqlite3](/index.php/Sqlite3 "Sqlite3"), MS SQL and [Oracle](/index.php/Oracle "Oracle"). It's a simpler alternative to [PhpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin"). You can find more pieces of information about this project at [official page](http://www.adminer.org/en/) or [Wikipedia](https://en.wikipedia.org/wiki/Adminer "wikipedia:Adminer").

## Installation

Ensure you do not have an older copy of Adminer:

```
$ rm -r /srv/http/adminer

```

[Install](/index.php/Pacman "Pacman") [adminer](https://aur.archlinux.org/packages/adminer/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR") and add the following line to `/etc/httpd/conf/httpd.conf`:

## Configuration under Apache

```
Include conf/extra/httpd-adminer.conf

```

Then [restart](/index.php/Restart "Restart") your [apache](/index.php/Apache "Apache") daemon.

```
# systemctl restart httpd

```

**Note:** The Adminer can be accessed by your browser on [http://localhost/adminer](http://localhost/adminer).

In case there is an (403) error, change the following lines inside the `/etc/httpd/conf/extra/httpd-adminer.conf` file:

```
Alias /adminer "/usr/share/webapps/adminer"
<Directory "/usr/share/webapps/adminer">
     AllowOverride All
     Require all granted
     #php_admin_value open_basedir "/srv/:/tmp/:/usr/share/webapps/:/etc/webapps:/usr/share/pear/"
</Directory>

```

Restart the [restart](/index.php/Restart "Restart") [apache](/index.php/Apache "Apache") daemon again.

```
# systemctl restart httpd

```

## See also

*   [Official Adminer webpage](http://www.adminer.org/en/)
*   [Author's weblog](http://php.vrana.cz/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Adminer&oldid=407001](https://wiki.archlinux.org/index.php?title=Adminer&oldid=407001)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")