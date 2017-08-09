Pi-hole is a shell-script based project that manages blocklists of known advertisements and malware and seamlessly interacts with [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) to simply drop all any request to a known bad-actor. Pi-hole replaces your router as the LAN's DNS so all requests go through it without the need to install anything on the client-side. This setup effectively deploys network-wide adblocking (ie for all connected devices). The package comes with a nice webUI (as well as a CLI interface) and is very lightweight and scaleable.

## Contents

*   [1 Pi-hole Server](#Pi-hole_Server)
    *   [1.1 Installation](#Installation)
    *   [1.2 Initial configuration](#Initial_configuration)
        *   [1.2.1 Dnsmasq](#Dnsmasq)
        *   [1.2.2 Router](#Router)
        *   [1.2.3 Web Server](#Web_Server)
            *   [1.2.3.1 Lighttpd](#Lighttpd)
            *   [1.2.3.2 Nginx](#Nginx)
    *   [1.3 Web interface](#Web_interface)
    *   [1.4 FTL](#FTL)
*   [2 Using Pi-hole together with OpenVPN](#Using_Pi-hole_together_with_OpenVPN)
*   [3 Pi-hole Standalone](#Pi-hole_Standalone)
    *   [3.1 Installation](#Installation_2)
    *   [3.2 Initial configuration](#Initial_configuration_2)
        *   [3.2.1 Dnsmasq](#Dnsmasq_2)
        *   [3.2.2 Openresolve](#Openresolve)
*   [4 See also](#See_also)

## Pi-hole Server

### Installation

[Install](/index.php/Install "Install") [pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/) and [pi-hole-server](https://aur.archlinux.org/packages/pi-hole-server/).

### Initial configuration

#### Dnsmasq

Ensure that the following line in `/etc/dnsmasq.conf` is uncommented:

 `/etc/dnsmasq.conf` 
```
[...]
conf-dir=/etc/dnsmasq.d/,*.conf

```

[Enable](/index.php/Enable "Enable") `dnsmasq.service` and re/start it.

#### Router

Pi-hole needs to be the DNS for the LAN in order to work properly. Typical home users rely on their router to resolve DNS queries. The prefered method is to simply redefine the DNS entry **on the router** to use the IP address of the box running Pi-hole. Configuring the router is outside the scope of this article. An alternative is to manually define the DNS entries for each device connecting to the router although this can be tedious. See, [How do I configure my devices to use Pi-hole as their DNS server?](https://discourse.pi-hole.net/t/how-do-i-configure-my-devices-to-use-pi-hole-as-their-dns-server/245)

#### Web Server

Users may optionally choose a web server for the Pi-hole web interface.

**Note:** Pi-hole does not strictly require a web interface as many commands are possible via the CLI interface.

The AUR package provides example config files for both [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) and [nginx](https://www.archlinux.org/packages/?name=nginx). Other web servers can also run the WebUI, but are currently unsupported.

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
# cp /usr/share/pihole/configs/lighttpd.example.conf /etc/lighttpd/lighttpd.conf

```

[Enable](/index.php/Enable "Enable") `lighttpd.service` and re/start it:

##### Nginx

[Install](/index.php/Install "Install") [nginx-mainline](https://www.archlinux.org/packages/?name=nginx-mainline) and [php-fpm](https://www.archlinux.org/packages/?name=php-fpm).

Edit `/etc/php/php-fpm.d/www.conf` and change the listen directive to the following:

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
# cp /usr/share/pihole/configs/nginx.example.conf /etc/nginx/conf.d/pihole.conf

```

[Enable](/index.php/Enable "Enable") `nginx.service` `php-fpm.service` and re/start them.

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

`pi-hole-ftl.service` is statically enabled; re/start it.

## Using Pi-hole together with OpenVPN

One can use both [OpenVPN](/index.php/OpenVPN "OpenVPN") (server) together with Pi-hole to effectively route the remote traffic from the clients though Pi-hole's DNS thus dropping ads for the clients. A reduction in cellular data usage is expected since ads are never allowed to load. Make sure `/etc/openvpn/server/server.conf` contains two key lines as illustrated below replacing the literal "xxx.xxx.xxx.xxx" with the IP address of the box running pi-hole:

```
push "redirect-gateway def1 bypass-dhcp"
push "dhcp-option DNS xxx.xxx.xxx.xxx"

```

**Note:** This should be the only modification needed.

## Pi-hole Standalone

The Archlinux Pi-hole Standalone variant is born from the need to use pi-hole services in a mobile context. [Sky-hole article](http://dlaa.me/blog/post/skyhole) was inspirational.

### Installation

[Install](/index.php/Install "Install") the [pi-hole-standalone](https://aur.archlinux.org/packages/pi-hole-standalone/) package.

### Initial configuration

#### Dnsmasq

Setup is identical to the steps described in [#Dnsmasq](#Dnsmasq).

#### Openresolve

Edit `/etc/resolvconf.conf` to uncomment the name_servers line:

 `/etc/resolvconf.conf` 
```
[...]
name_servers=127.0.0.1

```

and update resolvconf:

```
# resolvconf -u

```

## See also

*   [Pi-hole Homepage](https://pi-hole.net/)
*   [Pi-hole GitHub Page](https://github.com/pi-hole/pi-hole)
*   [Pi-hole FTL GitHub Page](https://github.com/pi-hole/FTL)
*   [Sky-Hole, the basic idea under Pi-hole standalone](http://dlaa.me/blog/post/skyhole)