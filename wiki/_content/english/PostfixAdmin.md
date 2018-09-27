[PostfixAdmin](http://postfixadmin.sourceforge.net/) is a web interface for [Postfix](/index.php/Postfix "Postfix") used to manage mailboxes, virtual domains and aliases.

## Installation

To use PostfixAdmin, you need a working Apache/MySQL/PHP setup as described in [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server").

For IMAP functionality, you will need to install [php-imap](https://www.archlinux.org/packages/?name=php-imap) and uncomment `extension=imap` in `/etc/php/php.ini`.

Next, [install](/index.php/Install "Install") [postfixadmin](https://www.archlinux.org/packages/?name=postfixadmin).

## Configuration

Edit the PostfixAdmin configuration file:

 `/etc/webapps/postfixadmin/config.inc.php` 
```
$CONF['configured'] = true;
// correspond to dovecot maildir path /home/vmail/%d/%u 
$CONF['domain_path'] = 'YES';
$CONF['domain_in_mailbox'] = 'NO';
$CONF['database_type'] = 'mysqli';
$CONF['database_host'] = 'localhost';
$CONF['database_user'] = 'postfix_user';
$CONF['database_password'] = 'hunter2';
$CONF['database_name'] = 'postfix_db';

// globally change all instances of ''change-this-to-your.domain.tld'' 
// to an appropriate value

```

If installing dovecot and you changed the password scheme in dovecot (to SHA512-CRYPT for example), reflect that with Postfix

 `/etc/webapps/postfixadmin/config.inc.php` 
```
$CONF['encrypt'] = 'dovecot:SHA512-CRYPT';

```

As of dovecot 2, dovecotpw has been deprecated. You will also want to ensure that your config reflects the new binary name.

 `/etc/webapps/postfixadmin/config.inc.php` 
```
$CONF['dovecotpw'] = "/usr/sbin/doveadm pw";

```

**Note:** For this to work it does not suffice to have dovecot installed, it also needs to be configured. See [Dovecot#Dovecot configuration](/index.php/Dovecot#Dovecot_configuration "Dovecot").

Create the Apache configuration file:

 `/etc/httpd/conf/extra/httpd-postfixadmin.conf` 
```
Alias /postfixadmin "/usr/share/webapps/postfixAdmin/public"
<Directory "/usr/share/webapps/postfixAdmin/public">
    DirectoryIndex index.html index.php
    AllowOverride All
    Options FollowSymlinks
    Require all granted
</Directory>

```

To only allow localhost access to postfixadmin (for heightened security), add this to the previous <Directory> directive:

```
   Order Deny,Allow
   Deny from all
   Allow from 127.0.0.1

```

Now, include httpd-postfixadmin.conf to `/etc/httpd/conf/httpd.conf`:

```
# PostfixAdmin configuration
Include conf/extra/httpd-postfixadmin.conf

```

Finally, navigate to [http://127.0.0.1:80/postfixadmin/setup.php](http://127.0.0.1:80/postfixadmin/setup.php) to finish the setup. Generate your setup password hash at the bottom of the page once it is done. Write the hash to the config file

 `/etc/webapps/postfixadmin/config.inc.php` 
```
$CONF['setup_password'] = 'yourhashhere';

```

Now you can create a superadmin account at [http://127.0.0.1:80/postfixadmin/setup.php](http://127.0.0.1:80/postfixadmin/setup.php)

**Note:** If you go to yourdomain/postfixadmin/setup.php and it says do not find config.inc.php, add `/etc/webapps/postfixadmin` to the `open_basedir` line in `/etc/php/php.ini`.

**Note:** If you get a blank page check the syntax of the file with `php -l /etc/webapps/postfixadmin/config.inc.php`.