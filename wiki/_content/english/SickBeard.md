[Sick Beard](http://sickbeard.com) is a PVR for newsgroup users (with limited torrent support). It watches for new episodes of your favorite shows and when they are posted it downloads them, sorts and renames them, and optionally generates metadata for them. It currently supports NZBs.org, NZBMatrix, NZBs'R'Us, Newzbin, Womble's Index, NZB.su, TVTorrents and EZRSS and retrieves show information from theTVDB.com and TVRage.com.

## Installation

[Install](/index.php/Install "Install") the [sickbeard](https://aur.archlinux.org/packages/sickbeard/) package.

[Start/enable](/index.php/Start/enable "Start/enable") `sickbeard.service`.

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