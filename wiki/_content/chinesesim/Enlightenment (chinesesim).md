**翻译状态：** 本文是英文页面 [Enlightenment](/index.php/Enlightenment "Enlightenment") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-04-18，点击[这里](https://wiki.archlinux.org/index.php?title=Enlightenment&diff=0&oldid=254514)可以查看翻译后英文页面的改动。

[Enlightenment - Enlightenment](http://trac.enlightenment.org/e/wiki/Enlightenment) 的描述：

	*Enlightenment* 桌面环境基于 Enlightenment Foundation Libraries 与其他基本的如文件管理器、桌面图标和部件等的桌面环境组件，提供了一个高效而又惊艳的窗口管理器。它的优势在于：在提供了前所未有的定制主题的能力的同时仍然能在老旧的硬件和嵌入式设备上运行流畅。

## Contents

*   [1 Enlightenment Desktop Shell (之前的 E17)](#Enlightenment_Desktop_Shell_.28.E4.B9.8B.E5.89.8D.E7.9A.84_E17.29)
*   [2 安装](#.E5.AE.89.E8.A3.85)
    *   [2.1 使用 extra 仓库](#.E4.BD.BF.E7.94.A8_extra_.E4.BB.93.E5.BA.93)
    *   [2.2 从AUR安装](#.E4.BB.8EAUR.E5.AE.89.E8.A3.85)
*   [3 启动 Enlightenment](#.E5.90.AF.E5.8A.A8_Enlightenment)
    *   [3.1 startx](#startx)
    *   [3.2 Entrance](#Entrance)
    *   [3.3 其它](#.E5.85.B6.E5.AE.83)
*   [4 配置网络](#.E9.85.8D.E7.BD.AE.E7.BD.91.E7.BB.9C)
    *   [4.1 connman](#connman)
    *   [4.2 NetworkManager](#NetworkManager)
*   [5 配置输入法](#.E9.85.8D.E7.BD.AE.E8.BE.93.E5.85.A5.E6.B3.95)
    *   [5.1 ibus](#ibus)
*   [6 安装主题](#.E5.AE.89.E8.A3.85.E4.B8.BB.E9.A2.98)
*   [7 Modules and Gadgets](#Modules_and_Gadgets)
    *   [7.1 Places](#Places)
    *   [7.2 缩放窗口](#.E7.BC.A9.E6.94.BE.E7.AA.97.E5.8F.A3)
        *   [7.2.1 Engage](#Engage)
*   [8 集成 Gnome Keyring](#.E9.9B.86.E6.88.90_Gnome_Keyring)
*   [9 故障及解决办法](#.E6.95.85.E9.9A.9C.E5.8F.8A.E8.A7.A3.E5.86.B3.E5.8A.9E.E6.B3.95)
    *   [9.1 屏幕解锁不工作](#.E5.B1.8F.E5.B9.95.E8.A7.A3.E9.94.81.E4.B8.8D.E5.B7.A5.E4.BD.9C)
    *   [9.2 难以分辨的字体](#.E9.9A.BE.E4.BB.A5.E5.88.86.E8.BE.A8.E7.9A.84.E5.AD.97.E4.BD.93)
    *   [9.3 无法挂载内部分区](#.E6.97.A0.E6.B3.95.E6.8C.82.E8.BD.BD.E5.86.85.E9.83.A8.E5.88.86.E5.8C.BA)
*   [10 相关链接](#.E7.9B.B8.E5.85.B3.E9.93.BE.E6.8E.A5)

## Enlightenment Desktop Shell (之前的 E17)

包括 Enlightment [窗口管理器](/index.php/Window_Manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window Manager (简体中文)")和提供了如工具包、对象画布和抽象对象等额外的桌面环境特性的 Enlightenment Foundation Libraries(EFL) 。从 2005 年开始开发，并在 2011 年 2 月发布第一个稳定的 1.0 发行版。Enlightenment 窗口管理器已于 2012 年 12 月 21 日发布，EFL 库的 1.7.4 版也同期发布。目前很多人可以毫无障碍地将 Enlightenment 作为日常桌面环境使用。

**Warning:** This page refers to both stable and development packages. Any PKGBUILD which ends with -svn or -git will use unstable development code. Use them at your own risk. Since the release of the EFL libraries and Enlightenment itself, it's no longer necessary and even discouraged to build the core programs from SVN or GIT. "Unless you're developing E or willing to live bleeding edge, stay away from trunk."([source](http://sourceforge.net/mailarchive/message.php?msg_id=30310890)) Unfortunately, many of the additional software packages have not been released and building from SVN or GIT is the only way to use them.

## 安装

### 使用 extra 仓库

安装 Enlightenment：

```
pacman -S enlightenment17

```

安装 e17 的附加模块以及应用程序

```
pacman -S e-modules-extra-svn

```

你或许需要安装额外的 [字体](/index.php/Fonts "Fonts") ，至少需要一个 True Type 字体。详见 [桌面环境推荐使用的字体](/index.php/Fonts#Desktop_environments "Fonts") 。

如果你需要的 e17 软件包不在 extra 仓库，可以看看在不在[AUR](/index.php/AUR "AUR")中。

### 从AUR安装

可以从 AUR 上下载[enlightenment17-git](https://aur.archlinux.org/packages/enlightenment17-git/)得到最新的 SVN 版源码及其依赖的包构建文件（PKGBUILDs）。

## 启动 Enlightenment

### startx

如果你用 `startx` 或者一个简单的 [Display manager](/index.php/Display_manager "Display manager") ，比如 XDM 或者 [SLiM](/index.php/SLiM "SLiM") 的话，在 [xinitrc](/index.php/Xinitrc "Xinitrc") 中添加下面的命令：

```
exec enlightenment_start

```

### Entrance

Enlightenment 现在提供了新的显示管理器 Entrance，可以通过 [entrance-git](https://aur.archlinux.org/packages/entrance-git/) 软件包从 [AUR](/index.php/AUR "AUR") 安装。通过 `/etc/entrance.conf` 配置。要使用entrance：

```
 # systemctl enable entrance.service 

```

### 其它

更高级一点的显示管理器，比如 [GDM](/index.php/GDM "GDM") 和 [KDM](/index.php/KDM "KDM") 会自动检测到 E17。这多亏了 [enlightenment17](https://www.archlinux.org/packages/?name=enlightenment17) 软件包里的 `/usr/share/xsessions/enlightenment.desktop` 文件。

## 配置网络

### connman

E17 推荐的网络管理器是 [Connman](/index.php/Connman "Connman")，可以通过 [community] 软件仓库中的[connman](https://www.archlinux.org/packages/?name=connman)软件包进行安装。}} 。为了与 Enlightenment 的默认网络模块交互工作，需要安装[AUR](/index.php/AUR "AUR") 中的 [econnman](https://aur.archlinux.org/packages/econnman/) 或 [econnman-git](https://aur.archlinux.org/packages/econnman-git/)。

设置为开机启动:

```
systemctl enable connman.service

```

ConnMan 启动很快并能自动配置 DHCP。如果你安装了 [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") ，ConnMan 会使用它显示所有可用的无线连接。

### NetworkManager

你可以使用 [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) 来管理网络连接。

```
pacman -S networkmanager

```

然后你就可以按照 [NetworkManager](/index.php/NetworkManager "NetworkManager") 页面里的指示配置就可以了。你也可以使用 [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) 来帮助你设置。

```
pacman -S network-manager-applet

```

你可以将它设置成自动启动程序，以便每次 E17 启动时，它都在系统托盘中：

```
Settings -> Settings Panel -> Apps -> Startup Applications -> System -> Network

```

## 配置输入法

E17 内置了输入法支持的模块，支持的输入法有 iiimf 、scim 和 uim 。使用这些输入法的配置在

```
Settings -> Settings Panel -> Language -> Input Method Settings -> Advanced

```

System 配置中，使用者只需选择即可。使用其他输入法的用户可以在 Personal 配置中添加。

### ibus

ibus 的配置参数为：

```
Input Method Parameters:
 Name              ibus
 Execute Command   /usr/bin/ibus-daemon --xim
 Setup Command     /usr/bin/ibus-setup

```

```
Exported Environment Variables:
 GTK_IM_MODULE     ibus
 QT_IM_MODULE      ibus
 XMODIFIERS        @im=ibus

```

## 安装主题

更多的定制主题可以见下面：

*   [exchange.enlightenment.org](http://exchange.enlightenment.org) ，你可以使用 AUR 的 [e17-themes](https://aur.archlinux.org/packages/e17-themes/) 来安装上面的内容。
*   [e17-stuff.org](http://www.e17-stuff.org).

.edj 格式的主题文件可以从配置对话框安装，2010 年的时候主题的管理方式产生了变化，所以要使用老主题，需要先运行：

```
edje_convert <theme>.edj

```

**注意:** edje_convert 二进制转换器已经不被上游支持，参见: [trac.enlightenment.org](http://trac.enlightenment.org/e/changeset/56156)

同时还可以修改 etk toolkit 的主题，通过 `etk_prefs` 可以启动 etk toolkit 配置。

## Modules and Gadgets

	Module

	在 enlightenment 中指 gadget 的后端代码。

	Gadget

	前端或用户界面，可以帮助 Enlightenment 用户完成某种功能。

许多模块提供了可以加入桌面或 shelf 的 Gadgets，有些模块如 CPUFreq 仅提供了单一的 Gadget，而其他模块如 Composite 没有任何 gadgets，但是提供了附加功能。注意有些 gadgets 如 Systray 仅能加入 shelf 而其他模块如 Moon 仅能放到桌面上。

### Places

Places 源代码中的 [README](http://trac.enlightenment.org/e/browser/trunk/E-MODULES-EXTRA/places/README):

	Places module

	*This module manage the volumes device attached to the system.*

Places 是一个帮助用户浏览文件和设备的插件，支持的设备包括电话、摄像机或其他各种 USB 存储设备。

**Note:** e17中这一模组已非必需

### 缩放窗口

*Scale Windows* 模块需要启用 compositing，可以将所有打开的窗口缩小到一个屏幕。可以加入桌面或通过快捷键启用。

可以将 `ALT + Tab` 绑定到 Scale Windows 以进行窗口选择，进入 `Menu > Settings > Settings Panel > Input > Keys`，按照喜好进行按键设置。

要将窗口选择快捷键绑定到 Scale Windows，在左边面板中找到 "ALT" 部分并选中 `ALT + Tab`，然后在左边窗口中找到 "Scale Windows" 部分，然后选择 `Select Next` 或 `Select Next (All)`，区别在于要显示所有桌面的窗口还是当前桌面的窗口。点击 "Apply" 保存绑定。

**Note:** 在[extra]中这个模块已非必要。如果需要，应当安装 AUR 中的[comp-scale-svn](https://aur.archlinux.org/packages/comp-scale-svn/)

##### Engage

Engage is CairoDock/GLX-Dock style docking bar for both application launchers and open applications. It requires compositing to be enabled and has full controls for transparency, size, zoom levels, and more.

Available from [engage-svn](https://aur.archlinux.org/packages/engage-svn/)

## 集成 Gnome Keyring

e17可以使用 Gnome Keyring 。为使其正常运作，你需要做如下一些工作： 依次点击 配置面板 -> 应用程序 -> 启动应用程序，激活“保存证书与密钥”、“GPG 口令代理”、“SSH 密钥代理”和“安全存储服务”； 编辑~/.profile文件，添加下列代码：

```
if [ -n "$GNOME_KEYRING_PID" ]; then
    eval $(gnome-keyring-daemon --start)
    export SSH_AUTH_SOCK
    export GNOME_KEYRING_CONTROL
    export GPG_AGENT_INFO
fi

```

## 故障及解决办法

如果你遇到了预料之外的程序行为，可以试试下面的方法：

1.  在默认的主题中看此行为是否还存在
2.  备份 `~/.e` 然后将其删除。 (比如：`mv ~/.e ~/.e.back`)

如果你确定你发现了一个 bug ，请直接向上游提交。 [http://trac.enlightenment.org/e/report](http://trac.enlightenment.org/e/report)

### 屏幕解锁不工作

如果屏幕锁不接受你的密码，在 `/etc/pam.d/enlightenment` 中添加下面一行：

```
auth required pam_unix_auth.so

```

### 难以分辨的字体

如果字体太小难以辨认，确认你安装了正确的软件包：

```
pacman -S ttf-dejavu ttf-bitstream-vera

```

### 无法挂载内部分区

检查用户是否属于 storage 组：

 `# groups <user>` 

如果不是：

```
# groupadd storage 
# gpasswd -a <user> storage
```

然后创建文件：

 `# nano /etc/polkit-1/localauthority/50-local.d/10-storage-group-mount-override.pkla` 

并加入：

```
[storage group mount override]
Identity=unix-group:storage
Action=org.freedesktop.udisks2.filesystem-mount-system
ResultAny=yes
ResultInactive=yes
ResultActive=yes

```

详情参见[论坛帖子](http://bbs.archbang.org/viewtopic.php?id=2720).

## 相关链接

*   [exchange.enlightenment.org](http://exchange.enlightenment.org/)
*   [e17-stuff.org](http://e17-stuff.org/)
*   [Bodhi Guide to Enlightenment](http://www.bodhilinux.com/e17guide/e17guideEN/)