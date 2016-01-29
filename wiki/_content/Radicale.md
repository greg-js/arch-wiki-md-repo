# Radicale

Related articles

*   [DAViCal](/index.php/DAViCal "DAViCal")
*   [Kcaldav](/index.php/Kcaldav "Kcaldav")
*   [AgenDAV](/index.php/AgenDAV "AgenDAV")

Radicale is a server designed to support the CalDav and CardDav protocols. It is based on Python 2.6-3.5.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Integration](#Integration)
*   [3 Client support](#Client_support)

## Installation

[Install](/index.php/Install "Install") the [radicale](https://aur.archlinux.org/packages/radicale/)<sup><small>AUR</small></sup> package.

## Configuration

The main configuration file is located at `/etc/radicale/config`.

Many of the configuration options can be changed by command-line:

```
$radicale --help

```

### Integration

Radicale can be integrated with HTTP webservers like Apache which support the mod_wgsi interface. This causes several options for the configuration of Radicale to be ignored, including: hosts, daemon, pid, ssl, certificate, key, protocol and ciphers keys in the [server] section of the config. Install the radicale module in the python path and write the .wgsi file (to document root).

```
# import radicale
# radicale.log.start()
# application = radicale.Application()
```

The next step is to set up a virtual host for radicale. An example:

```
<VirtualHost *:80>
    ServerName cal.yourdomain.org

    WSGIDaemonProcess radicale user=www-data group=www-data threads=1
    WSGIScriptAlias / /var/www/radicale.wsgi

    <Directory /var/www>
        WSGIProcessGroup radicale
        WSGIApplicationGroup %{GLOBAL}
        AllowOverride None
        Order allow,deny
        allow from all
    </Directory>
</VirtualHost>
```

## Client support

Since it uses the CalDav and CardDav protocals, it should support most clients. Currently, the officially supported list is this: Mozilla Lightning GNOME Evolution KDE KOrganizer aCal, ContactSync, CalendarSync, CalDAV-Sync CardDAV-Sync and DAVdroid for Google Android InfCloud, CalDavZAP, CardDavMATE Apple iOS Mac OSX Calendar/Contacts syncEvolution

Retrieved from "[https://wiki.archlinux.org/index.php?title=Radicale&oldid=409928](https://wiki.archlinux.org/index.php?title=Radicale&oldid=409928)"