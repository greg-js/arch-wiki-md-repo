From the [WireGuard](https://www.wireguard.com/) project homepage:

	WireGuard is an extremely simple yet fast and modern VPN that utilizes state-of-the-art cryptography. It aims to be faster, simpler, leaner, and more useful than IPSec, while avoiding the massive headache. It intends to be considerably more performant than OpenVPN. WireGuard is designed as a general purpose VPN for running on embedded interfaces and super computers alike, fit for many different circumstances. Initially released for the Linux kernel, it plans to be cross-platform and widely deployable.

**Warning:** WireGuard has not undergone proper degrees of security auditing and the protocol is still subject to change [[1]](https://www.wireguard.com/#work-in-progress).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Key generation](#Key_generation)
    *   [2.2 Peer A setup](#Peer_A_setup)
    *   [2.3 Peer B setup](#Peer_B_setup)
    *   [2.4 Basic checkups](#Basic_checkups)
    *   [2.5 Persistent configuration](#Persistent_configuration)
    *   [2.6 Example peer configuration](#Example_peer_configuration)
    *   [2.7 Example configuration for systemd-networkd](#Example_configuration_for_systemd-networkd)
*   [3 Specific use-case: VPN server](#Specific_use-case:_VPN_server)
    *   [3.1 Server](#Server)
    *   [3.2 Key generation](#Key_generation_2)
    *   [3.3 Server config](#Server_config)
    *   [3.4 Client config](#Client_config)
*   [4 Testing the tunnel](#Testing_the_tunnel)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Routes are periodically reset](#Routes_are_periodically_reset)
    *   [5.2 Broken DNS resolution](#Broken_DNS_resolution)
    *   [5.3 Low MTU](#Low_MTU)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Using systemd-networkd](#Using_systemd-networkd)
        *   [6.1.1 Server](#Server_2)
        *   [6.1.2 Client foo](#Client_foo)
        *   [6.1.3 Client bar](#Client_bar)
    *   [6.2 Store private keys in encrypted form](#Store_private_keys_in_encrypted_form)
    *   [6.3 Endpoint with changing IP](#Endpoint_with_changing_IP)
    *   [6.4 Generate QR code](#Generate_QR_code)
*   [7 See also](#See_also)

## Installation

1.  [Install](/index.php/Install "Install") [wireguard-tools](https://www.archlinux.org/packages/?name=wireguard-tools).
2.  Install the appropriate kernel module:
    *   [wireguard-arch](https://www.archlinux.org/packages/?name=wireguard-arch) for the default [linux](https://www.archlinux.org/packages/?name=linux) kernel.
    *   [wireguard-lts](https://www.archlinux.org/packages/?name=wireguard-lts) for the LTS [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) kernel.
    *   [wireguard-dkms](https://www.archlinux.org/packages/?name=wireguard-dkms) for the DKMS variant for other [kernels](/index.php/Kernel "Kernel").

**Note:** WireGuard has been merged in Linux 5.6\. [[2]](https://lists.zx2c4.com/pipermail/wireguard/2020-January/004906.html)

**Tip:** [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") and [NetworkManager](/index.php/NetworkManager "NetworkManager") both have native support for setting up WireGuard interfaces, they only require the kernel module.

*   For details on systemd-networkd, see [#Using systemd-networkd](#Using_systemd-networkd).
*   For NetworkManager, read the [WireGuard in NetworkManager blog post](https://blogs.gnome.org/thaller/2019/03/15/wireguard-in-networkmanager/).

## Usage

The below commands demonstrate how to setup a basic tunnel between two peers with the following settings:

 Peer A | Peer B |
| External IP address | 198.51.100.101 | 203.0.113.102 |
| Internal IP address | 10.0.0.1/24 | 10.0.0.2/24 |
| WireGuard listening port | UDP/51871 | UDP/51902 |

The external addresses should already exist. For example, peer A should be able to ping peer B via `ping 203.0.113.102`, and vice versa. The internal addresses will be new addresses created by the [ip(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip.8) commands below and will be shared internally within the new WireGuard network using [wg(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wg.8). The `/24` in the IP addresses is the [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing").

### Key generation

To create a private key:

```
$ wg genkey > privatekey

```

**Note:** It is recommended to only allow reading and writing access for the owner:
```
$ chmod 600 privatekey

```

To create a public key:

```
$ wg pubkey < privatekey > publickey

```

Alternatively, do this all at once:

```
$ wg genkey | tee privatekey | wg pubkey > publickey

```

One can also generate a preshared key to add an additional layer of symmetric-key cryptography to be mixed into the already existing public-key cryptography, for post-quantum resistance.

```
# wg genpsk > preshared

```

### Peer A setup

This peer will listen on UDP port 51871 and will accept connection from peer B by linking its public key with both its inner and outer IPs addresses.

```
# ip link add dev wg0 type wireguard
# ip addr add 10.0.0.1/24 dev wg0
# wg set wg0 listen-port 51871 private-key ./privatekey
# wg set wg0 peer *PEER_B_PUBLIC_KEY* persistent-keepalive 25 allowed-ips 10.0.0.2/32 endpoint 203.0.113.102:51902
# ip link set wg0 up

```

`*PEER_B_PUBLIC_KEY*` should have the same format as `EsnHH9m6RthHSs+sd9uM6eCHe/mMVFaRh93GYadDDnM=`. The keyword `allowed-ips` is a list of addresses that peer A will be able to send traffic to; `allowed-ips 0.0.0.0/0` would allow sending traffic to any IPv4 address, `::/0` allows sending traffic to any IPv6 address.

### Peer B setup

As with peer A, whereas the wireguard daemon is listening on the UDP port 51902 and accept connection from peer A only.

```
# ip link add dev wg0 type wireguard
# ip addr add 10.0.0.2/24 dev wg0
# wg set wg0 listen-port 51902 private-key ./privatekey
# wg set wg0 peer *PEER_A_PUBLIC_KEY* persistent-keepalive 25 allowed-ips 10.0.0.1/32 endpoint 198.51.100.101:51871
# ip link set wg0 up

```

### Basic checkups

Invoking the [wg(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wg.8) command without parameter will give a quick overview of the current configuration.

As an example, when Peer A has been configured we are able to see its identity and its associated peers:

 `[user@peer-a]# wg` 
```
interface: wg0
  public key: UguPyBThx/+xMXeTbRYkKlP0Wh/QZT3vTLPOVaaXTD8=
  private key: (hidden)
  listening port: 51871

peer: 9jalV3EEBnVXahro0pRMQ+cHlmjE33Slo9tddzCVtCw=
  endpoint: 203.0.113.102:51902
  allowed ips: 10.0.0.2/32
```

At this point one could reach the end of the tunnel:

```
[user@peer-a]$ ping 10.0.0.2

```

### Persistent configuration

The configuration can be saved by utilizing `showconf`:

```
# wg showconf wg0 > /etc/wireguard/wg0.conf
# wg setconf wg0 /etc/wireguard/wg0.conf

```

### Example peer configuration

 `/etc/wireguard/wg0.conf` 
```
[Interface]
PrivateKey = *CLIENT_PRIVATE_KEY*

[Peer]
PublicKey = *SERVER_PUBLICKEY*
AllowedIPs = 10.0.0.0/24, 10.123.45.0/24, 1234:4567:89ab::/48
Endpoint = *SERVER_ENDPOINT*:51871
PersistentKeepalive = 25
```

### Example configuration for systemd-networkd

See [#Using systemd-networkd](#Using_systemd-networkd).

## Specific use-case: VPN server

**Note:** Usage of the terms "server" and "client" are used here specifically for newcomers to WireGuard and for current users of OpenVPN to help familiarize with the construction of configuration files. WireGuard documentation simply refers to both of these concepts as "peers."

The purpose of this section is to setup a WireGuard "server" and generic "clients" to enable access to the server/network resources through an encrypted and secured tunnel like [OpenVPN](/index.php/OpenVPN "OpenVPN") and others. The server runs on Linux and the clients can run any number of platforms (the WireGuard Project offers apps on both iOS and Android platforms in addition to Linux, Windows and MacOS). See the official project [install link](https://www.wireguard.com/install/) for more.

**Tip:** Instead of using [wireguard-tools](https://www.archlinux.org/packages/?name=wireguard-tools) for server/client configuration, one may want to use [systemd-networkd](#Using_systemd-networkd) native WireGuard support.

### Server

On the peer that will act as the "server", first enable IPv4 forwarding using [sysctl](/index.php/Sysctl "Sysctl"):

```
# sysctl -w net.ipv4.ip_forward=1

```

To make the change permanent, add `net.ipv4.ip_forward = 1` to `/etc/sysctl.d/99-sysctl.conf`.

A properly configured [firewall](/index.php/Firewall "Firewall") is *HIGHLY recommended* for any Internet-facing device.

If the server have the public IP configured, be sure to:

*   Allow UDP traffic on the specified port(s) on which WireGuard will be running (for example allowing traffic on 51820/udp).
*   Setup the forwarding policy for the firewall if it is not included in the WireGuard config for the interface itself `/etc/wireguard/wg0.conf`. The example below should have the iptables rules and work as-is.

If the server is behind NAT, be sure to forward the specified port(s) on which WireGuard will be running (for example, 51820/UDP) from the router to the WireGuard server.

### Key generation

Generate key pairs for the server and for each client as explained in [#Key generation](#Key_generation).

### Server config

Create the "server" config file:

 `/etc/wireguard/wg0.conf` 
```
[Interface]
Address = 10.200.200.1/24
ListenPort = 51820
PrivateKey = *SERVER_PRIVATE_KEY*

# note - substitute *eth0* in the following lines to match the Internet-facing interface
# if the server is behind a router and receive traffic via NAT, this iptables rules are not needed
PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

[Peer]
# foo
PublicKey = *PEER_FOO_PUBLIC_KEY*
PresharedKey = *PRE-SHARED_KEY*
AllowedIPs = 10.200.200.2/32

[Peer]
# bar
PublicKey = *PEER_BAR_PUBLIC_KEY*
AllowedIPs = 10.200.200.3/32
```

Additional peers ("clients") can be listed in the same format as needed. Each peer requires the `PublicKey` to be set. However, specifying `PresharedKey` is optional.

Notice that the `Address` have mask "/24" and the clients on `AllowedIPs` "/32". The client only use their IP and the server only send back their respective address.

The interface can be managed manually using [wg-quick(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wg-quick.8) or using a [systemd](/index.php/Systemd "Systemd") service managed via [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1).

The interface may be brought up using `wg-quick up wg0` respectively by [starting](/index.php/Start "Start") and potentially [enabling](/index.php/Enable "Enable") the interface via `wg-quick@*interface*.service`, e.g. `wg-quick@wg0.service`. To close the interface use `wg-quick down wg0` respectively [stop](/index.php/Stop "Stop") `wg-quick@*interface*.service`.

### Client config

Create the corresponding "client" config file(s):

 `foo.conf` 
```
[Interface]
Address = 10.200.200.2/24
PrivateKey = *PEER_FOO_PRIVATE_KEY*
DNS = 10.200.200.1

[Peer]
PublicKey = *SERVER_PUBLICKEY*
PresharedKey = *PRE-SHARED_KEY*
AllowedIPs = 0.0.0.0/0, ::/0
Endpoint = my.ddns.example.com:51820
```
 `bar.conf` 
```
[Interface]
Address = 10.200.200.3/24
PrivateKey = *PEER_BAR_PRIVATE_KEY*
DNS = 10.200.200.1

[Peer]
PublicKey = *SERVER_PUBLICKEY*
PresharedKey = *PRE-SHARED KEY*
AllowedIPs = 0.0.0.0/0, ::/0
Endpoint = my.ddns.example.com:51820
```

Using the catch-all `AllowedIPs = 0.0.0.0/0, ::/0` will forward all IPv4 (`0.0.0.0/0`) and IPv6 (`::/0`) traffic over the VPN.

**Note:** Users of [NetworkManager](/index.php/NetworkManager "NetworkManager"), may need to [enable](/index.php/Enable "Enable") the `NetworkManager-wait-online.service` and users of [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") may need to [enable](/index.php/Enable "Enable") the `systemd-networkd-wait-online.service` to wait until devices are network ready before attempting wireguard connection.

## Testing the tunnel

Once a tunnel has been established, one can use [gnu-netcat](https://www.archlinux.org/packages/?name=gnu-netcat) to send traffic through it to test out throughput, CPU usage, etc. On one side of the tunnel, run `nc` in listen mode and on the other side, pipe some data from `/dev/zero` into `nc` in sending mode.

In the example below, port 2222 is used for the traffic (be sure to allow traffic on port 2222 if using a firewall).

On one side of the tunnel listen for traffic:

```
$ nc -vvlnp 2222

```

On the other side of the tunnel, send some traffic:

```
$ dd if=/dev/zero bs=1024K count=1024 | nc -v 10.0.0.203 2222

```

Status can be monitored using `wg` directly.

 `# wg` 
```
interface: wg0
  public key: UguPyBThx/+xMXeTbRYkKlP0Wh/QZT3vTLPOVaaXTD8=
  private key: (hidden)
  listening port: 51820

peer: 9jalV3EEBnVXahro0pRMQ+cHlmjE33Slo9tddzCVtCw=
  preshared key: (hidden)
  endpoint: 192.168.1.216:53207
  allowed ips: 10.0.0.0/0
  latest handshake: 1 minutes, 17 seconds ago
  transfer: 56.43 GiB received, 1.06 TiB sent
```

## Troubleshooting

### Routes are periodically reset

If you are not configuring WireGuard from [NetworkManager](/index.php/NetworkManager "NetworkManager"), make sure that NetworkManager is not managing the WireGuard interface(s):

 `/etc/NetworkManager/conf.d/unmanaged.conf` 
```
[keyfile]
unmanaged-devices=interface-name:wg*
```

### Broken DNS resolution

When tunneling all traffic through a WireGuard interface, the connection can become seemingly lost after a while or upon new connection. This could be caused by a [network manager](/index.php/Network_manager "Network manager") or [DHCP](/index.php/DHCP "DHCP") client overwriting `/etc/resolv.conf`.

By default *wg-quick* uses *resolvconf* to register new [DNS](/index.php/DNS "DNS") entries (from the `DNS` keyword in the configuration file). This will cause issues with [network managers](/index.php/Network_manager "Network manager") and [DHCP](/index.php/DHCP "DHCP") clients that do not use *resolvconf*, as they will overwrite `/etc/resolv.conf` thus removing the DNS servers added by wg-quick.

The solution is to use networking software that supports [resolvconf](/index.php/Resolvconf "Resolvconf").

**Note:** If you are using [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved"), make sure that [systemd-resolvconf](https://www.archlinux.org/packages/?name=systemd-resolvconf) is [installed](/index.php/Install "Install").

In case of [NetworkManager](/index.php/NetworkManager "NetworkManager"), it does not use resolvconf by default. This will not be an issue when using [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved"), but if you do not use systemd-resolved, [install](/index.php/Install "Install") [openresolv](https://www.archlinux.org/packages/?name=openresolv) and configure NetworkManager to use it: [NetworkManager#Use openresolv](/index.php/NetworkManager#Use_openresolv "NetworkManager").

### Low MTU

Due to too low MTU (lower than 1280), wg-quick may have failed to create the WireGuard interface. This can be solved by setting the MTU value in WireGuard configuration in Interface section on client.

 `/foo.config` 
```
[Interface]
Address = 10.200.200.2/24
MTU = 1500
PrivateKey = *PEER_FOO_PRIVATE_KEY*
DNS = 10.200.200.1
```

## Tips and tricks

### Using systemd-networkd

[systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") has native support for WireGuard protocols and therefore does not require the [wireguard-tools](https://www.archlinux.org/packages/?name=wireguard-tools) package.

In order to prevent leak of private keys, it is recommended to set the permissions of the *.netdev* file:

```
# chown root:systemd-network /etc/systemd/network/99-*.netdev
# chmod 0640 /etc/systemd/network/99-*.netdev

```

#### Server

 `/etc/systemd/network/99-server.netdev` 
```
[NetDev]
Name = wg0
Kind = wireguard
Description = WireGuard

[WireGuard]
ListenPort = 51820
PrivateKey = *SERVER_PRIVATE_KEY*

[WireGuardPeer]
PublicKey = PEER_FOO_PUBLIC_KEY
PresharedKey = *PRE-SHARED_KEY*
AllowedIPs = 10.200.200.2/32

[WireGuardPeer]
PublicKey = *PEER_BAR_PUBLIC_KEY*
PresharedKey = *PRE-SHARED_KEY*
AllowedIPs = 10.200.200.3/32
```
 `/etc/systemd/network/99-server.network` 
```
[Match]
Name = wg0

[Network]
Address = 10.200.200.1/32

[Route]
Gateway = 10.200.200.1
Destination = 10.200.200.0/24
```

#### Client foo

 `/etc/systemd/network/99-client.netdev` 
```
[NetDev]
Name = wg0
Kind = wireguard
Description = WireGuard

[WireGuard]
PrivateKey = *FOO_PRIVATE_KEY*

[WireGuardPeer]
PublicKey = *SERVER_PUBLICKEY*
PresharedKey = *PRE-SHARED_KEY*
AllowedIPs = 10.200.0.0/24
Endpoint = my.ddns.example.com:51820
PersistentKeepalive = 25
```
 `/etc/systemd/network/99-client.network` 
```
[Match]
Name = wg0

[Network]
Address = 10.200.200.2/32

[Route]
Gateway = 10.200.200.1
Destination = 10.200.200.0/24
GatewayOnlink=true
```

#### Client bar

 `/etc/systemd/network/99-client.netdev` 
```
[NetDev]
Name = wg0
Kind = wireguard
Description = WireGuard

[WireGuard]
PrivateKey = *PEER_BAR_PRIVATE_KEY*

[WireGuardPeer]
PublicKey = *SERVER_PUBLICKEY*
PresharedKey = *PRE-SHARED_KEY*
AllowedIPs = 10.200.0.0/24
Endpoint = my.ddns.example.com:51820
PersistentKeepalive = 25
```
 `/etc/systemd/network/99-client.network` 
```
[Match]
Name = wg0

[Network]
Address = 10.200.200.3/32

[Route]
Gateway = 10.200.200.1
Destination = 10.200.200.0/24
GatewayOnLink=true
```

### Store private keys in encrypted form

It may be desirable to store private keys in encrypted form, such as through use of [pass](https://www.archlinux.org/packages/?name=pass). Just replace the PrivateKey line under [Interface] in the configuration file with:

```
PostUp = wg set %i private-key <(su user -c "export PASSWORD_STORE_DIR=/path/to/your/store/; pass WireGuard/private-keys/%i")

```

where *user* is the Linux username of interest. See the [wg-quick(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wg-quick.8) man page for more details.

### Endpoint with changing IP

After resolving a server's domain, WireGuard [will not check for changes in DNS again](https://lists.zx2c4.com/pipermail/wireguard/2017-November/002028.html).

If the WireGuard server is frequently changing its IP-address due DHCP, Dyndns, IPv6, ..., any WireGuard client is going to lose its connection, until its endpoint is updated via something like `wg set "$INTERFACE" peer "$PUBLIC_KEY" endpoint "$ENDPOINT"`.

Also be aware, if the endpoint is ever going to change its address (for example when moving to a new provider/datacenter), just updating DNS will not be enough, so periodically running reresolve-dns might make sense on any DNS-based setup.

Luckily, [wireguard-tools](https://www.archlinux.org/packages/?name=wireguard-tools) provides an example script `/usr/share/wireguard/examples/reresolve-dns/reresolve-dns.sh`, that parses WG configuration files and automatically resets the endpoint address.

One needs to run the `/usr/share/wireguard/examples/reresolve-dns/reresolve-dns.sh /etc/wireguard/wg.conf` periodically to recover from an endpoint that has changed its IP.

One way of doing so is by updating all WireGuard endpoints once every thirty seconds[[3]](https://git.zx2c4.com/WireGuard/tree/contrib/examples/reresolve-dns/README) via a systemd timer:

 `/etc/systemd/system/wireguard_reresolve-dns.timer` 
```
[Unit]
Description=Periodically reresolve DNS of all WireGuard endpoints

[Timer]
OnCalendar=*:*:0/30

[Install]
WantedBy=timers.target
```
 `/etc/systemd/system/wireguard_reresolve-dns.service` 
```
[Unit]
Description=Reresolve DNS of all WireGuard endpoints
Wants=network-online.target
After=network-online.target

[Service]
Type=oneshot
ExecStart=/bin/sh -c 'for i in /etc/wireguard/*.conf; do /usr/share/wireguard/examples/reresolve-dns/reresolve-dns.sh "$i"; done'
```

Afterwards [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `wireguard_reresolve-dns.timer`

### Generate QR code

If the client is a mobile device such as a phone, [qrencode](https://www.archlinux.org/packages/?name=qrencode) can be used to generate client's configuration QR code and display it in terminal:

```
$ qrencode -t ansiutf8 < client.conf

```

## See also

*   [Wikipedia:WireGuard](https://en.wikipedia.org/wiki/WireGuard "wikipedia:WireGuard")
*   [Presentations by Jason Donenfeld](https://www.wireguard.com/presentations/).
*   [Mailing list](https://lists.zx2c4.com/mailman/listinfo/wireguard)
*   [Unofficial WireGuard Documentation](https://docs.sweeting.me/s/wireguard)
*   [Debian:Wireguard](https://wiki.debian.org/Wireguard "debian:Wireguard")