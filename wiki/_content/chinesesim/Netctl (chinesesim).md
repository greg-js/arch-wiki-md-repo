相关文章

*   [网络配置](/index.php/%E7%BD%91%E7%BB%9C%E9%85%8D%E7%BD%AE "网络配置")
*   [无线网络配置](/index.php/%E6%97%A0%E7%BA%BF%E7%BD%91%E7%BB%9C%E9%85%8D%E7%BD%AE "无线网络配置")
*   [Wicd (简体中文)](/index.php/Wicd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wicd (简体中文)")
*   [网桥](/index.php/%E7%BD%91%E6%A1%A5 "网桥")

**翻译状态：** 本文是英文页面 [Netctl](/index.php/Netctl "Netctl") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-01-10，点击[这里](https://wiki.archlinux.org/index.php?title=Netctl&diff=0&oldid=504831)可以查看翻译后英文页面的改动。

Netctl 是基于命令行的网络管理器，支持场景配置。它是 Arch Linux 网络管理方面的原生项目。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 配置](#配置)
*   [3 使用](#使用)
    *   [3.1 启动配置文件](#启动配置文件)
    *   [3.2 启用配置文件](#启用配置文件)
    *   [3.3 特殊 systemd 单元](#特殊_systemd_单元)
        *   [3.3.1 有线连接](#有线连接)
        *   [3.3.2 无线连接](#无线连接)
*   [4 提示与技巧](#提示与技巧)
    *   [4.1 配置示例](#配置示例)
        *   [4.1.1 有线连接](#有线连接_2)
        *   [4.1.2 无线连接(WPA-PSK)](#无线连接(WPA-PSK))
    *   [4.2 隐藏无线密码](#隐藏无线密码)
    *   [4.3 使用体验版图形用户界面](#使用体验版图形用户界面)
    *   [4.4 Eduroam](#Eduroam)
    *   [4.5 绑定](#绑定)
        *   [4.5.1 负载均衡](#负载均衡)
        *   [4.5.2 有线 -> 无线故障切换](#有线_->_无线故障切换)
    *   [4.6 使用任意接口](#使用任意接口)
    *   [4.7 使用钩子](#使用钩子)
        *   [4.7.1 范例](#范例)
            *   [4.7.1.1 在已有连接上执行命令](#在已有连接上执行命令)
            *   [4.7.1.2 激活 network-online.target](#激活_network-online.target)
            *   [4.7.1.3 设置默认 DHCP 客户端](#设置默认_DHCP_客户端)
*   [5 排错](#排错)
    *   [5.1 Job for netctl@wlan(...).service failed](#Job_for_netctl@wlan(...).service_failed)
    *   [5.2 dhcpcd: ipv4_addroute: File exists](#dhcpcd:_ipv4_addroute:_File_exists)
    *   [5.3 DHCP timeout issues](#DHCP_timeout_issues)
    *   [5.4 Connection timeout issues](#Connection_timeout_issues)
    *   [5.5 Problems with netctl-auto on resume](#Problems_with_netctl-auto_on_resume)
    *   [5.6 netctl-auto suddenly stopped working for WiFi adapters](#netctl-auto_suddenly_stopped_working_for_WiFi_adapters)
    *   [5.7 netctl-auto does not automatically unblock a wireless card to use an interface](#netctl-auto_does_not_automatically_unblock_a_wireless_card_to_use_an_interface)
    *   [5.8 RTNETLINK answers: File exists (with multiple NICs)](#RTNETLINK_answers:_File_exists_(with_multiple_NICs))
*   [6 参见](#参见)

## 安装

[netctl](https://www.archlinux.org/packages/?name=netctl) 是 [base](https://www.archlinux.org/groups/x86_64/base/) 包组的成员，所以系统中应当已经安装了。否则可以手工[安装](/index.php/Install "Install")。 netctl 有一些用于自动连接的[#特殊 systemd 单元](#特殊_systemd_单元)需要一些附加依赖包，详情参阅该章节。 下表列出 netctl 的其他可选依赖包：

| 功能 | 依赖 |
| WPA | [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) |
| DHCP | [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) or [dhclient](https://www.archlinux.org/packages/?name=dhclient) |
| Wifi menus | [dialog](https://www.archlinux.org/packages/?name=dialog) |
| PPPoE | [ppp](https://www.archlinux.org/packages/?name=ppp) |

**警告:** 请使用`systemctl --type=service`确保其它可以配置网络的服务都没有运行，同时使用多个网络配置工具会导致冲突。

## 配置

`netctl` 使用配置文件来管理网络连接，并按需自动或手动启动不同的操作模式

*netctl*的配置文件保存在 `/etc/netctl/` 。一些配置文件的示例位于 `/etc/netctl/examples/`。

若要使用上述示例配置文件，只需将其从 `/etc/netctl/examples/` 复制到 `/etc/netctl/` 并按需配置。参见下述[#配置示例](#配置示例)。编辑配置文件所需的首要参数是网络*端口(interface)*，详阅[网络配置#更改设备名称](/index.php/%E7%BD%91%E7%BB%9C%E9%85%8D%E7%BD%AE#更改设备名称 "网络配置")。

**提示：**

如要配置无线网络，可以用 root 身份运行 `wifi-menu -o` 以自动在 `/etc/netctl/` 中生成配置文件。*wifi-menu* 需要 [dialog](https://www.archlinux.org/packages/?name=dialog) 包。

如要在有线网络接口上启用静态IP，并忽略线缆连接状况，可以在配置文件中添加 `SkipNoCarrier=yes` 配置项

配置文件的完整配置项清单请参阅：[netctl.profile.5](http://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.profile.5)

## 使用

netctl 的完整命令清单请参阅：[netctl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.1)

### 启动配置文件

创建了一个配置文件之后请尝试用它建立一个连接。下例中的 *profile* 仅使用配置文件的文件名，不要带全路径名。

```
# netctl start profile

```

如果上面的命令返回失败，可以使用 `journalctl -xn` 和 `netctl status *profile*` 命令获取进一步的失败原因信息。

### 启用配置文件

下列命令实现开机时自动启动配置文件：

```
# netctl enable *profile*

```

这条命令将创建并启用一个随计算机启动而自动运行的 [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 服务。对配置文件本身的修改无法自动关联到前述创建的服务文件，修改之后，需用下述命令重新启用该配置：

```
# netctl reenable *profile*

```

启用的配置文件将在下次引导时自动启动。显然，只有线缆已连接或已处于无线信号覆盖区域时，配置文件才能成功启动。

如果需要在多个配置文件之间频繁切换（比如携带笔记本电脑旅行），应改用 [#特殊 systemd 单元](#特殊_systemd_单元) 一节的方法代替本节所述方法。

### 特殊 systemd 单元

*netctl* 提供了特殊的 [systemd](/index.php/Systemd "Systemd") 服务以实现有线与无线连接的自动切换。这些特殊的 systemd 单元的完整清单请参阅 [netctl.special(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.special.7)。

#### 有线连接

[安装](/index.php/Install "Install") [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) 包，并且[启动/启用](/index.php/Start/enable "Start/enable") `netctl-ifplugd@*interface*.service` systemd 单元。网线插入/拔出时，DHCP 配置文件将被启动/停止。

*   `netctl-ifplugd@*interface*.service` 优先启用使用了 [DHCP](https://en.wikipedia.org/wiki/DHCP "wikipedia:DHCP") 的配置文件。
*   若要自动启动一个静态 IP 配置文件，需要在其中增加 `ExcludeAuto=no` 配置项。
*   若要使某个静态 IP 配置文件的优先级高于使用 DHCP 的配置文件，可以增加 `Priority=2` 配置项，这将使其优先级高于使用 DHCP 的配置文件默认的 `Priority=1`。

#### 无线连接

[安装](/index.php/Install "Install") [wpa_actiond](https://aur.archlinux.org/packages/wpa_actiond/) 包并[启动/启用](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#使用单元 "Systemd (简体中文)") `netctl-auto@*interface*.service` systemd 单元。当在不同网络覆盖区域间移动（漫游）时，*netctl* 配置文件将会自动启动/停止。

*   *netctl-auto* 要求配置文件必须使用 `Security=wpa-configsection` 或 `Security=wpa` 配置项才能工作，不能使用 `Security=wpa-config` 配置项。

*   如果希望某些无线网络配置**不要**被 `netctl-auto@*interface*.service`自动启用，需要特别在该配置文件中加入 `ExcludeAuto=yes` 。
*   如果存在多个无线访问点可用，可以在 *WPAConfigSection* 配置节中加入 `priority=` 配置项（参阅 `/etc/netctl/examples/wireless-wpa-configsection`）。

注意，服务单元名称中的 *interface* 一词不要原文照抄，应当替换成实际的接口设备名，如 `netctl-auto@wlp4s0.service`。详情参阅 `netctl.profile(5)`。

**注意:**

*   如果任何一个配置文件包含错误，例如包含空变量 `Key=`，即使这个文件未被使用，也将加载失败并报错 `"Failed to read or parse configuration '/run/network/wpa_supplicant_wlan0.conf'`。
*   本方法与 [启用配置文件](#启用配置文件) 矛盾。如果你之前已经通过netctl启用了一个配置文件，运行 `netctl disable *profile*` 来防止这个配置在计算机启动时被启用两次。

通过 netctl-auto 的命令动作可以在不停止 `netctl-auto.service` 服务的情况下手工控制一个不受 netctl-auto 管理的网络接口。完整的 netctl-auto 命令动作列表参阅 [netctl-auto(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl-auto.1)。

## 提示与技巧

### 配置示例

#### 有线连接

For a DHCP connection, only the `Interface` has to be configured after copying the `/etc/netctl/examples/ethernet-dhcp` example profile to `/etc/netctl`.

For example:

 `/etc/netctl/*my_dhcp_profile*` 
```
Interface=enp1s0
Connection=ethernet
IP=dhcp

```

For a static IP configuration copy the `/etc/netctl/examples/ethernet-static` example profile to `/etc/netctl` and modify `Interface`, `Address`, `Gateway` and `DNS`) as needed.

For example:

 `/etc/netctl/*my_static_profile*` 
```
Interface=enp1s0
Connection=ethernet
IP=static
Address=('10.1.10.2/24')
Gateway=('10.1.10.1')
DNS=('10.1.10.1')

```

Take care to include the subnet notation of `/24`. It equates to a netmask of `255.255.255.0`) and without it the profile will fail to start. See also [CIDR notation](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing"). To alias more than one IP address per a NIC set `Address=('10.1.10.2/24' '192.168.1.2/24')`.

#### 无线连接(WPA-PSK)

The following applies for the standard wireless connections using a pre-shared key (WPA-PSK).

 `/etc/netctl/wireless-wpa` 
```
Description='A simple WPA encrypted wireless connection using 256-bit PSK'
Interface=wlp2s2
Connection=wireless
Security=wpa
IP=dhcp
ESSID=*your_essid*
Key=\"64cf3ced850ecef39197bb7b7b301fc39437a6aa6c6a599d0534b16af578e04a
```

**注意:**

*   Make sure to use the **special quoting rules** for the `Key` variable as explained at the end of [netctl.profile(5)](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.profile.5.txt).
*   If the passphrase fails, try removing the `\"` in the `Key` variable.
*   Although "encrypted", the key that you put in the profile configuration is enough to connect to a WPA-PSK network. Therefore this process is only useful for hiding the human-readable version of the passphrase. This will not prevent anyone with read access to this file from connecting to the network.

### 隐藏无线密码

You can also follow the following step to obfuscate the wireless passphrase (*wifi-menu* does it automatically when using the `-o` flag):

Users **not** wishing to have the passphrase to their wireless network stored in *plain text* have the option of storing the corresponding 256-bit pre-shared key instead, which is calculated from the passphrase and the SSID using standard algorithms.

Calculate your 256-bit PSK using [wpa_passphrase](/index.php/WPA_supplicant#Connecting_with_wpa_passphrase "WPA supplicant"):

 `$ wpa_passphrase *your_essid*` 
```
network={
  ssid="*your_essid*"
  #psk="*passphrase*"
  psk=64cf3ced850ecef39197bb7b7b301fc39437a6aa6c6a599d0534b16af578e04a
}
```

The *pre-shared key* (psk) now needs to replace the plain text passphrase of the `Key` variable in the profile.

### 使用体验版图形用户界面

如果你想使用图形用户界面管理 *netctl* 和你的网络连接，并且不在意使用非官方体验版软件包的话，可以从 [AUR](/index.php/AUR "AUR") 安装 [netgui](https://aur.archlinux.org/packages/netgui/)。注意：它毕竟还只是一个 beta 版，你应该熟悉 *netctl* 的语法以便解决可能出现的问题。另一个图形用户界面程序的替代品是 [netctl-gui](https://aur.archlinux.org/packages/netctl-gui/)，它提供了基于 Qt 的图形界面、DBus 守护进程和 KDE 桌面小部件。第三个替代品是 [netmenu](https://aur.archlinux.org/packages/netmenu/)，它使用 [dmenu](https://www.archlinux.org/packages/?name=dmenu) 作为图形界面。

### Eduroam

参阅 [WPA2 Enterprise#netctl](/index.php/WPA2_Enterprise#netctl "WPA2 Enterprise")

### 绑定

引自 [内核文档](https://www.kernel.org/doc/Documentation/networking/bonding.txt):

	*The Linux bonding driver provides a method for aggregating multiple network interfaces into a single logical "bonded" interface. The behavior of the bonded interfaces depends on the mode. Generally speaking, modes provide either hot standby or load balancing services. Additionally, link integrity monitoring may be performed.*

	*（Linux bonding 驱动提供了把多个网络接口聚合成一个“绑定”的单一逻辑接口的途径。绑定后接口的行为取决于绑定的模式，一般来说，提供“主备”和“负载均衡”两种模式。另外，可以提供对连接总体情况的监测功能。）*

#### 负载均衡

要用 netctl 配合 bonding，需要从官方软件源安装 [ifenslave](https://www.archlinux.org/packages/?name=ifenslave)。

复制 `/etc/netctl/examples/bonding` 到 `/etc/netctl/bond0` 然后进行编辑。例如:

 `/etc/netctl/bond0` 
```
Description='Bond Interface'
Interface='bond0'
Connection=bond
BindsToInterfaces=('eth0' 'eth1')
IP=dhcp
IP6=stateless
```

现在你可以停用之前的配置文件。然后设置 bonding 为自动启动，切换到新的配置。例如：

```
# netctl switch-to bond0

```

**注意:** 这将使用 `bonding` 驱动的默认策略 round-robin（负载均衡）。详见[官方文档](https://www.kernel.org/doc/Documentation/networking/bonding.txt)。

**提示：** 查看状态和绑定模式： `$ cat /proc/net/bonding/bond0` 

#### 有线 -> 无线故障切换

这一部分探讨怎样用bonding来实现当有线以太网无法工作时自动切换至无线网络。我们假设所有的网络接口默认启动dhcdpcd服务。

你需要从官方源安装软件包：[ifenslave](https://www.archlinux.org/packages/?name=ifenslave) 和 [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant).

首先设置 `bonding` 驱动使用 `active-backup`:

 `/etc/modprobe.d/bonding.conf` 
```
options bonding mode=active-backup
options bonding miimon=100
options bonding primary=eth0
options bonding max_bonds=0
```

`max_bonds` 选项避免了 `Interface bond0 already exists` 错误。如果使用了MAC过滤，应当添加设置 `fail_over_mac=active`。

接下来，编写一个netctl配置文件来绑定两个网络接口：

 `/etc/netctl/failover` 
```
Description='A wired connection with failover to wireless'
Interface='bond0'
Connection=bond
BindsToInterfaces=('eth0' 'wlan0')
IP='dhcp'
SkipNoCarrier='no'
```

设置该配置文件自启动：

```
# netctl enable failover

```

将 wpa_supplicant 配置为关联一个已知网络，可以通过 netctl profile (记得设置 IP='no'), 和一个长期运行的 wpa_supplicant 服务或者 wpa_cli 命令实现。具体方法请访问 [wpa_supplicant](/index.php/WPA_supplicant_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "WPA supplicant (简体中文)") 页面。想要长期运行 wpa_supplicant 服务，创建一个wpa_supplicant配置文件`/etc/wpa_supplicant/wpa_supplicant-wlan0.conf` 然后运行：

```
# systemctl enable wpa_supplicant@wlan0

```

在有线网络配置中设置`IP='no'`。IP地址应当只被分配到bond0接口。

如果你有一个有线连接和无线连接连接到同一个网络，现在可以将有线网络断开连接，然后重新连接而依然保持网络通畅。在大多数情况下，甚至连流媒体音乐都不会卡顿。

### 使用任意接口

In some cases it may be desirable to allow a profile to use any interface on the system. A common example use case is using a common disk image across many machines with differing hardware (this is especially useful if they are headless). If you use the kernel's naming scheme, and your machine has only one ethernet interface, you can probably guess that eth0 is the right interface. If you use udev's [Predictable Network Interface Names](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames/), however, names will be assigned based on the specific hardware itself (e.g. enp1s0), rather than simply the order that the hardware was detected (e.g. eth0, eth1). This means that a netctl profile may work on one machine and not another, because they each have different interface names.

A quick and dirty solution is to make use of the `/etc/netctl/interfaces/` directory. Choose a name for your interface alias (`en-any` in this example), and write the following to a file with that name (making sure it is executable).

 `/etc/netctl/interfaces/en-any` 
```
#!/bin/bash
for interface in /sys/class/net/en*; do
        break;
done
Interface=$(basename $interface)
echo "en-any: using interface $Interface";

```

Then create a profile that uses the interface. Pay special attention to the `Interface` directive. The rest are only provided as examples.

 `/etc/netctl/wired` 
```
Description='Wired'
Interface=en-any
Connection=ethernet
IP=static
Address=('192.168.1.15/24')
Gateway='192.168.1.1'
DNS=('192.168.1.1')

```

When the `wired` profile is started, any machine using the two files above will automatically bring up and configure the first ethernet interface found on the system, regardless of what name udev assigned to it. Note that this is not the most robust way to go about configuring interfaces. If you use multiple interfaces, netctl may try to assign the same interface to them, and will likely cause a disruption in connectivity. If you do not mind a more complicated solution, `netctl-auto` is likely to be more reliable.

### 使用钩子

netctl supports hooks in `/etc/netctl/hooks/` and per interface hooks in `/etc/netctl/interfaces/`. You can set any option in a hook/interface that you can in a profile. They are read the same way! Most importantly this includes `ExecUpPost` and `ExecDownPre`.

When a profile is read, netctl sources *all executable* scripts in `hooks`, then it reads the profile file for the connection and finally it sources an executable script with the name of the interface used in the profile from the `interfaces` directory. Therefore, declarations in an interface script override declarations in the profile, which override declarations in hooks.

The variables `$INTERFACE`, `$SSID`, `$ACTION` and `$Profile` are available in hooks/interfaces **only** when using `netctl-auto`

#### 范例

##### 在已有连接上执行命令

 `/etc/netctl/hooks/myservices` 
```
#!/bin/sh
ExecUpPost="systemctl start crashplan.service; systemctl start dropbox@<username>.service"
ExecDownPre="systemctl stop crashplan.service; systemctl stop dropbox@<username>.service"

```

##### 激活 network-online.target

 `/etc/netctl/hooks/status` 
```
#!/bin/sh
ExecUpPost="systemctl start network-online.target"
ExecDownPre="systemctl stop network-online.target"

```

Using this, systemd services requiring an active network connection can be [ordered](/index.php/Systemd#Handling_dependencies "Systemd") to start only after the `network-online.target` is reached, and can be stopped before the connection is brought down.

##### 设置默认 DHCP 客户端

To set or change the DHCP client used for all profiles:

 `/etc/netctl/hooks/dhcp` 
```
#!/bin/sh
DHCPClient='dhclient'

```

Alternatively, it may also be specified for a specific network interface by creating an executable file `/etc/netctl/interfaces/<interface>` with the following line:

```
DHCPClient='dhclient'

```

## 排错

### Job for netctl@wlan(...).service failed

Some people have an issue when they connect to a network with *netctl*, for example:

 `# netctl start wlan0-ssid` 
```
Job for netctl@wlan0\x2ssid.service failed. See 'systemctl status netctl@wlan0\x2ssid.service' and 'journalctl -xn' for details.

```

When then looking at `journalctl -xn`, either of the following are shown:

1\. If your device (`wlan0` in this case) is up:

```
network[2322]: The interface of network profile 'wlan0-ssid' is already up

```

Setting the interface down should resolve the problem:

```
# ip link set wlan0 down

```

Then retry:

```
# netctl start wlan0-ssid

```

2\. If it is down:

```
dhcpcd[261]: wlan0: ipv4_sendrawpacket: Network is down

```

One way to solve this is to use a different DHCP client, for example [dhclient](https://www.archlinux.org/packages/?name=dhclient). After installing the package configure *netctl* to use it:

 `/etc/netctl/wlan0-ssid` 
```
...
DHCPClient='dhclient'

```

Adding the `ForceConnect` option may also be helpful:

 `/etc/netctl/wlan0-ssid` 
```

...

ForceConnect=yes

```

Save it and try to connect with the profile:

```
# netctl start wlan0-ssid

```

### dhcpcd: ipv4_addroute: File exists

On some systems dhcpcd in combination with netctl causes timeout issues on resume, particularly when having switched networks in the meantime. netctl will report that you are successfully connected but you still receive timeout issues. In this case, the old default route still exists and is not being renewed. A workaround to avoid this misbehaviour is to switch to [dhclient](#Set_default_DHCP_client) as the default dhcp client. More information on the issue can be found [here](https://bbs.archlinux.org/viewtopic.php?pid=1399842#p1399842).

### DHCP timeout issues

If you are having timeout issues when requesting leases via DHCP you can set the timeout value higher than netctl's 30 seconds by default. Create a file in `/etc/netctl/hooks/` or `/etc/netctl/interfaces/`, add `TimeoutDHCP=40` to it for a timeout of 40 seconds and make the file executable.

### Connection timeout issues

If you are having timeout issues that are unrelated to DHCP (on a static ethernet connection for example), and are experiencing errors similar to the following when starting your profile:

 `# journalctl _SYSTEMD_UNIT=netctl@*profile*.service` 
```
Starting network profile '*profile*'...
No connection found on interface 'eth0' (timeout)
Failed to bring the network up for profile '*profile*'

```

Then you should increase carrier and up timeouts by adding `TimeoutUp=` and `TimeoutCarrier=` to your profile file:

 `/etc/netctl/*profile*` 
```
...
TimeoutUp=300
TimeoutCarrier=300

```

Do not forget to reenable your profile:

```
# netctl reenable *profile*

```

### Problems with netctl-auto on resume

Sometimes *netctl-auto* fails to reconnect when the system resumes from suspend. An easy solution is to restart the service for *netctl-auto*. This can be automated with an additional service like the following:

 `/etc/systemd/system/netctl-auto-resume@.service` 
```
[Unit]
Description=restart netctl-auto on resume.
Requisite=netctl-auto@%i.service
After=suspend.target

[Service]
Type=oneshot
ExecStart=/usr/bin/systemctl restart netctl-auto@%i.service

[Install]
WantedBy=suspend.target

```

To [enable](/index.php/Enable "Enable") this service for your wireless card, for example, enable `netctl-auto-resume@wlan0.service` as root. Change `wlan0` to the required network interface.

If the device is not yet running on resume when the unit is started, this will fail. It can be fixed by adding the following dependency in the *After* line:

 `/etc/systemd/system/netctl-auto-resume@.service` 
```
...
After=suspend.target sys-subsystem-net-devices-%i.device
...

```

### netctl-auto suddenly stopped working for WiFi adapters

This problem seems to be related to a recent wpa_supplicant update (see [FS#44731](https://bugs.archlinux.org/task/44731)), but a work-around is quite trivial. Just create a file for your interface (e.g. wlp3s0) in /etc/netctl/interfaces with the following content and make it executable:

 `/etc/netctl/interfaces/wlp3s0` 
```
WPAOptions="-m ''"

```

After that, try to restart your netctl-auto service and WiFi auto detection should work well again.

### netctl-auto does not automatically unblock a wireless card to use an interface

Many laptops have a hardware button (or switch) to turn off wireless card, however, the card can also be blocked by the kernel. This can be handled by [rfkill](/index.php/Rfkill "Rfkill").

If you want *netctl-auto* to automatically unblock your wireless card to connect to a particular network, set `RFKill=++auto++` option for the wireless connection of your choice, as specified in the [netctl.profile(5)](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.profile.5.txt) man page.

### RTNETLINK answers: File exists (with multiple NICs)

This is a very misleading response, it really means that you have assigned a default gateway in an earlier netctl control file. When netctl starts up the n-th NIC and goes to set its local route, it fails because there is already a default route from n-1.

Remove it and everything works, except you no longer have a default route and so cannot access things such as the internet. `ExecUpPost` does not work as it gets executed for each network card.

A possible solution is creating a new service:

 `/etc/systemd/system/defaultrouter.service` 
```
[Unit]
Description
Requires=netctl.service
After=netctl.service
Before=ntpd.service,dnsmasq.service

[Service]
Type=oneshot
ExecStart=/usr/bin/ip route add default via 192.168.xxx.yyy
```

## 参见

*   [Initial mailing list announcement](https://lists.archlinux.org/pipermail/arch-projects/2012-December/003473.html)
*   [官方陈述页面](https://bbs.archlinux.org/viewtopic.php?id=157670)
*   在AUR中有一个可用的cinnamon applet: [cinnamon-applet-netctl-systray-menu](https://aur.archlinux.org/packages/cinnamon-applet-netctl-systray-menu/)