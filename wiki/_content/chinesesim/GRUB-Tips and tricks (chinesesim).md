**翻译状态：** 本文是英文页面 [GRUB/Tips and tricks](/index.php/GRUB/Tips_and_tricks "GRUB/Tips and tricks") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-06-12，点击[这里](https://wiki.archlinux.org/index.php?title=GRUB%2FTips+and+tricks&diff=0&oldid=573028)可以查看翻译后英文页面的改动。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 其它安装方式](#其它安装方式)
    *   [1.1 安装到 U 盘](#安装到_U_盘)
        *   [1.1.1 BIOS](#BIOS)
        *   [1.1.2 EFI](#EFI)
    *   [1.2 安装到分区上或者无分区磁盘上](#安装到分区上或者无分区磁盘上)
    *   [1.3 只生成 core.img](#只生成_core.img)
*   [2 图形化配置工具](#图形化配置工具)
*   [3 视觉配置](#视觉配置)
    *   [3.1 设置帧缓冲分辨率](#设置帧缓冲分辨率)
    *   [3.2 915resolution 破解](#915resolution_破解)
    *   [3.3 背景图像和点阵字体](#背景图像和点阵字体)
    *   [3.4 主题](#主题)
    *   [3.5 菜单颜色](#菜单颜色)
    *   [3.6 隐藏菜单](#隐藏菜单)
    *   [3.7 禁用 framebuffer](#禁用_framebuffer)
*   [4 通过 GRUB 直接启动 ISO9660 映像文件](#通过_GRUB_直接启动_ISO9660_映像文件)
*   [5 持久块设备命名法](#持久块设备命名法)
*   [6 使用卷标](#使用卷标)
*   [7 用密码保护 GRUB 菜单](#用密码保护_GRUB_菜单)
    *   [7.1 只针对编辑 GRUB 和控制台选项进行密码保护](#只针对编辑_GRUB_和控制台选项进行密码保护)
*   [8 在没有按着 SHIFT 键时隐藏 GRUB 界面](#在没有按着_SHIFT_键时隐藏_GRUB_界面)
*   [9 将 UUID 和基础脚本结合使用](#将_UUID_和基础脚本结合使用)
*   [10 多个启动条目](#多个启动条目)
    *   [10.1 取消子菜单](#取消子菜单)
    *   [10.2 调用之前的启动条目](#调用之前的启动条目)
    *   [10.3 修改默认菜单条目](#修改默认菜单条目)
    *   [10.4 自动启动非默认启动条目（仅一次）](#自动启动非默认启动条目（仅一次）)
*   [11 演奏一曲](#演奏一曲)
*   [12 为早期启动手动配置核心映像](#为早期启动手动配置核心映像)
*   [13 UEFI 延伸阅读](#UEFI_延伸阅读)
    *   [13.1 另一种安装方法](#另一种安装方法)
    *   [13.2 UEFI 固件解决方案](#UEFI_固件解决方案)
    *   [13.3 在固件启动管理器中创建 GRUB 条目](#在固件启动管理器中创建_GRUB_条目)
    *   [13.4 独立的 GRUB](#独立的_GRUB)
    *   [13.5 技术信息](#技术信息)

## 其它安装方式

### 安装到 U 盘

#### BIOS

假设 U 盘的第一个分区是 FAT32格式，其分区是/dev/sdy1

```
# mkdir -p /mnt/usb
# mount /dev/sdy1 /mnt/usb
# grub-install --target=i386-pc --debug --boot-directory=/mnt/usb/boot /dev/sdy
# grub-mkconfig -o /mnt/usb/boot/grub/grub.cfg

```

可以选择将配置备份到 `grub.cfg`：

```
# mkdir -p /mnt/usb/etc/default
# cp /etc/default/grub /mnt/usb/etc/default
# cp -a /etc/grub.d /mnt/usb/etc

```

```
# sync; umount /mnt/usb

```

#### EFI

在你运行 `grub-install` 的时候使用 `--removable` 选项，就可以让 GRUB 把它的 EFI 映像写入到 `/boot/efi/EFI/BOOT/BOOTX64.efi`，这样启动固件就可以在没有 UEFI 启动条目的的情况下找到。

### 安装到分区上或者无分区磁盘上

**警告:** GRUB **极不推荐** 将其安装到分区启动扇区或者无分区磁盘上（Grub Legacy 和 syslinux 相反）。这种安装方式不安全，当升级时可能会损坏。Arch 开发人员也 **不支持** 这种方式.

下面的命令将会将 GRUB 安装到分区扇区或者无分区磁盘（也称作超级软盘），或者安装到软盘上。下面例子中以 `/dev/sdaX` 作为 `/boot` 分区。

```
# chattr -i /boot/grub/i386-pc/core.img
# grub-install --target=i386-pc --debug --force /dev/sdaX
# chattr +i /boot/grub/i386-pc/core.img

```

**注意:**

*   `/dev/sdaX` 仅用作示例。
*   `--target=i386-pc` 令 `grub-install` 仅为 BIOS 系统安装。建议总是使用这个选项来排除 grub-install 命令中的模糊性。

你应该使用 `--force` 选项来启用对 blocklists（块列表）的支持，而不应该使用 `--grub-setup=/bin/true`，后者类似于单纯地生成 `core.img`。

`grub-install` 会生成以下警告，来提醒你哪里有可能出现问题。

```
/sbin/grub-setup: warn: Attempting to install GRUB to a partitionless disk or to a partition. This is a BAD idea.
/sbin/grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists.
                        However, blocklists are UNRELIABLE and their use is discouraged.

```

不使用 `--force` 选项则可能会出现以下错误，并且 `grub-setup` 不会将启动代码安装到启动扇区上：

```
/sbin/grub-setup: error: will not proceed with blocklists

```

而指定了 `--force`，会出现：

```
Installation finished. No error reported.

```

`grub-setup` 默认不启用这个选项，是因为在分区或者无分区磁盘上，`grub` 依赖于嵌入分区引导扇区的块列表 (blocklists) 来定位 `/boot/grub/i386-pc/core.img` 和前缀目录 `/boot/grub`。而 `core.img` 在分区上的扇区位置很有可能随着分区文件系统的更改而变化（复制文件，删除文件等）。详情请参考 [https://bugzilla.redhat.com/show_bug.cgi?id=728742](https://bugzilla.redhat.com/show_bug.cgi?id=728742) 和 [https://bugzilla.redhat.com/show_bug.cgi?id=730915](https://bugzilla.redhat.com/show_bug.cgi?id=730915).

临时解决方案是给 `/boot/grub/i386-pc/core.img` 文件加“不可变”(immutable) 标志（按照上面提过的，使用 `chattr` 命令）。这样 `core.img` 文件的位置就不会变。只有当将 GRUB 安装到分区启动扇区或者无分区磁盘上时才需要给 `/boot/grub/i386-pc/core.img` 加上“不可变”标志，在安装到 MBR 或者单纯地生成 `core.img` 而不嵌入到其他引导扇区里的时候，就不用添加（正如上面所述）。

然而即使没有报错，生成的 `grub.cfg` 文件也不会包含正确的 UUID。参考 [https://bbs.archlinux.org/viewtopic.php?pid=1294604#p1294604](https://bbs.archlinux.org/viewtopic.php?pid=1294604#p1294604) 。 要解决这个问题，使用如下命令：

```
# mount /dev/sdxY /mnt        #Your root partition.
# mount /dev/sdxZ /mnt/boot   #Your boot partition (if you have one).
# arch-chroot /mnt
# pacman -S linux
# grub-mkconfig -o /boot/grub/grub.cfg

```

### 只生成 core.img

通过添加 `--grub-setup=/bin/true` 选项，`grub-install` 命令会填充 `/boot/grub` 文件夹并生成 `/boot/grub/i386-pc/core.img`，但是 **不会** 将 GRUB 启动引导代码嵌入到 MBR、MBR 后部区域或者分区引导扇区中。

```
# grub-install --target=i386-pc --grub-setup=/bin/true --debug /dev/sda

```

**注意:**

*   `/dev/sda` 仅是示例。
*   `--target=i386-pc` 令 `grub-install` 仅为 BIOS 系统安装。建议总是使用这个选项来排除 grub-install 命令中的模糊性。

生成后，Grub Legacy 或者 syslinux 就可以通过链式加载 GRUB 的 `core.img` 来间接加载 Linux 内核或者多启动内核了。参阅[Syslinux (简体中文)#Chainloading](/index.php/Syslinux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Chainloading "Syslinux (简体中文)")。

## 图形化配置工具

可以安装下列软件包：

*   **grub-customizer** — GRUB 或者 BURG 的 GTK+ 定制器

	[https://launchpad.net/grub-customizer](https://launchpad.net/grub-customizer) || [grub-customizer](https://www.archlinux.org/packages/?name=grub-customizer)

*   **grub2-editor-frameworks** — grub2-editor 的非官方 KF5 port

	[https://github.com/maz-1/grub2-editor](https://github.com/maz-1/grub2-editor) || [grub2-editor-frameworks](https://aur.archlinux.org/packages/grub2-editor-frameworks/)

*   **startupmanager** — 用来修改 GRUB Legacy, GRUB, Usplash 和 Splashy 设置的图形应用 ([已被废止](https://launchpad.net/startup-manager/+announcement/8300))

	[http://sourceforge.net/projects/startup-manager/](http://sourceforge.net/projects/startup-manager/) || [startupmanager](https://aur.archlinux.org/packages/startupmanager/)

## 视觉配置

GRUB 默认支持改变菜单外观。如果你没有初始化，请务必以视频模式 gfxmode 初始化 GRUB 图形终端 gfxterm，你可以在 [GRUB (简体中文)#"No suitable mode found" 错误](/index.php/GRUB_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#"No_suitable_mode_found"_错误 "GRUB (简体中文)")一节找到这部分内容。此视频模式由 GRUB 通过 gfxpayload 传递给 Linux 内核，任何视觉配置都需要这种模式才能够有效果。

### 设置帧缓冲分辨率

GRUB 既可以为自己，也可以为内核设定帧缓冲。现在已经不使用老的 `vga=` 配置了，推荐方法是在 `/etc/default/grub` 文件中按照下面的例子编辑，来设定宽度（像素）x高度（像素）x[颜色深度](https://en.wikipedia.org/wiki/color_depth "wikipedia:color depth")：

```
GRUB_GFXMODE=1024x768x32
GRUB_GFXPAYLOAD_LINUX=keep

```

可以指定多种分辨率，包括默认的 `auto`，所以建议你编辑成这个样：`GRUB_GFXMODE=<心仪的分辨率>,<后备分辨率比如 1024x768>,auto`。更多信息请见 [GRUB gfxmode 文档](https://www.gnu.org/software/grub/manual/grub/html_node/gfxmode.html)。 [gfxpayload](https://www.gnu.org/software/grub/manual/html_node/gfxpayload.html#gfxpayload) 属性可以确保内核也保持该分辨率。

**注意:**

*   只有显卡通过 [VESA BIOS 拓展](https://en.wikipedia.org/wiki/VESA_BIOS_Extensions "wikipedia:VESA BIOS Extensions")支持的模式才能用。要查看所支持的模式列表，安装 [hwinfo](https://www.archlinux.org/packages/?name=hwinfo) 然后以 root 权限运行 `hwinfo --framebuffer`。或者进入 GRUB 命令行运行 `videoinfo` 命令。
*   早期版本的 [NVIDIA](/index.php/NVIDIA "NVIDIA") 专有驱动（使用显卡 GeForce GTX 970，驱动 nvidia 370 进行了测试）支持的 `GRUB_GFXMODE` 格式为 `*<宽>*x*<高>*-*<色深>*`（例如 `1920x1200-24`，而不是 `1920x1200x24`）。这应该不会影响新的显卡和驱动。使用比较新的驱动的 Pascal 显卡（以 GeForce GTX 1060 显卡和 nvidia 381.22 驱动测试）没法使用上文建议的格式，而且会引发严重的问题，包括但不限于系统崩溃以及 hard lock。当前的驱动和显卡最好使用标准的 `*<width>*x*<height>*x*<depth>*` 格式来配置 `GRUB_GFXMODE`。
*   确保在修改完后运行 `grub-mkconfig -o /boot/grub/grub.cfg`。

这种方法不管用的话，可以试试老的 `vga=` 方法。将它添加到 `/etc/default/grub` 文件中的 `"GRUB_CMDLINE_LINUX_DEFAULT="` 一行就行了。比如 `"GRUB_CMDLINE_LINUX_DEFAULT="quiet splash vga=792"` 可以将系统的分辨率设定为 `1024x768`。

### 915resolution 破解

有些时候,Intel 显卡无法通过 `# hwinfo --framebuffer` 或 `vbeinfo` 显示你需要的分辨率。这种情况下，你可以使用 `915resolution` 破解。这种破解会临时性的修改显卡 BIOS 来添加所需的分辨率。详情请参考[915resolution 主页](http://915resolution.mango-lang.org/)。这个包可以在这里找到：[915resolution](https://aur.archlinux.org/packages/915resolution/)

首先，找一个你想要修改的视频模式。为此需要在 GRUB 命令行模式下运行：

 `sh:grub> 915resolution -l` 
```
Intel 800/900 Series VBIOS Hack : version 0.5.3
[...]
**Mode 30** : 640x480, 8 bits/pixel
[...]

```

然后，使用 `1440x900` 分辨率覆盖 `Mode 30`：

 `/etc/grub.d/00_header` 
```
[...]
**915resolution 30 1440 900  # 添加这行**
set gfxmode=${GRUB_GFXMODE}
[...]

```

最后按照之前描述的方式设置 `GRUB_GFXMODE`，再重新生成 GRUB 配置文件，重启并测试是否生效。

### 背景图像和点阵字体

GRUB 原生支持设置背景图像和 `pf2` 格式的点阵字体。[grub](https://www.archlinux.org/packages/?name=grub) 包中包含了 unifont 字体，名为`unicode.pf2`，（也有可能只包含名为 `ascii.pf2` 的ASCII字符字体）。

在载入正确的模块之后，GRUB 支持的图像格式有 tga, png 和 jpeg。所支持的最大图像分辨率跟硬件有关。

请确保你已经设定了合适的[帧缓冲分辨率](#设置帧缓冲分辨率)。

按如下方式编辑 `/etc/default/grub`：

```
GRUB_BACKGROUND="/boot/grub/myimage"
#GRUB_THEME="/path/to/gfxtheme"
GRUB_FONT="/path/to/font.pf2"

```

**注意:** 如果你将 GRUB 安装在单独的分区上，`grub.cfg` 文件中会自动将 `/boot/grub/myimage` 改成 `/grub/myimage`。

需要[重新生成](/index.php/GRUB_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#生成主配置文件 "GRUB (简体中文)") `grub.cfg` 来让修改起作用。如果成功添加了背景图片，用户会在运行命令的终端中看到 `"Found background image..."`。如果句话没有出现，你设定的图像信息可能没有成功添加进 `grub.cfg` 文件。

如果图像没有正确显示，执行如下检查：

*   在 `/etc/default/grub` 文件中，图像的路径和名字要正确
*   图像的大小和格式要合适 (tga, png, 8-bit jpg)
*   图像需要以 RGB 模式存储，而且没有索引
*   `/etc/default/grub` 文件里面开启了 console 模式
*   需要执行 `grub-mkconfig` 命令以将图像信息写入 `/boot/grub/grub.cfg` 文件
*   `grub-mkconfig` 脚本不会对 `grub.cfg` 文件中所写的文件名添加引号，所以要确保这些名字里没有空格

### 主题

下面的例子将展示如何使用 GRUB 包里面的 Starfield 主题：

编辑 `/etc/default/grub`

```
GRUB_THEME="/usr/share/grub/themes/starfield/theme.txt"

```

需要[重新生成](/index.php/GRUB_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#生成主配置文件 "GRUB (简体中文)") `grub.cfg` 来让修改起作用。如果配置成功的话，在重生成配置过程中，会在终端里出现 `Found theme: /usr/share/grub/themes/starfield/theme.txt`。

一旦使用了主题，你设置的背景图像通常就不起作用了。

### 菜单颜色

GRUB 支持设置菜单颜色。可使用的颜色能从 [GRUB 手册](https://www.gnu.org/software/grub/manual/html_node/Theme-file-format.html)里面找到。示例如下：

编辑 `/etc/default/grub`：

```
GRUB_COLOR_NORMAL="light-blue/black"
GRUB_COLOR_HIGHLIGHT="light-cyan/blue"

```

### 隐藏菜单

GRUB 特性之一就是支持隐藏/跳过菜单，可以在需要的时候按 `Esc` 来取消隐藏/跳过。同时还支持设置是否显示 timeout 计时器。

按照你的想法来编辑 `/etc/default/grub`。添加下面的几行可以启动这个功能，其中计时器被设定为 5 秒钟，而且可以被用户看到：

```
GRUB_TIMEOUT=5
GRUB_TIMEOUT_STYLE='countdown'

```

GRUB_TIMEOUT 是设置显示菜单前等待几秒。

### 禁用 framebuffer

使用 NVIDIA 私有驱动的用户可能希望禁用 GRUB 的 framebuffer，因为它会导致驱动错误。

要禁用 framebuffer，只要在 `/etc/default/grub` 中取消下面这行的注释：

```
GRUB_TERMINAL_OUTPUT=console

```

如果你想保留 GRUB 的 framebuffer，解决方法是在 GRUB 载入内核前进入文字模式。可以通过在 `/etc/default/grub` 中进行如下修改：

```
GRUB_GFXPAYLOAD_LINUX=text

```

## 通过 GRUB 直接启动 ISO9660 映像文件

GRUB 支持通过 loopback 设备直接从 ISO 映像启动，例如参考 [Multiboot USB drive#Using GRUB and loopback devices](/index.php/Multiboot_USB_drive#Using_GRUB_and_loopback_devices "Multiboot USB drive")。

## 持久块设备命名法

为[块设备持久命名](/index.php/Persistent_block_device_naming_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Persistent block device naming (简体中文)") (Persistent block device naming) 的一种方式是使用全局的 UUID 来区分分区，而不是用老的 `/dev/sd*` 表示法。其好处在上面链接中已详述。

GRUB 默认就使用文件系统的 UUID 来为块设备持久命名。

**注意:** 每次相关的文件系统调整后，就需要在 `/etc/default/grub` 中使用新的 UUID，然后更新`/boot/grub.cfg`。通过 Live-CD 调整分区和文件系统后要特别注意这点。

是否使用 UUID 由 `/etc/default/grub` 里的这个选项控制：

```
GRUB_DISABLE_LINUX_UUID=true

```

## 使用卷标

通过使用 `search` 命令的 `--label`参数，可以使用卷标，即附加在文件系统上方便人阅读的字符串。首先，给文件系统设置一个卷标：

```
# tune2fs -L *卷标* *分区*

```

然后使用这个卷标添加启动条目。例如这样：

```
menuentry "Arch Linux, session texte" {
  search --label --set=root archroot
  linux /boot/vmlinuz-linux root=/dev/disk/by-label/archroot ro
  initrd /boot/initramfs-linux.img
}

```

## 用密码保护 GRUB 菜单

**警告:** 如果有人能对你的机器进行物理上的访问，而且可以使用 Live USB 或磁盘启动（例如 BIOS 允许从外接磁盘启动），而 `/boot` 又处于一个没有加密的分区上面，那他就可以非常简单地通过编辑 GRUB 设置文件来绕过下面的这些。参考[GRUB (简体中文)#/boot 加密](/index.php/GRUB_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#/boot_加密 "GRUB (简体中文)")和[Security (简体中文)#磁盘加密](/index.php/Security_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#磁盘加密 "Security (简体中文)")。

如果你想禁止其他人改变启动参数或者使用 GRUB 命令行，可以给 GRUB 的配置文件关联一个用户名/密码。只需 运行 `grub-mkpasswd-pbkdf2`，输入密码然后确认：

 `grub-mkpasswd-pbkdf2` 
```
[...]
Your PBKDF2 is grub.pbkdf2.sha512.10000.C8ABD3E93C4DFC83138B0C7A3D719BC650E6234310DA069E6FDB0DD4156313DA3D0D9BFFC2846C21D5A2DDA515114CF6378F8A064C94198D0618E70D23717E82.509BFA8A4217EAD0B33C87432524C0B6B64B34FBAD22D3E6E6874D9B101996C5F98AB1746FE7C7199147ECF4ABD8661C222EEEDB7D14A843261FFF2C07B1269A

```

然后将下面的内容添加到 `/etc/grub.d/40_custom`：

 `/etc/grub.d/40_custom` 
```
set superusers="**用户名**"
password_pbkdf2 **用户名** **<密码>**
```

这里的 `<密码>` 是由 `grub-mkpasswd_pbkdf2` 所生成的那个字符串。

然后重新生成主配置文件，现在你的 GRUB 命令行、启动参数和所有的启动条目都得到保护了。

可以参考 [GRUB 手册](https://www.gnu.org/software/grub/manual/grub.html#Security)中的 "Security" 部分来将设置放宽或者针对多用户进行更复杂的定制。

### 只针对编辑 GRUB 和控制台选项进行密码保护

对一个菜单条目添加 `--unrestricted` 选项将会允许所有的用户启动这个操作系统，但却不能修改这个条目，也不能进入 GRUB 命令行控制台。 只有超级用户或者由 `--user` 开关指定的用户才能修改这个菜单条目。

 `/boot/grub/grub.cfg`  `menuentry 'Arch Linux' --unrestricted --class arch --class gnu-linux --class os ...` 

要给 Linux 启动条目添加 `--unrestricted`，可以修改 `/etc/grub.d/10_linux` 文件开头的 `CLASS` 变量。

 `/etc/grub.d/10_linux`  `CLASS="--class gnu-linux --class gnu --class os --unrestricted"` 

## 在没有按着 SHIFT 键时隐藏 GRUB 界面

为了获取更快的启动速度，而不用等 GRUB 倒计时，可以命令 GRUB 在启动时隐藏目录，仅在 `Shift` 被按住的时候才显示。

将如下行添加到`/etc/default/grub`来启动这个功能：

```
 GRUB_FORCE_HIDDEN_MENU="true"

```

然后创建连接里的文件[[1]](https://gist.githubusercontent.com/anonymous/8eb2019db2e278ba99be/raw/257f15100fd46aeeb8e33a7629b209d0a14b9975/gistfile1.sh)，给它可执行权限，然后重新生成主配置文件：

```
# chmod a+x /etc/grub.d/31_hold_shift
# grub-mkconfig -o /boot/grub/grub.cfg

```

**注意:** 这个设置使用 keystatus 来检测按键事件，所以可能在某些机器上不能用。

## 将 UUID 和基础脚本结合使用

如果你想要使用 UUID 来避免不可靠的 BIOS 设备命名或者正在研究 GRUB 语法，这里有个使用了 UUID 的启动菜单项，和一个让 GRUB 使用你系统中正确的磁盘分区的小脚本。如果你想要将其移植到自己的系统上，只需要把 UUID 改成你的系统上的就行了。这个例子假设系统的 boot 和 root 文件系统是在不同的分区上，如果你还有其他分区，请相应地修改 GRUB 设置。

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

## 多个启动条目

### 取消子菜单

如果你安装了多个内核，比如说 linux 和 linux-lts，那么 `grub-mkconfig` 默认会把他们分成一组建立一个子菜单。如果你不想这样，可以在 `/etc/default/grub` 文件里添加下面这行来回到仅有一个菜单的情形：

```
 GRUB_DISABLE_SUBMENU=y

```

### 调用之前的启动条目

GRUB 能够记住你最近一次使用的启动项，并且在下次启动时将其作为默认项。当你使用多个内核或操作系统时（比如当前的 Arch 和一个用来做后备选项的 LTS 内核），这个特性很有用。要开启这个功能，编辑 `/etc/default/grub` 中的 `GRUB_DEFAULT` 选项：

```
GRUB_DEFAULT=saved

```

上面的命令会告诉 GRUB 使用记住的启动项为默认启动项。要想让 GRUB 记住当前选择的启动项，将下面的行添加到 `/etc/default/grub`：

```
GRUB_SAVEDEFAULT=true

```

仅当 /boot 不是 btrfs 文件系统的时候才能用，因为 GRUB 没法对 btrfs 进行写入操作。但它会生成一个容易误导人的错误信息："sparse file not allowed. Press any key to continue."

**注意:** 手动添加启动项到 `/etc/grub.d/40_custom` 或 `/boot/grub/custom.cfg`中，比如添加 Windows 启动项，需要先添加`savedefault`选项。

### 修改默认菜单条目

可以通过修改 `/etc/default/grub` 中的 `GRUB_DEFAULT` 值来改变默认启动项：

使用菜单标题：

```
GRUB_DEFAULT='Advanced options for Arch Linux>Arch Linux, with Linux linux'

```

使用数字编号：

```
 GRUB_DEFAULT="1>2"

```

GRUB 启动项序号从 0 开始计数，0 代表第一个启动项，也是上述选项的默认值，1 表示第二个启动项，以此类推。主菜单和子菜单项之间用 `>` 隔开。

上面的例子启动的是主菜单项 'Advanced options for Arch Linux' 下子菜单的第三项。

### 自动启动非默认启动条目（仅一次）

如果你想在下一次启动的时候启动一个非默认的启动项，命令 `grub-reboot` 非常有用。当系统下一次启动时，GRUB 会自动载入这个命令后的第一个参数所指的那个启动项，而以后再次启动时，GRUB 会回到正常状态加载默认条目。这样就不用修改配置文件或者在启动时进行手动选择了。

**注意:** 这个功能需要在 `/etc/default/grub` 中设定 `GRUB_DEFAULT=saved`，然后重新生成`grub.cfg`；或者在手动生成的 `grub.cfg` 中, 使用 `set default="${saved_entry}"`。

## 演奏一曲

通过修改 `GRUB_INIT_TUNE` 变量，你可以在启动时让 PC-speaker 演奏曲子。比如要演奏柏辽兹《幻想交响曲》“妖魔夜宴”乐章片段（大管部分），你可以添加下面的设置：

`GRUB_INIT_TUNE="312 262 3 247 3 262 3 220 3 247 3 196 3 220 3 220 3 262 3 262 3 294 3 262 3 247 3 220 3 196 3 247 3 262 3 247 5 220 1 220 5"`

更多相关信息可以查看 `info grub -n play`。

## 为早期启动手动配置核心映像

如果你需要用一个特殊的键盘布局，或者要让 GRUB 环境访问 `/boot` 的配置步骤太过复杂，导致 GRUB 没法自动配置，你可以自己生成一个核心映像。在 UEFI 系统上，核心映像就是在启动时需要被固件载入的 `grubx64.efi` 文件。自己建立一个核心映像，就可以嵌入在早期启动过程中需要用到的所有模块，以及用来引导 GRUB 配置脚本。

首先，假设在一个 UEFI 系统中，我们需要在早期启动过程中载入 `dvorak` 键盘布局，以输入 `/boot` 加密分区的密码。

从生成的 `/boot/grub/grub.cfg` 文件中查看需要使用哪些模块来挂载加密的 `/boot` 分区。例如在你的 `menuentry` 一项中你应该看到类似下面的内容：

```
insmod diskfilter cryptodisk luks gcry_rijndael gcry_rijndael gcry_sha256
insmod ext2
cryptomount -u 1234abcdef1234abcdef1234abcdef
set root='cryptouuid/1234abcdef1234abcdef1234abcdef'
```

把这些模块都记下来，他们都应该被包含到核心映像里面。现在把你的键盘布局打包，它应该作为一个 memdisk 来嵌入到核心映像里：

```
# grub-kbdcomp -o dvorak.gkb dvorak
# tar cf memdisk.tar dvorak.gkb

```

现在创建需要在 GRUB 核心映像中使用的配置文件。这和正常的 GRUB 配置文件的格式是一样的，但只需要简单几行来载入 `/boot` 分区里的主配置文件就可以了：

 `early-grub.cfg` 
```
set root=(memdisk)
set prefix=($root)/

terminal_input at_keyboard
keymap /dvorak.gkb

cryptomount -u 1234abcdef1234abcdef1234abcdef
set root='cryptouuid/1234abcdef1234abcdef1234abcdef'
set prefix=($root)/grub

configfile grub.cfg
```

最后，生成核心映像，列出在 `grub.cfg` 文件中所需要的所有模块，再加上 `early-grub.cfg` 脚本中所使用的模块。上例中需要的模块有 `memdisk`, `tar`, `at_keyboard`, `keylayouts` 和 `configfile`。

```
# grub-mkimage -c early-grub.cfg -o grubx64.efi -O x86_64-efi -m memdisk.tar diskfilter cryptodisk luks gcry_rijndael gcry_sha256 ext2 memdisk tar at_keyboard keylayouts configfile

```

生成的 EFI 核心映像可以和由 `grub-install` 所自动生成的一样使用，把它放在你的 EFI 分区，然后使用 `efibootmgr` 来启用它，或者依照你的系统固件来适当地进行配置。

## UEFI 延伸阅读

下面是关于通过 UEFI 安装 Arch 的其他相关信息。

### 另一种安装方法

通常，不管 EFI 系统分区挂载到哪，GRUB 都会将所有文件包括配置文件放到 `/boot`。

如果你想将所有的文件放在 EFI 系统分区中，请给 grub-install 命令添加 `--boot-directory=*esp*` 选项：

```
# grub-install --target=x86_64-efi --efi-directory=*esp* --bootloader-id=grub --boot-directory=*esp* --debug

```

这个命令会将 GRUB 文件放在 {{ic|*esp*/grub} 而不是 `/boot/grub` 中。使用这个方法，请确保 grub-mkconfig 将配置文件放在与上面一样的目录里：

```
# grub-mkconfig -o *esp*/grub/grub.cfg

```

其他的配置是完全一样的。

### UEFI 固件解决方案

一些 UEFI 固件要求可启动 *.efi* 文件叫一个特定的名字而且放在一个特定的位置中： `*esp*/EFI/boot/bootx64.efi`（其中 `*esp*` 是 UEFI 分区挂载点）。这时如果不能满足这些条件，就会不能启动。好在这对那些没有这些要求的固件没有影响。

要满足要求，首先创建必要的目录，然后通过如下方式复制 `.efi` 并重新命名：

```
# mkdir *esp*/EFI/boot
# cp *esp*/EFI/grub_uefi/grubx64.efi *esp*/EFI/boot/bootx64.efi

```

### 在固件启动管理器中创建 GRUB 条目

`grub-install` 会自动尝试在启动管理器中创建 GRUB 条目。如果没有成功，请参考 [Unified Extensible Firmware Interface (简体中文)#efibootmgr](/index.php/Unified_Extensible_Firmware_Interface_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#efibootmgr "Unified Extensible Firmware Interface (简体中文)")，里面有如何使用 `efibootmgr` 创建启动目录条目的介绍。一般来说，这个问题都是因为你没有以 UEFI 模式启动 CD/USB 造成的。请参考 [Unified Extensible Firmware Interface (简体中文)#从 ISO 创建 UEFI 可启动 USB](/index.php/Unified_Extensible_Firmware_Interface_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#从_ISO_创建_UEFI_可启动_USB "Unified Extensible Firmware Interface (简体中文)")。

### 独立的 GRUB

本节假设你要为 x86_64 系统 (x86_64-efi) 创建一个独立的 GRUB。至于 32 位 (IA32) EFI 系统，适当地将 `x86_64-efi` 修改成 `i386-efi` 就可以了。

你可以建立一个 `grubx64_standalone.efi` 应用，这个 UEFI 应用将所有的模组嵌入应用内部的一个 tar 包中，所以就不需要使用单独的目录来存放 GRUB UEFI 模组和其他相关文件了。使用 [grub](https://www.archlinux.org/packages/?name=grub) 包里的 `grub-mkstandalone` 命令按照下面的方法操作来实现这个功能：

```
# echo 'configfile ${cmdpath}/grub.cfg' > /tmp/grub.cfg
# grub-mkstandalone -d /usr/lib/grub/x86_64-efi/ -O x86_64-efi --modules="part_gpt part_msdos" --locales="en@quot" --themes="" -o "*esp*/EFI/grub/grubx64_standalone.efi" "boot/grub/grub.cfg=/tmp/grub.cfg" -v

```

然后把 GRUB 配置文件复制到 `*esp*/EFI/grub/grub.cfg`，再使用 [efibootmgr](/index.php/Unified_Extensible_Firmware_Interface_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#efibootmgr "Unified Extensible Firmware Interface (简体中文)") 为 `*esp*/EFI/grub/grubx64_standalone.efi` 创建一个 UEFI 启动管理器条目。

**注意:** 要让 `${cmdpath}` 功能正常工作，`--modules="part_gpt part_msdos"` 选项（包含引号）是必要的。

**警告:** 如果你在填写 `${cmdpath}` 的时候漏掉一个斜杠（比如把 `(hd1,msdos2)/EFI/Boot` 写成 `(hd1,msdos2)EFI/Boot`），你就会发现 `grub.cfg` 文件没法读取，然后被迫进入 GRUB 命令行中。如果出现这样的问题，检查 `${cmdpath}` 设置成了什么 (`echo ${cmdpath}` )，然后手工载入配置文件（例如 `configfile (hd1,msdos2)/EFI/Boot/grub.cfg`）。

### 技术信息

GRUB EFI 文件总是要配置文件放在 `${prefix}/grub.cfg`。当然在独立的 GRUB EFI 文件中，`${prefix}` 位于一个 tar 包的内部，嵌入在 GRUB EFI 文件自身之中（在 GRUB 环境中，这被称作 `(memdisk)`）。这个 tar 包包含了所有在正常的 GRUB EFI 下存储在 `/boot/grub` 中的文件。

因为将 `/boot/grub` 中的内容嵌入到了独立映像的内部，它就不再对任何实际的（外部的） `/boot/grub` 有任何依赖了。因此在独立 GRUB EFI 文件的情形下 `${prefix}==(memdisk)/boot/grub`，而且独立的 GRUB EFI 文件认为其配置文件存放于 `${prefix}/grub.cfg==(memdisk)/boot/grub/grub.cfg`。

因此要让独立的 GRUB EFI 文件读取存储在与 EFI 文件相同目录（在 GRUB 环境中用 `${cmdpath}` 表示）下的外部 `grub.cfg` 时，我们创建一个简单的 `/tmp/grub.cfg` 来让 GRUB 使用 `${cmdpath}/grub.cfg` 来做其配置文件。（在 `(memdisk)/boot/grub/grub.cfg` 中使用 `configfile ${cmdpath}/grub.cfg` 命令。）然后我们给 grub-mkstandalone 添加 `"boot/grub/grub.cfg=/tmp/grub.cfg"` 选项，把这个 `/tmp/grub.cfg` 文件复制到 `${prefix}/grub.cfg`（事实上就是 `(memdisk)/boot/grub/grub.cfg`）。

这样，独立的 GRUB EFI 文件和这个 `grub.cfg` 可以存放在 EFI 系统分区中的任何一个目录里，只有它们处在同一个目录中就可以。这样它们就变得可移植了。