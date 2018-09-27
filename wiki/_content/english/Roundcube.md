[Roundcube](https://roundcube.net) is a full-featured, [PHP](/index.php/PHP "PHP") web-based mail client.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 MariaDB](#MariaDB)
    *   [2.2 SQLite](#SQLite)
    *   [2.3 Other Databases](#Other_Databases)
    *   [2.4 Roundcube](#Roundcube)
    *   [2.5 PHP](#PHP)
    *   [2.6 Webserver (Apache)](#Webserver_.28Apache.29)
    *   [2.7 Webserver (Nginx)](#Webserver_.28Nginx.29)
*   [3 Install Roundcube](#Install_Roundcube)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Setting Roundcube up for use with an IMAP/SMTP server that only allows TLS authentication](#Setting_Roundcube_up_for_use_with_an_IMAP.2FSMTP_server_that_only_allows_TLS_authentication)
    *   [4.2 PDF and OpenDocument file preview](#PDF_and_OpenDocument_file_preview)
    *   [4.3 Calendar Support](#Calendar_Support)
        *   [4.3.1 Update the roundcube database](#Update_the_roundcube_database)
        *   [4.3.2 Configure the calendar service](#Configure_the_calendar_service)
        *   [4.3.3 Sabre\VObject\Property\Text Not Found](#Sabre.5CVObject.5CProperty.5CText_Not_Found)
        *   [4.3.4 Enable the Plugin](#Enable_the_Plugin)
    *   [4.4 Synchronize address book with CardDav contacts](#Synchronize_address_book_with_CardDav_contacts)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 SMTP Error: Authentication failure](#SMTP_Error:_Authentication_failure)
*   [6 See also](#See_also)

## Installation

Install the [roundcubemail](https://www.archlinux.org/packages/?name=roundcubemail) package. Further you will need a database (e.g. [MariaDB](/index.php/MariaDB "MariaDB")) and a [web server](/index.php/Web_server "Web server") with [PHP](/index.php/PHP "PHP")-support (this guide will assume the [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server")).

## Configuration

### MariaDB

Here's an example on how you could setup a database for Roundcube with [MariaDB](/index.php/MariaDB "MariaDB") called `roundcubemail` for the user `roundcube` identified by the password `password`:

 `$ mysql -u root -p` 
```
CREATE DATABASE roundcubemail;
GRANT ALL PRIVILEGES ON roundcubemail.* TO 'roundcube'@'localhost' IDENTIFIED BY 'password';

```

For any database you use, you will need to initialize the roundcubemail database tables. Here is an example of how to do this with [MariaDB](/index.php/MariaDB "MariaDB"):

```
$ mysql -u root -p roundcubemail < /usr/share/webapps/roundcubemail/SQL/mysql.initial.sql

```

### SQLite

A SQLite DB will be created automagically by Roundcube. Ensure the file specified in the configuration is located in a basedir location. Consider adding /var/lib/roundcubemail to your basedir definition. This implies creating the directory and chowning it to http.

### Other Databases

Roundcubemail has installation scripts for mssql, Oracle, and PostgreSQL.

### Roundcube

Copy the example configuration file and adjust it to your configuration:

```
# cp /etc/webapps/roundcubemail/config/config.inc.php.sample /etc/webapps/roundcubemail/config/config.inc.php

```

Set your mail server settings, and set `enable_installer` to enable the setup wizard:

 `/etc/webapps/roundcubemail/config/config.inc.php` 
```
$config['db_dsnw'] = 'mysql://roundcube:****@localhost/roundcubemail';
$config['default_host'] = 'tls://localhost'; // IMAP host
$config['smtp_server'] = 'tls://localhost';
$config['smtp_port'] = 587;
$config['des_key'] = 'some_awesome_long_semi_random_string';
$config['enable_installer'] = true;

```

For roundcube to be able to detect mime-types from filename extensions you need to point it to a mime.types file. Apache usually comes with one.

```
# cp /etc/httpd/conf/mime.types /etc/webapps/roundcubemail/config/mime.types
# chown http:http /etc/webapps/roundcubemail/config/mime.types

```
 `/etc/webapps/roundcubemail/config/config.inc.php` 
```
$config['mime_types'] = '/etc/webapps/roundcubemail/config/mime.types';

```

If you are not using Apache, check the information available in /etc/webapps/roundcubemail/config/defaults.inc.php .

### PHP

Make sure to adjust following variables to these minimal values in your PHP configuration:

 `/etc/php/php.ini` 
```
date.timezone = "UTC"

```

and uncomment

```
extension=iconv

```

**If** you have configured `open_basedir` in `php.ini`, make sure it includes `/etc/webapps` and `/usr/share/webapps`, so PHP can open the required Roundcube files. If `open_basedir` is disabled/commented out (the default setting), you don't have to do anything.

### Webserver (Apache)

Copy the configuration file for Apache to its configuration directory:

```
# cp /etc/webapps/roundcubemail/apache.conf /etc/httpd/conf/extra/roundcube.conf

```

And include it at the bottom of

 `/etc/httpd/conf/httpd.conf` 
```
Include conf/extra/roundcube.conf

```

Restart Apache (`httpd.service`).

### Webserver (Nginx)

**Warning:** This is an example configuration of RoundCube running in an subdirectory of the web root and has been compiled based on experiments with information from multiple sources, proceed with caution

**Note:** This assumes you already have a working [nginx](/index.php/Nginx "Nginx") server setup with [php-fpm](/index.php/Nginx#FastCGI "Nginx").

Add a location block for RoundCube

 `/etc/nginx.conf` 
```
location /webmail {
        alias /usr/share/webapps/roundcubemail;
        access_log /var/log/nginx/roundcube_access.log;
        error_log /var/log/nginx/roundcube_error.log;
        # Favicon
        location ~ ^/webmail/favicon.ico$ {
                root /usr/share/webapps/roundcubemail/skins/classic/images;
                log_not_found off;
                access_log off;
                expires max;
        }
        # Robots file
        location ~ ^/webmail/robots.txt {
                allow all;
                log_not_found off;
                access_log off;
        }
        # Deny Protected directories 
        location ~ ^/webmail/(config|temp|logs)/ {
                 deny all;
        }
        location ~ ^/webmail/(README|INSTALL|LICENSE|CHANGELOG|UPGRADING)$ {
                deny all;
        }
        location ~ ^/webmail/(bin|SQL)/ {
                deny all;
        }
        # Hide .md files
        location ~ ^/webmail/(.+\.md)$ {
                deny all;
        }
        # Hide all dot files
        location ~ ^/webmail/\. {
                deny all;
                access_log off;
                log_not_found off;
        }
        #Roundcube fastcgi config
        location ~ /webmail(/.*\.php)$ {
                include fastcgi.conf;
                fastcgi_pass unix:/run/php-fpm/php-fpm.sock;
                fastcgi_split_path_info ^/webmail/(.+\.php)(/.*)$;
                fastcgi_index index.php;
                fastcgi_param SCRIPT_FILENAME /usr/share/webapps/roundcubemail/$fastcgi_script_name;
                fastcgi_param PATH_INFO $fastcgi_path_info;
                fastcgi_param PHP_VALUE open_basedir="/tmp/:/var/cache/roundcubemail:/usr/share/webapps/roundcubemail:/etc/webapps/roundcubemail:/usr/share/pear/:/var/log/roundcubemail";
        }
}

```

Finally [restart](/index.php/Restart "Restart") the `nginx.service` unit.

## Install Roundcube

Finally you can visit the Roundcube installation wizard in your browser: [http://localhost/roundcube/installer](http://localhost/roundcube/installer)

For security reasons, you should **disable the installer when you have completed the wizard**: remove `$config['enable_installer'] = true;` from `config.inc.php`.

Because the `~/roundcube/config` directory contains sensitive information about your server, it's also a good idea to disallow access to this directory by adding these lines, too.

 `/etc/httpd/conf/extra/roundcube.conf` 
```
  <Directory /usr/share/webapps/roundcubemail/config>
     Options -FollowSymLinks
     AllowOverride None
     Require all denied
  </Directory>

```

## Tips and tricks

### Setting Roundcube up for use with an IMAP/SMTP server that only allows TLS authentication

It is quite common for modern IMAP/SMTP servers to only allow encrypted authentication, say using STARTTLS. **If you are setting Roundcube up for TLS authentication, the web-based installer won't help you.** You will need to edit the `/etc/webapps/roundcubemail/config/config.inc.php` by hand, adding the following lines:

```
 $config['default_host'] = 'tls://mail.my_domain.org';
 // For STARTTLS IMAP
 $config['imap_conn_options'] = array(
     'ssl' => array(
       'verify_peer'       => true,
       // certificate is not self-signed if cafile provided
       'allow_self_signed' => false,
       'cafile'  => '/etc/ssl/certs/Your_CA_certificate.pem',
       // For Letsencrypt use the following two lines and remove the 'cafile' option above.
       //'ssl_cert => '/etc/letsencrypt/live/mail.my_domain.org/fullchain.pem'
       //'ssl_key'  => '/etc/letsencrypt/live/mail.my_domain.org/privkey.pem'
       // probably optional parameters
       'ciphers' => 'TLSv1+HIGH:!aNull:@STRENGTH',
       'peer_name'         => 'mail.my_domain.org',
     ),
 );
 // For STARTTLS SMTP
 $config['smtp_conn_options'] = array(
     'ssl' => array(
       'verify_peer'       => true,
       // certificate is not self-signed if cafile provided
       'allow_self_signed' => false,
       'cafile'  => '/etc/ssl/certs/Your_CA_certificate.pem',
       // For Letsencrypt use the following two lines and remove the 'cafile' option above.
       //'ssl_cert => '/etc/letsencrypt/live/mail.my_domain.org/fullchain.pem'
       //'ssl_key'  => '/etc/letsencrypt/live/mail.my_domain.org/privkey.pem'
       // probably optional parameters
       'ciphers' => 'TLSv1+HIGH:!aNull:@STRENGTH',
       'peer_name'         => 'mail.my_domain.org',
     ),
 );

```

where `mail.my_domain.org` is the `CN` host name in your SSL certificate (i.e. the hostname of your IMAP server), and `/etc/ssl/certs/Your_CA_certificate.pem` is the path to your SSL certificate. You might need to adjust the `ciphers` element to correspond to the ciphers allowed by your IMAP server.

A complete list of PHP SSL configuration options [can be found here](http://php.net/manual/en/context.ssl.php).

### PDF and OpenDocument file preview

The following Roundcube extensions enable you to preview PDF or OpenDocument file attachements.

Install the [roundcubemail-plugins-kolab](https://aur.archlinux.org/packages/roundcubemail-plugins-kolab/) package and adjust following configuration file to enable the extensions.

 `/etc/webapps/roundcubemail/config/config.inc.php` 
```
$config['plugins'] = array(
    'pdfviewer',
    'odfviewer'
);

```

If you encounter any file permission issues, than try this command:

 `chown -R http:http /usr/share/webapps/roundcubemail/plugins/odfviewer/files` 

### Calendar Support

Install the [roundcubemail-plugins-kolab](https://aur.archlinux.org/packages/roundcubemail-plugins-kolab/) package.

#### Update the roundcube database

```
# mysql -u root -p roundcubemail < /usr/share/webapps/roundcubemail/plugins/calendar/drivers/database/SQL/mysql.initial.sql

```

#### Configure the calendar service

The default configuration should suffice for most applications, however we still need to move it into place.

```
# cp /usr/share/webapps/roundcubemail/plugins/calendar/config.inc.php.dist /usr/share/webapps/roundcubemail/plugins/calendar/config.inc.php

```

#### Sabre\VObject\Property\Text Not Found

If you get this error, it means that either Sabre was not included with the plugin or it is out of date

```
# cd /usr/share/webapps/roundcubemail ; composer update ; composer require sabre/dav ~3.1.3

```

#### Enable the Plugin

 `/etc/webapps/roundcubemail/config/config.inc.php` 
```
$config['plugins'] = array(
    'calendar'
);

```

### Synchronize address book with CardDav contacts

It's useful to use the Roundcube address book to have auto-completion features for address fields etc. If you have your contacts stored somewhere else and the remote application offers a CardDav server for synchronization, then you can use the [roundcube-rcmcarddav](https://aur.archlinux.org/packages/roundcube-rcmcarddav/) extension from the [AUR](/index.php/AUR "AUR") to access your remote address book in Roundcube. To enable it, adjust following lines in your config file:

 `/etc/webapps/roundcubemail/config/config.inc.php` 
```
$config['plugins'] = array(
    'carddav'
);
```

Further usage instructions can be found [here](https://github.com/blind-coder/rcmcarddav).

## Troubleshooting

### SMTP Error: Authentication failure

You may first try to disable(comment) the following settings in *config.inc.php* as shown:

```
//$config['smtp_user'] = '%u';
//$config['smtp_pass'] = '%p';

```

## See also

*   [The Roundcube Howto Config Wiki page](https://github.com/roundcube/roundcubemail/wiki/Configuration)
*   [Offical web page](http://roundcube.net)
*   [Official installation manual](https://github.com/roundcube/roundcubemail/wiki/Installation)