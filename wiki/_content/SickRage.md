# SickRage

[Sick Rage](https://www.sickrage.tv/) is an automatic video library manager for TV Shows. It watches for new episodes of your favorite shows, and when they are posted it does its magic.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Running as a systemd service](#Running_as_a_systemd_service)
    *   [1.2 Password protecting the webui](#Password_protecting_the_webui)
    *   [1.3 Compatible torrent clients](#Compatible_torrent_clients)
    *   [1.4 First time usage](#First_time_usage)

## Installation

Install [sickrage](https://aur.archlinux.org/packages/sickrage/)<sup><small>AUR</small></sup> or [sickrage-git](https://aur.archlinux.org/packages/sickrage-git/)<sup><small>AUR</small></sup>. Or install [sickrage2-git](https://aur.archlinux.org/packages/sickrage2-git/)<sup><small>AUR</small></sup>, a fork of sickrage. It contains the application and a systemd service file.

### Running as a systemd service

Sickrage can automatically run on start-up:

```
 # systemctl enable sickrage
 # systemctl start sickrage

```

### Password protecting the webui

By default, the SickRage webui running on port 8081 is not protected by a password. To set a username and password, edit the SickRage config file at `/opt/sickrage/config.ini` and change the `web_username` and `web_password` settings:

 `/opt/sickrage/config.ini` 

```
 web_username =
 web_password =
```

### Compatible torrent clients

**For some you will need to enable the web-interface to work**

*   "Black Hole" (saves .torrent files to a directory)
*   uTorrent
*   [Transmission](/index.php/Transmission "Transmission")
*   [Deluge](/index.php/Deluge "Deluge")
*   Synologie DS
*   [rtorrent](https://www.archlinux.org/packages/?name=rtorrent)
*   [qBittorent](https://aur.archlinux.org/packages/qBittorent/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): package not found]</sup>

### First time usage

Sick Rage is a web-application that can be accessed on [http://localhost:8081](http://localhost:8081), when Sick Rage reports that it doesn't know it's version, just hit the update button. It will check for updates, restart itself and set it's current version. The settings are pretty straightforward. If you already have a storage of series, just point Sick Rage to it and it will analyze it and try to add your already downloaded series to it's own list.

Retrieved from "[https://wiki.archlinux.org/index.php?title=SickRage&oldid=414563](https://wiki.archlinux.org/index.php?title=SickRage&oldid=414563)"