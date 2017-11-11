Related articles

*   [Dnsmasq](/index.php/Dnsmasq "Dnsmasq")
*   [Lighttpd](/index.php/Lighttpd "Lighttpd")
*   [Linux_Containers](/index.php/Linux_Containers "Linux Containers")
*   [Nginx](/index.php/Nginx "Nginx")
*   [OpenVPN](/index.php/OpenVPN "OpenVPN")

Pi-hole is a shell-script based project that manages blocklists of known advertisements and malware and seamlessly interacts with [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) to simply drop all any request to a known bad-actor. Pi-hole replaces your router as the LAN's DNS so all requests go through it without the need to install anything on the client-side. This setup effectively deploys network-wide adblocking (ie for all connected devices). The package comes with a nice webUI (as well as a CLI interface) and is very lightweight and scaleable.

## Contents

*   [1 Pi-hole Server](#Pi-hole_Server)
    *   [1.1 Installation](#Installation)
    *   [1.2 Initial configuration](#Initial_configuration)
        *   [1.2.1 Dnsmasq](#Dnsmasq)
        *   [1.2.2 Web Server](#Web_Server)
            *   [1.2.2.1 Lighttpd](#Lighttpd)
            *   [1.2.2.2 Nginx](#Nginx)
        *   [1.2.3 FTL](#FTL)
*   [2 Configuration of the router and of Pi-hole](#Configuration_of_the_router_and_of_Pi-hole)
    *   [2.1 Preferred method](#Preferred_method)
    *   [2.2 Fallback method](#Fallback_method)
*   [3 Using Pi-hole together with OpenVPN](#Using_Pi-hole_together_with_OpenVPN)
*   [4 Pi-hole Standalone](#Pi-hole_Standalone)
    *   [4.1 Installation](#Installation_2)
    *   [4.2 Initial configuration](#Initial_configuration_2)
        *   [4.2.1 Dnsmasq](#Dnsmasq_2)
        *   [4.2.2 Openresolve](#Openresolve)
*   [5 See also](#See_also)

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

For security reason, if you want to populate [PHP open_basedir](/index.php/PHP#Configuration "PHP") directive, Pi-hole administration web interface needs access to following files and directories:

```
/srv/http/pihole:/run/pihole-ftl/pihole-FTL.port:/run/log/pihole/pihole.log:/run/log/pihole-ftl/pihole-FTL.log:/etc/pihole:/etc/hosts:/etc/hostname:/etc/dnsmasq.d/03-pihole-wildcard.conf:/proc/meminfo:/proc/cpuinfo:/sys/class/thermal/thermal_zone0/temp:/tmp

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

Copy the package provided default config for Pi-hole:

```
# mkdir /etc/nginx/conf.d
# cp /usr/share/pihole/configs/nginx.example.conf /etc/nginx/conf.d/pihole.conf

```

[Enable](/index.php/Enable "Enable") `nginx.service` `php-fpm.service` and re/start them.

#### FTL

FTL is part of Pi-hole project. It is a database-like wrapper/API providing the frontend to Pi-hole's DNS query log. One can configure FTL in `/etc/pihole/pihole-FTL.conf`. [Read](https://github.com/pi-hole/FTL#ftls-config-file) project documentation for details.

`pi-hole-ftl.service` is statically enabled; re/start it.

## Configuration of the router and of Pi-hole

### Preferred method

Most users will want the all of the following functionality:

1.  Per-host tracking on Pi-hole (i.e. logging of DNS requests tied to individual machines by their respective hostnames).
2.  The ability to resolve hostnames on the LAN.
3.  Ad blocking/network monitoring provided by Pi-hole.

To achieve all of the above, the router should be configured to advertise Pi-hole's IP address for DNS resolution to clients, but retain the actual DNS resolution itself *upstream* of the Pi-hole box. Pi-hole should be configured to simply use the router as its *sole* DNS entry.

On the router, use a custom dnsmasq config entry to advertise the IP of the Pi-hole box. The syntax is:

```
dhcp-option=6,IP_of_Pi-hole

```

If Pi-hole is running on a machine whose IP address is 192.168.1.250, this becomes:

```
dhcp-option=6,192.168.1.250

```

On Pi-hole, login to the web interface ([http://pi.hole](http://pi.hole)), select "Settings" and define the IP address of the *router* as the only upstream DNS server. Do not define any other DNS entries for Pi-hole.

**Tip:** A simple check to see that the router is setup correctly is to first renew a DHCP lease, then inspect the contents of `/etc/resolv.conf` on the target client machine. One should see the IP address of the Pi-hole box, not the IP address of the router.

### Fallback method

**Note:** The above configuration may not be possible on some routers depending on the feature set exposed the firmware. The configuration above is confirmed to work on some popular open-source firmwares such as [LEDE/OpenWRT](https://forum.lede-project.org/t/lede-pi-hole-works-perfectly-need-to-understand-why-so-i-can-configure-tomatousb-the-same-way/8274), [DD-WRT](https://www.dd-wrt.com/site/index), and [TomatoUSB](http://www.linksysinfo.org/index.php?threads/redefining-dns-from-router-to-a-box-running-pi-hole.73576/#post-292078) to name a few.

Users unable to configure the router as directed above are referred to [this guide](https://discourse.pi-hole.net/t/how-do-i-configure-my-devices-to-use-pi-hole-as-their-dns-server/245) for setup instructions that gives most of the functionality in the list above. Key limitations of using this method include:

1.  Per-host tracking on Pi-hole (i.e. logging of DNS requests tied to individual machines by their respective hostnames).
2.  The ability to resolve hostnames on the LAN.

## Using Pi-hole together with OpenVPN

One can use both [OpenVPN](/index.php/OpenVPN "OpenVPN") (server) together with Pi-hole to effectively route the remote traffic from the clients though Pi-hole's DNS thus dropping ads for the clients. A reduction in cellular data usage is expected since ads are never allowed to load. Make sure `/etc/openvpn/server/server.conf` contains two key lines as illustrated below replacing the literal "xxx.xxx.xxx.xxx" with the IP address of the box running Pi-hole:

```
push "redirect-gateway def1 bypass-dhcp"
push "dhcp-option DNS xxx.xxx.xxx.xxx"

```

If it still doesn't work, try creating a file `/etc/dnsmasq.d/00-openvpn.conf` with the following contents:

```
interface=tun0

```

This may be necessary to make `dnsmasq` listen on `tun0`.

## Pi-hole Standalone

The Archlinux Pi-hole Standalone variant is born from the need to use Pi-hole services in a mobile context. [Sky-hole article](http://dlaa.me/blog/post/skyhole) was inspirational.

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