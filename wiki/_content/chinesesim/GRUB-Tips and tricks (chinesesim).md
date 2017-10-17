See [GRUB](/index.php/GRUB "GRUB") for the main article.

## Contents

*   [1 其它安装方式](#.E5.85.B6.E5.AE.83.E5.AE.89.E8.A3.85.E6.96.B9.E5.BC.8F)
    *   [1.1 安装到U盘](#.E5.AE.89.E8.A3.85.E5.88.B0U.E7.9B.98)
        *   [1.1.1 BIOS](#BIOS)
        *   [1.1.2 EFI](#EFI)
    *   [1.2 安装到分区上或者无分区磁盘上](#.E5.AE.89.E8.A3.85.E5.88.B0.E5.88.86.E5.8C.BA.E4.B8.8A.E6.88.96.E8.80.85.E6.97.A0.E5.88.86.E5.8C.BA.E7.A3.81.E7.9B.98.E4.B8.8A)
    *   [1.3 只生成core.img](#.E5.8F.AA.E7.94.9F.E6.88.90core.img)
*   [2 图形化配置工具](#.E5.9B.BE.E5.BD.A2.E5.8C.96.E9.85.8D.E7.BD.AE.E5.B7.A5.E5.85.B7)
*   [3 视觉配置](#.E8.A7.86.E8.A7.89.E9.85.8D.E7.BD.AE)
    *   [3.1 设置帧缓冲分辨率](#.E8.AE.BE.E7.BD.AE.E5.B8.A7.E7.BC.93.E5.86.B2.E5.88.86.E8.BE.A8.E7.8E.87)
        *   [3.1.1 设定帧缓冲的分辨率](#.E8.AE.BE.E5.AE.9A.E5.B8.A7.E7.BC.93.E5.86.B2.E7.9A.84.E5.88.86.E8.BE.A8.E7.8E.87)
    *   [3.2 915resolution hack](#915resolution_hack)
    *   [3.3 背景图像和点阵字体](#.E8.83.8C.E6.99.AF.E5.9B.BE.E5.83.8F.E5.92.8C.E7.82.B9.E9.98.B5.E5.AD.97.E4.BD.93)
    *   [3.4 Theme](#Theme)
    *   [3.5 菜单颜色](#.E8.8F.9C.E5.8D.95.E9.A2.9C.E8.89.B2)
    *   [3.6 隐藏菜单](#.E9.9A.90.E8.97.8F.E8.8F.9C.E5.8D.95)
    *   [3.7 禁用framebuffer](#.E7.A6.81.E7.94.A8framebuffer)
*   [4 Booting ISO9660 image file directly via GRUB](#Booting_ISO9660_image_file_directly_via_GRUB)
*   [5 持久块设备命名法](#.E6.8C.81.E4.B9.85.E5.9D.97.E8.AE.BE.E5.A4.87.E5.91.BD.E5.90.8D.E6.B3.95)
*   [6 使用卷标](#.E4.BD.BF.E7.94.A8.E5.8D.B7.E6.A0.87)
*   [7 用密码保护 GRUB 菜单](#.E7.94.A8.E5.AF.86.E7.A0.81.E4.BF.9D.E6.8A.A4_GRUB_.E8.8F.9C.E5.8D.95)
*   [8 启动时隐藏GRUB界面,除非按着SHIFT键](#.E5.90.AF.E5.8A.A8.E6.97.B6.E9.9A.90.E8.97.8FGRUB.E7.95.8C.E9.9D.A2.2C.E9.99.A4.E9.9D.9E.E6.8C.89.E7.9D.80SHIFT.E9.94.AE)
*   [9 使用 UUID 和基础脚本](#.E4.BD.BF.E7.94.A8_UUID_.E5.92.8C.E5.9F.BA.E7.A1.80.E8.84.9A.E6.9C.AC)
*   [10 手动创建 grub.cfg](#.E6.89.8B.E5.8A.A8.E5.88.9B.E5.BB.BA_grub.cfg)
*   [11 Multiple entries](#Multiple_entries)
    *   [11.1 Disable submenu](#Disable_submenu)
    *   [11.2 调用之前的启动项](#.E8.B0.83.E7.94.A8.E4.B9.8B.E5.89.8D.E7.9A.84.E5.90.AF.E5.8A.A8.E9.A1.B9)
    *   [11.3 Changing the default menu entry](#Changing_the_default_menu_entry)
    *   [11.4 设定下次启动的启动项(一次性,非持久)](#.E8.AE.BE.E5.AE.9A.E4.B8.8B.E6.AC.A1.E5.90.AF.E5.8A.A8.E7.9A.84.E5.90.AF.E5.8A.A8.E9.A1.B9.28.E4.B8.80.E6.AC.A1.E6.80.A7.2C.E9.9D.9E.E6.8C.81.E4.B9.85.29)
*   [12 UEFI 延伸阅读](#UEFI_.E5.BB.B6.E4.BC.B8.E9.98.85.E8.AF.BB)
    *   [12.1 其他方法](#.E5.85.B6.E4.BB.96.E6.96.B9.E6.B3.95)
    *   [12.2 在固件启动管理器中创建GRUB条目](#.E5.9C.A8.E5.9B.BA.E4.BB.B6.E5.90.AF.E5.8A.A8.E7.AE.A1.E7.90.86.E5.99.A8.E4.B8.AD.E5.88.9B.E5.BB.BAGRUB.E6.9D.A1.E7.9B.AE)
    *   [12.3 创建GRUB Standalone模式的UEFI应用程序](#.E5.88.9B.E5.BB.BAGRUB_Standalone.E6.A8.A1.E5.BC.8F.E7.9A.84UEFI.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
    *   [12.4 Technical information](#Technical_information)

## 其它安装方式

### 安装到U盘

#### BIOS

假设 U盘的第一个分区是 FAT32，其分区是/dev/sdy1

```
# mkdir -p /mnt/usb
# mount /dev/sdy1 /mnt/usb
# grub-install --target=i386-pc --debug --boot-directory=/mnt/usb/boot /dev/sdy
# grub-mkconfig -o /mnt/usb/boot/grub/grub.cfg

```

可以选择将配置备份到 `grub.cfg`:

```
# mkdir -p /mnt/usb/etc/default
# cp /etc/default/grub /mnt/usb/etc/default
# cp -a /etc/grub.d /mnt/usb/etc

```

```
# sync; umount /mnt/usb

```

#### EFI

To have grub write its EFI image to `/boot/efi/EFI/BOOT/BOOTX64.efi`, which the boot firmware will be able to find without any UEFI boot entry, use `--removable` when you run `grub-install`.

### 安装到分区上或者无分区磁盘上

**警告:** GRUB **不推荐**将其安装到分区启动扇区或者无分区磁盘上(Grub Legacy和syslinux相反).这种安装方式不安全,当升级时可能会损坏. Arch开发人员也不支持这种方式

下面的命令将会将 GRUB 安装到分区扇区或者无分区磁盘上,下面例子中 `/dev/sdaX` 用作 `/boot`

```
# chattr -i /boot/grub/i386-pc/core.img
# grub-install --target=i386-pc --debug --force /dev/sdaX
# chattr +i /boot/grub/i386-pc/core.img

```

*   使用 `--target=i386-pc` 参数时，仅安装 BIOS 系统. 推荐一直标明这点以防混淆.
*   不应使用`--grub-setup=/bin/true`(这个选项的效果类似于只生成`core.img`)
*   `grub-install`会生成以下警告, 请了解这个方式有可能出现的问题。

```
/sbin/grub-setup: warn: Attempting to install GRUB to a partitionless disk or to a partition. This is a BAD idea.
/sbin/grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists. 
                        However, blocklists are UNRELIABLE and their use is discouraged.

```

*   必须使用`--force`选项来启用对 blocklists (块列表)的支持。否则会出现以下错误,并且不会将启动代码安装到启动扇区上:

```
/sbin/grub-setup: error: will not proceed with blocklists

```

而指定了`--force`,会出现:

```
Installation finished. No error reported.

```

`grub-setup` 默认不允许这种情况的原因是,在分区或者无分区磁盘上,`grub`依赖于嵌入分区引导扇区的块列表(blocklists)来定位`/boot/grub/i386-pc/core.img`和`/boot/grub`.而`core.img`在分区上的扇区位置很有可能随着分区文件系统的更改而变化(复制文件,删除文件等).详情请参考https://bugzilla.redhat.com/show_bug.cgi?id=728742 和 [https://bugzilla.redhat.com/show_bug.cgi?id=730915](https://bugzilla.redhat.com/show_bug.cgi?id=730915).

临时解决方案是给`/boot/grub/i386-pc/core.img`文件加"不可变"(immutable)标志.这样 `core.img` 文件的位置就不会变。只有当将`grub`安装到分区启动扇区或者无分区磁盘上时才需要给core.img加"不可变"标志.

执行`grub-install`并不会生成GRUB配置文件,请移至[#生成主配置文件](#.E7.94.9F.E6.88.90.E4.B8.BB.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)一节

即使没有报错，生成的 `grub.cfg` 文件并不会包含正确的 UUID。参考 [https://bbs.archlinux.org/viewtopic.php?pid=1294604#p1294604.要解决这个问题：](https://bbs.archlinux.org/viewtopic.php?pid=1294604#p1294604.要解决这个问题：)

```
# mount /dev/sdxY /mnt        #Your root partition.
# mount /dev/sdxZ /mnt/boot   #Your boot partition (if you have one).
# arch-chroot /mnt
# pacman -S linux
# grub-mkconfig -o /boot/grub/grub.cfg

```

### 只生成core.img

通过添加`--grub-setup=/bin/true`选项,`grub-install`命令会填充`/boot/grub`文件夹并生成`/boot/grub/i386-pc/core.img`,但是不会将grub启动引导代码嵌入到MBR,post-MBR gap和分区引导扇区中, 以 `/dev/sda` 磁盘为例：

```
# grub-install --target=i386-pc --grub-setup=/bin/true --debug /dev/sda

```

**Note:** `--target=i386-pc`指示`grub-install`是为使用BIOS的系统安装. 推荐一直标明这点以防混淆.

生成后, Grub Legacy 或者 syslinux 就可以通过链式加载 GRUB 的`core.img`来间接加载Linux内核或者多启动内核了.参阅[Syslinux#Chainloading](/index.php/Syslinux#Chainloading "Syslinux")。

## 图形化配置工具

*   **grub-customizer** — 定制bootloader(GRUB or BURG)

	[https://launchpad.net/grub-customizer](https://launchpad.net/grub-customizer) || [grub-customizer](https://aur.archlinux.org/packages/grub-customizer/)

*   **grub2-editor** — KDE4上配置GRUB的控制模组

	[http://kde-apps.org/content/show.php?content=139643](http://kde-apps.org/content/show.php?content=139643) || [grub2-editor](https://aur.archlinux.org/packages/grub2-editor/)

*   **kcm-grub2** — 可以管理大部分常用GRUB配置的kcm模组

	[http://kde-apps.org/content/show.php?content=137886](http://kde-apps.org/content/show.php?content=137886) || [kcm-grub2](https://aur.archlinux.org/packages/kcm-grub2/)

*   **startupmanager** — GRUB Legacy, GRUB, Usplash and Splashy的图形化配置工具([abandonned](https://launchpad.net/startup-manager/+announcement/8300))

	[http://sourceforge.net/projects/startup-manager/](http://sourceforge.net/projects/startup-manager/) || [startupmanager](https://aur.archlinux.org/packages/startupmanager/)

## 视觉配置

在GRUB的默认情况中是可以改变菜单外观的。如果你没有初始化，请务必初始化 GRUB 图形终端，带视频模式的gfxmode和gfxterm。你可以在 [GRUB#"No suitable mode found" error](/index.php/GRUB#.22No_suitable_mode_found.22_error "GRUB")的到这部分内容。此视频模式由GRUB通过“ gfxpayload '传递给Linux内核，为了有效果，任何视觉配置需要这种模式。

### 设置帧缓冲分辨率

#### 设定帧缓冲的分辨率

GRUB既可以为自己,也可以为内核设定帧缓冲.现在已经不使用老的`vga=`配置了.推荐方法是在`/etc/default/grub`进行如下编辑:

```
GRUB_GFXMODE=1024x768x32
GRUB_GFXPAYLOAD_LINUX=keep

```

运行以下命令使配置生效:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

`gfxpayload`属性会确保内核也保持这个分辨率

**Note:**

*   如果示例不起作用,请尝试用`vbemode="0x105"`代替`gfxmode="1024x768x32"`.请使用适合你屏幕的分辨率.
*   可以通过`# hwinfo --framebuffer`命令来显示所有可以使用的分辨率模式(hwinfo在[community](/index.php/Community "Community")里),在GRUB命令行下,可以使用`vbeinfo` 命令

这种方法不管用的话,可以试试老的`vga=`方法.将它添加到`"GRUB_CMDLINE_LINUX_DEFAULT="`里面就行了,比如 `"GRUB_CMDLINE_LINUX_DEFAULT="quiet splash vga=792"` 这会将系统的分辨率设定为1024*768

可以选择以下分辨率中的一种:`640×480`, `800×600`, `1024×768`, `1280×1024`, `1600×1200`, `1920×1200`

### 915resolution hack

有些时候,Intel显卡无法通过`# hwinfo --framebuffer` 或`vbeinfo`显示你需要的分辨率.这种情况下,你可以使用`915resolution hack`.915resolution hack会临时性的修改显卡BIOS来添加所需的分辨率.详情请参考[915resolution's home page](http://915resolution.mango-lang.org/)

首先,找一个你想要替代的视频模式.例如在GRUB命令行模式下运行:

 `sh:grub> 915resolution -l` 
```
Intel 800/900 Series VBIOS Hack : version 0.5.3
[...]
**Mode 30** : 640x480, 8 bits/pixel
[...]

```

然后,使用`1440x900` 分辨率覆盖`Mode 30`

 `/etc/grub.d/00_header` 
```
[...]
**915resolution 30 1440 900  # Inserted line**
set gfxmode=${GRUB_GFXMODE}
[...]

```

最后,设置`GRUB_GFXMODE`,重新生成GRUB配置文件,重启并测试是否生效:

```
# grub-mkconfig -o /boot/grub/grub.cfg
# reboot

```

### 背景图像和点阵字体

GRUB原生支持设置背景图像和点阵字体(以pf2格式).[grub](https://www.archlinux.org/packages/?name=grub)包含unifont字体,名为`unicode.pf2`.(也有可能只包含名为`ascii.pf2`的ASCII字符字体)

GRUB支持的图像格式有tga,png,jpeg.所支持的最大图像分辨率跟硬件有关.

Make sure you have set up the proper [framebuffer resolution](#Setting_the_framebuffer_resolution). 请确保你已经设定了合适的[帧缓冲分辨率](#.E8.AE.BE.E5.AE.9A.E5.B8.A7.E7.BC.93.E5.86.B2.E7.9A.84.E5.88.86.E8.BE.A8.E7.8E.87)

编辑`/etc/default/grub`:

```
GRUB_BACKGROUND="/boot/grub/myimage"
#GRUB_THEME="/path/to/gfxtheme"
GRUB_FONT="/path/to/font.pf2"

```

**Note:** 如果你将GRUB安装在单独的分区上, `/boot/grub/myimage` 应该改为 `/grub/myimage`.

重新生成配置文件:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

如果成功的添加了背景图片,那么用户会在命令行中看到`"Found background image..."`. 如果没有看到`"Found background image..."`,图像信息就可能没有嵌入`grub.cfg`中了.

如果图像没有正确显示,执行如下检查:

*   在`/etc/default/grub`里,图像的路径和名字是否正确
*   图像的大小和格式是否合适(tga,png,8-bit jpg)
*   图像是不是以RGB模式存储,是不是没有索引
*   `/etc/default/grub`里面是不是没有开启console模式
*   是否执行`grub-mkconfig`以重新生成配置文件

### Theme

下面的例子将展示如何使用GRUB包重的starfield主题:

编辑 `/etc/default/grub`

```
GRUB_THEME="/usr/share/grub/themes/starfield/theme.txt"

```

重生成配置:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

配置成功的话,在重生成配置过程中,会出现`Found theme: /usr/share/grub/themes/starfield/theme.txt`.使用主题就不会使用之前的背景图像

### 菜单颜色

GRUB支持设置菜单颜色.可使用的颜色能从[the GRUB Manual](https://www.gnu.org/software/grub/manual/html_node/Theme-file-format.html)里面找到.示例如下:

编辑`/etc/default/grub`:

```
GRUB_COLOR_NORMAL="light-blue/black"
GRUB_COLOR_HIGHLIGHT="light-cyan/blue"

```

重建配置档:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

### 隐藏菜单

GRUB特性之一就是支持隐藏/跳过目录,同时支持按`Esc`来打断隐藏/跳过.同时还支持设置是否显示timeout计时器 下面的例子设置5s钟内没有按Esc键就启动默认的启动项,并且在屏幕上显示倒计时:

编辑`/etc/default/grub`:

```
GRUB_HIDDEN_TIMEOUT=5
GRUB_HIDDEN_TIMEOUT_QUIET=false

```

重建配置档:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

### 禁用framebuffer

使用NVIDIA私有驱动的用户可能希望禁用GRUB的framebuffer,因为会导致驱动错误.

在`/etc/default/grub`中添加(如果已经有背注释掉的这行,就取消注释):

```
GRUB_TERMINAL_OUTPUT=console

```

重建配置档:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

如果你想保留GRUB的framebuffer,解决方法是在GRUB载入内核前进入文字模式.可以通过在`/etc/default/grub`设置如下:

```
GRUB_GFXPAYLOAD_LINUX=text

```

然后重建配置档.

## Booting ISO9660 image file directly via GRUB

GRUB supports booting from ISO images directly via loopback devices, see [Multiboot USB drive#Using GRUB and loopback devices](/index.php/Multiboot_USB_drive#Using_GRUB_and_loopback_devices "Multiboot USB drive") for examples.

## 持久块设备命名法

[持久块设备命名法](/index.php/Persistent_block_device_naming "Persistent block device naming")(Persistent block device naming)的一个目的是使用全局的UUID来区分分区,而不是用老的`/dev/sd*`表示法.好处显而易见.

GRUB默认使用持久块设备命名法

**Note:** 每次文件系统调整过后,就需要用新的UUID来更新`/boot/grub.cfg`.通过Live-CD调整分区和文件系统后要特别注意这点

是否使用UUID由`/etc/default/grub`里的这个选项控制:

```
# GRUB_DISABLE_LINUX_UUID=true

```

无论如何,变更配置后请重建配置档:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

## 使用卷标

GRUB支持以卷标识别文件系统(通过`search`命令的`--label参数`).

首先,给文件系统设置一个卷标:

```
# tune2fs -L *LABEL* *PARTITION*

```

然后在启动项中使用这个卷标:

```
menuentry "Arch Linux, session texte" {
  search --label --set=root archroot
  linux /boot/vmlinuz-linux root=/dev/disk/by-label/archroot ro
  initrd /boot/initramfs-linux.img
}

```

## 用密码保护 GRUB 菜单

如果你想禁止其他人改变启动参数或者使用GRUB命令行,可以给GRUB配置添加用户名/密码. 运行 `grub-mkpasswd-pbkdf2`,输入密码:

 `grub-mkpasswd-pbkdf2` 
```
[...]
Your PBKDF2 is grub.pbkdf2.sha512.10000.C8ABD3E93C4DFC83138B0C7A3D719BC650E6234310DA069E6FDB0DD4156313DA3D0D9BFFC2846C21D5A2DDA515114CF6378F8A064C94198D0618E70D23717E82.509BFA8A4217EAD0B33C87432524C0B6B64B34FBAD22D3E6E6874D9B101996C5F98AB1746FE7C7199147ECF4ABD8661C222EEEDB7D14A843261FFF2C07B1269A

```

然后将下面的内容添加到`/etc/grub.d/00_header`:

 `/etc/grub.d/00_header` 
```
cat << EOF

set superusers="**username**"
password_pbkdf2 **username** **<password>**

EOF

```

**Note:** 不能直接将

set superusers="**username**" password_pbkdf2 **username** **<password>** 添加到/etc/grub.d/00_header中去,而必须使用上述方法.否则会报错 password_pbkdf2: not found

`<password>`是`grub-mkpasswd_pbkdf2`生成的那个加密过后密码.

然后重建配置档.其他用户没有密码就不能变更GRUB配置或者使用GRUB命令行了.

可以参考[the GRUB manual](https://www.gnu.org/software/grub/manual/grub.html#Security)中的"Security"部分来进行更多的客制化安全设定

## 启动时隐藏GRUB界面,除非按着SHIFT键

为了获取更快的启动速度,而不用等GRUB倒计时,可以命令GRUB在启动时隐藏目录,除非SHIFT被按着. 将如下行添加到`/etc/default/grub`:

```
 GRUB_FORCE_HIDDEN_MENU="true"

```
 `/etc/grub.d/31_hold_shift` 
```
#! /bin/sh
set -e

# grub-mkconfig helper script.
# Copyright (C) 2006,2007,2008,2009  Free Software Foundation, Inc.
#
# GRUB is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# GRUB is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with GRUB.  If not, see <http://www.gnu.org/licenses/>.

prefix="/usr"
exec_prefix="${prefix}"
datarootdir="${prefix}/share"

export TEXTDOMAIN=grub
export TEXTDOMAINDIR="${datarootdir}/locale"
source "${datarootdir}/grub/grub-mkconfig_lib"

found_other_os=

make_timeout () {

  if [ "x${GRUB_FORCE_HIDDEN_MENU}" = "xtrue" ] ; then 
    if [ "x${1}" != "x" ] ; then
      if [ "x${GRUB_HIDDEN_TIMEOUT_QUIET}" = "xtrue" ] ; then
    verbose=
      else
    verbose=" --verbose"
      fi

      if [ "x${1}" = "x0" ] ; then
    cat <<EOF
if [ "x\${timeout}" != "x-1" ]; then
  if keystatus; then
    if keystatus --shift; then
      set timeout=-1
    else
      set timeout=0
    fi
  else
    if sleep$verbose --interruptible 3 ; then
      set timeout=0
    fi
  fi
fi
EOF
      else
    cat << EOF
if [ "x\${timeout}" != "x-1" ]; then
  if sleep$verbose --interruptible ${GRUB_HIDDEN_TIMEOUT} ; then
    set timeout=0
  fi
fi
EOF
      fi
    fi
  fi
}

adjust_timeout () {
  if [ "x$GRUB_BUTTON_CMOS_ADDRESS" != "x" ]; then
    cat <<EOF
if cmostest $GRUB_BUTTON_CMOS_ADDRESS ; then
EOF
    make_timeout "${GRUB_HIDDEN_TIMEOUT_BUTTON}" "${GRUB_TIMEOUT_BUTTON}"
    echo else
    make_timeout "${GRUB_HIDDEN_TIMEOUT}" "${GRUB_TIMEOUT}"
    echo fi
  else
    make_timeout "${GRUB_HIDDEN_TIMEOUT}" "${GRUB_TIMEOUT}"
  fi
}

  adjust_timeout

    cat <<EOF
if [ "x\${timeout}" != "x-1" ]; then
  if keystatus; then
    if keystatus --shift; then
      set timeout=-1
    else
      set timeout=0
    fi
  else
    if sleep$verbose --interruptible 3 ; then
      set timeout=0
    fi
  fi
fi
EOF

```

## 使用 UUID 和基础脚本

如果你想要使用UUID来避免不可靠的BIOS设备命名或者正在研究GRUB语法,这里有个使用UUID的示例性的启动项配置脚本.如果你想要将其移植到自己的系统上,只需要修改UUID就行了.这个例子假设系统的boot和root文件系统是在不同的分区上.如果你还有其他分区,请做相应修改.

```
menuentry "Arch Linux 64" {
    # Set the UUIDs for your boot and root partition respectively
    set the_boot_uuid=ece0448f-bb08-486d-9864-ac3271bd8d07
    set the_root_uuid=c55da16f-e2af-4603-9e0b-03f5f565ec4a

    # (Note: This may be the same as your boot partition)

    # Get the boot/root devices and set them in the root and grub_boot variables
    search --fs-uuid $the_root_uuid --set=root
    search --fs-uuid $the_boot_uuid --set=grub_boot

    # Check to see if boot and root are equal.
    # If they are, then append /boot to $grub_boot (Since $grub_boot is actually the root partition)
    if [ $the_boot_uuid == $the_root_uuid ] ; then
        set grub_boot=($grub_boot)/boot
    else
        set grub_boot=($grub_boot)
    fi

    # $grub_boot now points to the correct location, so the following will properly find the kernel and initrd
    linux $grub_boot/vmlinuz-linux root=/dev/disk/by-uuid/$the_root_uuid ro
    initrd $grub_boot/initramfs-linux.img
}

```

## 手动创建 grub.cfg

**Warning:** *不推荐*编辑这个文件.这个文件由`grub-mkconfig`生成,最好编辑`/etc/default/grub`和`/etc/grub.d`文件夹下的脚本以实现修改.

基本的GRUB配置文件使用如下选项:

*   `(hd*X*,*Y*)` 是*X*磁盘的*Y*分区,分区从1开始计数,磁盘从0开始计数.
*   `set default=*N*`设定用户选择超时时间过后的默认启动项
*   `set timeout=*M*`设定用户选择超时时间(秒).
*   `menuentry "title" {entry options}`设置一个名为`title`的启动项
*   `set root=(hd*X*,*Y*)`设定启动分区(kernel和GRUB模组所在磁盘),/boot没被要求独占一个分区,有可能就是root分区下的一个文件夹

示例配置如下:

 `/boot/grub/grub.cfg` 
```
# Config file for GRUB - The GNU GRand Unified Bootloader
# /boot/grub/grub.cfg

# DEVICE NAME CONVERSIONS
#
#  Linux           Grub
# -------------------------
#  /dev/fd0        (fd0)
#  /dev/sda        (hd0)
#  /dev/sdb2       (hd1,2)
#  /dev/sda3       (hd0,3)
#

# Timeout for menu
set timeout=5

# Set default boot entry as Entry 0
set default=0

# (0) Arch Linux
menuentry "Arch Linux" {
  set root=(hd0,1)
  linux /vmlinuz-linux root=/dev/sda3 ro
  initrd /initramfs-linux.img
}

## (1) Windows
#menuentry "Windows" {
#  set root=(hd0,3)
#  chainloader +1
#}

```

## Multiple entries

### Disable submenu

If you have multiple kernels installed, say linux and linux-lts, by default `grub-mkconfig` groups them in a submenu. If you do not like this behaviour you can go back to one single menu by adding the following line to `/etc/default/grub`:

```
 GRUB_DISABLE_SUBMENU=y

```

### 调用之前的启动项

GRUB能够记住你当前使用的启动项并且在下次启动时将其作为默认项.当你使用多个内核或操作系统时,这个特性很有用. 编辑`/etc/default/grub`中的`GRUB_DEFAULT`选项:

```
GRUB_DEFAULT=saved

```

上面的命令会告诉GRUB使用记住的启动项为默认启动项. 将下面的行添加到`/etc/default/grub`会让GRUB记住当前的启动项:

```
GRUB_SAVEDEFAULT=true

```

**Note:** 手动添加启动项到`/etc/grub.d/40_custom`或`/boot/grub/custom.cfg`中,比如Windows启动项,需要添加`savedefault`

### Changing the default menu entry

可以通过修改`/etc/default/grub`中的`GRUB_DEFAULT`值来改变默认启动项

```
GRUB_DEFAULT=0

```

GRUB启动项序号从0开始计数.0代表第一个启动项.

除了使用启动项序号,也可以使用启动项名:

```
GRUB_DEFAULT='Arch Linux, with Linux core repo kernel'

```

### 设定下次启动的启动项(一次性,非持久)

命令`grub-reboot`可以设置下次启动时启动哪个启动项而不必修改配置文件或者在启动时手动选择.这个设置是一次性的,即不会改变GRUB的默认启动项.

**Note:** 需要在`/etc/default/grub`中设定 `GRUB_DEFAULT=saved`,然后重建配置档.在手动生成的 `grub.cfg`中, 使用 `set default="${saved_entry}"`.

## UEFI 延伸阅读

下面是关于通过 UEFI 安装 Arch 的相关信息。

### 其他方法

通常，不管 EFI 系统分区是否挂载，GRUB 都会将所有文件放到 `/boot`。

如果你想将所有的文件放在 ESP 中,请给grub-install命令添加 `--boot-directory=*esp*` 选项:

```
# grub-install --target=x86_64-efi --efi-directory=*esp* --bootloader-id=grub --boot-directory=*esp* --debug

```

这个命令会将 GRUB 文件放在 {{ic|*esp*/grub} 而不是 `/boot/grub` 中. 使用这个方法, 请确保 grub-mkconfig 设置了正确的目录:

```
# grub-mkconfig -o *esp*/grub/grub.cfg

```

配置档是一样的.

### 在固件启动管理器中创建GRUB条目

`grub-install`会自动尝试在启动管理器中创建GRUB条目.如果没有成功,请参考,里面有关于使用`efibootmgr`创建启动目录条目的介绍.一般来说,这个问题都是因为你没有以UEFI模式启动CD/USB造成的.请参考[UEFI#Create UEFI bootable USB from ISO](/index.php/UEFI#Create_UEFI_bootable_USB_from_ISO "UEFI").

### 创建GRUB Standalone模式的UEFI应用程序

可以建立一个`grubx64_standalone.efi`,这个应用将所有的模组嵌入自身的memdisk中,所以就不需要使用单独的目录来存放GRUB UEFI模组和其他相关文件了,使用[grub](https://www.archlinux.org/packages/?name=grub)包里的`grub-mkstandalone`可以实现这个功能.

最简单的的方法就是使用`grub-mkstandalone`,不过,我们还可以指定嵌入哪些模组:

```
# grub-mkstandalone --directory="/usr/lib/grub/x86_64-efi/" --format="x86_64-efi" --compression="xz" \
--output="$esp/EFI/grub/grubx64_standalone.efi" <你想嵌入的模组>

```

`grubx64_standalone.efi`文件要求将`grub.cfg`放置到`(memdisk)/boot/grub`中,而这个memdisk是嵌入到EFI应用当中的.`grub-mkstandlone`脚本允许传递将要嵌入memdisk的文件列表.(上面命令里的"<你想嵌入的模组>")

如果你的`grub.cfg`的路径是`/home/user/Desktop/grub.cfg`,那么需要创建一个临时的`/home/user/Desktop/boot/grub/`目录,然后将grub.cfg复制到其中并进入这个目录并运行:

```
# grub-mkstandalone --directory="/usr/lib/grub/x86_64-efi/" --format="x86_64-efi" --compression="xz" \
--output="$esp/EFI/grub/grubx64_standalone.efi" "boot/grub/grub.cfg"

```

进入`/home/user/Desktop/boot/grub/`但是传递`boot/grub/grub.cfg`参数(请注意是`boot/`而不是`/boot/`)的原因是`grub-mkstandalone`会自动将boot/grub/grub.cfg处理为`/(memdisk)/boot/grub/grub.cfg`

如果你传递`/home/user/Desktop/grub.cfg`,那么处理后的结果会是`(memdisk)/home/user/Desktop/grub.cfg`.如果传递`/home/user/Desktop/boot/grub/grub.cfg`,那么结果就是`(memdisk)/home/user/Desktop/boot/grub/grub.cfg`.所以需要进入`/home/user/Desktop/boot/grub/`并传递`boot/grub/grub.cfg`参数,因为这样才能生成`grub.efi`需要的`(memdisk)/boot/grub/grub.cfg`.

如果需要为`$esp/EFI/arch_grub/grubx64_standalone.efi`创建一个UEFI启动器条目,使用`efibootmgr`.[#Create GRUB entry in the Firmware Boot Manager](#Create_GRUB_entry_in_the_Firmware_Boot_Manager)里有介绍

### Technical information

The GRUB EFI file always expects its config file to be at `${prefix}/grub.cfg`. However in the standalone GRUB EFI file, the `${prefix}` is located inside a tar archive and embedded inside the standalone GRUB EFI file itself (inside the GRUB environment, it is denoted by `"(memdisk)"`, without quotes). This tar archive contains all the files that would be stored normally at `/boot/grub` in case of a normal GRUB EFI install.

Due to this embedding of `/boot/grub` contents inside the standalone image itself, it does not rely on actual (external) `/boot/grub` for anything. Thus in case of standalone GRUB EFI file `${prefix}==(memdisk)/boot/grub` and the standalone GRUB EFI file reads expects the config file to be at `${prefix}/grub.cfg==(memdisk)/boot/grub/grub.cfg`.

Hence to make sure the standalone GRUB EFI file reads the external `grub.cfg` located in the same directory as the EFI file (inside the GRUB environment, it is denoted by `${cmdpath}` ), we create a simple `/tmp/grub.cfg` which instructs GRUB to use `${cmdpath}/grub.cfg` as its config (`configfile ${cmdpath}/grub.cfg` command in `(memdisk)/boot/grub/grub.cfg`). We then instruct grub-mkstandalone to copy this `/tmp/grub.cfg` file to `${prefix}/grub.cfg` (which is actually `(memdisk)/boot/grub/grub.cfg`) using the option `"boot/grub/grub.cfg=/tmp/grub.cfg"`.

This way, the standalone GRUB EFI file and actual `grub.cfg` can be stored in any directory inside the EFI System Partition (as long as they are in the same directory), thus making them portable.