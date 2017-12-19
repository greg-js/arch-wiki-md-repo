**翻译状态：** 本文是英文页面 [Udev](/index.php/Udev "Udev") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-10-19，点击[这里](https://wiki.archlinux.org/index.php?title=Udev&diff=0&oldid=493547)可以查看翻译后英文页面的改动。

摘自[维基百科：Udev](https://en.wikipedia.org/wiki/Udev "wikipedia:Udev")：

	udev 是 Linux 内核的设备管理器。总的来说，它取代了 devfs 和 hotplug，负责管理 `/dev` 中的设备节点。同时，udev 也处理所有用户空间发生的硬件添加、删除事件，以及某些特定设备所需的固件加载。

`udev` 取代了`hotplug` 和 `hwdetect`两个工具。

与传统的顺序加载相比，udev 通过并行加载内核模块提供了潜在的性能优势。异步加载模块的方式也有一个天生的缺点：无法保证每次加载模块的顺序，如果机器具有多个块设备，那么它们的设备节点可能随机变化。例如如果有两个硬盘，`/dev/sda` 可能会随机变成`/dev/sdb`。[本文后面](#.E8.AE.BE.E7.BD.AE.E9.9D.99.E6.80.81.E8.AE.BE.E5.A4.87.E5.90.8D)有更详细的信息。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 udev 规则](#udev_.E8.A7.84.E5.88.99)
    *   [2.1 编写 udev 规则](#.E7.BC.96.E5.86.99_udev_.E8.A7.84.E5.88.99)
    *   [2.2 列出设备属性](#.E5.88.97.E5.87.BA.E8.AE.BE.E5.A4.87.E5.B1.9E.E6.80.A7)
    *   [2.3 加载前测试规则](#.E5.8A.A0.E8.BD.BD.E5.89.8D.E6.B5.8B.E8.AF.95.E8.A7.84.E5.88.99)
    *   [2.4 加载新规则](#.E5.8A.A0.E8.BD.BD.E6.96.B0.E8.A7.84.E5.88.99)
*   [3 Udisks](#Udisks)
*   [4 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [4.1 访问固件编程器（烧录器）和 USB 虚拟串行设备](#.E8.AE.BF.E9.97.AE.E5.9B.BA.E4.BB.B6.E7.BC.96.E7.A8.8B.E5.99.A8.EF.BC.88.E7.83.A7.E5.BD.95.E5.99.A8.EF.BC.89.E5.92.8C_USB_.E8.99.9A.E6.8B.9F.E4.B8.B2.E8.A1.8C.E8.AE.BE.E5.A4.87)
    *   [4.2 VGA 线缆接入时执行规则](#VGA_.E7.BA.BF.E7.BC.86.E6.8E.A5.E5.85.A5.E6.97.B6.E6.89.A7.E8.A1.8C.E8.A7.84.E5.88.99)
    *   [4.3 侦测新的 eSATA 设备](#.E4.BE.A6.E6.B5.8B.E6.96.B0.E7.9A.84_eSATA_.E8.AE.BE.E5.A4.87)
    *   [4.4 将内置 SATA 接口标记为 eSATA](#.E5.B0.86.E5.86.85.E7.BD.AE_SATA_.E6.8E.A5.E5.8F.A3.E6.A0.87.E8.AE.B0.E4.B8.BA_eSATA)
    *   [4.5 设置静态设备名](#.E8.AE.BE.E7.BD.AE.E9.9D.99.E6.80.81.E8.AE.BE.E5.A4.87.E5.90.8D)
        *   [4.5.1 视频设备](#.E8.A7.86.E9.A2.91.E8.AE.BE.E5.A4.87)
        *   [4.5.2 打印机](#.E6.89.93.E5.8D.B0.E6.9C.BA)
    *   [4.6 唤醒挂起的 USB 设备](#.E5.94.A4.E9.86.92.E6.8C.82.E8.B5.B7.E7.9A.84_USB_.E8.AE.BE.E5.A4.87)
    *   [4.7 触发事件](#.E8.A7.A6.E5.8F.91.E4.BA.8B.E4.BB.B6)
    *   [4.8 触发 udev 规则事件的桌面提示](#.E8.A7.A6.E5.8F.91_udev_.E8.A7.84.E5.88.99.E4.BA.8B.E4.BB.B6.E7.9A.84.E6.A1.8C.E9.9D.A2.E6.8F.90.E7.A4.BA)
*   [5 排错](#.E6.8E.92.E9.94.99)
    *   [5.1 屏蔽模块](#.E5.B1.8F.E8.94.BD.E6.A8.A1.E5.9D.97)
    *   [5.2 Debug output](#Debug_output)
    *   [5.3 udevd 引导时挂起](#udevd_.E5.BC.95.E5.AF.BC.E6.97.B6.E6.8C.82.E8.B5.B7)
    *   [5.4 BusLogic](#BusLogic)
    *   [5.5 一些移动设备不可移除](#.E4.B8.80.E4.BA.9B.E7.A7.BB.E5.8A.A8.E8.AE.BE.E5.A4.87.E4.B8.8D.E5.8F.AF.E7.A7.BB.E9.99.A4)
    *   [5.6 声音问题和一些不能自动加载的模块](#.E5.A3.B0.E9.9F.B3.E9.97.AE.E9.A2.98.E5.92.8C.E4.B8.80.E4.BA.9B.E4.B8.8D.E8.83.BD.E8.87.AA.E5.8A.A8.E5.8A.A0.E8.BD.BD.E7.9A.84.E6.A8.A1.E5.9D.97)
    *   [5.7 IDE CD/DVD 驱动器的支持](#IDE_CD.2FDVD_.E9.A9.B1.E5.8A.A8.E5.99.A8.E7.9A.84.E6.94.AF.E6.8C.81)
    *   [5.8 光驱被标识为磁盘](#.E5.85.89.E9.A9.B1.E8.A2.AB.E6.A0.87.E8.AF.86.E4.B8.BA.E7.A3.81.E7.9B.98)
*   [6 参阅](#.E5.8F.82.E9.98.85)

## 安装

Udev 现在是 [systemd](https://www.archlinux.org/packages/?name=systemd) 的组成部分，默认已安装。有关信息请查阅 `systemd-udevd.service(8)` 的[手册页](/index.php/Man_page "Man page")。

AUR 里有一个独立的 Udev 派生版：[eudev](/index.php/Eudev "Eudev")。

## udev 规则

udev 规则以管理员身份编写并保存在 `/etc/udev/rules.d/` 目录，其文件名必须以 `.rules` 结尾。各种软件包提供的规则文件位于 `/lib/udev/rules.d/`。如果 `/usr/lib` 和 `/etc` 这两个目录中有同名文件，则 `/etc` 中的文件优先。

### 编写 udev 规则

**警告:** 要挂载可移动设备，请**不要**通过在 udev 规则中调用 `mount` 命令的方法。对 FUSE 文件系统将会导致 `Transport endpoint not connected` 错误。应代之以 [udisks](/index.php/Udisks_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udisks (简体中文)") 以正确处理自动挂载。或者把挂载动作放在 udev 规则内部：

将 `/usr/lib/systemd/system/systemd-udevd.service` 复制到 `/etc/systemd/system/systemd-udevd.service`，将 `MountFlags=slave` 替换为 `MountFlags=shared`。[（来源）](http://unix.stackexchange.com/a/154318)

Keep in mind though that udev is not intended to invoke long-running processes.

*   要想学习写udev规则，请访问[编写 udev 规则](http://www.reactivated.net/writing_udev_rules.html)。（译注：[这里](http://www.cnitblog.com/luofuchong/archive/2007/12/18/37831.html)有一篇转载的该文简体中文译本）
*   要想查看 udev 规则的例子，请查阅上述文章的 [范例](http://www.reactivated.net/writing_udev_rules.html#example-printer) 章节。

下面是一个规则的实例，给出的是当接入一个摄像头时创建一个符号链接 `/dev/video-cam1` 。首先，我们发现摄像头被接入并且被挂载为 `/dev/video2` 设备。写下这条规则的原因是由于下一次引导时这个设备可能会有个不同的名字，比如 `/dev/video0`。

 `# udevadm info -a -p $(udevadm info -q path -n /dev/video2)` 
```
Udevadm info starts with the device specified by the devpath and then walks up the chain of parent devices. It prints for every device found, all possible attributes in the udev rules key format. A rule to match, can be composed by the attributes of the device and the attributes from one single parent device.

  looking at device '/devices/pci0000:00/0000:00:04.1/usb3/3-2/3-2:1.0/video4linux/video2':
    KERNEL=="video2"
    SUBSYSTEM=="video4linux"
    ...
  looking at parent device '/devices/pci0000:00/0000:00:04.1/usb3/3-2/3-2:1.0':
    KERNELS=="3-2:1.0"
    SUBSYSTEMS=="usb"
    ...
  looking at parent device '/devices/pci0000:00/0000:00:04.1/usb3/3-2':
    KERNELS=="3-2"
    SUBSYSTEMS=="usb"
    ...
    ATTRS{idVendor}=="05a9"
    ...
    ATTRS{manufacturer}=="OmniVision Technologies, Inc."
    ATTRS{removable}=="unknown"
    ATTRS{idProduct}=="4519"
    ATTRS{bDeviceClass}=="00"
    ATTRS{product}=="USB Camera"
    ...

```

From the video4linux device we use `KERNEL=="video2"` and `SUBSYSTEM=="video4linux"`, then we match the webcam using vendor and product ID's from the usb parent `SUBSYSTEMS=="usb"`, `ATTRS{idVendor}=="05a9"` and `ATTRS{idProduct}=="4519"`.

 `/etc/udev/rules.d/83-webcam.rules` 
```
KERNEL=="video[0-9]*", SUBSYSTEM=="video4linux", SUBSYSTEMS=="usb", ATTRS{idVendor}=="05a9", ATTRS{idProduct}=="4519", SYMLINK+="video-cam1"

```

In the example above we create a symlink using `SYMLINK+="video-cam1"` but we could easily set user `OWNER="john"` or group using `GROUP="video"` or set the permissions using `MODE="0660"`. However, if you intend to write a rule to do something when a device is being removed, be aware that device attributes may not be accessible. In this case, you will have to work with preset device [environment variables](/index.php/Environment_variables "Environment variables"). To monitor those environment variables, execute the following command while unplugging your device:

```
# udevadm monitor --environment --udev

```

In this command's output, you will see value pairs such as ID_VENDOR_ID and ID_MODEL_ID, which match your previously used attributes "idVendor" and "idProduct". A rule that uses device environment variables may look like this:

 `/etc/udev/rules.d/83-webcam-removed.rules` 
```
ACTION=="remove", SUBSYSTEM=="usb", ENV{ID_VENDOR_ID}=="05a9", ENV{ID_MODEL_ID}=="4519", RUN+="/path/to/your/script"

```

### 列出设备属性

To get a list of all of the attributes of a device you can use to write rules, run this command:

```
# udevadm info -a -n [device name]

```

Replace `[device name]` with the device present in the system, such as `/dev/sda` or `/dev/ttyUSB0`.

If you do not know the device name you can also list all attributes of a specific system path:

```
# udevadm info -a -p /sys/class/backlight/acpi_video0

```

### 加载前测试规则

```
# udevadm test $(udevadm info -q path -n [device name]) 2>&1

```

This will not perform all actions in your new rules but it will however process symlink rules on existing devices which might come in handy if you are unable to load them otherwise. You can also directly provide the path to the device you want to test the udev rule for:

```
# udevadm test /sys/class/backlight/acpi_video0/

```

### 加载新规则

Udev 自动侦测规则文件的变化，所以修改会立即生效，无需重启 udev。但已接入设备的规则不会自动触发。像 USB 这类热插拔设备也许需要重新插拔才能使新规则生效，也可能需要卸载并重载内核的 ohci-hcd 和 ehci-hcd 模块以重新挂载所有 USB 设备。

如果规则自动重载失败

```
# udevadm control --reload

```

可以手工强制触发规则

```
# udevadm trigger

```

## Udisks

参阅 [Udisks](/index.php/Udisks_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udisks (简体中文)").

## 提示与技巧

### 访问固件编程器（烧录器）和 USB 虚拟串行设备

下列规则允许 group 组用户访问 [USBtinyISP](http://www.ladyada.net/make/usbtinyisp/)（用于 AVR 微控制器的 USB 接口编程器）：

 `/etc/udev/rules.d/50-usbtinyisp.rules` 
```
SUBSYSTEMS=="usb", ATTRS{idVendor}=="1781", ATTRS{idProduct}=="0c9f", GROUP="users", MODE="0660"
SUBSYSTEMS=="usb", ATTRS{idVendor}=="16c0", ATTRS{idProduct}=="0479", GROUP="users", MODE="0660"
```

用 *lsusb* 命令可获取其他种类设备的厂商 ID 和产品 ID。

### VGA 线缆接入时执行规则

创建包含下列内容的规则文件 `/etc/udev/rules.d/95-monitor-hotplug.rules` ，可以在 VGA 线缆插入时执行 [arandr](https://www.archlinux.org/packages/?name=arandr)：

```
KERNEL=="card0", SUBSYSTEM=="drm", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="/home/*username*/.Xauthority", RUN+="/usr/bin/arandr"

```

**提示：** 某些显示管理器把 .Xauthority 文件保存在用户家目录以外的位置，需要修改 ENV{XAUTHORITY} 的内容。例如，[GNOME 显示管理器](/index.php/GDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GDM (简体中文)") 里的.Xauthority 文件路径如下所示： `$ printenv XAUTHORITY`  `/run/user/1000/gdm/Xauthority` 

### 侦测新的 eSATA 设备

If your eSATA drive is not detected when you plug it in, there are a few things you can try. You can reboot with the eSATA plugged in. Or you could try

```
# echo 0 0 0 | tee /sys/class/scsi_host/host*/scan

```

Or you could install [scsiadd](https://aur.archlinux.org/packages/scsiadd/) (from the AUR) and try

```
# scsiadd -s

```

Hopefully, your drive is now in `/dev`. If it is not, you could try the above commands while running

```
# udevadm monitor

```

to see if anything is actually happening.

### 将内置 SATA 接口标记为 eSATA

If you connected a eSATA bay or an other eSATA adapter the system will still recognize this disk as an internal SATA drive. [GNOME](/index.php/GNOME "GNOME") and [KDE](/index.php/KDE "KDE") will ask you for your root password all the time. The following rule will mark the specified SATA-Port as an external eSATA-Port. With that, a normal GNOME user can connect their eSATA drives to that port like a USB drive, without any root password and so on.

 `/etc/udev/rules.d/10-esata.rules` 
```
DEVPATH=="/devices/pci0000:00/0000:00:1f.2/host4/*", ENV{UDISKS_SYSTEM}="0"

```

**Note:** The `DEVPATH` can be found after connection the eSATA drive with the following commands (replace `sdb` accordingly):
```
# udevadm info -q path -n /dev/sdb
/devices/pci0000:00/0000:00:1f.2/host4/target4:0:0/4:0:0:0/block/sdb

```

```
# find /sys/devices/ -name sdb
/sys/devices/pci0000:00/0000:00:1f.2/host4/target4:0:0/4:0:0:0/block/sdb

```

### 设置静态设备名

由于 udev 异步加载所有模块，使得它们被初始化的次序不同。这将导致设备会随机改变名称。可以添加一条 udev 规则使得设备使用静态名称。

对于块设备和网络设备的规则配置，请分别参阅 [块设备持久化命名](/index.php/Persistent_block_device_naming_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Persistent block device naming (简体中文)") 和[网络配置-设备命名](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.AE.BE.E5.A4.87.E5.91.BD.E5.90.8D "Network configuration (简体中文)")。

#### 视频设备

For setting up the webcam in the first place, refer to [Webcam configuration](/index.php/Webcam_setup#Webcam_configuration "Webcam setup").

Using multiple webcams, useful for example with [motion](https://www.archlinux.org/packages/?name=motion) (software motion detector which grabs images from video4linux devices and/or from webcams), will assign video devices as /dev/video0..n randomly on boot. The recommended solution is to create symlinks using an *udev* rule (as in the example in [#编写 udev 规则](#.E7.BC.96.E5.86.99_udev_.E8.A7.84.E5.88.99)：

 `/etc/udev/rules.d/83-webcam.rules` 
```
KERNEL=="video[0-9]*", SUBSYSTEM=="video4linux", SUBSYSTEMS=="usb", ATTRS{idVendor}=="05a9", ATTRS{idProduct}=="4519", SYMLINK+="video-cam1"
KERNEL=="video[0-9]*", SUBSYSTEM=="video4linux", SUBSYSTEMS=="usb", ATTRS{idVendor}=="046d", ATTRS{idProduct}=="08f6", SYMLINK+="video-cam2"
KERNEL=="video[0-9]*", SUBSYSTEM=="video4linux", SUBSYSTEMS=="usb", ATTRS{idVendor}=="046d", ATTRS{idProduct}=="0840", SYMLINK+="video-cam3"

```

**Note:** Using names other than `/dev/video*` will break preloading of `v4l1compat.so` and perhaps `v4l2convert.so`

#### 打印机

If you use multiple printers, `/dev/lp[0-9]` devices will be assigned randomly on boot, which will break e.g. [CUPS](/index.php/CUPS "CUPS") configuration.

You can create following rule, which will create symlinks under `/dev/lp/by-id` and `/dev/lp/by-path`, similar to [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") scheme:

 `/etc/udev/rules.d/60-persistent-printer.rules` 
```
ACTION=="remove", GOTO="persistent_printer_end"

# This should not be necessary
#KERNEL!="lp*", GOTO="persistent_printer_end"

SUBSYSTEMS=="usb", IMPORT{builtin}="usb_id"
ENV{ID_TYPE}!="printer", GOTO="persistent_printer_end"

ENV{ID_SERIAL}=="?*", SYMLINK+="lp/by-id/$env{ID_BUS}-$env{ID_SERIAL}"

IMPORT{builtin}="path_id"
ENV{ID_PATH}=="?*", SYMLINK+="lp/by-path/$env{ID_PATH}"

LABEL="persistent_printer_end"

```

### 唤醒挂起的 USB 设备

First, find vendor and product ID of your device, for example

 `# lsusb | grep Logitech`  `Bus 007 Device 002: ID 046d:c52b Logitech, Inc. Unifying Receiver` 

Now change the `power/wakeup` attribute of the device and the USB controller it is connected to, which is in this case `driver/usb7/power/wakeup`. Use the following rule:

 `/etc/udev/rules.d/50-wake-on-device.rules` 
```
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="046d", ATTRS{idProduct}=="c52b", ATTR{power/wakeup}="enabled", ATTR{driver/usb7/power/wakeup}="enabled"

```

**Note:** Also make sure the USB controller is enabled in `/proc/acpi/wakeup`.

### 触发事件

It can be useful to trigger various udev events. For example, you might want to simulate a USB device disconnect on a remote machine. In such cases, use `udevadm trigger`:

```
# udevadm trigger -v -t subsystems -c remove -s usb -a "idVendor=abcd"

```

This command will trigger a USB remove event on all USB devices with vendor ID `abcd`.

### 触发 udev 规则事件的桌面提示

Invoking an external script containing calls to `notify-send` via *udev* [can sometimes be challenging](https://bbs.archlinux.org/viewtopic.php?id=212364) since the notification(s) never display on the Desktop. Here is an example of what commands and environmental variables need to be included in which files for `notify-send` to successfully be executed from a *udev* rule. NOTE: a number of variables are hardcoded in this example, thus consider making them portable (i.e., $USER rather than user's shortname) once you understand the example.

1) The following *udev* rule executes a script that plays a notification sound and sends a desktop notification when screen brightness is changed according to power state on a laptop. Create the file:

 `/etc/udev/rules.d/99-backlight_notification.rules` 
```
Play a notification sound and send a desktop notification when screen brightness is changed according to power state on a laptop (a second ''udev'' rule actually changes the screen brightness)
# Rule for when switching to battery
ACTION=="change", SUBSYSTEM=="power_supply", ATTR{type}=="Mains", ATTR{online}=="0", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="/home/USERNAME/.Xauthority" RUN+="/usr/bin/su USERNAME_TO_RUN_SCRIPT_AS -c /usr/local/bin/brightness_notification.sh"
# Rule for when switching to AC
ACTION=="change", SUBSYSTEM=="power_supply", ATTR{type}=="Mains", ATTR{online}=="1", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="/home/USERNAME/.Xauthority" RUN+="/usr/bin/su USERNAME_TO_RUN_SCRIPT_AS -c /usr/local/bin/brightness_notification.sh"

```

Note: 1) `USERNAME_TO_RUN_SCRIPT_AS` and `USERNAME` need to be changed to that of the shortname for the user of the graphical session where the notification will be displayed and 2) the script needs to be executed with `/usr/bin/su`, which will place its ownership under the user of the graphical session (rather than root/the system) where the notification will be displayed.

2) Contents of the executable script to be run on trigger of the *udev* rule:

 `/usr/local/bin/brightness_notification.sh` 
```
#!/usr/bin/env bash

export XAUTHORITY=/home/USERNAME_TO_RUN_SCRIPT_AS/.Xauthority
export DISPLAY=:0
export DBUS_SESSION_BUS_ADDRESS="unix:path=/run/user/UID_OF_USER_TO_RUN_SCRIPT_AS/bus"

/usr/bin/sudo -u USERNAME_TO_RUN_SCRIPT_AS /usr/bin/paplay --server /run/user/UID_OF_USER_TO_RUN_SCRIPT_AS/pulse/native /home/USERNAME/.i3/sounds/Click1.wav > /dev/null 2>&1

/usr/bin/notify-send -i /usr/share/icons/gnome/256x256/status/battery-full-charging.png 'Changing Power States' --expire-time=4000

```

Note: 1) `USERNAME_TO_RUN_SCRIPT_AS`, `UID_OF_USER_TO_RUN_SCRIPT_AS` and `USERNAME` needs to be changed to that of the shortname for the user and user's UID of the graphical session where the notification will be displayed; 2) `/usr/bin/sudo` is needed when playing audio via pulseaudio; and, 3) three environmental variables (i.e., `XAUTHORITY`, `DISPLAY` and `DBUS_SESSION_BUS_ADDRESS`) for the user of the graphical session where the notification will be displayed need to be defined and exported.

**Warning:** The `XAUTHORITY`, `DISPLAY` and `DBUS_SESSION_BUS_ADDRESS` environment variables must be defined correctly.

3) Load/reload the new *udev* rule (see above) and test it by unplugging the power supply to the laptop.

**Tip:** See also [xpub](https://github.com/Ventto/xpub) as a method for getting the user's display environment variables and exporting the last into *udev* rules via `IMPORT` key.

## 排错

### 屏蔽模块

极个别情况下，udev 也会犯错或加载错误的模块。为了防止错误的发生，你可以使用模块禁用列表。只要模块加入该列表，无论是启动时，或者是运行时（如usb硬盘等）udev都不会加载这些模块。参见[blacklisting](/index.php/Blacklisting "Blacklisting").

### Debug output

To get hardware debug info, use the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `udev.log-priority=debug`. Alternatively you can set

 `/etc/udev/udev.conf`  `udev_log="debug"` 

This option can also be compiled into your initramfs by adding the config file to your `FILES` array

 `/etc/mkinitcpio.conf`  `FILES="... /etc/udev/udev.conf"` 

and then rebuilding the initramfs with

```
# mkinitcpio -p linux

```

### udevd 引导时挂起

After migrating to LDAP or updating an LDAP-backed system udevd can hang at boot at the message "Starting UDev Daemon". This is usually caused by udevd trying to look up a name from LDAP but failing, because the network is not up yet. The solution is to ensure that all system group names are present locally.

Extract the group names referenced in udev rules and the group names actually present on the system:

```
# fgrep -r GROUP /etc/udev/rules.d/ /usr/lib/udev/rules.d | perl -nle '/GROUP\s*=\s*"(.*?)"/ && print $1;' | sort | uniq > udev_groups
# cut -f1 -d: /etc/gshadow /etc/group | sort | uniq > present_groups

```

To see the differences, do a side-by-side diff:

```
# diff -y present_groups udev_groups
...
network							      <
nobody							      <
ntp							      <
optical								optical
power							      |	pcscd
rfkill							      <
root								root
scanner								scanner
smmsp							      <
storage								storage
...

```

In this case, the `pcscd` group is for some reason not present in the system. [Add the missing groups](/index.php/Users_and_groups#Group_management "Users and groups"). Also, make sure that local resources are looked up before resorting to LDAP. `/etc/nsswitch.conf` should contain the following line:

```
group: files ldap

```

### BusLogic

BusLogic 设备被损坏而且导致启动时死机。这是一个内核的Bug目前还没有修正。

### 一些移动设备不可移除

创建自定义 udev 规则，设置 UDISKS_SYSTEM_INTERNAL=0。参见 udisks 手册。

### 声音问题和一些不能自动加载的模块

一些用户发现 `/etc/modprobe.d/sound.conf` 中的遗留配置会引起这些问题，请清理配置并重试。

**注意:** 从 `udev>=171` 开始 OSS 模拟模块(`snd_seq_oss, snd_pcm_oss, snd_mixer_oss`) 默认不会自动装载。

### IDE CD/DVD 驱动器的支持

Starting with version 170, udev does not support CD-ROM/DVD-ROM drives that are loaded as traditional IDE drives with the `ide_cd_mod` module and show up as `/dev/hd*`. The drive remains usable for tools which access the hardware directly, like *cdparanoia*, but is invisible for higher userspace programs, like KDE.

A cause for the loading of the ide_cd_mod module prior to others, like sr_mod, could be e.g. that you have for some reason the module piix loaded with your [initramfs](/index.php/Initramfs "Initramfs"). In that case you can just replace it with ata_piix in your `/etc/mkinitcpio.conf`.

### 光驱被标识为磁盘

If the group ID of your optical drive is set to `disk` and you want to have it set to `optical`, you have to create a custom udev rule:

 `/etc/udev/rules.d` 
```
# permissions for IDE CD devices
SUBSYSTEMS=="ide", KERNEL=="hd[a-z]", ATTR{removable}=="1", ATTRS{media}=="cdrom*", GROUP="optical"

# permissions for SCSI CD devices
SUBSYSTEMS=="scsi", KERNEL=="s[rg][0-9]*", ATTRS{type}=="5", GROUP="optical"
```

## 参阅

*   [udev 主页](https://www.kernel.org/pub/linux/utils/kernel/hotplug/udev/udev.html)
*   [udev 介绍](https://www.linux.com/news/hardware/peripherals/180950-udev)
*   [udev 邮件列表](http://vger.kernel.org/vger-lists.html#linux-hotplug)
*   [Scripting with udev](http://jasonwryan.com/blog/2014/01/20/udev/)
*   [编写 udev 规则](http://www.reactivated.net/writing_udev_rules.html)
*   [LFS 系统设备与模块处理](http://www.linuxfromscratch.org/lfs/view/6.1/chapter07/udev.html)
*   [Running GUI or accessing display variables from udev rules](https://github.com/Ventto/xpub)
*   中文读者可参阅 [金步国](http://www.jinbuguo.com/)先生翻译的 [udev 中文手册](http://www.jinbuguo.com/systemd/udev.html)