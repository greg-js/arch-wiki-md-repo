There are several ways to set up a Virtual Private Network through SSH. Note that, while this may be useful from time to time, it may not be a full replacement for a regular VPN. See for example [[1]](http://sites.inka.de/bigred/devel/tcp-tcp.html).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Using badvpn's tun2socks](#Using_badvpn's_tun2socks)
    *   [1.1 Start SSH dynamic SOCKS proxy](#Start_SSH_dynamic_SOCKS_proxy)
    *   [1.2 Set up badvpn and tunnel interface](#Set_up_badvpn_and_tunnel_interface)
    *   [1.3 Get traffic into the tunnel](#Get_traffic_into_the_tunnel)
*   [2 OpenSSH's built in tunneling](#OpenSSH's_built_in_tunneling)
    *   [2.1 Create tun interfaces using systemd-networkd](#Create_tun_interfaces_using_systemd-networkd)
        *   [2.1.1 Creating interfaces in SSH command](#Creating_interfaces_in_SSH_command)
    *   [2.2 Start SSH](#Start_SSH)
    *   [2.3 Troubleshooting](#Troubleshooting)
*   [3 Using PPP over SSH](#Using_PPP_over_SSH)
    *   [3.1 Helper script](#Helper_script)
*   [4 See also](#See_also)

## Using badvpn's tun2socks

[badvpn](https://www.archlinux.org/packages/?name=badvpn) is a collection of utilities for various VPN-related use cases.

### Start SSH dynamic SOCKS proxy

First, we'll set up a normal SSH dynamic socks proxy like usual:

```
$ ssh -TND 4711 <your_user>@<SSH_server>

```

### Set up badvpn and tunnel interface

Afterwards, we can go ahead with setting up the TUN.

```
# ip tuntap add dev tun0 mode tun user <your_local_user>
# ip addr replace 10.0.0.1/24 dev tun0
# badvpn-tun2socks --tundev tun0 --netif-ipaddr 10.0.0.2 --netif-netmask 255.255.255.0 --socks-server-addr localhost:4711

```

Now you have a working local `tun0` interface which routes all traffic going into it through the SOCKS proxy you set up earlier.

### Get traffic into the tunnel

All that's left to do now is to set up a local route to get some traffic into it. Let's set up a route that routes all traffic into it. We'll need three routes:

1.  Route that goes to the SSH server that we use for the tunnel with a low metric.
2.  Route for DNS server (because tun2socks doesn't do UDP which is necessary for DNS) with a low metric.
3.  Default route for all other traffic with a higher metric than the other routes.

The idea behind setting the metrics specifically is because we need to ensure that the route picked to the SSH server is always direct because otherwise it would go back into the SSH tunnel which would cause a loop and we'd lose the SSH connection as a result. Apart from that, we need to set an explicit DNS route because tun2socks doesn't tunnel UDP (required for DNS). We also need a new default route with a lower metric than your old default route so that traffic goes into the tunnel at all. With all of that said, let's get to work:

```
# ip route add <IP_of_SSH_server> via <IP_of_original_gateway> metric 5
# ip route add <IP_of_DNS_server> via <IP_of_original_gateway> metric 5
# ip route add default via 10.0.0.2 metric 6

```

Now all traffic (except for DNS and the SSH server itself) should go through `tun0`.

## OpenSSH's built in tunneling

OpenSSH has built-in TUN/TAP support using `-w<local-tun-number>:<remote-tun-number>`. Here, a layer 3/point-to-point/ TUN tunnel is described. It is also possible to create a layer 2/ethernet/TAP tunnel.

### Create tun interfaces using systemd-networkd

 `/etc/systemd/network/vpn.netdev` 
```
[NetDev]
Name=tun5
Kind=tun

[Tun]
User=vpn
Group=network
```
 `/etc/systemd/network/vpn.network` 
```
[Match]
Name=tun5

[Address]
Address=192.168.200.2/24
```

Once these files are created, enable them by [restarting](/index.php/Restart "Restart") `systemd-networkd.service`.

Also, you may manage tun interfaces with `ip tunnel` command.

#### Creating interfaces in SSH command

SSH can create both interfaces automatically, but you should configure IP and routing after the connection is established.

```
ssh \
  -o PermitLocalCommand=yes \
  -o LocalCommand="sudo ifconfig tun5 192.168.244.2 pointopoint 192.168.244.1 netmask 255.255.255.0" \
  -o ServerAliveInterval=60 \
  -w 5:5 vpn@example.com \
  'sudo ifconfig tun5 192.168.244.1 pointopoint 192.168.244.2 netmask 255.255.255.0; echo tun0 ready'
```

### Start SSH

```
ssh -f -w5:5 vpn@example.com -i ~/.ssh/key "sleep 1000000000"

```

or you may add keep-alive options if you are behind a NAT.

```
ssh -f -w5:5 vpn@example.com \
        -o ServerAliveInterval=30 \
        -o ServerAliveCountMax=5 \
        -o TCPKeepAlive=yes \
        -i ~/.ssh/key "sleep 1000000000"
```

### Troubleshooting

*   ssh should have access rights to tun interface or permissions to create it. Check owner of tun interface and/or /dev/net/tun.
*   Obviously if you want to access a network rather than a single machine you should properly set up IP packet forwarding, routing and maybe a netfilter on both sides.

## Using PPP over SSH

[pppd](/index.php/Pppd "Pppd") can easily be used to create a tunnel through an SSH server:

```
# pppd updetach noauth silent nodeflate pty "/usr/bin/ssh root@remote-gw /usr/sbin/pppd nodetach notty noauth" ipparam vpn 10.0.8.1:10.0.8.2

```

When the VPN is established, you can route traffic through it. To get access to an internal network:

```
# ip route add 192.168.0.0/16 via 10.0.8.2

```

To route all Internet traffic through the tunnel, for example, to protect your communication on an unencrypted network, first add a route to the SSH server through your regular gateway:

```
# ip route add <remote-gw> via <current default gateway>

```

Next, replace the default route with the tunnel

```
# ip route replace default via 10.0.8.2

```

### Helper script

[pvpn](https://github.com/halhen/pvpn) (package [pvpn](https://aur.archlinux.org/packages/pvpn/)) is a wrapper script around `pppd` over SSH.

## See also

*   [Network configuration](/index.php/Network_configuration "Network configuration")
*   [Router](/index.php/Router "Router")
*   [OpenSSH](/index.php/OpenSSH "OpenSSH")
*   [sshuttle](https://www.archlinux.org/packages/?name=sshuttle), a [python](/index.php/Python "Python") tunnel