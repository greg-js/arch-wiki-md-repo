**翻译状态：** 本文是英文页面 [Intel_GMA3600](/index.php/Intel_GMA3600 "Intel GMA3600") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-10-12，点击[这里](https://wiki.archlinux.org/index.php?title=Intel_GMA3600&diff=0&oldid=361396)可以查看翻译后英文页面的改动。

Intel GMA3600 是基于 PowerVR SGX 545 显示核心的集成显卡，搭载于 Atom N2600,N2800,D2550 中。

Linux 内核从 3.5 版本开始支持此设备。

## Contents

*   [1 Xorg 驱动](#Xorg_.E9.A9.B1.E5.8A.A8)
*   [2 问题解决](#.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [2.1 恢复后黑屏](#.E6.81.A2.E5.A4.8D.E5.90.8E.E9.BB.91.E5.B1.8F)
    *   [2.2 播放视频](#.E6.92.AD.E6.94.BE.E8.A7.86.E9.A2.91)
*   [3 参阅](#.E5.8F.82.E9.98.85)

## Xorg 驱动

目前没有单独的 Xorg 驱动，请使用 [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) 提供的 modesetting 驱动:

 `/etc/X11/xorg.conf.d/20-gpudriver.conf` 
```
Section "Device"
    Identifier "Intel GMA3600"
    Driver     "modesetting"
EndSection

```

modesetting 驱动可以使用 xrandr 禁用/启用 LVDS, VGA 等端口，修改分辨率.

下面设置可以禁用 LVDS 并强制启用 VGA：

 `/etc/X11/xorg.conf.d/20-gpudriver.conf` 
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

## 问题解决

### 恢复后黑屏

如果恢复系统后黑屏，请执行：

```
# touch /etc/pm/sleep.d/99video

```

### 播放视频

目前没有办法使用视频加速，可以用 Atom CPU 用多线程解码:

```
mplayer -lavdopts threads=4 -fs myvideo.avi

```

## 参阅

*   [https://www.change.org/en-GB/petitions/intel-listen-to-the-community-and-develop-gma3600-drivers-for-linux](https://www.change.org/en-GB/petitions/intel-listen-to-the-community-and-develop-gma3600-drivers-for-linux)
*   [http://ubuntuforums.org/showthread.php?t=1953734](http://ubuntuforums.org/showthread.php?t=1953734)
*   [http://communities.intel.com/message/158477](http://communities.intel.com/message/158477)