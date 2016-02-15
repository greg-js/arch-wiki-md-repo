**翻译状态：** 本文是英文页面 [Plymouth](/index.php/Plymouth "Plymouth") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-07-16，点击[这里](https://wiki.archlinux.org/index.php?title=Plymouth&diff=0&oldid=213045)可以查看翻译后英文页面的改动。

[Plymouth](http://fedoraproject.org/wiki/Releases/FeatureBetterStartup) 是一个来自于Fedora社区的提供美化启动图形界面的功能的项目。它依靠[KMS](https://wiki.archlinux.org/index.php/Kernel_mode_setting)尽可能早的设置显示器的原始分辨率显示，之后产生美化的启动引导界面直至登陆界面。

## Contents

*   [1 准备](#.E5.87.86.E5.A4.87)
*   [2 安装](#.E5.AE.89.E8.A3.85)
    *   [2.1 在Initcpio中包含Plymouth](#.E5.9C.A8Initcpio.E4.B8.AD.E5.8C.85.E5.90.ABPlymouth)
    *   [2.2 内核命令行](#.E5.86.85.E6.A0.B8.E5.91.BD.E4.BB.A4.E8.A1.8C)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 显示延迟](#.E6.98.BE.E7.A4.BA.E5.BB.B6.E8.BF.9F)
    *   [3.2 更改主题](#.E6.9B.B4.E6.94.B9.E4.B8.BB.E9.A2.98)
*   [4 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [4.1 Replacing the Arch Logo](#Replacing_the_Arch_Logo)
*   [5 请参阅](#.E8.AF.B7.E5.8F.82.E9.98.85)

## 准备

**警告:** Plymouth目前正在开发中，可能存在bug。

Plymouth primarily uses to display graphics. Plymouth依靠 [KMS](/index.php/KMS "KMS") (Kernel Mode Setting) 显示图形界面。如果你无法使用KMS(例如使用闭源驱动)，那么就需要使用[framebuffer](/index.php/Framebuffer#Framebuffer_Resolution "Framebuffer")代替。

如果既没有KMS也没有framebuffer，那么Plymouth将使用文本模式。

## 安装

从[AUR](/index.php/AUR "AUR")中安装Plymouth:[plymouth](https://aur.archlinux.org/packages/plymouth/)是稳定版本而[plymouth-git](https://aur.archlinux.org/packages/plymouth-git/)是开发版本。

如果你使用的是[KDM](/index.php/KDM "KDM"),那么你需要安装[kdebase-workspace-plymouth](https://aur.archlinux.org/packages/kdebase-workspace-plymouth/),否则KDM可能不能正常启动。

如果你使用的是[GDM](/index.php/GDM "GDM"),那么你需要安装[gdm-plymouth](https://aur.archlinux.org/packages/gdm-plymouth/), which compiles gdm with plymouth support。

### 在Initcpio中包含Plymouth

把Plymouth添加到`/etc/[mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf")`的HOOKS一行，且"必须"在"base","udev"之后"：

 `/etc/mkinitcpio.conf`  `HOOKS="base udev plymouth[...] "` 
**警告:** 如果你使用 **encrypt** hook[硬盘加密](/index.php/System_Encryption_with_LUKS_for_dm-crypt "System Encryption with LUKS for dm-crypt")，你_必须_ 使用**plymouth-encrypt** 替代以便提示输入TTY 密码

对于早期KMS，需要添加模块到 `/etc/mkinitcpio.conf`中的MODULES 行， [radeon](/index.php/Radeon "Radeon") (ATI显卡), [i915](/index.php/Intel "Intel") (Intel显卡) or [nouveau](/index.php/Nouveau "Nouveau") (nvidia显卡)：

 `/etc/mkinitcpio.conf` 

```
MODULES="i915"
**or**
MODULES="radeon"
**or**
MODULES="nouveau"
```

### 内核命令行

你需要在引导程序设置`quiet splash`参数。查看[Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") 了解更多

```
# mkinitcpio -p linux

```

## 配置

### 显示延迟

自0.9.0版 plymouth 在/etc/plymouth/plymouthd.conf有一个新选项

 `/etc/plymouth/plymouthd.conf` 

```
[Daemon]
Theme=spinner
ShowDelay=5
```

On systems that boot quickly, you may only see a flicker of your splash theme before your DM or login prompt is ready. You can set ShowDelay to an interval (in seconds) longer than your boot time to prevent this flicker and only show a blank screen. The default is 5 seconds, but you may wish to change this to a lower value to see your splash earlier during boot.

### 更改主题

Plymouth自带了一些主题：

1.  Fade-in: "简单的有淡出淡入的星星的主题"
2.  Glow: "伴随着新兴标志的饼状引导进度条的企业主题"
3.  Script: "脚本案例插件" (漂亮的Arch Logo主题)
4.  Solar: "带有燃烧的蓝色星球的空间主题"
5.  Spinner: "带有加载框的简单主题"
6.  Spinfinity: "显示旋转的无穷大标志的主题"
7.  Text: "三种颜色的进度条(Fedora默认的白、浅蓝、蓝启动进度条)")
8.  Details: "详细的启动信息滚动输出"

默认选择**spinner**.你可以修改`/etc/plymouth/plymouthd.conf`文件来更改主题, 例如:

 `/etc/plymouth/plymouthd.conf` 

```
[Daemon]
Theme=spinner
ShowDelay=5
```

显示当前主题:

 `plymouth-set-default-theme ` 

你可以使用以下命令获得已安装的主题列表：

 `plymouth-set-default-theme -l` 

要不重启预览主题。按 Ctrl+Alt+F2 切换终端，使用root登陆：

```
#plymouthd
#plymouth --show-splash
```

再按Ctrl+Alt+F2退出预览并输入：

 `#plymouth --quit` 

设置你喜欢的主题：

 `# plymouth-set-default-theme -R <theme name>` 

重启。

## 提示与技巧

During boot you can switch to kernel messages by pressing "Home" (or "Escape") key.

### Replacing the Arch Logo

The following themes use the Arch Linux logo supplied by Plymouth in `/usr/share/plymouth/arch-logo.png`: fade-in, script, solar, spinfinity. Replacing this image with one of your choice and rebuilding the initrd image will give you your new splash image with the theme of your choice.

## 请参阅

*   [Original Spec](http://fedoraproject.org/wiki/Releases/FeatureBetterStartup)
*   [Related forum thread](https://bbs.archlinux.org/viewtopic.php?id=81406)