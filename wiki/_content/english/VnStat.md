[vnStat](http://humdi.net/vnstat/) is a lightweight (command line) network traffic monitor. It monitors selectable interfaces and stores network traffic logs in a database for later analysis.

## Installation

[Install](/index.php/Install "Install") the [vnstat](https://www.archlinux.org/packages/?name=vnstat) package.

## Configuration

[Start/Enable](/index.php/Systemd#Using_units "Systemd") the `vnstat.service` daemon.

Pick a preferred network interface and edit the `Interface` variable in the `/etc/vnstat.conf` accordingly. To list all interfaces available to vnstat, use `vnstat --iflist`.

To start monitoring a particular interface you must initialize a database first. Each interface needs its own database. The command to initialize one for the `eth0` interface is:

```
# vnstat -u -i eth0

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