**翻译状态：** 本文是英文页面 [WPA_Supplicant](/index.php/WPA_Supplicant "WPA Supplicant") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-04-21，点击[这里](https://wiki.archlinux.org/index.php?title=WPA_Supplicant&diff=0&oldid=307229)可以查看翻译后英文页面的改动。

[wpa_supplicant](http://hostap.epitest.fi/wpa_supplicant/) 是跨平台的 WPA [supplicant](https://en.wikipedia.org/wiki/Supplicant_(computer) "wikipedia:Supplicant (computer)")，支持 WEP, WPA 和 WPA2 ([IEEE 802.11i](https://en.wikipedia.org/wiki/IEEE_802.11i "wikipedia:IEEE 802.11i") / RSN (Robust Secure Network)). 可以在桌面、笔记本甚至嵌入式系统中使用。

*wpa_supplicant* 是在客户端使用的 IEEE 802.1X/WPA 组件， 支持与 WPA Authenticator 的交互，控制漫游和无线驱动的 IEEE 802.11 验证和关联。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 启动](#.E5.90.AF.E5.8A.A8)
    *   [2.1 systemd](#systemd)
    *   [2.2 dhcpcd](#dhcpcd)
    *   [2.3 Manually](#Manually)
*   [3 Configuration](#Configuration)
    *   [3.1 wpa_passphrase](#wpa_passphrase)
    *   [3.2 Specifying driver](#Specifying_driver)
*   [4 Using wpa_cli](#Using_wpa_cli)
    *   [4.1 Adding a new network using wpa_cli](#Adding_a_new_network_using_wpa_cli)
    *   [4.2 Action script](#Action_script)
*   [5 See also](#See_also)

## 安装

从 [官方软件仓库](/index.php/Official_repositories "Official repositories") 中安装软件包 [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant)。

此外软件包 [wpa_supplicant_gui](https://www.archlinux.org/packages/?name=wpa_supplicant_gui) 提供了图形界面 *wpa_gui*。

## 启动

This section describes common methods of starting *wpa_supplicant*, pick one that suits you best.

### systemd

*wpa_supplicant* provides multiple service files:

*   `wpa_supplicant.service` - uses [D-Bus](/index.php/D-Bus "D-Bus"), recommended for [NetworkManager](/index.php/NetworkManager "NetworkManager") users.
*   `wpa_supplicant@.service` - accepts the interface name as an argument and starts the *wpa_supplicant* daemon for this interface. It reads the configuration file in `/etc/wpa_supplicant/wpa_supplicant-*interface*.conf`.
*   `wpa_supplicant-nl80211@.service` - also interface specific, but explicitly forces the `nl80211` driver (see below). The configuration file path is `/etc/wpa_supplicant/wpa_supplicant-nl80211-*interface*.conf`.
*   `wpa_supplicant-wired@.service` - also interface specific, uses the `wired` driver. The configuration file path is `/etc/wpa_supplicant/wpa_supplicant-wired-*interface*.conf`.

### dhcpcd

[dhcpcd](/index.php/Dhcpcd "Dhcpcd") contains a hook (enabled by default) to automatically launch *wpa_supplicant* on wireless interfaces. It is started only if:

*   no *wpa_supplicant* process is already listening on that interface.
*   a *wpa_supplicant* configuration file exists. *dhcpcd* checks `/etc/wpa_supplicant.conf` and `/etc/wpa_supplicant/wpa_supplicant.conf` by default, but a custom path can be set by adding `env wpa_supplicant_conf=*configuration_file_path*` into `/etc/dhcpcd.conf`.

### Manually

*wpa_supplicant* accepts multiple command line arguments, notably:

*   `-B` - fork into background
*   `-c *filename*` - path to configuration file
*   `-i *interface*` - interface to listen on

See `man 8 wpa_supplicant` for the full argument list. For example, the common usage is:

```
# wpa_supplicant -B -i *interface* -c *configuration_file*

```

## Configuration

[wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) provides a reference configuration file located at `/etc/wpa_supplicant/wpa_supplicant.conf` which contains detailed documentation for all the available options and their utilisation, as well as examples. Consider making a backup of it first, because some of the methods decribed below for automatically adding network configurations to `wpa_supplicant.conf` will strip all comments from the file.

In its simplest form, a configuration file requires only a network configuration block. For example:

 `/etc/wpa_supplicant/foobar.conf` 
```
network={
    ssid="..."
}
```

Once you have a configuration file, you can [start](#Starting) the *wpa_supplicant* daemon as described in the previous section and connect to the wireless network, using a [static IP](/index.php/Network_configuration#Static_IP_address "Network configuration") or [DHCP](/index.php/Network_configuration#Dynamic_IP_address "Network configuration").

### wpa_passphrase

A network configuration can be automatically generated using the *wpa_passphrase* tool and added to the configuration file. This is useful for connecting to secured networks requiring a passphrase. For example:

 `$ wpa_passphrase *essid* *passphrase*` 
```
network={
    ssid="*essid*"
    #psk="*passphrase*"
    psk=f5d1c49e15e679bebe385c37648d4141bc5c9297796a8a185d7bc5ac62f954e3
}
```

Some unusually complex passphrases may require input from a file:

```
$ wpa_passphrase *essid* < *passphrase.txt*

```

**Tip:** Both *wpa_supplicant* and *wpa_passphrase* can be combined to associate with almost all WPA2 (Personal) networks:
```
# wpa_supplicant -B -i *interface* -c <(wpa_passphrase *essid* *passphrase*)

```

### Specifying driver

You might need to specify a driver to be used. For a list of supported drivers see the output of `wpa_supplicant -h`.

*   `nl80211` is the current standard, but not all wireless chip's modules support it.
*   `wext` is currently deprecated, but still widely supported.

Use the `-D` switch to specify the driver:

```
# wpa_supplicant -B -i *interface* -c *configuration_file* -D *driver*

```

## Using wpa_cli

*Wpa_supplicant* can be controlled manually at runtime, by using the *wpa_cli* utility. To enable *wpa_cli*, the *wpa_supplicant* daemon must be configured to create a "control interface" (socket) by setting the *ctrl_interface* variable in the *wpa_supplicant* configuration file (default location `/etc/wpa_supplicant/wpa_supplicant.conf`).

The user will also need to be given access to this socket, by specifying which [group](/index.php/Users_and_groups "Users and groups") has access to it. A new group might be created for this purpose, and users added to it, or an already existing group can be used - typically `wheel`.

The following setting will create the socket in `/run/wpa_supplicant/` and allow the members of group `wheel` to access it:

```
ctrl_interface=DIR=/run/wpa_supplicant GROUP=wheel

```

It is possible to modify the *wpa_supplicant* configuration file itself through the *wpa_cli*. This is useful for manually adding new networks to the roaming configuration file without needing to restart the *wpa_supplicant* daemon. To enable this, in the configuration file set the *update_config* variable to 1:

```
update_config=1

```

The *wpa_supplicant* daemon must be running, before *wpa_cli* can start (see [#Starting](#Starting) for details). Then start

```
$ wpa_cli

```

It will look for the control socket at the location given in the configuration file, or the location can be set manually with the `-p` option). You can specify the interface that will be configured with the `-i` option, otherwise the first found wireless interface managed by *wpa_supplicant* will be used.

When *wpa_cli* is invoked, an interactive prompt (`>`) will appear. The prompt has tab completion and descriptions of completed commands.

### Adding a new network using wpa_cli

To scan for available networks, enter "scan" at the `>` prompt. A notification will appear when the scan is complete:

```
> scan
OK
<3>CTRL-EVENT-SCAN-RESULTS
>

```

Then enter "scan_results" to display them:

```
> scan_results
bssid / frequency / signal level / flags / ssid
00:00:00:00:00:00 2462 -49 [WPA2-PSK-CCMP][ESS] MYSSID
11:11:11:11:11:11 2437 -64 [WPA2-PSK-CCMP][ESS] ANOTHERSSID
>

```

To associate with *MYSSID*, tell *wpa_supplicant* about it. Each network in the configuration file is indexed numerically, beginning with zero. If you add a new network, it will be assigned a new number accordingly.

```
> add_network
0
>

```

Use this number to specify which network your settings apply to. For a new network, set its SSID, in quotes:

```
> set_network 0 ssid "*MYSSID*"
OK
>

```

Even if your access point is not is protected, the cli apparently still requires a [PSK](https://en.wikipedia.org/wiki/Pre-shared_key "wikipedia:Pre-shared key"), again in quotes. The passkey must be 8-63 characters.:

```
> set_network 0 psk "*passkey*"
OK
>

```

Enable it:

```
> enable_network 0
OK
>

```

And write the changes to the configuration file:

```
> save_config
OK
>

```

### Action script

*wpa_cli* can run in daemon mode and execute a specified script based on events from *wpa_supplicant*. Two events are supported: `CONNECTED` and `DISCONNECTED`. Some [environment variables](/index.php/Environment_variables "Environment variables") are available to the script, see `man 8 wpa_cli` for details.

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

Remember to make the script executable, then use the `-a` to pass the script path to *wpa_cli*:

```
$ wpa_cli -a *path_to_script*

```

## See also

*   [Kernel.org wpa_supplicant documentation](http://wireless.kernel.org/en/users/Documentation/wpa_supplicant)