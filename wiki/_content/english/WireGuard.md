From the [WireGuard](https://www.wireguard.io/) project homepage:

	Wireguard is an extremely simple yet fast and modern VPN that utilizes state-of-the-art cryptography. It aims to be faster, simpler, leaner, and more useful than IPSec, while avoiding the massive headache. It intends to be considerably more performant than OpenVPN. WireGuard is designed as a general purpose VPN for running on embedded interfaces and super computers alike, fit for many different circumstances. Initially released for the Linux kernel, it plans to be cross-platform and widely deployable. It is currently under heavy development, but already it might be regarded as the most secure, easiest to use, and simplest VPN solution in the industry.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Server](#Server)
    *   [2.2 Client](#Client)
*   [3 Setup a VPN server](#Setup_a_VPN_server)
    *   [3.1 Server](#Server_2)
    *   [3.2 Client](#Client_2)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 DKMS module not available](#DKMS_module_not_available)

## Installation

Install the [wireguard-dkms](https://www.archlinux.org/packages/?name=wireguard-dkms) and [wireguard-tools](https://www.archlinux.org/packages/?name=wireguard-tools) packages.

## Usage

To create a public and private key

```
$ wg genkey | tee privatekey | wg pubkey > publickey

```

The following demonstartes how to setup a simple connection between two peers.

#### Server

Setup a server connection that accepts connections from any IP with the correct private key

```
$ ip link add dev wg0 type wireguard
$ ip addr add 10.0.0.1/24 dev wg0
$ wg set wg0 listen-port 51820 private-key ./privatekey
$ wg set wg0 peer [client public key] allowed-ips 0.0.0.0/0

```

#### Client

Setup a client to connect with the server.

```
$ ip link add dev wg0 type wireguard
$ ip addr add 10.0.0.1/24 dev wg0
$ wg set wg0 private-key ./privatekey
$ wg set wg0 peer [server public key] allowed-ips 10.0.0.1/24 endpoint [server ip]:56104 persistent-keepalive 25

```

The config can be saved by utilizing `showconf`

```
$ wg showconf wg0 > /etc/wireguard/wg0.conf
$ wg setconf wg0 /etc/wireguard/wg0.conf

```

## Setup a VPN server

Wireguard comes with a tool to quickly create and tearn down VPN servers and clients, `wg-quick`. Note that the config file used here is not a valid config file that can be used with `wg setconf`.

#### Server

 `/etc/wireguard/wg0server.conf` 
```
[Interface]
Address = 10.200.100.1/24
PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
ListenPort = 51820
PrivateKey = [SERVER PRIVATE KEY]

[Peer]
PublicKey = [CLIENT PUBLIC KEY]
AllowedIPs = 10.200.100.2/32  # This denotes the clients IP.
```

Bring this interface up by using `wg-quick up wg0server`, and use `wg-quick down wg0server` to bring it down.

#### Client

 `/etc/wireguard/wg0.conf` 
```
[Interface]
Address = 10.200.100.2/32  # The client IP from wg0server.conf
PrivateKey = [CLIENT PRIVATE KEY]
DNS = 10.200.100.1

[Peer]
PublicKey = [SERVER PUBLICKEY]
AllowedIPs = 0.0.0.0/0
Endpoint = [SERVER ENDPOINT]:51820
PersistentKeepalive = 25
```

Bring this interface up by using `wg-quick up wg0`, and use `wg-quick down wg0` to bring it down.

## Troubleshooting

### DKMS module not available

If the following command does not list any module after you installed [wireguard-dkms](https://www.archlinux.org/packages/?name=wireguard-dkms),

```
$ modprobe wireguard && lsmod | grep wireguard

```

or if creating a new link returns

```
# ip link add dev wg0 type wireguard
RTNETLINK answers: Operation not supported

```

you probably miss the linux headers.

These headers are available in [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) or [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers) depending of the kernel installed on your system.