Related articles

*   [DAViCal](/index.php/DAViCal "DAViCal")
*   [Kcaldav](/index.php/Kcaldav "Kcaldav")
*   [AgenDAV](/index.php/AgenDAV "AgenDAV")

[Radicale](http://radicale.org/) is a server designed to support the CalDav and CardDav protocols. It requires at least Python 3.3.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Integration](#Integration)
*   [3 Client support](#Client_support)
*   [4 See also](#See_also)

## Installation

**Warning:** Radicale got a major release change. You need to export old version 1.x calendars *before* you install version 2.x. Please, [read](http://radicale.org/1to2/).

[Install](/index.php/Install "Install") the [radicale](https://www.archlinux.org/packages/?name=radicale) package.

## Configuration

The main configuration file is located at `/etc/radicale/config`.

Many of the configuration options can be changed on the command-line:

```
$ radicale --help

```

### Integration

Radicale can be integrated with HTTP webservers like [Apache](/index.php/Apache "Apache") which support the WSGI interface. Install the [mod_wsgi](https://www.archlinux.org/packages/?name=mod_wsgi) Apache module.

This causes several options for the configuration of Radicale to be ignored, including: hosts, daemon, pid, ssl, certificate, key, protocol and ciphers keys in the [server] section of the config. Install the radicale module in the python path and write the .wsgi file (to document root).

```
from radicale import application

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

If you installed the Radicale package via pacman, you must also change the ownership of this directory:

```
# chown http:http /var/lib/radicale

```

Otherwise, the wsgi script will fail on its first run.

## Client support

Since it uses the CalDav and CardDav protocols, it should support most clients. Currently, the officially supported list is this:

*   [Thunderbird Lightning extension](/index.php/Thunderbird#Extensions "Thunderbird")
*   [GNOME/Evolution](/index.php/GNOME/Evolution "GNOME/Evolution")
*   KOrganizer [korganizer](https://www.archlinux.org/packages/?name=korganizer)
*   InfCloud [infcloud](https://aur.archlinux.org/packages/infcloud/), CalDavZAP [caldavzap](https://aur.archlinux.org/packages/caldavzap/), CardDavMATE [carddavmate](https://aur.archlinux.org/packages/carddavmate/)
*   syncEvolution [syncevolution](https://aur.archlinux.org/packages/syncevolution/)
*   aCal, ContactSync, CalendarSync, CalDAV-Sync CardDAV-Sync and DAVx⁵ for Google Android
*   Apple iOS
*   Mac OSX Calendar/Contacts

## See also

*   [Project Website radicale.org](http://radicale.org/)