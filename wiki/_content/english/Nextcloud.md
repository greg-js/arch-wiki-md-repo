From [Wikipedia](https://en.wikipedia.org/wiki/ownCloud "wikipedia:ownCloud"): Nextcloud is functionally very similar to the widely used Dropbox, with the primary functional difference being that Nextcloud is free and open-source, and thereby allowing anyone to install and operate it without charge on a private server. In contrary to proprietary services like Dropbox, the open architecture allows adding additional functionality to the server in form of so-called applications.Nextcloud is an actively maintained fork of ownCloud.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Required Packages](#Required_Packages)
    *   [1.2 Optional Packages](#Optional_Packages)
*   [2 PHP Configuration](#PHP_Configuration)
*   [3 Setup mariadb and nextcloud DB](#Setup_mariadb_and_nextcloud_DB)
*   [4 Setup Apache](#Setup_Apache)
*   [5 Switch to Cron from AJAX](#Switch_to_Cron_from_AJAX)
*   [6 Enable memcache](#Enable_memcache)
*   [7 (Optional) SSL Setup and its hardening plus SSL hardening](#.28Optional.29_SSL_Setup_and_its_hardening_plus_SSL_hardening)
    *   [7.1 Enable SSL with a self signed certificate](#Enable_SSL_with_a_self_signed_certificate)
    *   [7.2 SSL hardening](#SSL_hardening)

## Installation

### Required Packages

[Install](/index.php/Install "Install") the [apache](https://www.archlinux.org/packages/?name=apache) [php](https://www.archlinux.org/packages/?name=php) [php-apache](https://www.archlinux.org/packages/?name=php-apache) [mariadb](https://www.archlinux.org/packages/?name=mariadb) packages from the [official repositories](/index.php/Official_repositories "Official repositories").

[Install](/index.php/Install "Install") the [nextcloud](https://aur.archlinux.org/packages/nextcloud/) package from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

[Install](/index.php/Install "Install") the required [PHP](/index.php/PHP "PHP") modules packages: [php-gd](https://www.archlinux.org/packages/?name=php-gd) [php-intl](https://www.archlinux.org/packages/?name=php-intl) [php-mcrypt](https://www.archlinux.org/packages/?name=php-mcrypt) from the [official repositories](/index.php/Official_repositories "Official repositories").

[Install](/index.php/Install "Install") from the [official repositories](/index.php/Official_repositories "Official repositories") the [APCu](/index.php/PHP#APCu "PHP") PHP module for memory caching: [php-apcu](https://www.archlinux.org/packages/?name=php-apcu).

### Optional Packages

For file preview generation [Install](/index.php/Install "Install") the following packages:

[ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) and either [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) or [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh) from the [official repositories](/index.php/Official_repositories "Official repositories").

[php-imagick](https://aur.archlinux.org/packages/php-imagick/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

[nextcloud-client](https://aur.archlinux.org/packages/nextcloud-client/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") for the Desktop Client

## PHP Configuration

Edit `/etc/php/php.ini` and uncomment the following required modules:

```
gd.so
iconv.so
xmlrpc.so
zip.so

```

Also uncomment the following required modules for [mariadb](/index.php/Mariadb "Mariadb"):

```
extension=pdo_mysql.so

```

Uncomment the following recommended [PHP](/index.php/PHP "PHP") modules:

```
bz2.so
curl.so
intl.so
mcrypt.so

```

**Note:** If you are installing this on a 32-bit based OS (ie the current Arch Linux for ARM ([https://archlinuxarm.org/](https://archlinuxarm.org/)) uses a 32-bit OS for Raspberry Pi), then do not configure open_basedir - refer to the Nextcloud manual: [https://docs.nextcloud.com/server/10/admin_manual/configuration_files/big_file_upload_configuration.html#configuring-php](https://docs.nextcloud.com/server/10/admin_manual/configuration_files/big_file_upload_configuration.html#configuring-php)

Add the following to `open_basedir`:

```
/usr/share/webapps/nextcloud:/dev/urandom

```

**Note:** You may also need to add the `/tmp` directory in `open_basedir` if Apache only displays a blank page. Check `/var/log/httpd/error_log` file to confirm this problem

## Setup mariadb and nextcloud DB

Configure [mariadb](/index.php/Mariadb "Mariadb"):

```
# mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql

```

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `mariadb.service`.

Secure [mariadb](/index.php/Mariadb "Mariadb"):

```
# mysql_secure_installation

```

Create `nextcloud` database:

```
$ mysql -u root -p

```

At the prompt, insert the following lines (make sure to enter them separately).

**Note:** Change `*username*` and `*password*` to your specific values and note them down as you will need them later.

```
CREATE DATABASE IF NOT EXISTS nextcloud;
CREATE USER ‘*username*’@’localhost’ IDENTIFIED BY ‘*password*’;
GRANT ALL PRIVILEGES ON nextcloud.* TO ‘*username*’@’localhost’ IDENTIFIED BY ‘*password*’;
quit

```

## Setup Apache

Copy Nextcloud’s [Apache](/index.php/Apache "Apache") configuration file to [Apache](/index.php/Apache "Apache") configuration directory:

```
# cp /etc/webapps/nextcloud/apache.example.conf /etc/httpd/conf/extra/nextcloud.conf

```

Edit `/etc/httpd/conf/httpd.conf` and:

Comment the line:

```
#LoadModule mpm_event_module modules/mod_mpm_event.so

```

Uncomment the line:

```
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

After `LoadModule dir_module modules/mod_dir.so`, place the following module:

```
LoadModule php7_module modules/libphp7.so

```

At the end of the `Include` list place the following line:

```
Include conf/extra/php7_module.conf

```

At the end of the `LoadModule` list add the following line:

```
AddHandler php7-script php

```

At the bottom of `/etc/httpd/conf/httpd.conf` add the following line:

```
Include conf/extra/nextcloud.conf

```

Enable (uncomment) the following modules:

```
LoadModule rewrite_module modules/mod_rewrite.so
LoadModule headers_module modules/mod_headers.so
LoadModule env_module modules/mod_env.so
LoadModule dir_module modules/mod_dir.so
LoadModule mime_module modules/mod_mime.so

```

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the [apache](https://www.archlinux.org/packages/?name=apache) service `httpd`

## Switch to Cron from AJAX

Nextcloud requires scheduled execution of some tasks, and by default it archives this by using AJAX, however AJAX is the least reliable method, and it is recommended to use [Cron](/index.php/Cron "Cron") instead.

To do so, first install [cronie](https://www.archlinux.org/packages/?name=cronie):

```
# pacman -S cronie

```

Then create a job for `http` user:

```
# crontab -u http -e

```

This would open editor, paste this:

```
*/15  *  *  *  * php -f /usr/share/webapps/nextcloud/cron.php

```

Save the file and exit. Now you should [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `cronie.service`.

You can verify that everything is set by running

```
# crontab -u http -l

```

Finally, set Cron option in Nextcloud settings to Cron.

## Enable memcache

Enable memcache by uncommenting the following line in `/etc/php/conf.d/apcu.ini`:

```
extension=apcu.so

```

Log onto Nextcloud and set it up by pointing your browser to: `[http://localhost/nextcloud](http://localhost/nextcloud)`. Follow the on screen instructions to setup Nextcloud

**Note:** Remember to use the DB username/password you set up above

After Nextcloud is set up, add the following line to `/usr/share/webapps/nextcloud/config/config.php`:

```
'memcache.local' => '\OC\Memcache\APCu',

```

[Restart](/index.php/Restart "Restart") the [apache](https://www.archlinux.org/packages/?name=apache) `httpd` service.

## (Optional) SSL Setup and its hardening plus SSL hardening

**Tip:** See the [Let's Encrypt](/index.php/Let%27s_Encrypt "Let's Encrypt") for details about free, automated ssl certificates.

### Enable SSL with a self signed certificate

Edit `/etc/httpd/conf/httpd.conf` and uncomment the following lines:

```
LoadModule ssl_module modules/mod_ssl.so
LoadModule socache_shmcb_module modules/mod_socache_shmcb.so
Include conf/extra/httpd-ssl.conf

```

Still while in `/etc/httpd/conf/httpd.conf` add port `443` to your `Listen` ports:

```
Listen 443

```

Create the certificate issuing the following commands:

```
# cd /etc/httpd/conf
# openssl req -new -x509 -nodes -newkey rsa:4096 -keyout server.key -out server.crt -days 1095
# chmod 400 server.key
```

### SSL hardening

Edit `/etc/httpd/conf/extra/httpd-ssl.conf` and under the `VirtualHost:443` section add the following section:

```
<IfModule mod_headers.c>
Header always set Strict-Transport-Security "max-age=15768000; includeSubDomains; preload"
</IfModule>

```

[Restart](/index.php/Restart "Restart") the [apache](https://www.archlinux.org/packages/?name=apache) `httpd` service.