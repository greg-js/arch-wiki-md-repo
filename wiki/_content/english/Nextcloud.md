From [Wikipedia](https://en.wikipedia.org/wiki/ownCloud "wikipedia:ownCloud"): Nextcloud is functionally very similar to the widely used Dropbox, with the primary functional difference being that Nextcloud is free and open-source, and thereby allowing anyone to install and operate it without charge on a private server. In contrary to proprietary services like Dropbox, the open architecture allows adding additional functionality to the server in form of so-called applications.Nextcloud is an actively maintained fork of ownCloud.

## Contents

*   [1 Prerequisites](#Prerequisites)
*   [2 Installation](#Installation)
    *   [2.1 Database support](#Database_support)
        *   [2.1.1 MariaDB](#MariaDB)
    *   [2.2 Optional Packages](#Optional_Packages)
    *   [2.3 Setup Apache](#Setup_Apache)
    *   [2.4 Switch to Cron from AJAX](#Switch_to_Cron_from_AJAX)
    *   [2.5 Enable memcache](#Enable_memcache)
    *   [2.6 (Optional) SSL Setup and its hardening plus SSL hardening](#.28Optional.29_SSL_Setup_and_its_hardening_plus_SSL_hardening)
        *   [2.6.1 Enable SSL with a self signed certificate](#Enable_SSL_with_a_self_signed_certificate)
    *   [2.7 SSL hardening](#SSL_hardening)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Collabora Online Office integration](#Collabora_Online_Office_integration)

## Prerequisites

*NextCloud* needs a [web server](/index.php/Category:Web_server "Category:Web server"), [PHP](/index.php/PHP "PHP") and a [database](/index.php/Category:Database_management_systems "Category:Database management systems"). For instance, a classic [LAMP stack](/index.php/LAMP "LAMP") should work fine and is the [recommended configuration](https://docs.nextcloud.com/server/11/admin_manual/installation/system_requirements.html).

## Installation

[Install](/index.php/Install "Install") the [nextcloud](https://aur.archlinux.org/packages/nextcloud/) package.

[Install](/index.php/Install "Install") the required [PHP](/index.php/PHP "PHP") modules packages: [php-gd](https://www.archlinux.org/packages/?name=php-gd) [php-intl](https://www.archlinux.org/packages/?name=php-intl) [php-mcrypt](https://www.archlinux.org/packages/?name=php-mcrypt), and uncomment the following [required extensions](https://docs.nextcloud.com/server/9/admin_manual/installation/source_installation.html#prerequisites-label) in `/etc/php/php.ini`:

```
bz2.so
curl.so
gd.so
iconv.so
xmlrpc.so
zip.so

```

**Note:** If you are installing this on a 32-bit based OS (ie the current Arch Linux for ARM ([https://archlinuxarm.org/](https://archlinuxarm.org/)) uses a 32-bit OS for Raspberry Pi), then do not configure open_basedir - refer to the Nextcloud manual: [https://docs.nextcloud.com/server/11/admin_manual/configuration_files/big_file_upload_configuration.html#configuring-php](https://docs.nextcloud.com/server/11/admin_manual/configuration_files/big_file_upload_configuration.html#configuring-php)

Add the following to `open_basedir`:

```
/usr/share/webapps/nextcloud:/dev/urandom

```

**Note:** You may also need to add the `/tmp` directory in `open_basedir` if Apache only displays a blank page. Check `/var/log/httpd/error_log` file to confirm this problem

Optional enable [APCu](/index.php/PHP#APCu "PHP") PHP module for memory caching.

### Database support

Depending on which database backend you are going to use, uncomment the following extensions in `/etc/php/php.ini`:

*   For [MySQL](/index.php/MySQL "MySQL"), uncomment `pdo_mysql.so`.
*   For [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), uncomment `pdo_pgsql.so` and `pgsql.so`, and install [php-pgsql](https://www.archlinux.org/packages/?name=php-pgsql).
*   For [SQLite](/index.php/SQLite "SQLite"), uncomment `pdo_sqlite.so` and `sqlite3.so`, and install [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite).

#### MariaDB

Create `nextcloud` database:

```
$ mysql -u root -p

```

At the prompt, insert the following lines (make sure to enter them separately):

```
CREATE DATABASE IF NOT EXISTS nextcloud;
CREATE USER ‘*username*’@’localhost’ IDENTIFIED BY ‘*password*’;
GRANT ALL PRIVILEGES ON nextcloud.* TO ‘*username*’@’localhost’ IDENTIFIED BY ‘*password*’;
FLUSH PRIVILEGES;
quit

```

### Optional Packages

For file preview generation [Install](/index.php/Install "Install") the following packages:

[ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) and either [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) or [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh) from the [official repositories](/index.php/Official_repositories "Official repositories").

[php-imagick](https://aur.archlinux.org/packages/php-imagick/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

[nextcloud-client](https://aur.archlinux.org/packages/nextcloud-client/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") for the Desktop Client

### Setup Apache

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

### Switch to Cron from AJAX

Nextcloud requires scheduled execution of some tasks, and by default it archives this by using AJAX, however AJAX is the least reliable method, and it is recommended to use [Cron](/index.php/Cron "Cron") instead.

To do so, first install the [cronie](https://www.archlinux.org/packages/?name=cronie) package.

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

### Enable memcache

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

### (Optional) SSL Setup and its hardening plus SSL hardening

**Tip:** See the [Let's Encrypt](/index.php/Let%27s_Encrypt "Let's Encrypt") for details about free, automated ssl certificates.

#### Enable SSL with a self signed certificate

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

## Tips and tricks

### Collabora Online Office integration

Install [nextcloud-app-collabora-online](https://aur.archlinux.org/packages/nextcloud-app-collabora-online/) from the [AUR](/index.php/AUR "AUR"). Add following reverse proxy settings to your nextcloud domain config, in this case for [Nginx](/index.php/Nginx "Nginx"):

```
# static files
location ^~ /loleaflet {
 proxy_pass [https://localhost:9980](https://localhost:9980);
 proxy_set_header Host $http_host;
}
# WOPI discovery URL
location ^~ /hosting/discovery {
 proxy_pass [https://localhost:9980](https://localhost:9980);
 proxy_set_header Host $http_host;
}
# websockets, download, presentation and image upload
location ^~ /lool {
 proxy_pass [https://localhost:9980](https://localhost:9980);
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection "upgrade";
 proxy_set_header Host $http_host;
}

```

There's also a [setup instruction](https://nextcloud.com/collaboraonline/) for [Apache](/index.php/Apache "Apache"). Assuming you already have the docker deamon up and running, you can now pull the latest docker image for Collabora Online. Adjust the second command with the domain name of your Nextcloud server.

```
docker pull collabora/code
docker run -t -d -p 127.0.0.1:9980:9980 -e 'domain=cloud\\.nextcloud\\.com' --restart always --cap-add MKNOD collabora/code

```

When updating the docker image you can run the same commands, but before that kill all running processes of the old image:

```
docker ps
docker stop CONTAINER_ID
docker rm CONTAINER_ID

```

Now you can enable the Collabora Online app in your Nextcloud instance. In the last step, you have to configure your domain in the administrator settings regarding the Collabora Online app.