[蓝牙](http://www.bluetooth.org/)是一个短距离无线通信标准，适用于手机、计算机和其他电子设备之间的通信。在 Linux 中，通常使用的蓝牙协议栈实现是 [BlueZ](http://www.bluez.org/).

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 通过命令行工具配置蓝牙](#.E9.80.9A.E8.BF.87.E5.91.BD.E4.BB.A4.E8.A1.8C.E5.B7.A5.E5.85.B7.E9.85.8D.E7.BD.AE.E8.93.9D.E7.89.99)
    *   [2.1 Bluetoothctl](#Bluetoothctl)
*   [3 图形化前端](#.E5.9B.BE.E5.BD.A2.E5.8C.96.E5.89.8D.E7.AB.AF)
    *   [3.1 GNOME Bluetooth](#GNOME_Bluetooth)
    *   [3.2 Bluedevil](#Bluedevil)
    *   [3.3 Blueberry](#Blueberry)
    *   [3.4 Blueman](#Blueman)
*   [4 手工配置](#.E6.89.8B.E5.B7.A5.E9.85.8D.E7.BD.AE)
    *   [4.1 音频流](#.E9.9F.B3.E9.A2.91.E6.B5.81)
*   [5 配对](#.E9.85.8D.E5.AF.B9)
*   [6 使用 Obex 发送接收文件](#.E4.BD.BF.E7.94.A8_Obex_.E5.8F.91.E9.80.81.E6.8E.A5.E6.94.B6.E6.96.87.E4.BB.B6)
*   [7 示例](#.E7.A4.BA.E4.BE.8B)
    *   [7.1 西门子 S55](#.E8.A5.BF.E9.97.A8.E5.AD.90_S55)
    *   [7.2 罗技鼠标 MX Laser / M555b](#.E7.BD.97.E6.8A.80.E9.BC.A0.E6.A0.87_MX_Laser_.2F_M555b)
    *   [7.3 摩托罗拉 V900](#.E6.91.A9.E6.89.98.E7.BD.97.E6.8B.89_V900)
    *   [7.4 摩托罗拉 RAZ](#.E6.91.A9.E6.89.98.E7.BD.97.E6.8B.89_RAZ)
    *   [7.5 使用bluez-simple-agent来跟iPhone配对](#.E4.BD.BF.E7.94.A8bluez-simple-agent.E6.9D.A5.E8.B7.9FiPhone.E9.85.8D.E5.AF.B9)
*   [8 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [8.1 passkey-agent](#passkey-agent)
    *   [8.2 Blueman](#Blueman_2)
    *   [8.3 gnome-bluetooth](#gnome-bluetooth)
    *   [8.4 Bluetooth USB 适配器](#Bluetooth_USB_.E9.80.82.E9.85.8D.E5.99.A8)
    *   [8.5 hcitool scan: 没找到设备](#hcitool_scan:_.E6.B2.A1.E6.89.BE.E5.88.B0.E8.AE.BE.E5.A4.87)
    *   [8.6 我的电脑不可见](#.E6.88.91.E7.9A.84.E7.94.B5.E8.84.91.E4.B8.8D.E5.8F.AF.E8.A7.81)
    *   [8.7 Nautilus cannot browse files](#Nautilus_cannot_browse_files)
*   [9 资源](#.E8.B5.84.E6.BA.90)

## 安装

[安装](/index.php/Install "Install") [bluez](https://www.archlinux.org/packages/?name=bluez) 和 [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) 软件包。[bluez](https://www.archlinux.org/packages/?name=bluez) 软件包提供蓝牙协议栈，[bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) 软件包提供 `bluetoothctl` 工具。 如果尚未加载通用蓝牙驱动则需先加载：

```
# modprobe btusb

```

然后 [启动](/index.php/Start "Start") `bluetooth.service` systemd 单元。可以在系统引导时自动 [启用](/index.php/Enable "Enable") 它。

**注意:**

*   默认情况下，蓝牙仅为 `lp` 用户组中的用户启用 bnep0 设备。如果想要加入蓝牙系统，需确认已将用户加入该组。可以修改`/etc/dbus-1/system.d/bluetooth.conf`文件中相应的组配置来实现。
*   有些蓝牙适配器是与无线网卡绑定在一起的（比如：[英特尔迅驰](http://www.intel.com/content/www/us/en/wireless-products/centrino-advanced-n-6235.html)）。这就要求无线网卡先被启用（典型情况是在笔记本电脑上用快捷键启用）以便蓝牙适配器对内核可见。
*   有些厂家（如 Broadcom）的蓝牙卡与网卡有冲突（不兼容）。这就需要确认在网络服务引导之前蓝牙设备已连接。

## 通过命令行工具配置蓝牙

### Bluetoothctl

通过命令行配对是最可靠的选择。准确的配对过程依不同设备类型及其所提供的输入功能而各不相同。下面提供使用`/usr/bin/bluetoothctl`配对的一般过程：

启动 `bluetoothctl` 交互命令。可以输入 `help` 列出所有有效的命令。

*   输入`power on` 命令打开控制器电源。默认是关闭的。
*   输入`devices` 命令获取要配对设备的 MAC 地址。
*   如果设备未在清单中列出，输入 `scan on` 命令设置设备发现模式。
*   输入`agent on` 命令打开代理。
*   输入 `pair *MAC Address*` 开始配对（支持 tab 键补全）。
*   如果使用无 PIN 码设备，再次连接可能需要手工认证。输入 `trust *MAC Address*` 命令。
*   最后，用 `connect *MAC_address*` 命令建立连接。

以下为一个交互实例：

```
# bluetoothctl 
[NEW] Controller 00:10:20:30:40:50 pi [default]
[bluetooth]# agent KeyboardOnly 
Agent registered
[bluetooth]# default-agent 
Default agent request successful
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

```

为使系统重启后激活设备，需添加一条 udev 规则：

 `/etc/udev/rules.d/10-local.rules` 
```
# Set bluetooth power up
ACTION=="add", KERNEL=="hci0", RUN+="/usr/bin/hciconfig hci0 up"
```

为使设备在系统挂起后唤醒时自动上电，应使用如下例所示 *systemd* 服务：

 `/etc/systemd/system/bluetooth-auto-power@.service` 
```
[Unit]
Description=Bluetooth auto power on
After=bluetooth.service sys-subsystem-bluetooth-devices-%i.device suspend.target

[Service]
Type=oneshot
#We could also do a 200 char long call to bluez via dbus. Except this does not work since bluez does not react to dbus at this point of the resume sequence and I do not know how I get this service to run at a time it does. So we just ignore bluez and force %i up using hciconfig. Welcome to the 21st century.
#ExecStart=/usr/bin/dbus-send --system --type=method_call --dest=org.bluez /org/bluez/%I org.freedesktop.DBus.Properties.Set string:org.bluez.Adapter1 string:Powered variant:boolean:true
ExecStart=/usr/bin/hciconfig %i up

[Install]
WantedBy=suspend.target

```

## 图形化前端

下面的软件包提供了一个图形化的界面来自定义蓝牙。

### GNOME Bluetooth

[GNOME Bluetooth](https://wiki.gnome.org/Projects/GnomeBluetooth) 是 [GNOME](/index.php/GNOME "GNOME") 的 蓝牙管理工具。[gnome-bluetooth](https://www.archlinux.org/packages/?name=gnome-bluetooth) 软件包提供后端。[gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) 提供状态监视小部件。[gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) 提供图形化配置前端工具，可以在**活动概览**中输入**Bluetooth**或者用 `gnome-control-center bluetooth` 命令打开。可以用 `bluetooth-sendto` 命令直接向远端设备发送文件。

要接收文件，必须安装 [gnome-user-share](https://www.archlinux.org/packages/?name=gnome-user-share) 软件包。然后在 *设置 -> 共享* 中授权配对的设备通过蓝牙接收文件。

**小贴士:** 若要在 Thunar 中文件属性的*发送到*菜单中增加蓝牙选项，参阅[这里](http://docs.xfce.org/xfce/thunar/send-to)的命令。（需要设置的命令是 `bluetooth-sendto %F`)。

### Bluedevil

bluedevil 是 [KDE](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)") 的蓝牙管理工具，可以用 [bluedevil](https://www.archlinux.org/packages/?name=bluedevil)（KDE Plasma 5）或 [bluedevil4](https://www.archlinux.org/packages/?name=bluedevil4)（KDE 4）[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")。

确认`bluetooth`守护进程在运行。你可以在dolphin和系统通知区域里得到一个蓝牙图标，你可以通过点击这个图标来设置bluedevil、检测蓝牙设备等等。你也可以通过KDE的系统设置来配置bluedevil。

### Blueberry

*Blueberry* 是 GNOME Bluetooth 的另一替代方案，可工作于所有桌面环境。可安装 [blueberry](https://www.archlinux.org/packages/?name=blueberry) 软件包。它提供了配置工具（*blueberry*）和系统托盘程序（*blueberry-tray*）。

### Blueman

参阅 [Blueman](/index.php/Blueman "Blueman")

## 手工配置

你需要编辑 `/etc/bluetooth` 下的配置文件来实现人工配置Bluez。它们是：

```
audio.conf
input.conf
main.conf
network.conf
rfcomm.conf

```

默认的配置文件在绝大多数情况下都能都正常工作。绝大多数的配置选项在她们的文件里都有丰富的文档注释，所以自定义成为了一个简单到阅读配置选项的描述和注释的工作。全局设置从`main.conf`开始

### 音频流

如果你想启用从你的设备到计算机的音频流，你必须更改 `audio.conf` 然后添加这个到 `[General]` 部分：

```
 Enable=Socket

```

## 配对

**注意:** 这一部分描述可能不是完全的准确。感谢**Gattschardo**解决了**个人验证码**部分

许多蓝牙(Bluetooth)设备要求在使用时[配对](http://en.wikipedia.org/wiki/Bluetooth#Pairing)。 实际上的过程取决于配对涉及到的设备和这些设备的输入功能。 在移动电话上的配对过程可能会像下面那样：

*   计算机向移动电话发送一个配对请求
*   移动电话上会提示输入一个由计算机给出的PIN（个人识别码）码
*   必须在计算机上重新输入同一个序列（指上文中的PIN）。

通过执行一下命令来搜索外部设备

```
 $ hcitool scan

```

在不使用gnome-bluez包的情况下配对设备，你需要使用一个包含在bluez包里的，叫做*bluez-simple-agent*的工具。你需要从常用的软件仓库里获取几个跟python相关的工具来使这种方法可用：dbus-python和pygobject。 如果你准备好了，你可以以root身份执行这个脚本：

```
 # bluez-simple-agent

```

如果它工作正常，你应当会在控制台得到消息："Agent registered" 。

现在你可以开始从你的移动电话开始配对工作，这个脚本会在控制台询问你PIN码，你输入进去然后按回车键确认，这样就完成了配对工作。接下来可以通过^C-c终止这个脚本的执行，只需要在配对的时候使用这个脚本，而连接设备时不需要用到它。

需要查看例子.请向下翻页到示例部分。

## 使用 Obex 发送接收文件

除了KDE和Gnome Bluetooth软件包之外，Obexfs是另一个选择，它可以允许你挂载你的移动电话作为文件系统的一部分。注意，如果要使用Obex，你需要一个能够提供Obex FTP服务的设备。 安装Obex;

```
# pacman -S obexfs

```

然后你可以以root权限运行如下命令来挂载你的移动电话

```
# obexfs -b <devices mac address> /mountpoint

```

单看更多挂载选项，参阅http://dev.zuckschwerdt.org/openobex/wiki/ObexFs

## 示例

### 西门子 S55

这是我链接我的S55的过程。（我还没搞明白怎么样通过电话来初始化连接。）

*   根据安装步骤

```
  $> hcitool scan
  Scanning ...
          XX:XX:XX:XX:XX:XX  NAME
  $> B=XX:XX:XX:XX:XX:XX

```

在另一个终端启动simple-agent

```
  $> su -c bluez-simple-agent 
  Password: 
  Agent registered

```

回到上一个终端

```
  $> obexftp -b $B -l "Address book"
  # Phone ask for pin, I enter it and answer yes when asked if I want to save the device
  ...
  <file name="5F07.adr" size="78712" modified="20030101T001858" user-perm="WD" group-perm="" />
  ...
  $> obexftp -b 00:01:E3:6B:FF:D7 -g "Address book/5F07.adr"
  Browsing 00:01:E3:6B:FF:D7 ...
  Channel: 5
  Connecting...done
  Receiving "Address book/5F07.adr"... Sending "Address book"... done
  Disconnecting...done
  $> obexftp -b 00:01:E3:6B:FF:D7 -p a                      
  ...
  Sending "a"... done
  Disconnecting...done

```

### 罗技鼠标 MX Laser / M555b

快速测试连接

```
$> hidd --connect XX:XX:XX:XX:XX:XX

```

通过桌面想到设置鼠标一实现自动重连。 如果你的桌面环境不提供对此任务的支持，参阅[Bluetooth mouse manual configuration](/index.php/Bluetooth_mouse_manual_configuration "Bluetooth mouse manual configuration")向导.

### 摩托罗拉 V900

在安装blueman并且运行blueman-applet之后,在摩托罗拉设备的菜单connections -> bluetooth下单击"find me"。在blueman-applet搜索设备，找到摩托罗拉，然后单击blueman-applet中的“添加。单击“bond”，输入pin码，根据摩托罗达上的提示输入相同的pin码，在终端执行：

```
  cd ~/
  mkdir bluetooth-temp
  obexfs -n xx:yy:zz:... ~/bluetooth-temp
  cd ~/bluetooth-temp

```

然后浏览... 这样操作时只能访问音频、视频和图片。

### 摩托罗拉 RAZ

```
> pacman -S obextool obexfs obexftp openobex bluez

```

```
> lsusb
Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 002: ID 03f0:171d Hewlett-Packard Wireless (Bluetooth + WLAN) Interface [Integrated Module]
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

```
> hciconfig hci0 up

```

```
> hciconfig
hci0:   Type: BR/EDR  Bus: USB
        BD Address: 00:16:41:97:BA:5E  ACL MTU: 1017:8  SCO MTU: 64:8
        UP RUNNING
        RX bytes:348 acl:0 sco:0 events:11 errors:0
        TX bytes:38 acl:0 sco:0 commands:11 errors:0

```

```
> hcitool dev
Devices:
        hci0    00:16:41:97:BA:5E

```

**注意：确保手机上的蓝牙处于打开状态并且是可见的**

```
> hcitool scan
Scanning ...
        00:1A:1B:82:9B:6D       [quirxi]

```

```
> hcitool inq
Inquiring ...
        00:1A:1B:82:9B:6D       clock offset: 0x1ee4    class: 0x522204

```

```
> l2ping 00:1A:1B:82:9B:6D
Ping: 00:1A:1B:82:9B:6D from 00:16:41:97:BA:5E (data size 44) ...
44 bytes from 00:1A:1B:82:9B:6D id 0 time 23.94ms
44 bytes from 00:1A:1B:82:9B:6D id 1 time 18.85ms
44 bytes from 00:1A:1B:82:9B:6D id 2 time 30.88ms
44 bytes from 00:1A:1B:82:9B:6D id 3 time 18.88ms
44 bytes from 00:1A:1B:82:9B:6D id 4 time 17.88ms
44 bytes from 00:1A:1B:82:9B:6D id 5 time 17.88ms
6 sent, 6 received, 0% loss

```

```
> hcitool name  00:1A:1B:82:9B:6D
[quirxi]

```

```
# hciconfig -a hci0
hci0:   Type: BR/EDR  Bus: USB
        BD Address: 00:16:41:97:BA:5E  ACL MTU: 1017:8  SCO MTU: 64:8
        UP RUNNING
        RX bytes:9740 acl:122 sco:0 events:170 errors:0
        TX bytes:2920 acl:125 sco:0 commands:53 errors:0
        Features: 0xff 0xff 0x8d 0xfe 0x9b 0xf9 0x00 0x80
        Packet type: DM1 DM3 DM5 DH1 DH3 DH5 HV1 HV2 HV3
        Link policy:
        Link mode: SLAVE ACCEPT
        Name: 'BCM2045'
        Class: 0x000000
        Service Classes: Unspecified
        Device Class: Miscellaneous,
        HCI Version: 2.0 (0x3)  Revision: 0x204a
        LMP Version: 2.0 (0x3)  Subversion: 0x4176
        Manufacturer: Broadcoml / Corporation (15)

```

```
> hcitool info 00:1A:1B:82:9B:6D
Requesting information ...
        BD Address:  00:1A:1B:82:9B:6D
        Device Name: [quirxi]
        LMP Version: 1.2 (0x2) LMP Subversion: 0x309
        Manufacturer: Broadcom Corporation (15)
        Features: 0xff 0xfe 0x0d 0x00 0x08 0x08 0x00 0x00
                <3-slot packets> <5-slot packets> <encryption> <slot offset>
                <timing accuracy> <role switch> <hold mode> <sniff mode>
                <RSSI> <channel quality> <SCO link> <HV2 packets>
                <HV3 packets> <A-law log> <CVSD> <power control>
                <transparent SCO> <AFH cap. slave> <AFH cap. master>

```

**编辑你的main.conf并且输入对应与你手机的class( Class = 0x100100 ):**

```
> vim /etc/bluetooth/main.conf

```

```
  # Default device class. Only the major and minor device class bits are
  # considered.
  #Class = 0x000100
  Class =  0x100100

```

```
> /etc/rc.d/dbus start
:: Starting D-BUS system messagebus 
[DONE]

```

```
> /etc/rc.d/bluetooth start
:: Stopping bluetooth subsystem:  pand dund rfcomm hidd  bluetoothd
[DONE]
:: Starting bluetooth subsystem:  bluetoothd

```

**通过bluez-simple-agent配对只需要做一次。当你的手机要求输入pin码时，输入0000**

```
> /usr/bin/bluez-simple-agent hci0 00:1A:1B:82:9B:6D
RequestPinCode (/org/bluez/10768/hci0/dev_00_1A_1B_82_9B_6D)
Enter PIN Code: 0000
Release
New device (/org/bluez/10768/hci0/dev_00_1A_1B_82_9B_6D)

```

**现在你可以动过ObexFTP来访问你手机上的文件了：**

```
> obexftp -v -b 00:1A:1B:82:9B:6D -B 9 -l
Connecting..\done
Tried to connect for 448ms
Receiving "(null)"...-<?xml version="1.0" ?>
<!DOCTYPE folder-listing SYSTEM "obex-folder-listing.dtd">
<folder-listing>
<parent-folder />
<folder name="audio" size="0" type="folder" modified="20101010T132323Z" user-perm="RW" />
<folder name="video" size="0" type="folder" modified="20101010T132323Z" user-perm="RW" />
<folder name="picture" size="0" type="folder" modified="20101010T132323Z" user-perm="RW" />
</folder-listing>
done
Disconnecting..\done

```

**你也可以把你的手机作为文件系统的一部分挂载在你的计算机上：**

```
> groupadd bluetooth
> mkdir /mnt/bluetooth
> chown root:bluetooth /mnt/bluetooth
> chmod 775 /mnt/bluetooth
> usermod -a -G bluetooth arno

```

```
> obexfs -b 00:1A:1B:82:9B:6D /mnt/bluetooth/
> l /mnt/bluetooth/
total 6
drwxr-xr-x 1 root root    0 10\. Okt 13:25 .
drwxr-xr-x 5 root root 4096 10\. Okt 10:08 ..
drwxr-xr-x 1 root root    0 10\. Okt 2010  audio
drwxr-xr-x 1 root root    0 10\. Okt 2010  picture
drwxr-xr-x 1 root root    0 10\. Okt 2010  video

```

### 使用bluez-simple-agent来跟iPhone配对

假设有一个叫做hci0的蓝牙设备和一个在hcitool里显示为'00:00:DE:AD:BE:EF'的iPhone：

```
   # bluez-simple-agent hci0 00:00:DE:AD:BE:EF
   Passcode:

```

## 疑难解答

### passkey-agent

```
$> passkey-agent --default 1234
Can't register passkey agent
The name org.bluez was not provided by any .service files

```

你可能在启动<tt>/etc/rc.d/dbus</tt>之前启动了 <tt>/etc/rc.d/bluetooth</tt>

```
$> hciconfig dev
# (no listing)

```

尝试运行 <tt>hciconfig hc0 up</tt>

### Blueman

如果blueman-applet启动失败，试着删除整个*/var/lib/bluetooth*目录然后重新启动电脑（或者仅仅重启hal、dbus和bluetooth这几个服务）。

```
# rm -rf /var/lib/bluetooth
# reboot

```

### gnome-bluetooth

如果你通过在蓝牙属性里接受文件时受到如下消息：

```
 Bluetooth OBEX start failed: Invalid path
 Bluetooth FTP start failed: Invalid path

```

那么运行

```
 # pacman -S xdg-user-dirs
 $ xdg-user-dirs-update

```

你可以通过下列方式修改路径：

```
 $ vi ~/.config/user-dirs.dirs

```

### Bluetooth USB 适配器

如果你在使用USB适配器，你应当确认你的适配器被正确识别。你可以在插入适配器时通过查看<tt>/var/log/messages.log</tt>，这应当会出现类似于下面所示的信息：

```
# tail -f /var/log/messages.log
May  2 23:36:40 tatooine usb 4-1: new full speed USB device using uhci_hcd and address 9
May  2 23:36:40 tatooine usb 4-1: configuration #1 chosen from 1 choice
May  2 23:36:41 tatooine hcid[8109]: HCI dev 0 registered
May  2 23:36:41 tatooine hcid[8109]: HCI dev 0 up
May  2 23:36:41 tatooine hcid[8109]: Device hci0 has been added
May  2 23:36:41 tatooine hcid[8109]: Starting security manager 0
May  2 23:36:41 tatooine hcid[8109]: Device hci0 has been activated

```

查看支持的硬件列表，请参考本页的[resources](/index.php/Bluetooth#Resources "Bluetooth")。

如果你只得到了前面两行，说明了电脑发现了这个设备，但是你需要手动启动它。 例如：

```
hciconfig -a hci0
hci0:	Type: USB
	BD Address: 00:00:00:00:00:00 ACL MTU: 0:0 SCO MTU: 0:0
	DOWN 
	RX bytes:0 acl:0 sco:0 events:0 errors:0
	TX bytes:0 acl:0 sco:0 commands:0 errors:
sudo hciconfig hci0 up
hciconfig -a hci0
hci0:	Type: USB
	BD Address: 00:02:72:C4:7C:06 ACL MTU: 377:10 SCO MTU: 64:8
	UP RUNNING 
	RX bytes:348 acl:0 sco:0 events:11 errors:0
	TX bytes:38 acl:0 sco:0 commands:11 errors:0

```

要验证这个设备被正确检测，你可以使用<tt>bluez-utils</tt>当中的<tt>hcitool</tt>。你可以通过下面方式获得受支持的设备、它们的识别码和硬件地址：

```
$ hcitool dev
Devices:
        hci0	00:1B:DC:0F:DB:40

```

可以通过<tt>hciconfig</tt>获得关于这个设备更详细的信息。

```
$ hciconfig -a hci0
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

### hcitool scan: 没找到设备

*   在某些Dell的笔记本电脑(比如 Studio 15)上，你必须把蓝牙模式由HID改成HCI

```
# hid2hci

```

*   有时候这个简单的命令也会有用：

```
# hciconfig hci0 up

```

### 我的电脑不可见

如果不能从你的移动电话上找到你的电脑，打开PSCAN和ISCAN：

```
# 打开 PSCAN 和 ISCAN
$ hciconfig hci0 piscan 
# 确认操作有效
$ hciconfig 
hci0:   Type: USB
        BD Address: 00:12:34:56:78:9A ACL MTU: 192:8 SCO MTU: 64:8
        **UP RUNNING PSCAN ISCAN**
        RX bytes:20425 acl:115 sco:0 events:526 errors:0
        TX bytes:5543 acl:84 sco:0 commands:340 errors:0

```

**注意:** 检查/etc/bluetooth/main.conf中的发现倒计时和配对倒计时

试着在 /etc/bluetooth/main.conf 改变设备的class

```
# Default device class. Only the major and minor device class bits are
# considered.
#Class = 0x000100 (from default config)
Class = 0x100100

```

This was the only solution to make my computer visible for my phone.

### Nautilus cannot browse files

If nautilus doesn't open and show this error:

```
Nautilus cannot handle obex: locations. Couldn't display "obex://[XX:XX:XX:XX:XX:XX]/".

```

Install gvfs-obexftp package:

```
# pacman -S gvfs-obexftp

```

## 资源

*   [Official Linux Bluetooth protocol stack](http://www.bluez.org)
*   [List of Linux supported Bluetooth Hardware](http://www.holtmann.org/linux/bluetooth/devices.html) >> The list is not available anymore!
*   [openSUSE Bluetooth Hardware Compatibility List (HCL)](http://en.opensuse.org/HCL/Bluetooth_Adapters)
*   [Gentoo wiki is usually good](http://www.gentoo.org/doc/en/bluetooth-guide.xml)
*   [Accessing a Bluetooth phone on Linux Gazette](http://linuxgazette.net/109/oregan3.html)
*   [Bluetooth computer visibility](http://www.adamish.com/blog/#a000361)