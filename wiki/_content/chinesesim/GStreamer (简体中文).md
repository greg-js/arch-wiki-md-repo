**翻译状态：** 本文是英文页面 [GStreamer](/index.php/GStreamer "GStreamer") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间： 2014-06-15，点击[这里](https://wiki.archlinux.org/index.php?title=GStreamer&diff=0&oldid=313588)可以查看翻译后英文页面的改动。

Gstreamer是一个基于管道的多媒体框架。Gstreamer使用C语言编写，基于GObject。 Gstreamer允许程序员创建各种媒体处理组件，包括简单的音频播放，音频与视频播放，录制，流媒体控制与媒体编辑。其管道式设计是创建多种多媒体程序的基础，例如视频编辑器，流媒体服务器，以及媒体播放器。 Gstreamer是跨平台框架，目前已知可在下列平台上工作：Linux (x86, PowerPC 以及 ARM), Solaris (Intel 和 SPARC), Mac OS X, Microsoft Windows 以及 OS/400。Gstreamer是发布在GPL（GNU通用公共授权）协议下的自由软件。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 当前版本插件](#.E5.BD.93.E5.89.8D.E7.89.88.E6.9C.AC.E6.8F.92.E4.BB.B6)
    *   [1.2 旧版本插件](#.E6.97.A7.E7.89.88.E6.9C.AC.E6.8F.92.E4.BB.B6)
*   [2 整合](#.E6.95.B4.E5.90.88)
    *   [2.1 PulseAudio](#PulseAudio)
    *   [2.2 轻量级桌面](#.E8.BD.BB.E9.87.8F.E7.BA.A7.E6.A1.8C.E9.9D.A2)
    *   [2.3 KDE / Phonon integration](#KDE_.2F_Phonon_integration)
*   [3 Bugs](#Bugs)
*   [4 相关链接](#.E7.9B.B8.E5.85.B3.E9.93.BE.E6.8E.A5)

## 安装

从官方源 [official repositories](/index.php/Official_repositories "Official repositories")中安装一个版本的gstreamer:

*   [gstreamer](https://www.archlinux.org/packages/?name=gstreamer) - 当前版本。
*   [gstreamer0.10](https://www.archlinux.org/packages/?name=gstreamer0.10) - 更旧但是支持更多程序的版本。

为了让gstreamer发挥作用，安装你所需要的插件

### 当前版本插件

*   [gst-libav](https://www.archlinux.org/packages/?name=gst-libav) - 基于Libav的插件，包含众多编解码器。
*   [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad) - 需要更多改进，测试以及资料的插件。
*   [gst-plugins-base](https://www.archlinux.org/packages/?name=gst-plugins-base) - 基本的Gstreamer组件。
*   [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good) - 发布于LGPL许可证下，质量较高的插件。
*   [gst-plugins-ugly](https://www.archlinux.org/packages/?name=gst-plugins-ugly) - 质量较高，但是可能造成分发问题的插件。
*   [gst-vaapi](https://www.archlinux.org/packages/?name=gst-vaapi) - [VA-API](/index.php/VA-API#GStreamer "VA-API") 支持.
*   [gst-plugin-libde265](https://aur.archlinux.org/packages/gst-plugin-libde265/) - Gstreamer下的[libde265](https://aur.archlinux.org/packages/libde265/) 插件 (开源的h.265视频解码实现)。

### 旧版本插件

*   [gstreamer0.10-bad-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-bad-plugins) - 需要更多改进，测试以及资料的插件。
*   [gstreamer0.10-base-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-base-plugins) - 基本的Gstreamer组件。
*   [gstreamer0.10-ffmpeg](https://www.archlinux.org/packages/?name=gstreamer0.10-ffmpeg) - 基于Libav的插件，包含众多编解码器
*   [gstreamer0.10-good-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-good-plugins) - 发布于LGPL许可证下，质量较高的插件。
*   [gstreamer0.10-good-plugins-slim](https://aur.archlinux.org/packages/gstreamer0.10-good-plugins-slim/) - 发布于LGPL许可证下，质量较高的插件。 移除了GNOME 和 ASCII-art依赖.
*   [gstreamer0.10-ugly-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-ugly-plugins) - 质量较高，但是可能造成分发问题的插件。
*   [gstreamer0.10-vaapi](https://aur.archlinux.org/packages/gstreamer0.10-vaapi/) - [VAAPI](/index.php/VA-API#GStreamer "VA-API") 支持.
*   [gstreamer0.10-plugin-libde265](https://aur.archlinux.org/packages/gstreamer0.10-plugin-libde265/) - Gstreamer下的[libde265](https://aur.archlinux.org/packages/libde265/) 插件 (开源的h.265视频解码实现)。

## 整合

### PulseAudio

[PulseAudio](/index.php/PulseAudio "PulseAudio") 支持由 *good* 插件包提供.

### 轻量级桌面

如果需要设置GStreamer，例如切换音频输出设备，使用[gstreamer-properties](https://aur.archlinux.org/packages/gstreamer-properties/)软件包提供的*gstreamer-properties*。这个程序可以以每个用户的身份独立进行配置，或者以root身份进行全局配置。每个用户的独立设置放在`$HOME/.gconf/system/gstreamer`目录下，全局设置放在`/etc/gconf/gconf.xml.defaults`目录下。

### KDE / Phonon integration

请查看 [Phonon](/index.php/Phonon "Phonon").

## Bugs

如果使用录制软件录制视频时出现`GStreamer-CRITICAL **: gst_mini_object_unref: assertion `mini_object->refcount > 0' failed`错误， 安装 [gstreamer0.10-ffmpeg](https://www.archlinux.org/packages/?name=gstreamer0.10-ffmpeg) 以便修复.

## 相关链接

*   [Sound](/index.php/Sound "Sound")
*   [http://gstreamer.freedesktop.org/](http://gstreamer.freedesktop.org/)