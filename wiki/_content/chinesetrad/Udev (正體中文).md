其他關於 **udev** 的資訊可以參考下面的連接 :

*   [http://www.kernel.org/pub/linux/utils/kernel/hotplug/udev-FAQ](http://www.kernel.org/pub/linux/utils/kernel/hotplug/udev-FAQ)
*   [https://bbs.archlinux.org/viewtopic.php?t=5702&start=0](https://bbs.archlinux.org/viewtopic.php?t=5702&start=0)

要把系統轉換到 Udev 下，你需要執行下列幾個步驟.

## Contents

*   [1 安裝 udev 套件](#.E5.AE.89.E8.A3.9D_udev_.E5.A5.97.E4.BB.B6)
*   [2 編輯 /etc/fstab](#.E7.B7.A8.E8.BC.AF_.2Fetc.2Ffstab)
*   [3 重新開機](#.E9.87.8D.E6.96.B0.E9.96.8B.E6.A9.9F)
    *   [3.1 警告 : 無法開啟一個 initial console](#.E8.AD.A6.E5.91.8A_:_.E7.84.A1.E6.B3.95.E9.96.8B.E5.95.9F.E4.B8.80.E5.80.8B_initial_console)
    *   [3.2 系統一直連續重啟不停](#.E7.B3.BB.E7.B5.B1.E4.B8.80.E7.9B.B4.E9.80.A3.E7.BA.8C.E9.87.8D.E5.95.9F.E4.B8.8D.E5.81.9C)
*   [4 使用者自訂 Udev](#.E4.BD.BF.E7.94.A8.E8.80.85.E8.87.AA.E8.A8.82_Udev)
*   [5 下面這一部份只適用於 udev >= 053](#.E4.B8.8B.E9.9D.A2.E9.80.99.E4.B8.80.E9.83.A8.E4.BB.BD.E5.8F.AA.E9.81.A9.E7.94.A8.E6.96.BC_udev_.3E.3D_053)
    *   [5.1 編輯權限和規則](#.E7.B7.A8.E8.BC.AF.E6.AC.8A.E9.99.90.E5.92.8C.E8.A6.8F.E5.89.87)
*   [6 Symlinking devices](#Symlinking_devices)
*   [7 相關資料](#.E7.9B.B8.E9.97.9C.E8.B3.87.E6.96.99)

## 安裝 udev 套件

```
pacman -S udev

```

## 編輯 /etc/fstab

請先把 sysfs 這一行設定註解掉，然後 "usbdevfs" 這一行設定必須改為使用 "usbfs" (在同一行內有兩個地方要修改). 最後, 請檢查 `/etc/fstab` 內是否一行設定包含了 `/dev/shm` 這個指定. 在編輯完 `/etc/fstab` 後，上面提到的這幾行應該看起來如同下面列出的一般 :

```
#sysfs /sys sysfs defaults 0 0
usbfs /proc/bus/usb usbfs defaults 0 0
none /dev/shm tmpfs defaults 0 0
none /dev/pts devpts defaults 0 0

```

你可能還需要把 `/etc/fstab` 這個檔案內的其他設定也依照上面的解釋一併修正，以符合 udev 的命名規則.

Make sure you use the `/dev/hda1` format and not `/dev/discs/disc0/part1` in `/etc/fstab` or you will get a false report of corrupt disk on booting.

## 重新開機

大功告成, 系統轉換完畢.

### 警告 : 無法開啟一個 initial console

如果你的系統在開機載入核心時當機並出現下面這一行警告訊息

```
WARNING: Unable to open an initial console

```

*   拿出你的 Arch Linux 安裝光碟然後用他來開機
*   掛載上你的 root 硬碟分割區 (例如 : "mount /dev/discs/disc0/part3 /mnt")
*   鍵入 chroot 轉移到新的掛載目錄上 (例如 : "chroot /mnt")
*   用下面的指令在 /dev 下建立缺少的 static nodes (靜態節點) :

```
cd /dev
mknod -m 660 console c 5 1
mknod -m 660 null c 1 3

```

These nodes are required for starting Udev. You might have both/only one of them/none missing.

More information [here](http://webpages.charter.net/decibelshelp/LinuxHelp_UDEVPrimer.html#consnull).

### 系統一直連續重啟不停

如果你的系統一直不停的連續重啟, 你可能需要把 menu.lst 裡面的下面這一行移除 :

```
devfs=nomount

```

然後當系統啟動完畢後, 請在終端機模式的命令列下鍵入:

```
/sbin/migrate-udev

```

現在，你可以再把 devfs=nomount 這一行放回 menu.lst 這個檔案內然後重新啟動系統. 這應該可以解決系統連續重啟的問題.

## 使用者自訂 Udev

When udev starts up, it will read all .rules files in **/etc/udev/rules.d/**. When udev is adding a device node, it reads these rules files in lexicographical order until it finds a match. That means that if you need any customizations, you should create a file that is lexicographically-less than the default file, **udev.rules**. It is the Arch custom to use **00.rules** for customizations, but obviously you can be more creative if you wish.

You should not edit the **/etc/udev/rules.d/udev.rules** file yourself, as it is used by the developers to improve the default ruleset for new users. If you need to tweak a rule from the default ruleset, just copy the line(s) and paste them into a **00.rules** file.

## 下面這一部份只適用於 udev >= 053

### 編輯權限和規則

The latest version of udev has some upstream changes in the configuration layout.

Permissions and user/group ownership are no longer defined in separate files -- instead they are specified within the rules file itself. Look at /etc/udev/rules.d/udev.rules for examples.

This means that any custom permissions need to be moved into a rules file like /etc/udev/rules.d/udev.rules or /etc/udev/rules.d/00-my.rules. The old files in etc/udev/permissions.d/ have no effect anymore and can be removed.

See the udev(8) manpage for more information on writing rules. The files in etc/udev/permissions.d/ have no effect anymore and can be removed.

The normal user should not need to define new rules, all you have to do is to add the user to the right groups in /etc/group:

```
gpasswd -a <username> video
gpasswd -a <username> audio
gpasswd -a <username> optical
gpasswd -a <username> floppy
gpasswd -a <username> storage
gpasswd -a <username> scanner

```

關於 group 權限的解說 :

```
video: enable tv cards, framebuffer devices (not! graphic cards they belong to users group)
audio: get access to sound devices and rtc
optical: allow burning and ripping from cd/dvd devices
floppy: allow formating and partitioning on floppy devices
storage: allow formating and partitioning on removable storage devices, like usbsticks or usb harddrives.
scanner: allow using the scanner devices

```

Symlinks of cd/dvd devices are done automatically and should fit your needs.

已知的問題:

*   如果你更新到 udev >=053 同時系統無法辨識你的 usb 拇指碟，請記得從新開機，然後一切應該都會恢復正常了

## Symlinking devices

this is only an example but it should be clear how it works. Add this at the `/etc/udev/rules.d/00-myrules.rules`:

```
# cdrom/cdrw links
KERNEL="hdc", SYMLINK="dvd"
KERNEL="hdd", SYMLINK="cdrom cdrecorder"
#important for modem users, change to ttyS1 if serial port 2 is used
KERNEL="ttyS0", SYMLINK="modem"
```

to check if your symlinks work or to restart udev:

```
/sbin/udevstart

```

更多關於規則的設定的資料請參閱:
[http://www.reactivated.net/udevrules.php](http://www.reactivated.net/udevrules.php)

## 相關資料

*   [Map Custom Device Entries with udev](/index.php/Map_Custom_Device_Entries_with_udev "Map Custom Device Entries with udev")