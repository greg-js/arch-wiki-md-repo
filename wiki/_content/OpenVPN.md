# OpenVPN

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [OpenVPN in Linux containers](/index.php/OpenVPN_in_Linux_containers "OpenVPN in Linux containers")

This article describes a basic installation and configuration of [OpenVPN](http://openvpn.net), suitable for private and small business use. For more detailed information, please see the [OpenVPN 2.3 man page](https://community.openvpn.net/openvpn/wiki/Openvpn23ManPage) and the [OpenVPN documentation](http://openvpn.net/index.php/open-source/documentation). OpenVPN is a robust and highly flexible [VPN](https://en.wikipedia.org/wiki/VPN "wikipedia:VPN") daemon. It supports [SSL/TLS](https://en.wikipedia.org/wiki/SSL/TLS "wikipedia:SSL/TLS") security, [Ethernet bridging](https://en.wikipedia.org/wiki/Bridging_(networking) "wikipedia:Bridging (networking)"), [TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol "wikipedia:Transmission Control Protocol") or [UDP](https://en.wikipedia.org/wiki/User_Datagram_Protocol "wikipedia:User Datagram Protocol") [tunnel transport](https://en.wikipedia.org/wiki/Tunneling_protocol "wikipedia:Tunneling protocol") through [proxies](https://en.wikipedia.org/wiki/Proxy_server "wikipedia:Proxy server") or [NAT](https://en.wikipedia.org/wiki/Network_address_translation "wikipedia:Network address translation"). Additionally it has support for dynamic IP addresses and [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol "wikipedia:Dynamic Host Configuration Protocol"), scalability to hundreds or thousands of users, and portability to most major OS platforms.

OpenVPN is tightly bound to the [OpenSSL](http://www.openssl.org) library, and derives much of its crypto capabilities from it. It supports conventional encryption using a [pre-shared secret key](https://en.wikipedia.org/wiki/Pre-shared_key "wikipedia:Pre-shared key") (Static Key mode) or [public key security](https://en.wikipedia.org/wiki/Public_key "wikipedia:Public key") ([SSL/TLS](https://en.wikipedia.org/wiki/SSL/TLS "wikipedia:SSL/TLS") mode) using client & server certificates. Additionally it supports unencrypted TCP/UDP tunnels.

OpenVPN is designed to work with the [TUN/TAP](https://en.wikipedia.org/wiki/TUN/TAP "wikipedia:TUN/TAP") virtual networking interface that exists on most platforms. Overall, it aims to offer many of the key features of [IPSec](https://en.wikipedia.org/wiki/Ipsec "wikipedia:Ipsec") but with a relatively lightweight footprint. OpenVPN was written by James Yonan and is published under the [GNU General Public License (GPL)](https://en.wikipedia.org/wiki/GNU_General_Public_License "wikipedia:GNU General Public License").

## Contents

*   [1 Install OpenVPN](#Install_OpenVPN)
*   [2 Kernel configuration](#Kernel_configuration)
*   [3 Connect to a VPN provided by a third party](#Connect_to_a_VPN_provided_by_a_third_party)
*   [4 Create a Public Key Infrastructure (PKI) from scratch](#Create_a_Public_Key_Infrastructure_.28PKI.29_from_scratch)
*   [5 A basic L3 IP routing configuration](#A_basic_L3_IP_routing_configuration)
    *   [5.1 The server configuration file](#The_server_configuration_file)
    *   [5.2 The client configuration file](#The_client_configuration_file)
        *   [5.2.1 Drop root privileges after connecting](#Drop_root_privileges_after_connecting)
    *   [5.3 Testing the OpenVPN configuration](#Testing_the_OpenVPN_configuration)
    *   [5.4 Configure the MTU with Fragment and MSS](#Configure_the_MTU_with_Fragment_and_MSS)
    *   [5.5 IPv6](#IPv6)
        *   [5.5.1 Connect to the server via IPv6](#Connect_to_the_server_via_IPv6)
        *   [5.5.2 Provide IPv6 inside the tunnel](#Provide_IPv6_inside_the_tunnel)
*   [6 Starting OpenVPN](#Starting_OpenVPN)
    *   [6.1 Manual startup](#Manual_startup)
    *   [6.2 systemd service configuration](#systemd_service_configuration)
    *   [6.3 Letting NetworkManager start a connection](#Letting_NetworkManager_start_a_connection)
    *   [6.4 Gnome configuration](#Gnome_configuration)
*   [7 Routing all client traffic through the server](#Routing_all_client_traffic_through_the_server)
    *   [7.1 Firewall configuration](#Firewall_configuration)
        *   [7.1.1 ufw](#ufw)
        *   [7.1.2 iptables](#iptables)
    *   [7.2 Prevent leaks if vpn goes down](#Prevent_leaks_if_vpn_goes_down)
        *   [7.2.1 ufw](#ufw_2)
*   [8 L3 IPv4 routing](#L3_IPv4_routing)
    *   [8.1 Prerequisites for routing a LAN](#Prerequisites_for_routing_a_LAN)
        *   [8.1.1 Routing tables](#Routing_tables)
    *   [8.2 Connect the server LAN to a client](#Connect_the_server_LAN_to_a_client)
    *   [8.3 Connect the client LAN to a server](#Connect_the_client_LAN_to_a_server)
    *   [8.4 Connect both the client and server LANs](#Connect_both_the_client_and_server_LANs)
    *   [8.5 Connect clients and client LANs](#Connect_clients_and_client_LANs)
*   [9 DNS](#DNS)
*   [10 L2 Ethernet bridging](#L2_Ethernet_bridging)
*   [11 Troubleshooting](#Troubleshooting)
    *   [11.1 Resolve issues](#Resolve_issues)
    *   [11.2 Client daemon not restarting after suspend](#Client_daemon_not_restarting_after_suspend)
    *   [11.3 Connection drops out after some time of inactivity](#Connection_drops_out_after_some_time_of_inactivity)
*   [12 See Also](#See_Also)

## Install OpenVPN

[Install](/index.php/Install "Install") the [openvpn](https://www.archlinux.org/packages/?name=openvpn) package.

**Note:** The software contained in this package supports both server and client mode, so install it on all machines that need to create VPN connections.

## Kernel configuration

OpenVPN requires TUN/TAP support, which is already configured in the default kernel. If you build your own kernel, make sure to enable the `tun` module as below:

 `Kernel config file` 

```
 Device Drivers
  --> Network device support
    [M] Universal TUN/TAP device driver support
```

Read [Kernel modules](/index.php/Kernel_modules "Kernel modules") for more information.

## Connect to a VPN provided by a third party

To connect to a VPN service provided by a third party, most of the following can most likely be ignored, especially regarding server setup. Most likely you will want to begin with [#The client configuration file](#The_client_configuration_file) and skip ahead to [#Starting OpenVPN](#Starting_OpenVPN) after that. Use the certificates and instructions given by your provider, for instance see: [Airvpn](/index.php/Airvpn "Airvpn").

**Note:** Most free VPN providers will (often only) offer [PPTP](/index.php/PPTP_server "PPTP server"), which is drastically easier to setup and configure, but is [not secure](http://poptop.sourceforge.net/dox/protocol-security.phtml).

## Create a Public Key Infrastructure (PKI) from scratch

If you are setting up OpenVPN from scratch, you will need to create a [Public Key Infrastructure (PKI)](https://en.wikipedia.org/wiki/Public_key_infrastructure "wikipedia:Public key infrastructure").

Create the needed certificates and keys by following: [Create a Public Key Infrastructure Using the easy-rsa Scripts](/index.php/Create_a_Public_Key_Infrastructure_Using_the_easy-rsa_Scripts "Create a Public Key Infrastructure Using the easy-rsa Scripts").

The final step of the key creation process is to copy the files needed to the correct machines through a secure channel.

**Note:** The rest of this article assumes that the keys and certificates are placed in `/etc/openvpn`.

The public ca.crt certificate is needed on all servers and clients. The private ca.key key is secret and only needed on the key generating machine.

A server needs server.crt, dh2048.pem (public), server.key, and ta.key (private).

A client needs client.crt (public), client.key, and ta.key (private).

## A basic L3 IP routing configuration

**Note:** Unless otherwise explicitly stated, the rest of this article assumes this basic configuration.

OpenVPN is an extremely versatile piece of software and many configurations are possible, in fact machines can be both "servers" and "clients", blurring the distinction between server and client.

What really distinguishes a server from a client (apart from the type of certificate used) is the configuration file itself. The OpenVPN daemon start-up script reads all the .conf configuration files it finds in `/etc/openvpn` on start-up and acts accordingly. If it finds more than one configuration file, it will start one OpenVPN process per configuration file.

This article explains how to set up a server named elmer and a client that connects to it named bugs. More servers and clients can easily be added by creating more key/certificate pairs and adding more server and client configuration files.

The OpenVPN package comes with a collection of example configuration files for different purposes. The sample server and client configuration files make an ideal starting point for a basic OpenVPN setup with the following features:

*   Uses [Public Key Infrastructure (PKI)](https://en.wikipedia.org/wiki/Public_key_infrastructure "wikipedia:Public key infrastructure") for authentication.
*   Creates a VPN using a virtual TUN network interface (OSI L3 IP routing).
*   Listens for client connections on UDP port 1194 (OpenVPN's [official IANA port number](https://en.wikipedia.org/wiki/Port_number "wikipedia:Port number")).
*   Distributes virtual addresses to connecting clients from the 10.8.0.0/24 subnet.

For more advanced configurations, please see the official [OpenVPN 2.2 man page](http://openvpn.net/index.php/manuals/427-openvpn-22.html) and the [OpenVPN documentation](http://openvpn.net/index.php/open-source/documentation).

### The server configuration file

Copy the example server configuration file to `/etc/openvpn/server.conf`:

```
# cp /usr/share/openvpn/examples/server.conf /etc/openvpn/server.conf

```

Edit the following:

*   The `ca`, `cert`, `key`, and `dh` parameters to reflect the path and names of the keys and certificates. Specifying the paths will allow you to run the OpenVPN executable from any directory for testing purposes.
*   Enable the SSL/TLS HMAC handshake protection. **Note the use of the parameter 0 for a server**.
*   It is recommended to run OpenVPN with reduced privileges once it has initialized. Do this by uncommenting the `user` and `group` directives.

 `/etc/openvpn/server.conf` 

```
ca /etc/openvpn/ca.crt
cert /etc/openvpn/elmer.crt
key /etc/openvpn/elmer.key

dh /etc/openvpn/dh2048.pem
.
.
tls-auth /etc/openvpn/ta.key **0**
.
.
user nobody
group nobody

```

**Note:** Note that if the server is behind a firewall or a NAT translating router, you will have to forward the OpenVPN UDP port (1194) to the server.

### The client configuration file

Copy the example client configuration file to `/etc/openvpn/client.conf`:

```
# cp /usr/share/openvpn/examples/client.conf /etc/openvpn/client.conf

```

Edit the following:

*   The `remote` directive to reflect either the server's [Fully Qualified Domain Name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name "wikipedia:Fully qualified domain name"), hostname (as known to the client), or its IP address.
*   Uncomment the `user` and `group` directives to drop privileges.
*   The `ca`, `cert`, and `key` parameters to reflect the path and names of the keys and certificates.
*   Enable the SSL/TLS HMAC handshake protection. **Note the use of the parameter 1 for a client**.

 `/etc/openvpn/client.conf` 

```
remote elmer.acmecorp.org 1194
.
.
user nobody
group nobody
ca /etc/openvpn/ca.crt
cert /etc/openvpn/bugs.crt
key /etc/openvpn/bugs.key
.
.
tls-auth /etc/openvpn/ta.key **1**

```

#### Drop root privileges after connecting

Using the options `user nobody` and `group nobody` in the configuration file makes _openvpn_ drop its privileges after establishing the connection. The downside is that upon VPN disconnect the daemon is unable to delete its set network routes again. If one wants to limit transmitting traffic without the VPN connection, this may be advantageous. However, it requires manual action to delete the routes and will, hence, often be undesired. For this case the [OpenVPN howto](https://openvpn.net/index.php/open-source/documentation/howto.html#security) explains how to create an unprivileged user mode and wrapper script to have the routes restored automatically.

Further, it is possible to let OpenVPN start as a non-privileged user in the first place, without ever running as root, see [this OpenVPN wiki page](https://community.openvpn.net/openvpn/wiki/UnprivilegedUser).

### Testing the OpenVPN configuration

Run `# openvpn /etc/openvpn/server.conf` on the server, and `# openvpn /etc/openvpn/client.conf` on the client. You should see something similar to this:

 `# openvpn /etc/openvpn/server.conf` 

```
Wed Dec 28 14:41:26 2011 OpenVPN 2.2.1 x86_64-unknown-linux-gnu [SSL] [LZO2] [EPOLL] [eurephia] built on Aug 13 2011
Wed Dec 28 14:41:26 2011 NOTE: OpenVPN 2.1 requires '--script-security 2' or higher to call user-defined scripts or executables
Wed Dec 28 14:41:26 2011 Diffie-Hellman initialized with 2048 bit key
.
.
Wed Dec 28 14:41:54 2011 bugs/95.126.136.73:48904 MULTI: primary virtual IP for bugs/95.126.136.73:48904: 10.8.0.6
Wed Dec 28 14:41:57 2011 bugs/95.126.136.73:48904 PUSH: Received control message: 'PUSH_REQUEST'
Wed Dec 28 14:41:57 2011 bugs/95.126.136.73:48904 SENT CONTROL [bugs]: 'PUSH_REPLY,route 10.8.0.1,topology net30,ping 10,ping-restart 120,ifconfig 10.8.0.6 10.8.0.5' (status=1)
```

 `# openvpn /etc/openvpn/client.conf` 

```
Wed Dec 28 14:41:50 2011 OpenVPN 2.2.1 i686-pc-linux-gnu [SSL] [LZO2] [EPOLL] [eurephia] built on Aug 13 2011
Wed Dec 28 14:41:50 2011 NOTE: OpenVPN 2.1 requires '--script-security 2' or higher to call user-defined scripts or executables
Wed Dec 28 14:41:50 2011 LZO compression initialized
.
.
Wed Dec 28 14:41:57 2011 GID set to nobody
Wed Dec 28 14:41:57 2011 UID set to nobody
Wed Dec 28 14:41:57 2011 Initialization Sequence Completed
```

On the server, find the IP address assigned to the tunX device:

 `# ip addr show` 

```
.
.
40: tun0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN qlen 100
    link/none
    inet 10.8.0.1 peer 10.8.0.2/32 scope global tun0
```

Here we see that the server end of the tunnel has been given the IP address 10.8.0.1.

Do the same on the client:

 `# ip addr show` 

```
.
.
37: tun0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN qlen 100
    link/none
    inet 10.8.0.6 peer 10.8.0.5/32 scope global tun0
```

And the client side has been given the IP address 10.8.0.6.

Now try pinging the interfaces.

On the server:

 `# ping -c3 10.8.0.6` 

```
PING 10.8.0.6 (10.8.0.6) 56(84) bytes of data.
64 bytes from 10.8.0.6: icmp_req=1 ttl=64 time=238 ms
64 bytes from 10.8.0.6: icmp_req=2 ttl=64 time=237 ms
64 bytes from 10.8.0.6: icmp_req=3 ttl=64 time=205 ms

--- 10.8.0.6 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 205.862/227.266/238.788/15.160 ms
```

On the client:

 `# ping -c3 10.8.0.1` 

```
PING 10.8.0.1 (10.8.0.1) 56(84) bytes of data.
64 bytes from 10.8.0.1: icmp_req=1 ttl=64 time=158 ms
64 bytes from 10.8.0.1: icmp_req=2 ttl=64 time=158 ms
64 bytes from 10.8.0.1: icmp_req=3 ttl=64 time=157 ms

--- 10.8.0.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2001ms
rtt min/avg/max/mdev = 157.426/158.278/158.940/0.711 ms
```

You now have a working OpenVPN installation, and your client (bugs) will be able to use services on the server (elmer), and vice versa.

**Note:** If using a firewall, make sure that IP packets on the TUN device are not blocked.

### Configure the MTU with Fragment and MSS

**Note:** If you do not configure MTU, then you will notice that small packets like ping and DNS will work, however web browsing will not work.

Now it is time to configure the maximum segment size (MSS). In order to do this we need to discover what is the smallest MTU along the path between the client and server. In order to do this you can ping the server and disable fragmentation. Then specify the max packet size.

 `# ping -c5 -M do -s 1500 elmer.acmecorp.org` 

```
PING elmer.acmecorp.org (99.88.77.66) 1500(1528) bytes of data.
From 1.2.3.4 (99.88.77.66) icmp_seq=1 Frag needed and DF set (mtu = 576)
From 1.2.3.4 (99.88.77.66) icmp_seq=1 Frag needed and DF set (mtu = 576)
From 1.2.3.4 (99.88.77.66) icmp_seq=1 Frag needed and DF set (mtu = 576)
From 1.2.3.4 (99.88.77.66) icmp_seq=1 Frag needed and DF set (mtu = 576)
From 1.2.3.4 (99.88.77.66) icmp_seq=1 Frag needed and DF set (mtu = 576)

--- core.myrelay.net ping statistics ---
0 packets transmitted, 0 received, +5 errors
```

We received an ICMP message telling us the MTU is 576 bytes. The means we need to fragment the UDP packets smaller then 576 bytes to allow for some UDP overhead.

 `# ping -c5 -M do -s 548 elmer.acmecorp.org` 

```
PING elmer.acmecorp.org (99.88.77.66) 548(576) bytes of data.
556 bytes from 99.88.77.66: icmp_seq=1 ttl=48 time=206 ms
556 bytes from 99.88.77.66: icmp_seq=2 ttl=48 time=224 ms
556 bytes from 99.88.77.66: icmp_seq=3 ttl=48 time=206 ms
556 bytes from 99.88.77.66: icmp_seq=4 ttl=48 time=207 ms
556 bytes from 99.88.77.66: icmp_seq=5 ttl=48 time=208 ms

--- myrelay.net ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4001ms
rtt min/avg/max/mdev = 206.027/210.603/224.158/6.832 ms
```

After some trial and error..., we discover that we need to fragment packets on 548 bytes. In order to do this we specify this fragment size in the configuration and instruct OpenVPN to fix the Maximum Segment Size (MSS).

 `/etc/openvpn/client.conf` 

```
remote elmer.acmecorp.org 1194
.
.
fragment 548
mssfix 548
.
.
user nobody
group nobody
.
.
ca /etc/openvpn/ca.crt
cert /etc/openvpn/bugs.crt
key /etc/openvpn/bugs.key
.
.
tls-auth /etc/openvpn/ta.key **1**

```

We also need to tell the server about the fragmentation. Note that "mssfix" is NOT needed in the server configuration.

 `/etc/openvpn/server.conf` 

```
ca /etc/openvpn/ca.crt
cert /etc/openvpn/elmer.crt
key /etc/openvpn/elmer.key

dh /etc/openvpn/dh2048.pem
.
.
tls-auth /etc/openvpn/ta.key **0**
.
.
user nobody
group nobody
.
.
fragment 548

```

**Note:** The following will add about 3 minutes to OpenVPN start time. It is advisable to configure the fragment size unless your client is a laptop that will be connecting over many different networks and the bottle neck is on the client side.

You can also allow OpenVPN to do this for you by having OpenVPN do the ping testing every time the client connects to the VPN. Be patient, since your client may not inform you about the test being run and the connection may appear as nonfunctional until finished.

 `/etc/openvpn/client.conf` 

```
remote elmer.acmecorp.org 1194
.
.
mtu-test
.
.
user nobody
group nobody
.
.
ca /etc/openvpn/ca.crt
cert /etc/openvpn/bugs.crt
key /etc/openvpn/bugs.key
.
.
tls-auth /etc/openvpn/ta.key **1**

```

### IPv6

#### Connect to the server via IPv6

In order to enable Dual Stack for OpenVPN, you have to change `proto udp` to `proto udp6` in both server.conf and client.conf. Afterwards both IPv4 and IPv6 are enabled.

#### Provide IPv6 inside the tunnel

In order to provide IPv6 inside the tunnel, you need to have a IPv6 prefix routed to your OpenVPN server. Either set up a static route on your gateway (if you have a static block assigned), or use a DHCPv6 client to get a prefix with DHCPv6 Prefix delegation (see [IPv6 Prefix delegation](/index.php/IPv6#Prefix_delegation_.28DHCPv6-PD.29 "IPv6") for details). You can also use a unique local address from the address block fc00::/7\. Both methods have advantages and disadvantages:

*   Many ISPs only provide dynamically changing IPv6 prefixes. OpenVPN does not support prefix changes, so you need to change your server.conf every time the prefix is changed (Maybe can be automated with a script).
*   ULA addresses are not routed to the Internet, and setting up NAT is not as straightforward as with IPv4\. So you cannot route the entire traffic over the tunnel. If you only want to connect two sites via IPv6, without the need to connect to the Internet over the tunnel, the ULA addresses may be easier to use.

After you have received a prefix (a /64 is recommended), append the following to the server.conf:

```
server-ipv6 2001:db8:0:123::/64

```

This is the IPv6 equivalent to the default 10.8.0.0/24 network of OpenVPN and needs to be taken from the DHCPv6 client. Or use for example fd00:1234::/64.

If you want to push a route to your home network (192.168.1.0/24 equivalent), also append:

```
push "route-ipv6 2001:db8:0:abc::/64"

```

OpenVPN does not yet include DHCPv6, so there is no method to e.g. push DNS server over IPv6\. This needs to be done with IPv4\. The [OpenVPN Wiki](https://community.openvpn.net/openvpn/wiki/IPv6) provides some other configuration options.

## Starting OpenVPN

### Manual startup

To troubleshoot a VPN connection, start the client's daemon manually with `openvpn /etc/openvpn/client.conf` as root. The server can be started the same way using its own configuration file (e.g., `openvpn /etc/openvpn/server.conf`).

### systemd service configuration

To start OpenVPN automatically at system boot, either for a client or for a server, [enable](/index.php/Enable "Enable") `openvpn@_<configuration>_.service` on the applicable machine.

For example, if the client configuration file is `/etc/openvpn/client.conf`, the service name is `openvpn@client.service`. Or, if the server configuration file is `/etc/openvpn/server.conf`, the service name is `openvpn@server.service`.

### Letting NetworkManager start a connection

On a client you might not always need to run a VPN tunnel and/or only want to establish it for a specific NetworkManager connection. This can be done by adding a script to `/etc/NetworkManager/dispatcher.d/`. In the following example "Provider" is the name of the NetworkManager connection:

 `/etc/NetworkManager/dispatcher.d/10-openvpn` 

```
#!/bin/bash

case "$2" in
  up)
    if [ "$CONNECTION_ID" == "Provider" ]; then
      systemctl start openvpn@client
    fi
  ;;
  down)
    systemctl stop openvpn@client
  ;;
esac
```

See [NetworkManager#Network services with NetworkManager dispatcher](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") for more details.

### Gnome configuration

If you would like to connect a client to an OpenVPN server through Gnome's built-in network configuration do the following. First, install `networkmanager-openvpn`. Then go to the Settings menu and choose Network. Click the plus sign to add a new connection and choose VPN. From there you can choose OpenVPN and manually enter the settings, or you can choose to import [#The client configuration file](#The_client_configuration_file) if you have already created one. If you followed the instructions in this article then it will be located at `/etc/openvpn/client.conf`. To connect to the VPN simply turn the connection on.

## Routing all client traffic through the server

**Note:** There are potential pitfalls when routing all traffic through a VPN server. Refer to [the OpenVPN documenation on this topic](http://openvpn.net/index.php/open-source/documentation/howto.html#redirect) for more information.

By default only traffic directly to and from an OpenVPN server passes through the VPN. To have all traffic, including web traffic, pass through the VPN do the following. First add the following to your server's configuration file (i.e., `/etc/openvpn/server.conf`) [[1]](http://openvpn.net/index.php/open-source/documentation/howto.html#redirect):

```
push "redirect-gateway def1"
push "dhcp-option DNS 10.8.0.1"

```

Change "10.8.0.1" to your preferred DNS IP address.

If you have problems with non responsive DNS after connecting to server, install [BIND](/index.php/BIND "BIND") as simple DNS forwarder and push the IP address of the OpenVPN server as DNS to clients.

Now you need to [enable packet forwarding](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing") on the server.

In addition to above, your server's firewall will need to be set up to allow VPN traffic through it, which is described below for both [ufw](/index.php/Ufw "Ufw") and [iptables](/index.php/Iptables "Iptables").

### Firewall configuration

#### ufw

In order to configure your ufw settings for VPN traffic first add the following to `/etc/default/ufw`:

 `/etc/default/ufw`  `DEFAULT_FORWARD_POLICY="ACCEPT"` 

Now change `/etc/ufw/before.rules`, and add the following code after the header and before the "*filter" line. Do not forget to change the IP/subnet mask to match the one in `/etc/openvpn/server.conf`.

 `/etc/ufw/before.rules` 

```
# NAT (Network Address Translation) table rules
*nat
:POSTROUTING ACCEPT [0:0]

# Allow traffic from clients to enp1s0
-A POSTROUTING -s 10.8.0.0/24 -o enp1s0 -j MASQUERADE

# do not delete the "COMMIT" line or the NAT table rules above will not be processed
COMMIT
```

Lastly, open OpenVPN port 1194:

```
ufw allow 1194

```

#### iptables

In order to allow VPN traffic through your iptables firewall of your server, first create an iptables rule for NAT forwarding [[2]](http://openvpn.net/index.php/open-source/documentation/howto.html#redirect) on the server:

```
iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o eth0 -j MASQUERADE

```

If you have difficulty pinging the server through the VPN, you may need to add explicit rules to open up TUN/TAP interfaces to all traffic. If that is the case, do the following [[3]](https://community.openvpn.net/openvpn/wiki/255-qconnection-initiated-with-xxxxq-but-i-cannot-ping-the-server-through-the-vpn):

**Warning:** There are security implications for the following rules if you do not trust all clients which connect to the server. Refer to the [OpenVPN documentation on this topic](https://community.openvpn.net/openvpn/wiki/255-qconnection-initiated-with-xxxxq-but-i-cannot-ping-the-server-through-the-vpn) for more details.

```
 # Allow TUN interface connections to OpenVPN server
 iptables -A INPUT -i tun+ -j ACCEPT
 # Allow TUN interface connections to be forwarded through other interfaces
 iptables -A FORWARD -i tun+ -j ACCEPT
 # Allow TAP interface connections to OpenVPN server
 iptables -A INPUT -i tap+ -j ACCEPT
 # Allow TAP interface connections to be forwarded through other interfaces
 iptables -A FORWARD -i tap+ -j ACCEPT

```

When you are satisfied make the changes permanent as shown in [iptables#Configuration and usage](/index.php/Iptables#Configuration_and_usage "Iptables").

### Prevent leaks if vpn goes down

The idea is simple: prevent all traffic through our default interface (enp3s0 for example) and only allow tun0. If the openvpn connection drops, your computer will lose its internet access and therefore, avoid your programs to continue connecting through an insecure network adapter.

Be sure to set up a script to restart openvpn if it goes down if you do not want to manually restart it.

#### ufw

```
 # Default policies
 ufw default deny incoming
 ufw default deny outgoing

 # Openvpn interface (adjust interface accordingly to your configuration)
 ufw allow in on tun0
 ufw allow out on tun0

 # Local Network (adjust ip accordingly to your configuration)
 ufw allow in on enp3s0 from 192.168.1.0/24
 ufw allow out on enp3s0 to 192.168.1.0/24

 # Openvpn (adjust port accordingly to your configuration)
 ufw allow out on enp3s0 to any port 1194
 ufw allow in on enp3s0 from any port 1194

```

**Warning:** DNS **will not** work **unless** you run your own dns server like [BIND](/index.php/BIND "BIND")

Otherwise, you will need to allow dns leak. **Be sure to trust your dns server!**

```
 # DNS
 ufw allow in from any to any port 53
 ufw allow out from any to any port 53

```

## L3 IPv4 routing

This section describes how to connect client/server LANs to each other using L3 IPv4 routing.

### Prerequisites for routing a LAN

For a host to be able to forward IPv4 packets between the LAN and VPN, it must be able to forward the packets between its NIC and its tun/tap device. See [Internet sharing#Enable packet forwarding](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing") for configuration details.

#### Routing tables

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Investigate if a routing protocol like RIP, QUAGGA, BIRD, etc can be used (Discuss in [Talk:OpenVPN#](https://wiki.archlinux.org/index.php/Talk:OpenVPN))

By default, all IP packets on a LAN addressed to a different subnet get sent to the default gateway. If the LAN/VPN gateway is also the default gateway, there is no problem and the packets get properly forwarded. If not, the gateway has no way of knowing where to send the packets. There are a couple of solutions to this problem.

*   Add a static route to the default gateway routing the VPN subnet to the LAN/VPN gateway's IP address.
*   Add a static route on each host on the LAN that needs to send IP packets back to the VPN.
*   Use [iptables](/index.php/Iptables "Iptables")' NAT feature on the LAN/VPN gateway to masquerade the incoming VPN IP packets.

### Connect the server LAN to a client

The server is on a LAN using the 10.66.0.0/24 subnet. To inform the client about the available subnet, add a push directive to the server configuration file: `/etc/openvpn/server.conf`  `push "route 10.66.0.0 255.255.255.0"` 

**Note:** To route more LANs from the server to the client, add more push directives to the server configuration file, but keep in mind that the server side LANs will need to know how to route to the client.

### Connect the client LAN to a server

Prerequisites:

*   Any subnets used on the client side, must be unique and not in use on the server or by any other client. In this example we will use 192.168.4.0/24 for the clients LAN.
*   Each client's certificate has a unique Common Name, in this case bugs.
*   The server may not use the duplicate-cn directive in its config file.

Create a client configuration directory on the server. It will be searched for a file named the same as the client's common name, and the directives will be applied to the client when it connects.

```
# mkdir -p /etc/openvpn/ccd

```

Create a file in the client configuration directory called bugs, containing the `iroute 192.168.4.0 255.255.255.0` directive. It tells the server what subnet should be routed to the client:

 `/etc/openvpn/ccd/bugs`  `iroute 192.168.4.0 255.255.255.0` 

Add the client-config-dir and the `route 192.168.4.0 255.255.255.0` directive to the server configuration file. It tells the server what subnet should be routed from the tun device to the server LAN:

 `/etc/openvpn/server.conf` 

```
client-config-dir ccd
route 192.168.4.0 255.255.255.0

```

**Note:** To route more LANs from the client to the server, add more iroute and route directives to the appropriate configuration files, but keep in mind that the client side LANs will need to know how to route to the server.

### Connect both the client and server LANs

Combine the two previous sections:

 `/etc/openvpn/server.conf` 

```
push "route 10.66.0.0 255.255.255.0"
.
.
client-config-dir ccd
route 192.168.4.0 255.255.255.0

```

 `/etc/openvpn/ccd/bugs`  `iroute 192.168.4.0 255.255.255.0` 

**Note:** Remember to make sure that all the LANs or the needed hosts can route to all the destinations.

### Connect clients and client LANs

By default clients will not see each other. To allow IP packets to flow between clients and/or client LANs, add a client-to-client directive to the server configuration file: `/etc/openvpn/server.conf`  `client-to-client` 

In order for another client or client LAN to see a specific client LAN, you will need to add a push directive for each client subnet to the server configuration file (this will make the server announce the available subnet(s) to other clients):

 `/etc/openvpn/server.conf` 

```
client-to-client
push "route 192.168.4.0 255.255.255.0"
push "route 192.168.5.0 255.255.255.0"
.
.

```

**Note:** As always, make sure that the routing is properly configured.

## DNS

The DNS servers used by the system are defined in `/etc/resolv.conf`. Traditionally, this file is the responsibility of whichever program deals with connecting the system to the network (e.g. Wicd, NetworkManager, etc...) However, OpenVPN will need to modify this file if you want to be able to resolve names on the remote side. To achieve this in a sensible way, install [openresolv](https://www.archlinux.org/packages/?name=openresolv), which makes it possible for more than one program to modify `resolv.conf` without stepping on each-other's toes.

Before continuing, test openresolv by restarting your network connection and ensuring that `resolv.conf` states that it was generated by _resolvconf_, and that your DNS resolution still works as before. You should not need to configure openresolv; it should be automatically detected and used by your network system.

For Linux, OpenVPN can send DNS host information, but expects an external process to act on it. This can be done with a [openvpn-update-resolv-conf](https://github.com/masterkorp/openvpn-update-resolv-conf) script, which can be saved for example at `/etc/openvpn/update-resolv-conf` and make it executable with [chmod](/index.php/Chmod "Chmod"). There is also an AUR package: [openvpn-update-resolv-conf](https://aur.archlinux.org/packages/openvpn-update-resolv-conf/)<sup><small>AUR</small></sup> which will take care of the script installation for you.

Once the script is installed add lines like the following into your OpenVPN client configuration file:

```
script-security 2
up /etc/openvpn/update-resolv-conf
down /etc/openvpn/update-resolv-conf

```

Now, when your launch your OpenVPN connection, you should find that your resolv.conf file is updated accordingly, and also returns to normal when your close the connection.

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** The above does not work on shutdown when following [Drop root privileges after connecting](/index.php?title=Drop_root_privileges_after_connecting&action=edit&redlink=1 "Drop root privileges after connecting (page does not exist)"). (Discuss in [Talk:OpenVPN#Dropping root privileges: sub-section in DNS is out-of-sync](https://wiki.archlinux.org/index.php/Talk:OpenVPN#Dropping_root_privileges:_sub-section_in_DNS_is_out-of-sync))

## L2 Ethernet bridging

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Please add a well thought out section on L2 bridging. (Discuss in [Talk:OpenVPN#](https://wiki.archlinux.org/index.php/Talk:OpenVPN))

For now see: [OpenVPN Bridge](/index.php/OpenVPN_Bridge "OpenVPN Bridge")

## Troubleshooting

### Resolve issues

If you are having resolve issues when starting your profile:

 `# journalctl _SYSTEMD_UNIT=openvpn@_profile_.service` 

```
RESOLVE: Cannot resolve host address: example.com: Name or service not known

```

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Ordering "After=network.target" does not work universally. See [network.target](http://www.freedesktop.org/wiki/Software/systemd/NetworkTarget/). Further, not the original unit in `/usr/lib` should be modified but a copy, cross-referencing [Systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd"). (Discuss in [Talk:OpenVPN#](https://wiki.archlinux.org/index.php/Talk:OpenVPN))

Then, **only if your network setup can be started before OpenVPN**, you should force OpenVPN to wait for the network by adding `Requires=network.target` and `After=network.target` to the OpenVPN systemd service file:

 `/usr/lib/systemd/system/openvpn@.service` 

```
[Unit]
Description=OpenVPN connection to %i
Requires=network.target
After=network.target
...

```

Do not forget to run `systemctl daemon-reload` and [restart](/index.php/Restart "Restart") `openvpn@_profile_.service`.

### Client daemon not restarting after suspend

If you put your client system to sleep, and on resume openvpn does not restart, resulting in broken connectivity, create the following file:

 `/usr/lib/systemd/system-sleep/vpn.sh` 

```
#!/bin/sh
if [ "$1" == "pre" ]
then
  killall openvpn
fi
```

Make it executable `chmod a+x /usr/lib/systemd/system-sleep/vpn.sh`

 `/etc/systemd/system/openvpn@.service.d/restart.conf` 

```
[Service]
Restart=always
```

### Connection drops out after some time of inactivity

If the VPN-Connection drops some seconds after it stopped transmitting data and, even though it states it is connected, no data can be transmitted through the tunnel, try adding a `keepalive`directive to the server's configuration:

 `/etc/openvpn/server.conf` 

```
.
.
keepalive 10 120
.
.

```

In this case the server will send ping-like messages to all of its clients every `10` seconds, thus keeping the tunnel up. If the server does not receive a response within `120` seconds from a specific client, it will assume this client is down.

A small ping-interval can increase the stability of the tunnel, but will also cause slightly higher traffic. Depending on your connection, also try lower intervals than 10 seconds.

## See Also

*   [OpenVPN Official Site](https://openvpn.net/index.php/open-source.html)
*   [Airvpn](/index.php/Airvpn "Airvpn")

Retrieved from "[https://wiki.archlinux.org/index.php?title=OpenVPN&oldid=412455](https://wiki.archlinux.org/index.php?title=OpenVPN&oldid=412455)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Virtual Private Network](/index.php/Category:Virtual_Private_Network "Category:Virtual Private Network")