Hurricane Electric offers a free [tunnel broker](http://tunnelbroker.net/) service that is relatively painless to use under Arch if you wish to add IPv6 connectivity to an IPv4-only host.

These instructions work for [SixXS](http://www.sixxs.net/) tunnels as well.

## Contents

*   [1 Registering for a tunnel](#Registering_for_a_tunnel)
*   [2 Setting up SixXS tunnel](#Setting_up_SixXS_tunnel)
*   [3 Setting up Hurricane Electric tunnel](#Setting_up_Hurricane_Electric_tunnel)
*   [4 systemd-networkd](#systemd-networkd)
*   [5 Using the tunneling with dynamic IPv4 IP](#Using_the_tunneling_with_dynamic_IPv4_IP)

## Registering for a tunnel

It is not that hard to do. Feel free to fill in the directions here if something seems tricky, but otherwise just go the tunnel broker site and complete the registration.

## Setting up SixXS tunnel

First, you need to have [aiccu](https://www.archlinux.org/packages/?name=aiccu) and [radvd](https://www.archlinux.org/packages/?name=radvd) installed.

Now edit `/etc/aiccu.conf` and fill in your data. If you have several tunnels, you need to also supplement the tunnel_id option in the file. The following is an example for a dynamic ayiay tunnel.

```
username <username>
password <password>
protocol tic
server tic.sixxs.net
ipv6_interface sixxs
automatic true
requiretls true
pidfile /var/run/aiccu.pid
defaultroute true
makebeats true
behindnat true

```

Test the configuration now with:

```
# systemctl start aiccu

```

If it works you can add a dispatcher script for the NetworkManager, so it will start whenever your network is ready. Note that enabling the service via systemd will not work, as the network will not be ready on boot. Please see [FS#38221](https://bugs.archlinux.org/task/38221) for more details.

 `/etc/NetworkManager/dispatcher.d/99-aiccu` 
```
#!/bin/bash
# -*- coding: utf-8 -*-
# Manual Running/Test: ./99-aiccu eth0 up
if [ -e /sys/fs/cgroup/systemd ]; then
  case "$2" in
    up)
      systemctl start aiccu.service
      ;;
    down)
      systemctl stop aiccu.service
      ;;
  esac
fi
```

Configuring radvd and LAN side IP of the router: See [Router](/index.php/Router#IPv6 "Router").

## Setting up Hurricane Electric tunnel

Create the following systemd unit, replacing bold text with the IP addresses you got from HE:

**Note:** If you are behind a NAT (typical home router setup), use your *local* IPv4 address for `**Client_IPv4_Address**`, e.g. `192.168.0.2`.
 `/etc/systemd/system/he-ipv6.service` 
```
[Unit]
Description=he.net IPv6 tunnel
After=network.target

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/bin/ip tunnel add he-ipv6 mode sit remote **Server_IPv4_Address** local **Client_IPv4_Address** ttl 255
ExecStart=/usr/bin/ip link set he-ipv6 up mtu 1480
ExecStart=/usr/bin/ip addr add **Client_IPv6_Address** dev he-ipv6
ExecStart=/usr/bin/ip -6 route add ::/0 dev he-ipv6
ExecStop=/usr/bin/ip -6 route del ::/0 dev he-ipv6
ExecStop=/usr/bin/ip link set he-ipv6 down
ExecStop=/usr/bin/ip tunnel del he-ipv6

[Install]
WantedBy=multi-user.target
```

Then start/enable `he-ipv6.service`.

## systemd-networkd

If [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") handles your network connections, it's probably a better idea to let it handle tunnel broker too (instead of using a `.service` file).

 `/etc/systemd/network/he-tunnel.netdev` 
```
[Match]

[NetDev]
Name=he-ipv6
Kind=sit
MTUBytes=1480

[Tunnel]
Local=<local IPv4>
Remote=<tunnel endpoint>
TTL=255

```
 `/etc/systemd/network/he-tunnel.network` 
```
[Match]
Name=he-ipv6

[Network]
Address=<local IPv6>
Gateway=<IPv6 gateway>
DNS=2001:4860:4860::8888
DNS=2001:4860:4860::8844

[Route]
Destination=::/0

```

And, add this line to `[Network]` section of your default Internet connection `.network` file:

```
Tunnel=he-ipv6

```

## Using the tunneling with dynamic IPv4 IP

The simplest way of using tunelling with a dynamic IPv4 IP is to set up a cronjob that is going to periodically update your current address. To do that open `crontab -e` and add, in a new line:

```
*/10 * * * * wget -O /dev/null https://USERNAME:PASSWORD@ipv4.tunnelbroker.net/ipv4_end.php?tid=TUNNELID >> /dev/null 2>&1

```

Which should also make wget quiet and not bothering you with emails about its activity. Please replace USERNAME, PASSWORD and TUNNELID by the details of your account and tunnel. I would recommend running the command on its own first, to check if it works. To do that run:

```
wget https://USERNAME:PASSWORD@ipv4.tunnelbroker.net/ipv4_end.php?tid=TUNNELID

```