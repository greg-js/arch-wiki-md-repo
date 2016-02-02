# SickBeard

[Sick Beard](http://sickbeard.com) is a PVR for newsgroup users (with limited torrent support). It watches for new episodes of your favorite shows and when they are posted it downloads them, sorts and renames them, and optionally generates metadata for them. It currently supports NZBs.org, NZBMatrix, NZBs'R'Us, Newzbin, Womble's Index, NZB.su, TVTorrents and EZRSS and retrieves show information from theTVDB.com and TVRage.com.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Running as a systemd service](#Running_as_a_systemd_service)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Daemon won't start](#Daemon_won.27t_start)

## Installation

Install [sickbeard](https://aur.archlinux.org/packages/sickbeard/)<sup><small>AUR</small></sup>, available in the [AUR](/index.php/AUR "AUR"). It contains the application and a systemd service file.

### Running as a systemd service

You can run sickbeard automatically from boot using the systemd service.

```
 # systemctl enable sickbeard

```

## Troubleshooting

### Daemon won't start

Sickbeard's systemd script attaches the app to `/run/sickbeard.pid`. If starting sickbeard fails and journalctl states:

```
Unable to write PID file: No such file or directory [2]

```

you can:

*   reboot
*   run: `systemd-tmpfiles --create`

This will create the directory, based on `/usr/lib/tmpfiles.d/sickbeard.conf` which the sickbeard package installs.

You can read more about this problem [in this forum thread](https://bbs.archlinux.org/viewtopic.php?id=158625).

Retrieved from "[https://wiki.archlinux.org/index.php?title=SickBeard&oldid=353244](https://wiki.archlinux.org/index.php?title=SickBeard&oldid=353244)"