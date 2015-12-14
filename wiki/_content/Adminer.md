# Adminer

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[Adminer](http://www.adminer.org/) is a simple tool for database management. It's possible to manage [MySQL](/index.php/MySQL "MySQL"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), [Sqlite3](/index.php/Sqlite3 "Sqlite3"), MS SQL and [Oracle](/index.php/Oracle "Oracle").

It's a simpler alternative to [PhpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin"). You can find more pieces of information about this project at the [official page](http://www.adminer.org/en/) or at [Wikipedia](https://en.wikipedia.org/wiki/Adminer "wikipedia:Adminer").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration under Apache](#Configuration_under_Apache)
*   [3 Configuration under Nginx](#Configuration_under_Nginx)
*   [4 See also](#See_also)

## Installation

Ensure you do not have a manually downloaded copy of Adminer installed!

[Install](/index.php/Install "Install") [adminer](https://aur.archlinux.org/packages/adminer/)<sup><small>AUR</small></sup>.

Adminer will be installed as `/usr/share/webapps/adminer/index.php`.

Don't forget to enable `mysqli.so` in your `/etc/php/php.ini` by uncommenting following line:

```
 extension=mysqli.so

```

**Warning:** As of PHP 5.5, `mysql.so` is [deprecated](http://www.php.net/manual/de/migration55.deprecated.php) and will fill up your log files with error messages. It is no longer available in PHP 7.0.

## Configuration under Apache

Add the following line to `/etc/httpd/conf/httpd.conf`:

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

## Configuration under Nginx

Ensure that the [php FastCGI interface](/index.php/Nginx#PHP_configuration "Nginx") is configured correct.

Then ad the folwing `server` block to your `/etc/nginx/nginx.conf` or place it in a file under `/etc/nginx/servers-available/` and [enable](/index.php/Nginx#Managing_server_entries "Nginx") it.

Afterwards restart the server with `systemctl restart nginx.service`.

 `/etc/nginx/nginx.conf` 

```
server {
        listen 80;
        server_name db.domainname.dom;
        root /usr/share/webapps/adminer;

        # If you want to use a .htpass file, uncomment the three following lines.
        #auth_basic "Admin-Area! Password needed!";
        #auth_basic_user_file /usr/share/webapps/adminer/.htpass;
        #access_log /var/log/nginx/adminer-access.log;

        error_log /var/log/nginx/adminer-error.log;
        location / {
                index index.php;
                try_files $uri $uri/ /index.php?$args;
                }

location ~ .php$ {
        include fastcgi.conf;
        #fastcgi_pass localhost:9000;
        fastcgi_pass unix:/run/php-fpm/php-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME /usr/share/webapps/adminer$fastcgi_script_name;
        }
}

```

## See also

*   [Official Adminer webpage](http://www.adminer.org/en/)
*   [Author's weblog](http://php.vrana.cz/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Adminer&oldid=412265](https://wiki.archlinux.org/index.php?title=Adminer&oldid=412265)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")