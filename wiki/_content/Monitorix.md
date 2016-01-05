# Monitorix

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Anything-sync-daemon](/index.php/Anything-sync-daemon "Anything-sync-daemon")
*   [lm_sensors](/index.php/Lm_sensors "Lm sensors")
*   [hddtemp](/index.php/Hddtemp "Hddtemp")

[Monitorix](http://www.monitorix.org/) is an open source, lightweight system monitoring tool designed to monitor as many services and system resources as possible. It has been created to be used under production UNIX/Linux servers, but due to its simplicity and small size many use it on embedded devices as well.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Start and viewing data](#Start_and_viewing_data)
*   [4 Configure an external webserver](#Configure_an_external_webserver)
    *   [4.1 Lighttpd](#Lighttpd)
    *   [4.2 Apache](#Apache)
    *   [4.3 Nginx](#Nginx)
*   [5 Using tmpfs to Store RRD databases](#Using_tmpfs_to_Store_RRD_databases)

## Installation

[Install](/index.php/Install "Install") the package [monitorix](https://aur.archlinux.org/packages/monitorix/)<sup><small>AUR</small></sup>.

**Note:** Without a compatible font already installed, the Monitorix graphs will not contain any text. If this happens, install the [terminus-font](https://www.archlinux.org/packages/?name=terminus-font).

## Configuration

Edit `/etc/monitorix/monitorix.conf` to match graphing options and system-specific variables. For a complete list of options and features, see the [man page](http://www.monitorix.org/documentation.html).

Most of the user settings are self explanatory based on the commented text within the configuration file itself.

Monitorix comes with a light, built-in webserver; via the dependency [perl-http-server-simple](https://www.archlinux.org/packages/?name=perl-http-server-simple). It is, however, disabled by default. To use it, change the configuration option as follows:

 `/etc/monitorix/monitorix.conf` 

```
....
<httpd_builtin>

enabled = y
....
```

See the configuration file for the other related options, for example [accesss restrictions](http://www.monitorix.org/documentation.html#3), or [#Configure an external webserver](#Configure_an_external_webserver).

## Start and viewing data

[Start](/index.php/Start "Start") `monitorix.service` and [enable](/index.php/Enable "Enable") it to run at boot like any other systemd service.

To view system stats, using the perl-http-server, simply point a browser to http://localhost:8080/monitorix to see the data.

**Tip:** If it is the first time running Monitorix, it will take several minutes before data are available to be displayed graphically; so be patient.

## Configure an external webserver

### Lighttpd

[lighttpd](https://www.archlinux.org/packages/?name=lighttpd) is another option.

By default, cgi support is not enabled in lighttpd. To enable it and to assign perl to process _.cgi_ files, add the following two lines to `/etc/lighttpd/lighttpd.conf`:

```
server.modules		= ( "mod_cgi" )
cgi.assign		= ( ".cgi" => "/usr/bin/perl" )

```

### Apache

[apache](https://www.archlinux.org/packages/?name=apache) is yet another option.

### Nginx

[nginx](https://www.archlinux.org/packages/?name=nginx) can be used as a reverse proxy/webserver by adding the following server block the nginx config:

```
server {
    listen       80;
    server_name  your.domain.com;

    location / {
       proxy_pass http://127.0.0.1:8080/;
       proxy_buffering off;
    }

    location ~ ^/monitorix/(.+\.png)$ {
        alias /srv/http/monitorix/$1;
    }
}

```

Also add `url_prefix_proxy = http://your.domain.com` to `/etc/monitorix/monitorix.conf`.

## Using tmpfs to Store RRD databases

[Anything-sync-daemon](https://aur.archlinux.org/packages/Anything-sync-daemon/)<sup><small>AUR</small></sup> is a package which provides a pseudo-daemon that makes use of tmpfs to store RRD Databases for Monitorix. Doing so will greatly reduce hdd reads/writes.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Monitorix&oldid=414406](https://wiki.archlinux.org/index.php?title=Monitorix&oldid=414406)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Status monitoring and notification](/index.php/Category:Status_monitoring_and_notification "Category:Status monitoring and notification")