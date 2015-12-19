# Apache HTTP Server

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [PHP](/index.php/PHP "PHP")
*   [MySQL](/index.php/MySQL "MySQL")
*   [PhpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin")
*   [Adminer](/index.php/Adminer "Adminer")
*   [Xampp](/index.php/Xampp "Xampp")
*   [mod_perl](/index.php/Mod_perl "Mod perl")

The [Apache HTTP Server](https://en.wikipedia.org/wiki/Apache_HTTP_Server "wikipedia:Apache HTTP Server"), or Apache for short, is a very popular web server, developed by the Apache Software Foundation.

Apache is often used together with a scripting language such as PHP and database such as MySQL. This combination is often referred to as a [LAMP](https://en.wikipedia.org/wiki/LAMP_(software_bundle) "wikipedia:LAMP (software bundle)") stack (**L**inux, **A**pache, **M**ySQL, **P**HP). This article describes how to set up Apache and how to optionally integrate it with [PHP](/index.php/PHP "PHP") and [MySQL](/index.php/MySQL "MySQL").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Advanced options](#Advanced_options)
    *   [2.2 User directories](#User_directories)
    *   [2.3 TLS/SSL](#TLS.2FSSL)
    *   [2.4 Virtual hosts](#Virtual_hosts)
        *   [2.4.1 Managing many virtual hosts](#Managing_many_virtual_hosts)
*   [3 Extensions](#Extensions)
    *   [3.1 PHP](#PHP)
        *   [3.1.1 Using php5 with php-fpm and mod_proxy_fcgi](#Using_php5_with_php-fpm_and_mod_proxy_fcgi)
        *   [3.1.2 Using php5 with apache2-mpm-worker and mod_fcgid](#Using_php5_with_apache2-mpm-worker_and_mod_fcgid)
        *   [3.1.3 MySQL/MariaDB](#MySQL.2FMariaDB)
        *   [3.1.4 SPDY](#SPDY)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Apache Status and Logs](#Apache_Status_and_Logs)
    *   [4.2 Error: PID file /run/httpd/httpd.pid not readable (yet?) after start](#Error:_PID_file_.2Frun.2Fhttpd.2Fhttpd.pid_not_readable_.28yet.3F.29_after_start)
    *   [4.3 Upgrading Apache to 2.4 from 2.2](#Upgrading_Apache_to_2.4_from_2.2)
    *   [4.4 Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.](#Apache_is_running_a_threaded_MPM.2C_but_your_PHP_Module_is_not_compiled_to_be_threadsafe.)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [apache](https://www.archlinux.org/packages/?name=apache) package.

## Configuration

Apache configuration files are located in `/etc/httpd/conf`. The main configuration file is `/etc/httpd/conf/httpd.conf`, which includes various other configuration files. The default configuration file should be fine for a simple setup. By default, it will serve the directory `/srv/http` to anyone who visits your website.

To start Apache, start `httpd.service` [using systemd](/index.php/Systemd#Using_units "Systemd").

Apache should now be running. Test by visiting [http://localhost/](http://localhost/) in a web browser. It should display a simple index page.

For optional further configuration, see the following sections.

### Advanced options

These options in `/etc/httpd/conf/httpd.conf` might be interesting for you:

```
User http

```

For security reasons, as soon as Apache is started by the root user (directly or via startup scripts) it switches to this UID. The default user is _http_, which is created automatically during installation.

```
Listen 80

```

This is the port Apache will listen to. For Internet-access with router, you have to forward the port.

If you want to setup Apache for local development you may want it to be only accessible from your computer. Then change this line to `Listen 127.0.0.1:80`.

```
ServerAdmin you@example.com

```

This is the admin's email address which can be found on e.g. error pages.

```
DocumentRoot "/srv/http"

```

This is the directory where you should put your web pages.

Change it, if you want to, but do not forget to also change `<Directory "/srv/http">` to whatever you changed your `DocumentRoot` to, or you will likely get a **403 Error** (lack of privileges) when you try to access the new document root. Do not forget to change the `Require all denied` line to `Require all granted`, otherwise you will get a **403 Error**. Remember that the DocumentRoot directory and its parent folders must allow execution permission to others (can be set with `chmod o+x /path/to/DocumentRoot`), otherwise you will get a **403 Error**.

```
AllowOverride None

```

This directive in `<Directory>` sections causes Apache to completely ignore `.htaccess` files. Note that this is now the default for Apache 2.4, so you need to explicitly allow overrides if you plan to use `.htaccess` files. If you intend to use `mod_rewrite` or other settings in `.htaccess` files, you can allow which directives declared in that file can override server configuration. For more info refer to the [Apache documentation](http://httpd.apache.org/docs/current/mod/core.html#allowoverride).

**Tip:** If you have issues with your configuration you can have Apache check the configuration with: `apachectl configtest`

More settings can be found in `/etc/httpd/conf/extra/httpd-default.conf`:

To turn off your server's signature:

```
ServerSignature Off

```

To hide server information like Apache and PHP versions:

```
ServerTokens Prod

```

### User directories

User directories are available by default through [http://localhost/~yourusername/](http://localhost/~yourusername/) and show the contents of `~/public_html` (this can be changed in `/etc/httpd/conf/extra/httpd-userdir.conf`).

If you do not want user directories to be available on the web, comment out the following line in `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/httpd-userdir.conf

```

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** It is not necessary to set `+x` for every users, setting it only for the webserver via ACLs suffices (see [Access Control Lists#Granting execution permissions for private files to a Web Server](/index.php/Access_Control_Lists#Granting_execution_permissions_for_private_files_to_a_Web_Server "Access Control Lists")). (Discuss in [Talk:Apache HTTP Server#](https://wiki.archlinux.org/index.php/Talk:Apache_HTTP_Server))

You must make sure that your home directory permissions are set properly so that Apache can get there. Your home directory and `~/public_html` must be executable for others ("rest of the world"):

```
$ chmod o+x ~
$ chmod o+x ~/public_html
$ chmod -R o+r ~/public_html

```

Restart `httpd.service` to apply any changes. See also [Umask#Set the mask value](/index.php/Umask#Set_the_mask_value "Umask").

### TLS/SSL

[openssl](https://www.archlinux.org/packages/?name=openssl) provides TLS/SSL support and is installed by default on Arch installations.

Create a private key and self-signed certificate. This is adequate for most installations that do not require a [CSR](https://en.wikipedia.org/wiki/Certificate_signing_request "wikipedia:Certificate signing request"):

```
# cd /etc/httpd/conf
# openssl req -new -x509 -nodes -newkey rsa:4096 -keyout apache.key -out apache.crt -days 1095
# chmod 400 apache.key
# chmod 444 apache.crt

```

Then edit `/etc/httpd/conf/extra/httpd-ssl.conf` to reflect the new key and certificate:

*   `SSLCertificateFile "/etc/httpd/conf/server.crt" => SSLCertificateFile "/etc/httpd/conf/apache.crt",`,
*   `SSLCertificateKeyFile "/etc/httpd/conf/server.key" => SSLCertificateKeyFile "/etc/httpd/conf/apache.key",`

**Note:** The -days switch is optional and RSA keysize can be as low as 2048 (default).

If you need to create a [CSR](https://en.wikipedia.org/wiki/Certificate_signing_request "wikipedia:Certificate signing request"), follow these keygen instructions instead of the above:

```
# openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:4096 -out apache.key
# chmod 400 apache.key
# openssl req -new -sha256 -key apache.key -out apache.csr
# openssl x509 -req -days 1095 -in apache.csr -signkey apache.key -out apache.crt

```

**Note:** For more openssl options, read the [man page](https://www.openssl.org/docs/apps/openssl.html) or peruse openssl's [extensive documentation](https://www.openssl.org/docs/).

Then, in `/etc/httpd/conf/httpd.conf`, uncomment the following three lines:

```
LoadModule ssl_module modules/mod_ssl.so
LoadModule socache_shmcb_module modules/mod_socache_shmcb.so
Include conf/extra/httpd-ssl.conf

```

**Warning:** If you plan on implementing SSL/TLS, know that some variations and implementations are [still](https://weakdh.org/#affected) [vulnerable to attack](https://en.wikipedia.org/wiki/Transport_Layer_Security#Attacks_against_TLS.2FSSL "wikipedia:Transport Layer Security"). For details on these current vulnerabilities within SSL/TLS and how to apply appropriate changes to the web server, visit [http://disablessl3.com/](http://disablessl3.com/) and [https://weakdh.org/sysadmin.html](https://weakdh.org/sysadmin.html)

**Tip:** Mozilla has a useful [SSL/TLS article](https://wiki.mozilla.org/Security/Server_Side_TLS) which includes [Apache specific](https://wiki.mozilla.org/Security/Server_Side_TLS#Apache) configuration guidelines as well as an [automated tool](https://mozilla.github.io/server-side-tls/ssl-config-generator/) to help create a more secure configuration.

Restart `httpd.service` to apply any changes.

### Virtual hosts

**Note:** You will need to add a separate <VirtualHost dommainame:443> section for virtual host SSL support. See [#Managing many virtual hosts](#Managing_many_virtual_hosts) for an example file.

If you want to have more than one host, uncomment the following line in `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/httpd-vhosts.conf

```

In `/etc/httpd/conf/extra/httpd-vhosts.conf` set your virtual hosts. The default file contains an elaborate example that should help you get started.

To test the virtual hosts on you local machine, add the virtual names to your `/etc/hosts` file:

```
127.0.0.1 domainname1.dom 
127.0.0.1 domainname2.dom

```

Restart `httpd.service` to apply any changes.

#### Managing many virtual hosts

If you have a huge amount of virtual hosts, you may want to easily disable and enable them. It is recommended to create one configuration file per virtual host and store them all in one folder, eg: `/etc/httpd/conf/vhosts`.

First create the folder:

```
# mkdir /etc/httpd/conf/vhosts

```

Then place the single configuration files in it:

```
# nano /etc/httpd/conf/vhosts/domainname1.dom
# nano /etc/httpd/conf/vhosts/domainname2.dom
...

```

In the last step, `Include` the single configurations in your `/etc/httpd/conf/httpd.conf`:

```
#Enabled Vhosts:
Include conf/vhosts/domainname1.dom
Include conf/vhosts/domainname2.dom

```

You can enable and disable single virtual hosts by commenting or uncommenting them.

A very basic vhost file will look like this:

 `/etc/httpd/conf/vhosts/domainname1.dom` 

```
<VirtualHost domainname1.dom:80>
    ServerAdmin webmaster@domainname1.dom
    DocumentRoot "/home/user/http/domainname1.dom"
    ServerName domainname1.dom
    ServerAlias domainname1.dom
    ErrorLog "/var/log/httpd/domainname1.dom-error_log"
    CustomLog "/var/log/httpd/domainname1.dom-access_log" common

    <Directory "/home/user/http/domainname1.dom">
        Require all granted
    </Directory>
</VirtualHost>

<VirtualHost domainname1.dom:443>
    ServerAdmin webmaster@domainname1.dom
    DocumentRoot "/home/user/http/domainname1.dom"
    ServerName domainname1.dom:443
    ServerAlias domainname1.dom:443
    ErrorLog "/var/log/httpd/domainname1.dom-error_log"
    CustomLog "/var/log/httpd/domainname1.dom-access_log" common

    <Directory "/home/user/http/domainname1.dom">
        Require all granted
    </Directory>

    SSLEngine on
    SSLCertificateFile "/etc/httpd/conf/apache.crt"
    SSLCertificateKeyFile "/etc/httpd/conf/apache.key"
</VirtualHost>
```

## Extensions

### PHP

**Tip:** If you are using PHP 7 (to hit the repositories soon), replace all `php5` mentions below with `php7`.

To install [PHP](/index.php/PHP "PHP"), first [install](/index.php/Install "Install") the [php](https://www.archlinux.org/packages/?name=php) and [php-apache](https://www.archlinux.org/packages/?name=php-apache) packages.

**Note:** `libphp5.so` included with [php-apache](https://www.archlinux.org/packages/?name=php-apache) does not work with `mod_mpm_event` ([FS#39218](https://bugs.archlinux.org/task/39218)). You will have to use `mod_mpm_prefork` instead. Otherwise you will get the following error:

```
Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.  You need to recompile PHP.
AH00013: Pre-configuration failed
httpd.service: control process exited, code=exited status=1
```

As the configuration of `/etc/httpd/conf/httpd.conf` has for standard the `mod_mpm_event` you will have to use `mod_mpm_prefork` in order for `libphp5.so` to work properly. To do so open `/etc/httpd/conf/httpd.conf` comment the line:

 `LoadModule mpm_event_module modules/mod_mpm_event.so` 

and uncomment the line:

 `LoadModule mpm_prefork_module modules/mod_mpm_prefork.so` As an alternative, you can use `mod_proxy_fcgi` (see [#Using php5 with php-fpm and mod_proxy_fcgi](#Using_php5_with_php-fpm_and_mod_proxy_fcgi) below).

To enable PHP, add these lines to `/etc/httpd/conf/httpd.conf`:

*   Place this in the `LoadModule` list anywhere after `LoadModule dir_module modules/mod_dir.so`:

```
LoadModule php5_module modules/libphp5.so

```

*   Place this at the end of the `Include` list:

```
Include conf/extra/php5_module.conf

```

If your `DocumentRoot` is not `/srv/http`, add it to `open_basedir` in `/etc/php/php.ini` as such:

```
open_basedir=/srv/http/:/home/:/tmp/:/usr/share/pear/:/path/to/documentroot

```

Restart `httpd.service` [using systemd](/index.php/Systemd#Using_units "Systemd")

To test whether PHP was correctly configured: create a file called `test.php` in your Apache `DocumentRoot` directory (e.g. `/srv/http/` or `~/public_html`) with the following contents:

```
<?php phpinfo(); ?>

```

To see if it works go to: [http://localhost/test.php](http://localhost/test.php) or [http://localhost/~myname/test.php](http://localhost/~myname/test.php)

For advanced configuration and extensions, please read [PHP](/index.php/PHP "PHP").

#### Using php5 with php-fpm and mod_proxy_fcgi

**Note:** Unlike the widespread setup with ProxyPass, the proxy configuration with SetHandler respects other Apache directives like DirectoryIndex. This ensures a better compatibility with software designed for libphp5, mod_fastcgi and mod_fcgid. If you still want to try ProxyPass, experiment with a line like this: `ProxyPassMatch ^/(.*\.php(/.*)?)$ unix:/run/php-fpm/php-fpm.sock|fcgi://localhost/srv/http/$1` 

*   [Install](/index.php/Install "Install") the [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) package.

*   Set `listen` in `/etc/php/php-fpm.conf` like this (these values are currently the defaults):

```
;listen = 127.0.0.1:9000
listen = /run/php-fpm/php-fpm.sock
listen.owner = http
listen.group = http

```

*   Append following to `/etc/httpd/conf/httpd.conf`:

```
<FilesMatch \.php$>
    SetHandler "proxy:unix:/run/php-fpm/php-fpm.sock|fcgi://localhost/"
</FilesMatch>
<Proxy "fcgi://localhost/" enablereuse=on max=10>
</Proxy>
<IfModule dir_module>
    DirectoryIndex index.php index.html
</IfModule>

```

The pipe between sock and fcgi is not allowed to be surrounded by a space! "localhost" after fcgi: can be replaced by any string but it should match in SetHandler and Proxy directives. More here: [https://httpd.apache.org/docs/2.4/mod/mod_proxy_fcgi.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy_fcgi.html) SetHandler and Proxy can be used per vhost configs but the name after fcgi:// should differ for each vhost setup.

*   If you have it added, remove the php module, as this is no longer needed.

```
LoadModule php5_module modules/libphp5.so

```

*   [Restart](/index.php/Restart "Restart") the apache php-fpm daemon again.

#### Using php5 with apache2-mpm-worker and mod_fcgid

*   Uncomment following in `/etc/conf.d/apache`:

```
HTTPD=/usr/bin/httpd.worker

```

*   Uncomment following in `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/httpd-mpm.conf

```

*   [Install](/index.php/Install "Install") the [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid) and [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) packages from the [official repositories](/index.php/Official_repositories "Official repositories").

*   Create `/etc/httpd/conf/extra/php5_fcgid.conf` with following content:

 `/etc/httpd/conf/extra/php5_fcgid.conf` 

```
# Required modules: fcgid_module

<IfModule fcgid_module>
    AddHandler php-fcgid .php
    AddType application/x-httpd-php .php
    Action php-fcgid /fcgid-bin/php-fcgid-wrapper
    ScriptAlias /fcgid-bin/ /srv/http/fcgid-bin/
    SocketPath /var/run/httpd/fcgidsock
    SharememPath /var/run/httpd/fcgid_shm
        # If you don't allow bigger requests many applications may fail (such as WordPress login)
        FcgidMaxRequestLen 536870912
        # Path to php.ini – defaults to /etc/phpX/cgi
        DefaultInitEnv PHPRC=/etc/php/
        # Number of PHP childs that will be launched. Leave undefined to let PHP decide.
        #DefaultInitEnv PHP_FCGI_CHILDREN 3
        # Maximum requests before a process is stopped and a new one is launched
        #DefaultInitEnv PHP_FCGI_MAX_REQUESTS 5000
        <Location /fcgid-bin/>
        SetHandler fcgid-script
        Options +ExecCGI
    </Location>
</IfModule>

```

*   Create the needed directory and symlink it for the PHP wrapper:

```
# mkdir /srv/http/fcgid-bin
# ln -s /usr/bin/php-cgi /srv/http/fcgid-bin/php-fcgid-wrapper

```

*   Edit `/etc/httpd/conf/httpd.conf`:

```
#LoadModule php5_module modules/libphp5.so
LoadModule fcgid_module modules/mod_fcgid.so
Include conf/extra/php5_fcgid.conf

```

and [restart](/index.php/Daemons "Daemons") **httpd**.

**Note:** As of Apache 2.4 you can now use [mod_proxy_fcgi](http://httpd.apache.org/docs/2.4/mod/mod_proxy_fcgi.html) (part of the official distribution) with PHP-FPM (and the new event MPM). See this [configuration example](http://wiki.apache.org/httpd/PHP-FPM).

#### MySQL/MariaDB

Follow the instructions in [PHP#MySQL/MariaDB](/index.php/PHP#MySQL.2FMariaDB "PHP").

When configuration is complete, [restart](/index.php/Restart "Restart") `httpd.service` to apply all the changes.

#### SPDY

mod_spdy is a SPDY module for Apache 2.2 that allows your web server to take advantage of SPDY features like stream multiplexing and header compression.

Follow the instructions in [Apache and spdy](/index.php/Apache_and_spdy "Apache and spdy").

## Troubleshooting

### Apache Status and Logs

See the status of the Apache daemon with [systemctl](/index.php/Systemctl "Systemctl").

Apache logs can be found in `/var/log/httpd/`

### Error: PID file /run/httpd/httpd.pid not readable (yet?) after start

Comment out the unique_id_module: `#LoadModule unique_id_module modules/mod_unique_id.so`

### Upgrading Apache to 2.4 from 2.2

If you use `php-apache`, follow the introductory note to [Apache with PHP](#PHP) above.

Access Control has changed. Convert all `Order`, `Allow`, `Deny` and `Satisfy` directives to the new `Require` syntax. [mod_access_compat](http://httpd.apache.org/docs/2.4/mod/mod_access_compat.html) allows you to use the deprecated format during a transition phase.

More information: [Upgrading to 2.4 from 2.2](http://httpd.apache.org/docs/2.4/upgrading.html)

### Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.

If when loading `php5_module` the `httpd.service` fails, and you get an error like this in the journal:

```
Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.  You need to recompile PHP.

```

you need to replace `mpm_event_module` with `mpm_prefork_module`:

 `/etc/httpd/conf/httpd.conf` 

```
<s>LoadModule mpm_event_module modules/mod_mpm_event.so</s>
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

and restart `httpd.service`.

## See also

*   [Apache Official Website](http://www.apache.org/)
*   [Tutorial for creating self-signed certificates](http://www.akadia.com/services/ssh_test_certificate.html)
*   [Apache Wiki Troubleshooting](http://wiki.apache.org/httpd/CommonMisconfigurations)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Apache_HTTP_Server&oldid=412777](https://wiki.archlinux.org/index.php?title=Apache_HTTP_Server&oldid=412777)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")