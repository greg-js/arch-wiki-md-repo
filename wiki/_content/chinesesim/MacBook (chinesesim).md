在MacBook上安装Arch Linux与在其他电脑上安装Arch Linux非常相似。然而，由于MacBook的特殊硬件配置，需要一些特殊的考虑，因此建立MacBook专页。更多背景信息，可以从[官方安装指南](/index.php/Official_Arch_Linux_Install_Guide "Official Arch Linux Install Guide")以及[安装后小贴士](/index.php/Post_Installation_Tips "Post Installation Tips")上获取。本文同样适用于MacBook Pro系列机型，也支持32位及64位版本。如果您正在使用MacBook 5,2并且有其他疑问，请猛击[MacBook5,2](/index.php/Macbook5,2 "Macbook5,2")获取帮助。

## Contents

*   [1 概述](#.E6.A6.82.E8.BF.B0)
*   [2 安装 Mac OS X 以及固件更新](#.E5.AE.89.E8.A3.85_Mac_OS_X_.E4.BB.A5.E5.8F.8A.E5.9B.BA.E4.BB.B6.E6.9B.B4.E6.96.B0)
*   [3 分区](#.E5.88.86.E5.8C.BA)
    *   [3.1 仅安装Arch Linux](#.E4.BB.85.E5.AE.89.E8.A3.85Arch_Linux)
    *   [3.2 Mac OS X与Arch Linux共存](#Mac_OS_X.E4.B8.8EArch_Linux.E5.85.B1.E5.AD.98)
*   [4 从GRUB直接启动](#.E4.BB.8EGRUB.E7.9B.B4.E6.8E.A5.E5.90.AF.E5.8A.A8)
    *   [4.1 编译](#.E7.BC.96.E8.AF.91)
    *   [4.2 grub.cfg示例](#grub.cfg.E7.A4.BA.E4.BE.8B)
*   [5 安装](#.E5.AE.89.E8.A3.85)
*   [6 安装后配置](#.E5.AE.89.E8.A3.85.E5.90.8E.E9.85.8D.E7.BD.AE)
    *   [6.1 Xorg](#Xorg)
        *   [6.1.1 视频](#.E8.A7.86.E9.A2.91)
            *   [6.1.1.1 NVIDIA注意](#NVIDIA.E6.B3.A8.E6.84.8F)
            *   [6.1.1.2 MacBook 6,2+-EFI](#MacBook_6.2C2.2B-EFI)
        *   [6.1.2 触摸板](#.E8.A7.A6.E6.91.B8.E6.9D.BF)
        *   [6.1.3 键盘](#.E9.94.AE.E7.9B.98)
            *   [6.1.3.1 NVIDIA配置](#NVIDIA.E9.85.8D.E7.BD.AE)
    *   [6.2 Wi-Fi](#Wi-Fi)
    *   [6.3 电源管理](#.E7.94.B5.E6.BA.90.E7.AE.A1.E7.90.86)
        *   [6.3.1 笔记本模式工具](#.E7.AC.94.E8.AE.B0.E6.9C.AC.E6.A8.A1.E5.BC.8F.E5.B7.A5.E5.85.B7)
        *   [6.3.2 睡眠（内核挂起）](#.E7.9D.A1.E7.9C.A0.EF.BC.88.E5.86.85.E6.A0.B8.E6.8C.82.E8.B5.B7.EF.BC.89)
        *   [6.3.3 休眠](#.E4.BC.91.E7.9C.A0)
    *   [6.4 声音配置](#.E5.A3.B0.E9.9F.B3.E9.85.8D.E7.BD.AE)
    *   [6.5 蓝牙](#.E8.93.9D.E7.89.99)
    *   [6.6 iSight配置](#iSight.E9.85.8D.E7.BD.AE)
    *   [6.7 温度感应](#.E6.B8.A9.E5.BA.A6.E6.84.9F.E5.BA.94)
    *   [6.8 色彩配置](#.E8.89.B2.E5.BD.A9.E9.85.8D.E7.BD.AE)
    *   [6.9 苹果远程控制](#.E8.8B.B9.E6.9E.9C.E8.BF.9C.E7.A8.8B.E6.8E.A7.E5.88.B6)
    *   [6.10 HFS分区共享](#HFS.E5.88.86.E5.8C.BA.E5.85.B1.E4.BA.AB)
    *   [6.11 HFS+ 分区](#HFS.2B_.E5.88.86.E5.8C.BA)
    *   [6.12 Home目录共享](#Home.E7.9B.AE.E5.BD.95.E5.85.B1.E4.BA.AB)
        *   [6.12.1 在OS X中](#.E5.9C.A8OS_X.E4.B8.AD)
            *   [6.12.1.1 第一步：改变UID与GID](#.E7.AC.AC.E4.B8.80.E6.AD.A5.EF.BC.9A.E6.94.B9.E5.8F.98UID.E4.B8.8EGID)
            *   [6.12.1.2 第二步：改变Home目录权限](#.E7.AC.AC.E4.BA.8C.E6.AD.A5.EF.BC.9A.E6.94.B9.E5.8F.98Home.E7.9B.AE.E5.BD.95.E6.9D.83.E9.99.90)
        *   [6.12.2 在Arch中](#.E5.9C.A8Arch.E4.B8.AD)
    *   [6.13 避免GRUB启动前EFI长时间执行](#.E9.81.BF.E5.85.8DGRUB.E5.90.AF.E5.8A.A8.E5.89.8DEFI.E9.95.BF.E6.97.B6.E9.97.B4.E6.89.A7.E8.A1.8C)
    *   [6.14 关闭启动响铃](#.E5.85.B3.E9.97.AD.E5.90.AF.E5.8A.A8.E5.93.8D.E9.93.83)
*   [7 rEFIt](#rEFIt)
    *   [7.1 rEFIt可能会遇到的问题](#rEFIt.E5.8F.AF.E8.83.BD.E4.BC.9A.E9.81.87.E5.88.B0.E7.9A.84.E9.97.AE.E9.A2.98)
*   [8 参考资料](#.E5.8F.82.E8.80.83.E8.B5.84.E6.96.99)
*   [9 MacBook Air (4,2) 内核补丁](#MacBook_Air_.284.2C2.29_.E5.86.85.E6.A0.B8.E8.A1.A5.E4.B8.81)

## 概述

在MacBook上安装Arch Linux可以分为一下几个步骤

1.  **[安装Mac OS X](#.E5.AE.89.E8.A3.85_Mac_OS_X_.E4.BB.A5.E5.8F.8A.E5.9B.BA.E4.BB.B6.E6.9B.B4.E6.96.B0)**：忽略安装过程最后的配置，此处将从一个新安装的OS X开始。
2.  **[固件更新](#.E5.AE.89.E8.A3.85_Mac_OS_X_.E4.BB.A5.E5.8F.8A.E5.9B.BA.E4.BB.B6.E6.9B.B4.E6.96.B0)**：这将有助于减少错误以及提供硬件的新特性。
3.  **[分区](#.E5.88.86.E5.8C.BA)**：这步中可以调整OS X分区大小或删除分区并为Arch Linux建立分区。
4.  **[安装Arch Linux](#.E5.AE.89.E8.A3.85)**：真正安装Arch Linux的过程。
5.  **[安装后配置](#.E5.AE.89.E8.A3.85.E5.90.8E.E9.85.8D.E7.BD.AE)**：针对MacBook的特殊配置。

**Tip:** rEFIt是EFI固件电脑上很流行的一个启动器，包括了Mac电脑。它能够在系统安装过程中的任何时候安装，更多信息请猛击[rEFIt](/index.php/MacBook#rEFIt "MacBook")

## 安装 Mac OS X 以及固件更新

[Apple](http://www.apple.com/)已经提供了详尽的安装Mac OS X的教程。按照此教程安装好OS X后，点击菜单：

```
苹果图标 --> 软件升级

```

来更新所有软件。更新完成之后，您需要重启电脑。重启后请再次检查软件升级以确保所有软件都更新到了最新版。

**Note:** 有时软件更新不会对您电脑的所有固件进行更新，然而，您可以在苹果支持网站中自己搜索这些升级。

如果您不打算安装Mac OS X，请为这些文件做好备份：

```
/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBVideoSupport.kext/Contents/MacOS/AppleUSBVideoSupport

```

这个文件将在后期调试iSight时用到。同样的，请备份色彩配置

```
/Library/ColorSync/Profiles/Displays/<此处的文件>

```

在调试[色彩配置](#.E8.89.B2.E5.BD.A9.E9.85.8D.E7.BD.AE)时会用到。

## 分区

下一步就是将硬盘重新分区。如果Mac OS X按照一般流程安装，那么您的硬盘将是GPT格式分区表，会有以下两个分区：

*   **EFI分区**：一个大小有200MB的分区，在磁盘开始部分。有些分区工具会将其读作FAT分区，通常标为*#1*
*   **Mac OS X分区**：这个分区*(HFS+)*一般是占用了硬盘的所有其他空间。通常标为*#2*

分区策略依据您想安装多少操作系统而定，有如下两个选项：

*   [仅安装Arch Linux](#.E4.BB.85.E5.AE.89.E8.A3.85Arch_Linux)单系统。
*   [Mac OS X与Arch Linux共存](#Mac_OS_X.E4.B8.8EArch_Linux.E5.85.B1.E5.AD.98)双系统。

如果您不知道改选哪种方式，我们建议您选择双系统，这样您可以在任何时候回到Mac OS X。

### 仅安装Arch Linux

这种情况最好办。大多数情况下，分区操作与将Arch Linux安装在其他硬件上没两样。 唯一的不同点在于MacBook的启动响铃。为了确保启动响铃是关闭的，请提前在Mac OS X系统中就将音量调至静音。MacBook固件依赖于Mac OS X的配置。请注意，如果你选择去掉Mac OS X的分区，除了用另外一块硬盘来加载OS X进行设置固件外没有其他任何办法。

这之后可以使用parted来进行分区操作。最简单的办法是将分区表转为msdos格式，然后和平常一样来进行分区。GRUB不能认出GPT格式的分区表。

**Note:** 用parted对硬盘分区只需要用从Arch Linux core install disk启动，然后以root权限打开parted程序。此操作可在安装前完成。

完成这一步骤之后，可以查看[安装](#.E5.AE.89.E8.A3.85)部分。

### Mac OS X与Arch Linux共存

让Mac OS X与Arch Linux共存的最简单的分区方法是用Mac OS X的分区工具后用Arch Linux的工具完善。

**Warning:** 这种方法最好只在新安装的OS X中尝试，在一个预安装的OS X中可能发生不可预料的结果。

过程：

*   在Mac OS X中，运行磁盘工具

*   在左侧栏，选择硬盘，请注意，是选择硬盘，而不是分区。点击右侧的分区标签。

*   选择要重置大小的分区。

*   确定你要给你的Mac OS X分区留多少空间，以及留多少空间给Arch Linux。记住一个Mac OS X大约需要15至20GB的空间，请留足空间以方便日后安装软件。

*   最后，设置Mac OS X分区的大小，然后在空白区域创建一个分区。

**Note:** 如果你希望在Mac OS X与Arch Linux之间共享一个分区，那么需要做些额外的操作，具体操作可以参照此处[分区共享](#HFS.E5.88.86.E5.8C.BA.E5.85.B1.E4.BA.AB)

*   上述操作顺利完成后就可以进入下一步了，否则，请一定在Mac OS X上解决这些问题。

*   按住ALT键来从Arch Linux启动光盘启动。

*   现在，运行parted来完成后续操作。

```
# parted

```

*   删除空分区。你可以随意按照你的想法设置这个分区。请注意MBR是必须装在4个主分区上的，包括了EFI预留分区。也就是留下了2个主分区给Arch Linux。一种分区策略是分配一个根分区和一个Home分区，然后swap可以使用文件。要不然就是分配一个分区用于共享。下面会有详细说明。

*   此时，如果你需要多系统启动，你需要重启电脑，用rEFIt来修复磁盘上的分区表。如果你这样干，那您会需要重装GRUB来是Mac系统认出Linux分区。当你进入rEFIt菜单后，选择更新分区表，然后按Y

```
# reboot

```

*   完成了，可以继续安装过程了。

## 从GRUB直接启动

在efi上直接启动GRUB2而不用rEFIt是可以的。一下的操作在MacBook7,1上是可行的。建议将GRUB安装在fat32或者HFS+分区上，ext2或者ext3应该也行。GRUB的苹果加载命令在7,1上还暂时不能使用，但可以用过下面的补丁实现[补丁地址](https://savannah.gnu.org/bugs/index.php?33185)。

GRUB装上硬盘分区后，固件需要知道从哪儿启动它。这步操作可以在OS X或者OS X安装光盘。下面的命令指明了GRUB是安装在OS X系统的/efi/grub中

```
sudo bless --folder /efi/grub --file /efi/grub/grub.efi

```

### 编译

有些型号可能需要将EFI_ARCH设置成i386。

```
bzr branch --revision -2 bzr://bzr.savannah.gnu.org/grub/trunk/grub grub
cd grub
./autogen.sh
patch -p1 < appleloader_macbook_7_1.patch
export EFI_ARCH=x86_64
./configure --with-platform=efi --target=${EFI_ARCH} --program-prefix=""
make
cd grub-core
../grub-mkimage -O ${EFI_ARCH}-efi -d . -o grub.efi -p "" part_gpt part_msdos ntfs ntfscomp hfsplus fat ext2 normal chain boot configfile linux multiboot
cp grub.efi *.mod *.lst yourinstalllocation

```

### grub.cfg示例

此处应该有更好的方法来加载Windows系统。

```
set debug=video
insmod efi_gop

menuentry "Arch Linux EFI" {
  set root=(hd0,3)
  #search --set -f /boot/vmlinuz-linux-efi-physical
  #loadbios /boot/vbtrace_bios.bin /boot/int10.bin
  linux /boot/vmlinuz-linux-efi-physical root=/dev/sda3 reboot=pci resume=/dev/sda3 resume_offset=151552
  initrd /boot/initramfs-linux-efi-physical.img
}

menuentry "MacOSX" {
  set root=(hd0,2)
  # Search the root device for Mac OS X's loader.
  #search --set -f /usr/standalone/i386/boot.efi
  # Load the loader.
  chainloader /usr/standalone/i386/boot.efi
}

menuentry "Windows 7" {
  appleloader HD
}

menuentry "Boot from CD" {
  appleloader CD
}

menuentry "Boot from USB" {
  appleloader USB
}

```

## 安装

**Note:** 本部分安装过程只是用于Mac OS X与Arch Linux共存的情况，如果你只想单独使用Arch Linux，可以按照官方安装指南，然后跳到[安装后配置](#.E5.AE.89.E8.A3.85.E5.90.8E.E9.85.8D.E7.BD.AE)

*   从Arch Linux安装光盘启动

**Note:** 有些MacBook用户反映键盘不能正确响应，那就按照下面的参数来启动光盘。

**Note:** 截止2011年4月30日，MacBook7,1不能从普通的iso镜像启动，但最新的[archboot](/index.php/Archboot "Archboot")应该有用。

```
boot: arch noapic irqpoll acpi=force

```

*   以root登陆

*   打开Arch Linux安装程序

```
/arch/setup

```

*   按照[官方安装文档](/index.php/Installation_guide "Installation guide")中说明的过程来做，但是在下面几个部分中请留意：
    *   在[准备磁盘](/index.php/Installation_guide#Prepare_Hard_Drive "Installation guide")部分，只要做设置磁盘挂在这步，注意要设对磁盘挂载点。
    *   在[安装启动器](/index.php/Installation_guide#Install_a_boot_loader "Installation guide")部分，编辑menu.lst文件，添加**reboot=pci**到**kernel**行的末尾，例如下面这行： `kernel /vmlinuz-linux root=/dev/sda5 ro reboot=pci` 这样你的MacBook才能从Arch Linux正常重启
    *   还是在[安装启动器](/index.php/Installation_guide#Install_a_boot_loader "Installation guide")部分，将GRUB安装至`/boot`所在的分区。
        **Warning:** 别把GRUB安装到*/dev/sda*这样的地方！！！这样做会造成系统不稳定。

    *   在[配置系统](/index.php/Installation_guide#Configure_the_system "Installation guide")部分，编辑 /etc/mkinitcpio.conf，添加**usbinput**到**HOOKS**行的**autodetect**之后。这样才能在Arch Linux启动之前加载键盘驱动

*   安装完成之后就可以重启系统了。

```
# reboot

```

*   把Arch Linux安装光盘从光驱中退出。

## 安装后配置

### Xorg

按照[Xorg](/index.php/Xorg "Xorg")来安装Xorg。

#### 视频

不同的MacBook有不同型号的显卡，可以通过下面命令来查看显卡种类

```
$ lspci | grep VGA

```

*   如果返回的字符串中包含**intel**，那你只需要安装**xf86-video-intel**驱动，用如下命令：

```
# pacman -S xf86-video-intel

```

*   如果返回的是nVidia，可以参看[NVIDIA](/index.php/NVIDIA "NVIDIA")

*   如果返回ATI或者AMD，参见[ATI](/index.php/ATI "ATI")

##### NVIDIA注意

**Tip:** MacBookPro 6,2 - 使用合适的[NVIDIA](/index.php/NVIDIA "NVIDIA")驱动，在使用[Pure Video HD](/index.php/NVIDIA#Pure_Video_HD_.28VDPAU.2FVAAPI.29 "NVIDIA")之后支持硬件视频解码。

对于使用NVIDIA显卡的MacBook，背景亮度可以通过[AUR](/index.php/AUR "AUR")中的[nvidia-bl](https://aur.archlinux.org/packages/nvidia-bl/)包解决。

##### MacBook 6,2+-EFI

截至2011年4月30日，nvidia驱动在此类EFI型号的机子下不能正常工作。可以了解一下[mesa-git](https://aur.archlinux.org/packages/mesa-git/PKGBUILD)这个包。

#### 触摸板

触摸板应该已经有了基本的功能。可以安装AUR中的[xf86-input-multitouch-git](https://aur.archlinux.org/packages/xf86-input-multitouch-git/)包来达到和Mac OS X类似的多点触控效果，最多支持三点触控，包含了三指水平与垂直滑动。可以从[项目主页](http://bitmath.org/code/multitouch/) 获取更多消息。

xf86-input-multitouch-git除了编辑源代码外不支持配置。一些用户也正面临这从palm上得到错误的点击。现在有个可定制度更高的包[xf86-input-mtrack-git](https://aur.archlinux.org/packages/xf86-input-mtrack-git/)。在其[readme](https://github.com/BlueDragonX/xf86-input-mtrack)中能得到更多配置信息。

下面的配置在MacBook 7,1中正常工作

```
 Option "Thumbsize" "50"
 Option "ScrollDistance" "100"

```

可能你还需要添加下面的内容

```
MatchDevicePath "/dev/input/event10"

```

在更旧的MacBook机型上，比如MacBook 2,1中，可能需要安装xf86-input-synaptics包才能正常工作。可以查看[Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")获取更多信息。

#### 键盘

MacBook的键盘默认是能正常工作的。如果想切换fn键，可以查看[Apple Keyboard](/index.php/Apple_Keyboard "Apple Keyboard")。

可以通过**xbindkeys**来重新设置键，或者通过DE配置。有另一种很好的方法，安装[pommed](https://aur.archlinux.org/packages/pommed/)

根据你MacBook的硬件来配置**/etc/pommed.conf**，可以以**/etc/pommed.conf.mac**或者**/etc/pommed.conf.ppc**为模板来建立这个配置。

##### NVIDIA配置

如果在使用 pommed 后亮度仍然不正常， 请确认你安装了 [nvidia-bl](https://aur.archlinux.org/packages/nvidia-bl/) 并添加以下命令：

```
find . -name "*" -exec sed -i 's/mbp_backlight/nvidia_backlight/' '{}' \;

```

到 pommed PKGBUILD build() 函数中，然后重新编译。引用自 [this forum post](https://bbs.archlinux.org/viewtopic.php?id=105091).

另一个解决方案是修改 pommed PKGBUILD build():

```
find . -name "*" -exec sed -i 's/nvidia_backlight/apple_backlight/' '{}' \;

```

如果上面两种方法都不能解决，那么你需要尝试以下方法：

运行 nvidia-settings，编辑 '/etc/X11/xorg.conf' 添加以下代码到 Device 部分：

```
Option "RegistryDwords" "EnableBrightnessControl=1"

```

保存并重启，检查亮度调节是否正常工作。 点击查看更多信息 [Ubuntu MacBookPro5,5](https://help.ubuntu.com/community/MacBookPro5-5/Precise#LCD)

### Wi-Fi

不同型号的MacBook使用不同的网卡模块。

使用以下命令查看你的Macbook使用的网卡型号：

```
# lspci | grep Network

```

*   如果你使用的是 Atheros，无需任何设定即可正常工作。

*   如果你使用的是 Broadcom，请在 [Broadcom BCM4312](/index.php/Broadcom_BCM4312 "Broadcom BCM4312") 页面查看教程。

*   MacBook 5.0 和 6.0 使用 BCM43xx，在 [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") 页面查看有关 broadcom-wl 驱动的部分。 网络接口在重启后会互换，所以最好使用 udev 规则来定义它们（教程在 [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") 页面）。

*   MacBook 8.1 使用 BCM4331，即不被Linux支持 (3.0 和 3.1) ，Broadcom 也没有提供闭源驱动，直到在 Linux 3.2 中才被初步支持。如果你需要在旧的内核上使用，你需要安装这里的驱动[compat-drivers](https://backports.wiki.kernel.org/index.php/Documentation/compat-drivers)

**注意:** 如果你经常丢失连接，你需要关闭无线电源管理。 如果你在运行 [pm-utils](/index.php/Pm-utils "Pm-utils")，你需要创建一个执行文件文件 `/etc/pm/wireless` 替代无线电源管理：
```
#!/bin/sh
iwconfig wlp2s0 power off

```

### 电源管理

#### 笔记本模式工具

#### 睡眠（内核挂起）

#### 休眠

### 声音配置

### 蓝牙

### iSight配置

### 温度感应

### 色彩配置

### 苹果远程控制

### HFS分区共享

### HFS+ 分区

### Home目录共享

#### 在OS X中

##### 第一步：改变UID与GID

##### 第二步：改变Home目录权限

#### 在Arch中

### 避免GRUB启动前EFI长时间执行

### 关闭启动响铃

## rEFIt

**Note:** rEFIt只是在开机是给你提供OS X和Linux的启动菜单而已。如果没有这个需求的话，rEFIt不是必须的。

详情参考[refit myths](http://refit.sourceforge.net/myths/).

在OS X下，从[Refit主页](http://refit.sourceforge.net/)下载".dmg"格式的安装包，并像其他苹果软件一样安装。

**Note:** 如果你此前已经对磁盘分过区的话（比如准备安装ArchLinux之前的准备），那rEFIt默认是不启用的。你需要手动执行安装到系统路径/efi/refit/的"enable.sh"脚本

手动启用rEFIt的方法：

*   打开**终端**：
*   执行**cd /efi/refit; ./enable.sh**命令

### rEFIt可能会遇到的问题

如果你在安装Arch或者rEFIt后遇到了问题，特别是启动时在启动菜单中看不到启动项，或者出现下面的GRUB提示时：

```
GRUB>_

```

请您参考下 [http://mac.linux.be/content/problems-refit-and-grub-after-installation](http://mac.linux.be/content/problems-refit-and-grub-after-installation)

该页面将会教你如何启动的Arch系统，将有问题的Arch系统挂载上去，然后chroot进入该系统，通过gptsyc重新安装GRUB。文中提到的那些用于debian系统的命令基本上都可以在Arch上工作。不过注意不要将GRUB安装错地方了（wrong spot怎么翻译？）

你可从 [http://packages.debian.org/sid/gptsync](http://packages.debian.org/sid/gptsync) 获取到gptsync。 或者通过下面两个命令之一分别下载32/64位版本的：

```
wget http://ftp.us.debian.org/debian/pool/main/r/refit/gptsync_0.14-2_i386.deb
wget http://ftp.us.debian.org/debian/pool/main/r/refit/gptsync_0.14-2_amd64.deb

```

由于是.deb包，所以你可能需要先安装deb2targz

```
pacman -S deb2targz

```

## 参考资料

*   [http://www.netsoc.tcd.ie/~theorie/interblag/2010/01/30/installing-arch-linux-on-a-mac-pro/](http://www.netsoc.tcd.ie/~theorie/interblag/2010/01/30/installing-arch-linux-on-a-mac-pro/)
*   [http://allanmcrae.com/2010/04/installing-arch-on-a-macbook-pro-5-5/](http://allanmcrae.com/2010/04/installing-arch-on-a-macbook-pro-5-5/)
*   [http://linux-junky.blogspot.com/2011/08/triple-boot-archlinux-windows-7-and-mac.html](http://linux-junky.blogspot.com/2011/08/triple-boot-archlinux-windows-7-and-mac.html)

## MacBook Air (4,2) 内核补丁

Linus的内核树中的当前版本（Linux 3.0.7）中，包含几个问题。我（telmich）已经搜集了下面几个问题的修复补丁：

*   分辨率是1280x800而非正确的1440x900
*   触摸板不能正常工作或被检测为Synaptics
*   FN + F1～F12组合键不工作（例如：fn啥都干不了）
*   FN+F5～F12等多媒体键映射错误
*   网络处理的驱动/brcmsmac驱动（Hanging network applications / brcmsmac driver）

您可以从 [http://git.schottelius.org/?p=foreign/linux-macbook-air;a=summary](http://git.schottelius.org/?p=foreign/linux-macbook-air;a=summary) 获取到打好补丁的内核，其中包括如下分支：

1.  keith-jiri: Keith Packard提供的显卡驱动补丁、Jiri Kosina提供的FN功能键补丁
2.  keith-jiri-brcmsmac: 上面提到的补丁加上网络处理的驱动
3.  jiri-kbdmapping: FN功能键和映射关系修复补丁
4.  keith-jiri-kbdmapping: 第一个分支加上多媒体键补丁
5.  keith-jiri-kbdmapping-brcmsmac: 以上所有的集合 (**不确定的情况下，推荐使用这个分支**)

你可以很简单的用当前ArchLinux的配置文件来编译内核：

```
# 请先通过git检出对应分支的源代码!
cd linux-macbook-air

# 使用当前的配置作为基础
zcat /proc/config.gz > .config

# 编译内核时，可能会询问几个未配置的选项
make -j5

```