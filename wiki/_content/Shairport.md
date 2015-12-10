# Shairport

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Shairport is a utility for emulating AirPlay functionality on Linux. However, since it has been created by reverse-engineering Apple's key used in its AirPort Express, be advised that the functionality may be removed at Apple's discretion. ShairPort does not support AirPlay v2 (video and photo streaming).

## Installation

[Install](/index.php/Install "Install") the [shairport-sync](https://www.archlinux.org/packages/?name=shairport-sync) package.

## Configuration

The configuration file can be found at `/etc/conf.d/shairport-sync`. It consists on a single variable allowing arguments to be passed to the service. In the example below, iTunes would label the server as 'My Server Name' rather than the default 'Shairport Sync on <hostname>'.

 `/etc/conf.d/shairport-sync` 

```
# ShairportSync Daemon options
SHAIRPORT_ARGS="--name='My Server Name'"

```

## Starting

[Start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `shairport-sync.service` using systemd.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Shairport&oldid=390215](https://wiki.archlinux.org/index.php?title=Shairport&oldid=390215)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Streaming](/index.php/Category:Streaming "Category:Streaming")