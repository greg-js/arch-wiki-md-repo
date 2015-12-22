# Roundcube

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[Roundcube](http://roundcube.net) is a full-featured, [PHP](/index.php/PHP "PHP") web-based mail client.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 MariaDB](#MariaDB)
    *   [2.2 Roundcube](#Roundcube)
    *   [2.3 PHP](#PHP)
    *   [2.4 Webserver (Apache)](#Webserver_.28Apache.29)
    *   [2.5 Webserver (Nginx)](#Webserver_.28Nginx.29)
*   [3 Install Roundcube](#Install_Roundcube)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Setting Roundcube up for use with an IMAP server that only allows TLS authentication](#Setting_Roundcube_up_for_use_with_an_IMAP_server_that_only_allows_TLS_authentication)
    *   [4.2 PDF and OpenDocument file preview](#PDF_and_OpenDocument_file_preview)
    *   [4.3 Synchronize address book with CardDav contacts](#Synchronize_address_book_with_CardDav_contacts)
*   [5 See also](#See_also)

## Installation

Install the [roundcubemail](https://www.archlinux.org/packages/?name=roundcubemail) package. Further you will need a database (e.g. [MariaDB](/index.php/MariaDB "MariaDB")) and a [web server](/index.php/Category:Web_server "Category:Web server") with [PHP](/index.php/PHP "PHP")-support (this guide will assume the [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server")).

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

### Roundcube

Copy the example configuration file and adjust it to your configuration:

```
# cp /etc/webapps/roundcubemail/config/config.inc.php.sample /etc/webapps/roundcubemail/config/config.inc.php

```

Set your mail server settings, and set `enable_installer` to enable the setup wizard:

 `/etc/webapps/roundcubemail/config/config.inc.php` 

```
$config['db_dsnw'] = 'mysql://roundcube:****@localhost/roundcubemail';
$config['default_host'] = 'tls://localhost';
$config['smtp_server'] = 'localhost';
$config['enable_installer'] = true;

```

### PHP

Make sure to adjust following variables to these minimal values in your PHP config:

 `/etc/php/php.ini` 

```
date.timezone = "UTC"

```

and uncomment

```
extension=iconv.so
extension=mbstring.so

```

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

**Warning:** This is an example config of RoundCube running in an subdirectory of the web root and has been compiled based on experiments with information from multiple sources, proceed with caution

**Note:** This assumes you already have a working [nginx](/index.php/Nginx "Nginx") server setup with [php-fpm](/index.php/Nginx#PHP_configuration "Nginx")

Add a location block for RoundCube

 `/etc/nginx.conf` 

```
location /webmail {
        alias /usr/share/webapps/roundcubemail;
        access_log /var/log/nginx/roundcube_access.log;
        error_log /var/log/nginx/roundcube_error.log;
        #Favicon
        location ~ ^/favicon.ico$ {
                root /usr/share/webapps/roundcubemail/skins/classic/images;
                log_not_found off;
                access_log off;
                expires max;
        }
        #Robots file
        location ~ ^/robots.txt {
                allow all;
                log_not_found off;
                access_log off;
        }
        #Deny Protected directories 
        location ~ ^/(config|temp|logs)/ {
                 deny all;
        }
        location ~ ^/(README|INSTALL|LICENSE|CHANGELOG|UPGRADING)$ {
                deny all;
        }
        location ~ ^/(bin|SQL)/ {
                deny all;
        }
        #Hide all dot files
        location ~ /\. {
                deny all;
                access_log off;
                log_not_found off;
        }
        #Roundcube fastcgi config
        location ~ /webmail(/.*\.php)$ {
                set $valid_fastcgi_script_name $1;
                include fastcgi_params;
                fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
                fastcgi_split_path_info ^(.+.php)(/.*)$;
                fastcgi_index index.php;
                fastcgi_param SCRIPT_FILENAME /usr/share/webapps/roundcubemail/$valid_fastcgi_script_name;
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

### Setting Roundcube up for use with an IMAP server that only allows TLS authentication

It's quite common for modern IMAP servers to only allow encrypted authentication, say using STARTTLS. **If you are setting Roundcube up for TLS authentication, the web-based installer won't help you.** You will need to edit the `/etc/webapps/roundcubemail/config/config.inc.php` by hand, adding the following lines:

```
 $config['default_host'] = 'tls://mail.my_domain.org';

```

```
 $config['imap_conn_options'] = array(
     'ssl' => array(
       'verify_peer'       => true,
       'allow_self_signed' => true,
       'peer_name'         => 'mail.my_domain.org',
       'ciphers' => 'TLSv1+HIGH:!aNull:@STRENGTH',
       'cafile'  => '/etc/ssl/certs/ssl-cert-cyrus.my_domain.org.pem',
     ),
 );

```

where `mail.my_domain.org` is the `CN` host name in your SSL certificate (i.e. the hostname of your IMAP server), and `/etc/ssl/certs/ssl-cert-cyrus.my_domain.org.pem` is the path to your SSL certificate. You might need to adjust the `ciphers` element to correspond to the ciphers allowed by your IMAP server.

A complete list of PHP SSL configuration options [can be found here](http://php.net/manual/en/context.ssl.php).

### PDF and OpenDocument file preview

Following Roundcube extensions enables you to preview PDF or OpenDocument file attachements. Install [roundcubemail-plugins-kolab](https://aur.archlinux.org/packages/roundcubemail-plugins-kolab/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR") and adjust following configuration file to enable the extensions:

 `/etc/webapps/roundcubemail/config/config.inc.php` 

```
$config['plugins'] = array(
    'pdfviewer',
    'odfviewer'
);

```

If you encounter any file permission issues, than try this command:

 `chown -R http:http /usr/share/webapps/roundcubemail/plugins/odfviewer/files` 

### Synchronize address book with CardDav contacts

It's useful to use the Roundcube address book to have auto-completion features for address fields etc. If you have your contacts stored somewhere else and the remote application offers a CardDav server for synchronization, then you can use the [roundcube-rcmcarddav](https://aur.archlinux.org/packages/roundcube-rcmcarddav/)<sup><small>AUR</small></sup> extension from the [AUR](/index.php/AUR "AUR") to access your remote address book in Roundcube. To enable it, adjust following lines in your config file:

 `/etc/webapps/roundcubemail/config/config.inc.php` 

```
$config['plugins'] = array(
    'carddav'
);
```

Further usage instructions can be found [here](https://github.com/blind-coder/rcmcarddav).

## See also

*   [The Roundcube Howto Config Wiki page](http://trac.roundcube.net/wiki/Howto_Config)
*   [Offical web page](http://roundcube.net)
*   [Official installation manual](http://trac.roundcube.net/wiki/Howto_Install)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Roundcube&oldid=413100](https://wiki.archlinux.org/index.php?title=Roundcube&oldid=413100)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Email clients](/index.php/Category:Email_clients "Category:Email clients")