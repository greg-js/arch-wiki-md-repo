相关文章

*   [Display manager](/index.php/Display_manager "Display manager")
*   [KDE (简体中文)](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)")

**翻译状态：** 本文是英文页面 [SDDM](/index.php/SDDM "SDDM") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-12-19，点击[这里](https://wiki.archlinux.org/index.php?title=SDDM&diff=0&oldid=349882)可以查看翻译后英文页面的改动。

[Simple Desktop Display Manager](https://en.wikipedia.org/wiki/Simple_Desktop_Display_Manager 。 维基百科介绍：

	*Simple Desktop Display Manager (SDDM) 是用于X11和wayland视窗系统的显示管理器（图形登录界面）。 SDDM 使用C++11重写并且支持通过 QML改变主题。它是KDM的接替者并且与KDE Frameworks 5, KDE Plasma 5 和 KDE Applications 5协同使用。*

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 自动登录](#.E8.87.AA.E5.8A.A8.E7.99.BB.E5.BD.95)
    *   [2.2 主题设置](#.E4.B8.BB.E9.A2.98.E8.AE.BE.E7.BD.AE)
        *   [2.2.1 主设置](#.E4.B8.BB.E8.AE.BE.E7.BD.AE)
        *   [2.2.2 编辑主题](#.E7.BC.96.E8.BE.91.E4.B8.BB.E9.A2.98)
        *   [2.2.3 光标](#.E5.85.89.E6.A0.87)
        *   [2.2.4 修改头像](#.E4.BF.AE.E6.94.B9.E5.A4.B4.E5.83.8F)
*   [3 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [3.1 登陆后挂起](#.E7.99.BB.E9.99.86.E5.90.8E.E6.8C.82.E8.B5.B7)
    *   [3.2 KDE Plasma 中无桌面特效](#KDE_Plasma_.E4.B8.AD.E6.97.A0.E6.A1.8C.E9.9D.A2.E7.89.B9.E6.95.88)
    *   [3.3 SDDM 在 tty1 中开启，而不是tty7](#SDDM_.E5.9C.A8_tty1_.E4.B8.AD.E5.BC.80.E5.90.AF.EF.BC.8C.E8.80.8C.E4.B8.8D.E6.98.AFtty7)

## 安装

从 [官方仓库](/index.php/Official_repositories "Official repositories")[安装](/index.php/Pacman "Pacman")[sddm](https://www.archlinux.org/packages/?name=sddm) 软件包。

然后按照 [Display manager (简体中文)#加载显示管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.8A.A0.E8.BD.BD.E6.98.BE.E7.A4.BA.E7.AE.A1.E7.90.86.E5.99.A8 "Display manager (简体中文)") 的说明配置SDDM在系统引导时启动。

## 配置

SDDM的配置文件为 `/etc/sddm.conf` 。运行 [sddm.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/sddm.conf.5) 可以了解所有的选项。

在使用了 [systemd](/index.php/Systemd "Systemd") 的系统中, 由于 SDDM 默认使用 `systemd-logind` 管理会话，无需作额外的设置，因此安装SDDM时将不会产生配置文件。如果你确实需要修改配置文件，SDDM提供了一个命令用于产生一个包含了默认设置的配置文件样本:

```
# sddm --example-config > /etc/sddm.conf

```

### 自动登录

与 KDM相似 , SDDM 支持修改配置文件实现自动登录, 例如:

 `/etc/sddm.conf` 
```
[Autologin]
User=john
Session=kde-plasma.desktop
```

以上的配置文件使得系统启动时自动以用户`john`开启一个KDE Plasma会话。支持的会话类型可以在 `ls /usr/share/xsessions/`中找到。

**Warning:** 如果配置不当, 自动登录可以使能够接触到你的电脑的攻击者毫不费力地进入你的桌面。只有当你有其他认证方式保证系统安全时才应该开启自动登录，比如 [根文件系统加密](/index.php/Encrypted_Root_Filesystem "Encrypted Root Filesystem")。

目前尚不支持自动登录的同时锁定会话[[1]](https://github.com/sddm/sddm/issues/306)。

### 主题设置

在`[Theme]`部分中更改主题设置。 可以在[AUR](/index.php/AUR "AUR")获得一些主题, 例如[archlinux-themes-sddm](https://aur.archlinux.org/packages/archlinux-themes-sddm/)。

#### 主设置

在`Current`值中设置当前主题, 例如`Current=archlinux-simplyblack`。

#### 编辑主题

SDDM的默认主题目录是`/usr/share/sddm/themes/`。可以将您定制的主题添加到该目录的子目录下。研究创建修改或安装您自己的主题的文件。

#### 光标

要设置鼠标光标，请将`CursorTheme` 设置为您选择的光标。

#### 修改头像

您可以将一个简单的`png`图像重命名为`username.face.icon`并放在默认目录`/usr/share/sddm/faces/`下。或者也可以更改默认目录来满足你的欲望, 例如`FacesDir=/var/lib/AccountsService/icons/`。

## 故障排除

### 登陆后挂起

尝试删除*~/.Xauthority*。

### KDE Plasma 中无桌面特效

从KDM换为SDDM并登录KDE Plasma 4后，桌面特效被禁用且无法开启，似乎是由于SDDM错误地以"Failsafe"模式启动KDE Plasma。此时注销并且在SDDM界面中更换会话类型即可。

### SDDM 在 tty1 中开启，而不是tty7

由于 [systemd 的原因](http://0pointer.de/blog/projects/serial-console.html) ，SDDM默认在tty1开启第一个图形会话。如果你喜欢以前 tty1 到 tty6 作为文本终端的习惯, 将下面内容加入 `sddm.conf`:

 `/etc/sddm.conf` 
```
[XDisplay]
MinimumVT=7
```