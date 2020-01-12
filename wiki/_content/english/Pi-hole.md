Related articles

*   [dnsmasq](/index.php/Dnsmasq "Dnsmasq")
*   [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution")
*   [lighttpd](/index.php/Lighttpd "Lighttpd")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [nginx](/index.php/Nginx "Nginx")
*   [OpenVPN](/index.php/OpenVPN "OpenVPN")
*   [WireGuard](/index.php/WireGuard "WireGuard")

[Pi-hole](https://pi-hole.net/) project is a [DNS sinkhole](https://en.wikipedia.org/wiki/DNS_sinkhole "wikipedia:DNS sinkhole") that compiles a blocklist of domains from multiple third-party sources. Pi-hole uses [pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/) ([dnsmasq](/index.php/Dnsmasq "Dnsmasq") fork) to seamlessly drop any and all requests for domains in its blocklist. Running it effectively deploys network-wide ad-blocking without the need to configure individual clients. The package comes with an optional web and a CLI interfaces.

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
            *   [2.2.2.2 Set-up lighttpd](#Set-up_lighttpd)
        *   [2.2.3 Update hosts file](#Update_hosts_file)
    *   [2.3 Making devices use Pi-hole](#Making_devices_use_Pi-hole)
*   [3 Pi-hole standalone](#Pi-hole_standalone)
    *   [3.1 Installation](#Installation_2)
    *   [3.2 Configuration](#Configuration_2)
        *   [3.2.1 Timer](#Timer)
        *   [3.2.2 FTL](#FTL_2)
    *   [3.3 Usage](#Usage)
*   [4 Usage](#Usage_2)
    *   [4.1 Using web interface](#Using_web_interface)
    *   [4.2 Using CLI](#Using_CLI)
        *   [4.2.1 Pi-hole DNS management](#Pi-hole_DNS_management)
        *   [4.2.2 Forced update of ad-serving domains list](#Forced_update_of_ad-serving_domains_list)
        *   [4.2.3 Temporarily disable Pi-hole](#Temporarily_disable_Pi-hole)
*   [5 Tips & Tricks](#Tips_&_Tricks)
    *   [5.1 Password-protected web interface](#Password-protected_web_interface)
    *   [5.2 DNS over HTTPS](#DNS_over_HTTPS)
    *   [5.3 Optimise for solid state drives](#Optimise_for_solid_state_drives)
    *   [5.4 Use with VPN server](#Use_with_VPN_server)
        *   [5.4.1 OpenVPN](#OpenVPN)
        *   [5.4.2 WireGuard](#WireGuard)
    *   [5.5 Nginx instead of Lighttpd](#Nginx_instead_of_Lighttpd)
    *   [5.6 Additional blocklists](#Additional_blocklists)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Data loss on reboot](#Data_loss_on_reboot)
    *   [6.2 Failed to start Pi-hole FTLDNS engine](#Failed_to_start_Pi-hole_FTLDNS_engine)
    *   [6.3 DNSMasq package conflict](#DNSMasq_package_conflict)
    *   [6.4 Unknown Status and changes not being saved](#Unknown_Status_and_changes_not_being_saved)
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

It is a DNS resolver/forwarder and a database-like wrapper/API that provides long-term storage of requests which users can query through the "long-term data" section of the WebGUI. Data are collected and stored in two places:

1.  Daily data are stored in RAM and are captured in real-time within `/run/log/pihole/pihole.log`
2.  Historical data (i.e. over multiple days/weeks/months) are stored on the file system `/etc/pihole/pihole-FTL.db` written out at a user-specified interval.

`pihole-FTL.service` is statically enabled; re/start it. For FTL configuration, see [upstream documentation](https://docs.pi-hole.net/ftldns/configfile/).

**Note:** Starting `pihole-FTL.service` is likelly going to fail. See [#Failed to start Pi-hole FTLDNS engine](#Failed_to_start_Pi-hole_FTLDNS_engine).

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

##### Set-up lighttpd

**Tip:** You can use Nginx web server instead. See [#Nginx instead of Lighttpd](#Nginx_instead_of_Lighttpd).

[Install](/index.php/Install "Install") [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) and [php-cgi](https://www.archlinux.org/packages/?name=php-cgi).

Copy the package provided default config for Pi-hole:

```
# cp /usr/share/pihole/configs/lighttpd.example.conf /etc/lighttpd/lighttpd.conf

```

[Enable](/index.php/Enable "Enable") `lighttpd.service` and re/start it.

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

**Tip:** Pi-Hole hosting device can also make use of Pi-Hole. Just change DNS settings to only IP address `127.0.0.1`.

## Pi-hole standalone

### Installation

[Install](/index.php/Install "Install") the [pi-hole-standalone](https://aur.archlinux.org/packages/pi-hole-standalone/) package.

### Configuration

#### Timer

The Pi-hole standalone package install a statically enabled timer (and relative service) will weekly update Pi-hole blacklisted servers list. If you do not like default timer timings (from upstrem project) you can, of course, [edit](/index.php/Edit "Edit") it or preventing from being executed by [masking](/index.php/Systemd#Using_units "Systemd") it. You need to manually start `pi-hole-gravity.timer` or simply reboot after your configuration is finished.

#### FTL

See [#FTL](#FTL).

### Usage

Change the computer's network settings so the only DNS server in use is `127.0.0.1`.

## Usage

Both standalone and server versions can be controlled via CLI, but only server version can be controlled via web interface.

**Note:** Web interface is so powerful that you don't need CLI at all.

### Using web interface

Go to [pi.hole](http://pi.hole/admin/) or `<Pi-Hole IP address>/admin/` to access web interface.

### Using CLI

#### Pi-hole DNS management

By default Pi-hole uses the Google DNS server. You can change which DNS servers Pi-hole uses with:

```
$ pihole -a setdns *server*

```

You can specify multiple DNS servers by separating their addresses with commas.

#### Forced update of ad-serving domains list

If you need to update the blocked domain list, on the machine running Pi-hole you can execute

```
$ pihole -g

```

#### Temporarily disable Pi-hole

Pi-hole can be paused via CLI by executing:

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

## Tips & Tricks

### Password-protected web interface

You might want to password-protect the Pi-hole web interface. Run the following command and enter your password:

```
pihole -a -p

```

To disable the password protection, set a blank password.

### DNS over HTTPS

Pi-Hole can be configured to use [DNS over HTTPS](/index.php/DNS_over_HTTPS "DNS over HTTPS"). Run a local DNS-server such as [cloudflared](/index.php/DNS_over_HTTPS#cloudflared "DNS over HTTPS") using the privacy-first DNS [1.1.1.1](https://1.1.1.1/) by Cloudflare, and use `127.0.0.1#5053` as a DNS server in Pi-Hole.

### Optimise for solid state drives

If Pi-hole is running on a [solid state drive](/index.php/Solid_state_drive "Solid state drive") (SD card, SSD etc..) it is recommended to uncomment the `DBINTERVAL` value and change it to at least `60.0` to minimize writes to the database:

 `/etc/pihole/pihole-FTL.conf` 
```

...

## Database Interval
## How often do we store queries in FTL's database -minutes-?
## See: https://docs.pi-hole.net/ftldns/database/
## Options: number of minutes
DBINTERVAL=60.0

...

```

After changes have been performed, [restart](/index.php/Restart "Restart") `pihole-FTL.service`.

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

### Nginx instead of Lighttpd

This is [unofficial, community-supported configuration](https://docs.pi-hole.net/guides/nginx-configuration/). Make sure that PHP is set-up (see [#Set-up PHP](#Set-up_PHP)) and lighttpd server is inactive.

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

### Additional blocklists

Pi-Hole was intended to block ads, but it can also be used to block other unwanted content:

1.  Tracking domains
2.  Malware domains
3.  Piracy sites
4.  Fake news sites
5.  Phishing sites

**Note:** Pi-Hole blocklists must contain **domains**. Some blocklists might contain IP addresses of 127.0.0.1 and domain combination - this format is accepted by Pi-Hole.

There are many sources providing these blocklists. Some examples: [hosts-file.net](https://hosts-file.net/?s=Download), [firebog.net](https://firebog.net/) and [dbl.oisd.nl](https://www.reddit.com/comments/bppug1).

## Troubleshooting

### Data loss on reboot

Systems without a [RTC](/index.php/RTC "RTC") such as some ARM devices will likely experience loss of data in the query log upon rebooting. When systems lacking a [RTC](/index.php/RTC "RTC") boot, the time is set *after* the network and resolver come up. Aspects of Pi-hole can get started before this happens leading to the data loss. An incorrectly set [RTC](/index.php/RTC "RTC") can also cause problems. See: [Installation guide#Time zone](/index.php/Installation_guide#Time_zone "Installation guide") and [System time](/index.php/System_time "System time").

For devices lacking a [RTC](/index.php/RTC "RTC"): A hacky work-around for this is to use [Systemd#Drop-in files](/index.php/Systemd#Drop-in_files "Systemd") against `pihole-FTL.service` wherein a delay is built in calling `/usr/bin/sleep x` in a `ExecStartPre` statement. Note that the value of "x" in the sleep time depends on how long your specific hardware takes to establish the time sync.

[Issue#11008](https://github.com/systemd/systemd/issues/11008) against systemd-timesyncd is currently preventing the use of the *time-sync.target* to automate this.

### Failed to start Pi-hole FTLDNS engine

It might be that `systemd-resolved.service` already occupied port 53, which is required for `pihole-FTL.service`. To resolve this, [stop and disable](/index.php/Systemd#Using_units "Systemd") `systemd-resolved.service` and [restart](/index.php/Restart "Restart") `pihole-FTL.service`.

### DNSMasq package conflict

Since Pi-hole-FTL 4.0, a private fork of dnsmasq is integrated in the FTL sub-project. The original [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) package is now conflicting with [pi-hole-ftl](https://aur.archlinux.org/packages/pi-hole-ftl/) and will be uninstalled when upgrading from a previous version. It's still possible to use the previous dnsmasq config files, just ensure that `conf-dir=/etc/dnsmasq.d/,*.conf` in the original `/etc/dnsmasq.conf` is not commented out.

### Unknown Status and changes not being saved

The issue, as seen in Task#63704, is with SystemD-created user `http`, which is created in expired state. To fix it, run:

```
 sudo chage --expiredate -1 http

```

## See also

*   [Pi-hole homepage](https://pi-hole.net/)
*   [Pi-hole GitHub page](https://github.com/pi-hole/pi-hole)
*   [Pi-hole FTL GitHub page](https://github.com/pi-hole/FTL)
*   [Sky-Hole, the basic idea under Pi-hole standalone](http://dlaa.me/blog/post/skyhole)