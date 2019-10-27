[netdata](https://github.com/firehol/netdata/) is a system for distributed real-time performance and health monitoring. *netdata* is created by the group that also created [FireHOL and FireQOS](/index.php/FireHOL "FireHOL").

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

Netdata reads its configuration file from `/etc/netdata/netdata.conf`. This config file is not needed by default. Netdata works with default settings without it, but it does allow you to adapt the general behavior of Netdata. You can find all these settings, with their default values, by accessing the URL `[http://localhost:19999/netdata.conf](http://localhost:19999/netdata.conf)`.

The plugins folders is at `/usr/lib/netdata` and their configuration at `/usr/lib/netdata/conf.d`.

### Behind a web server

*netdata* can be run behind another web server (proxy) and you can configure it accordingly. *netdata* [documentation](https://docs.netdata.cloud/) has examples for [Apache](https://docs.netdata.cloud/docs/running-behind-apache), [Nginx](https://docs.netdata.cloud/docs/running-behind-nginx), [lighttpd](https://docs.netdata.cloud/docs/running-behind-lighttpd), [haproxy](https://docs.netdata.cloud/docs/running-behind-haproxy) and [caddy](https://docs.netdata.cloud/docs/running-behind-caddy).

### Built-in web server

By default *netdata* is accessible at `[http://localhost:19999/](http://localhost:19999/)` or `[http://ip:19999/](http://ip:19999/)`.

### Optimization

*netdata* can be optimized for:

1.  [Low resources](https://docs.netdata.cloud/docs/performance)
2.  [High performance](https://docs.netdata.cloud/docs/high-performance-netdata)
3.  [IoT](https://docs.netdata.cloud/docs/netdata-for-iot)