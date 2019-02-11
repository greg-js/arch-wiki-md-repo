[蓝牙（Bluetooth）](https://en.wikipedia.org/wiki/Bluetooth "wikipedia:Bluetooth")是一个短距离无线通信标准，适用于手机，计算机和其他电子设备之间的通信。在 Linux 中，通常使用的蓝牙协议栈实现是 [BlueZ](http://www.bluez.org/)。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
    *   [1.1 前端](#前端)
        *   [1.1.1 控制台](#控制台)
        *   [1.1.2 图形界面](#图形界面)
*   [2 配对](#配对)
*   [3 配置](#配置)
    *   [3.1 开机后自动启动](#开机后自动启动)
*   [4 音频](#音频)
*   [5 疑难解答](#疑难解答)
    *   [5.1 已弃用的Bluez工具](#已弃用的Bluez工具)
    *   [5.2 gnome-bluetooth](#gnome-bluetooth)
    *   [5.3 蓝牙USB电子狗](#蓝牙USB电子狗)
        *   [5.3.1 Audio devices start to skip at short distance from dongle](#Audio_devices_start_to_skip_at_short_distance_from_dongle)
    *   [5.4 Logitech Bluetooth USB Dongle](#Logitech_Bluetooth_USB_Dongle)
    *   [5.5 hcitool scan: Device not found](#hcitool_scan:_Device_not_found)
    *   [5.6 rfkill unblock：不能unblock](#rfkill_unblock：不能unblock)
    *   [5.7 电脑蓝牙不可见](#电脑蓝牙不可见)
    *   [5.8 罗技键盘配对不了](#罗技键盘配对不了)
    *   [5.9 HSP/HFP profiles](#HSP/HFP_profiles)
    *   [5.10 Foxconn / Hon Hai / Lite-On Broadcom device](#Foxconn_/_Hon_Hai_/_Lite-On_Broadcom_device)
    *   [5.11 设备配对后过一会儿又断开](#设备配对后过一会儿又断开)
    *   [5.12 设备连接不了，日志里有错误](#设备连接不了，日志里有错误)
    *   [5.13 设备扫描不出来](#设备扫描不出来)

## 安装

1.  [安装](/index.php/Install "Install") [bluez](https://www.archlinux.org/packages/?name=bluez)，这个软件包提供蓝牙的协议栈。
2.  [安装](/index.php/Install "Install") [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils)， 其提供 `bluetoothctl` 工具。 可选的软件包有 [bluez-utils-compat](https://aur.archlinux.org/packages/bluez-utils-compat/)，可额外安装 [已弃用的BLuez工具](#Deprecated_BlueZ_tools)。
3.  通用蓝牙驱动是 `btusb` 内核模块。[检查](/index.php/Kernel_module_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#获取信息 "Kernel module (简体中文)") 模块是否加载了。如果没有就先[加载模块](/index.php/Kernel_module_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#手动加载卸载 "Kernel module (简体中文)")。
4.  [Start/enable](/index.php/Start/enable "Start/enable") `bluetooth.service`。

**注意:**

*   蓝牙守护进程默认只会给属于`lp`组的用户暴露出bnep0设备。 如果你想连接到一个蓝牙范围的话先加入那个组。 你可以在 `/etc/dbus-1/system.d/bluetooth.conf` 修改那个组。
*   有的蓝牙适配器和无线网卡绑在一起（比如 [Intel Centrino](http://www.intel.com/content/www/us/en/wireless-products/centrino-advanced-n-6235.html)）。 这样的情况需要先启用无线网卡（笔记本上一般可以用功能键）来让内核可以识别蓝牙适配器。
*   有的蓝牙适配器（比如 Broadcom）和网络适配器冲突。所以你必须在网络服务启动之前先连接蓝牙。
*   类似于hcitool和hciconfig的工具已经停止开发，[bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) 里也没有包括，所以尽量不要使用它们。如果还是想用的话可以安装 [bluez-utils-compat](https://aur.archlinux.org/packages/bluez-utils-compat/)。 参阅和See [FS#53110](https://bugs.archlinux.org/task/53110) and [Bluez邮件列表](https://www.spinics.net/lists/linux-bluetooth/msg69239.html)

### 前端

#### 控制台

*   **bluetoothctl** — Pairing a device from the shell is one of the simplest and most reliable options.

	[http://www.bluez.org/](http://www.bluez.org/) || [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils)

**提示：** 输入 `echo -e "<command1>
<command2>
" | bluetoothctl` 来自动化bluetoothctl命令

#### 图形界面

下面的软件包提供图形界面来设置蓝牙。

*   **GNOME Bluetooth** — [GNOME](/index.php/GNOME "GNOME")的蓝牙工具。
    *   [gnome-bluetooth](https://www.archlinux.org/packages/?name=gnome-bluetooth) 提供后端。
    *   [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) 提供状态托盘。
    *   [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) 可通过图形界面配置蓝牙。可以在活动预览输入“蓝牙”或者运行 `gnome-control-center bluetooth` 进行配置。
    *   你还可以直接运行 `bluetooth-sendto` 命令来把文件发送到远程设备。
    *   打开蓝牙设置面板来接收文件；只有在蓝牙设置面板打开时才能接收文件。
    *   To add a Bluetooth entry to the *Send To* menu in Thunar's file properties menu, see instructions [here](http://docs.xfce.org/xfce/thunar/send-to). (The command that needs to be configured is `bluetooth-sendto %F`).

	[https://wiki.gnome.org/Projects/GnomeBluetooth](https://wiki.gnome.org/Projects/GnomeBluetooth) ||

*   **Bluedevil** — [KDE](/index.php/KDE "KDE")的蓝牙工具。如果Dolphin和系统托盘里没有蓝牙图标，就在系统托盘选项里启用，或者添加一个挂件。点击图标或在KDE系统设置里都可以配置蓝牙。

	[https://projects.kde.org/projects/kde/workspace/bluedevil](https://projects.kde.org/projects/kde/workspace/bluedevil) || [bluedevil](https://www.archlinux.org/packages/?name=bluedevil)

*   **Blueberry** — Linux Mint的GNOME Bluetooth变种，可在所有桌面环境工作。*Blueberry* 不支持通过Obex Object推送来接收文件。

	[https://github.com/linuxmint/blueberry](https://github.com/linuxmint/blueberry) || [blueberry](https://www.archlinux.org/packages/?name=blueberry)

*   **[Blueman](/index.php/Blueman "Blueman")** — 全功能蓝牙管理器。

	[https://github.com/blueman-project/blueman](https://github.com/blueman-project/blueman) || [blueman](https://www.archlinux.org/packages/?name=blueman)

*   **[ObexFTP](/index.php/ObexFTP "ObexFTP")** — 在任意启动了OBEX的设备上传输文件的工具。

	[http://dev.zuckschwerdt.org/openobex/wiki/ObexFtp](http://dev.zuckschwerdt.org/openobex/wiki/ObexFtp) || [obexftp](https://aur.archlinux.org/packages/obexftp/)

## 配对

**注意:** 使用蓝牙之前先检查有没有被 [rfkill](/index.php/Rfkill "Rfkill") 禁用。

这一小节介绍直接用*bluetoothctl*配置*bluez5*的方法，如果你已经有前端（比如GNOME Bluetooth）的话就不需要了。

真实步骤取决于包括的设备和它们的功能。以下是配对设备的一般步骤：

运行 `bluetoothctl` 交互命令。输入 `help` 来获取帮助。

1.  (optional) Select a default controller with `select *MAC_address*`.
2.  Enter `power on` to turn the power to the controller on. It is off by default and will turn off again each reboot, see [#Auto power-on after boot](#Auto_power-on_after_boot).
3.  Enter `devices` to get the MAC Address of the device with which to pair.
4.  Enter device discovery mode with `scan on` command if device is not yet on the list.
5.  Turn the agent on with `agent on` or choose a specific agent: if you press tab twice after `agent` you should see a list of available agents, e.g. DisplayOnly KeyboardDisplay NoInputNoOutput DisplayYesNo KeyboardOnly off on.
6.  Enter `pair *MAC_address*` to do the pairing (tab completion works).
7.  If using a device without a PIN, one may need to manually trust the device before it can reconnect successfully. Enter `trust *MAC_address*` to do so.
8.  Enter `connect *MAC_address*` to establish a connection.

以下为一个交互实例：

```
# bluetoothctl 
[NEW] Controller 00:10:20:30:40:50 pi [default]
[bluetooth]# agent KeyboardOnly 
Agent registered
[bluetooth]# default-agent 
Default agent request successful
[bluetooth]# power on
Changing power on succeeded
[CHG] Controller 00:10:20:30:40:50 Powered: yes
[bluetooth]# scan on
Discovery started
[CHG] Controller 00:10:20:30:40:50 Discovering: yes
[NEW] Device 00:12:34:56:78:90 myLino
[CHG] Device 00:12:34:56:78:90 LegacyPairing: yes
[bluetooth]# pair 00:12:34:56:78:90
Attempting to pair with 00:12:34:56:78:90
[CHG] Device 00:12:34:56:78:90 Connected: yes
[CHG] Device 00:12:34:56:78:90 Connected: no
[CHG] Device 00:12:34:56:78:90 Connected: yes
Request PIN code
[agent] Enter PIN code: 1234
[CHG] Device 00:12:34:56:78:90 Paired: yes
Pairing successful
[CHG] Device 00:12:34:56:78:90 Connected: no
[bluetooth]# connect 00:12:34:56:78:90
Attempting to connect to 00:12:34:56:78:90
[CHG] Device 00:12:34:56:78:90 Connected: yes
Connection successful

```

## 配置

### 开机后自动启动

蓝牙在重启后默认不会自动启动。命令 `hciconfig hci0 up` 已经被弃用，参阅 [release note](http://www.bluez.org/release-of-bluez-5-35/)。你只需要将 `AutoEnable=true` 添加在 `/etc/bluetooth/main.conf` 底部的 `[Policy]` 下面：

 `/etc/bluetooth/main.conf` 
```
[Policy]
AutoEnable=true
```

## 音频

要使用蓝牙耳机或音响的话要先安装 [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth)。 默认的PulseAudio配置就可以直接用蓝牙耳机或音响了。

**注意:** 有时要用 [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) 选择音频的输出设备。

如果你有全局的 PulseAudio 设置，首先确保运行守护进程（一般是 `pulse`）的用户在 `lp` 组，并且在 PulseAudio 配置中加载蓝牙模块：

 `/etc/pulse/system.pa` 
```
...
load-module module-bluetooth-policy
load-module module-bluetooth-discover
...
```

[Bluetooth headset](/index.php/Bluetooth_headset "Bluetooth headset") 页面有更多关于蓝牙耳机和音响的信息。

## 疑难解答

### 已弃用的Bluez工具

Eight BlueZ tools [were deprecated](https://git.kernel.org/pub/scm/bluetooth/bluez.git/commit/?id=b1eb2c4cd057624312e0412f6c4be000f7fc3617) and removed from [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils), although not all of them were superseded by newer tools. The [bluez-utils-compat](https://aur.archlinux.org/packages/bluez-utils-compat/) package provides an alternative version of [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) with the deprecated tools.

| Deprecated tool | Most likely replacement |
| [gatttool](https://manpages.debian.org/stretch/bluez/gatttool.1.en.html) | btgatt-client, [D-Bus Gatt API](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/gatt-api.txt) |
| [hciattach](https://manpages.debian.org/stretch/bluez/hciattach.1.en.html) | btattach |
| [hciconfig](https://manpages.debian.org/stretch/bluez/hciconfig.1.en.html) | btmgmt (and bluetoothctl?) |
| [hcidump](https://manpages.debian.org/stretch/bluez-hcidump/hcidump.1.en.html) | btmon (and btsnoop) |
| [hcitool](https://manpages.debian.org/stretch/bluez/hcitool.1.en.html) | missing, [D-Bus Device API](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/device-api.txt) available |
| [rfcomm](https://manpages.debian.org/stretch/bluez/rfcomm.1.en.html) | missing, implement with [D-Bus Profile1 API](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/profile-api.txt)? |
| [ciptool](https://manpages.debian.org/stretch/bluez/ciptool.1.en.html) |
| [sdptool](https://manpages.debian.org/stretch/bluez/sdptool.1.en.html) | missing, functionality seems to be scattered over different D-Bus objects: [Profile](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/profile-api.txt), [Advertising](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/advertising-api.txt), and the UUIDs arrays in [device](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/device-api.txt) and [adapter](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/adapter-api.txt). |

### gnome-bluetooth

如果接收文件时出现以下信息：

```
Bluetooth OBEX start failed: Invalid path
Bluetooth FTP start failed: Invalid path

```

确保 [XDG user directories](/index.php/XDG_user_directories "XDG user directories") 存在。

### 蓝牙USB电子狗

如果你在使用USB电子狗，你要先检查蓝牙电子狗是否被识别。插入USB电子狗后可通过 `journalctl -f` 检测（或查看 `/var/log/messages.log`）。 可能像下面这样:(注意hci）：

```
Feb 20 15:00:24 hostname kernel: [ 2661.349823] usb 4-1: new full-speed USB device number 3 using uhci_hcd
Feb 20 15:00:24 hostname bluetoothd[4568]: HCI dev 0 registered
Feb 20 15:00:24 hostname bluetoothd[4568]: Listening for HCI events on hci0
Feb 20 15:00:25 hostname bluetoothd[4568]: HCI dev 0 up
Feb 20 15:00:25 hostname bluetoothd[4568]: Adapter /org/bluez/4568/hci0 has been enabled

```

如果只有前两行，说明系统找到了设备而只需要启动它。 例：

 `hciconfig -a hci0` 
```
hci0:	Type: USB
	BD Address: 00:00:00:00:00:00 ACL MTU: 0:0 SCO MTU: 0:0
	DOWN 
	RX bytes:0 acl:0 sco:0 events:0 errors:0
        TX bytes:0 acl:0 sco:0 commands:0 errors:

```

```
# hciconfig hci0 up

```
 `hciconfig -a hci0` 
```
hci0:	Type: USB
	BD Address: 00:02:72:C4:7C:06 ACL MTU: 377:10 SCO MTU: 64:8
	UP RUNNING 
	RX bytes:348 acl:0 sco:0 events:11 errors:0
        TX bytes:38 acl:0 sco:0 commands:11 errors:0

```

用 `bluez-utils` 里的 `hcitool` 检查设备是否被检测到。 要获取可用设备和他们的标识和MAC地址可以输入：

 `$ hcitool dev` 
```
Devices:
        hci0	00:1B:DC:0F:DB:40

```

设备的详细信息可以用获取 `hciconfig`：

 `$ hciconfig -a hci0` 
```
hci0:   Type: USB
        BD Address: 00:1B:DC:0F:DB:40 ACL MTU: 310:10 SCO MTU: 64:8
        UP RUNNING PSCAN ISCAN
        RX bytes:1226 acl:0 sco:0 events:27 errors:0
        TX bytes:351 acl:0 sco:0 commands:26 errors:0
        Features: 0xff 0xff 0x8f 0xfe 0x9b 0xf9 0x00 0x80
        Packet type: DM1 DM3 DM5 DH1 DH3 DH5 HV1 HV2 HV3
        Link policy: RSWITCH HOLD SNIFF PARK
        Link mode: SLAVE ACCEPT 
        Name: 'BlueZ (0)'
        Class: 0x000100
        Service Classes: Unspecified
        Device Class: Computer, Uncategorized
        HCI Ver: 2.0 (0x3) HCI Rev: 0xc5c LMP Ver: 2.0 (0x3) LMP Subver: 0xc5c
        Manufacturer: Cambridge Silicon Radio (10)

```

#### Audio devices start to skip at short distance from dongle

If other devices share the same USB host, they can [interrupt communication with audio devices](https://bbs.archlinux.org/viewtopic.php?pid=1440161#p1440161). Make sure it is the only device attached to its bus. For example:

 `$ lsusb` 
```
Bus 002 Device 002: ID 0a12:0001 Cambridge Silicon Radio, Ltd Bluetooth Dongle (HCI mode)
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 004: ID 048d:1345 Integrated Technology Express, Inc. Multi Cardreader
Bus 001 Device 003: ID 0424:a700 Standard Microsystems Corp. 2 Port Hub
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### Logitech Bluetooth USB Dongle

There are Logitech dongles (ex. Logitech MX5000) that can work in two modes: Embedded and HCI. In embedded mode dongle emulates a USB device so it seems to your PC that you are using a normal USB mouse/keyoard.

If you hold the little red Button on the USB BT mini-receiver it will enable the other mode. Hold the red button on the BT dongle and plug it into the computer, and after 3-5 seconds of holding the button, the Bluetooth icon will appear in the system tray. [Discussion](http://ubuntuforums.org/showthread.php?t=1332197)

Alternatively, you can install the [bluez-hid2hci](https://www.archlinux.org/packages/?name=bluez-hid2hci) package. When you connect your Logitech dongle it will automatically switch.

### hcitool scan: Device not found

*   On some Dell laptops (e.g. Studio 15) you have to switch the Bluetooth mode from HID to HCI. Install the [bluez-hid2hci](https://www.archlinux.org/packages/?name=bluez-hid2hci) package, then [udev](/index.php/Udev "Udev") should do this automatically. Alternatively, you can run this command to switch to HCI manually:

```
# /usr/lib/udev/hid2hci

```

*   If the device will not show up and you have a Windows operating system on your machine, try booting it and enable the bluetooth adapter from windows.

*   Sometimes also this simple command helps:

```
# hciconfig hci0 up

```

### rfkill unblock：不能unblock

如果你的设备unblock后依然是soft blocked，试试：

```
$ connmanctl enable bluetooth

```

### 电脑蓝牙不可见

手机蓝牙扫描不到电脑？启动PSCAN和ISCAN：

```
# enable PSCAN and ISCAN
$ hciconfig hci0 piscan 
# check it worked

```
 `$ hciconfig` 
```
hci0:   Type: USB
        BD Address: 00:12:34:56:78:9A ACL MTU: 192:8 SCO MTU: 64:8
        **UP RUNNING PSCAN ISCAN**
        RX bytes:20425 acl:115 sco:0 events:526 errors:0
        TX bytes:5543 acl:84 sco:0 commands:340 errors:0

```

**注意:** 在 `/etc/bluetooth/main.conf` 检查设备可见超时和配对超时

Try changing device class in `/etc/bluetooth/main.conf` as following:

```
# Default device class. Only the major and minor device class bits are
# considered.
#Class = 0x000100 (from default config)
Class = 0x100100

```

This was the only solution to make my computer visible for my phone.

### 罗技键盘配对不了

If you do not get the passkey when you try to pair your Logitech keyboard, type the following command:

```
# hciconfig hci0 sspmode 0

```

If after pairing, the keyboard still does not connect, check the output of `hcidump -at`. If the latter indicates repeatedly connections-disconnections like the following message:

```
   status 0x00 handle 11 reason 0x13
   Reason: Remote User Terminated Connection

```

then, the only solution for now is to install [the old Bluetooth stack](/index.php/Bluez4 "Bluez4").

### HSP/HFP profiles

bluez5 removed support for the HSP/HFP profiles (telephony headset for [TeamSpeak](/index.php/TeamSpeak "TeamSpeak"), [Skype](/index.php/Skype "Skype"), etc.). You need to install [PulseAudio](/index.php/PulseAudio "PulseAudio") (>= version 6) or another application that implements HSP/HFP itself.

### Foxconn / Hon Hai / Lite-On Broadcom device

Some of these devices require the firmware to be flashed into the device at boot. The firmware is not provided but can converted from a Microsoft Windows *.hex* file into a *.hcd* using [hex2hcd](https://github.com/jessesung/hex2hcd) (which is installed with [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils)).

In order to get the right *.hex* file, try searching the device vendor:product code obtained with *lsusb*, for example:

```
   ...
   Bus 002 Device 004: ID **04ca:2006** Lite-On Technology Corp. Broadcom BCM43142A0 Bluetooth Device
   ...

```

or

```
   Bus 004 Device 004: Id **0489:e031** Foxconn / Hon Hai

```

Alternatively, boot into Windows (a virtual machine installation will suffice) and get the firmware name from the Device Manager utility. If you want to know the model of your device but cannot see it in *lsusb*, you might see it in *lsusb -v* as `iProduct`.

The *.hex* file can be extracted from the downloaded Windows driver without having to run Windows for it. Download the right driver, for example [Bluetooth Widcomm](http://www.fujitsupc.com/downloads/mobile/BLUETOOTH_WIDCOMM_V6.5.0.3100_WIN7-32_FPC46-1771-01.EXE) (listed among the drivers for [Lifebook P771](http://support.fujitsupc.com/CS/Portal/supportsearch.do?srch=DOWNLOADS&Series=P%20Series&Model=P771&ProductType=Notebook%20PC)), which contains the drivers for many Broadcomm devices. In case of Bluetooth Widcomm, the driver is a self-extracting RAR archive, so it can be extracted using *[unrar](https://www.archlinux.org/packages/?name=unrar) x*. To find out which of the many *.hex* files is the right one for you, look in the file `Win32/bcbtums-win7x86-brcm.inf` and search for `[RAMUSB**E031**.CopyList]`, where `E031` should be replaced with the product code (the second hex number in *lsusb*) of your device in upper-case. Underneath you should see the file name of the right *.hex* file.

Once you have the *.hcd* file, copy it into `/lib/firmware/brcm/BCM.hcd` - this filename is suggested by `dmesg` and it may change in your case so check your *dmesg* output in order to verify. Then reload the *btusb* module:

```
# rmmod btusb
# modprobe btusb

```

In some cases (with older kernels?), you have to flash the *.hcd* file with the *brcm_patchram_plus* utility, provided by [brcm_patchram_plus-git](https://aur.archlinux.org/packages/brcm_patchram_plus-git/). First, make sure in *dmesg* that the device is recognized by *btusb* as a bluetooth device. Then, run the following (replace *04ca 2006* with your vendor product pair):

```
# echo '04ca 2006' > /sys/bus/usb/drivers/btusb/new_id

```

Turn on the device:

```
# hciconfig hci0 up

```

Flash the firmware:

```
# brcm_patchram_plus_usb --patchram fw-04ca_2006.hcd hci0

```

The device should now be available. See [BBS#162688](https://bbs.archlinux.org/viewtopic.php?id=162688) for information on making these changes persistent.

### 设备配对后过一会儿又断开

如果运行 `journalctl`有以下结果，并且你的设备配对后过一会儿又断开：

```
bluetoothd: Unable to get connect data for Headset Voice gateway: getpeername: Transport endpoint is not connected (107)
bluetoothd: connect error: Connection refused (111)

```

这可能是因为你在其它操作系统中用同样的蓝牙适配器配对了这个设备（比如双启动）。有的设备不能在MAC地址和多个设备联系的情况下工作。你可以先移除设配再重新配对：

```
$ bluetoothctl
[bluetooth]# devices
Device XX:XX:XX:XX:XX:XX My Device
[bluetooth]# remove XX:XX:XX:XX:XX:XX

```

再 [重启](/index.php/Restart "Restart") `bluetooth.service`，打开蓝牙适配器，让设备可见，重新扫描配对。因为蓝牙管理器不一样，有时需要重启系统。

### 设备连接不了，日志里有错误

如果你在连接设备时看见 `journalctl` 的输出有类似的消息：

```
a2dp-source profile connect failed for 9C:64:40:22:E1:3F: Protocol not available

```

安装 [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth) 再重启 [PulseAudio](/index.php/PulseAudio "PulseAudio")。这个错误在文件传输是也会有。

### 设备扫描不出来

有的节能蓝牙设备用bluetoothctl扫描不出来，比如Logitech MX Master。可以安装 [bluez-utils-compat](https://aur.archlinux.org/packages/bluez-utils-compat/)再 [启动](/index.php/Start "Start") `bluetooth.service` 再输入：

```
# bluetoothctl
[NEW] Controller (MAC) myhostname [default]
[bluetooth]# power on
[CHG] Controller (MAC) Class: 0x0c010c
Changing power on succeeded
[CHG] Controller (MAC) Powered: yes
[bluetooth]# scan on
Discovery started
[CHG] Controller (MAC) Discovering: yes

```

在另一个终端里输入：

```
# hcitool lescan

```

等待你的设备出现，再按 Ctrl+C。 bluetoothctl 就可以获取你的设备并正常配对了。