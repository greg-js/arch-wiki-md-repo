Related articles

*   [XAMPP](/index.php/XAMPP "XAMPP")
*   [/mod_perl](/index.php/Apache_HTTP_Server/mod_perl "Apache HTTP Server/mod perl")

The [Apache HTTP Server](https://en.wikipedia.org/wiki/Apache_HTTP_Server "wikipedia:Apache HTTP Server"), or Apache for short, is a very popular web server, developed by the Apache Software Foundation.

This article describes how to set up Apache and how to optionally integrate it with [PHP](/index.php/PHP "PHP").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Advanced options](#Advanced_options)
    *   [2.2 User directories](#User_directories)
    *   [2.3 TLS](#TLS)
        *   [2.3.1 Create a key and (self-signed) certificate](#Create_a_key_and_(self-signed)_certificate)
    *   [2.4 Virtual hosts](#Virtual_hosts)
        *   [2.4.1 Managing many virtual hosts](#Managing_many_virtual_hosts)
*   [3 Extensions](#Extensions)
    *   [3.1 PHP](#PHP)
        *   [3.1.1 Using libphp](#Using_libphp)
        *   [3.1.2 Using php-fpm and mod_proxy_fcgi](#Using_php-fpm_and_mod_proxy_fcgi)
        *   [3.1.3 Using apache2-mpm-worker and mod_fcgid](#Using_apache2-mpm-worker_and_mod_fcgid)
        *   [3.1.4 Test if PHP works](#Test_if_PHP_works)
    *   [3.2 HTTP2](#HTTP2)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Apache Status and Logs](#Apache_Status_and_Logs)
    *   [4.2 Error: PID file /run/httpd/httpd.pid not readable (yet?) after start](#Error:_PID_file_/run/httpd/httpd.pid_not_readable_(yet?)_after_start)
    *   [4.3 Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.](#Apache_is_running_a_threaded_MPM,_but_your_PHP_Module_is_not_compiled_to_be_threadsafe.)
    *   [4.4 AH00534: httpd: Configuration error: No MPM loaded.](#AH00534:_httpd:_Configuration_error:_No_MPM_loaded.)
    *   [4.5 AH00072: make_sock: could not bind to address](#AH00072:_make_sock:_could_not_bind_to_address)
    *   [4.6 Changing the max_execution_time in php.ini has no effect](#Changing_the_max_execution_time_in_php.ini_has_no_effect)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [apache](https://www.archlinux.org/packages/?name=apache) package.

## Configuration

Apache configuration files are located in `/etc/httpd/conf`. The main configuration file is `/etc/httpd/conf/httpd.conf`, which includes various other configuration files. The default configuration file should be fine for a simple setup. By default, it will serve the directory `/srv/http` to anyone who visits your website.

To start Apache, start `httpd.service` using [systemd](/index.php/Systemd#Using_units "Systemd").

Apache should now be running. Test by visiting [http://localhost/](http://localhost/) in a web browser. It should display a simple index page.

For optional further configuration, see the following sections.

### Advanced options

See the [full list of Apache configuration directives](https://httpd.apache.org/docs/trunk/mod/directives.html) and the [directive quick reference](https://httpd.apache.org/docs/trunk/mod/quickreference.html).

These options in `/etc/httpd/conf/httpd.conf` might be interesting for you:

```
User http

```

	For security reasons, as soon as Apache is started by the root user (directly or via startup scripts) it switches to this UID. The default user is *http*, which is created automatically during installation.

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

You must make sure that your home directory permissions are set properly so that Apache can get there. Your home directory and `~/public_html` must be executable for others ("rest of the world"):

```
$ chmod o+x ~
$ chmod o+x ~/public_html
$ chmod -R o+r ~/public_html

```

Restart `httpd.service` to apply any changes. See also [Umask#Set the mask value](/index.php/Umask#Set_the_mask_value "Umask").

### TLS

**Warning:** If you deploy [TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security "wikipedia:Transport Layer Security"), be sure to follow [weakdh.org's guide](https://weakdh.org/sysadmin.html) to prevent vulnerabilities. For more information see [Server-side TLS](/index.php/Server-side_TLS "Server-side TLS").

Firstly [obtain a certificate](/index.php/Obtain_a_certificate "Obtain a certificate").

In `/etc/httpd/conf/httpd.conf`, uncomment the following three lines:

```
LoadModule ssl_module modules/mod_ssl.so
LoadModule socache_shmcb_module modules/mod_socache_shmcb.so
Include conf/extra/httpd-ssl.conf

```

If using `certbot --apache`, the following line needs to be uncommented as well:

```
LoadModule rewrite_module modules/mod_rewrite.so

```

For TLS, you will need a key and certificate. If you own a public domain, you can use [Let's Encrypt](/index.php/Let%27s_Encrypt "Let's Encrypt") to obtain a certificate for free, otherwise follow [#Create a key and (self-signed) certificate](#Create_a_key_and_(self-signed)_certificate).

After obtaining a key and certificate, make sure the `SSLCertificateFile` and `SSLCertificateKeyFile` lines in `/etc/httpd/conf/extra/httpd-ssl.conf` point to the key and certificate. If a concatenated chain of CA certificates was also generated, add that filename against `SSLCertificateChainFile`.

Finally, restart `httpd.service` to apply any changes.

**Tip:** Mozilla has a useful [SSL/TLS article](https://wiki.mozilla.org/Security/Server_Side_TLS "mozillawiki:Security/Server Side TLS") as well as an [automated tool](https://mozilla.github.io/server-side-tls/ssl-config-generator/) to help create a more secure configuration.

#### Create a key and (self-signed) certificate

Create a private key and self-signed certificate. This is adequate for most installations that do not require a [CSR](https://en.wikipedia.org/wiki/Certificate_signing_request "wikipedia:Certificate signing request"):

```
# cd /etc/httpd/conf
# openssl req -new -x509 -nodes -newkey rsa:4096 -keyout server.key -out server.crt -days 1095
# chmod 400 server.key

```

**Note:** The -days switch is optional and RSA keysize can be as low as 2048 (default).

If you need to create a [CSR](https://en.wikipedia.org/wiki/Certificate_signing_request "wikipedia:Certificate signing request"), follow these keygen instructions instead of the above:

```
# cd /etc/httpd/conf
# openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:4096 -out server.key
# chmod 400 server.key
# openssl req -new -sha256 -key server.key -out server.csr
# openssl x509 -req -days 1095 -in server.csr -signkey server.key -out server.crt

```

**Note:** For more openssl options, read the [man page](https://www.openssl.org/docs/apps/openssl.html) or peruse openssl's [extensive documentation](https://www.openssl.org/docs/).

### Virtual hosts

**Note:** You will need to add a separate `<VirtualHost *:443>` section for virtual host SSL support. See [#Managing many virtual hosts](#Managing_many_virtual_hosts) for an example file.

If you want to have more than one host, uncomment the following line in `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/httpd-vhosts.conf

```

In `/etc/httpd/conf/extra/httpd-vhosts.conf` set your virtual hosts. The default file contains an elaborate example that should help you get started.

To test the virtual hosts on your local machine, add the virtual names to your `/etc/hosts` file:

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
<VirtualHost *:80>
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

<VirtualHost *:443>
    ServerAdmin webmaster@domainname1.dom
    DocumentRoot "/home/user/http/domainname1.dom"
    ServerName domainname1.dom:443
    ServerAlias domainname1.dom:443
    SSLEngine on
    SSLCertificateFile "/etc/httpd/conf/server.crt"
    SSLCertificateKeyFile "/etc/httpd/conf/server.key"
    ErrorLog "/var/log/httpd/domainname1.dom-error_log"
    CustomLog "/var/log/httpd/domainname1.dom-access_log" common

    <Directory "/home/user/http/domainname1.dom">
        Require all granted
    </Directory>
</VirtualHost>
```

## Extensions

### PHP

First install PHP as explained in on the [PHP](/index.php/PHP "PHP") page.

There are multiple methods to use PHP with Apache. [#Using libphp](#Using_libphp) is probably the easiest, but also the least scalable. libphp also requires you to change the mpm module, which may cause problems with other extensions (e.g. it is not compatible with [#HTTP2](#HTTP2)).

#### Using libphp

[Install](/index.php/Install "Install") the [php-apache](https://www.archlinux.org/packages/?name=php-apache) package.

In `/etc/httpd/conf/httpd.conf`, comment the line:

```
#LoadModule mpm_event_module modules/mod_mpm_event.so

```

and uncomment the line:

```
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

**Note:** The above is required, because `libphp7.so` included with [php-apache](https://www.archlinux.org/packages/?name=php-apache) does not work with `mod_mpm_event`, but will only work `mod_mpm_prefork` instead. ([FS#39218](https://bugs.archlinux.org/task/39218))

Otherwise you will get the following error:

```
Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.  You need to recompile PHP.
AH00013: Pre-configuration failed
httpd.service: control process exited, code=exited status=1
```
As an alternative, you can use `mod_proxy_fcgi` (see [#Using php-fpm and mod_proxy_fcgi](#Using_php-fpm_and_mod_proxy_fcgi) below).

To enable PHP, add these lines to `/etc/httpd/conf/httpd.conf`:

*   Place this at the end of the `LoadModule` list:

```
LoadModule php7_module modules/libphp7.so
AddHandler php7-script .php

```

*   Place this at the end of the `Include` list:

```
Include conf/extra/php7_module.conf

```

Restart `httpd.service` using [systemd](/index.php/Systemd#Using_units "Systemd").

#### Using php-fpm and mod_proxy_fcgi

**Note:** Unlike the widespread setup with ProxyPass, the proxy configuration with SetHandler respects other Apache directives like DirectoryIndex. This ensures a better compatibility with software designed for libphp7, mod_fastcgi and mod_fcgid. If you still want to try ProxyPass, experiment with a line like this: `ProxyPassMatch ^/(.*\.php(/.*)?)$ unix:/run/php-fpm/php-fpm.sock|fcgi://localhost/srv/http/$1` 

[Install](/index.php/Install "Install") the [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) package.

Enable proxy modules:

 `/etc/httpd/conf/httpd.conf` 
```
LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so

```

Create `/etc/httpd/conf/extra/php-fpm.conf` with the following content:

```
DirectoryIndex index.php index.html
<FilesMatch \.php$>
    SetHandler "proxy:unix:/run/php-fpm/php-fpm.sock|fcgi://localhost/"
</FilesMatch>

```

And include it at the bottom of `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/php-fpm.conf

```

**Note:** The pipe between `sock` and `fcgi` is not allowed to be surrounded by a space! `localhost` can be replaced by any string. More [here](https://httpd.apache.org/docs/2.4/mod/mod_proxy_fcgi.html)

You can configure PHP-FPM in `/etc/php/php-fpm.d/www.conf`, but the default setup should work fine.

Start and enable `php-fpm.service`. [Restart](/index.php/Restart "Restart") `httpd.service`.

#### Using apache2-mpm-worker and mod_fcgid

[Install](/index.php/Install "Install") the [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid) and [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) packages.

Create the needed directory and symlink it for the PHP wrapper:

```
# mkdir /srv/http/fcgid-bin
# ln -s /usr/bin/php-cgi /srv/http/fcgid-bin/php-fcgid-wrapper

```

Create `/etc/httpd/conf/extra/php-fcgid.conf` with the following content:

 `/etc/httpd/conf/extra/php-fcgid.conf` 
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

Edit `/etc/httpd/conf/httpd.conf`, enabling the actions module:

```
LoadModule actions_module modules/mod_actions.so

```

And add the following lines:

```
LoadModule fcgid_module modules/mod_fcgid.so
Include conf/extra/httpd-mpm.conf
Include conf/extra/php-fcgid.conf

```

[Restart](/index.php/Restart "Restart") `httpd.service`.

#### Test if PHP works

To test whether PHP was correctly configured: create a file called `test.php` in your Apache `DocumentRoot` directory (e.g. `/srv/http/` or `~/public_html`) with the following contents:

```
<?php phpinfo(); ?>

```

To see if it works go to: [http://localhost/test.php](http://localhost/test.php) or [http://localhost/~myname/test.php](http://localhost/~myname/test.php)

### HTTP2

To enable HTTP/2 support, uncomment the following line in `httpd.conf`:

```
LoadModule http2_module modules/mod_http2.so

```

And add the following line:

```
Protocols h2 http/1.1

```

For more information, see the [mod_http2](https://httpd.apache.org/docs/2.4/mod/mod_http2.html) documentation.

## Troubleshooting

### Apache Status and Logs

See the status of the Apache daemon with [systemctl](/index.php/Systemctl "Systemctl").

Apache logs can be found in `/var/log/httpd/`

### Error: PID file /run/httpd/httpd.pid not readable (yet?) after start

Comment out the `unique_id_module` line in `httpd.conf`: `#LoadModule unique_id_module modules/mod_unique_id.so`

### Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.

If when loading `php7_module` the `httpd.service` fails, and you get an error like this in the journal:

```
Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.  You need to recompile PHP.

```

you need to replace `mpm_event_module` with `mpm_prefork_module`:

 `/etc/httpd/conf/httpd.conf` 
```
~~LoadModule mpm_event_module modules/mod_mpm_event.so~~
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

and restart `httpd.service`.

### AH00534: httpd: Configuration error: No MPM loaded.

You might encounter this error after a recent upgrade. This is only the result of a recent change in `httpd.conf` that you might not have reproduced in your local configuration. To fix it, uncomment the following line.

 `/etc/httpd/conf/httpd.conf` 
```
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

Also check [the above](#Apache_is_running_a_threaded_MPM.2C_but_your_PHP_Module_is_not_compiled_to_be_threadsafe.) if more errors occur afterwards.

### AH00072: make_sock: could not bind to address

This can be caused by multiple things. Most common issue being that something is already listening on a given port, check via netstat that this is not happening:

```
# netstat -lnp | grep -e :80 -e :443

```

If you get any output, stop the given service that's taking up the port or kill the runaway process that is causing the port to be bound, and try again.

Another issue could be that Apache is not starting as root for some reason - try starting it manually and see if you still get the AH0072 error.

```
# httpd -k start

```

Finally, you can also have an error with your config and you are listening twice on the given port. Following is an example of a bad config that will trigger this issue:

```
Listen 0.0.0.0:80
Listen [::]:80

```

### Changing the max_execution_time in php.ini has no effect

If you changed the `max_execution_time` in `php.ini` to a value greater than 30 (seconds), you may still get a `503 Service Unavailable` response from Apache after 30 seconds. To solve this, add a `ProxyTimeout` directive to your http configuration right before the `<FilesMatch \.php$>` block:

 `/etc/httpd/conf/httpd.conf` 
```
ProxyTimeout 300

```

and restart `httpd.service`.

## See also

*   [Apache Official Website](https://www.apache.org/)
*   [Apache documentation](https://httpd.apache.org/docs/2.4/)
*   [Apache wiki](https://wiki.apache.org/httpd/)
*   [Apache documentation - Security Tips](https://httpd.apache.org/docs/current/misc/security_tips.html)
*   [Apache Wiki - Troubleshooting](https://wiki.apache.org/httpd/CommonMisconfigurations)
*   [Apache](https://wiki.debian.org/Apache "debian:Apache") on wiki.debian.org