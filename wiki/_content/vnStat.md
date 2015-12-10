# vnStat

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[vnStat](http://humdi.net/vnstat/) is a lightweight (command line) network traffic monitor. It monitors selectable interfaces and stores network traffic logs in a database for later analysis.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Start Systemd Service](#Start_Systemd_Service)
*   [3 Usage](#Usage)

## Installation

[Install](/index.php/Pacman "Pacman") [vnstat](https://www.archlinux.org/packages/?name=vnstat) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

First open `/etc/vnstat.conf` with your editor and check the interface name is set right, eg.:

```
# Interface "enp3s0"

```

### Start Systemd Service

After introducing the interface(s) and checking the config file. You can start the monitoring process via [systemd](/index.php/Systemd "Systemd")

```
# systemctl start vnstat.service

```

To make this service permanent use

```
# systemctl enable vnstat.service

```

## Usage

Query the network traffic:

```
# vnstat -q

```

Viewing live network traffic usage:

```
# vnstat -l

```

To find more options, use:

```
# vnstat --help

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=VnStat&oldid=383956](https://wiki.archlinux.org/index.php?title=VnStat&oldid=383956)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Networking](/index.php/Category:Networking "Category:Networking")