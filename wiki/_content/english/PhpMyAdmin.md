[phpMyAdmin](http://www.phpmyadmin.net/) is a web-based tool to help manage MySQL databases using an Apache/PHP frontend.

## Contents

*   [1 Installation](#Installation)
*   [2 Running](#Running)
    *   [2.1 PHP](#PHP)
    *   [2.2 Apache](#Apache)
    *   [2.3 Lighttpd](#Lighttpd)
    *   [2.4 Nginx](#Nginx)
*   [3 Configuration](#Configuration)
    *   [3.1 Using setup script](#Using_setup_script)
    *   [3.2 Add blowfish_secret passphrase](#Add_blowfish_secret_passphrase)
    *   [3.3 Enabling Configuration Storage](#Enabling_Configuration_Storage)
        *   [3.3.1 Setup database](#Setup_database)
        *   [3.3.2 Setup database user](#Setup_database_user)
    *   [3.4 Enabling templates catching](#Enabling_templates_catching)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [phpmyadmin](https://www.archlinux.org/packages/?name=phpmyadmin) package.

## Running

### PHP

Make sure the PHP [mysql](/index.php/PHP#MySQL/MariaDB "PHP") extension(s) have been enabled.

Optionally you can enable `extension=bz2` and `extension=zip` for compression support.

**Note:** If `open_basedir` has been set, make sure to include `/etc/webapps` to `open_basedir` in `/etc/php/php.ini`.

### Apache

Set up Apache to use PHP as outlined in the [Apache HTTP Server#PHP](/index.php/Apache_HTTP_Server#PHP "Apache HTTP Server") article.

Create the Apache configuration file:

 `/etc/httpd/conf/extra/phpmyadmin.conf` 
```
Alias /phpmyadmin "/usr/share/webapps/phpMyAdmin"
<Directory "/usr/share/webapps/phpMyAdmin">
    DirectoryIndex index.php
    AllowOverride All
    Options FollowSymlinks
    Require all granted
</Directory>
```

And include it in `/etc/httpd/conf/httpd.conf`:

```
# phpMyAdmin configuration
Include conf/extra/phpmyadmin.conf

```

**Note:** By default, everyone who can reach the Apache Web Server can see the phpMyAdmin login page under this URL. To change this, edit `/etc/httpd/conf/extra/phpmyadmin.conf` to your liking. For example, if you only want to be able to access it from the same machine, replace `Require all granted` by `Require local`. Beware that this will disallow connecting to PhpMyAdmin on a remote server. If you still want to access PhpMyAdmin on a remote server securely, you might want to consider setting up a [OpenSSH#Encrypted SOCKS tunnel](/index.php/OpenSSH#Encrypted_SOCKS_tunnel "OpenSSH").

After making changes to the Apache configuration file, [restart](/index.php/Restart "Restart") `httpd.service`.

### Lighttpd

Configuring [Lighttpd](/index.php/Lighttpd "Lighttpd"), make sure it is able to serve PHP files and `mod_alias` has been enabled.

Add the following alias for PhpMyAdmin to the config:

```
 alias.url = ( "/phpmyadmin" => "/usr/share/webapps/phpMyAdmin/")

```

### Nginx

Make sure to set up [nginx#FastCGI](/index.php/Nginx#FastCGI "Nginx") and using [server blocks](/index.php/Nginx#Server_blocks "Nginx") to easier management.

By preference; access phpMyAdmin by subdomain, e.g. `[https://pma.domain.tld](https://pma.domain.tld)`:

 `/etc/nginx/sites-available/pma.domain.tld` 
```
server {
    server_name pma.domain.tld;
    ; listen 80; # also listen on http
    ; listen [::]:80;
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    index index.php;
    access_log /var/log/nginx/pma.access.log;
    error_log /var/log/nginx/pma.error.log;

    # Allows limiting access to certain client addresses.
    ; allow 192.168.1.0/24;
    ; allow *my-ip*;
    ; deny all;

    root /usr/share/webapps/phpMyAdmin;
    location / {
        try_files $uri $uri/ =404;
    }

    error_page 404 /index.php;

    location ~ \.php$ {
        try_files $uri $document_root$fastcgi_script_name =404;

        fastcgi_split_path_info ^(.+\.php)(/.*)$;
        fastcgi_pass unix:/run/php-fpm/php-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;

        fastcgi_param HTTP_PROXY "";
        fastcgi_param HTTPS on;
        fastcgi_request_buffering off;
   }
}
```

Or by subdirectory, e.g. `[https://domain.tld/phpMyAdmin](https://domain.tld/phpMyAdmin)`:

 `/etc/nginx/sites-available/domain.tld` 
```
server {
    server_name domain.tld;
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    index index.php;
    access_log /var/log/nginx/domain.tld.access.log;
    error_log /var/log/nginx/domain.tld.error.log;

    root /srv/http/domain.tld;
    location / {
        try_files $uri $uri/ =404;
    }

    location /phpMyAdmin {
        root /usr/share/webapps/phpMyAdmin;
    }

    # Deny static files
    location ~ ^/phpMyAdmin/(README|LICENSE|ChangeLog|DCO)$ {
       deny all;
    }

    # Deny .md files
    location ~ ^/phpMyAdmin/(.+\.md)$ {
      deny all;
   }

   # Deny setup directories
   location ~ ^/phpMyAdmin/(doc|sql|setup)/ {
      deny all;
   }

   #FastCGI config for phpMyAdmin
   location ~ /phpMyAdmin/(.+\.php)$ {
      try_files $uri $document_root$fastcgi_script_name =404;

      fastcgi_split_path_info ^(.+\.php)(/.*)$;
      fastcgi_pass unix:/run/php-fpm/php-fpm.sock;
      fastcgi_index index.php;
      fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
      include fastcgi_params;

      fastcgi_param HTTP_PROXY "";
      fastcgi_param HTTPS on;
      fastcgi_request_buffering off;
   }
}

```

## Configuration

The main configuration file is located at `/etc/webapps/phpmyadmin/config.inc.php`.

If the [MySQL](/index.php/MySQL "MySQL") server is not on localhost, [append](/index.php/Append "Append") the following line:

```
$cfg['Servers'][$i]['host'] = 'localhost';

```

### Using setup script

To allow the usage of the phpMyAdmin setup script (e.g. [http://localhost/phpmyadmin/setup](http://localhost/phpmyadmin/setup)), make sure `/usr/share/webapps/phpMyAdmin` is writable for the `http` [user](/index.php/User "User"):

```
# mkdir /usr/share/webapps/phpMyAdmin/config
# chown http:http /usr/share/webapps/phpMyAdmin/config
# chmod 750 /usr/share/webapps/phpMyAdmin/config

```

### Add blowfish_secret passphrase

It is required to enter an unique 32 characters long string to fully use the blowfish algorithm used by PhpMyAdmin, thus preventing the message *ERROR: The configuration file now needs a secret passphrase (blowfish_secret)*:

 `/etc/webapps/phpmyadmin/config.inc.php`  `$cfg['blowfish_secret'] = '...';` 

### Enabling Configuration Storage

Extra options such as table linking, change tracking, PDF creation, and bookmarking queries are disabled by default, displaying *The phpMyAdmin configuration storage is not completely configured, some extended features have been deactivated.* on the homepage.

**Note:** This example assumes you want to use the default username **pma** as the `controluser`, and **pmapass** as the `controlpass`.

In `/etc/webapps/phpmyadmin/config.inc.php`, uncomment (remove the leading "//"s), and change them to your desired credentials if needed:

 `/etc/webapps/phpmyadmin/config.inc.php` 
```
/* User used to manipulate with storage */
// $cfg['Servers'][$i]['controlhost'] = 'my-host';
// $cfg['Servers'][$i]['controlport'] = '3306';
$cfg['Servers'][$i]['controluser'] = 'pma';
$cfg['Servers'][$i]['controlpass'] = 'pmapass';

/* Storage database and tables */
$cfg['Servers'][$i]['pmadb'] = 'phpmyadmin';
$cfg['Servers'][$i]['bookmarktable'] = 'pma__bookmark';
$cfg['Servers'][$i]['relation'] = 'pma__relation';
$cfg['Servers'][$i]['table_info'] = 'pma__table_info';
$cfg['Servers'][$i]['table_coords'] = 'pma__table_coords';
$cfg['Servers'][$i]['pdf_pages'] = 'pma__pdf_pages';
$cfg['Servers'][$i]['column_info'] = 'pma__column_info';
$cfg['Servers'][$i]['history'] = 'pma__history';
$cfg['Servers'][$i]['table_uiprefs'] = 'pma__table_uiprefs';
$cfg['Servers'][$i]['tracking'] = 'pma__tracking';
$cfg['Servers'][$i]['userconfig'] = 'pma__userconfig';
$cfg['Servers'][$i]['recent'] = 'pma__recent';
$cfg['Servers'][$i]['favorite'] = 'pma__favorite';
$cfg['Servers'][$i]['users'] = 'pma__users';
$cfg['Servers'][$i]['usergroups'] = 'pma__usergroups';
$cfg['Servers'][$i]['navigationhiding'] = 'pma__navigationhiding';
$cfg['Servers'][$i]['savedsearches'] = 'pma__savedsearches';
$cfg['Servers'][$i]['central_columns'] = 'pma__central_columns';
$cfg['Servers'][$i]['designer_settings'] = 'pma__designer_settings';
$cfg['Servers'][$i]['export_templates'] = 'pma__export_templates';
```

##### Setup database

Two options are available to create the required tables:

*   Import `/usr/share/webapps/phpMyAdmin/sql/create_tables.sql` by using PhpMyAdmin.
*   Execute `mysql -u root -p < /usr/share/webapps/phpMyAdmin/sql/create_tables.sql` in the command line.

##### Setup database user

To apply the required permissions for `controluser`, execute the following query:

**Note:** Make sure to replace all instances of `pma` and `pmapass` to the values set in `config.inc.php`. If you are setting this up for a remote database, then you must also change `localhost` to the proper host.

```
GRANT USAGE ON mysql.* TO 'pma'@'localhost' IDENTIFIED BY 'pmapass';
GRANT SELECT (
    Host, User, Select_priv, Insert_priv, Update_priv, Delete_priv,
    Create_priv, Drop_priv, Reload_priv, Shutdown_priv, Process_priv,
    File_priv, Grant_priv, References_priv, Index_priv, Alter_priv,
    Show_db_priv, Super_priv, Create_tmp_table_priv, Lock_tables_priv,
    Execute_priv, Repl_slave_priv, Repl_client_priv
    ) ON mysql.user TO 'pma'@'localhost';
GRANT SELECT ON mysql.db TO 'pma'@'localhost';
GRANT SELECT ON mysql.host TO 'pma'@'localhost';
GRANT SELECT (Host, Db, User, Table_name, Table_priv, Column_priv)
    ON mysql.tables_priv TO 'pma'@'localhost';

```

In order use the bookmark and relation features, set the following permissions:

```
GRANT SELECT, INSERT, UPDATE, DELETE ON phpmyadmin.* TO 'pma'@'localhost';

```

Re-login to ensure the new features are activated.

### Enabling templates catching

Edit `/etc/webapps/phpmyadmin/config.inc.php` to add the line:

```
 $cfg['TempDir'] = '/tmp/phpmyadmin';

```

## See also

*   [Wikipedia](https://en.wikipedia.org/wiki/phpMyAdmin "wikipedia:phpMyAdmin")