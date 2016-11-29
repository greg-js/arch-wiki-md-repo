Netatalk is a free, open-source implementation of the Apple Filing Protocol (AFP). It allows Unix-like operating systems to serve as file servers for Macintosh computers.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Guest access](#Guest_access)
*   [3 IP Tables](#IP_Tables)
*   [4 Enable Bonjour/Zeroconf](#Enable_Bonjour.2FZeroconf)

## Installation

Netatalk can be [installed](/index.php/Install "Install") with the [netatalk](https://aur.archlinux.org/packages/netatalk/) package.

## Configuration

Enable and/or start `netatalk.service` [using systemd](/index.php/Systemd#Using_units "Systemd").

Besides the configuration files that are installed (and checked during upgrade), netatalk may generate two files `/etc/netatalk/afp_signature.conf` or `/var/state/netatalk/afp_signature.conf` which holds the system UUID, and `/etc/netatalk/afp_voluuid.conf` or `/var/state/netatalk/afp_voluuid.conf` which holds volume UUIDs for TimeMachine. These files may remain after package removal and should be kept in most cases to disambiguate the services broadcast over the local network.

Netatalk 3.x uses a single configuration file, `/etc/afp.conf`. See `man afp.conf` and the following example (make sure processes have write access to `afpd.log`):

 `/etc/afp.conf` 
```
[Global]
 mimic model = TimeCapsule6,106
 log level = default:warn
 log file = /var/log/afpd.log
 hosts allow = 192.168.1.0/16

[Homes]
 basedir regex = /home

[TimeMachine]
 path = /mnt/timemachine
 valid users = tmuser
 time machine = yes

[Shared Media]
 path = /srv/share/media
 valid users = joe sam

```

**Warning:** Avoid using symbolic links in `afp.conf`

### Guest access

In order to allow guest **read-only** access to your shared folders, add following line to the `[Global]` section:

 `/etc/afp.conf` 
```
[Global]
uam list = uams_guest.so

```

To allow guest **read/write** access, first, allow read-only access as in the previous example and then add following lines to a particular share section:

 `/etc/afp.conf` 
```
[Your Share]
path = /mnt/public/share
rwlist = nobody

```

## IP Tables

If you use the [iptables](/index.php/Iptables "Iptables") package for firewall services, consider adding the following: (replace `-I` with `-A` as necessary)

 `Bonjour/Zeroconf` 
```
iptables -I INPUT -p udp --dport mdns -d 224.0.0.251 -j ACCEPT
iptables -I OUTPUT -p udp --dport mdns -d 224.0.0.251 -j ACCEPT
```
 `AFP`  `iptables -I INPUT -p tcp --dport afpovertcp -j ACCEPT`  `SLP` 
```
iptables -I INPUT -p tcp --dport slp -j ACCEPT
iptables -I OUTPUT -p tcp --dport slp -j ACCEPT
iptables -I INPUT -p udp --dport slp -j ACCEPT
iptables -I OUTPUT -p udp --dport slp -j ACCEPT
```
 `AppleTalk` 
```
iptables -I INPUT -p tcp -m multiport --dport at-rtmp,at-nbp,at-echo,at-zis -j ACCEPT
iptables -I OUTPUT -p tcp -m multiport --dport at-rtmp,at-nbp,at-echo,at-zis -j ACCEPT
```

## Enable Bonjour/Zeroconf

Bonjour/Zeroconf is now a requirement of netatalk and is compiled by default. No configuration is necessary, netatalk will register its own services using the dbus link. Make sure you set `-mimicmodel` to the desired string (see `/System/Library/CoreServices/CoreTypes.bundle/Contents/Info.plist` on a Mac for a full list).

You may need to enable and/or start `avahi-daemon.service` [using systemd](/index.php/Systemd#Using_units "Systemd") if it is not running yet.