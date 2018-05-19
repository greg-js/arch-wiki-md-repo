相关文章

*   [USB storage devices](/index.php/USB_storage_devices "USB storage devices")

**翻译状态：** 本文是英文页面 [MTP](/index.php/MTP "MTP") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-30，点击[这里](https://wiki.archlinux.org/index.php?title=MTP&diff=0&oldid=447354)可以查看翻译后英文页面的改动。

[MTP](https://en.wikipedia.org/wiki/Media_Transfer_Protocol "wikipedia:Media Transfer Protocol") 是 "Media Transfer Protocol" (媒体传输协议)的缩写,很多移动和多媒体设备都支持这个协议.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 功能](#.E5.8A.9F.E8.83.BD)
    *   [1.2 文件管理器集成](#.E6.96.87.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8.E9.9B.86.E6.88.90)
*   [2 用法](#.E7.94.A8.E6.B3.95)
    *   [2.1 libmtp](#libmtp)
    *   [2.2 mtpfs](#mtpfs)
    *   [2.3 jmtpfs](#jmtpfs)
    *   [2.4 go-mtpfs](#go-mtpfs)
    *   [2.5 simple-mtpfs](#simple-mtpfs)
    *   [2.6 使用媒体播放器](#.E4.BD.BF.E7.94.A8.E5.AA.92.E4.BD.93.E6.92.AD.E6.94.BE.E5.99.A8)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 libmtp](#libmtp_2)
        *   [3.1.1 Unknown device](#Unknown_device)
        *   [3.1.2 不能列举USB设备](#.E4.B8.8D.E8.83.BD.E5.88.97.E4.B8.BEUSB.E8.AE.BE.E5.A4.87)
    *   [3.2 gvfs-mtp](#gvfs-mtp)
    *   [3.3 jmtpfs Input/output error upon first access](#jmtpfs_Input.2Foutput_error_upon_first_access)
    *   [3.4 kio-mtp](#kio-mtp)

## 安装

### 功能

[直接安装](/index.php/Pacman "Pacman") 软件包 [libmtp](https://www.archlinux.org/packages/?name=libmtp)。仅安装 [libmtp](http://libmtp.sourceforge.net/) 就已经可以正确的访问设备。为了添加与文件管理器的集成或者是提高传输和访问的速度，还可以安装以下的软件包：

These packages to choose from all implement a [Wikipedia:Filesystem in Userspace](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace"):

*   [mtpfs](https://www.archlinux.org/packages/?name=mtpfs)
*   [jmtpfs](https://aur.archlinux.org/packages/jmtpfs/) - 据说对 Android 4+ 以上的设备支持更好
*   [go-mtpfs-git](https://aur.archlinux.org/packages/go-mtpfs-git/) - 据说对 Android 3+ 以上的设备支持更好
*   [simple-mtpfs](https://aur.archlinux.org/packages/simple-mtpfs/)
*   [android-file-transfer](https://www.archlinux.org/packages/?name=android-file-transfer) - MTP 客户端，有精简的 UI

以上的这些都旨在提供比 `libmtp` 更好的使用体验。因为 USB 设备实在是太多，所以你可能需要先研究一下哪个更加适合于你的设备。

**Tip:** 建议在安装 MTP 软件包后重启电脑。

### 文件管理器集成

为了能够直接在文件管理器中通过 MTP 查看 Android 设备，需要安装以下插件：

*   如果文件管理器使用 [GVFS](/index.php/GVFS "GVFS") （GNOME Files)，安装 [gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp) 提供 MTP 支持或者是安装 [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2) 提供 PTP 支持。
*   如果文件管理器使用 KIO （KDE 的 Dolphin），安装 [kio-extras](https://www.archlinux.org/packages/?name=kio-extras) （KIO 的依赖包）。

当所需要的软件包已经安装，就可以通过链接访问设备了。比如 `mtp://[usb:002,013]/`。

## 用法

在使用之前，可能需要先建立一个挂载点用于设备的挂载，本例中的挂载目录为 ~/mnt。还有，在连接电脑之前需要解锁手机屏幕。

### libmtp

检测设备

```
# mtp-detect

```

来查看 MTP 设备是否检测到，如果出错，查看 [troubleshooting libmtp](#libmtp_2)。

**Note:** 需要将当前用户添加到 `uucp` 用户组。

使用以下指令连接到设备:

```
# mtp-connect

```

同样,你也可以使用以下的独立命令来访问您的 MTP 设备:

```
 mtp-albumart        mtp-emptyfolders    mtp-getplaylist     mtp-reset           mtp-trexist
 mtp-albums          mtp-files           mtp-hotplug         mtp-sendfile
 mtp-connect         mtp-folders         mtp-newfolder       mtp-sendtr
 mtp-delfile         mtp-format          mtp-newplaylist     mtp-thumb
 mtp-detect          mtp-getfile         mtp-playlists       mtp-tracks

```

### mtpfs

**警告:** 以下的操作可能不能正常的工作，你必须求助于 [gphoto2](/index.php/Digital_Cameras#libgphoto2 "Digital Cameras") 或者是其他基于 gvfs 的文件管理器(如[PCManFM](/index.php/PCManFM "PCManFM")。

首先编辑 `/etc/fuse.conf` 注释掉以下行：

```
user_allow_other

```

将设备挂载到 `~/mnt`：

```
$ mtpfs -o allow_other ~/mnt

```

从 `~/mnt` 卸载设备：

```
$ fusermount -u ~/mnt

```

Make this cohere to the rest of Linux (use regular mount/umount commands) by doing two steps

```
$# ln -s <actual mount command's path/name>  <a name consistent with Linux's mount convention>
$  ln -s /sbin/jmtpfs                        /sbin/mount.jmtpfs

```

add this line to /etc/fstab;

```
 #jmtpfs <mount path>        fuse nodev,allow_other,<other options>                             0    0
  jmtpfs /home/sam/run/motog fuse nodev,allow_other,rw,user,noauto,noatime,uid=1000,gid=1000    0    0

```

Now mount the device and see if the options "took"

```
 $ mount /home/sam/run/motog
 Device 0 (VID=22b8 and PID=2e82) is a Motorola Moto G (ID2).
 Android device detected, assigning default bug flags
 $ mount 
  ...
  jmtpfs on /home/sam/run/motog type fuse.jmtpfs (rw,nosuid,nodev,noexec,noatime,user_id=1000,group_id=1000,allow_other,user=sam)

```

### jmtpfs

使用此命令挂载设备(需要确保挂载点可用):

```
$ jmtpfs ~/mtp

```

使用此命令卸载设备

```
$ fusermount -u ~/mtp

```

### go-mtpfs

**Note:** Mounting with `go-mtpfs` might fail if an external SD Card is present. If you try to access your device while having an SD card and go-mtpfs complains, try removing the SD card and mounting again.

Install [android-udev](https://www.archlinux.org/packages/?name=android-udev), which will allow you to edit `/etc/udev/rules.d/51-android.rules` and apply to your `idVendor` and `idProduct`, which you can see after running *mtp-detect*. To the end of the line, add your user `OWNER="<user>"`.

*   挂载设备:

```
go-mtpfs Android

```

*   卸载设备:

```
fusermount -u Android

```

您可以在 .bashrc 为这个命令设置一个别名,来让它更加的符合你的口味.

### simple-mtpfs

这是MTP设备的另外一个用户空间文件系统。 你可能会觉得它比[mtpfs](https://www.archlinux.org/packages/?name=mtpfs)更加可靠。你能通过AUR安装或者从源代码编译[simple-mtpfs](https://aur.archlinux.org/packages/simple-mtpfs/)。记住 **不要** 用root运行下面的命令。

*   查看MTP设备，运行：

```
 simple-mtpfs --list-devices

```

*   挂在一个MTP设备 (in this example device 0)，运行：

```
simple-mtpfs /path/to/your/mount/point

```

*   卸载，运行

```
 fusermount -u /path/to/your/mount/point

```

### 使用媒体播放器

您也可以在音乐播放器中使用 MTP 设备,例如 Amarok 等. 但是您也许要做以下的操作:编辑 `/etc/udev/rules.d/51-android.rules` [ MTP 设备使用示例如下(以 Galaxy Nexus 为例)]: 执行命令:

```
$ lsusb

```

查看您的设备信息,他们一般看起来像:

```
Bus 003 Device 011: ID 04e8:6860 Samsung Electronics Co., Ltd GT-I9100 Phone [Galaxy S II], GT-P7500 [Galaxy Tab 10.1]

```

在这种情况下，条目将是：

```
SUBSYSTEM=="usb", ATTR{idVendor}=="04e8", ATTR{idProduct}=="6860", MODE="0666", OWNER="[username]"

```

然后重新载入 udev 规则:

```
# udevadm control --reload

```

**Note:** 安装了 MTP 后您需要重启设备以使其生效

## Troubleshooting

### libmtp

#### Unknown device

如果你看到像这样的信息:

```
Device 0 (VID=XXXX and PID=XXXX) is UNKNOWN.
Please report this VID/PID and the device model to the libmtp development team

```

你应该核对你的设备是否列在[supported devices list](http://sourceforge.net/p/libmtp/code/ci/HEAD/tree/src/music-players.h)上。如果没有，那么你应该像开发团队报告，而且，可能你的 `libmtp` 稍稍有点过时。 允许你的设备能通过`libmtp`适当地使用，你应该添加你的设备到：

```
/etc/udev/rules.d/69-libmtp.rules

```

#### 不能列举USB设备

如果你在系统日志中看到像这样的信息(`journalctl`)

```
 usb usb4-port2: unable to enumerate USB device

```

你能够尝试下面的临时[解决方案](https://bbs.archlinux.org/viewtopic.php?pid=1087323#p1087323)

```
 # modprobe -vr uhci_hcd
 # modprobe -va ohci_hcd
 # modprobe -va uhci_hcd

```

如果它工作，你应该创建`/etc/modprobe.d/usb_hci_order.conf`和下面的内容。

```
 # create a dependency on ohci for uhci, which fixes problems
 # with external usb devices not showing up
 #
 softdep uhci_hcd pre: ohci_hcd

```

### gvfs-mtp

如果你已经安装了[gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp)，并且你的设备没有在文件管理器中出现,为了能够用自动挂在设备，你可能需要重启电脑或者写入一个udev规则。

插入设备后你能分别得到厂商ID和产品编号：

```
$ lsusb
Bus 001 Device 007: ID 0421:0661 Nokia Mobile Phones Lumia 920
(...)

```

在ID后的两串数字是*厂商ID* : *产品编号*

然后设定一个udev规则，

```
# nano /etc/udev/rules.d/51-android.rules

```

并且列出规则：

```
ATTR{idVendor}=="YOUR VENDOR ID HERE", ATTR{idProduct}=="YOUR PRODUCT ID HERE", SYMLINK+="libmtp",  MODE="660", ENV{ID_MTP_DEVICE}="1"

```

重新加载udev规则。

```
# udevadm control --reload

```

And reboot the system. Now file managers (like Thunar) should be able to automount the MTP Device. [[1]](https://bbs.archlinux.org/viewtopic.php?id=180719)

### jmtpfs Input/output error upon first access

Symptoms: jmtpfs successfully mounts, but as soon as one attempts to access files on the device (e.g. via `ls`), an error is reported:

```
 cannot access <mount-point>: Input/output error

```

This appears to be a security feature: MTP does not work when the phone is locked by the lockscreen. Unlock the phone and it should work again as long as the cord remains connected.

### kio-mtp

如果你不能够使用“打开文件管理器”操作，你可以通过编辑文件`/usr/share/apps/solid/actions/solid_mtp.desktop`解决这个问题。

使下面这行：

```
Exec=kioclient exec mtp:udi=%i/

```

变成

```
Exec=dolphin "mtp:/"

```