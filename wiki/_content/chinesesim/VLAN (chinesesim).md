**翻译状态：** 本文是英文页面 [VLAN](/index.php/VLAN "VLAN") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-04-28，点击[这里](https://wiki.archlinux.org/index.php?title=VLAN&diff=0&oldid=371497)可以查看翻译后英文页面的改动。

Virtual LANs give you the ability to sub-divide a LAN. Linux can accept **VLAN** tagged traffic and presents each **VLAN ID** as a different network interface (eg: `eth0.100` for **VLAN ID** `100`)

本文介绍如何通过 [iproute2](https://www.archlinux.org/packages/?name=iproute2) 和 [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") 或 [netctl](/index.php/Netctl "Netctl") 配置 VLAN 。

## Contents

*   [1 配置](#.E9.85.8D.E7.BD.AE)
    *   [1.1 创建 VLAN 设备](#.E5.88.9B.E5.BB.BA_VLAN_.E8.AE.BE.E5.A4.87)
    *   [1.2 添加 IP](#.E6.B7.BB.E5.8A.A0_IP)
    *   [1.3 关闭设备](#.E5.85.B3.E9.97.AD.E8.AE.BE.E5.A4.87)
    *   [1.4 移除设备](#.E7.A7.BB.E9.99.A4.E8.AE.BE.E5.A4.87)
    *   [1.5 开机启动](#.E5.BC.80.E6.9C.BA.E5.90.AF.E5.8A.A8)
        *   [1.5.1 systemd-networkd](#systemd-networkd)
        *   [1.5.2 netctl](#netctl)
*   [2 排错](#.E6.8E.92.E9.94.99)
    *   [2.1 udev 重命名虚拟设备](#udev_.E9.87.8D.E5.91.BD.E5.90.8D.E8.99.9A.E6.8B.9F.E8.AE.BE.E5.A4.87)

## 配置

此前 Arch Linux 用 `vconfig` 命令设置 VLANs ，该命令已被 `ip` 命令取代。请确认 [iproute2](https://www.archlinux.org/packages/?name=iproute2) 已安装。

下面的范例假定 **网口** 是 `eth0`，**名字** 是 `eth0.100` ，**vlan id** 是 `100`。

### 创建 VLAN 设备

用下列命令添加 VLAN 网口：

```
# ip link add link eth0 name eth0.100 type vlan id 100

```

执行 `ip link` 命令确认 VLAN 已创建。

这个 VLAN 网口就像一个普通的物理网口，所有流经这个网口的数据包将被加上 VLAN tag 并流经它关联的物理网口（本例中的 `eth0`）。仅配置为相同 VLAN 的设备可接收这些数据包，否则将被丢弃。 Using a **name** like `eth0.100` is just convention and not enforced; you can alternatively use `eth0_100` or something descriptive like `IPTV`. To see the VLAN ID on an interface, in case you used an unconventional name:

```
# ip -d link show eth0.100

```

The `-d` flag shows full details on an interface:

```
# ip -d addr show
4: eno1.100@eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
   link/ether 96:4a:9c:84:36:51 brd ff:ff:ff:ff:ff:ff promiscuity 0 
   **vlan protocol 802.1Q id 100 <REORDER_HDR>** 
   inet6 fe80::944a:9cff:fe84:3651/64 scope link 
      valid_lft forever preferred_lft forever

```

### 添加 IP

Now add an IPv4 address to the just created vlan link, and activate the link:

```
# ip addr add 192.168.100.1/24 brd 192.168.100.255 dev eth0.100
# ip link set dev eth0.100 up

```

### 关闭设备

To cleanly shutdown the setting before you remove the link, you can do:

 `# ip link set dev eth0.100 down` 

### 移除设备

Removing a VLAN interface is significantly less convoluted

 `# ip link delete eth0.100` 

### 开机启动

#### systemd-networkd

Use the following configuration files:

 `/etc/systemd/network/*eno1*.network` 
```
[Match]
Name=eno1

[Network]
DHCP=v4
VLAN=eno1.100
VLAN=eno1.200

```
 `/etc/systemd/network/'eno1.100*.netdev*` 
```
[Netdev]
Name=eno1.100
Kind=vlan

[VLAN]
Id=100

```
 `/etc/systemd/network/'eno1.200*.netdev*` 
```
[Netdev]
Name=eno1.200
Kind=vlan

[VLAN]
Id=200

```

Then [enable](/index.php/Enable "Enable") `systemd-networkd.service`. See [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") for details.

#### netctl

You can use [netctl](/index.php/Netctl "Netctl") for this purpose, see the self-explanatory example profiles in `/etc/netctl/examples/vlan-{dhcp,static}` .

## 排错

### udev 重命名虚拟设备

An annoyance is that [udev](/index.php/Udev "Udev") may try to rename virtual devices as they are added, thus ignoring the **name** configured for them (in this case `eth0.100`).

For instance, if the following commands are issued:

```
# ip link add link eth0 name eth0.100 type vlan id 100
# ip link show 

```

This could generate the following output:

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 16436 qdisc noqueue state UNKNOWN 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP qlen 1000
    link/ether aa:bb:cc:dd:ee:ff brd ff:ff:ff:ff:ff:ff
3: rename1@eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state DOWN 
    link/ether aa:bb:cc:dd:ee:ff brd ff:ff:ff:ff:ff:ff

```

**udev** has ignored the configured virtual interface name `eth0.100` and autonamed it **rename1**.

The solution is to edit `/etc/udev/rules.d/network_persistent.rules` and append **DRIVERS=="?*"** to the end of the physical interface's configuration line.

For example, for the interface **aa:bb:cc:dd:ee:ff** (eth0):

 `/etc/udev/rules.d/network_persistent.rules` 
```
SUBSYSTEM=="net", ATTR{address}=="aa:bb:cc:dd:ee:ff", NAME="eth0", DRIVERS=="?*"

```

A reboot should mean that VLANs configure correctly with the names assigned to them.