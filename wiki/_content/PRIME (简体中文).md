# PRIME (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** The list of drivers that support PRIME is incomplete. (Discuss in [Talk:PRIME (简体中文)#](https://wiki.archlinux.org/index.php/Talk:PRIME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)))

PRIME 是一项用于管理新型号笔记本电脑中的混合显卡的技术([Optimus for NVIDIA](/index.php/NVIDIA_Optimus "NVIDIA Optimus"), AMD动态切换显卡技术) 以下驱动程序可支持PRIME技术：

*   [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau)
*   [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati)
*   [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 故障排查](#.E6.95.85.E9.9A.9C.E6.8E.92.E6.9F.A5)
    *   [2.1 XRandR 只识别出一个显卡](#XRandR_.E5.8F.AA.E8.AF.86.E5.88.AB.E5.87.BA.E4.B8.80.E4.B8.AA.E6.98.BE.E5.8D.A1)
    *   [2.2 当程序使用独立显卡渲染时，程序黑屏](#.E5.BD.93.E7.A8.8B.E5.BA.8F.E4.BD.BF.E7.94.A8.E7.8B.AC.E7.AB.8B.E6.98.BE.E5.8D.A1.E6.B8.B2.E6.9F.93.E6.97.B6.EF.BC.8C.E7.A8.8B.E5.BA.8F.E9.BB.91.E5.B1.8F)
        *   [2.2.1 Black screen with GL-based compositors](#Black_screen_with_GL-based_compositors)

## 安装

首先，检查所有添附到你的显示器上的显卡：

 `$ xrandr --listproviders` 

```
Providers: number : 2
Provider 0: id: 0x7d cap: 0xb, Source Output, Sink Output, Sink Offload crtcs: 3 outputs: 4 associated providers: 1 name:Intel
Provider 1: id: 0x56 cap: 0xf, Source Output, Sink Output, Source Offload, Sink Offload crtcs: 6 outputs: 1 associated providers: 1 name:radeon

```

我们可以看到有两块显卡：Intel，也就是集成的图形卡（id为0x7d），以及 Radeon，也就是独立显卡（id为0x56），通常情况下对GPU要求高的程序应该使用独立显卡。我们可以看到，默认情况下被使用的显卡总是Intel集成显卡：

 `$ glxinfo | grep "OpenGL renderer"` 

```
OpenGL renderer string: Mesa DRI Intel(R) Ivybridge Mobile

```

为了使用独立显卡（此处以radeon为例），你必须先将集成显卡定义为offload provider，因为当前连接到显示器的是集成显卡：

```
$ xrandr --setprovideroffloadsink 0x56 0x7d

```

现在你可以在对显卡要求高的程序（如游戏，3D建模工具等等）中使用独立显卡了：

 `$ DRI_PRIME=1 glxinfo | grep "OpenGL renderer"` 

```
OpenGL renderer string: Gallium 0.4 on AMD TURKS

```

其他程序仍然会使用更节能的集成显卡。每次X11重启都必须再运行一次 `xrandr --setprovideroffloadsink 0x56 0x7d` ; 你可以写一个脚本并且在启动桌面环境时自动运行(或者将脚本放在 `/etc/X11/xinit/xinitrc.d/`目录下).

## 故障排查

### XRandR 只识别出一个显卡

删除或者移走 /etc/X11/xorg.conf 以及 /etc/X11/xorg.conf.d/ 目录下任何与GPU有关的文件

### 当程序使用独立显卡渲染时，程序黑屏

某些情况下PRIME的正常工作需要一个混合窗口管理器。如果你使用的窗口管理器不进行混合渲染，你可以在其基础上使用[xcompmgr](/index.php/Xcompmgr "Xcompmgr")。

#### Black screen with GL-based compositors

Currently there are issues with GL-based compositors and PRIME offloading. While Xrender-based compositors (xcompmgr, xfwm, compton's default backend, cairo-compmgr, and a few others) will work without issue, GL-based compositors (Mutter/muffin, Compiz, compton with GLX backend, Kwin's OpenGL backend, etc) will initially show a black screen, as if there was no compositor running. While you can force an image to appear by resizing the offloaded window, this is not a practical solution as it will not work for things such as full screen Wine applications. This means that desktop environments such as GNOME3 and Cinnamon have issues with using PRIME offloading.

Additionally if you are using an Intel IGP you might be able to fix the GL Compositing issue by running the IGP as UXA instead of SNA, however this may cause issues with the offloading process (ie, xrandr --listproviders may not list the discrete GPU).

Retrieved from "[https://wiki.archlinux.org/index.php?title=PRIME_(简体中文)&oldid=415637](https://wiki.archlinux.org/index.php?title=PRIME_(简体中文)&oldid=415637)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Graphics (简体中文)](/index.php/Category:Graphics_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Graphics (简体中文)")

Hidden category:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")