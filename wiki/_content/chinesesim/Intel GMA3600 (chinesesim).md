**翻译状态：** 本文是英文页面 [Intel_GMA3600](/index.php/Intel_GMA3600 "Intel GMA3600") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-2-16，点击[这里](https://wiki.archlinux.org/index.php?title=Intel_GMA3600&diff=0&oldid=361396)可以查看翻译后英文页面的改动。

Intel GMA3600是基于PowerVR SGX 545显示核心的集成显卡，搭载于Atom N2600和Atom N2800中。

## Contents

*   [1 News](#News)
*   [2 Kernel module driver](#Kernel_module_driver)
*   [3 Xorg driver](#Xorg_driver)
*   [4 Playing video](#Playing_video)

## News

Intel release a graphics driver for PowerVR: [http://downloadcenter.intel.com/Detail_Desc.aspx?agr=Y&DwnldID=21938](http://downloadcenter.intel.com/Detail_Desc.aspx?agr=Y&DwnldID=21938)

Be aware: The current version 1.03 (10/01/2012) has the following dependencies:

Bundle "Ant"

```
* Kernel: 3.0.0
* Mesa GL: 7.9
* Xorg: 1.9

```

Bundle "Bee"

```
* Kernel: 3.1.0
* Mesa GL: 7.11
* Xorg: 1.11

```

This means, unless you run a really outdated system this driver is useless for Arch-Linux.

## Kernel module driver

Kernel has an experimental support for this adapter since v3.3\. Since Kernel v3.5 the GMA3600 power features are supported. Now suspend/resume should properly work.

If after resume you got a blank screen try the following

```
sudo touch /etc/pm/sleep.d/99video

```

## Xorg driver

At the moment there is no accelerated driver for Xorg Server, but some support is available using the Xorg modesetting driver provided by package [xorg-server](https://www.archlinux.org/packages/?name=xorg-server).

/etc/X11/xorg.conf.d/20-gpudriver.conf:

```
Section "Device"
    Identifier "Intel GMA3600"
    Driver     "modesetting"
EndSection

```

The modesetting driver allows disabling/enabling LVDS, VGA, etc. ports and changing resolution using xrandr.

The following can be used to disable LVDS and force enable VGA if needed.

/etc/X11/xorg.conf.d/20-gpudriver.conf:

```
Section "Device"
    Identifier "Intel GMA3600"
    Driver     "modesetting"
    Option     "Monitor-LVDS-0" "Ignore"
    Option     "Monitor-VGA-0" "Monitor"
EndSection

Section "Monitor"
    Identifier "Ignore"
    Option     "Ignore"
EndSection

Section "Monitor"
    Identifier "Monitor"
    Option     "Enable"
EndSection

```

## Playing video

It is unable to utilize whole chip power and play fullHD movies using graphics acceleration. As workaround you could utilize the maximum power of your Atom CPU to decode video:

```
mplayer -lavdopts threads=4 -fs myvideo.avi

```