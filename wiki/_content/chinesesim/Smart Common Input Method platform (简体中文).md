**注意:** SCIM 已经 "不被开发者维护", 而 IBus 被 Red Hat 积极开发。Arch 用户安装软件时应该考虑用 [IBus](/index.php/IBus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "IBus (简体中文)") 或 [UIM](/index.php/UIM "UIM") 而不是 [SCIM](/index.php/SCIM "SCIM")。

Su Zhe (或 James Su)在为TurboLinux工作的时候，于2001年发起了SCIM项目，该项目的目标是：

*   为当前可用的输入法库提供一个统一前端；
*   作为IIIMF输入法框架的语言引擎；
*   尽可能多地提供各国输入引擎；
*   尽可能多地支持输入法协议/接口；
*   尽可能多地支持各种操作系统。

SCIM具有以下特性：

*   使用C++编写，完全面向对象结构；
*   高度模块化
*   体系结构非常灵活，可以作为其它C/S输入法环境的动态链接库；
*   简单的编程接口
*   完全支持i18n UCS4/UTF-8编码
*   具有许多便利的工具可以加速自身开发
*   具有特性丰富的图形化面板
*   统一的配置框架

## Contents

*   [1 安装SCIM](#.E5.AE.89.E8.A3.85SCIM)
    *   [1.1 安装输入法引擎](#.E5.AE.89.E8.A3.85.E8.BE.93.E5.85.A5.E6.B3.95.E5.BC.95.E6.93.8E)
    *   [1.2 安装 SCIM-BRIDGE](#.E5.AE.89.E8.A3.85_SCIM-BRIDGE)
*   [2 配置SCIM](#.E9.85.8D.E7.BD.AESCIM)
    *   [2.1 使用kdm/gdm时自动启动scim](#.E4.BD.BF.E7.94.A8kdm.2Fgdm.E6.97.B6.E8.87.AA.E5.8A.A8.E5.90.AF.E5.8A.A8scim)
    *   [2.2 环境变量](#.E7.8E.AF.E5.A2.83.E5.8F.98.E9.87.8F)
        *   [2.2.1 GNOME, XFCE, LXDE 用户](#GNOME.2C_XFCE.2C_LXDE_.E7.94.A8.E6.88.B7)
        *   [2.2.2 KDE3](#KDE3)
        *   [2.2.3 GTK](#GTK)
    *   [2.3 Locale 相关的文件](#Locale_.E7.9B.B8.E5.85.B3.E7.9A.84.E6.96.87.E4.BB.B6)
        *   [2.3.1 更多关于 locale 的疑难解答](#.E6.9B.B4.E5.A4.9A.E5.85.B3.E4.BA.8E_locale_.E7.9A.84.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [2.4 执行 SCIM](#.E6.89.A7.E8.A1.8C_SCIM)
        *   [2.4.1 GNOME](#GNOME)
        *   [2.4.2 KDE](#KDE)
*   [3 已知问题](#.E5.B7.B2.E7.9F.A5.E9.97.AE.E9.A2.98)
    *   [3.1 LWJGL (Lightweight Java Game Library) losing keyboard focus](#LWJGL_.28Lightweight_Java_Game_Library.29_losing_keyboard_focus)
*   [4 外部链接](#.E5.A4.96.E9.83.A8.E9.93.BE.E6.8E.A5)

## 安装SCIM

```
pacman -S scim

```

### 安装输入法引擎

目前SCIM包含许多各类的输入法（有些可能需要一些其它的库），覆盖30多种语言，包括中文（简体、繁体）、日文、韩文及许多欧洲语言：

```
(在[这里](http://www.scim-im.org/projects/imengines)察看所有支持的语言)

```

中文智能拼音：

```
pacman -S scim-pinyin

```

中文五笔及其它：

```
pacman -S scim-tables

```

日文：

```
pacman -S scim-anthy

```

韩文：

```
pacman -S scim-hangul

```

### 安装 SCIM-BRIDGE

SCIM-BRIDGE是SCIM的另外一个immodule，解决了SCIM本身的一些兼容性问题，并且能够同时提供GTK/QT3/QT4模块

可以从[AUR](https://aur.archlinux.org/)安装

## 配置SCIM

方法一： 为了让SCIM在桌面中自动启动并且正常工作，编辑~/.xinitrc，在启动桌面环境/窗口管理器的语句前面加入以下内容（如果使用scim-bridge，把下面的“scim”改为“scim-bridge”）：

```
export LC_CTYPE="zh_CN.UTF-8" （请改成你在X下使用的locale，如果没有合适的locale，请查询locale-gen相关信息）
export XMODIFIERS=@im=SCIM
export GTK_IM_MODULE="scim"
export QT_IM_MODULE="scim"
scim -d  

```

如果使用"scim -f socket -c socket -d"替换"scim -d "，会导致一些qt程序无法使用scim，比如eva。 现在进入X，scim应该已经启动了，你可以在图标上点击右键改变SCIM配置（比如去掉一些不用的输入法）。在任何程序中按Ctrl-Space就可以使用输入法了。

### 使用kdm/gdm时自动启动scim

创建一个新文件~/.xprofile，加入以下内容（如果使用scim-bridge，把下面的“scim”改为“scim-bridge”）：

```
export LC_CTYPE="zh_CN.UTF-8" 
export XMODIFIERS=@im=SCIM
export GTK_IM_MODULE="scim"
export QT_IM_MODULE="scim"
scim -d

```

查看[这里](https://www.archlinux.org/news/166/)获得更多官方信息。

方法二： Gnome用户可以试一下，编辑/etc/gtk-2.0/gtk.immodules，在最后加入以下内容：

```
 "/usr/lib/gtk-2.0/immodules/im-scim.so" 
 "scim" "SCIM Input Method" "scim" "/usr/share/locale" "ja:ko:zh" 

```

如果LC_CTYPE为"en_US.UTF-8“，需要将"ja:ko:zh"改成"en:ja:ko:zh"。当你输入命令gtk-query-immodules-2.0，你将会发现“en”是关键。随后重启。SCIM托盘可能不显示，但是当你设置好输入法后，按下CTRL+空格，输入条将会显示。KDE或许有类似的方法。警告：加了"en"，PC重启后任务栏可能不显示。按CTRL+ALT+F1进入SHELL，输入sudo reboot或reboot重启。或者用vi或vim编辑/etc/gtk-2.0/gtk.immodules。

### 环境变量

以下环境变量在运行scim**之前**必须被export：

```
export XMODIFIERS=@im=SCIM
export GTK_IM_MODULE="scim"
export QT_IM_MODULE="scim"

```

通常这些变量被放在脚本文件中，如 ~/.xinitrc 或者 /etc/profile (全局设置), 又或者 ~/.config/openbox/autostart (如果使用 Openbox 作为 窗口管理器).如果放在 ~/.xinitrc, 必须放在执行桌面环境/窗口管理器**之前**。

**如果你不知道那种方法更好，使用 /etc/profile.**

**注意:** 第一个环境变量与一些(少见的)选项如 `XMODIFIERS=urxvt` 冲突.

#### GNOME, XFCE, LXDE 用户

如果 _export QT_IM_MODULE="scim"_ 无法工作，可以使用 AUR 中的 [scim-bridge](https://aur.archlinux.org/packages/scim-bridge/)。在 2009.02.15 的更新中(scim 1.4.7-1, AUR 中的 scim-bridge 0.4.15-1)下面配置可以在 GNOME, XFCE, LXDE 中工作：

```
export QT_IM_MODULE="scim-bridge"

```

#### KDE3

将 QT IMM 设为 **xim** 或安装 AUR 中的 [scim-qtimm-cvs](https://aur.archlinux.org/packages/scim-qtimm-cvs/):

```
export QT_IM_MODULE="xim"

```

#### GTK

scim 无法在 gtk 应用程序中工作，请检查 GTK_IM_MODULE_FILE 环境变量，应该设置为 /etc/gtk-2.0/gtk.immodules 或包含输入法模块文件的目录。

在上面提到的脚本中加入下面内容，放到执行DE/WM之前:

```
gtk-query-immodules-2.0 > ~/.immodules
export GTK_IM_MODULE_FILE=~/.immodules

```

GTK 会从 ~/.immodules 中查找文件，如果将 GTK_IM_MODULE_FILE 设置为 /etc/gtk-2.0/gtk.immodules，不需要第一行。

### Locale 相关的文件

如果键盘 locale **不是** en_US.UTF-8 (或 en_US.utf8)，需要修改 ~/.scim/global (或系统设置 /etc/scim/global)的下面这行：

```
/SupportedUnicodeLocales = en_US.UTF-8,de_CH.UTF-8

```

将 de_CH.UTF-8 修改为所用 locale。

**注意:** locale 必须已经启用(/etc/locale-gen 中取消注释并以 root 执行 locale-gen ) 而且被 SCIM 支持(支持大部分 *.UTF-8 locales).

如下命令可以获得活动的 locale：

```
locale -a

```

(查看 /etc/locale.gen 也可以).

#### 更多关于 locale 的疑难解答

如果安装 scim 和输入法表之后，scim 还无法工作(点击系统图标无反应)，需要在 `/etc/profile` 中将 `LC_CTYPE` 设置为要使用的 locale。

```
LC_CTYPE="zh_CN.UTF-8"              //if you want to type simplified chinese

```

修改/etc/locale.gen 文件，取消 locale 前的注释并用 locale-gen 命令生成 locale：

```
locale-gen

```

### 执行 SCIM

可以直接执行:

```
scim

```

建议作为守护进程执行：

```
scim -d

```

可以将上面文件放入脚本中自动执行，例如 ~/.xinitrc (环境变量之后，DE/WM之前), /etc/profile (环境变量之后) 或 ~/.config/openbox/autostart (环境变量之后，可以 sleep 几秒)。

#### GNOME

使用 GNOME 需要执行：

```
 scim -f x11 -c simple -d

```

要自动启动，在 System > Preferences > Session 中创建上面一行命令。

**注意:** 如果使用 scim -f socket -c socket -d，SCIM 的配置文件无法修改。

#### KDE

KDE 中需要执行：

```
 scim -f socket -c socket -d

```

或者采取：

1.  从 [AUR](/index.php/AUR "AUR") 安装 **skim**.
2.  启动 **SKIM**，系统图标上右键，点击 'Configure'
3.  在 **Frontend > X Window** 中点击"Start skim automatically when KDE starts"
4.  登出并重启 X server (ctrl+alt+del)，重新登录

按键盘 _ctrl+space_ 激活输入法。

## 已知问题

### LWJGL (Lightweight Java Game Library) losing keyboard focus

一个解决方法是 kill scim ，应用程序就可以接收键盘输入了。

参见 [[1]](http://www.scim-im.org/forums#nabble-td2499750) 和 [[2]](http://ubuntuforums.org/showthread.php?t=1641861).

## 外部链接

*   [See the official news page for more details](https://www.archlinux.org/news/166/).