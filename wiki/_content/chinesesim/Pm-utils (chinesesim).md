**pm-utils** 是一个全新的电源挂起和电源状态设置框架。它被设计来替代 `powersave` 包中的相关脚本。

通常HAL使用pm-utilsl来执行一系列的hacks来解决驱动所不能提供的电源挂起方面的操作。可以很方便的在特定目录当中配置自定义的挂钩，挂钩可以由管理员来建立或者是被包含在安装包当中，如果安装包需要监视电源的挂起和电源状态的改变。

可以和 [Cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils") 包联合使用，为笔记本和台式机提供完整的电源管理方案。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 基本配置](#.E5.9F.BA.E6.9C.AC.E9.85.8D.E7.BD.AE)
    *   [2.1 挂起 / 休眠到内存](#.E6.8C.82.E8.B5.B7_.2F_.E4.BC.91.E7.9C.A0.E5.88.B0.E5.86.85.E5.AD.98)
    *   [2.2 待机 / 休眠到磁盘](#.E5.BE.85.E6.9C.BA_.2F_.E4.BC.91.E7.9C.A0.E5.88.B0.E7.A3.81.E7.9B.98)
    *   [2.3 在非root下执行挂起/休眠](#.E5.9C.A8.E9.9D.9Eroot.E4.B8.8B.E6.89.A7.E8.A1.8C.E6.8C.82.E8.B5.B7.2F.E4.BC.91.E7.9C.A0)
*   [3 高级配置](#.E9.AB.98.E7.BA.A7.E9.85.8D.E7.BD.AE)
    *   [3.1 配置文件中一些可以使用的变量](#.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6.E4.B8.AD.E4.B8.80.E4.BA.9B.E5.8F.AF.E4.BB.A5.E4.BD.BF.E7.94.A8.E7.9A.84.E5.8F.98.E9.87.8F)
    *   [3.2 如何关闭监测（钩子，hook）程序](#.E5.A6.82.E4.BD.95.E5.85.B3.E9.97.AD.E7.9B.91.E6.B5.8B.EF.BC.88.E9.92.A9.E5.AD.90.EF.BC.8Chook.EF.BC.89.E7.A8.8B.E5.BA.8F)
    *   [3.3 建立你自己的钩子](#.E5.BB.BA.E7.AB.8B.E4.BD.A0.E8.87.AA.E5.B7.B1.E7.9A.84.E9.92.A9.E5.AD.90)
*   [4 工作原理](#.E5.B7.A5.E4.BD.9C.E5.8E.9F.E7.90.86)
*   [5 已知问题](#.E5.B7.B2.E7.9F.A5.E9.97.AE.E9.A2.98)
    *   [5.1 Resume Hook](#Resume_Hook)
    *   [5.2 重新启动鼠标](#.E9.87.8D.E6.96.B0.E5.90.AF.E5.8A.A8.E9.BC.A0.E6.A0.87)
    *   [5.3 我点击的挂起但没有任何反应 / 日志文件在哪里](#.E6.88.91.E7.82.B9.E5.87.BB.E7.9A.84.E6.8C.82.E8.B5.B7.E4.BD.86.E6.B2.A1.E6.9C.89.E4.BB.BB.E4.BD.95.E5.8F.8D.E5.BA.94_.2F_.E6.97.A5.E5.BF.97.E6.96.87.E4.BB.B6.E5.9C.A8.E5.93.AA.E9.87.8C)
    *   [5.4 在Openbox 菜单添加睡眠模式](#.E5.9C.A8Openbox_.E8.8F.9C.E5.8D.95.E6.B7.BB.E5.8A.A0.E7.9D.A1.E7.9C.A0.E6.A8.A1.E5.BC.8F)
*   [6 相关资源](#.E7.9B.B8.E5.85.B3.E8.B5.84.E6.BA.90)
*   [7 Credits](#Credits)

## 安装

[pm-utils](https://aur.archlinux.org/packages/pm-utils/) 包可以从官方软件仓库安装：

```
# pacman -S pm-utils

```

**注意:** 如果你在 resuming video 时遇到问题，你也许需要从[官方源](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")同时安装 [vbetool](https://www.archlinux.org/packages/?name=vbetool)。

**注意:** 如果你从清洁安装开始，确保你已经安装了 [acpi](https://www.archlinux.org/packages/?name=acpi)。

## 基本配置

### 挂起 / 休眠到内存

理想情况下，运行 `sudo pm-suspend` 将会保存运行程序的状态到内存并关闭内存之外的设备以节省电能。按下电源键会唤醒电脑。

有时 pm-suspend 会挂住，无法正常完成。原因可能是 "不正常" 的模块。如果知道是哪个模块导致问题，可以在 `/etc/pm/config.d/modules` SUSPEND_MODULES 配置项中加入这些模块：

```
SUSPEND_MODULES="uhci_hd button ehci_hd"

```

在挂起和唤醒电脑时，程序会对它们进行特别处理。

要在合上笔记本盖等电源事件发生时自动执行 pm-suspend，请参考 [Acpid](/index.php/Acpid "Acpid")。

### 待机 / 休眠到磁盘

要使用休眠功能，需要以root的身份编辑 `/boot/grub/menu.lst` ，并在内核选项中添加 **resume=/path/to/swap/drive** (e.g. /dev/sda2) 例如：

```
# (0) Arch Linux
title  Arch Linux
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda3 **resume=/dev/sda2** ro
initrd /initramfs-linux.img

```

当计算机进入休眠后，计算机会把内存中的所有信息保存到交换分区（swap partition）... 那么要求你的交换分区有足够的空间来保存RAM信息。

Raid swap :

```
# (0) Arch Linux
title  Arch Linux
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/md2 resume=/dev/md0 ro md=0,/dev/sda2,/dev/sdb2  md=2,/dev/sda5,/dev/sdb5 vga=773
initrd /initramfs-linux.img

```

如果你想要使用UUID来代替磁盘编号(UUID使用blkid命令找出，需要超级用户权限):

```
# (0) Arch Linux
title  Arch Linux
root   (hd0,0)
kernel /vmlinuz-linux cryptdevice=/dev/sda2:main root=/dev/mapper/main-root  resume=/dev/disk/by-uuid/1d893194-b151-43cd-a89e-6f89bd8b9f99 ro
initrd /initramfs-linux.img

```

当你的机器休眠的时候，数据会从内存转向swap分区，所以最好swap空间至少要等于内存的。

对于**GRUB2**，需要修改 `/boot/grub/grub.cfg`的"linux"行。这是个例子（注意修改你的UUID）：

```
linux   /boot/vmlinuz-linux root=/dev/disk/by-uuid/818dc030-8108-4428-8859-b73a58d0b0f3 ro  quiet resume=/dev/sda2

```

关于永久性的讨论,请移步(英文) [论坛](https://bbs.archlinux.org/viewtopic.php?pid=886789#p88678).

即使你的swap分区小于内存,也有很大的可能成功的休眠.根据 [kernel documentation](http://www.mjmwired.net/kernel/Documentation/power/interface.txt), *`/sys/power/image_size` 控制休眠到磁盘镜像的大小*,其中有一个500M的默认值。*休眠将竭尽所能的确保镜像的大小不会超过这个阀值。* 你可以增加或者减少swap分区的大小来提高休眠的速度.

**注意:** 你必须添加`resume` 钩子到 `/etc/mkinitcpio.conf`文件中, 移步 [常见问题解答](#Resume_Hook)!

### 在非root下执行挂起/休眠

因为必须在root权限下允许 `pm-utils` 脚本，一般情况下，你希望没有root密码的普通用户来执行这些脚本。这时，你需要使用visudo来编辑 `/etc/sudoers` 文件，例如：

```
# visudo

```

添加如下几行，记住把 *username* 替换成你自己的登录名：

```
*username*  ALL = (ALL) NOPASSWD: /usr/sbin/pm-hibernate
*username*  ALL = (ALL) NOPASSWD: /usr/sbin/pm-suspend

```

保存并推出 visudo

之后，你可以在普通用户下允许下面的脚本：

```
$ sudo pm-hibernate

```

或者是

```
$ sudo pm-suspend

```

同时，把你的用户加入到 *power* 组，这样桌面小应用程序可以使用挂起操作。如果你不这样做，当你使用如 gnome shutdown 的程序来进行挂起/休眠操作的时候，计算机会发出烦人的声音和锁住屏幕。

```
# gpasswd -a *username* power

```

完成以上步骤后，你可以使用 gnome 的电源管理工具 (也许也能使用 kpowersave) 来进行自动的挂起/休眠，比如在合上笔记本上盖和电池电量不足的时候...

## 高级配置

主要的配置文件是**`/usr/lib/pm-utils/defaults`**. 但是建议你不要去修改这个文件，因为此文件会随着软件包的升级而被重置。如果需要配置可以修改Y**`/etc/pm/config.d/`** 。

你可以将下列简单的配置以"modules" 或 "config"的命名加入`/etc/pm/config.d`中，这个设置将会替代系统的一般配置。

```
SUSPEND_MODULES="button uhci_hcd"

```

### 配置文件中一些可以使用的变量

```
SUSPEND_MODULES="button" # 列表当中的模块将在系统挂起时被卸载。

```

### 如何关闭监测（钩子，hook）程序

如果你不喜欢某个监测程序或觉得某个监测程序无用甚至影响正常使用的话，你可以将他视为一个Bug来报告。当然，我们也可以很简单的去禁用它。你可以通过管理`/etc/pm/sleep.d/`目录中所对应设备的文件控制监测程序的运行与否。例如：

```
touch /etc/pm/sleep.d/45pcmcia

```

你就可以建立一个`/usr/lib/pm-utils/sleep.d/45pcmcia`文件，来禁用pcmcia。

对于这个假的钩子程序不要设置可执行属性位。

### 建立你自己的钩子

如果你想建立一些只属于你自己的挂起/休眠设置，你只需要简单的把你的钩子放到`/etc/pm/hooks`。这个文件夹中的钩子会在挂起的时候按照字母顺序执行，并在唤醒过程中按照字母逆序执行（因此通常它们的名字以两位数字开头使得顺序更加明了）。

以下展示的是一个非实用的钩子，它会把一些信息写入你的log文件：

```
#!/bin/bash
case $1 in
    hibernate)
        echo "Hey guy, we are going to suspend to disk!"
        ;;
    suspend)
        echo "Oh, this time we are doing a suspend to RAM. Cool!"
        ;;
    thaw)
        echo "oh, suspend to disk is over, we are resuming..."
        ;;
    resume)
        echo "hey, the suspend to RAM seems to be over..."
        ;;
    *)  echo "somebody is calling me totally wrong."
        ;;
esac

```

把以上内容写入`/etc/pm/sleep.d/66dummy`文件中，并执行`chmod +x /etc/pm/sleep.d/66dummy`，之后在挂起/唤醒过程中它将产生一些无实际作用的行。

***注意：** 所有的钩子都以root用户执行。这意味着你需要在创建临时文件、检查PATH环境变量等时候多加小心，以避免安全问题。*

## 工作原理

这个概念看起来很简单：这些系统脚本 (`pm-suspend`、`pm-hibernate`、`pm-suspend-hybrid`)将会运行名为"hooks"的可执行文件，这些脚本将会按照字母顺序进行挂起或休眠。一旦hooks运行成功，电脑就会进入休眠状态。直到下次唤醒PC时，所有的脚本按照相反的顺序从内存或者磁盘恢复工作。hooks做了很多事情，例如准备启动，停止蓝牙工作，或者卸载相关的模块。 通常，挂起和休眠都会从HAL或者桌面部件中启用（例如gnome-power-manager、 kpowersave。）

***注意：** `suspend-hybrid` 还是一个半成品，并不保证一定可用。*

也可以设置电脑在高功耗或低功耗模式下工作，利用这条命令`pm-powersave` 使用参数`true` 或 `false`。它的工作状况基本与挂起的情况相同。

管理挂起的hooks文件在以下这些地方：

*   `/usr/lib/pm-utils/sleep.d` (发行版提供)
*   `/etc/pm/sleep.d` (系统管理员添加)

管理电源状态的hooks文件在以下这些地方：

*   `/usr/lib/pm-utils/power.d` (发行版提供)
*   `/etc/pm/power.d` (系统管理员添加)

在`/etc/pm/` 的HOOKS会优先于 `/usr/lib/pm-utils/`内的HOOKS, 那么作为系统管理员就可以仅仅设置`/etc/pm/`而不用理会发行版提供的HOOKS文件。

## 已知问题

如果你的休眠与挂起功能不能正常工作，那么一些有用的信息可能会输出到这个文件**`/var/log/pm-suspend.log`**，比如运行了哪些HOOK以及他们输出了什么。

### Resume Hook

系统有时会提示你需要将`resume` hook 添加到 initrd image中,，否则内核将提醒你没有resume. 那么，使用**ROOT**权限编辑`/etc/mkinitcpio.conf` 并且将 `resume` 添加到 HOOKS 中：

```
HOOKS="base udev autodetect ide scsi sata ***resume*** filesystems "

```

这只是一个示范，你的HOOKS可以安装自己的需要编辑。

`resume` 必须放在 'ide', 'scsi' and/or 'sata' *之后* ，但必须在 'filesystems'之前。这里应该有一个适当的 'resume' 文件 /lib/initcpio/hooks （修改合适你的配置）, hook文件是 'mkinitcpio'包的一部分。

最后，你必须重新制作内核镜像，否则那些变更不会生效。

```
# mkinitcpio -p linux

```

*注意: 如果你使用的是自己编译的内核，那么必须用 -p 参数重新制作镜像。*

例如这样做:

```
$ cat /etc/pm/sleep.d/50-hdparm_pm 
#!/bin/dash

if [ -n "$1" ] && ([ "$1" = "resume" ] || [ "$1" = "thaw" ]); then
	hdparm -B 254 /dev/sda > /dev/null
fi

```

### 重新启动鼠标

某些笔记本电脑在挂起之后会不能使用。要纠正此问题的一种方法是通过HOOKS`/etc/pm/hooks`(see [hooks](#Creating_your_own_hooks))强制重新初始化 PS/2 的驱动程序(这里指 `i8042`)

```
#!/bin/sh  
echo -n "i8042" > /sys/bus/platform/drivers/i8042/unbind
echo -n "i8042" > /sys/bus/platform/drivers/i8042/bind

```

### 我点击的挂起但没有任何反应 / 日志文件在哪里

当你从桌面部件使用挂起功能时没有正确执行，那么请尝试ROOT权限手动执行 `pm-suspend` 或 `pm-hibernate` [manually from a root shell in a terminal](#Triggering_suspend_manually). 有可能你会在终端看见一些有用的输出信息。 系统挂起的脚本也会在log留下错误信息[logfile at **`/var/log/pm-suspend.log`**](#Troubleshooting).

### 在Openbox 菜单添加睡眠模式

Openbox users can add the new scripts as additional shutdown options within the Openbox menu by adding the items to a new or existing sub-menu in `~/.config/openbox/menu.xml`, for example:

```
<menu id="64" label="Shutdown">
	<item label="Lock"> <action name="Execute"> <execute>xscreensaver-command -lock</execute> </action> </item>
	<item label="Logout"> <action name="Exit"/> </item>
	<item label="Reboot"> <action name="Execute"> <execute>sudo shutdown -r now</execute> </action> </item>
	<item label="Poweroff"> <action name="Execute"> <execute>sudo shutdown -h now </execute> </action> </item>
	***<item label="Hibernate"> <action name="Execute"> <execute>sudo pm-hibernate</execute> </action> </item>***
	***<item label="Suspend"> <action name="Execute"> <execute>sudo pm-suspend</execute> </action> </item>***
</menu>

```

## 相关资源

[HAL Quirk Site](http://people.freedesktop.org/~hughsient/quirk/) - Common solutions and frequently asked questions
[Cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils") - CPU Frequency Scaling and CPU Power schemes
[SpeedStep](/index.php/SpeedStep "SpeedStep") - More information on CPU frequency scaling (some of which is obsolete)

## Credits

*This wiki entry was originally sourced from the [OpenSUSE Wiki](http://en.opensuse.org/Pm-utils) (Licensed under GPL). A big thank you goes to the `pm-utils` developers and documenters for their time.*