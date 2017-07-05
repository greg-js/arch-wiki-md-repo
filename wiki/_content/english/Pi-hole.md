From the [Pi-hole README.md on GitHub](https://github.com/pi-hole/pi-hole):

	The Pi-Hole™ is an advertising-aware DNS/Web server. If an ad domain is queried, a small Web page or GIF is delivered in place of the advertisement..

	The gravity.sh does most of the magic. The script pulls in ad domains from many sources and compiles them into a single list of over 1.6 million entries (if you decide to use the mahakala list). This script is controlled by the pihole command. Please run pihole -h to see what commands can be run via pihole.

This wiki page tries to cover the need for configuration and use instructions of this Pi-hole adaptations for Archlinux not officially supported by the main project. For bugs, issues and general reporting, plaese refer to [pi-hole-server AUR page](https://aur.archlinux.org/packages/pi-hole-server/) for server package or [pi-hole-standalone AUR page](https://aur.archlinux.org/packages/pi-hole-standalone/) for standalone package.

## Contents

*   [1 Pi-hole Server](#Pi-hole_Server)
    *   [1.1 Installation](#Installation)
    *   [1.2 First install configuration](#First_install_configuration)
        *   [1.2.1 Dnsmasq](#Dnsmasq)
        *   [1.2.2 Web Server](#Web_Server)
            *   [1.2.2.1 Lighttpd](#Lighttpd)
            *   [1.2.2.2 Nginx](#Nginx)
    *   [1.3 Web interface](#Web_interface)
    *   [1.4 FTL](#FTL)
*   [2 Using Pi-hole together with OpenVPN](#Using_Pi-hole_together_with_OpenVPN)
*   [3 Pi-hole Standalone](#Pi-hole_Standalone)
    *   [3.1 Installation](#Installation_2)
    *   [3.2 First install configuration](#First_install_configuration_2)
        *   [3.2.1 Dnsmasq](#Dnsmasq_2)
        *   [3.2.2 Openresolve](#Openresolve)
*   [4 See also](#See_also)

## Pi-hole Server

### Installation

[Install](/index.php/Install "Install") [pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/) and [pi-hole-server](https://aur.archlinux.org/packages/pi-hole-server/).

### First install configuration

#### Dnsmasq

Setup dnsmasq which will resolve DNS queries for your LAN and manage filtering ads directly by pi-hole.

**Users already using dnsmasq**: Edit `/etc/dnsmasq.conf` and uncomment the last line:

 `/etc/dnsmasq.conf` 
```
...
conf-dir=/etc/dnsmasq.d/,*.conf

```

**Users not making use of dnsmasq prior to installing Pi-hole**: Copy the pi-hole-server-provided config file replacing the standard one (or simply diff the two):

```
# cp /usr/share/pihole/configs/dnsmasq.main /etc/dnsmasq.conf

```

If necessary, [enable](/index.php/Enable "Enable") `dnsmasq.service` and re/start it. Pi-hole needs to be the DNS for your LAN. Likely, your router is preforming this task currently, so the primary DNS on the router needs to be redefined to use the IP address of the box running Pi-hole. Configuring the router is outside the scope of this article, but a mandatory step.

#### Web Server

Users may optionally choose a web server for the Pi-hole web interface.

**Note:** Pi-hole does not strictly require a web interface as many commands are possible via the CLI interface.

Upstream officially supports [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) and provides config files for it. The AUR package also provides config files for [nginx](https://www.archlinux.org/packages/?name=nginx), so either is supported out-of-the-box. Other web servers can also run the webUI, but are unsupported.

Any webserver will require the following edit to enable the sockets extension:

 `/etc/php/php.ini` 
```
[...]
extension=sockets.so
[...]
```

##### Lighttpd

[Install](/index.php/Install "Install") [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) and [php-cgi](https://www.archlinux.org/packages/?name=php-cgi).

```
# cp /usr/share/pihole/configslighttpd.example.conf /etc/lighttpd/lighttpd.conf

```

If necessary, [enable](/index.php/Enable "Enable") `lighttpd.service` and re/start it:

##### Nginx

[Install](/index.php/Install "Install") [nginx](https://www.archlinux.org/packages/?name=nginx) or [nginx-mainline](https://www.archlinux.org/packages/?name=nginx-mainline) and [php-fpm](https://www.archlinux.org/packages/?name=php-fpm).

Edit `/etc/php/php-fpm.d/www.conf` and changing the listen directive to the following:

```
listen = 127.0.0.1:9000  

```

Modify `/etc/nginx/nginx.conf` to contain the following in the **http** section:

```
gzip            on;
gzip_min_length 1000;
gzip_proxied    expired no-cache no-store private auth;
gzip_types      text/plain application/xml application/json application/javascript application/octet-stream text/css;
include /etc/nginx/conf.d/*.conf;

```

Copy the package provided default config for pi-hole:

```
# mkdir /etc/nginx/conf.d
# cp /etc/pihole/configs/nginx.example.conf /etc/nginx/conf.d/pihole.conf

```

If necessary, [enable](/index.php/Enable "Enable") `nginx.service` `php-fpm.service` and re/start them.

### Web interface

The Pi-hole web interface is very complete and well done. One can use it to, configure nearly every aspect of [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq), execute lots of Pi-hole available commands, control white lists and black lists, and monitor ad filtering. Connect to web interface at

```
http://<IP/Hostname of Pi-hole machine>/admin/

```

or

```
[http://pi.hole/admin](http://pi.hole/admin)

```

### FTL

FTL is part of Pi-hole project. It is a database-like wrapper/API providing the frontend to Pi-hole's DNS query log. One can configure FTL in `/etc/pihole/pihole-FTL.conf`. [Read](https://github.com/pi-hole/FTL#ftls-config-file) project documentation for details.

## Using Pi-hole together with OpenVPN

One can use both [OpenVPN](/index.php/OpenVPN "OpenVPN") (server) together with Pi-hole to effectively route the remote traffic from the clients though Pi-hole's DNS thus dropping ads for the clients. A reduction in cellular data usage is expected since ads are never allowed to load. Make sure `/etc/openvpn/server/server.conf` contains two key lines as illustrated below replacing the literal "xxx.xxx.xxx.xxx" with the IP address of the box running pi-hole:

```
push "redirect-gateway def1 bypass-dhcp"
push "dhcp-option DNS xxx.xxx.xxx.xxx"

```

**Note:** This should be the only modified needed.

## Pi-hole Standalone

The Archlinux Pi-hole Standalone variant is born from the need to use pi-hole services in a mobile context. [Sky-hole article](http://dlaa.me/blog/post/skyhole) was inspirational.

### Installation

[Install](/index.php/Install "Install") the [pi-hole-standalone](https://aur.archlinux.org/packages/pi-hole-standalone/) package.

### First install configuration

#### Dnsmasq

Setup is identical to the steps described in [Pi-hole#Dnsmasq](/index.php/Pi-hole#Dnsmasq "Pi-hole").

#### Openresolve

Edit `/etc/resolvconf.conf` to uncomment the name_servers line and update resolvconf:

```
# sed -i 's|#name_servers=127.0.0.1|name_servers=127.0.0.1|' /etc/resolvconf.conf
# resolvconf -u

```

## See also

*   [Pi-hole Homepage](https://pi-hole.net/)
*   [Pi-hole GitHub Page](https://github.com/pi-hole/pi-hole)
*   [Pi-hole FTL GitHub Page](https://github.com/pi-hole/FTL)
*   [Sky-Hole, the basic idea under Pi-hole standalone](http://dlaa.me/blog/post/skyhole)