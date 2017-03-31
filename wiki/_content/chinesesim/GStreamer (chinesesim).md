**翻译状态：** 本文是英文页面 [GStreamer](/index.php/GStreamer "GStreamer") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间： 2014-06-15，点击[这里](https://wiki.archlinux.org/index.php?title=GStreamer&diff=0&oldid=313588)可以查看翻译后英文页面的改动。

Gstreamer是一个基于管道的多媒体框架。Gstreamer使用C语言编写，基于GObject。 Gstreamer允许程序员创建各种媒体处理组件，包括简单的音频播放，音频与视频播放，录制，流媒体控制与媒体编辑。其管道式设计是创建多种多媒体程序的基础，例如视频编辑器，流媒体服务器，以及媒体播放器。 Gstreamer是跨平台框架，目前已知可在下列平台上工作：Linux (x86, PowerPC 以及 ARM), Solaris (Intel 和 SPARC), Mac OS X, Microsoft Windows 以及 OS/400。Gstreamer是发布在GPL（GNU通用公共授权）协议下的自由软件。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 整合](#.E6.95.B4.E5.90.88)
    *   [2.1 PulseAudio](#PulseAudio)
    *   [2.2 轻量级桌面](#.E8.BD.BB.E9.87.8F.E7.BA.A7.E6.A1.8C.E9.9D.A2)
    *   [2.3 KDE / Phonon integration](#KDE_.2F_Phonon_integration)
    *   [2.4 硬件加速](#.E7.A1.AC.E4.BB.B6.E5.8A.A0.E9.80.9F)
*   [3 Bugs](#Bugs)
*   [4 相关链接](#.E7.9B.B8.E5.85.B3.E9.93.BE.E6.8E.A5)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [gstreamer](https://www.archlinux.org/packages/?name=gstreamer) 软件包.

为了让gstreamer发挥作用，安装你所需要的插件

*   [gst-libav](https://www.archlinux.org/packages/?name=gst-libav) - 基于Libav的插件，包含众多编解码器。
*   [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad) - 需要更多改进，测试以及资料的插件。
*   [gst-plugins-base](https://www.archlinux.org/packages/?name=gst-plugins-base) - 基本的Gstreamer组件。
*   [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good) - 发布于LGPL许可证下，质量较高的插件。
*   [gst-plugins-ugly](https://www.archlinux.org/packages/?name=gst-plugins-ugly) - 质量较高，但是可能造成分发问题的插件。
*   [gst-plugin-libde265](https://aur.archlinux.org/packages/gst-plugin-libde265/) - [libde265](https://aur.archlinux.org/packages/libde265/) 插件 (开源的h.265视频解码实现)。

## 整合

### PulseAudio

[PulseAudio](/index.php/PulseAudio "PulseAudio") 支持由 *good* 插件包提供.

### 轻量级桌面

如果需要设置GStreamer，例如切换音频输出设备，使用[gstreamer-properties](https://aur.archlinux.org/packages/gstreamer-properties/)软件包提供的*gstreamer-properties*。这个程序可以以每个用户的身份独立进行配置，或者以root身份进行全局配置。每个用户的独立设置放在`$HOME/.gconf/system/gstreamer`目录下，全局设置放在`/etc/gconf/gconf.xml.defaults`目录下。

### KDE / Phonon integration

请查看 [Phonon](/index.php/Phonon "Phonon").

### 硬件加速

见 [Hardware video acceleration (简体中文)](/index.php/Hardware_video_acceleration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Hardware video acceleration (简体中文)").

GStreamer 将会自动的检测并使用正确的 API [[1]](http://docs.gstreamer.com/display/GstSDK/Playback+tutorial+8%3A+Hardware-accelerated+video+decoding). 根据您的系统，您可以安装：

*   [gstreamer-vaapi](https://www.archlinux.org/packages/?name=gstreamer-vaapi) for VA-API support.
*   [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad) for VDPAU support.

**注意:** 在 Intel GPUs 上启用 VA-API 支持可能会遇到视频文件缩略图的问题 详见 [GNOME Files#Thumbnailing not working for video files](/index.php/GNOME_Files#Thumbnailing_not_working_for_video_files "GNOME Files").

## Bugs

如果使用录制软件录制视频时出现`GStreamer-CRITICAL **: gst_mini_object_unref: assertion `mini_object->refcount > 0' failed`错误， 安装 [gstreamer0.10-ffmpeg](https://aur.archlinux.org/packages/gstreamer0.10-ffmpeg/) 以便修复.

## 相关链接

*   [Sound](/index.php/Sound "Sound")
*   [http://gstreamer.freedesktop.org/](http://gstreamer.freedesktop.org/)