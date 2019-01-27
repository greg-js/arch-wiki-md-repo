Related articles

*   [dnsmasq](/index.php/Dnsmasq "Dnsmasq")
*   [lighttpd](/index.php/Lighttpd "Lighttpd")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [nginx](/index.php/Nginx "Nginx")
*   [OpenVPN](/index.php/OpenVPN "OpenVPN")

[Pi-hole](https://pi-hole.net/) is a [DNS sinkhole](https://en.wikipedia.org/wiki/DNS_sinkhole "wikipedia:DNS sinkhole") that compiles a blocklist of domains known to host advertisements and malware from multiple third-party sources. Pi-hole uses [dnsmasq](/index.php/Dnsmasq "Dnsmasq") to seamlessly drop any and all requests for domains in its blocklist. Running it effectively deploys network-wide ad-blocking without the need to configure individual clients. The package comes with a web and a CLI interface.

## Contents

*   [1 Pi-hole server](#Pi-hole_server)
    *   [1.1 Installation](#Installation)
    *   [1.2 Initial configuration](#Initial_configuration)
        *   [1.2.1 FTL](#FTL)
        *   [1.2.2 Web server](#Web_server)
            *   [1.2.2.1 Lighttpd](#Lighttpd)
            *   [1.2.2.2 Nginx](#Nginx)
        *   [1.2.3 /etc/hosts](#/etc/hosts)
    *   [1.3 Making devices use Pi-hole](#Making_devices_use_Pi-hole)
        *   [1.3.1 Troubleshooting](#Troubleshooting)
    *   [1.4 Using Pi-hole together with OpenVPN](#Using_Pi-hole_together_with_OpenVPN)
    *   [1.5 Password-protect web interface](#Password-protect_web_interface)
*   [2 Pi-hole Standalone](#Pi-hole_Standalone)
    *   [2.1 Installation](#Installation_2)
    *   [2.2 Initial configuration](#Initial_configuration_2)
        *   [2.2.1 Dnsmasq](#Dnsmasq)
        *   [2.2.2 Configuring host name resolution](#Configuring_host_name_resolution)
            *   [2.2.2.1 Manually](#Manually)
            *   [2.2.2.2 Openresolve](#Openresolve)
*   [3 Using Pi-hole](#Using_Pi-hole)
    *   [3.1 Pi-hole DNS management](#Pi-hole_DNS_management)
    *   [3.2 Forced update of ad-serving domains list](#Forced_update_of_ad-serving_domains_list)
    *   [3.3 Temporarily disable Pi-hole](#Temporarily_disable_Pi-hole)
*   [4 Troubleshooting](#Troubleshooting_2)
    *   [4.1 Data loss on reboot](#Data_loss_on_reboot)
*   [5 See also](#See_also)

## Pi-hole server

### Installation

[Install](/index.php/Install "Install") the [pi-hole-server](https://aur.archlinux.org/packages/pi-hole-server/) package.

### Initial configuration

#### FTL

The [Pi-hole FTL engine](https://github.com/pi-hole/FTL) ([pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/)) is a dependency of the Pi-hole main project.

FTL is a DNS resolver/forwarder and a database-like wrapper/API that provides long-term storage of requests which users can query through the "long-term data" section of the WebGUI. To be clear, data are collected and stored in two places:

1.  Daily data are stored in RAM and are captured in real-time within `/run/log/pihole/pihole.log`
2.  Historical data (i.e. over multiple days/weeks/months) are stored on the file system `/etc/pihole/pihole-FTL.db` written out at a user-specified interval.

`pihole-FTL.service` is statically enabled; re/start it. See the [official documentation](https://docs.pi-hole.net/ftldns/configfile/) to configure FTL.

**Tip:** If Pi-hole is running on a [solid state drive](/index.php/Solid_state_drive "Solid state drive") (single-board computers SD, SSD, M.2/NVMe device, etc...) it is recommended to set the `DBINTERVAL` value to at least `60.0` to minimize writes to the database.

**Note:** Since Pi-hole-FTL 4.0, a private fork of dnsmasq is integrated in the FTL sub-project. The original [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) package is now conflicting with [pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/) and will be uninstalled when upgrading from a previous version. It's still possible to use the previous dnsmasq config files, just ensure that `conf-dir=/etc/dnsmasq.d/,*.conf` in the original `/etc/dnsmasq.conf` is not commented out.

#### Web server

Optionally choose a web server for the Pi-hole web interface.

**Note:** Pi-hole does not strictly require a web interface as many commands are possible via the CLI interface.

Example config files that work out-of-the-box are provided for both [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) and [nginx](https://www.archlinux.org/packages/?name=nginx). Other web servers can also run the WebUI, but are currently unsupported.

Install [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite) and enable the relevant extensions detailed here:

 `/etc/php/php.ini` 
```
[...]
extension=pdo_sqlite
[...]
extension=sockets
extension=sqlite3
[...]
```

For security reasons, one can populate the [PHP open_basedir](/index.php/PHP#Configuration "PHP") directive however, the Pi-hole administration web interface will need access to following files and directories:

```
/srv/http/pihole
/run/pihole-ftl/pihole-FTL.port
/run/log/pihole/pihole.log
/run/log/pihole-ftl/pihole-FTL.log
/etc/pihole
/etc/hosts
/etc/hostname
/etc/dnsmasq.d/02-pihole-dhcp.conf
/etc/dnsmasq.d/03-pihole-wildcard.conf
/etc/dnsmasq.d/04-pihole-static-dhcp.conf
/proc/meminfo
/proc/cpuinfo
/sys/class/thermal/thermal_zone0/temp
/tmp

```

##### Lighttpd

[Install](/index.php/Install "Install") [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) and [php-cgi](https://www.archlinux.org/packages/?name=php-cgi).

Copy the package provided default config for Pi-hole:

```
# cp /usr/share/pihole/configs/lighttpd.example.conf /etc/lighttpd/lighttpd.conf

```

[Enable](/index.php/Enable "Enable") `lighttpd.service` and re/start it.

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

#### /etc/hosts

[filesystem](https://www.archlinux.org/packages/?name=filesystem) ships with an empty `/etc/hosts` file which is known to prevent Pi-hole from fetching block lists. One must append the following to this file to insure correct operation, noting that *ip.address.of.pihole* should be the actual IP address of the machine running Pi-hole (eg 192.168.1.250) and *myhostname* should be the actual hostname of the machine running Pi-hole.

```
127.0.0.1              localhost
ip.address.of.pihole   pi.hole myhostname

```

For more, see [Issue#1800](https://github.com/pi-hole/pi-hole/issues/1800).

### Making devices use Pi-hole

[The upstream documentation](https://discourse.pi-hole.net/t/how-do-i-configure-my-devices-to-use-pi-hole-as-their-dns-server/245) documents four different methods:

1.  Define Pi-hole's IP address as the only DNS entry in the router
2.  Advertise Pi-hole's IP address via dnsmasq in the router (if supported)
3.  Manually configure each device to use the Pi-hole as their DNS server
4.  [Use Pi-hole's built-in DHCP server](https://discourse.pi-hole.net/t/how-do-i-use-pi-holes-built-in-dhcp-server-and-why-would-i-want-to/3026)

#### Troubleshooting

*   If you setup a DHCP-based method and ad blocking does not work on a device, it might still have an outdated DHCP lease. If you do not know how to renew your DHCP lease, try restarting the device.
*   A simple check to see that the router is setup correctly is to first renew a DHCP lease, then inspect the contents of `/etc/resolv.conf` on a Linux client. One should see the IP address of the Pi-hole box, not the IP address of the router.
*   If you are having problems with method 2, try disabling the `dns-rebind` feature on the router (if present).

### Using Pi-hole together with OpenVPN

An [OpenVPN](/index.php/OpenVPN "OpenVPN") server can be configured to advertise a Pi-hole instance to its clients. Add the following two lines to your `/etc/openvpn/server/server.conf`:

```
push "redirect-gateway def1 bypass-dhcp"
push "dhcp-option DNS *Pi-Hole-IP*"

```

If it still does not work, try creating a file `/etc/dnsmasq.d/00-openvpn.conf` with the following content:

```
interface=tun0

```

It may be necessary to make `dnsmasq` listen on `tun0`.

### Password-protect web interface

To password-protect the Pi-hole web interface, run the following command and enter your password:

```
pihole -a -p

```

To disable the password protection set a blank password.

## Pi-hole Standalone

**Note:** [pi-hole-standalone](https://aur.archlinux.org/packages/pi-hole-standalone/) is not officially supported by the Pi-hole project.

The Arch Linux Pi-hole Standalone variant is born from the need to use Pi-hole services in a mobile context. [Sky-hole article](http://dlaa.me/blog/post/skyhole) was inspirational.

### Installation

[Install](/index.php/Install "Install") the [pi-hole-standalone](https://aur.archlinux.org/packages/pi-hole-standalone/) package. The Pi-hole standalone package install a statically enabled timer (and relative service) will weekly update Pi-hole blacklisted servers list. If you do not like default timer timings (from upstrem project) you can, of course, [edit](/index.php/Edit "Edit") it or preventing from being executed by [masking](/index.php/Systemd#Using_units "Systemd") it. You need to manually start `pi-hole-gravity.timer` or simply reboot after your configuration is finished.

### Initial configuration

#### Dnsmasq

Ensure that the following line in `/etc/dnsmasq.conf` is uncommented:

```
conf-dir=/etc/dnsmasq.d/,*.conf

```

[Enable](/index.php/Enable "Enable") `dnsmasq.service` and re/start it.

#### Configuring host name resolution

The Pi-hole standalone package to work properly requires that a unique DNS is set on your machine. That DNS address need to be your machine itself. This can be done in several ways.

##### Manually

If no service on your machine automatically handles the `/etc/resolv.conf` file, you can easily edit it to insert the following **unique** item `nameserver`:

 `/etc/resolv.conf` 
```
[...]
nameserver 127.0.0.1

```

**Note:** No other `nameserver` items need to be present in the config file.

##### Openresolve

It is likely that is the [openresolv](https://www.archlinux.org/packages/?name=openresolv) service to handle `/etc/resolv.conf` if you use a network connection manager such as [netctl](/index.php/Netctl "Netctl") or [NetworkManager](/index.php/NetworkManager "NetworkManager"). If it is your case, you must force [openresolv](https://www.archlinux.org/packages/?name=openresolv) to use **localhost** as name server.
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

By default Pi-hole uses the Google DNS server. You can change which DNS servers Pi-hole uses with:

```
$ pihole -a setdns *server*

```

You can specify multiple DNS servers by separating their addresses with commas.

For server package only, you can manage this via web interface ([http://pi.hole](http://pi.hole)) going to *Settings* and adding desired DNS servers in *Upstream DNS Servers* section. *Save* to apply changes.

### Forced update of ad-serving domains list

If you need to update the blocked domain list, on the machine running Pi-hole you can execute

```
$ pihole -g

```

or, server package only, via web interface ([http://pi.hole](http://pi.hole)) go to *Tools/Update Lists* and execute *Update Lists*.

### Temporarily disable Pi-hole

Pi-hole can be easily paused through its web interface ([http://pi.hole](http://pi.hole)): go to *Disable* and choose the suspension option that best suits your case. It is possible via CLI too by executing

```
$ pihole disable [time]

```

If you leave `time` blank disabling will be permanent until later manual reenabling. `time` can be expressed in seconds or minutes with syntax #s and #m. For example, to disable Pi-hole for 5 minutes only, you can execute

```
$ pihole disable 5m

```

At any time you can reenable Pi-hole by executing

```
$ pihole enable

```

or, via web interface, clicking on *Enable*.

## Troubleshooting

### Data loss on reboot

Systems without a [RTC](/index.php/RTC "RTC") such as some ARM devices will likely experience loss of data in the query log upon rebooting. When systems lacking a [RTC](/index.php/RTC "RTC") boot, the time is set *after* the network and resolver come up. Aspects of Pi-hole can get started before this happens leading to the data loss. An incorrectly set [RTC](/index.php/RTC "RTC") can also cause problems. See: [Installation_guide#Time_zone](/index.php/Installation_guide#Time_zone "Installation guide") and [System_time](/index.php/System_time "System time").

For devices lacking a [RTC](/index.php/RTC "RTC"): A hacky work-around for this is to use [Systemd#Drop-in_files](/index.php/Systemd#Drop-in_files "Systemd") against `pihole-FTL.service` wherein a delay is built in calling `/usr/bin/sleep x` in a `ExecStartPre` statement. Note that the value of "x" in the sleep time depends on how long your specific hardware takes to establish the time sync.

[Issue#11008](https://github.com/systemd/systemd/issues/11008) against systemd-timesyncd is currently preventing the use of the *time-sync.target* to automate this.

## See also

*   [Pi-hole homepage](https://pi-hole.net/)
*   [Pi-hole GitHub page](https://github.com/pi-hole/pi-hole)
*   [Pi-hole FTL GitHub page](https://github.com/pi-hole/FTL)
*   [Sky-Hole, the basic idea under Pi-hole standalone](http://dlaa.me/blog/post/skyhole)