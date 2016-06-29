**翻译状态：** 本文是英文页面 [Enlightenment](/index.php/Enlightenment "Enlightenment") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-04-18，点击[这里](https://wiki.archlinux.org/index.php?title=Enlightenment&diff=0&oldid=254514)可以查看翻译后英文页面的改动。

## Contents

*   [1 Enlightenment](#Enlightenment)
    *   [1.1 安装](#.E5.AE.89.E8.A3.85)
        *   [1.1.1 从AUR安装](#.E4.BB.8EAUR.E5.AE.89.E8.A3.85)
    *   [1.2 启动 Enlightenment](#.E5.90.AF.E5.8A.A8_Enlightenment)
        *   [1.2.1 Entrance](#Entrance)
        *   [1.2.2 手动启动 Enlightenment](#.E6.89.8B.E5.8A.A8.E5.90.AF.E5.8A.A8_Enlightenment)
    *   [1.3 配置](#.E9.85.8D.E7.BD.AE)
        *   [1.3.1 网络](#.E7.BD.91.E7.BB.9C)
*   [2 配置输入法](#.E9.85.8D.E7.BD.AE.E8.BE.93.E5.85.A5.E6.B3.95)
    *   [2.1 ibus](#ibus)
*   [3 安装主题](#.E5.AE.89.E8.A3.85.E4.B8.BB.E9.A2.98)
*   [4 Modules and Gadgets](#Modules_and_Gadgets)
    *   [4.1 Places](#Places)
    *   [4.2 缩放窗口](#.E7.BC.A9.E6.94.BE.E7.AA.97.E5.8F.A3)
        *   [4.2.1 Engage](#Engage)
*   [5 集成 Gnome Keyring](#.E9.9B.86.E6.88.90_Gnome_Keyring)
*   [6 故障及解决办法](#.E6.95.85.E9.9A.9C.E5.8F.8A.E8.A7.A3.E5.86.B3.E5.8A.9E.E6.B3.95)
    *   [6.1 屏幕解锁不工作](#.E5.B1.8F.E5.B9.95.E8.A7.A3.E9.94.81.E4.B8.8D.E5.B7.A5.E4.BD.9C)
    *   [6.2 难以分辨的字体](#.E9.9A.BE.E4.BB.A5.E5.88.86.E8.BE.A8.E7.9A.84.E5.AD.97.E4.BD.93)
    *   [6.3 无法挂载内部分区](#.E6.97.A0.E6.B3.95.E6.8C.82.E8.BD.BD.E5.86.85.E9.83.A8.E5.88.86.E5.8C.BA)
*   [7 相关链接](#.E7.9B.B8.E5.85.B3.E9.93.BE.E6.8E.A5)

## Enlightenment

这个软件包括Enlightenment [Enlightenment](https://www.enlightenment.org/) 窗体管理器[window manager](/index.php/Window_manager "Window manager") 和 Enlightenment Foundation Libraries (EFL), 他提供额外的桌面环境特性,比如工具包,对象画布抽象对象.从2005年开始开发,但2011年2月才看到1.0稳定版本.

### 安装

可以 [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 同名软件包 [enlightenment](https://www.archlinux.org/packages/?name=enlightenment) 来安装 enlightenment .

也可以安装 [terminology](https://www.archlinux.org/packages/?name=terminology), 这是一个基于ELF的终端程序 .

#### 从AUR安装

**警告:** 某些软件包是不稳定的开发版，请自己决定.

开发版本的软件包和源码及其依赖的包构建文件可以从AUR下载 [enlightenment-git](https://aur.archlinux.org/packages/enlightenment-git/) .

以下是基于EFL 的应用,大部份是开发版本，没有正式发布:

*   [econcentration-git](https://aur.archlinux.org/packages/econcentration-git/) – Econcentration 打牌游戏
*   [ecrire-git](https://aur.archlinux.org/packages/ecrire-git/) – Ecrire 文本编辑器
*   [elbow-git](https://aur.archlinux.org/packages/elbow-git/) – Elbow 浏览器
*   [eluminance-git](https://aur.archlinux.org/packages/eluminance-git/) – Eluminance 图片浏览器
*   [emprint-git](https://aur.archlinux.org/packages/emprint-git/) – Emprint 截屏工具
*   [enjoy-git](https://aur.archlinux.org/packages/enjoy-git/) – [Enjoy](https://trac.enlightenment.org/e/wiki/Enjoy) 音乐播放
*   [epad](https://aur.archlinux.org/packages/epad/) – ePad 文本编辑器
*   [eperiodique](https://aur.archlinux.org/packages/eperiodique/) – [Eperiodique](http://eperiodique.sourceforge.net/) periodic 表格查看
*   [ephoto-git](https://aur.archlinux.org/packages/ephoto-git/) – [Ephoto](https://trac.enlightenment.org/e/wiki/Ephoto) 图片查看器
*   [epour](https://aur.archlinux.org/packages/epour/) and [epour-git](https://aur.archlinux.org/packages/epour-git/) – Epour BT客户端
*   [epymc-git](https://aur.archlinux.org/packages/epymc-git/) – E Python 多媒体中心
*   [equate-git](https://aur.archlinux.org/packages/equate-git/) – Equate 计算器
*   [eruler-git](https://aur.archlinux.org/packages/eruler-git/) – Eruler 屏幕尺和测量工具
*   [efbb-git](https://aur.archlinux.org/packages/efbb-git/) – Escape from Booty Bay 愤怒的小鸟类型游戏
*   [elemines-git](https://aur.archlinux.org/packages/elemines-git/) – [Elemines](http://elemines.sourceforge.net/) 扫雷类型游戏
*   [espionage-git](https://aur.archlinux.org/packages/espionage-git/) – Espionage D-Bus 工具
*   [ev-git](https://aur.archlinux.org/packages/ev-git/) – ev 简单图片查看
*   [e_cho-git](https://aur.archlinux.org/packages/e_cho-git/) – E_Cho simon类型游戏
*   [e_jeweled-git](https://aur.archlinux.org/packages/e_jeweled-git/) – E_Jeweled 宝石类型游戏
*   [rage](https://aur.archlinux.org/packages/rage/) and [rage-git](https://aur.archlinux.org/packages/rage-git/) – Rage 视频播放器
*   [jesus-git](https://aur.archlinux.org/packages/jesus-git/) – 文件管理器

### 启动 Enlightenment

很简单，从你喜欢的[display manager](/index.php/Display_manager "Display manager")选择*Enlightenment* ， 或配置 [xinitrc](/index.php/Xinitrc "Xinitrc") 来启动 。

#### Entrance

**警告:** Entrance 还是实验性质的版本 , 还不被systemd完全支持 ，请自己决定 .

Enlightenment 有个新的显示管理器，叫Entrance, 目前由 [entrance-git](https://aur.archlinux.org/packages/entrance-git/) 提供. Entrance 很复杂，并且配置由 `/etc/entrance.conf` 管理 . 可以用命令 enable `entrance.service` 来启用 [using systemd](/index.php/Systemd#Using_units "Systemd").

#### 手动启动 Enlightenment

如果你喜欢手工启动他 , 把下面内容加入 `~/.xinitrc` 文件 :

 `~/.xinitrc` 
```
exec enlightenment_start

```

然后可以输入 `startx` 来启动 Enlightenment . 详见 [xinitrc](/index.php/Xinitrc "Xinitrc") .

### 配置

Enlightenment has a sophisticated configuration system that can be accessed from the Main menu's Settings submenu.

#### 网络

**ConnMan**

Enlightenment 首先的网络管理器是 [ConnMan](/index.php/Connman "Connman") ，包名： [connman](https://www.archlinux.org/packages/?name=connman) . 配置方法见： [Connman](/index.php/Connman "Connman") .

高多配置, 您还可以安装Econnman (通过 AUR : [econnman](https://aur.archlinux.org/packages/econnman/) 或 [econnman-git](https://aur.archlinux.org/packages/econnman-git/)) .

**把 ConnMan 放进桌面面板Shelf**

1.  设置 -> 扩展 -> 模块
2.  系统
3.  连接管理 （Connection Manager）
4.  加载
5.  屏幕底部面板右键
6.  面板Shelf -> 内容
7.  然后 ,找到 *ConnMan*.
8.  点击添加 *Add* .

**NetworkManager**

你也可以使用 [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) 来管理网络连接 . 见 [NetworkManager](/index.php/NetworkManager "NetworkManager") .

你可能也需要 [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) 的帮助 . 把他加入自动启动，这样每次进桌面就能看到他在系统托盘 . 方法是： *设置 > 全部 > 应用程序 > 启动应用程序 > 系统* ， 开启 *Network*.

如果没有 [#System tray](#System_tray)， 当网络连接时，指示器将不会显示。

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