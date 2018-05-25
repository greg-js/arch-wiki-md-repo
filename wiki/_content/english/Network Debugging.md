Related articles

*   [VLAN](/index.php/VLAN "VLAN")

## Contents

*   [1 Link status](#Link_status)
    *   [1.1 RTNETLINK answers: Cannot assign requested address](#RTNETLINK_answers:_Cannot_assign_requested_address)
*   [2 IP address](#IP_address)
*   [3 Ping & Tracepath/Traceroute](#Ping_.26_Tracepath.2FTraceroute)

## Link status

In the overview of `ip a`, the link status will already be displayed. But it can also be displayed by running:

```
$ ip link show dev eth0

```

This will provide an output along the lines of:

```
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state DOWN qlen 1000
   link/ether 70:5a:b6:8a:a0:87 brd ff:ff:ff:ff:ff:ff

```

Bringing up an interface can be done by issuing:

```
# ip link set dev eth0 up

```

#### RTNETLINK answers: Cannot assign requested address

If you get this error when trying to set an interface up, its most probably because you've got an invalid MAC address. To set a working MAC, see [MAC address spoofing](/index.php/MAC_address_spoofing "MAC address spoofing").

## IP address

In the overview provided by `ip a`, the ip address will already be displayed. But it can also be displayed by running:

```
$ ip addr show dev eth0

```

This will provide an output along the lines of:

```
 2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
   link/ether 70:5a:b6:8a:a0:87 brd ff:ff:ff:ff:ff:ff
   inet 192.168.1.143/24 brd 192.168.1.255 scope global eth0
   inet6 fe80::725a:b6ff:fe8a:a087/64 scope link 
      valid_lft forever preferred_lft forever

```

Adding a temporary ip address:

```
# ip addr add 192.168.1.143/24 dev eth0

```

Removing an ip address:

```
# ip addr del 192.168.1.143/24 dev eth0

```

## Ping & Tracepath/Traceroute

The ping command can help test connectivity towards a specific host.

The first step would be verifying connectivity towards the default gateway (replace the ip address with your own default gateway):

```
$ ping -c4 192.168.1.1

```

When erasing the "-c4" parameter, the ping will continue endlessly. It can be aborted by hitting "Control-C".

```
PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
64 bytes from 192.168.1.1: icmp_req=1 ttl=64 time=0.193 ms
64 bytes from 192.168.1.1: icmp_req=2 ttl=64 time=0.190 ms
64 bytes from 192.168.1.1: icmp_req=3 ttl=64 time=0.192 ms
64 bytes from 192.168.1.1: icmp_req=4 ttl=64 time=0.189 ms

--- 192.168.1.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 2999ms
rtt min/avg/max/mdev = 0.165/0.184/0.193/0.014 ms

```

The output above indicated the default gateway is reachable. When instead a "`Destination Host Unreachable`" message is displayed, doublecheck the ip address, netmask and default gateway config. This message can also be displayed when ICMP traffic is not permitted towards the default gateway (blocked by a firewall, router,...).

The next step is verifying connectivity towards the configured dns server(s). When no reply is received, `tracepath` or `traceroute` can be used to verify the routing towards said server and get an idea of where the issue lies.

```
$ traceroute 8.8.4.4

```

Traceroute also used ICMP to determine the path and hence there can be "no reply" answers as well when ICMP traffic is blocked.