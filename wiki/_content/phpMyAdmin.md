# phpMyAdmin

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[phpMyAdmin](http://www.phpmyadmin.net/) is a web-based tool to help manage MySQL databases using an Apache/PHP frontend. It requires a working [LAMP](/index.php/LAMP "LAMP") setup.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 PHP](#PHP)
    *   [2.2 Apache](#Apache)
    *   [2.3 Lighttpd](#Lighttpd)
    *   [2.4 Nginx](#Nginx)
        *   [2.4.1 Option 1: subdomain](#Option_1:_subdomain)
        *   [2.4.2 Option 2: subdirectory](#Option_2:_subdirectory)
*   [3 phpMyAdmin configuration](#phpMyAdmin_configuration)
    *   [3.1 Add blowfish_secret passphrase](#Add_blowfish_secret_passphrase)
    *   [3.2 Enabling Configuration Storage (optional)](#Enabling_Configuration_Storage_.28optional.29)
        *   [3.2.1 creating phpMyAdmin database](#creating_phpMyAdmin_database)
        *   [3.2.2 creating phpMyAdmin database user](#creating_phpMyAdmin_database_user)
*   [4 Accessing your phpMyAdmin installation](#Accessing_your_phpMyAdmin_installation)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Fixing open_basedir warning](#Fixing_open_basedir_warning)
    *   [5.2 #2006 - MySQL server has gone away](#.232006_-_MySQL_server_has_gone_away)

## Installation

Install the [phpmyadmin](https://www.archlinux.org/packages/?name=phpmyadmin) and [php-mcrypt](https://www.archlinux.org/packages/?name=php-mcrypt) packages from the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

### PHP

You need to enable the `mysqli` and `mcrypt` (if you want phpMyAdmin internal authentication) extensions in PHP by editing `/etc/php/php.ini` and uncommenting the following lines:

```
extension=mysqli.so
extension=mcrypt.so

```

Optionally you can enable `bz2.so` and `zip.so` for compression support.

You need to make sure that PHP can access `/etc/webapps`. Add it to `open_basedir` in `/etc/php/php.ini` if necessary:

```
open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/:/etc/webapps/

```

You also need to edit the config file (`/usr/share/webapps/phpmyadmin/config.inc.php`) to add the blowfish secret. You can use [this page](https://www.question-defense.com/tools/phpmyadmin-blowfish-secret-generator) to get one generated for you.

### Apache

**Note:** The following works (at least no obvious problems) with Apache 2.4 and php-apache/mod_mpm_prefork or php-fpm/mod_proxy_handler

Set up Apache to use php as outlined in the [LAMP](/index.php/LAMP#PHP "LAMP") article.

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

**Note:** By default, everyone who can reach the Apache Web Server can see the phpMyAdmin login page under this URL. To change this, edit `/etc/httpd/conf/extra/phpmyadmin.conf` to your liking. For example, if you only want to be able to access it from the same machine, replace `Require all granted` by `Require local`. Beware that this will disallow connecting to PhpMyAdmin on a remote server.

### Lighttpd

Configuring Lighttpd is similar to Apache. Make sure Lighttpd is setup to serve PHP files (see [Lighttpd](/index.php/Lighttpd "Lighttpd")).

Make an alias for phpmyadmin in your Lighttpd config.

```
 alias.url = ( "/phpmyadmin" => "/usr/share/webapps/phpMyAdmin/")

```

Then enable mod_alias, mod_fastcgi and mod_cgi in your config ( server.modules section )

Restart Lighttpd and go to [[1]](http://localhost/phpmyadmin/).

### Nginx

#### Option 1: subdomain

Using this method, you'll access PhpMyAdmin as `phpmyadmin.<domain>`.

Configurating Nginx is similar to Apache (and Lighttpd, for that matter). Make sure Nginx is setup to serve PHP files (see [Nginx](/index.php/Nginx "Nginx")).

You can setup a sub domain (or domain) with a server block like so (if using php-fpm):

```
 server {
         server_name     phpmyadmin.<domain.tld>;

         root    /usr/share/webapps/phpMyAdmin;
         index   index.php;

         location ~ \.php$ {
                 try_files      $uri =404;
                 fastcgi_pass   unix:/run/php-fpm/php-fpm.sock;
                 fastcgi_index  index.php;
                 include        fastcgi.conf;
         }
 }

```

To access this url on your localhost, you can simply add an entry in /etc/hosts:

```
 127.0.0.1	phpmyadmin.<domain.tld>

```

You need to update PHP's open_basedir option to add the appropriate directories. Either in /etc/php/php.ini:

```
 open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/:/etc/webapps/

```

Or if running php-fpm with a separate entry for phpmyadmin, you can overwrite this value in your pool definition (in /etc/php/fpm.d/<pool file>):

```
 php_admin_value[open_basedir] = /tmp/:/usr/share/webapps/:/etc/webapps/

```

If the above doesn't fix it try adding the following to your NGINX Configuration below the other fastcgi_param (I think its something to do with the Suhosin-Patch)

```
 fastcgi_param  PHP_ADMIN_VALUE  open_basedir="/srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/:/etc/webapps/";

```

While you can enter anything for the blowfish password, you may want to choose a randomly generated string of characters (most likely for security reasons). Here's a handy tool that will do that for you on the web[[2]](http://www.question-defense.com/tools/phpmyadmin-blowfish-secret-generator).

When using SSL, you might run into the problem that the links on the pages generated by phpMyAdmin incorrectly start with "http" instead of "https" which may cause errors. To fix this, you can add the following fcgi_param to your SSL-enabled server section (in addition to your usual fastcgi params):

```
 fastcgi_param HTTPS on;

```

#### Option 2: subdirectory

Using this method, you'll access PhpMyAdmin as `localhost/phpmyadmin`, similarly to Apache.

To get PhpMyAdmin working with your [nginx](/index.php/Nginx "Nginx") setup, first take note of the root of the server you want to use. Supposing it is `/srv/http`, now create a symlink:

```
 # ln -s /usr/share/webapps/phpMyAdmin/ /srv/http/phpmyadmin

```

## phpMyAdmin configuration

phpMyAdmin's configuration file is located at `/etc/webapps/phpmyadmin/config.inc.php`. If you have a local MySQL server, it should be usable without making any modifications.

If your MySQL server is not on the localhost, uncomment and edit the following line:

```
$cfg['Servers'][$i]['host'] = 'localhost';

```

If you would like to use phpMyAdmin setup script by calling [http://localhost/phpmyadmin/setup](http://localhost/phpmyadmin/setup) you will need to create a config directory that's writeable by the _httpd_ user in `/usr/share/webapps/phpMyAdmin` as follows:

```
# cd /usr/share/webapps/phpMyAdmin
# mkdir config
# chgrp http config
# chmod g+w config

```

### Add blowfish_secret passphrase

If you see the following error message at the bottom of the page when you first log in to /phpmyadmin (using a previously setup MySQL username and password) :

```
ERROR: The configuration file now needs a secret passphrase (blowfish_secret)

```

You need to add a blowfish password to the phpMyAdmin's config file. Edit `/etc/webapps/phpmyadmin/config.inc.php` and insert a random blowfish "password" in the line

```
$cfg['blowfish_secret'] = _; /* YOU MUST FILL IN THIS FOR COOKIE AUTH! */_

```

Go [here](http://www.question-defense.com/tools/phpmyadmin-blowfish-secret-generator) to get a nicely generated blowfish_secret and paste it between the _marks. It should now look something like this:_

```
$cfg['blowfish_secret'] = 'qtdRoGmbc9{8IZr323xYcSN]0s)r$9b_JUnb{~Xz'; /* YOU MUST FILL IN THIS FOR COOKIE AUTH! */

```

The error should go away if you refresh the phpmyadmin page.

### Enabling Configuration Storage (optional)

Now that the basic database server has been setup, it _is_ functional, however by default, extra options such as table linking, change tracking, PDF creation, and bookmarking queries are disabled. You will see a message at the bottom of the main phpMyAdmin page, "The phpMyAdmin configuration storage is not completely configured, some extended features have been deactivated. To find out why...", This section addresses how to to enable these extra features.

**Note:** This example assumes you want to use the username **pma** as the controluser, and **pmapass** as the controlpass. These should be changed (the _very_ least, you should change the password!) to something more secure.

In `/etc/webapps/phpmyadmin/config.inc.php`, uncomment (remove the leading "//"s on) these two lines, and change them to your desired credentials:

```
// $cfg['Servers'][$i]['controluser'] = 'pma';
// $cfg['Servers'][$i]['controlpass'] = 'pmapass';
```

You will need this information later, so keep it in mind.

Beneath the controluser setup section, uncomment these lines:

```
/* Storage database and tables */
// $cfg['Servers'][$i]['pmadb'] = 'phpmyadmin';
// $cfg['Servers'][$i]['bookmarktable'] = 'pma__bookmark';
// $cfg['Servers'][$i]['relation'] = 'pma__relation';
// $cfg['Servers'][$i]['table_info'] = 'pma__table_info';
// $cfg['Servers'][$i]['table_coords'] = 'pma__table_coords';
// $cfg['Servers'][$i]['pdf_pages'] = 'pma__pdf_pages';
// $cfg['Servers'][$i]['column_info'] = 'pma__column_info';
// $cfg['Servers'][$i]['history'] = 'pma__history';
// $cfg['Servers'][$i]['table_uiprefs'] = 'pma__table_uiprefs';
// $cfg['Servers'][$i]['tracking'] = 'pma__tracking';
// $cfg['Servers'][$i]['userconfig'] = 'pma__userconfig';
// $cfg['Servers'][$i]['recent'] = 'pma__recent';
// $cfg['Servers'][$i]['favorite'] = 'pma__favorite';
// $cfg['Servers'][$i]['users'] = 'pma__users';
// $cfg['Servers'][$i]['usergroups'] = 'pma__usergroups';
// $cfg['Servers'][$i]['navigationhiding'] = 'pma__navigationhiding';
// $cfg['Servers'][$i]['savedsearches'] = 'pma__savedsearches';
// $cfg['Servers'][$i]['central_columns'] = 'pma__central_columns';
// $cfg['Servers'][$i]['designer_settings'] = 'pma__designer_settings';
// $cfg['Servers'][$i]['export_templates'] = 'pma__export_templates';
```

Next, create the user with the above details. Don't set any permissions for it just yet.

**Note:** If you can't login to phpmyadmin, make sure that your mysql server is started.

##### creating phpMyAdmin database

Using the phpMyAdmin web interface: Import `/usr/share/webapps/phpMyAdmin/sql/create_tables.sql` from phpMyAdmin -> Import. **or** Using command line: `mysql -u root -p < /usr/share/webapps/phpMyAdmin/sql/create_tables.sql`.

##### creating phpMyAdmin database user

Now to apply the permissions to your controluser, in the [SQL tab](/index.php/MySQL "MySQL"), make sure to replace all instances of 'pma' and 'pmapass' to the values set in config.inc.php. If you are setting this up for a remote database, then you must also change 'localhost' to the proper host:

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

In order to take advantage of the bookmark and relation features, you will also need to give **pma** some additional permissions:

**Note:** as long as you did not change the value of **$cfg['Servers'][$i]['pmadb']** in `/etc/webapps/phpmyadmin/config.inc.php`, then **<pma_db>** should be **phpmyadmin**

 `GRANT SELECT, INSERT, UPDATE, DELETE ON <pma_db>.* TO 'pma'@'localhost';` 

Log out, and back in to ensure the new features are activated. The message at the bottom of the main screen should now be gone.

## Accessing your phpMyAdmin installation

Your phpMyAdmin installation is now complete. Before you start using it you need to restart Apache.

You can access your phpMyAdmin installation by going to [http://localhost/phpmyadmin/](http://localhost/phpmyadmin/)

## Troubleshooting

### Fixing open_basedir warning

If you see the following Warning when entering the homepage of PhpMyAdmin:

```
Warning in ./libraries/Config.class.php#1147
file_exists(): open_basedir restriction in effect. File(./config.inc.php) is not within the allowed path(s): (/srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/)

```

It means that phpmyadmin was not able to find where the `config.inc.php` file is located.

In order to fix that, you need to indicate the path in `/etc/php/php.ini` of the `phpmyadmin` directory containing the file, which should be `/etc/webapps`, putting it at the end of the paths separated with a `:` in the `open_basedir` variable:

 `/etc/php/php.ini`  `open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/**:/etc/webapps/**` 

Once you have done that, [restart](/index.php/Restart "Restart") `httpd.service`.

Now refresh the page, and you should no longer have the warning.

### #2006 - MySQL server has gone away

If, when trying to log into PhpMyAdmin, you encounter

```
#2006 - MySQL server has gone away

Connection for controluser as defined in your configuration failed.

```

a fix seems to be to make sure you do not have SSL connection between PhpMyAdmin and MariaDB activated. Hence comment out or set to `false` the following line:

 `/etc/webapps/phpmyadmin/config.inc.php`  `$cfg['Servers'][$i]['ssl'] = true;` 

**Note:** There surely must be a better fix since 'ssl = true' worked before. Also do not disable SSL if your PhpMyAdmin install is somehow not on the same server as MySQL!

Retrieved from "[https://wiki.archlinux.org/index.php?title=PhpMyAdmin&oldid=414669](https://wiki.archlinux.org/index.php?title=PhpMyAdmin&oldid=414669)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")