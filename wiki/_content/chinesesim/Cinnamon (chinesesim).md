相关文章

*   [Nemo](/index.php/Nemo "Nemo")
*   [GNOME](/index.php/GNOME "GNOME")
*   [MATE](/index.php/MATE "MATE")
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager](/index.php/Display_manager "Display manager")

**翻译状态：** 本文是英文页面 [Cinnamon](/index.php/Cinnamon "Cinnamon") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-09-12，点击[这里](https://wiki.archlinux.org/index.php?title=Cinnamon&diff=0&oldid=436684)可以查看翻译后英文页面的改动。

[Cinnamon](http://cinnamon.linuxmint.com/) 是一个提供先进创新的特点和传统的用户体验的Linux桌面。然而，底层的技术是基于 [GNOME](/index.php/GNOME "GNOME") 的分支. 在Cinnamon 2.2版本中，Cinnamon已经是一个完整的桌面环境，不仅仅是一个GNOME的前端。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 启动 Cinnamon](#.E5.90.AF.E5.8A.A8_Cinnamon)
    *   [2.1 图形化登录](#.E5.9B.BE.E5.BD.A2.E5.8C.96.E7.99.BB.E5.BD.95)
    *   [2.2 手动启动Cinnamon](#.E6.89.8B.E5.8A.A8.E5.90.AF.E5.8A.A8Cinnamon)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 Cinnamon系统设置](#Cinnamon.E7.B3.BB.E7.BB.9F.E8.AE.BE.E7.BD.AE)
    *   [3.2 应用程序和扩展](#.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E5.92.8C.E6.89.A9.E5.B1.95)
    *   [3.3 按下电源按钮睡眠](#.E6.8C.89.E4.B8.8B.E7.94.B5.E6.BA.90.E6.8C.89.E9.92.AE.E7.9D.A1.E7.9C.A0)
    *   [3.4 管理 Cinnamon 使用的语言](#.E7.AE.A1.E7.90.86_Cinnamon_.E4.BD.BF.E7.94.A8.E7.9A.84.E8.AF.AD.E8.A8.80)
*   [4 小贴士](#.E5.B0.8F.E8.B4.B4.E5.A3.AB)
    *   [4.1 创建自定义应用程序](#.E5.88.9B.E5.BB.BA.E8.87.AA.E5.AE.9A.E4.B9.89.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
    *   [4.2 默认的桌面背景壁纸路径](#.E9.BB.98.E8.AE.A4.E7.9A.84.E6.A1.8C.E9.9D.A2.E8.83.8C.E6.99.AF.E5.A3.81.E7.BA.B8.E8.B7.AF.E5.BE.84)
    *   [4.3 添加“计算机”“主目录”“回收站”等常用图标与新的启动器](#.E6.B7.BB.E5.8A.A0.E2.80.9C.E8.AE.A1.E7.AE.97.E6.9C.BA.E2.80.9D.E2.80.9C.E4.B8.BB.E7.9B.AE.E5.BD.95.E2.80.9D.E2.80.9C.E5.9B.9E.E6.94.B6.E7.AB.99.E2.80.9D.E7.AD.89.E5.B8.B8.E7.94.A8.E5.9B.BE.E6.A0.87.E4.B8.8E.E6.96.B0.E7.9A.84.E5.90.AF.E5.8A.A8.E5.99.A8)
    *   [4.4 菜单编辑器](#.E8.8F.9C.E5.8D.95.E7.BC.96.E8.BE.91.E5.99.A8)
    *   [4.5 工作区](#.E5.B7.A5.E4.BD.9C.E5.8C.BA)
    *   [4.6 隐藏桌面图标](#.E9.9A.90.E8.97.8F.E6.A1.8C.E9.9D.A2.E5.9B.BE.E6.A0.87)
    *   [4.7 图标和主题](#.E5.9B.BE.E6.A0.87.E5.92.8C.E4.B8.BB.E9.A2.98)
    *   [4.8 声音效果](#.E5.A3.B0.E9.9F.B3.E6.95.88.E6.9E.9C)
    *   [4.9 调整窗口的大小](#.E8.B0.83.E6.95.B4.E7.AA.97.E5.8F.A3.E7.9A.84.E5.A4.A7.E5.B0.8F)
    *   [4.10 截图](#.E6.88.AA.E5.9B.BE)
*   [5 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [5.1 cinnamon设置无法找到一个特定的模块](#cinnamon.E8.AE.BE.E7.BD.AE.E6.97.A0.E6.B3.95.E6.89.BE.E5.88.B0.E4.B8.80.E4.B8.AA.E7.89.B9.E5.AE.9A.E7.9A.84.E6.A8.A1.E5.9D.97)
    *   [5.2 Video tearing](#Video_tearing)
    *   [5.3 禁用*网络管理*小程序](#.E7.A6.81.E7.94.A8.E7.BD.91.E7.BB.9C.E7.AE.A1.E7.90.86.E5.B0.8F.E7.A8.8B.E5.BA.8F)

## 安装

Cinnamon 通过包 [cinnamon](https://www.archlinux.org/packages/?name=cinnamon) 进行 [安装](/index.php/%E5%AE%89%E8%A3%85 "安装").

## 启动 Cinnamon

### 图形化登录

在你喜欢的 [display manager](/index.php/Display_manager "Display manager") 选择 *Cinnamon* 或者是 *Cinnamon (Software Rendering)* 。Cinnamon选项是3D加速的版本，一般使用这个。如果你的显卡驱动出现问题，试试“'cinnamon（软件渲染）”，这个禁用了3D加速。

### 手动启动Cinnamon

如果你喜欢控制台启动Cinnamon, 添加以下行到 [Xinitrc](/index.php/Xinitrc "Xinitrc"):

 `~/.xinitrc` 
```
 exec cinnamon-session

```

如果你想用 *Cinnamon (Software Rendering)* , 用 `cinnamon-session-cinnamon2d` 代替 `cinnamon-session`.

## 配置

Cinnamon很容易配置，大部分的配置都是在图形化界面下完成。更多详情可查看以下网站[applets](http://cinnamon-spices.linuxmint.com/applets)/ [extensions](http://cinnamon-spices.linuxmint.com/extensions)/[theming](http://cinnamon-spices.linuxmint.com/themes).

### Cinnamon系统设置

启动*cinnamon系统设置*：

```
$ cinnamon-settings

```

查看设置界面的模块：

```
 $ pacman -Ql cinnamon | awk -F'[_.]' '/cs_.+\.py/ {print $2}'

```

打开其中的一个模块

```
$ cinnamon-settings 模块名称

```

示例：

```
$ cinnamon-settings panel

```

	打印机

	安装 [system-config-printer](https://www.archlinux.org/packages/?name=system-config-printer) 进行打印机配置

	网络

	添加网络模块的支持, 请看 [Network Manager](/index.php/NetworkManager#Configuration "NetworkManager").要在 Network manager 里面保存 Wifi 密码，需要安装 [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring")。

	蓝牙

	安装软件包 [blueberry](https://www.archlinux.org/packages/?name=blueberry)

### 应用程序和扩展

许多cinnamon的应用程序和扩展可以在 [AUR](/index.php/AUR "AUR"), ([package search](https://aur.archlinux.org/packages.php?O=0&K=cinnamon-&do_Search=Go))找到,也可以在Cinnamon的“小程序”和“拓展”中找到 (*在线获取更多*选项卡中):

```
$ cinnamon-settings applets
$ cinnamon-settings extensions

```

也可以从 [Cinnamon spices](http://cinnamon-spices.linuxmint.com/)下载并手动安装.

**Note:** 如果你安装后没有发现这些拓展或者是应用程序, 用 `Alt+F2` 并在对话框键入 `r` 重启 Cinnamon .

### 按下电源按钮睡眠

这是电源按钮默认的操作。如需更改，打开`cinnamon-settings`**系统设置**，点击**电源管理**。更改**按下电源按钮时**选项，选择你所希望使用的操作。

### 管理 Cinnamon 使用的语言

**Note:** Cinnamon 控制面板从 2.2 版本开始删除了语言配置模块[[1]](http://segfault.linuxmint.com/2014/04/cinnamon-2-2/)

*   要添加删除语言，请查看 [Locale](/index.php/Locale "Locale").
*   要在启用的语言间切换，请安装软件包 [mintlocale](https://aur.archlinux.org/packages/mintlocale/).
*   要修改键盘布局: **System Settings > Hardware > Keyboard > Layouts**.

## 小贴士

### 创建自定义应用程序

关于创建自定义应用程序，可以在 [这里](http://developer.linuxmint.com/reference/2.6/cinnamon-tutorials/write-applet.html)和[这里](http://cinnamon.linuxmint.com/?p=144) 找到教程.

### 默认的桌面背景壁纸路径

当你在Cinnamon设置自定义的路径的壁纸，, Cinnamon 会将其复制到 `~/.cinnamon/backgrounds`. 因此， 每一个改变你的壁纸，你都得再次在设置菜单添加你的墙纸到或将其复制到 `~/.cinnamon/backgrounds`.

### 添加“计算机”“主目录”“回收站”等常用图标与新的启动器

你可以在“设置”=>“桌面”添加部分常有图标，如“计算机”“主目录”“回收站”等。如要添加其它的启动器，右击桌面并选择“在此创建一个新的启动器”即可。

### 菜单编辑器

菜单小程序支持自定义命令。右键单击"菜单"小程序，然后点击"配置..."，然后点击“打开菜单编辑器”。选择一个子菜单（或者创建一个新的子菜单），然后选择“新建项目”。填好名称、命令和备注。如果需要在终端运行，选中“在终端运行”复选框，图形化应用程序不选中“在终端运行”复选框。然后点击”确定“并关闭菜单编辑器。启动器就添加到了菜单。

### 工作区

默认情况下，有2个工作区。增加，按Ctrl+ Alt +上键显示所有的工作区。然后点击右边的加号按钮在屏幕添加更多的工作区。

### 隐藏桌面图标

用下面的命令更改设置：

```
$ gsettings set org.nemo.desktop show-desktop-icons false

```

### 图标和主题

Linux Mint风格的主题和图标可以在AUR安装： [mint-x-theme](https://aur.archlinux.org/packages/mint-x-theme/)和[mint-x-icons](https://aur.archlinux.org/packages/mint-x-icons/). 可以在 `Settings → Themes → Other settings`编辑主题.

Linux Mint Cinnamon 官方主题可以通过 [mint-cinnamon-themes](https://aur.archlinux.org/packages/mint-cinnamon-themes/) 软件包进行安装.

### 声音效果

Cinnamon没有附带那些Linux Mint默认使用的像桌面启动之类声音事件。这些声音效果可与安装[cinnamon-sound-effects](https://aur.archlinux.org/packages/cinnamon-sound-effects/)和[mint-sounds](https://aur.archlinux.org/packages/mint-sounds/)。声音事件可以在`Settings → Sound → Sound Effects`编辑。

### 调整窗口的大小

用Alt+右键调整窗口的大小，使用gsettings：

```
$ gsettings set org.cinnamon.desktop.wm.preferences resize-with-right-button true

```

### 截图

As explained in [Taking a screenshot](/index.php/Taking_a_screenshot#Cinnamon "Taking a screenshot"), installing [gnome-screenshot](https://www.archlinux.org/packages/?name=gnome-screenshot) will add this functionality. The default shortcut key is `Prt Sc` key. This binding ca be changed in the applet *Menu > Preferences > Keyboard* under *Shortcuts > System > Screenshots and Recording*. The default save directory is `$HOME/Pictures`, but can be customized with eg.

```
$ gsettings set org.gnome.gnome-screenshot auto-save-directory file:///home/*USER*/*some_path*

```

## 故障排除

### cinnamon设置无法找到一个特定的模块

If *cinnamon-settings* does not start with the message that it cannot find a certain module, e.g. the Image module, it is likely that it uses outdated compiled files which refer to no longer existing file locations. In this case remove all `*.pyc` files in `/usr/lib/cinnamon-settings` and its sub-folders. See the [upstream bug report](https://github.com/linuxmint/Cinnamon/issues/2495).

### Video tearing

Because [muffin](https://www.archlinux.org/packages/?name=muffin) is based upon [mutter](https://www.archlinux.org/packages/?name=mutter), video tearing fixes for [GNOME](/index.php/GNOME "GNOME") should also work in Cinnamon. See [GNOME/Troubleshooting#Tear-free video with Intel HD Graphics](/index.php/GNOME/Troubleshooting#Tear-free_video_with_Intel_HD_Graphics "GNOME/Troubleshooting") for more information.

### 禁用*网络管理*小程序

即使你不使用[NetworkManager](/index.php/NetworkManager "NetworkManager")或者从默认面板删除*网络管理*小程序，Cinnamon依然会载入*nm-applet* 并显示在系统托盘上。你**不能**卸载[NetworkManager](/index.php/NetworkManager "NetworkManager")，因为[NetworkManager](/index.php/NetworkManager "NetworkManager")被[cinnamon](https://www.archlinux.org/packages/?name=cinnamon)和[cinnamon-control-center](https://www.archlinux.org/packages/?name=cinnamon-control-center)需要，但是你可以很容易将其禁用。首先，你应该把自启动文件从`/etc/xdg/autostart/nm-applet.desktop`复制到`~/.config/autostart/nm-applet.desktop`。然后用你喜欢的文本编辑器打开，并在最后加上`X-GNOME-Autostart-enabled=false`。

另外，你也可以通过创建以下符号链接来禁用：

```
$ ln -s /bin/true /usr/local/bin/nm-applet

```