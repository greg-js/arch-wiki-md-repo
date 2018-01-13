Related articles

*   [网络配置](/index.php/%E7%BD%91%E7%BB%9C%E9%85%8D%E7%BD%AE "网络配置")
*   [无线网络配置](/index.php/%E6%97%A0%E7%BA%BF%E7%BD%91%E7%BB%9C%E9%85%8D%E7%BD%AE "无线网络配置")
*   [WPA2 Enterprise](/index.php/WPA2_Enterprise "WPA2 Enterprise")

**翻译状态：** 本文是英文页面 [WPA_Supplicant](/index.php/WPA_Supplicant "WPA Supplicant") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-10-01，点击[这里](https://wiki.archlinux.org/index.php?title=WPA_Supplicant&diff=0&oldid=450471)可以查看翻译后英文页面的改动。

[wpa_supplicant](http://hostap.epitest.fi/wpa_supplicant/) 是跨平台的 WPA [请求者程序（supplicant）](https://en.wikipedia.org/wiki/Supplicant_(computer) "wikipedia:Supplicant (computer)")，支持 WEP、WPA 和 WPA2（[IEEE 802.11i](https://en.wikipedia.org/wiki/IEEE_802.11i "wikipedia:IEEE 802.11i") / RSN （健壮安全网络-Robust Secure Network））。可以在桌面、笔记本甚至嵌入式系统中使用。

*wpa_supplicant* 是在客户端使用的 IEEE 802.1X/WPA 组件，支持与 WPA Authenticator 的交互，控制漫游和无线驱动的 IEEE 802.11 验证和关联。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 概览](#.E6.A6.82.E8.A7.88)
*   [3 用 wpa_cli 连接](#.E7.94.A8_wpa_cli_.E8.BF.9E.E6.8E.A5)
*   [4 带 wpa 通行字的连接](#.E5.B8.A6_wpa_.E9.80.9A.E8.A1.8C.E5.AD.97.E7.9A.84.E8.BF.9E.E6.8E.A5)
*   [5 高级用法](#.E9.AB.98.E7.BA.A7.E7.94.A8.E6.B3.95)
    *   [5.1 配置](#.E9.85.8D.E7.BD.AE)
    *   [5.2 连接](#.E8.BF.9E.E6.8E.A5)
        *   [5.2.1 手动连接](#.E6.89.8B.E5.8A.A8.E8.BF.9E.E6.8E.A5)
        *   [5.2.2 引导时连接（systemd）](#.E5.BC.95.E5.AF.BC.E6.97.B6.E8.BF.9E.E6.8E.A5.EF.BC.88systemd.EF.BC.89)
    *   [5.3 wpa_cli 操作脚本](#wpa_cli_.E6.93.8D.E4.BD.9C.E8.84.9A.E6.9C.AC)
*   [6 排错](#.E6.8E.92.E9.94.99)
    *   [6.1 某些硬件上 nl80211 驱动不支持](#.E6.9F.90.E4.BA.9B.E7.A1.AC.E4.BB.B6.E4.B8.8A_nl80211_.E9.A9.B1.E5.8A.A8.E4.B8.8D.E6.94.AF.E6.8C.81)
    *   [6.2 挂载了网络共享（CIFS）时的关机问题](#.E6.8C.82.E8.BD.BD.E4.BA.86.E7.BD.91.E7.BB.9C.E5.85.B1.E4.BA.AB.EF.BC.88CIFS.EF.BC.89.E6.97.B6.E7.9A.84.E5.85.B3.E6.9C.BA.E9.97.AE.E9.A2.98)
    *   [6.3 口令相关的问题](#.E5.8F.A3.E4.BB.A4.E7.9B.B8.E5.85.B3.E7.9A.84.E9.97.AE.E9.A2.98)
*   [7 参阅](#.E5.8F.82.E9.98.85)

## 安装

[安装](/index.php/Install "Install") [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) 软件包。

此外软件包 [wpa_supplicant_gui](https://aur.archlinux.org/packages/wpa_supplicant_gui/) 提供了图形界面 *wpa_gui*。

## 概览

连接到加密无线网络的第一步是让 *wpa_supplicant* 获取 WPA 认证者的认证。为此， *wpa_supplicant* 必须进行配置以使其能够向认证者提交认证信息。

一旦完成认证，就可以正常连接网络，并通过 [iproute2](/index.php/Core_utilities_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#ip "Core utilities (简体中文)") 手工获取 IP 地址；或者使用 [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") 或 [dhcpcd](/index.php/Dhcpcd "Dhcpcd")之类的网络管理程序，通过配置一个*接口*然后通过 DHCP 自动获取 IP 地址。参阅[无线网络管理](/index.php/%E6%97%A0%E7%BA%BF%E7%BD%91%E7%BB%9C%E9%85%8D%E7%BD%AE#.E6.97.A0.E7.BA.BF.E7.BD.91.E7.BB.9C.E7.AE.A1.E7.90.86 "无线网络配置")和[配置 IP 地址](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E9.85.8D.E7.BD.AE_IP_.E5.9C.B0.E5.9D.80 "Network configuration (简体中文)")等文章中的方法和范例。

## 用 wpa_cli 连接

This connection method allows scanning for the available networks, making use of *wpa_cli*, a command line tool which can be used to interactively configure *wpa_supplicant* at runtime. See [wpa_cli(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_cli.8) for details.

In order to use *wpa_cli*, a control interface must be specified for *wpa_supplicant*, and it must be given the rights to update the configuration. Do this by creating a minimal configuration file:

 `/etc/wpa_supplicant/example.conf` 
```
ctrl_interface=/run/wpa_supplicant
update_config=1
```

Now start *wpa_supplicant* with:

```
# wpa_supplicant -B -i *interface* -c /etc/wpa_supplicant/example.conf

```

**提示：** To discover your wireless network interface name, issue the `ip link` command.

At this point run:

```
# wpa_cli

```

This will present an interactive prompt (`>`), which has tab completion and descriptions of completed commands.

**提示：** The default location of the control socket is `/var/run/wpa_supplicant/`, custom path can be set manually with the `-p` option to match the *wpa_supplicant* configuration. It is also possible to specify the interface to be configured with the `-i` option, otherwise the first found wireless interface managed by *wpa_supplicant* will be used.

Use the `scan` and `scan_results` commands to see the available networks:

```
> scan
OK
<3>CTRL-EVENT-SCAN-RESULTS
> scan_results
bssid / frequency / signal level / flags / ssid
00:00:00:00:00:00 2462 -49 [WPA2-PSK-CCMP][ESS] MYSSID
11:11:11:11:11:11 2437 -64 [WPA2-PSK-CCMP][ESS] ANOTHERSSID

```

To associate with `MYSSID`, add the network, set the credentials and enable it:

```
> add_network
0
> set_network 0 ssid "MYSSID"
> set_network 0 psk "passphrase"
> enable_network 0
<2>CTRL-EVENT-CONNECTED - Connection to 00:00:00:00:00:00 completed (reauth) [id=0 id_str=]

```

If the SSID does not have password authentication, you must explicitly configure the network as keyless by replacing the command `set_network 0 psk "passphrase"` with `set_network 0 key_mgmt NONE`.

**注意:**

*   Each network is indexed numerically, so the first network will have index 0.
*   The [PSK](https://en.wikipedia.org/wiki/Pre-shared_key "wikipedia:Pre-shared key") is computed from the *quoted* "passphrase" string, as also shown by the [wpa_passphrase](#Connecting_with_wpa_passphrase) command. Nonetheless, you can enter the PSK directly by passing it to `psk` *without* quotes.

Finally save this network in the configuration file:

```
> save_config
OK

```

Once association is complete, all that is left to do is obtain an IP address as indicated in the [#Overview](#Overview), for example:

```
# dhcpcd *interface*

```

## 带 wpa 通行字的连接

用命令行工具 *wpa_passphrase* 生成 *wpa_supplicant* 所需的最小配置，可以快速连接到已知 SSID 的无线网络。例如：

 `$ wpa_passphrase MYSSID passphrase` 
```
network={
    ssid="MYSSID"
    #psk="passphrase"
    psk=59e0d07fa4c7741797a4e394f38a5c321e3bed51d54ad5fcbd3f84bc7415d73d
}
```

上例表明，*wpa_supplicant* 可以与 *wpa_passphrase* 协同工作，只需简单地这样即可做：

```
# wpa_supplicant -B -i *interface* -c <(wpa_passphrase MYSSID passphrase)

```

**注意:** 由于存在进程替换，这个命令**不能**以 [sudo](/index.php/Sudo "Sudo") 方式执行，必须切换到 root 身份。否则会报错：
```
Successfully initialized wpa_supplicant
Failed to open config file '/dev/fd/63', error: No such file or directory
Failed to read or parse configuration '/dev/fd/63'

```
参阅：[Help:Reading (简体中文)#一般用户还是 root 用户](/index.php/Help:Reading_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.B8.80.E8.88.AC.E7.94.A8.E6.88.B7.E8.BF.98.E6.98.AF_root_.E7.94.A8.E6.88.B7 "Help:Reading (简体中文)")。

**提示：**

*   如果输入内容包含空格请使用引号。例如：`"secret passphrase"`。
*   要找出无线网卡的名字，使用 `ip link` 命令。
*   某些不常用的复杂通行字要求从文件输入，例如：`wpa_passphrase MYSSID < passphrase.txt`；或者从命令行输入，例如：`wpa_passphrase MYSSID <<< "passphrase"`。

之后就可以像[#概览](#.E6.A6.82.E8.A7.88)中所述获取 IP 地址：

```
# dhcpcd *interface*

```

## 高级用法

对于各种纷繁复杂的网络，更常见的场景是使用 [EAP](https://zh.wikipedia.org/wiki/%E6%89%A9%E5%B1%95%E8%AE%A4%E8%AF%81%E5%8D%8F%E8%AE%AE) 管理配置文件。各种配置及其范例可参阅手册页[wpa_supplicant.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.conf.5)；所有可支持的配置参数可参考范例文件 `/etc/wpa_supplicant/wpa_supplicant.conf`。

### 配置

如上文中[#带 wpa 通行字的连接](#.E5.B8.A6_wpa_.E9.80.9A.E8.A1.8C.E5.AD.97.E7.9A.84.E8.BF.9E.E6.8E.A5)一节所述，一个基本的配置文件可以这样生成：

```
# wpa_passphrase MYSSID passphrase > /etc/wpa_supplicant/example.conf

```

这样仅仅是创建了一个网络配置节段。包含更多通用配置项的配置文件类似下面这样：

 `/etc/wpa_supplicant/example.conf` 
```
ctrl_interface=/var/run/wpa_supplicant
ctrl_interface_group=wheel
update_config=1
fast_reauth=1
ap_scan=1

network={
    ssid="MYSSID"
    psk=59e0d07fa4c7741797a4e394f38a5c321e3bed51d54ad5fcbd3f84bc7415d73d
}
```

如果可以不顾及安全问题，其中的通行字可以换成由引号包围的纯文本：

```
network={
    ssid="MYSSID"
    psk="passphrase"
}
```

如果某一网络没有设置通行字，比如一个公共无线网络，就是这样：

```
network={
    ssid="MYSSID"
    key_mgmt=NONE
}
```

Further `network` blocks may be added manually, or using *wpa_cli* as illustrated in [#Connecting with wpa_cli](#Connecting_with_wpa_cli). In order to use *wpa_cli*, a control interface must be set with the `ctrl_interface` option. Setting `ctrl_interface_group=wheel` allows users belonging to such group to execute *wpa_cli*. This setting can be used to enable users without root access (or equivalent via sudo etc) to connect to wireless networks. Also add `update_config=1` so that changes made with *wpa_cli* to `example.conf` can be saved. Note that any user that is a member of the `ctrl_interface_group` group will be able to make changes to the file if this is turned on.

`fast_reauth=1` and `ap_scan=1` are the *wpa_supplicant* options active globally at the time of writing. Whether you need them, or other global options too for that matter, depends on the type of network to connect to. If you need other global options, simply copy them over to the file from `/etc/wpa_supplicant/wpa_supplicant.conf`.

Alternatively, `wpa_cli set` can be used to see options' status or set new ones. Multiple network blocks may be appended to this configuration: the supplicant will handle association to and roaming between all of them. The strongest signal defined with a network block usually is connected to by default, one may define `priority=` to influence behaviour.

An advantage to be mentioned in using a customized configuration file at `/etc/wpa_supplicant/wpa_supplicant.conf` is that it is used by default by [dhcpcd](/index.php/Dhcpcd "Dhcpcd"). If you do so, you might want to make a backup of the original and delete the extensive network block examples in it. Otherwise, do not be surprised if your device suddenly connects to networks defined in them. In any case, changes to new versions of the configuration file should of course be [merged](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files").

**提示：** To configure a network block to a hidden wireless *SSID*, which by definition will not turn up in a regular scan, the option `scan_ssid=1` has to be defined in the network block.

### 连接

#### 手动连接

First start *wpa_supplicant* command, whose most commonly used arguments are:

*   `-B` - Fork into background.
*   `-c *filename*` - Path to configuration file.
*   `-i *interface*` - Interface to listen on.
*   `-D *driver*` - Optionally specify the driver to be used. For a list of supported drivers see the output of `wpa_supplicant -h`.
    *   `nl80211` is the current standard, but not all wireless chip's modules support it.
    *   `wext` is currently deprecated, but still widely supported.

See [wpa_supplicant(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.8) for the full argument list. For example:

```
# wpa_supplicant -B -i *interface* -c /etc/wpa_supplicant/example.conf

```

followed by a method to obtain an ip address manually as indicated in the [#Overview](#Overview), for example:

```
# dhcpcd *interface*

```

**提示：** *dhcpcd* has a hook that can lauch *wpa_supplicant* implicitly, see [dhcpcd#10-wpa_supplicant](/index.php/Dhcpcd#10-wpa_supplicant "Dhcpcd").

#### 引导时连接（systemd）

*wpa_supplicant* 软件包中提供了多个 [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 服务文件：

*   `wpa_supplicant.service` - 使用 [D-Bus](/index.php/D-Bus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "D-Bus (简体中文)") ，建议 [NetworkManager](/index.php/NetworkManager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NetworkManager (简体中文)") 用户使用。
*   `wpa_supplicant@.service` - 接受网口名作为参数，启动服务于该网口的 *wpa_supplicant* 守护进程。这个服务将读取 `/etc/wpa_supplicant/wpa_supplicant-*interface*.conf` 这个配置文件。
*   `wpa_supplicant-nl80211@.service` - 同样接受网口名作为参数，但明确限定使用 `nl80211` 驱动（详阅下文）。它的配置文件是 `/etc/wpa_supplicant/wpa_supplicant-nl80211-*interface*.conf`。
*   `wpa_supplicant-wired@.service` - 同样接受网口名作为参数，使用 `wired`（有线网络）驱动。它的配置文件是 `/etc/wpa_supplicant/wpa_supplicant-wired-*interface*.conf`。

在引导时激活无线网络，就是激活服务于某个无线网络接口的上述服务单元之一。

现在就可以像[概览](#.E6.A6.82.E8.A7.88)一节所述，可以选定某个网络接口并[激活](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)")其服务单元的一个实例，从而获取一个 IP 地址。

**提示：** *dhcpcd* 可以后台加载 *wpa_supplicant* ，参阅 [dhcpcd (简体中文)#10-wpa_supplicant](/index.php/Dhcpcd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#10-wpa_supplicant "Dhcpcd (简体中文)").

### wpa_cli 操作脚本

*wpa_cli* can run in daemon mode and execute a specified script based on events from *wpa_supplicant*. Two events are supported: `CONNECTED` and `DISCONNECTED`. Some [environment variables](/index.php/Environment_variables "Environment variables") are available to the script, see [wpa_cli(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_cli.8) for details.

The following example will use [desktop notifications](/index.php/Desktop_notifications "Desktop notifications") to notify the user about the events:

```
#!/bin/bash

case "$2" in
    CONNECTED)
        notify-send "WPA supplicant: connection established";
        ;;
    DISCONNECTED)
        notify-send "WPA supplicant: connection lost";
        ;;
esac

```

Remember to make the script executable, then use the `-a` flag to pass the script path to *wpa_cli*:

```
$ wpa_cli -a */path/to/script*

```

## 排错

**警告:** Make sure that you are **not** using the default configuration file at `/etc/wpa_supplicant/wpa_supplicant.conf`, which is filled with uncommented examples that will lead to lots of random errors in practice. This is a known packaging bug of the [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) package: [FS#40661](https://bugs.archlinux.org/task/40661).

### 某些硬件上 nl80211 驱动不支持

On some (especially old) hardware, *wpa_supplicant* may fail with the following error:

```
Successfully initialized wpa_supplicant
nl80211: Driver does not support authentication/association or connect commands
wlan0: Failed to initialize driver interface

```

This indicates that the standard `nl80211` driver does not support the given hardware. The deprecated `wext` driver might still support the device:

```
# wpa_supplicant -B -i wlan0 **-D wext** -c /etc/wpa_supplicant/example.conf

```

If the command works to connect, and the user wishes to use [systemd](/index.php/Systemd "Systemd") to manage the wireless connection, it is necessary to [edit](/index.php/Systemd#Drop-in_files "Systemd") the `wpa_supplicant@.service` unit provided by the package and modify the `ExecStart` line accordingly:

 `/etc/systemd/system/wpa_supplicant@.service.d/wext.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/wpa_supplicant -c/etc/wpa_supplicant/wpa_supplicant-%I.conf -i%I **-Dnl80211,wext**
```

**注意:** Multiple comma separated driver wrappers in option `-Dnl80211,wext` makes *wpa_supplicant* use the first driver wrapper that is able to initialize the interface (see [wpa_supplicant(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.8)). This is useful when using mutiple or removable (e.g. USB) wireless devices which use different drivers.

### 挂载了网络共享（CIFS）时的关机问题

When you use wireless to connect to network shares you might have the problem that the shutdown takes a very long time. That is because systemd runs against a 3 minute timeout. The reason is that WPA supplicant is shut down too early, i.e. before systemd tries to unmount the share(s). A [bug report](https://github.com/systemd/systemd/issues/1435) suggests a work-around by [editing](/index.php/Systemd#Drop-in_files "Systemd") the `wpa_supplicant@.service` as follows:

 `/etc/systemd/system/wpa_supplicant.service.d/override.conf` 
```
[Unit]
After=dbus.service
```

### 口令相关的问题

[wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) may not work properly if directly passed via stdin particularly long or complex passphrases which include special characters. This may lead to errors such as `failed 4-way WPA handshake, PSK may be wrong` when launching [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant).

In order to solve this try using here strings `wpa_passphrase <MYSSID> <<< "<passphrase>"` or passing a file to the `-c` flag instead:

```
$ wpa_supplicant -i <interface> -c /etc/wpa_supplicant/wpa_supplicant.conf

```

In some instances it was found that storing the passphrase cleartext in the `psk` key of the `wpa_supplicant.conf` `network` block gave positive results (see [[1]](http://www.linuxquestions.org/questions/linux-wireless-networking-41/wpa-4-way-handshake-failed-843394/)). However, this approach is rather insecure. Using `wpa_cli` to create this file instead of manually writing it gives the best results most of the time and therefore is the recommended way to proceed.

## 参阅

*   [WPA Supplicant 主页](http://hostap.epitest.fi/wpa_supplicant/)
*   [wpa_cli 用例](https://gist.github.com/buhman/7162560)
*   [wpa_supplicant(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.8)
*   [wpa_supplicant.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.conf.5)
*   [wpa_cli(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_cli.8)
*   [Kernel.org wpa_supplicant 文档](http://wireless.kernel.org/en/users/Documentation/wpa_supplicant)