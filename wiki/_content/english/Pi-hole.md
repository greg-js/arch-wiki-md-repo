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
    *   [1.3 Configuration of the router and of Pi-hole](#Configuration_of_the_router_and_of_Pi-hole)
        *   [1.3.1 Preferred method](#Preferred_method)
        *   [1.3.2 Fallback method](#Fallback_method)
            *   [1.3.2.1 Automatic method: Set Your DNS Server In Your Router's Settings](#Automatic_method:_Set_Your_DNS_Server_In_Your_Router.27s_Settings)
            *   [1.3.2.2 Manual Method: Manual configure DNS entry for your devices](#Manual_Method:_Manual_configure_DNS_entry_for_your_devices)
        *   [1.3.3 Pi-hole centric method](#Pi-hole_centric_method)
    *   [1.4 Using Pi-hole together with OpenVPN](#Using_Pi-hole_together_with_OpenVPN)
*   [2 Pi-hole Standalone](#Pi-hole_Standalone)
    *   [2.1 Installation](#Installation_2)
    *   [2.2 Initial configuration](#Initial_configuration_2)
        *   [2.2.1 Dnsmasq](#Dnsmasq_2)
        *   [2.2.2 Configuring host name resolution](#Configuring_host_name_resolution)
            *   [2.2.2.1 Manually](#Manually)
            *   [2.2.2.2 Openresolve](#Openresolve)
*   [3 Using Pi-hole](#Using_Pi-hole)
    *   [3.1 Pi-hole DNS management](#Pi-hole_DNS_management)
    *   [3.2 Forced update of ad-serving domains list](#Forced_update_of_ad-serving_domains_list)
    *   [3.3 Protect web interface access (server package only)](#Protect_web_interface_access_.28server_package_only.29)
    *   [3.4 Temporarily disable Pi-hole](#Temporarily_disable_Pi-hole)
*   [4 See also](#See_also)

## Pi-hole Server

### Installation

[Install](/index.php/Install "Install") [pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/) and [pi-hole-server](https://aur.archlinux.org/packages/pi-hole-server/). The Pi-hole server package installs two timers (and relative services), both statically enabled:

*   pi-hole-gravity.timer will weekly update Pi-hole blacklisted servers list.
*   pi-hole-logtruncate.timer will daily clean LAN DNS requests log.

If you do not like default timers timings (from upstrem project) you can, of course, [edit](/index.php/Edit "Edit") them or preventing from being executed by [masking](/index.php/Systemd#Using_units "Systemd") them.
You need to manually start them or simply reboot after your configuration is finished.

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

Example config files that work out-of-the-box are provided for both [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) and [nginx](https://www.archlinux.org/packages/?name=nginx). Other web servers can also run the WebUI, but are currently unsupported.

Install [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite) and enable the relevant extensions detailed here:

 `/etc/php/php.ini` 
```
[...]
extension=pdo_sqlite
[...]
extension=sockets.so
extension=sqlite3
[...]
```

For security reasons, one can populate the [PHP open_basedir](/index.php/PHP#Configuration "PHP") directive however, the Pi-hole administration web interface will need access to following files and directories:

```
/srv/http/pihole:/run/pihole-ftl/pihole-FTL.port:/run/log/pihole/pihole.log:/run/log/pihole-ftl/pihole-FTL.log:/etc/pihole:/etc/hosts:/etc/hostname:/etc/dnsmasq.d/03-pihole-wildcard.conf:/proc/meminfo:/proc/cpuinfo:/sys/class/thermal/thermal_zone0/temp:/tmp

```

##### Lighttpd

[Install](/index.php/Install "Install") [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) and [php-cgi](https://www.archlinux.org/packages/?name=php-cgi).

Copy the package provided default config for Pi-hole:

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

FTL is part of Pi-hole project. It is a database-like wrapper/API providing the frontend to Pi-hole's DNS query log. FTL is the only way the Pi-hole web interface accesses data collected by dnsmasq usage and is therefore a requirement.
It's possible to configure FTL editing `/etc/pihole/pihole-FTL.conf` with following parameters (the option shown first is the default):

*   SOCKET_LISTENING=localonly|all (Listen only for local socket connections or permit all connections)
*   TIMEFRAME=rolling24h|yesterday|today (Rolling data window, up to 48h (today + yesterday), or up to 24h (only today, as in Pi-hole v2.x ))
*   QUERY_DISPLAY=yes|no (Display all queries? Set to no to hide query display)
*   AAAA_QUERY_ANALYSIS=yes|no (Allow FTL to analyze AAAA queries from pihole.log?)
*   MAXDBDAYS=365 (How long should queries be stored in the database? Setting this to 0 disables the database altogether)
*   RESOLVE_IPV6=yes|no (Should FTL try to resolve IPv6 addresses to host names?)
*   RESOLVE_IPV4=yes|no (Should FTL try to resolve IPv4 addresses to host names?)
*   DBINTERVAL=1.0 (How often do we store queries in FTL's database [minutes]?)
*   DBFILE=/etc/pihole/pihole-FTL.db (Specify path and filename of FTL's SQLite long-term database. Setting this to DBFILE= disables the database altogether)

**Tip:** If Pi-hole is running on a solide state device (Single-board computers SD, SSD, M.2/NVMe device, etc...) it is recommended to set the DBINTERVAL value at least to 60.0 to extend it's life.

`pi-hole-ftl.service` is statically enabled; re/start it.

### Configuration of the router and of Pi-hole

#### Preferred method

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

**Note:** For a full network and Pi-hole functionality, you may need to disable, if present on your router firmware, the `dns-rebind` feature.

**Note:** The above configuration may not be possible on some routers depending on the feature set exposed the firmware. The configuration above is confirmed to work on some popular open-source firmwares such as [LEDE/OpenWRT](https://forum.lede-project.org/t/lede-pi-hole-works-perfectly-need-to-understand-why-so-i-can-configure-tomatousb-the-same-way/8274), [DD-WRT](https://www.dd-wrt.com/site/index), and [TomatoUSB](http://www.linksysinfo.org/index.php?threads/redefining-dns-from-router-to-a-box-running-pi-hole.73576/#post-292078) to name a few.

#### Fallback method

Users unable to configure the router as directed above are referred to [this upstream guide](https://discourse.pi-hole.net/t/how-do-i-configure-my-devices-to-use-pi-hole-as-their-dns-server/245) for setup instructions.
For completeness, an overview of the guide will be provided below.
You can follow two methods:

##### Automatic method: Set Your DNS Server In Your Router's Settings

This is the fastest way to get all of your devices using Pi-hole. If you set this configuration via your router's DHCP options, any device that connects to your network will immediately begin blocking ads.

**Tip:** Make sure you adjust this setting under your **LAN** settings and not the **WAN**.

Go to the **DHCP Server section** of your router and set your Pi-hole box IP address as your unique DNS server for your **LAN**.

**Warning:** If you have existing network devices on your network when you make this change, you will not see ads getting blocked until the DHCP lease is renewed. For simplicity, restart those devices.

**Note:** Note that your Pi-hole should be the only DNS server set here as Pi-hole already delivers the other upstream servers. If you set another server in your router, it's possible your ad blocking will be negatively affected..

##### Manual Method: Manual configure DNS entry for your devices

You can manually configure each device to use Pi-hole as their DNS server. You just need the IP address of your Pi-hole and then follow the instructions below for your operating system.

**Linux**
In many of modern Linux Desktop Environment, DNS settings are configured through Network Manager.

1.  Click System > Preferences > Network Connections
2.  Select the connection for which you want to configure
3.  Click Edit
4.  Select the IPv4 Settings or IPv6 Settings tab
5.  If the selected method is Automatic (DHCP), open the dropdown and select Automatic (DHCP) addresses only instead. If the method is set to something else, do not change it.
6.  In the DNS servers field, enter your Pi's IP addresses
7.  Click Apply to save the change
8.  Repeat the procedure for additional network connections you want to change.

If you don't use Network Manager, plese refer to your connection manager instruction for specific DNS manual settings.
If you don't use a connection manager at all your DNS settings are specified in `/etc/resolv.conf`: edit it to insert the following **unique** `nameserver` item:

 `/etc/resolv.conf` 
```
[...]
nameserver <Pi-hole_box_IP>

```

where `<Pi-hole_box_IP>` is IP address of the machine that run Pi-hole.

**macOS**

1.  Click Apple > System Preferences > Network
2.  Highlight the connection for which you want to configure DNS
3.  Click Advanced
4.  Select the DNS tab
5.  Click + to replace any listed addresses with, or add, your Pi's IP addresses at the top of the list:
6.  Click Apply > OK
7.  Repeat the procedure for additional network connections you want to change.

**Windows**
DNS settings are specified in the TCP/IP Properties window for the selected network connection.

1.  Go to the Control Panel
2.  Click Network and Internet > Network and Sharing Center > Change adapter settings
3.  Select the connection for which you want to configure
4.  Right-click Local Area Connection > Properties
5.  Select the Networking tab
6.  Select Internet Protocol Version 4 (TCP/IPv4) or Internet Protocol Version 6 (TCP/IPv6)
7.  Click Properties
8.  Click Advanced
9.  Select the DNS tab
10.  Click OK
11.  Select Use the following DNS server addresses
12.  Replace those addresses with the IP addresses of your Pi
13.  Restart the connection you selected in step 3
14.  Repeat the procedure for additional network connections you want to change.

#### Pi-hole centric method

You can follow another method to configure your LAN. You can set up the machine running Pi-hole as a DHCP server and turn off all network services on your router, relegating it to a simple gateway/natter.

**Warning:** Dnsmasq should be just installed or you should use the default Pi-hole dnsmasq configuration provided with the package. The following instructions may overwrite your dnsmasq customizations if present.

For semplicity of configuration and exposure, only the method via web interface will be followed:

*   Go to your router configuration interface and turn off DHCP service. Take note of your router IP address.
*   Go to Pi-hole web interface ([http://pi.hole](http://pi.hole))
*   Go to **Settings/Pi-hole DHCP Server**
*   Check **DHCP server enabled**
*   Set DHCP range for your LAN valorizing **From** and **To** boxes. For example: From 192.168.1.2 To 192.168.1.100
*   Set your router IP address into **Router** box. For example: 192.168.1.1
*   Optional: From **Advanced DHCP settings** check **Enable IPv6 support (SLAAC + RA)** if you want IPv6 support and functionality.
*   Optional: If you need some static DHCP lease you can configure them going to **DHCP leases/Static DHCP leases configuration** section.
*   Save to apply changes.

**Warning:** If you have existing network devices on your network when you make this change, you will not see ads getting blocked until the DHCP lease is renewed. For simplicity, restart those devices.

### Using Pi-hole together with OpenVPN

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
The Pi-hole standalone package install a statically enabled timer (and relative service) will weekly update Pi-hole blacklisted servers list. If you do not like default timer timings (from upstrem project) you can, of course, [edit](/index.php/Edit "Edit") it or preventing from being executed by [masking](/index.php/Systemd#Using_units "Systemd") it.
You need to manually start `pi-hole-gravity.timer` or simply reboot after your configuration is finished.

### Initial configuration

#### Dnsmasq

Ensure that the following line in `/etc/dnsmasq.conf` is uncommented:

 `/etc/dnsmasq.conf` 
```
[...]
conf-dir=/etc/dnsmasq.d/,*.conf

```

[Enable](/index.php/Enable "Enable") `dnsmasq.service` and re/start it.

#### Configuring host name resolution

The Pi-hole standalone package to work properly requires that a unique DNS is set on your machine. That DNS address need to be your machine itself.
This can be done in several ways.

##### Manually

If no service on your machine automatically handles the `/etc/resolv.conf` file, you can easily edit it to insert the following **unique** item `nameserver`:

 `/etc/resolv.conf` 
```
[...]
nameserver 127.0.0.1

```

**Note:** No other `nameserver` items need to be present in the config file.

##### Openresolve

It is likely that is the [openresolv](https://www.archlinux.org/packages/?name=openresolv) service to handle `/etc/resolv.conf` if you use a network connection manager such as [netctl](https://www.archlinux.org/packages/?name=netctl), [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) or others. If it is your case, you must force [openresolv](https://www.archlinux.org/packages/?name=openresolv) to use **localhost** as name server.
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

## Using Pi-hole

As previously mentioned, Pi-hole offers the ability to be configured and used both through the command line and through its web interface (server package only).

### Pi-hole DNS management

At first installation, Pi-hole is defaulted to use Google DNS for name resolution of your LAN requests. If you want to change servers or simply add others on the machine running Pi-hole you can execute

```
pihole -a setdns [DNS1],[DNS2],...

```

followed by a comma separated list of DNS servers you want Pi-hole will use. For example, if in addition to Google's DNS you want to add those of Comodo run

```
pihole -a setdns 8.8.8.8,8.8.4.4,8.26.56.26,8.20.246.20

```

For server package only, you can manage this via web interface ([http://pi.hole](http://pi.hole)) going to **Settings** and adding desired DNS servers in **Upstream DNS Servers** section. **Save** to apply changes.

### Forced update of ad-serving domains list

If you need to update the blocked domain list, on the machine running Pi-hole you can execute

```
pihole -g

```

or, server package only, via web interface ([http://pi.hole](http://pi.hole)) go to **Tools/Update Lists** and execute **Update Lists**.

### Protect web interface access (server package only)

Pi-hole web interface can be password protected to prevent unauthorized use. On the machine running Pi-hole you can execute

```
pihole -a -p <pwd>

```

where `<pwd>` is the password you want to assign. You can leave it blank for tipical *nix password request and confirmation.
To disable password login retype

```
pihole -a -p

```

leaving **all** blank.

### Temporarily disable Pi-hole

Pi-hole can be easily paused through its web interface ([http://pi.hole](http://pi.hole)): go to **Disable** and choose the suspension option that best suits your case.
It is possible via CLI too by executing

```
pihole disable [time]

```

If you leave `time` blank disabling will be permanent until later manual reenabling.
`time` can be expressed in seconds or minutes with syntax #s and #m. For example, to disable Pi-hole for 5 minutes only, you can execute

```
pihole disable 5m

```

At any time you can reenable Pi-hole by executing

```
pihole enable

```

or, via web interface, clicking on **Enable**.

## See also

*   [Pi-hole Homepage](https://pi-hole.net/)
*   [Pi-hole GitHub Page](https://github.com/pi-hole/pi-hole)
*   [Pi-hole FTL GitHub Page](https://github.com/pi-hole/FTL)
*   [Sky-Hole, the basic idea under Pi-hole standalone](http://dlaa.me/blog/post/skyhole)