Hurricane Electric offers a free [tunnel broker](http://tunnelbroker.net/) service that is relatively painless to use under Arch if you wish to add IPv6 connectivity to an IPv4-only host.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Registering for a tunnel](#Registering_for_a_tunnel)
*   [2 Setting up Hurricane Electric tunnel](#Setting_up_Hurricane_Electric_tunnel)
*   [3 systemd-networkd](#systemd-networkd)
*   [4 Using the tunneling with dynamic IPv4 IP](#Using_the_tunneling_with_dynamic_IPv4_IP)

## Registering for a tunnel

It is not that hard to do. Feel free to fill in the directions here if something seems tricky, but otherwise just go the tunnel broker site and complete the registration.

## Setting up Hurricane Electric tunnel

Create the following systemd unit, replacing bold text with the IP addresses you got from HE:

**Note:** If you are behind a NAT (typical home router setup), use your *local* IPv4 address for `*client_IPv4_address*`, e.g. `192.168.0.2`.
 `/etc/systemd/system/he-ipv6.service` 
```
[Unit]
Description=he.net IPv6 tunnel
After=network.target

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/bin/ip tunnel add he-ipv6 mode sit remote *server_IPv4_address* local *client_IPv4_address* ttl 255
ExecStart=/usr/bin/ip link set he-ipv6 up mtu 1480
ExecStart=/usr/bin/ip addr add *client_IPv6_address* dev he-ipv6
ExecStart=/usr/bin/ip -6 route add ::/0 dev he-ipv6
ExecStop=/usr/bin/ip -6 route del ::/0 dev he-ipv6
ExecStop=/usr/bin/ip link set he-ipv6 down
ExecStop=/usr/bin/ip tunnel del he-ipv6

[Install]
WantedBy=multi-user.target
```

Then [start/enable](/index.php/Start/enable "Start/enable") `he-ipv6.service`.

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

```

And, add this line to `[Network]` section of your default Internet connection `.network` file:

```
Tunnel=he-ipv6

```

## Using the tunneling with dynamic IPv4 IP

The simplest way of using tunelling with a dynamic IPv4 IP is to set up a cronjob that is going to periodically update your current address. The example URL and an *Update Key* can be found in the *Advanced* tab of the *Tunnel Details* page.

To check if the update works, run the following command (replace `*USERNAME*`, `*UPDATEKEY*` and `*TUNNELID*` by the details of your account and tunnel):

```
$ wget -O - https://*USERNAME*:*UPDATEKEY*@ipv4.tunnelbroker.net/nic/update?hostname=*TUNNELID*

```

If it works, create a cronjob by opening `crontab -e` and adding a new line:

```
*/10 * * * * wget -q -O /dev/null https://*USERNAME*:*UPDATEKEY*@ipv4.tunnelbroker.net/nic/update?hostname=*TUNNELID*

```