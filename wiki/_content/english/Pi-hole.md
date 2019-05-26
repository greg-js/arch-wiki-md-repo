Related articles

*   [dnsmasq](/index.php/Dnsmasq "Dnsmasq")
*   [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution")
*   [lighttpd](/index.php/Lighttpd "Lighttpd")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [nginx](/index.php/Nginx "Nginx")
*   [OpenVPN](/index.php/OpenVPN "OpenVPN")
*   [WireGuard](/index.php/WireGuard "WireGuard")

[Pi-hole](https://pi-hole.net/) is a [DNS sinkhole](https://en.wikipedia.org/wiki/DNS_sinkhole "wikipedia:DNS sinkhole") that compiles a blocklist of domains known to host advertisements and malware from multiple third-party sources. Pi-hole uses [dnsmasq](/index.php/Dnsmasq "Dnsmasq") to seamlessly drop any and all requests for domains in its blocklist. Running it effectively deploys network-wide ad-blocking without the need to configure individual clients. The package comes with a web and a CLI interface.

**Note:** Pi-hole on Arch Linux is not officially supported by the Pi-hole project.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overview](#Overview)
*   [2 Pi-hole server](#Pi-hole_server)
    *   [2.1 Installation](#Installation)
    *   [2.2 Configuration](#Configuration)
        *   [2.2.1 FTL](#FTL)
        *   [2.2.2 Web interface](#Web_interface)
            *   [2.2.2.1 Set-up PHP](#Set-up_PHP)
            *   [2.2.2.2 Set-up web server](#Set-up_web_server)
                *   [2.2.2.2.1 Lighttpd](#Lighttpd)
                *   [2.2.2.2.2 Nginx](#Nginx)
            *   [2.2.2.3 Protect with password](#Protect_with_password)
        *   [2.2.3 Update hosts file](#Update_hosts_file)
    *   [2.3 Making devices use Pi-hole](#Making_devices_use_Pi-hole)
*   [3 Pi-hole standalone](#Pi-hole_standalone)
    *   [3.1 Installation](#Installation_2)
    *   [3.2 Configuration](#Configuration_2)
        *   [3.2.1 FTL](#FTL_2)
        *   [3.2.2 Configuring host name resolution](#Configuring_host_name_resolution)
            *   [3.2.2.1 Manually](#Manually)
            *   [3.2.2.2 Openresolve](#Openresolve)
*   [4 Using Pi-hole](#Using_Pi-hole)
    *   [4.1 Pi-hole DNS management](#Pi-hole_DNS_management)
    *   [4.2 Forced update of ad-serving domains list](#Forced_update_of_ad-serving_domains_list)
    *   [4.3 Temporarily disable Pi-hole](#Temporarily_disable_Pi-hole)
*   [5 Tips & Tricks](#Tips_&_Tricks)
    *   [5.1 Cloudflared DNS service](#Cloudflared_DNS_service)
    *   [5.2 Use with VPN server](#Use_with_VPN_server)
        *   [5.2.1 OpenVPN](#OpenVPN)
        *   [5.2.2 WireGuard](#WireGuard)
    *   [5.3 Additional blocklists](#Additional_blocklists)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Data loss on reboot](#Data_loss_on_reboot)
    *   [6.2 Failed to start Pi-hole FTLDNS engine](#Failed_to_start_Pi-hole_FTLDNS_engine)
*   [7 See also](#See_also)

## Overview

There are 2 versions of Pi-Hole available for Arch Linux:

*   [#Pi-hole server](#Pi-hole_server) - This is default and well-known Pi-Hole server that most users are looking for. It is designed to be used as a DNS server for other devices on the LAN.
*   [#Pi-hole standalone](#Pi-hole_standalone) - This is alternative lightweight Pi-Hole installation, designed for a mobile context. It is intended to be used on the same device (e.g. laptop), where no external and centralised Pi-Hole server is available. It also has no web interface and automatically updates.

## Pi-hole server

### Installation

[Install](/index.php/Install "Install") the [pi-hole-server](https://aur.archlinux.org/packages/pi-hole-server/) package.

### Configuration

#### FTL

The [Pi-hole FTL engine](https://github.com/pi-hole/FTL) ([pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/)) is a dependency of the Pi-hole main project.

FTL is a DNS resolver/forwarder and a database-like wrapper/API that provides long-term storage of requests which users can query through the "long-term data" section of the WebGUI. To be clear, data are collected and stored in two places:

1.  Daily data are stored in RAM and are captured in real-time within `/run/log/pihole/pihole.log`
2.  Historical data (i.e. over multiple days/weeks/months) are stored on the file system `/etc/pihole/pihole-FTL.db` written out at a user-specified interval.

`pihole-FTL.service` is statically enabled; re/start it. See the [official documentation](https://docs.pi-hole.net/ftldns/configfile/) to configure FTL.

**Tip:** If Pi-hole is running on a [solid state drive](/index.php/Solid_state_drive "Solid state drive") (single-board computers SD, SSD, M.2/NVMe device, etc...) it is recommended to set the `DBINTERVAL` value to at least `60.0` to minimize writes to the database.

**Note:** Since Pi-hole-FTL 4.0, a private fork of dnsmasq is integrated in the FTL sub-project. The original [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) package is now conflicting with [pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/) and will be uninstalled when upgrading from a previous version. It's still possible to use the previous dnsmasq config files, just ensure that `conf-dir=/etc/dnsmasq.d/,*.conf` in the original `/etc/dnsmasq.conf` is not commented out.

#### Web interface

Pi-hole has a very powerful, user friendly, but completely optional web interface. It allows not only to change settings, but analyse and visualise DNS queries performed by other devices.

##### Set-up PHP

Install [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite) ([php](https://www.archlinux.org/packages/?name=php) will be installed automatically) and enable the relevant extensions detailed here:

 `/etc/php/php.ini` 
```
[...]
extension=pdo_sqlite
[...]
extension=sockets
extension=sqlite3
[...]
```

For security reasons, one can optionally populate the [PHP open_basedir](/index.php/PHP#Configuration "PHP") directive however, the Pi-hole administration web interface will need access to following files and directories:

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

##### Set-up web server

Example config files that work out-of-the-box are provided for both [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) and [nginx](https://www.archlinux.org/packages/?name=nginx). Other web servers can also be used, but are currently unsupported.

###### Lighttpd

[Install](/index.php/Install "Install") [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) and [php-cgi](https://www.archlinux.org/packages/?name=php-cgi).

Copy the package provided default config for Pi-hole:

```
# cp /usr/share/pihole/configs/lighttpd.example.conf /etc/lighttpd/lighttpd.conf

```

[Enable](/index.php/Enable "Enable") `lighttpd.service` and re/start it.

###### Nginx

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

##### Protect with password

Optionally, you might want to password-protect the Pi-hole web interface. Run the following command and enter your password:

```
pihole -a -p

```

To disable the password protection, set a blank password.

#### Update hosts file

[filesystem](https://www.archlinux.org/packages/?name=filesystem) ships with an empty `/etc/hosts` file which is known to prevent Pi-hole from fetching block lists. One must append the following to this file to ensure correct operation, noting that *ip.address.of.pihole* should be the actual IP address of the machine running Pi-hole (eg 192.168.1.250) and *myhostname* should be the actual hostname of the machine running Pi-hole.

```
127.0.0.1              localhost
ip.address.of.pihole   pi.hole myhostname

```

For more, see [Issue#1800](https://github.com/pi-hole/pi-hole/issues/1800).

### Making devices use Pi-hole

To use Pi-Hole, make sure that your devices use Pi-Hole's IP address as their only DNS server. To accomplish this, there are generally 2 methods to make it happen:

1.  In router's LAN DHCP settings, set Pi-Hole's IP address as the only DNS server available for connected devices.
2.  Manually configure each device to use Pi-Hole's IP address as their only DNS server.

**Note:** Some routers (or even ISPs) do not allow to change LAN DNS settings, so you might want to disable router's DHCP server and use [Pi-Hole's built in DHCP server instead](https://discourse.pi-hole.net/t/how-do-i-use-pi-holes-built-in-dhcp-server-and-why-would-i-want-to), as it is automatically configured to use Pi-Hole.

More information about making other devices use Pi-Hole can be found at [upstream documentation](https://discourse.pi-hole.net/t/how-do-i-configure-my-devices-to-use-pi-hole-as-their-dns-server/245).

## Pi-hole standalone

### Installation

[Install](/index.php/Install "Install") the [pi-hole-standalone](https://aur.archlinux.org/packages/pi-hole-standalone/) package. The Pi-hole standalone package install a statically enabled timer (and relative service) will weekly update Pi-hole blacklisted servers list. If you do not like default timer timings (from upstrem project) you can, of course, [edit](/index.php/Edit "Edit") it or preventing from being executed by [masking](/index.php/Systemd#Using_units "Systemd") it. You need to manually start `pi-hole-gravity.timer` or simply reboot after your configuration is finished.

### Configuration

#### FTL

Pi-hole-standalone now uses FTL as hostnames resolver. Since Pi-hole 4.0, a private fork of dnsmasq is integrated in the FTL sub-project. The original [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) package is now conflicting with [pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/) and will be uninstalled when upgrading from a previous version. It's still possible to use the previous dnsmasq config files.

Ensure that the following line in `/etc/dnsmasq.conf` is uncommented:

```
conf-dir=/etc/dnsmasq.d/,*.conf

```

If you do not have `/etc/dnsmasq.conf` file at all, you can use the example conf file within the package (`/usr/share/pihole/configs/dnsmasq.example.conf`) that will work out of box.

`pihole-FTL.service` is statically enabled; re/start it.

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

## Tips & Tricks

### Cloudflared DNS service

Pi-Hole can be configured to use privacy-first DNS [1.1.1.1](https://1.1.1.1/) by [Cloudflare](https://www.cloudflare.com/) over HTTPS (DOH). Install [cloudflared-bin](https://aur.archlinux.org/packages/cloudflared-bin/) and create the following file:

 `/etc/cloudflared/cloudflared.yml` 
```
proxy-dns: true
proxy-dns-upstream:
 - https://1.0.0.1/dns-query
 - https://1.1.1.1/dns-query
 - https://2606:4700:4700::1111/dns-query
 - https://2606:4700:4700::1001/dns-query
proxy-dns-port: 5053
proxy-dns-address: 0.0.0.0
logfile: /var/log/cloudflared.log

```

Then [start and enable](/index.php/Start/enable "Start/enable") `cloudflared@cloudflared.service`. Now you can use `127.0.0.1#5053` as a DNS server in Pi-Hole.

### Use with VPN server

Pi-Hole can be used by connected VPN clients.

#### OpenVPN

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

#### WireGuard

[WireGuard](/index.php/WireGuard "WireGuard") clients can be configured to use Pi-Hole DNS server. In the client configuration file, specify the following line:

```
DNS = *Pi-Hole-IP*

```

See more information in [WireGuard#Client config](/index.php/WireGuard#Client_config "WireGuard").

### Additional blocklists

Pi-Hole was intended to block ads, but it can also be used to block other unwanted content:

1.  Tracking domains
2.  Malware domains
3.  Piracy sites
4.  Fake news sites
5.  Phishing sites

**Note:** Pi-Hole blocklists must contain **domains**. Some blocklists might contain IP addresses of 127.0.0.1 and domain combination - this format is accepted by Pi-Hole.

There are many websites providing these blocklists, like [this](https://hosts-file.net/?s=Download) or [this](https://firebog.net/).

## Troubleshooting

### Data loss on reboot

Systems without a [RTC](/index.php/RTC "RTC") such as some ARM devices will likely experience loss of data in the query log upon rebooting. When systems lacking a [RTC](/index.php/RTC "RTC") boot, the time is set *after* the network and resolver come up. Aspects of Pi-hole can get started before this happens leading to the data loss. An incorrectly set [RTC](/index.php/RTC "RTC") can also cause problems. See: [Installation guide#Time zone](/index.php/Installation_guide#Time_zone "Installation guide") and [System time](/index.php/System_time "System time").

For devices lacking a [RTC](/index.php/RTC "RTC"): A hacky work-around for this is to use [Systemd#Drop-in files](/index.php/Systemd#Drop-in_files "Systemd") against `pihole-FTL.service` wherein a delay is built in calling `/usr/bin/sleep x` in a `ExecStartPre` statement. Note that the value of "x" in the sleep time depends on how long your specific hardware takes to establish the time sync.

[Issue#11008](https://github.com/systemd/systemd/issues/11008) against systemd-timesyncd is currently preventing the use of the *time-sync.target* to automate this.

### Failed to start Pi-hole FTLDNS engine

It might be that `systemd-resolved.service` already occupied port 53, which is required for `pihole-FTL.service`. To resolve this, [disable](/index.php/Disable "Disable") `systemd-resolved.service` and [restart](/index.php/Restart "Restart") `pihole-FTL.service`.

## See also

*   [Pi-hole homepage](https://pi-hole.net/)
*   [Pi-hole GitHub page](https://github.com/pi-hole/pi-hole)
*   [Pi-hole FTL GitHub page](https://github.com/pi-hole/FTL)
*   [Sky-Hole, the basic idea under Pi-hole standalone](http://dlaa.me/blog/post/skyhole)