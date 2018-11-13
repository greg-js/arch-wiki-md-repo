From the [WireGuard](https://www.wireguard.com/) project homepage:

	Wireguard is an extremely simple yet fast and modern VPN that utilizes state-of-the-art cryptography. It aims to be faster, simpler, leaner, and more useful than IPSec, while avoiding the massive headache. It intends to be considerably more performant than OpenVPN. WireGuard is designed as a general purpose VPN for running on embedded interfaces and super computers alike, fit for many different circumstances. Initially released for the Linux kernel, it plans to be cross-platform and widely deployable. It is currently under heavy development, but already it might be regarded as the most secure, easiest to use, and simplest VPN solution in the industry.

**Warning:** WireGuard has not undergone proper degrees of security auditing and the protocol is still subject to change.[[1]](https://www.wireguard.com/#work-in-progress)

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Peer A setup](#Peer_A_setup)
    *   [2.2 Peer B setup](#Peer_B_setup)
    *   [2.3 Basic checkups](#Basic_checkups)
    *   [2.4 Persistent configuration](#Persistent_configuration)
    *   [2.5 Example peer configuration](#Example_peer_configuration)
    *   [2.6 Example configuration for systemd-networkd](#Example_configuration_for_systemd-networkd)
*   [3 Setup a VPN server](#Setup_a_VPN_server)
    *   [3.1 Server](#Server)
    *   [3.2 Client (tunnel all traffic)](#Client_(tunnel_all_traffic))
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Routes are periodically reset](#Routes_are_periodically_reset)
    *   [4.2 Connection loss with NetworkManager](#Connection_loss_with_NetworkManager)
        *   [4.2.1 Using resolvconf](#Using_resolvconf)
        *   [4.2.2 Using dnsmasq](#Using_dnsmasq)
        *   [4.2.3 Using systemd-resolved](#Using_systemd-resolved)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Store private keys in encrypted form](#Store_private_keys_in_encrypted_form)

## Installation

[Install](/index.php/Install "Install") the [wireguard-tools](https://www.archlinux.org/packages/?name=wireguard-tools) package, which pulls in the [wireguard-dkms](https://www.archlinux.org/packages/?name=wireguard-dkms) package.

You also need the header files for your [Linux kernel](/index.php/Linux_kernel "Linux kernel"), for example [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) or [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers), otherwise you will not be able to load the `wireguard` module of the *wireguard-dkms* package.

## Usage

To create a public and private key on a peer:

```
$ wg genkey | tee privatekey | wg pubkey > publickey

```

Below commands will demonstrate how to setup a basic tunnel between two peers with the following settings:

 Peer A | Peer B |
| External IP address | 10.10.10.1/24 | 10.10.10.2/24 |
| Internal IP address | 10.0.0.1/24 | 10.0.0.2/24 |
| wireguard listening port | UDP/48574 | UDP/39814 |

The external addresses should already exist. For example, peer A should be able to ping peer B via `ping 10.10.10.2`, and vice versa. The internal addresses will be new addresses created by the *ip* commands below and will be shared internally within the new WireGuard network. The `/24` in the IP addresses is the [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing").

#### Peer A setup

This peer will listen on UDP port 48574 and will accept connection from peer B by linking its public key with both its inner and outer IPs addresses.

```
# ip link add dev wg0 type wireguard
# ip addr add 10.0.0.1/24 dev wg0
# wg set wg0 listen-port 48574 private-key ./privatekey
# wg set wg0 peer [Peer B public key] persistent-keepalive 25 allowed-ips 10.0.0.2/32 endpoint 10.10.10.2:39814
# ip link set wg0 up

```

`[Peer B public key]` should have the same format as `EsnHH9m6RthHSs+sd9uM6eCHe/mMVFaRh93GYadDDnM=`. `allowed-ips` is a list of addresses that peer A will be able to send traffic to. `allowed-ips 0.0.0.0/0` would allow sending traffic to any address.

#### Peer B setup

As with Peer A, whereas the wireguard daemon is listening on the UDP port 39814 and accept connection from peer A only.

```
# ip link add dev wg0 type wireguard
# ip addr add 10.0.0.2/24 dev wg0
# wg set wg0 listen-port 39814 private-key ./privatekey
# wg set wg0 peer [Peer A public key] persistent-keepalive 25 allowed-ips 10.0.0.1/32 endpoint 10.10.10.1:48574
# ip link set wg0 up

```

#### Basic checkups

Invoking the wg command without parameter will give a quick overview of the current configuration.

As an example, when Peer A has been configured we are able to see its identity and its associated peers:

```
 peer-a$ wg
 interface: wg0
   public key: UguPyBThx/+xMXeTbRYkKlP0Wh/QZT3vTLPOVaaXTD8=
   private key: (hidden)
   listening port: 48574

 peer: 9jalV3EEBnVXahro0pRMQ+cHlmjE33Slo9tddzCVtCw=
   endpoint: 10.10.10.2:39814
   allowed ips: 10.0.0.2/32

```

At this point one could reach the end of the tunnel:

```
 peer-a$ ping 10.0.0.2

```

#### Persistent configuration

The configuration can be saved by utilizing `showconf`:

```
# wg showconf wg0 > /etc/wireguard/wg0.conf
# wg setconf wg0 /etc/wireguard/wg0.conf

```

#### Example peer configuration

 `/etc/wireguard/wg0.conf` 
```
[Interface]
Address = 10.0.0.1/32
PrivateKey = [CLIENT PRIVATE KEY]

[Peer]
PublicKey = [SERVER PUBLICKEY]
AllowedIPs = 10.0.0.0/24, 10.123.45.0/24, 1234:4567:89ab::/48
Endpoint = [SERVER ENDPOINT]:51820
PersistentKeepalive = 25
```

#### Example configuration for systemd-networkd

 `/etc/systemd/network/30-wg0.netdev` 
```
[NetDev]
Name = wg0
Kind = wireguard
Description = Wireguard

[WireGuard]
PrivateKey = [CLIENT PRIVATE KEY]

[WireGuardPeer]
PublicKey = [SERVER PUBLIC KEY]
PresharedKey = [PRE SHARED KEY]
AllowedIPs = 10.0.0.0/24
Endpoint = [SERVER ENDPOINT]:51820
PersistentKeepalive = 25
```
 `/etc/systemd/network/30-wg0.network` 
```
[Match]
Name = wg0

[Network]
Address = 10.0.0.3/32
DNS = 10.0.0.1

[Route]
Gateway = 10.0.0.1
Destination = 10.0.0.0/24
```

## Setup a VPN server

Wireguard comes with a tool to quickly get started with Wireguard: *wg-quick*. Note that the configuration file used here is not a valid configuration file that can be used with `wg setconf`, and that you will possibly have to change at least the interface from `eth0` to the one you use.

#### Server

 `/etc/wireguard/wg0server.conf` 
```
[Interface]
Address = 10.0.0.1/24  # This is the virtual IP address, with the subnet mask we will use for the VPN
PostUp   = iptables -A FORWARD -i %i -j ACCEPT; iptables -A FORWARD -o %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -D FORWARD -o %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
ListenPort = 51820
PrivateKey = [SERVER PRIVATE KEY]

[Peer]
PublicKey = [CLIENT PUBLIC KEY]
AllowedIPs = 10.0.0.2/32  # This denotes the clients IP with a /32: the client only has ONE IP.
```

In order for the iptables rules to work, IPv4 forwarding should be enabled:

```
# sysctl net.ipv4.ip_forward=1

```

To make the change permanent, add `net.ipv4.ip_forward = 1` to `/etc/sysctl.d/99-sysctl.conf`.

Bring the interface up by using `wg-quick up wg0server`, and use `wg-quick down wg0server` to bring it down.

#### Client (tunnel all traffic)

 `/etc/wireguard/wg0.conf` 
```
[Interface]
Address = 10.0.0.2/24  # The client IP from wg0server.conf with the same subnet mask
PrivateKey = [CLIENT PRIVATE KEY]
DNS = 10.0.0.1

[Peer]
PublicKey = [SERVER PUBLICKEY]
AllowedIPs = 0.0.0.0/0, ::/0
Endpoint = [SERVER ENDPOINT]:51820
PersistentKeepalive = 25
```

Bring this interface up by using `wg-quick up wg0`, and use `wg-quick down wg0` to bring it down.

To bring this up automatically one can use `systemctl enable wg-quick@wg0`

If you use [NetworkManager](/index.php/NetworkManager "NetworkManager"), it may be necessary to also enable NetworkManager-wait-online.service `systemctl enable NetworkManager-wait-online.service`

or if you're using systemd-networkd, to enable systemd-networkd-wait-online.service `systemctl enable systemd-networkd-wait-online.service`

to wait until devices are network ready before attempting wireguard connection.

## Troubleshooting

### Routes are periodically reset

Make sure that [NetworkManager](/index.php/NetworkManager "NetworkManager") is not managing your Wireguard interface:

 `/etc/NetworkManager/conf.d/unmanaged.conf` 
```
[keyfile]
unmanaged-devices=interface-name:wg0
```

### Connection loss with NetworkManager

On desktop, connection loss can be experienced when all the traffic is tunnelled through a Wireguard interface: typically, the connection is seemingly lost after a while or upon new connection to an access point.

By default *wg-quick* uses a resolvconf provider such as [openresolv](/index.php/Openresolv "Openresolv") to register new [DNS](/index.php/DNS "DNS") entries (i.e. `DNS` keyword in the configuration file). However [NetworkManager](/index.php/NetworkManager "NetworkManager") does not use resolvconf by default: every time a new [DHCP](/index.php/DHCP "DHCP") lease is acquired, [NetworkManager](/index.php/NetworkManager "NetworkManager") overwrites the global DNS addresses with the DHCP-provided ones which might not be available through the tunnel.

#### Using resolvconf

If resolvconf is already used by the system and you still experience connection loss, make sure NetworkManager is configured to use it: [NetworkManager#Use openresolv](/index.php/NetworkManager#Use_openresolv "NetworkManager").

#### Using dnsmasq

See [Dnsmasq#openresolv](/index.php/Dnsmasq#openresolv "Dnsmasq") for configuration.

#### Using systemd-resolved

At the time of writing (Sept. 2018), the resolvconf-compatible mode offered by [systemd-resolvconf](https://www.archlinux.org/packages/?name=systemd-resolvconf) does not work with *wg-quick*. However [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") can still be used by *wg-quick* through the `PostUp` hook. First make sure that NetworkManager is configured with *systemd-resolved*: [NetworkManager#systemd-resolved](/index.php/NetworkManager#systemd-resolved "NetworkManager") and then alter the tunnel configuration:

 `/etc/wireguard/wg0.conf` 
```
[Interface]
Address = 10.0.0.2/24  # The client IP from wg0server.conf with the same subnet mask
PrivateKey = [CLIENT PRIVATE KEY]
PostUp = resolvectl domain %i "~."; resolvectl dns %i 10.0.0.1; resolvectl dnssec %i yes

[Peer]
PublicKey = [SERVER PUBLICKEY]
AllowedIPs = 0.0.0.0/0, ::0/0
Endpoint = [SERVER ENDPOINT]:51820
PersistentKeepalive = 25
```

Setting `"~."` as a domain name is necessary for *systemd-resolved* to give priority to the newly available DNS server.

No `PostDown` key is necessary as *systemd-resolved* automatically revert all parameters when `wg0` is torn down.

## Tips and tricks

### Store private keys in encrypted form

It may be desirable to store private keys in encrypted form, such as through use of [pass](https://www.archlinux.org/packages/?name=pass). Just replace the PrivateKey line under [Interface] in your configuration file with:

```
 PostUp = wg set %i private-key <(su user -c "export PASSWORD_STORE_DIR=/path/to/your/store/; pass WireGuard/private-keys/%i")

```

where user is your username. See the [wg-quick(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wg-quick.8) man page for more details.