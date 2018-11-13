From the [WireGuard](https://www.wireguard.com/) project homepage:

	Wireguard is an extremely simple yet fast and modern VPN that utilizes state-of-the-art cryptography. It aims to be faster, simpler, leaner, and more useful than IPSec, while avoiding the massive headache. It intends to be considerably more performant than OpenVPN. WireGuard is designed as a general purpose VPN for running on embedded interfaces and super computers alike, fit for many different circumstances. Initially released for the Linux kernel, it plans to be cross-platform and widely deployable. It is currently under heavy development, but already it might be regarded as the most secure, easiest to use, and simplest VPN solution in the industry.

**Warning:** *WireGuard has not undergone proper degrees of security auditing and the protocol is still subject to change.*[[1]](https://www.wireguard.com/#work-in-progress)

## Contents

*   [1 安装](#安装)
*   [2 使用](#使用)
    *   [2.1 Peer A 配置](#Peer_A_配置)
    *   [2.2 Peer B 配置](#Peer_B_配置)
    *   [2.3 基本检查](#基本检查)
    *   [2.4 配置持久化](#配置持久化)
    *   [2.5 示例 peer 配置](#示例_peer_配置)
*   [3 配置一个 VPN 服务器](#配置一个_VPN_服务器)
    *   [3.1 服务器](#服务器)
    *   [3.2 客户端 (转发所有流量)](#客户端_(转发所有流量))
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 DKMS module not available](#DKMS_module_not_available)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Store private keys in encrypted form](#Store_private_keys_in_encrypted_form)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [wireguard-tools](https://www.archlinux.org/packages/?name=wireguard-tools) 包.

## 使用

在 peer 上生成公钥和私钥：

```
$ wg genkey | tee privatekey | wg pubkey > publickey

```

下面的指令会演示如何以表中的配置建立一条两个 peer 之间的隧道

 Peer A | Peer B |
| External IP address | 10.10.10.1/24 | 10.10.10.2/24 |
| Internal IP address | 10.0.0.1/24 | 10.0.0.2/24 |
| wireguard listening port | UDP/48574 | UDP/39814 |

Peer 应当已经拥有外网地址。例如，peer A 应当能够通过 `ping 10.10.10.2` ping 通 peer B，反之亦然。内部地址是由下文 `ip` 命令创建的新地址，并且将在 WireGuard 网络中共享。IP地址中 `/24` 的含义详见 [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing")

#### Peer A 配置

这个 peer 将监听 UDP 端口 48574，通过将 peer B 的公钥与其内部和外部 IP 地址关联，接受来自 peer B 的连接。

```
# ip link add dev wg0 type wireguard
# ip addr add 10.0.0.1/24 dev wg0
# wg set wg0 listen-port 48574 private-key ./privatekey
# wg set wg0 peer [Peer B public key] persistent-keepalive 25 allowed-ips 10.0.0.2/32 endpoint 10.10.10.2:39814
# ip link set wg0 up

```

`[Peer B public key]` 的格式应当如同 `EsnHH9m6RthHSs+sd9uM6eCHe/mMVFaRh93GYadDDnM=`。`allowed-ips` 是 peer A 能够向之发送流量的地址列表。`allowed-ips 0.0.0.0/0` 将允许向任意地址发送流量。

#### Peer B 配置

如同 Peer A，只不过 wireguard 守护监听 UDP 端口 39814 并且只接受 peer A 的连接

```
# ip link add dev wg0 type wireguard
# ip addr add 10.0.0.2/24 dev wg0
# wg set wg0 listen-port 39814 private-key ./privatekey
# wg set wg0 peer [Peer A public key] persistent-keepalive 25 allowed-ips 10.0.0.1/32 endpoint 10.10.10.1:48574
# ip link set wg0 up

```

#### 基本检查

不带任何参数使用 wg 命令可以快速查看当前的配置。

例如，当 peer A 配置好之后，我们可以看见它的身份和与之关联的 peers。

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

此时我们可以 ping 通隧道的另一端：

```
 peer-a$ ping 10.0.0.2

```

#### 配置持久化

配置可以通过 `showconf` 来保存

```
# wg showconf wg0 > /etc/wireguard/wg0.conf
# wg setconf wg0 /etc/wireguard/wg0.conf

```

#### 示例 peer 配置

 `/etc/wireguard/wg0.conf` 
```
[Interface]
PrivateKey = [CLIENT PRIVATE KEY]

[Peer]
PublicKey = [SERVER PUBLICKEY]
AllowedIPs = 10.0.0.0/24, 10.123.45.0/24, 1234:4567:89ab::/48
Endpoint = [SERVER ENDPOINT]:51820
PersistentKeepalive = 25
```

## 配置一个 VPN 服务器

Wireguard 自带一个快速创建和销毁 VPN 服务器的工具，`wg-quick`。注意这里使用的配置文件不是一个能被 `wg setconf` 有效的配置文件，并且你可能至少要把 `eth0` 改成你实际使用的。

#### 服务器

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
AllowedIPs = 10.0.0.2/32  # 这表示客户端只有一个 ip。
```

要使 iptables 规则生效，启用 IPv4 转发：

```
# sysctl net.ipv4.ip_forward=1

```

永久保留这项改变，向 `/etc/sysctl.d/99-sysctl.conf` 添加 `net.ipv4.ip_forward = 1`。

使用 `wg-quick up wg0server` 启用 Interface，`wg-quick down wg0server` 用以关闭

#### 客户端 (转发所有流量)

 `/etc/wireguard/wg0.conf` 
```
[Interface]
Address = 10.0.0.2/24  # The client IP from wg0server.conf with the same subnet mask
PrivateKey = [CLIENT PRIVATE KEY]
DNS = 10.0.0.1

[Peer]
PublicKey = [SERVER PUBLICKEY]
AllowedIPs = 0.0.0.0/0, ::0/0
Endpoint = [SERVER ENDPOINT]:51820
PersistentKeepalive = 25
```

使用 `wg-quick up wg0` 来启用 Interface, 使用 `wg-quick down wg0` 来关闭。

使用 `systemctl enable wg-quick@wg0` 来自动启动。

如果你使用 [NetworkManager](/index.php/NetworkManager "NetworkManager"), 可能有必要启用 NetworkManager-wait-online.service `systemctl enable NetworkManager-wait-online.service`

或者你使用的是 systemd-networkd, 启用 systemd-networkd-wait-online.service `systemctl enable systemd-networkd-wait-online.service`

等待所有设备就绪再尝试 wireguard 连接

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

## Tips and tricks

### Store private keys in encrypted form

It may be desirable to store private keys in encrypted form, such as through use of [pass](https://www.archlinux.org/packages/?name=pass). Just replace the PrivateKey line under [Interface] in your config file with:

```
 PostUp = wg set %i private-key <(su user -c "export PASSWORD_STORE_DIR=/path/to/your/store/; pass WireGuard/private-keys/%i")

```

where user is your username. See the `wg-quick(8)` man page for more details.