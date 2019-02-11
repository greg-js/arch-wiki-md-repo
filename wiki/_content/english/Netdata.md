[netdata](https://github.com/firehol/netdata/) is a system for distributed real-time performance and health monitoring. *netdata* is created by the group that also created FireHOL and FireQOS.

*netdata* is designed to permanently run on all systems (physical and virtual servers, containers, IoT devices), without disrupting their core function.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Behind a web server](#Behind_a_web_server)
    *   [2.2 Built-in web server](#Built-in_web_server)
    *   [2.3 Optimization](#Optimization)

## Installation

[Install](/index.php/Install "Install") the [netdata](https://www.archlinux.org/packages/?name=netdata) package.

[Start/enable](/index.php/Start/enable "Start/enable") the `netdata` service.

## Configuration

The configuration file is located at `/etc/netdata/netdata.conf`. The plugins folders is at `/usr/lib/netdata` and their configuration at `/usr/lib/netdata/conf.d`.

### Behind a web server

*netdata* can be run behind another server and you can configure it accordingly. The [wiki](https://github.com/firehol/netdata/wiki/Running-behind-nginx) page has example for [Apache](/index.php/Apache "Apache"), [Nginx](/index.php/Nginx "Nginx"), [lighttpd](/index.php/Lighttpd "Lighttpd") and [caddy](/index.php/Caddy "Caddy").

### Built-in web server

By default *netdata* is accessible at `[http://localhost:19999/](http://localhost:19999/)` or `[http://ip:19999/](http://ip:19999/)`.

### Optimization

*netdata* can be optimized for:

1.  low resource (or)
2.  high performance