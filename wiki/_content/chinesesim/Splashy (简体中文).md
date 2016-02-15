[Splashy](http://splashy.alioth.debian.org)是一个在用户空间(userspace)实现Linux系统启动画面的软件。图形环境是通过基于 [directfb](http://www.directfb.org) 的 Linux framebuffer 层实现的。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 /etc/rc.conf](#.2Fetc.2Frc.conf)
    *   [2.2 在initramfs中包含splashy](#.E5.9C.A8initramfs.E4.B8.AD.E5.8C.85.E5.90.ABsplashy)
    *   [2.3 内核命令行](#.E5.86.85.E6.A0.B8.E5.91.BD.E4.BB.A4.E8.A1.8C)
    *   [2.4 主题](#.E4.B8.BB.E9.A2.98)
*   [3 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [3.1 GNOME 无法关闭](#GNOME_.E6.97.A0.E6.B3.95.E5.85.B3.E9.97.AD)

## 安装

首先要启用 [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting")，请参考不同显卡的指令：[ATI cards](/index.php/ATI#Kernel_mode-setting_.28KMS.29 "ATI"), [Intel cards](/index.php/Intel#KMS_.28Kernel_Mode_Setting.29 "Intel") 或 [Nvidia cards](/index.php/Nouveau#KMS "Nouveau")。

从[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")中安装[splashy-full](https://aur.archlinux.org/packages/splashy-full/)。

你也可以参看Arch Linux论坛上的[这张帖子](https://bbs.archlinux.org/viewtopic.php?id=48978)，里面有splashy软件包仓库。

## 配置

### /etc/rc.conf

将下面一行加入`/etc/rc.conf`：

 `/etc/rc.conf`  `SPLASH="splashy"` 

### 在initramfs中包含splashy

将**splashy**加到`/etc/[mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf")`中HOOKS的**末尾**，例如：

 `/etc/mkinitcpio.conf`  `HOOKS="base udev autodetect splashy ..."` 

为了提早启用 KMS，将内核模块 [radeon](/index.php/Radeon "Radeon")、[i915](/index.php/Intel "Intel")(Intel 显卡)、[nouveau](/index.php/Nouveau "Nouveau") (nvidia 显卡) 加入 `/etc/mkinitcpio.conf` 中的 MODULES 行 :

 `/etc/mkinitcpio.conf` 

```
MODULES="i915"
**或**
MODULES="radeon"
**或**
MODULES="nouveau"
```

重建内存盘镜像文件(更多信息请阅读[mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")):

 `# mkinitcpio -p [name of your kernel preset]` 

### 内核命令行

需要在启动加载程序的内核命令行中加入 **quiet splash**。下面是 [Grub2](/index.php/Grub2 "Grub2") 的 `/boot/grub/grub.cfg` 示例([GRUB](/index.php/GRUB "GRUB") 和 [LILO](/index.php/LILO "LILO") 也是类似):

```
linux /boot/vmlinuz-linux root=/dev/... ro quiet splash

```

同时编辑 `/etc/default/grub` 并在`GRUB_CMDLINE_LINUX_DEFAULT=""` 行加入内核参数:

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX_DEFAULT="ro quiet splash"` 

重新生成 `grub.cfg`:

 `# grub-mkconfig -o /boot/grub/grub.cfg` 

### 主题

你可以在AUR中安装[splashy-themes](https://aur.archlinux.org/packages/splashy-themes/)来获取好看的splashy主题。安装之后，请查看可利用的主题像这样：

 `ls /usr/share/splashy/themes` 

文件夹名字就是主题名字。现在把主题名字更改为你想要的主题，如：

 `# splashy_config -s darch-white` 
**注意:** 结尾为43的主题的屏幕纵横比为4:3，其它的都是宽屏。

设置好主题后（以及每次变更主题后）都需要重新运行

```
# mkinitcpio -p [所用内核的名字]

```

然后重新启动。

## 疑难解答

### GNOME 无法关闭

如果使用 Gnome 且 GDM 以守护进程运行 Splashy 将导致 Gnome 无法正常关机/重启。

请从 `/etc/rc.conf` 的 DAEMONS 中删除 **gdm**, 并通过`[/etc/inittab](/index.php/Display_manager#inittab_method "Display manager")` 启动 gdm.