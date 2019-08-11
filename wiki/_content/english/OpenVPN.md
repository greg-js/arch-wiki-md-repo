Related articles

*   [OpenVPN client in Linux Containers](/index.php/OpenVPN_client_in_Linux_Containers "OpenVPN client in Linux Containers")
*   [OpenVPN server in Linux Containers](/index.php/OpenVPN_server_in_Linux_Containers "OpenVPN server in Linux Containers")
*   [Easy-RSA](/index.php/Easy-RSA "Easy-RSA")

This article describes a basic installation and configuration of [OpenVPN](http://openvpn.net), suitable for private and small business use. For more detailed information, please see the [OpenVPN 2.4 man page](https://community.openvpn.net/openvpn/wiki/Openvpn24ManPage) and the [OpenVPN documentation](http://openvpn.net/index.php/open-source/documentation). OpenVPN is a robust and highly flexible [VPN](https://en.wikipedia.org/wiki/VPN "wikipedia:VPN") daemon. It supports [SSL/TLS](https://en.wikipedia.org/wiki/SSL/TLS "wikipedia:SSL/TLS") security, [Ethernet bridging](https://en.wikipedia.org/wiki/Bridging_(networking) "wikipedia:Bridging (networking)"), [TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol "wikipedia:Transmission Control Protocol") or [UDP](https://en.wikipedia.org/wiki/User_Datagram_Protocol "wikipedia:User Datagram Protocol") [tunnel transport](https://en.wikipedia.org/wiki/Tunneling_protocol "wikipedia:Tunneling protocol") through [proxies](https://en.wikipedia.org/wiki/Proxy_server "wikipedia:Proxy server") or [NAT](https://en.wikipedia.org/wiki/Network_address_translation "wikipedia:Network address translation"). Additionally it has support for dynamic IP addresses and [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol "wikipedia:Dynamic Host Configuration Protocol"), scalability to hundreds or thousands of users, and portability to most major OS platforms.

OpenVPN is tightly bound to the [OpenSSL](http://www.openssl.org) library, and derives much of its crypto capabilities from it. It supports conventional encryption using a [pre-shared secret key](https://en.wikipedia.org/wiki/Pre-shared_key "wikipedia:Pre-shared key") (Static Key mode) or [public key security](https://en.wikipedia.org/wiki/Public_key "wikipedia:Public key") ([SSL/TLS](https://en.wikipedia.org/wiki/SSL/TLS "wikipedia:SSL/TLS") mode) using client & server certificates. Additionally it supports unencrypted TCP/UDP tunnels.

OpenVPN is designed to work with the [TUN/TAP](https://en.wikipedia.org/wiki/TUN/TAP "wikipedia:TUN/TAP") virtual networking interface that exists on most platforms. Overall, it aims to offer many of the key features of [IPSec](https://en.wikipedia.org/wiki/Ipsec "wikipedia:Ipsec") but with a relatively lightweight footprint. OpenVPN was written by James Yonan and is published under the [GNU General Public License (GPL)](https://en.wikipedia.org/wiki/GNU_General_Public_License "wikipedia:GNU General Public License").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Kernel configuration](#Kernel_configuration)
*   [3 Connect to a VPN provided by a third party](#Connect_to_a_VPN_provided_by_a_third_party)
*   [4 Create a Public Key Infrastructure (PKI) from scratch](#Create_a_Public_Key_Infrastructure_(PKI)_from_scratch)
*   [5 A basic L3 IP routing configuration](#A_basic_L3_IP_routing_configuration)
    *   [5.1 Example configuration](#Example_configuration)
    *   [5.2 The server configuration file](#The_server_configuration_file)
        *   [5.2.1 Hardening the server](#Hardening_the_server)
        *   [5.2.2 Enabling compression](#Enabling_compression)
        *   [5.2.3 Deviating from the standard port and/or protocol](#Deviating_from_the_standard_port_and/or_protocol)
        *   [5.2.4 Running multiple instances of OpenVPN on different ports on the physical machine](#Running_multiple_instances_of_OpenVPN_on_different_ports_on_the_physical_machine)
    *   [5.3 The client config profile](#The_client_config_profile)
        *   [5.3.1 Run as unprivileged user](#Run_as_unprivileged_user)
    *   [5.4 Converting certificates to encrypted .p12 format](#Converting_certificates_to_encrypted_.p12_format)
    *   [5.5 Testing the OpenVPN configuration](#Testing_the_OpenVPN_configuration)
    *   [5.6 Configure the MTU with Fragment and MSS](#Configure_the_MTU_with_Fragment_and_MSS)
    *   [5.7 IPv6](#IPv6)
        *   [5.7.1 Connect to the server via IPv6](#Connect_to_the_server_via_IPv6)
        *   [5.7.2 Provide IPv6 inside the tunnel](#Provide_IPv6_inside_the_tunnel)
*   [6 Starting OpenVPN](#Starting_OpenVPN)
    *   [6.1 Manual startup](#Manual_startup)
    *   [6.2 systemd service configuration](#systemd_service_configuration)
    *   [6.3 Letting NetworkManager start a connection](#Letting_NetworkManager_start_a_connection)
    *   [6.4 Gnome configuration](#Gnome_configuration)
*   [7 Routing client traffic through the server](#Routing_client_traffic_through_the_server)
    *   [7.1 Firewall configuration](#Firewall_configuration)
        *   [7.1.1 firewalld](#firewalld)
        *   [7.1.2 ufw](#ufw)
        *   [7.1.3 iptables](#iptables)
    *   [7.2 Prevent leaks if VPN goes down](#Prevent_leaks_if_VPN_goes_down)
        *   [7.2.1 ufw](#ufw_2)
        *   [7.2.2 vpnfailsafe](#vpnfailsafe)
*   [8 L3 IPv4 routing](#L3_IPv4_routing)
    *   [8.1 Prerequisites for routing a LAN](#Prerequisites_for_routing_a_LAN)
        *   [8.1.1 Routing tables](#Routing_tables)
    *   [8.2 Connect the server LAN to a client](#Connect_the_server_LAN_to_a_client)
    *   [8.3 Connect the client LAN to a server](#Connect_the_client_LAN_to_a_server)
    *   [8.4 Connect both the client and server LANs](#Connect_both_the_client_and_server_LANs)
    *   [8.5 Connect clients and client LANs](#Connect_clients_and_client_LANs)
*   [9 DNS](#DNS)
    *   [9.1 Update resolv-conf script](#Update_resolv-conf_script)
    *   [9.2 Update systemd-resolved script](#Update_systemd-resolved_script)
    *   [9.3 Override DNS servers using NetworkManager](#Override_DNS_servers_using_NetworkManager)
*   [10 L2 Ethernet bridging](#L2_Ethernet_bridging)
*   [11 Config generators](#Config_generators)
    *   [11.1 ovpngen](#ovpngen)
    *   [11.2 openvpn-unroot](#openvpn-unroot)
*   [12 Troubleshooting](#Troubleshooting)
    *   [12.1 Client daemon not reconnecting after suspend](#Client_daemon_not_reconnecting_after_suspend)
    *   [12.2 Connection drops out after some time of inactivity](#Connection_drops_out_after_some_time_of_inactivity)
    *   [12.3 PID files not present](#PID_files_not_present)
    *   [12.4 Route configuration fails with systemd-networkd](#Route_configuration_fails_with_systemd-networkd)
    *   [12.5 tls-crypt unwrap error: packet too short](#tls-crypt_unwrap_error:_packet_too_short)
*   [13 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [openvpn](https://www.archlinux.org/packages/?name=openvpn) package, which provides both server and client mode.

Available frontends:

*   **NetworkManager OpenVPN** — NetworkManager VPN plugin for OpenVPN.

	[https://wiki.gnome.org/Projects/NetworkManager/VPN](https://wiki.gnome.org/Projects/NetworkManager/VPN) || [networkmanager-openvpn](https://www.archlinux.org/packages/?name=networkmanager-openvpn)

*   **QOpenVPN** — Simple OpenVPN GUI written in PyQt for systemd based distributions.

	[https://github.com/xmikos/qopenvpn](https://github.com/xmikos/qopenvpn) || [qopenvpn](https://www.archlinux.org/packages/?name=qopenvpn)

## Kernel configuration

OpenVPN requires TUN/TAP support, which is already configured in the default kernel. Users of custom kernel should make sure to enable the `tun` module:

 `Kernel config file` 
```
 Device Drivers
  --> Network device support
    [M] Universal TUN/TAP device driver support

```

Read [Kernel modules](/index.php/Kernel_modules "Kernel modules") for more information.

## Connect to a VPN provided by a third party

To connect to a VPN service provided by a third party, most of the following can most likely be ignored, especially regarding server setup. Begin with [#The client config profile](#The_client_config_profile) and skip ahead to [#Starting OpenVPN](#Starting_OpenVPN) after that. One should use the provider certificates and instructions, see [Category:VPN providers](/index.php/Category:VPN_providers "Category:VPN providers") for examples that can be adapted to other providers. [OpenVPN client in Linux Containers](/index.php/OpenVPN_client_in_Linux_Containers "OpenVPN client in Linux Containers") also has general applicable instructions, while it goes a step further by isolating an OpenVPN client process into a container.

**Note:** Most free VPN providers will (often only) offer [PPTP](/index.php/PPTP_server "PPTP server"), which is drastically easier to setup and configure, but [not secure](http://poptop.sourceforge.net/dox/protocol-security.phtml).

## Create a Public Key Infrastructure (PKI) from scratch

When setting up an OpenVPN server, users need to create a [Public Key Infrastructure (PKI)](https://en.wikipedia.org/wiki/Public_key_infrastructure "wikipedia:Public key infrastructure") which is detailed in the [Easy-RSA](/index.php/Easy-RSA "Easy-RSA") article. Once the needed certificates, private keys, and associated files are created via following the steps in the separate article, one should have 5 files in `/etc/openvpn/server` at this point:

```
ca.crt
dh.pem
servername.crt
servername.key
ta.key

```

Alternatively, as of OpenVPN 2.4, one can use Easy-RSA to generate certificates and keys using elliptic curves. See the OpenVPN documentation for details.

## A basic L3 IP routing configuration

**Note:** Unless otherwise explicitly stated, the rest of this article assumes a basic L3 IP routing configuration.

OpenVPN is an extremely versatile piece of software and many configurations are possible, in fact machines can be both servers and clients.

With the release of v2.4, server configurations are stored in `/etc/openvpn/server` and client configurations are stored in `/etc/openvpn/client` and each mode has its own respective systemd unit, namely, `openvpn-client@.service` and `openvpn-server@.service`.

### Example configuration

The OpenVPN package comes with a collection of example configuration files for different purposes. The sample server and client configuration files make an ideal starting point for a basic OpenVPN setup with the following features:

*   Uses [Public Key Infrastructure (PKI)](https://en.wikipedia.org/wiki/Public_key_infrastructure "wikipedia:Public key infrastructure") for authentication.
*   Creates a VPN using a virtual TUN network interface (OSI L3 IP routing).
*   Listens for client connections on UDP port 1194 (OpenVPN's official IANA port number[[1]](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml?search=openvpn)).
*   Distributes virtual addresses to connecting clients from the 10.8.0.0/24 subnet.

For more advanced configurations, please see the [openvpn(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/openvpn.8) man page and the [OpenVPN documentation](http://openvpn.net/index.php/open-source/documentation).

### The server configuration file

**Note:** Note that if the server is behind a firewall or a NAT translating router, the OpenVPN port must be forwarded on to the server.

Copy the example server configuration file `/usr/share/openvpn/examples/server.conf` to `/etc/openvpn/server/server.conf`.

Edit the file making a minimum of the following changes:

 `/etc/openvpn/server/server.conf` 
```
ca ca.crt
cert servername.crt
key servername.key
dh dh.pem
.
tls-crypt ta.key
.
user nobody
group nobody

```

#### Hardening the server

If security is a priority, additional configuration is recommended including: limiting the server to use a strong cipher/auth method and (optionally) limiting the set of enabled TLS ciphers to the newer ciphers. Starting from OpenVPN 2.4, the server and the client will automatically negotiate AES-256-GCM in TLS mode.

Add the following to `/etc/openvpn/server/server.conf`:

 `/etc/openvpn/server/server.conf` 
```
.
cipher AES-256-GCM
auth SHA512
tls-version-min 1.2
tls-cipher TLS-DHE-RSA-WITH-AES-256-GCM-SHA384:TLS-DHE-RSA-WITH-AES-128-GCM-SHA256:TLS-DHE-RSA-WITH-AES-256-CBC-SHA:TLS-DHE-RSA-WITH-CAMELLIA-256-CBC-SHA:TLS-DHE-RSA-WITH-AES-128-CBC-SHA:TLS-DHE-RSA-WITH-CAMELLIA-128-CBC-SHA
.

```

**Note:**

*   The .ovpn client profile **must** contain a matching cipher and auth line to work properly (at least with the iOS and Android client).
*   Using `tls-cipher` incorrectly may cause difficulty with debugging connections and may not be necessary. See [OpenVPN’s community wiki](https://community.openvpn.net/openvpn/wiki/Hardening#Useof--tls-cipher) for more information.

#### Enabling compression

Enabling compression is not recommended by upstream; doing so opens to the server the so-called VORACLE attack vector. See [this](https://community.openvpn.net/openvpn/wiki/VORACLE) article.

#### Deviating from the standard port and/or protocol

It is generally recommended to use OpenVPN over UDP, because [TCP over TCP is a bad idea](http://sites.inka.de/bigred/devel/tcp-tcp.html)[[2]](http://adsabs.harvard.edu/abs/2005SPIE.6011..138H).

Some networks may disallow OpenVPN connections on the default port and/or protocol. One strategy to circumvent this is to mimic HTTPS traffic which is very likely unobstructed.

To do so, configure `/etc/openvpn/server/server.conf` as such:

 `/etc/openvpn/server/server.conf` 
```
.
port 443
proto tcp
.

```

**Note:** The .ovpn client profile **must** contain a matching port and proto line to work properly!

#### Running multiple instances of OpenVPN on different ports on the physical machine

One can have multiple, concurrent instances of OpenVPN running on the same box. Each server needs to be defined in `/etc/openvpn/server/` as a separate .conf file. At a minimum, the parallel servers need to be running on different ports. A simple setup directs traffic connecting in to a separate IP pool. More advanced setups are beyond the scope of this guide.

Consider this example, running 2 concurrent servers, one port 443/udp and another on port 80/tcp.

First modify `/etc/openvpn/server/server.conf` created as so:

 `/etc/openvpn/server/server.conf` 
```
.
port 443
proto udp
server 10.8.0.0 255.255.255.0
.

```

Now copy it and modify the copy to run on 80/tcp:

 `/etc/openvpn/server/server2.conf` 
```
.
port 80
proto tcp
server 10.8.1.0 255.255.255.0
.

```

Be sure to setup the corresponding entries in the firewall, see the relevant sections in [#Firewall configuration](#Firewall_configuration).

### The client config profile

Copy the example client configuration file `/usr/share/openvpn/examples/client.conf` to `/etc/openvpn/client/`.

Edit the following:

*   The `remote` directive to reflect either the server's [Fully Qualified Domain Name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name "wikipedia:Fully qualified domain name"), hostname (as known to the client), or its IP address.
*   Uncomment the `user` and `group` directives to drop privileges.
*   The `ca`, `cert`, and `key` parameters to reflect the path and names of the keys and certificates.
*   Enable the TLS HMAC handshake protection (`--tls-crypt` or `--tls-auth`).

 `/etc/openvpn/client/client.conf` 
```
client
remote elmer.acmecorp.org 1194
.
user nobody
group nobody
ca ca.crt
cert client.crt
key client.key
.
tls-crypt ta.key # Replaces *tls-auth ta.key 1*

```

#### Run as unprivileged user

Using the options `user nobody` and `group nobody` in the configuration file makes *OpenVPN* drop its `root` privileges after establishing the connection. The downside is that upon VPN disconnect the daemon is unable to delete its set network routes again. If one wants to limit transmitting traffic without the VPN connection, then lingering routes may be considered beneficial. It can also happen, however, that the OpenVPN server pushes updates to routes at runtime of the tunnel. A client with dropped privileges will be unable to perform the update and exit with an error.

As it could seem to require manual action to manage the routes, the options `user nobody` and `group nobody` might seem undesirable. Depending on setup, however, there are different ways to handle these situations:

*   For errors of the unit, a simple way is to [edit](/index.php/Edit "Edit") it and add a `Restart=on-failure` to the `[Service]` section. Though, this alone will not delete any obsoleted routes, so it may happen that the restarted tunnel is not routed properly.
*   The package contains the `/usr/lib/openvpn/plugins/openvpn-plugin-down-root.so`, which can be used to let *openvpn* fork a process with root privileges with the only task to execute a custom script when receiving a down signal from the main process, which is handling the tunnel with dropped privileges (see also its [README](https://community.openvpn.net/openvpn/browser/plugin/down-root/README?rev=d02a86d37bed69ee3fb63d08913623a86c88da15)).

The OpenVPN HowTo's linked below go further by creating a dedicated non-privileged user/group, instead of the already existing `nobody`. The advantage is that this avoids potential risks when sharing a user among daemons:

*   The [OpenVPN HowTo](https://openvpn.net/index.php/open-source/documentation/howto.html#security) explains another way how to create an unprivileged user mode and wrapper script to have the routes restored automatically.
*   It is possible to let OpenVPN start as a non-privileged user in the first place, without ever running as root, see [this OpenVPN wiki](https://community.openvpn.net/openvpn/wiki/UnprivilegedUser) (howto). The howto assumes the presence of System V init, rather than [Systemd](/index.php/Systemd "Systemd") and does not cover the handling of `--up`/`--down` scripts - those should be handled the same way as the *ip* command, with additional attention to access rights.

**Tip:** [#openvpn-unroot](#openvpn-unroot) describes a tool to automate above setup.

### Converting certificates to encrypted .p12 format

Some software will only read VPN certificates that are stored in a password-encrypted .p12 file. These can be generated with the following command:

 `# openssl pkcs12 -export -inkey keys/bugs.key -in keys/bugs.crt -certfile keys/ca.crt -out keys/bugs.p12` 

### Testing the OpenVPN configuration

Run `# openvpn /etc/openvpn/server/server.conf` on the server, and `# openvpn /etc/openvpn/client/client.conf` on the client. Example output should be similar to the following:

 `# openvpn /etc/openvpn/server/server.conf` 
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
 `# openvpn /etc/openvpn/client/client.conf` 
```
Wed Dec 28 14:41:50 2011 OpenVPN 2.2.1 i686-pc-linux-gnu [SSL] [LZO2] [EPOLL] [eurephia] built on Aug 13 2011
Wed Dec 28 14:41:50 2011 NOTE: OpenVPN 2.1 requires '--script-security 2' or higher to call user-defined scripts or executables
.
.
Wed Dec 28 14:41:57 2011 GID set to nobody
Wed Dec 28 14:41:57 2011 UID set to nobody
Wed Dec 28 14:41:57 2011 Initialization Sequence Completed
```

[Find the IP address](/index.php/Network_configuration#IP_addresses "Network configuration") assigned to the tunX interface on the server, and [ping](/index.php/Ping "Ping") it from the client.

[Find the IP address](/index.php/Network_configuration#IP_addresses "Network configuration") assigned to the tunX interface on the client, and [ping](/index.php/Ping "Ping") it from the server.

**Note:** If using a firewall, make sure that IP packets on the TUN device are not blocked.

### Configure the MTU with Fragment and MSS

If experiencing issues when using (remote) services over OpenVPN (e.g. web browsing, [DNS](/index.php/DNS "DNS"), [NFS](/index.php/NFS "NFS")), it may be needed to set a MTU value manually.

The following message may indicate the MTU value should be adjusted:

```
read UDPv4 [EMSGSIZE Path-MTU=1407]: Message too long (code=90)

```

In order to get the maximum segment size (MSS), the client needs to discover the smallest MTU along the path to the server. In order to do this ping the server and disable fragmentation, then specify the maximum packet size [[3]](https://www.sonassi.com/help/troubleshooting/setting-correct-mtu-for-openvpn):

```
# ping -M do -s 1500 -c 1 example.com

```

Decrease the 1500 value by 10 each time, until the ping succeeds.

**Note:** Clients that do not support the 'fragment' directive (e.g. OpenELEC, [iOS app](https://docs.openvpn.net/connecting/connecting-to-access-server-with-apple-ios/faq-regarding-openvpn-connect-ios/)) are not able to connect to a server that uses the `fragment` directive. See `mtu-test` as alternative solution.

Update the client configuration to use the succeeded MTU value, e.g.:

 `/etc/openvpn/client/client.conf` 
```
remote example.com 1194
...
tun-mtu 1400 
mssfix 1360

```

OpenVPN may be instructed to test the MTU every time on client connect. Be patient, since the client may not inform about the test being run and the connection may appear as nonfunctional until finished. The following will add about 3 minutes to OpenVPN start time. It is advisable to configure the fragment size unless a client will be connecting over many different networks and the bottle neck is not on the server side:

 `/etc/openvpn/client/client.conf` 
```
remote example.com 1194
...
mtu-test
...

```

### IPv6

#### Connect to the server via IPv6

Starting from OpenVPN 2.4, OpenVPN will use `AF_INET` defined by the OS when just using `proto udp` or `proto tcp`, which in most cases will be IPv4 only. To use both IPv4 and IPv6, use `proto udp6` or `proto tcp6`. To enforce only IPv4-only, you need to use `proto udp4` or `proto tcp4`. On older OpenVPN versions, one server instance can only support either IPv4 or IPv6.

#### Provide IPv6 inside the tunnel

In order to provide IPv6 inside the tunnel, have an IPv6 prefix routed to the OpenVPN server. Either set up a static route on the gateway (if a static block is assigned), or use a DHCPv6 client to get a prefix with DHCPv6 Prefix delegation (see [IPv6 Prefix delegation](/index.php/IPv6#Prefix_delegation_(DHCPv6-PD) "IPv6") for details). Also consider using a unique local address from the address block fc00::/7\. Both methods have advantages and disadvantages:

*   Many ISPs only provide dynamically changing IPv6 prefixes. OpenVPN does not support prefix changes, so change the server.conf every time the prefix is changed (Maybe can be automated with a script).
*   ULA addresses are not routed to the Internet, and setting up NAT is not as straightforward as with IPv4\. This means one cannot route the entire traffic over the tunnel. Those wanting to connect two sites via IPv6, without the need to connect to the Internet over the tunnel, may want to use the ULA addresses for ease.

Alternatively, if you have no access to these mentioned methods, an NDP proxy should work. See [this StackExchange post](https://unix.stackexchange.com/questions/136211/routing-public-ipv6-traffic-through-openvpn-tunnel).

After having received a prefix (a /64 is recommended), append the following to the server.conf:

```
server-ipv6 2001:db8:0:123::/64

```

This is the IPv6 equivalent to the default 10.8.0.0/24 network of OpenVPN and needs to be taken from the DHCPv6 client. Or use for example fd00:1234::/64.

Those wanting to push a route to a home network (192.168.1.0/24 equivalent), need to also append:

```
push "route-ipv6 2001:db8:0:abc::/64"

```

OpenVPN does not yet include DHCPv6, so there is no method to e.g. push DNS server over IPv6\. This needs to be done with IPv4\. The [OpenVPN Wiki](https://community.openvpn.net/openvpn/wiki/IPv6) provides some other configuration options.

## Starting OpenVPN

### Manual startup

To troubleshoot a VPN connection, start the client's daemon manually with `openvpn /etc/openvpn/client/client.conf` as root. The server can be started the same way using its own configuration file (e.g., `openvpn /etc/openvpn/server/server.conf`).

### systemd service configuration

To start the OpenVPN server automatically at system boot, [enable](/index.php/Enable "Enable") `openvpn-server@*<configuration>*.service` on the applicable machine. For a client, [enable](/index.php/Enable "Enable") `openvpn-client@*<configuration>*.service` instead. (Leave `.conf` out of the `<configuration>` string.)

For example, if the client configuration file is `/etc/openvpn/client/*client*.conf`, the service name is `openvpn-client@*client*.service`. Or, if the server configuration file is `/etc/openvpn/server/*server*.conf`, the service name is `openvpn-server@*server*.service`.

### Letting NetworkManager start a connection

One might not always need to run a VPN tunnel and/or only want to establish it for a specific NetworkManager connection. This can be done by adding a script to `/etc/NetworkManager/dispatcher.d/`. In the following example "Provider" is the name of the NetworkManager connection:

 `/etc/NetworkManager/dispatcher.d/10-openvpn` 
```
#!/bin/bash

case "$2" in
  up)
    if [ "$CONNECTION_ID" == "Provider" ]; then
      systemctl start openvpn-client@*<configuration>*
    fi
  ;;
  down)
    systemctl stop openvpn-client@*<configuration>*
  ;;
esac
```

See [NetworkManager#Network services with NetworkManager dispatcher](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") for more details.

### Gnome configuration

To connect to an OpenVPN server through Gnome's built-in network configuration do the following. First, install [networkmanager-openvpn](https://www.archlinux.org/packages/?name=networkmanager-openvpn). Then go to the Settings menu and choose Network. Click the plus sign to add a new connection and choose VPN. From there, choose OpenVPN and manually enter the settings. One can optionally import [#The client config profile](#The_client_config_profile). Yet, be aware NetworkManager does not show error messages for options it does not import. To connect to the VPN simply turn the connection on and check the options are applied (e.g. via `journalctl -b -u NetworkManager`).

## Routing client traffic through the server

Without further configuration only traffic directly to and from the OpenVPN server's IP passes through the VPN. To have other traffic, like web traffic pass through the VPN, correspondent routes must be added. You can either add routes in the client's configuration or configure the server to push these routes to the client.

To redirect traffic to and from a subnet of the server, add `push "route <address pool> <subnet>"` right before the `remote <address> <port> udp/tcp`, like:

```
route 192.168.1.0 255.255.255.0

```

To redirect all traffic including Internet traffic to the server, add the following in the client's configuration:

```
redirect-gateway def1 bypass-dhcp ipv6

```

If you are running an IPv4-only server, drop the `ipv6` option. If you are going IPv6-only, use `redirect-gateway ipv6 !ipv4`.

To make the server push routes, [append](/index.php/Append "Append") `push "redirect-gateway def1 bypass-dhcp ipv6"` to the configuration file (i.e. `/etc/openvpn/server/server.conf`) [[4]](http://openvpn.net/index.php/open-source/documentation/howto.html#redirect) of the server. Note this is not a requirement and may even give performance issue:

```
push "redirect-gateway def1 bypass-dhcp ipv6"

```

If you are running an IPv4-only server, drop the `ipv6` option. If you are going IPv6-only, use `push "redirect-gateway ipv6 !ipv4"`

Use the `push "route <address pool> <subnet>"` option to allow clients reaching other subnets/devices behind the server:

```
push "route 192.168.1.0 255.255.255.0"
push "route 192.168.2.0 255.255.255.0"

```

Optionally, push local [DNS](/index.php/DNS "DNS") settings to clients (e.g. the DNS-server of the router and domain prefix *.internal*):

**Note:** One may need to use a simple [DNS](/index.php/DNS "DNS") forwarder like [BIND](/index.php/BIND "BIND") and push the IP address of the OpenVPN server as DNS to clients.

```
push "dhcp-option DNS 192.168.1.1"
push "dhcp-option DOMAIN internal"

```

After setting up the configuration file, [enable packet forwarding](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing") on the server. Additionally, the server's [firewall](/index.php/Firewall "Firewall") needs to be adjusted to allow VPN traffic, which is described below for both [ufw](#ufw) and [iptables](#iptables).

**Note:** There are potential pitfalls when routing all traffic through a VPN server. Refer to the [OpenVPN documentation](http://openvpn.net/index.php/open-source/documentation/howto.html#redirect) for more information.

### Firewall configuration

#### firewalld

If you use the default port 1194, enable the `openvpn` service. Otherwise, create a new service with a different port.

```
# firewall-cmd --zone=public --add-service openvpn

```

Now add masquerade to the zone:

```
# firewall-cmd --zone=FedoraServer --add-masquerade

```

Make these changes permanent:

```
# firewall-cmd --runtime-to-permanent

```

#### ufw

In order to allow [ufw](/index.php/Ufw "Ufw") forwarding (VPN) traffic [append](/index.php/Append "Append") the following to `/etc/default/ufw`:

 `/etc/default/ufw`  `DEFAULT_FORWARD_POLICY="ACCEPT"` 

Change `/etc/ufw/before.rules`, and [append](/index.php/Append "Append") the following code after the header and before the "*filter" line:

*   Change the IP/subnet mask to match the `server` set in the OpenVPN server configuration.
*   Change the [network interface](/index.php/Network_configuration#Check_the_connection "Network configuration") to the connection used by OpenVPN server.

 `/etc/ufw/before.rules` 
```
# NAT (Network Address Translation) table rules
*nat
:POSTROUTING ACCEPT [0:0]

# Allow traffic from clients to the interface
-A POSTROUTING -s 10.8.0.0/24 -o *interface* -j MASQUERADE

# Optionally duplicate this line for each subnet if your setup requires it
-A POSTROUTING -s 10.8.1.0/24 -o *interface* -j MASQUERADE

# do not delete the "COMMIT" line or the NAT table rules above will not be processed
COMMIT

# Don't delete these required lines, otherwise there will be errors
*filter
..
```

Make sure to open the chosen OpenVPN port (default 1194/udp):

```
# ufw allow 1194/udp

```

To apply the changes. [reload](/index.php/Reload "Reload")/[restart](/index.php/Restart "Restart") ufw:

```
# ufw reload

```

#### iptables

In order to allow VPN traffic through an [iptables](/index.php/Iptables "Iptables") firewall, first create an iptables rule for NAT forwarding [[5]](http://openvpn.net/index.php/open-source/documentation/howto.html#redirect) on the server. An example (assuming the interface to forward to is named `eth0`):

```
iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o eth0 -j MASQUERADE

```

If running multiple servers on different IP pools, add a corresponding line for each one, for example:

```
iptables -t nat -A POSTROUTING -s 10.8.1.0/24 -o eth0 -j MASQUERADE

```

If the server cannot be pinged through the VPN, one may need to add explicit rules to open up TUN/TAP interfaces to all traffic. If that is the case, do the following [[6]](https://community.openvpn.net/openvpn/wiki/255-qconnection-initiated-with-xxxxq-but-i-cannot-ping-the-server-through-the-vpn):

**Warning:** There are security implications for the following rules if one does not trust all clients which connect to the server. Refer to the [OpenVPN documentation on this topic](https://community.openvpn.net/openvpn/wiki/255-qconnection-initiated-with-xxxxq-but-i-cannot-ping-the-server-through-the-vpn) for more details.

```
iptables -A INPUT -i tun+ -j ACCEPT
iptables -A FORWARD -i tun+ -j ACCEPT
iptables -A INPUT -i tap+ -j ACCEPT
iptables -A FORWARD -i tap+ -j ACCEPT

```

Additionally be sure to accept connections from the OpenVPN port (default 1194) and through the physical interface.

When satisfied, make the changes permanent as shown in [iptables#Configuration and usage](/index.php/Iptables#Configuration_and_usage "Iptables").

Those with multiple `tun` or `tap` interfaces, or more than one VPN configuration can "pin" the name of the interface by specifying it in the OpenVPN config file, e.g. `tun22` instead of `tun`. This is advantageous if different firewall rules for different interfaces or OpenVPN configurations are wanted.

### Prevent leaks if VPN goes down

This prevents all traffic through the default interface (enp3s0 for example) and only allows traffic through tun0. If the OpenVPN connection drops, the system will lose its internet access thereby preventing connections through the default network interface.

One may want to set up a script to restart OpenVPN if it goes down.

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
 ufw allow in on enp3s0 from any port 1194
 ufw allow out on enp3s0 to any port 1194

```

**Warning:** DNS **will not** work **unless** running a dedicated DNS server like [BIND](/index.php/BIND "BIND").

Alternatively, one can allow DNS leaks. **Be sure to trust your DNS server!**

```
 # DNS
 ufw allow in from any to any port 53
 ufw allow out from any to any port 53

```

#### vpnfailsafe

Alternatively, the [vpnfailsafe](https://github.com/wknapik/vpnfailsafe) ([vpnfailsafe-git](https://aur.archlinux.org/packages/vpnfailsafe-git/)) script can be used by the client to prevent DNS leaks and ensure that all traffic to the internet goes over the VPN. If the VPN tunnel goes down, internet access will be cut off, except for connections to the VPN server(s). The script contains the functionality of [update-resolv-conf](#Update_resolv-conf_script), so the two do not need to be combined.

## L3 IPv4 routing

This section describes how to connect client/server LANs to each other using L3 IPv4 routing.

### Prerequisites for routing a LAN

For a host to be able to forward IPv4 packets between the LAN and VPN, it must be able to forward the packets between its NIC and its tun/tap device. See [Internet sharing#Enable packet forwarding](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing") for configuration details.

#### Routing tables

By default, all IP packets on a LAN addressed to a different subnet get sent to the default gateway. If the LAN/VPN gateway is also the default gateway, there is no problem and the packets get properly forwarded. If not, the gateway has no way of knowing where to send the packets. There are a couple of solutions to this problem.

*   Add a static route to the default gateway routing the VPN subnet to the LAN/VPN gateway's IP address.
*   Add a static route on each host on the LAN that needs to send IP packets back to the VPN.
*   Use [iptables](/index.php/Iptables "Iptables")' NAT feature on the LAN/VPN gateway to masquerade the incoming VPN IP packets.

### Connect the server LAN to a client

The server is on a LAN using the 10.66.0.0/24 subnet. To inform the client about the available subnet, add a push directive to the server configuration file: `/etc/openvpn/server/server.conf`  `push "route 10.66.0.0 255.255.255.0"` 
**Note:** To route more LANs from the server to the client, add more push directives to the server configuration file, but keep in mind that the server side LANs will need to know how to route to the client.

### Connect the client LAN to a server

Prerequisites:

*   Any subnets used on the client side, must be unique and not in use on the server or by any other client. In this example we will use 192.168.4.0/24 for the clients LAN.
*   Each client's certificate has a unique Common Name, in this case bugs.
*   The server may not use the duplicate-cn directive in its config file.
*   The CCD folder must be accessible via user and group defined in the server config file (typically nobody:nobody)

Create a client configuration directory on the server. It will be searched for a file named the same as the client's common name, and the directives will be applied to the client when it connects.

```
# mkdir -p /etc/openvpn/ccd

```

Create a file in the client configuration directory called bugs, containing the `iroute 192.168.4.0 255.255.255.0` directive. It tells the server what subnet should be routed to the client:

 `/etc/openvpn/ccd/bugs`  `iroute 192.168.4.0 255.255.255.0` 

Add the client-config-dir and the `route 192.168.4.0 255.255.255.0` directive to the server configuration file. It tells the server what subnet should be routed from the tun device to the server LAN:

 `/etc/openvpn/server/server.conf` 
```
client-config-dir ccd
route 192.168.4.0 255.255.255.0

```

**Note:** To route more LANs from the client to the server, add more iroute and route directives to the appropriate configuration files, but keep in mind that the client side LANs will need to know how to route to the server.

### Connect both the client and server LANs

Combine the two previous sections:

 `/etc/openvpn/server/server.conf` 
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

By default clients will not see each other. To allow IP packets to flow between clients and/or client LANs, add a client-to-client directive to the server configuration file:

 `/etc/openvpn/server/server.conf` 
```
client-to-client

```

In order for another client or client LAN to see a specific client LAN, add a push directive for each client subnet to the server configuration file (this will make the server announce the available subnet(s) to other clients):

 `/etc/openvpn/server/server.conf` 
```
client-to-client
push "route 192.168.4.0 255.255.255.0"
push "route 192.168.5.0 255.255.255.0"
..

```

**Note:** One may need to adjust the [firewall](#Firewall_configuration) to allow client traffic passing through the VPN server.

## DNS

The DNS servers used by the system are defined in `/etc/resolv.conf`. Traditionally, this file is the responsibility of whichever program deals with connecting the system to the network (e.g. Wicd, NetworkManager, etc.). However, OpenVPN will need to modify this file to be able to resolve names on the remote side. To achieve this in a sensible way, install [openresolv](/index.php/Openresolv "Openresolv"), which makes it possible for more than one program to modify `resolv.conf` without stepping on each-other's toes.

Before continuing, test openresolv by restarting the network connection and ensuring that `resolv.conf` states that it was generated by *resolvconf*, and that DNS resolution still works as before. No reconfiguration of openresolv should be required; it should be automatically detected and used by the network system.

For Linux, OpenVPN can send DNS host information, but expects an external process to act on it. This can be done with the `client.up` and `client.down` scripts packaged in `/usr/share/openvpn/contrib/pull-resolv-conf/`. See their comments on how to install them to `/etc/openvpn/client/`. The following is an excerpt of a resulting client configuration using the scripts in conjunction with *resolvconf* and options to [#Run as unprivileged user](#Run_as_unprivileged_user):

 `/etc/openvpn/client/*clienttunnel*.conf` 
```
user nobody
group nobody
# Optional, choose a suitable path to chroot into
chroot /srv
script-security 2
up /etc/openvpn/client/client.up 
plugin /usr/lib/openvpn/plugins/openvpn-plugin-down-root.so "/etc/openvpn/client/client.down tun0"

```

### Update resolv-conf script

**Note:** Using [update-systemd-resolved script](#Update_systemd-resolved_script) is recommended by update-resolv-conf author.

The [openvpn-update-resolv-conf](https://github.com/masterkorp/openvpn-update-resolv-conf) script is available as an alternative to packaged scripts. It needs to be saved for example at `/etc/openvpn/update-resolv-conf` and made [executable](/index.php/Executable "Executable").

If you prefer a package, there is [openvpn-update-resolv-conf-git](https://aur.archlinux.org/packages/openvpn-update-resolv-conf-git/) that does above for you. You still need to do the following.

Once the script is installed add lines like the following into the OpenVPN client configuration file:

```
script-security 2
up /etc/openvpn/update-resolv-conf
down /etc/openvpn/update-resolv-conf

```

**Note:** If manually placing the script on the filesystem, be sure to have [openresolv](https://www.archlinux.org/packages/?name=openresolv) installed.

Now, when launching the OpenVPN connection, `resolv.conf` should be updated accordingly, and also should get returned to normal when the connection is closed.

**Note:** When using `openresolv` with the *-p* or *-x* options in a script (as both the included `client.up` and `update-resolv-conf` scripts currently do), a DNS resolver like [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) or [unbound](https://www.archlinux.org/packages/?name=unbound) is required for `openresolv` to correctly update `/etc/resolv.conf`. In contrast, when using the default DNS resolution from `libc` the *-p* and *-x* options must be removed in order for `/etc/resolv.conf` to be correctly updated by `openresolv`. For example, if the script contains a command like `resolvconf -p -a` and the default DNS resolver from `libc` is being used, change the command in the script to be `resolvconf -a` .

### Update systemd-resolved script

**Note:** Since [systemd](/index.php/Systemd "Systemd") 229, [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") has exposed an API through DBus allowing management of DNS configuration on a per-link basis. Tools such as [openresolv](https://www.archlinux.org/packages/?name=openresolv) may not work reliably when `/etc/resolv.conf` is managed by `systemd-resolved`, and will not work at all if using `resolve` instead of `dns` in `/etc/nsswitch.conf`.

The [update-systemd-resolved](https://github.com/jonathanio/update-systemd-resolved) script links OpenVPN with `systemd-resolved` via DBus to update the DNS records.

Copy the script into `/etc/openvpn/scripts` and mark as [executable](/index.php/Executable "Executable") (or [install](/index.php/Install "Install") [openvpn-update-systemd-resolved](https://aur.archlinux.org/packages/openvpn-update-systemd-resolved/)) and [append](/index.php/Append "Append") the following lines into the OpenVPN client configuration file:

 `/etc/openvpn/client/client.conf` 
```
client
remote example.com 1194 udp
..
script-security 2
setenv PATH /usr/bin
up /etc/openvpn/scripts/update-systemd-resolved
down /etc/openvpn/scripts/update-systemd-resolved
down-pre

```

In order to send all DNS traffic through the VPN tunnel and prevent DNS leaks, also add the following line (see [[7]](https://github.com/jonathanio/update-systemd-resolved#dns-leakage)):

 `/etc/openvpn/client/client.conf` 
```
dhcp-option DOMAIN-ROUTE .

```

Make sure that the [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") service is configured and running.

### Override DNS servers using NetworkManager

By default [networkmanager-openvpn](https://www.archlinux.org/packages/?name=networkmanager-openvpn) plugin appends DNS servers provided by OpenVPN to `/etc/resolv.conf`. This may result in DNS instability (leakage).

The NetworkManager GUI does not provide any way to change this behavior, but it is possible to [completely override](https://bugs.launchpad.net/ubuntu/+source/network-manager/+bug/1211110/comments/92) DNS using connection configuration file.

If the override is applied, queries for non-public DNS records are sent to the external resolver, see [[8]](https://bugs.launchpad.net/network-manager/+bug/1624317).

To use DNS settings provided by the VPN connection add `dns-priority=-1` ([ipv4 section](https://developer.gnome.org/NetworkManager/stable/settings-ipv4.html)) to the file located at `/etc/NetworkManager/system-connections/*your_vpn_name*`, where `*your_vpn_name*` is the name of your VPN connection.

Making changes to the VPN connection with the NetworkManager GUI will remove the setting above.

To verify that the correct DNS server(s) are configured, see `resolvectl status` if systemd-resolved is in use, for other resolvers see [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution").

## L2 Ethernet bridging

For now see: [OpenVPN Bridge](/index.php/OpenVPN_Bridge "OpenVPN Bridge")

## Config generators

**Warning:** Users are highly recommended to pass through the manual configuration described above to gain knowledge about options and usage before using any additional automation scripts.

### ovpngen

The [ovpngen](https://aur.archlinux.org/packages/ovpngen/) package provides a simple shell script that creates OpenVPN compatible tunnel profiles in the unified file format suitable for the OpenVPN Connect app for Android and iOS.

Simply invoke the script with 5 tokens:

1.  Server Fully Qualified Domain Name of the OpenVPN server (or IP address).
2.  Full path to the CA cert.
3.  Full path to the client cert.
4.  Full path to the client private key.
5.  Full path to the server TLS shared secret key.
6.  Optionally a port number.
7.  Optionally a protocol (udp or tcp).

Example:

```
# ovpngen example.org /etc/openvpn/server/ca.crt /etc/easy-rsa/pki/signed/client1.crt /etc/easy-rsa/pki/private/client1.key /etc/openvpn/server/ta.key > foo.ovpn

```

If the server is configured to use tls-crypt, as is suggested in [#The server configuration file](#The_server_configuration_file), [manually edit](https://github.com/graysky2/ovpngen/issues/4) the resulting `foo.ovpn` replacing `<tls-auth>` and `</tls-auth>` with `<tls-crypt>` and `</tls-crypt>`.

The resulting `foo.ovpn` can be edited if desired as the script does insert some commented lines.

The client expects this file to be located in `/etc/openvpn/client/foo.conf`. Note the change in file extension from 'ovpn' to 'conf' in this case.

**Tip:** If the server.conf contains a specified cipher and/or auth line, it is highly recommended that users manually edit the generated .ovpn file adding matching lines for cipher and auth. Failure to do so may results in connection errors!

### openvpn-unroot

**Note:** If you intend to use a script such as the [#Update resolv-conf script](#Update_resolv-conf_script), you must add these scripts to your config before calling openvpn-unroot on it. Failing to do so will cause problems if the scripts require root permissions.

The steps necessary for OpenVPN to [#Run as unprivileged user](#Run_as_unprivileged_user), can be performed automatically using [openvpn-unroot](https://github.com/wknapik/openvpn-unroot) ([openvpn-unroot-git](https://aur.archlinux.org/packages/openvpn-unroot-git/)).

It automates the actions required for the [OpenVPN howto](https://community.openvpn.net/openvpn/wiki/UnprivilegedUser) by adapting it to systemd, and also working around the bug for persistent tun devices mentioned in the note.

## Troubleshooting

### Client daemon not reconnecting after suspend

[openvpn-reconnect](https://aur.archlinux.org/packages/openvpn-reconnect/), available on the AUR, solves this problem by sending a SIGHUP to openvpn after waking up from suspend.

Alternatively, restart OpenVPN after suspend by creating the following systemd service:

 `/etc/systemd/system/openvpn-reconnect.service` 
```
[Unit]
Description=Restart OpenVPN after suspend

[Service]
ExecStart=/usr/bin/pkill --signal SIGHUP --exact openvpn

[Install]
WantedBy=sleep.target
```

[Enable](/index.php/Enable "Enable") this service for it to take effect.

### Connection drops out after some time of inactivity

If the VPN-Connection drops some seconds after it stopped transmitting data and, even though it states it is connected, no data can be transmitted through the tunnel, try adding a `keepalive`directive to the server's configuration:

 `/etc/openvpn/server/server.conf` 
```
.
.
keepalive 10 120
.
.

```

In this case the server will send ping-like messages to all of its clients every 10 seconds, thus keeping the tunnel up. If the server does not receive a response within 120 seconds from a specific client, it will assume this client is down.

A small ping-interval can increase the stability of the tunnel, but will also cause slightly higher traffic. Depending on the connection, also try lower intervals than 10 seconds.

### PID files not present

The default systemd service file for openvpn-client does not have the --writepid flag enabled, despite creating /var/run/openvpn-client. If this breaks a config (such as an i3bar VPN indicator), simply change `openvpn-client@.service` using a [drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet"):

```
[Service]
ExecStart=
ExecStart=/usr/sbin/openvpn --suppress-timestamps --nobind --config %i.conf --writepid /var/run/openvpn-client/%i.pid

```

### Route configuration fails with systemd-networkd

When using [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") to manage network connections and attempting to tunnel all outgoing traffic through the VPN, OpenVPN may fail to add routes. This is a result of systemd-networkd attempting to manage the tun interface before OpenVPN finishes configuring the routes. When this happens, the following message will appear in the OpenVPN log.

```
openvpn[458]: RTNETLINK answers: Network is unreachable
openvpn[458]: ERROR: Linux route add command failed: external program exited with error status: 2

```

From systemd-233, systemd-networkd can be configured to ignore the tun connections and allow OpenVPN to manage them. To do this, create the following file:

 `/etc/systemd/network/90-tun-ignore.network` 
```
[Match]
Name=tun*

[Link]
Unmanaged=true
```

[Restart](/index.php/Restart "Restart") `systemd-networkd.service` to apply the changes. To verify that the changes took effect, start the previously problematic OpenVPN connection and run `networkctl`. The output should have a line similar to the following:

```
7 tun0             none               routable    unmanaged

```

### tls-crypt unwrap error: packet too short

This error shows up in the server log when a client that does not support tls-crypt, or a client that is misconfigured to use tls-auth while the server is configured to use tls-crypt, attempts to connect.

To support clients that do not support tls-crypt, replace `tls-crypt ta.key` with `tls-auth ta.key 0` (the default) in `server.conf`. Also replace `tls-crypt ta.key` with `tls-auth ta.key 1` (the default) in `client.conf`.

## See also

*   [Wikipedia:OpenVPN](https://en.wikipedia.org/wiki/OpenVPN "wikipedia:OpenVPN")
*   [Securing Network Communication with Stunnel, OpenSSH, and OpenVPN](https://www.infosecwriters.com/text_resources/pdf/securing_communication.pdf) (PDF)