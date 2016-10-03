**翻译状态：** 本文是英文页面 [Plymouth](/index.php/Plymouth "Plymouth") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-07，点击[这里](https://wiki.archlinux.org/index.php?title=Plymouth&diff=0&oldid=445529)可以查看翻译后英文页面的改动。

[Plymouth](http://fedoraproject.org/wiki/Releases/FeatureBetterStartup) 是一个来自于Fedora社区的提供美化启动图形界面的功能的项目。它依靠[KMS](/index.php/KMS "KMS")尽可能早的设置显示器的原始分辨率显示，之后产生美化的启动引导界面直至登陆界面。

## Contents

*   [1 准备](#.E5.87.86.E5.A4.87)
*   [2 安装](#.E5.AE.89.E8.A3.85)
    *   [2.1 plymouth 钩子](#plymouth_.E9.92.A9.E5.AD.90)
    *   [2.2 内核命令行](#.E5.86.85.E6.A0.B8.E5.91.BD.E4.BB.A4.E8.A1.8C)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 平滑过渡](#.E5.B9.B3.E6.BB.91.E8.BF.87.E6.B8.A1)
    *   [3.2 显示延迟](#.E6.98.BE.E7.A4.BA.E5.BB.B6.E8.BF.9F)
    *   [3.3 更改主题](#.E6.9B.B4.E6.94.B9.E4.B8.BB.E9.A2.98)
*   [4 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [4.1 显示内核消息](#.E6.98.BE.E7.A4.BA.E5.86.85.E6.A0.B8.E6.B6.88.E6.81.AF)
    *   [4.2 替换Arch Logo和创建自定义主题](#.E6.9B.BF.E6.8D.A2Arch_Logo.E5.92.8C.E5.88.9B.E5.BB.BA.E8.87.AA.E5.AE.9A.E4.B9.89.E4.B8.BB.E9.A2.98)
*   [5 请参阅](#.E8.AF.B7.E5.8F.82.E9.98.85)

## 准备

Plymouth 依靠 [KMS](/index.php/KMS "KMS") (Kernel Mode Setting) 显示图形界面。如果你无法使用KMS(例如使用闭源驱动)，那么就需要使用[framebuffer](/index.php/Framebuffer#Framebuffer_Resolution "Framebuffer")代替。EFI/UEFI 系统中，plymouth 可以使用 EFI framebuffer, 否则就使用[Uvesafb](/index.php/Uvesafb "Uvesafb")。

如果既没有KMS也没有framebuffer，那么Plymouth将使用文本模式。

## 安装

从[AUR](/index.php/AUR "AUR")中安装Plymouth:[plymouth](https://aur.archlinux.org/packages/plymouth/)是稳定版本而[plymouth-git](https://aur.archlinux.org/packages/plymouth-git/)是开发版本。

如果你使用的是[GDM](/index.php/GDM "GDM"),那么你需要安装[gdm-plymouth](https://aur.archlinux.org/packages/gdm-plymouth/),这个版本编译时加入了 plymouth 支持。

在非官方源[nullptr_t](/index.php/Unofficial_user_repositories#nullptr_t "Unofficial user repositories")也有支持。

### plymouth 钩子

把 `plymouth` 添加到 [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") 的 HOOKS行，且**必须**在"base","udev"**之后**：

 `/etc/mkinitcpio.conf`  `HOOKS="base udev plymouth [...] "` 
**警告:**

*   如果你使用 **encrypt** 钩子进行[硬盘加密](/index.php/System_Encryption_with_LUKS_for_dm-crypt "System Encryption with LUKS for dm-crypt")，你*必须* 使用**plymouth-encrypt** 替代`encrypt` 以便提示输入TTY 密码.
*   `plymouth-encrypt` 钩子不支持在 `cryptdevice=` 中使用 PARTUUID 参数。

### 内核命令行

你需要在引导程序设置`quiet splash`参数。查看[Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") 了解更多。

重建 initrd 镜像：

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

1.  Fade-in: "简单的有淡出淡入的星星的主题"
2.  Glow: "伴随着新兴标志的饼状引导进度条的企业主题"
3.  Script: "脚本案例插件" (漂亮的Arch Logo主题)
4.  Solar: "带有燃烧的蓝色星球的空间主题"
5.  Spinner: "带有加载框的简单主题"
6.  Spinfinity: "显示旋转的无穷大标志的主题"
7.  Text: "三种颜色的进度条(Fedora默认的白、浅蓝、蓝启动进度条)")
8.  Details: "详细的启动信息滚动输出"

显示当前主题:

 `plymouth-set-default-theme ` 

你可以使用以下命令获得已安装的主题列表：

 `plymouth-set-default-theme -l` 

默认选择**spinner**.你可以修改`/etc/plymouth/plymouthd.conf`文件来更改主题, 例如:

 `/etc/plymouth/plymouthd.conf` 
```
[Daemon]
Theme=spinner
ShowDelay=5
```

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

### 显示内核消息

启动时按 "Home" 或 "Escape" 按键会显示内核消息。

### 替换Arch Logo和创建自定义主题

fade-in, script, solar, spinfinity这些主题使用的Logo是由Plymouth在`/usr/share/plymouth/arch-logo.png`提供的。如果你想使用其他Logo，你可以从这些主题中选取或者从[AUR](/index.php/AUR "AUR")的Plymouth主题中选取，然后编辑*.plymouth（有时会编辑*.script），最后用所选择的图片替换。你应该创建一个新的主题安装包，因为`/usr/share/plymouth`中的文件可能不会通过升级软件而改变。

安装或者选择主题之后，应该重建initrd映像，使得新的闪屏生效。

## 请参阅

*   [Original Spec](http://fedoraproject.org/wiki/Releases/FeatureBetterStartup)
*   [Related forum thread](https://bbs.archlinux.org/viewtopic.php?id=81406)