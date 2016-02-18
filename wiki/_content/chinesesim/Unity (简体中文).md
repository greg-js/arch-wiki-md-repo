**翻译状态：** 本文是英文页面 [Unity](/index.php/Unity "Unity") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-11-08，点击[这里](https://wiki.archlinux.org/index.php?title=Unity&diff=0&oldid=234364)可以查看翻译后英文页面的改动。

[Unity](http://unity.ubuntu.com/) is an alternative shell for the GNOME desktop environment, developed by Canonical in its Ayatana project. It consists of several components including the Launcher, Dash, lenses, Panel, indicators, Notify OSD and Overlay Scrollbar. Unity used to available in two implementations: 'Unity' is the 3D accelerated version, which uses Compiz window manager and Nux toolkit; and 'Unity 2D' is a lighter alternative, which uses Metacity window manager and Qt toolkit. Unity 2D is already dropped by Canonical from Ubuntu 12.10\. Instead a version powered by Gallium3D llvmpipe alternative is used.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 源码安装](#.E6.BA.90.E7.A0.81.E5.AE.89.E8.A3.85)
    *   [1.2 软件源](#.E8.BD.AF.E4.BB.B6.E6.BA.90)
*   [2 更新](#.E6.9B.B4.E6.96.B0)
*   [3 疑难问题](#.E7.96.91.E9.9A.BE.E9.97.AE.E9.A2.98)
    *   [3.1 Unity在更新后不工作](#Unity.E5.9C.A8.E6.9B.B4.E6.96.B0.E5.90.8E.E4.B8.8D.E5.B7.A5.E4.BD.9C)
    *   [3.2 窗口装饰显示不正常](#.E7.AA.97.E5.8F.A3.E8.A3.85.E9.A5.B0.E6.98.BE.E7.A4.BA.E4.B8.8D.E6.AD.A3.E5.B8.B8)
    *   [3.3 窗口装饰不能使用某个特定的主题](#.E7.AA.97.E5.8F.A3.E8.A3.85.E9.A5.B0.E4.B8.8D.E8.83.BD.E4.BD.BF.E7.94.A8.E6.9F.90.E4.B8.AA.E7.89.B9.E5.AE.9A.E7.9A.84.E4.B8.BB.E9.A2.98)
    *   [3.4 在更新到Gnome 3.6后某些gtk主题看起来不正常](#.E5.9C.A8.E6.9B.B4.E6.96.B0.E5.88.B0Gnome_3.6.E5.90.8E.E6.9F.90.E4.BA.9Bgtk.E4.B8.BB.E9.A2.98.E7.9C.8B.E8.B5.B7.E6.9D.A5.E4.B8.8D.E6.AD.A3.E5.B8.B8)
    *   [3.5 新开的窗口总会被放到屏幕左上角](#.E6.96.B0.E5.BC.80.E7.9A.84.E7.AA.97.E5.8F.A3.E6.80.BB.E4.BC.9A.E8.A2.AB.E6.94.BE.E5.88.B0.E5.B1.8F.E5.B9.95.E5.B7.A6.E4.B8.8A.E8.A7.92)
    *   [3.6 窗口最大化后标题栏依然存在](#.E7.AA.97.E5.8F.A3.E6.9C.80.E5.A4.A7.E5.8C.96.E5.90.8E.E6.A0.87.E9.A2.98.E6.A0.8F.E4.BE.9D.E7.84.B6.E5.AD.98.E5.9C.A8)
*   [4 已知问题](#.E5.B7.B2.E7.9F.A5.E9.97.AE.E9.A2.98)
    *   [4.1 Ubuntu 12.10 新特性 *Webapps* 不正常](#Ubuntu_12.10_.E6.96.B0.E7.89.B9.E6.80.A7_Webapps_.E4.B8.8D.E6.AD.A3.E5.B8.B8)
    *   [4.2 *Indicator messages* 不正常](#Indicator_messages_.E4.B8.8D.E6.AD.A3.E5.B8.B8)

## 安装

有两种途径可供选择：

*   **从源码编译安装**
*   **添加软件源安装**

### 源码安装

All of the pkgbuilds can be browsed in [Github repository](https://github.com/chenxiaolong/Unity-for-Arch), where [Unity-For-Arch](https://github.com/chenxiaolong/Unity-for-Arch) provides a minimal working Unity shell, [Unity-For-Arch-Extra](https://github.com/chenxiaolong/Unity-for-Arch-Extra) provides some additoinal applications including **lightdm-ubuntu**(lightdm with ubuntu patch), **light-themes**, **ubuntu-tweak**(a popular ubuntu tweak tool) and so on.

最简安装Unity桌面环境：

1\. 'cd' 进一个你想要保存源码的目录，然后运行：

 `$ git clone [https://github.com/chenxiaolong/Unity-for-Arch.git](https://github.com/chenxiaolong/Unity-for-Arch.git)` 

Where [git](https://www.archlinux.org/packages/?name=git) is required.

2\. 打开README文件，按照上面的指示编译。基本上是这样的：

```
$ cd packagename
$ rm -rvf # 清理之前的编译文件
$ makepkg -sci # '-s' 意思是安装需要的依赖， '-c' 意思是编译完成后清理无关文件， '-i' 意思是编译完成后安装软件包

```

3\. 注销再登陆进Unity环境。

如想使用lightdm启动Unity，请从[Unity-For-Arch-Extra](https://github.com/chenxiaolong/Unity-for-Arch-Extra)安装 **lightdm-ubuntu** and **lightdm-unity-greeter** ，步骤基本和上面一致。 然后将lightdm加入自启动守护进程。使用Systemd的用户可以查看 [关于Systemd的文章](https://wiki.archlinux.org/index.php/Systemd_(简体中文)).

**Note:** 可以使用 [这个脚本](https://gist.github.com/3906721) 来使安装自动化。

### 软件源

已编译好的二进制包可以在[unity.humbug.in](http://unity.humbug.in/) 和 [unity.xe-xe.org](http://unity.xe-xe.org/)下载到。

在这里，以 **unity.xe-xe.org** 为例安装Unity。添加以下内容到 `/etc/pacman.conf`：

```
[unity]
Server = [http://unity.xe-xe.org/$arch](http://unity.xe-xe.org/$arch)

[unity-extra]
Server = [http://unity.xe-xe.org/extra/$arch](http://unity.xe-xe.org/extra/$arch)

```

执行以下命令：

```
$ pacman -Suy
$ pacman -S $(pacman -Slq unity)
```

使用另一个源 **mooos.org** 安装Unity。添加以下内容到 `/etc/pacman.conf`：

```
[moo]
SigLevel = Optional TrustAll
Server = [http://mooos.org/repos/moo/$arch](http://mooos.org/repos/moo/$arch)

```

执行以下命令：

```
$ sudo pacman -S unity

```

重启系统，使用 Ubuntu 会话：

sudo reboot

**Note:** There are many ubuntu-patched packages that replace original Arch packages. Also it is recommended to use freetype2-ubuntu and libxft-ubuntu from AUR.

**警告:** 请记住这些软件是 **非官方** 的，并且不是由Arch Linux的开发者维护的。

**警告:** 几乎所有和Unity相关的AUR里的软件包都过期了。请一定不要把那些过期的软件包和软件源里的混在一起。

## 更新

软件源里的Unity更新方法和Arch官方源的更新一样。

如果是源码安装：

1\. 'cd' into the 'Unity-for-Arch' directory where it was originally cloned

2\. 从github获取更新文件：

 `$ git pull` 

3\. 检查是否需要更新：

 `$ ./What_can_I_update\?.py` 

4\. 如果需要更新，请按照上面 **源码安装** 部分的说明。

**注意:** 有的时候如果一个关键性的软件包更新，会导致依赖于它的软件包需要重新编译。 比如，如果 **nux** 有更新，那么 **Unity** 一般会被要求重新编译。

## 疑难问题

### Unity在更新后不工作

尝试运行：

 `$ compiz.reset` 

然后注销再登陆进Unity。

如果问题仍然存在，请在[github](https://github.com/chenxiaolong/Unity-for-Arch/issues?state=open)报告问题 或者 在[Arch论坛](https://bbs.archlinux.org/viewtopic.php?id=125423&p=1)讨论。

### 窗口装饰显示不正常

试着安装 [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) 来调整主题。

### 窗口装饰不能使用某个特定的主题

请安装 metacity-ubuntu 而不是 metacity.

### 在更新到Gnome 3.6后某些gtk主题看起来不正常

Unity的默认主题light-themes也会这样，请添加

```
GtkLabel {
background-color: @transparent;
}

```

到 `.config/gtk3.0/gtk.css`

### 新开的窗口总会被放到屏幕左上角

请使用 **Metacity-ubuntu** 而不是 [metacity](https://www.archlinux.org/packages/?name=metacity)。 **Metacity-ubuntu** 现已被包括进 [Unity-for-Arch](https://github.com/chenxiaolong/Unity-for-Arch) 。

### 窗口最大化后标题栏依然存在

请使用 **Metacity-ubuntu** 而不是 [metacity](https://www.archlinux.org/packages/?name=metacity)。

## 已知问题

### Ubuntu 12.10 新特性 *Webapps* 不正常

### *Indicator messages* 不正常

It doesn't show any menus currently.