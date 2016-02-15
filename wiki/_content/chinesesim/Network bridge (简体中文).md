**翻译状态：** 本文是英文页面 [Network_bridge](/index.php/Network_bridge "Network bridge") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-05-07，点击[这里](https://wiki.archlinux.org/index.php?title=Network_bridge&diff=0&oldid=367464)可以查看翻译后英文页面的改动。

网桥是一种软件配置，用于连结两个或更多个不同网段。网桥的行为就像是一台虚拟的网络交换机，工作于透明模式（即其他机器不必关注网桥的存在与否）。任意的真实物理设备（例如 `eth0`）和虚拟设备（例如 `tap0`）都可以连接到网桥。

本文讲述如何创建至少包含一个以太网设备的网桥，这种应用常见于[QEMU](/index.php/QEMU "QEMU")、设置基于软件的访问点等场景。

## Contents

*   [1 创建网桥](#.E5.88.9B.E5.BB.BA.E7.BD.91.E6.A1.A5)
    *   [1.1 通过 bridge-utils](#.E9.80.9A.E8.BF.87_bridge-utils)
    *   [1.2 通过 iproute2](#.E9.80.9A.E8.BF.87_iproute2)
    *   [1.3 通过 netctl](#.E9.80.9A.E8.BF.87_netctl)
    *   [1.4 通过 systemd-networkd](#.E9.80.9A.E8.BF.87_systemd-networkd)
    *   [1.5 通过 NetworkManager](#.E9.80.9A.E8.BF.87_NetworkManager)
*   [2 分配 IP 地址](#.E5.88.86.E9.85.8D_IP_.E5.9C.B0.E5.9D.80)
*   [3 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [3.1 网桥使用无线网络端口](#.E7.BD.91.E6.A1.A5.E4.BD.BF.E7.94.A8.E6.97.A0.E7.BA.BF.E7.BD.91.E7.BB.9C.E7.AB.AF.E5.8F.A3)
*   [4 参阅](#.E5.8F.82.E9.98.85)

## 创建网桥

创建网桥有多种途径。

### 通过 bridge-utils

本节讲述用 [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils) 软件包里面的 _brctl_ 工具管理网桥。该软件包已进入官方仓库（[official repositories](/index.php/Official_repositories "Official repositories")）。_brctl_ 的完整选项清单请参阅 `man brctl`。

新建一个网桥：

```
# brctl addbr _bridge_name_

```

添加一个设备（例如`eth0`）到网桥：

```
# brctl addif _bridge_name_ eth0

```

显示当前存在的网桥及其所连接的网络端口：

```
$ brctl show

```

启动网桥：

```
# ip link set up dev _bridge_name_

```

删除网桥，需要先关闭它：

```
# ip link set dev _bridge_name_ down
# brctl delbr _bridge_name_

```

### 通过 iproute2

本节讲述用 [iproute2](https://www.archlinux.org/packages/?name=iproute2) 软件包里面的 _ip_ 工具管理网桥。该软件包包含在 [base](https://www.archlinux.org/groups/x86_64/base/) 包组中。

创建一个网桥并设置其状态为已启动：

```
# ip link add name _bridge_name_ type bridge
# ip link set dev _bridge_name_ up

```

添加一个网络端口（比如 eth0）到网桥中，要求先将该端口设置为混杂模式并启动该端口：

```
# ip link set dev eth0 promisc on
# ip link set dev eth0 up

```

把该端口添加到网桥中，再将其所有者设置为 `_bridge_name_` 就完成了配置：

```
# ip link set dev eth0 master _bridge_name_

```

要显示现存的网桥及其关联的端口，可以用 _bridge_ 工具（它也是 [iproute2](https://www.archlinux.org/packages/?name=iproute2) 的组成部分）。详阅 `man bridge`。

```
# bridge link show

```

若要删除网桥，应首先移除它所关联的所有端口，同时关闭端口的混杂模式并关闭端口以将其恢复至原始状态。

```
# ip link set eth0 promisc off
# ip link set eth0 down
# ip link set dev eth0 nomaster

```

当网桥的配置清空后就可以将其删除：

```
# ip link delete _bridge_name_ type bridge

```

### 通过 netctl

参阅 [Bridge with netctl](/index.php/Bridge_with_netctl "Bridge with netctl").

### 通过 systemd-networkd

参阅 [systemd-networkd#Bridge interface](/index.php/Systemd-networkd#Bridge_interface "Systemd-networkd").

### 通过 NetworkManager

Gnome's NetworkManager can create bridges, but currently will not auto-connect to them. Open Network Settings, add a new interface of type Bridge, add a new bridged connection, and select the MAC address of the device to attach to the bridge.

Now, find the UUID of the attached device (by default named "bridge0 slave 1"):

```
$ nmcli connection

```

Finally, enable that connection:

```
$ nmcli con up <UUID>

```

If NetworkManager's default interface for the device you added to the bridge connects automatically, you may want to disable that by clicking the gear next to it in Network Settings, and unchecking "Connect automatically" under "Identity."

## 分配 IP 地址

When the bridge is fully set up, it can be assigned an IP address:

```
# ip addr add dev _bridge_name_ 192.168.66.66/24

```

## 提示与技巧

### 网桥使用无线网络端口

To add a wireless interface to a bridge, you first have to assign the wireless interface to an access point or start an access point with [hostapd](/index.php/Software_access_point "Software access point"). Otherwise the wireless interface won't be added to the bridge.

See also [Bridging with a wireless NIC](https://wiki.debian.org/BridgeNetworkConnections#Bridging_with_a_wireless_NIC) on Debian wiki.

## 参阅

*   [Official documentation for bridge-utils](http://www.linuxfoundation.org/collaborate/workgroups/networking/bridge)
*   [Official documentation for iproute2](http://www.linuxfoundation.org/collaborate/workgroups/networking/iproute2)