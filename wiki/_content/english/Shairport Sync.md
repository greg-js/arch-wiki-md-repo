[Shairport Sync](https://github.com/mikebrady/shairport-sync) is an [w:AirPlay](https://en.wikipedia.org/wiki/AirPlay "w:AirPlay") audio player — it plays audio streamed from iTunes, iOS devices and third-party AirPlay sources such as ForkedDaapd and others. Audio played by a Shairport Sync-powered device stays synchronised with the source and hence with similar devices playing the same source. In this way, synchronised multi-room audio is possible without difficulty. (Hence the name Shairport Sync, BTW.)

Shairport Sync does not support AirPlay video or photo streaming.

Shairport Sync is a fork of the original Shairport which was based on reverse-engineering Apple's key used in its AirPort Express. Be advised that this functionality may be removed at Apple's discretion.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Starting](#Starting)
*   [4 Daemon Setup](#Daemon_Setup)

## Installation

[Install](/index.php/Install "Install") the [shairport-sync](https://www.archlinux.org/packages/?name=shairport-sync) package.

## Configuration

The configuration file can be found at `/etc/shairport-sync.conf`. It contains useful comments and configuration hints. More documentation is available in the [README](https://github.com/mikebrady/shairport-sync/blob/master/README.md#configuring-shairport-sync) file.

## Starting

[Start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `shairport-sync.service` using systemd.

## Daemon Setup

If you want to run shairport-sync as a daemon you will need to have a folder created in `/var/run` which is a tempfs by default in archlinux. To have a folder created automatically on boot create a tempfiles configuration file, for example

 `/usr/lib/tempfiles.d/shairport-sync.conf`  `d /var/run/shairport-sync 0755 username group` 

you can now use `shairport-sync -d` to run shairport-sync as a daemon, and `shairport-sync -k` to kill the daemon.