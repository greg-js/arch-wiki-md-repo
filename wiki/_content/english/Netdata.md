> Get control of your servers. Simple. Effective. Awesome.

[netdata](https://github.com/firehol/netdata/) is a system for distributed real-time performance and health monitoring. It provides unparalleled insights, in real-time, of everything happening on the system it runs (including applications such as web and database servers), using modern interactive web dashboards.

netdata is fast and efficient, designed to permanently run on all systems (physical & virtual servers, containers, IoT devices), without disrupting their core function.

## Contents

*   [1 Installation](#Installation)
*   [2 Enable at startup](#Enable_at_startup)
*   [3 Control the service](#Control_the_service)
*   [4 Configuring](#Configuring)
    *   [4.1 Netdata behind web server](#Netdata_behind_web_server)
    *   [4.2 Using built in webserver](#Using_built_in_webserver)
    *   [4.3 Optimization](#Optimization)
*   [5 Related](#Related)

## Installation

netdata can be installed using [netdata](https://www.archlinux.org/packages/?sort=&q=netdata) community package

```
   sudo pacman -S netdata

```

## Enable at startup

```
   sudo systemctl enable netdata

```

## Control the service

```
   sudo systemctl start netdata

```

## Configuring

Configuration file is located at `/etc/netdata/netdata.conf`

plugins folders is at `/usr/lib/netdata`

### Netdata behind web server

netdata can be run behind another server and you can configure it accordingly. The [wiki](https://github.com/firehol/netdata/wiki/Running-behind-nginx) page has example for Apache, Nginx, lighttpd and caddy.

### Using built in webserver

By default netdata is accessible at `[http://localhost:19999/](http://localhost:19999/)` or `[http://ip:19999/](http://ip:19999/)`

### Optimization

netdata can be optimized for

1.  low resource (or)
2.  high performance

## Related

netdata is created by the group who also created

*   FireHOL and FireQOS