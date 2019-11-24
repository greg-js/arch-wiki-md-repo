[Naemon](http://www.naemon.org/) is the new monitoring suite that aims to be faster and more stable, while giving you a clearer view of the state of your network.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Web interface](#Web_interface)
    *   [2.1 Apache configuration](#Apache_configuration)
*   [3 See also](#See_also)

## Installation

Install [naemon](https://aur.archlinux.org/packages/naemon/) from the [AUR](/index.php/AUR "AUR").

Copy `/etc/naemon/examples/*` to `/etc/naemon/conf.d/` if you want some example hosts and services to start with.

Install the plugins from [monitoring-plugins](https://www.archlinux.org/packages/?name=monitoring-plugins) as well as [fping](https://www.archlinux.org/packages/?name=fping).

## Web interface

Install [thruk](https://aur.archlinux.org/packages/thruk/), then uncomment:

 `/etc/naemon/naemon.cfg` 
```
broker_module=/usr/lib/naemon/naemon-livestatus/livestatus.so /var/cache/naemon/live

```

Thruk is a fast, modern GUI. Try out the [demo](https://demo.thruk.org/thruk/cgi-bin/login.cgi).

### Apache configuration

Add the http user to the naemon group:

```
usermod -aG naemon http

```

Load modules and include naemon-thruk.conf:

 `/etc/httpd/conf/httpd.conf` 
```
LoadModule rewrite_module modules/mod_rewrite.so                            
LoadModule fcgid_module modules/mod_fcgid.so 

Include conf/extra/thruk.conf

```

Set the thruk_user and thruk_group to naemon:

 `/etc/thruk/thruk_local.conf` 
```
thruk_user=naemon
thruk_group=naemon

```

Restart httpd and navigate to [http://localhost/thruk/](http://localhost/thruk/)

The default username and password is thrukadmin, thrukadmin.

## See also

*   [FAQ](http://www.naemon.org/documentation/faq/)
*   [op5 on Naemon, Nagios and the future](http://www.op5.com/blog/news/op5-naemon-nagios-future/)
*   [Andreas Ericsson: The future of Nagios](http://www.youtube.com/watch?v=YgbbyyNIiHc)