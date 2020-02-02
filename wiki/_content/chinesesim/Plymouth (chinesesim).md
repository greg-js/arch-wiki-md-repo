**翻译状态：** 本文是英文页面 [Plymouth](/index.php/Plymouth "Plymouth") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2020-01-29，点击[这里](https://wiki.archlinux.org/index.php?title=Plymouth&diff=0&oldid=445529)可以查看翻译后英文页面的改动。

[Plymouth](http://fedoraproject.org/wiki/Releases/FeatureBetterStartup) 是一个来自于Fedora社区的提供美化启动图形界面的功能的项目，现在它被列入了[freedesktop.org的软件列表](https://www.freedesktop.org/wiki/Software/#graphicsdriverswindowsystemsandsupportinglibraries)之中。它依靠[KMS](/index.php/KMS "KMS")尽可能早的设置显示器的原始分辨率显示，之后产生美化的启动引导界面直至登陆界面。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 准备](#准备)
*   [2 安装](#安装)
    *   [2.1 plymouth 钩子](#plymouth_钩子)
    *   [2.2 其他的Plymouth钩子（搭配Systemd钩子）](#其他的Plymouth钩子（搭配Systemd钩子）)
    *   [2.3 内核命令行](#内核命令行)
*   [3 配置](#配置)
    *   [3.1 平滑过渡](#平滑过渡)
    *   [3.2 显示延迟](#显示延迟)
    *   [3.3 更改主题](#更改主题)
*   [4 提示与技巧](#提示与技巧)
    *   [4.1 显示内核消息](#显示内核消息)
    *   [4.2 替换Arch Logo和创建自定义主题](#替换Arch_Logo和创建自定义主题)
*   [5 请参阅](#请参阅)

## 准备

Plymouth 依靠 [KMS](/index.php/KMS "KMS") (Kernel Mode Setting) 显示图形界面。在EFI/UEFI系统中，Plymouth可以使用EFI帧缓冲。如果你无法启用KMS，比如你使用了私有驱动，或者你只是纯粹不想使用EFI帧缓冲，那么可以考虑使用[Uvesafb](/index.php/Uvesafb "Uvesafb")来适配大屏分辨率。

如果既没有KMS也没有framebuffer，那么Plymouth将使用文本模式。

## 安装

从[AUR](/index.php/AUR "AUR")中安装Plymouth:[plymouth](https://aur.archlinux.org/packages/plymouth/)是稳定版本而[plymouth-git](https://aur.archlinux.org/packages/plymouth-git/)是开发版本。

如果你使用的是[GDM](/index.php/GDM "GDM"),那么你需要安装[gdm-plymouth](https://aur.archlinux.org/packages/gdm-plymouth/),这个版本编译时加入了 plymouth 支持。

### plymouth 钩子

把 `plymouth` 添加到 [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") 的 HOOKS行，且**必须**在"base","udev"**之后**：

 `/etc/mkinitcpio.conf`  `HOOKS="base udev plymouth [...] "` 
**警告:**

*   如果你使用 **encrypt** 钩子进行[硬盘加密](/index.php/System_Encryption_with_LUKS_for_dm-crypt "System Encryption with LUKS for dm-crypt")，你*必须* 使用**plymouth-encrypt** 替代`encrypt` 以便提示输入TTY 密码.
*   `plymouth-encrypt` 钩子不支持在 `cryptdevice=` 中使用 PARTUUID 或 PARTLABEL 参数。
*   对于根目录使用了[加密的ZFS文件系统](/index.php/Install_Arch_Linux_on_ZFS#Native_encryption "Install Arch Linux on ZFS")的用户，你必须安装[plymouth-zfs](https://aur.archlinux.org/packages/plymouth-zfs/)并用`plymouth-zfs`钩子替换`zfs`钩子。

加入了`plymouth-encrypt`钩子后，如果输入的密码不是以密码提示而是以明文形式传递到后台，你需要添加你的（内核）显卡驱动到initramfs中。例如，假设你在使用intel核显：

 `/etc/mkinitcpio.conf`  `MOUDLES=(i915 [...])` 

可能有些主题的启动也需要这么做。

### 其他的Plymouth钩子（搭配Systemd钩子）

如果你的[mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf")文件中包含了`systemd`钩子，那么将`plymouth`钩子替换为`sd-plymouth`钩子。此外，如果使用了硬盘加密，用`sd-encrypt`钩子替换`encrypt`或`plymouth-encrypt`:

 `/etc/mkinitcpio.conf`  `HOOKS=(base systemd sd-plymouth [...] sd-encrypt [...])` 

### 内核命令行

你需要通过引导程序[向内核传递参数](/index.php/Kernel_parameters "Kernel parameters")`quiet splash loglevel=3 rd.udev.log_priority=3 vt.global_cursor_default=0`。查看[Silent boot](/index.php/Silent_boot "Silent boot")词条查看更多影响终端输出的参数。

重建 initrd 镜像（见[mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")词条查看细节），例如：

```
# mkinitcpio -p linux

```

## 配置

### 平滑过渡

要启用平滑过渡，需要：

1.  禁用 [Display manager](/index.php/Display_manager "Display manager")，例如 `systemctl disable gdm.service`
2.  启用对应的 plymouth 服务(支持 GDM, LXDM, SLiM), 例如`systemctl enable gdm-plymouth.service`

### 显示延迟

自0.9.0版 plymouth 在/etc/plymouth/plymouthd.conf有一个新选项

 `/etc/plymouth/plymouthd.conf` 
```
[Daemon]
Theme=spinner
ShowDelay=5
```

对于启动很快的系统，在显示登陆框时会出现屏幕闪烁。可以设置 ShowDelay 为一个比启动时间更长的值，默认是 5 秒，可以根据机器状况进行调节。

### 更改主题

Plymouth自带了一些主题：

1.  **Fade-in**: "简单的有淡出淡入的星星的主题"
2.  **Glow**: "伴随着新兴标志的饼状引导进度条的企业主题"
3.  **Script**: "脚本案例插件" (漂亮的Arch Logo主题)
4.  **Solar**: "带有燃烧的蓝色星球的空间主题"
5.  **Spinner**: "带有加载框的简单主题"
6.  **Spinfinity**: "显示旋转的无穷大标志的主题"
7.  **Text**: "三种颜色的进度条(Fedora默认的白、浅蓝、蓝启动进度条)")
8.  **Details**: "详细的启动信息滚动输出"

开发版本的Plymouth([plymouth-git](https://aur.archlinux.org/packages/plymouth-git/))支持**BGRT**(Boot Graphics Resource Table)主题，它的样子是在可以的情况下显示带有OEM图标的Spinner主题。

此外你还可以在[AUR](/index.php/AUR "AUR")里安装其他主题，可以从[plymouth](https://aur.archlinux.org/packages/plymouth/)被依赖列表中甄选出主题。

显示当前主题:

```
$ plymouth-set-default-theme

```

你可以使用以下命令获得已安装的主题列表：

```
$ plymouth-set-default-theme -l

```

或是通过：

 `$ ls /usr/share/plymouth/themes` 
```
details golw solar spinner tribar 
fade-in script spinfinity text

```

默认选择**spinner**.你可以修改`/etc/plymouth/plymouthd.conf`文件来更改主题, 例如:

 `/etc/plymouth/plymouthd.conf` 
```
[Daemon]
Theme=spinner
ShowDelay=5
```

要不重启预览主题。按 Ctrl+Alt+F6 切换终端，使用root登陆：

```
# plymouthd
# plymouth --show-splash

```

再按Ctrl+Alt+F6并输入如下命令退出预览：

```
# plymouth --quit

```

设置你喜欢的主题：

 `# plymouth-set-default-theme -R <theme name>` 

重启。

## 提示与技巧

### 显示内核消息

启动时按 "Home" 或 "Escape" 按键会显示内核消息。

### 替换Arch Logo和创建自定义主题

fade-in, script, solar, spinfinity这些主题使用的Logo是由Plymouth在`/usr/share/plymouth/arch-logo.png`提供的。如果你想使用其他Logo，你可以从这些主题中选取或者从[AUR](/index.php/AUR "AUR")的Plymouth主题中选取，然后编辑*.plymouth（有时会编辑*.script），最后用所选择的图片替换。你应该创建一个新的主题安装包，因为`/usr/share/plymouth`中的文件可能不会通过升级软件而改变。

安装或者选择主题之后，应该重建initrd映像，使得新的主题生效。

## 请参阅

*   [Original Spec](http://fedoraproject.org/wiki/Releases/FeatureBetterStartup)
*   [Related forum thread](https://bbs.archlinux.org/viewtopic.php?id=81406)