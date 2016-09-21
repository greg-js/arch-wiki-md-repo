Radicale is a server designed to support the CalDav and CardDav protocols. It is based on Python 2.6-3.5.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Integration](#Integration)
*   [3 Client support](#Client_support)

## Installation

[Install](/index.php/Install "Install") the [radicale](https://aur.archlinux.org/packages/radicale/) package.

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

    WSGIDaemonProcess radicale user=http group=http threads=1
    WSGIScriptAlias / /srv/http/radicale.wsgi

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

Since it uses the CalDav and CardDav protocols, it should support most clients. Currently, the officially supported list is this:

*   [Thunderbird#Lightning - Calendar](/index.php/Thunderbird#Lightning_-_Calendar "Thunderbird")
*   [GNOME/Evolution](/index.php/GNOME/Evolution "GNOME/Evolution")
*   KOrganizer [korganizer](https://www.archlinux.org/packages/?name=korganizer)
*   InfCloud [infcloud](https://aur.archlinux.org/packages/infcloud/), CalDavZAP [caldavzap](https://aur.archlinux.org/packages/caldavzap/), CardDavMATE [carddavmate](https://aur.archlinux.org/packages/carddavmate/)
*   syncEvolution [syncevolution](https://aur.archlinux.org/packages/syncevolution/)
*   aCal, ContactSync, CalendarSync, CalDAV-Sync CardDAV-Sync and DAVdroid for Google Android
*   Apple iOS
*   Mac OSX Calendar/Contacts