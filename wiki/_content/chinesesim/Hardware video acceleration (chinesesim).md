相关文章

*   [VDPAU](/index.php/VDPAU_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "VDPAU (简体中文)")
*   [XvMC](/index.php/XvMC_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "XvMC (简体中文)")

**翻译状态：** 本文是英文页面 [VA-API](/index.php/VA-API "VA-API") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-01-27，点击[这里](https://wiki.archlinux.org/index.php?title=VA-API&diff=0&oldid=294616)可以查看翻译后英文页面的改动。

Hardware video acceleration makes it possible for the video card to decode/encode video, thus offloading the CPU and saving power.

Linux 中有多种方式可以实现视频加速:

*   **[视频加速API (Video Acceleration API, 缩写为VA-API)](http://www.freedesktop.org/wiki/Software/vaapi)** 是一套提供视频硬件编解码的开源库和标准。
*   **[Unix视频解码及演示 API （Video Decode and Presentation API for Unix，缩写为VDPAU）](http://http.download.nvidia.com/XFree86/vdpau/doxygen/html/)**是一个开源的库，它使得部分的视频解码和视频后期处理任务转移到GPU硬件上。

## Contents

*   [1 支持的硬件](#支持的硬件)
    *   [1.1 VA-API](#VA-API)
    *   [1.2 VDPAU](#VDPAU)
*   [2 支持的格式](#支持的格式)
    *   [2.1 VA-API](#VA-API_2)
    *   [2.2 VDPAU](#VDPAU_2)
*   [3 配置](#配置)
    *   [3.1 多显卡显示](#多显卡显示)
*   [4 支持的软件](#支持的软件)
    *   [4.1 开启软件的硬件加速](#开启软件的硬件加速)
    *   [4.2 GStreamer](#GStreamer)
    *   [4.3 MPlayer](#MPlayer)
    *   [4.4 VLC media player](#VLC_media_player)

## 支持的硬件

### VA-API

**开源驱动:**

*   [AMD](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)"): 位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的[libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver)和[mesa](https://www.archlinux.org/packages/?name=mesa)两者为 Radeon 9500 或更新的GPU提供支持。

*   [Intel](/index.php/Intel_graphics_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel graphics (简体中文)"): 位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的[libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver)软件包为 GMA 4500 系列或者更新的GPU提供支持。

*   [NVIDIA](/index.php/Nouveau_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Nouveau (简体中文)"): 位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的[libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver)和[mesa](https://www.archlinux.org/packages/?name=mesa)两者为 GeForce 8 系列和更新的GPU提供支持。位于AUR的 [nouveau-fw](https://aur.archlinux.org/packages/nouveau-fw/) 软件包包含从NVIDIA闭源驱动中提取出的必要的固件文件。

**闭源驱动:**

*   [AMD](/index.php/AMD_Catalyst_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AMD Catalyst (简体中文)"): 位于[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")的[libva-xvba-driver](https://aur.archlinux.org/packages/libva-xvba-driver/)软件包为 Radeon HD 4000 系列或更新的GPU提供支持。在 Radeon HD 5000 系列或者更新的GPU上请使用 [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) 驱动；在 Radeon HD 4000 系列上使用 [catalyst-total-hd234k](https://aur.archlinux.org/packages/catalyst-total-hd234k/) 作为驱动程序。

*   [NVIDIA](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)"): 位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的[libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver)软件包和 [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) 驱动为 GeForce 8 系列或更新的GPU提供支持。

### VDPAU

**开源驱动:**

*   [AMD](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)"): 位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的 [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) 软件包为 Radeon 9500 或更新的GPU提供支持。

*   [Intel](/index.php/Intel_graphics_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel graphics (简体中文)"): 位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的[libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl)和[libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver)这两个软件包为 GMA 4500 系列或者更新的GPU提供支持。

*   [NVIDIA](/index.php/Nouveau_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Nouveau (简体中文)"): 位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的 [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) 软件包为 GeForce 8 系列和更新的GPU提供支持。位于AUR的 [nouveau-fw](https://aur.archlinux.org/packages/nouveau-fw/) 软件包包含从NVIDIA闭源驱动中提取出的必要的[固件](http://nouveau.freedesktop.org/wiki/VideoAcceleration/#firmware) 。

**闭源驱动:**

*   [AMD](/index.php/AMD_Catalyst_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AMD Catalyst (简体中文)"): 位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的[libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl)、位于[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")的[libva-xvba-driver](https://aur.archlinux.org/packages/libva-xvba-driver/)软件包两者为 Radeon HD 4000 系列或更新的GPU提供支持。在 Radeon HD 5000 系列或者更新的GPU上请使用 [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) 驱动；在 Radeon HD 4000 系列上 使用 [catalyst-total-hd234k](https://aur.archlinux.org/packages/catalyst-total-hd234k/) 作为驱动程序。

*   [NVIDIA](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)"): 位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的[nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils)软件包为 GeForce 400 系列或更新的GPU提供支持。
*   GeForce 8/9 和 GeForce 100-300 系列由 [nvidia-340xx-utils](https://www.archlinux.org/packages/?name=nvidia-340xx-utils) 软件包支持。

## 支持的格式

### VA-API

 Open source | Proprietary |
 AMD | Intel | Nvidia | AMD | Nvidia |
| MPEG2 解码 | AMD Radeon 9500 或更新 | Intel GMA 4500 或更新 | Nvidia GeForce 8 或更新 | AMD Radeon HD 4000 或更新 | Nvidia GeForce 8 或更新 |
| MPEG4 解码 | AMD Radeon HD 6000 或更新 | -- | Nvidia GeForce 200 或更新 | AMD Radeon HD 6000 或更新 | Nvidia GeForce 200 或更新 |
| H264 解码 | AMD Radeon HD 4000 或更新 | Intel GMA 4500, Ironlake Graphics 或更新 | Nvidia GeForce 8 或更新 | AMD Radeon HD 4000 或更新 | Nvidia GeForce 8 或更新 |
| VC1 解码 | AMD Radeon HD 4000 或更新 | Intel Sandy Bridge Graphics 或更新 | Nvidia GeForce 8200, 8300, 8400, 9300, 200 或更新 | AMD Radeon HD 4000 或更新 | Nvidia GeForce 8 或更新 |
| MPEG2 编码 | -- | Intel Ivy Bridge Graphics 或更新 | -- | -- | -- |
| H264 编码 | -- | Intel Sandy Bridge Graphics 或更新 | -- | -- | -- |

[libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/) 软件包为其提供支持。具体方法和注意事项参看： [在 GMA 4500 硬解 H.264](/index.php/Intel_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#在_GMA_4500_硬解_H.264 "Intel (简体中文)")。

运行下面的命令以查看你的GPU支持哪些功能。这个命令由 [libva-utils](https://www.archlinux.org/packages/?name=libva-utils) 软件包提供:

 `$ vainfo` 

*VAEntrypointVLD* 表示你可以解码该格式，*VAEntrypointEncSlice* 表示你可以编码该格式。

### VDPAU

 开源 | 闭源 |
 AMD | Intel | Nvidia | AMD | Nvidia |
| MPEG2 decoding | Radeon 9500 and newer | 

<center>—</center>

 | GeForce 8 and newer | 

<center>—</center>

 | GeForce 8 and newer |
| MPEG4 decoding | Radeon HD 6000 and newer | 

<center>—</center>

 | GeForce 200 and newer | 

<center>—</center>

 | GeForce 200 and newer |
| H.264 decoding | Radeon HD 4000 and newer | GMA 4500, Ironlake Graphics and newer | GeForce 8 and newer | Radeon HD 4000 and newer | GeForce 8 and newer |
| HEVC (H.265) decoding | 

<center>—</center>

 | 

<center>—</center>

 | 

<center>—</center>

 | 

<center>—</center>

 | GeForce 900 and newer |
| VC1 decoding | Radeon HD 4000 and newer | 

<center>—</center>

 | GeForce 8 and newer | 

<center>—</center>

 | GeForce 8 and newer |

*   Supported by the [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/) package. See [Intel graphics#H.264 decoding on GMA 4500](/index.php/Intel_graphics#H.264_decoding_on_GMA_4500 "Intel graphics") for instructions and caveats.
*   As of version 0.3, the VA GL driver doesn't support any other hardware decoder than H.264.
*   [Except](https://en.wikipedia.org/wiki/Nvidia_PureVideo "wikipedia:Nvidia PureVideo") GeForce 8800 Ultra, 8800 GTX, 8800 GTS (320/640 MB).
*   Except GeForce GTX 970 and GTX 980.

要检查一个功能是否被 GPU 支持，可以使用 [vdpauinfo](https://www.archlinux.org/packages/?name=vdpauinfo) 软件包提供的命令：

```
$ vdpauinfo

```

## 配置

环境变量 `VDPAU_DRIVER` 决定使用的驱动。可以[全局设置](/index.php/Environment_variables#Defining_variables "Environment variables") 或 [针对一个用户](/index.php/Environment_variables#Defining_variables "Environment variables") 设置 [环境变量](/index.php/Environment_variables "Environment variables")

正确的驱动程序名称取决于您的设置：

*   Intel 或 AMD Catalyst 使用 `va_gl`.
*   开源AMD/ATI驱动程序,您需要将它设置为适当的驱动程序版本取决于你的GPU。
*   Nvidia的专有版本将变量设置为“nvidia”。

 `$ grep -i vdpau /var/log/Xorg.0.log` 
```
(II) RADEON(0): [DRI2] VDPAU driver: r300

```

然后设置 VDPAU 驱动：

```
VDPAU_DRIVER=r300

```

### 多显卡显示

对混合显卡(NVIDIA和AMD)，需要设置下面环境变量。

```
$ export DRI_PRIME=1

```

更多信息，参阅 [PRIME](/index.php/PRIME "PRIME") wiki 页面。

## 支持的软件

### 开启软件的硬件加速

*   **Adobe Flash Player** — 见 [Browser plugins#Adobe Flash Player](/index.php/Browser_plugins#Adobe_Flash_Player "Browser plugins").

	|| [flashplugin](https://www.archlinux.org/packages/?name=flashplugin)

*   **[MPlayer](/index.php/MPlayer "MPlayer") 或 [mplayer2](http://www.mplayer2.org/)** — 见[MPlayer#Enabling VDPAU](/index.php/MPlayer#Enabling_VDPAU "MPlayer").

	|| [mplayer](https://www.archlinux.org/packages/?name=mplayer) [mplayer2](https://aur.archlinux.org/packages/mplayer2/)

*   **gnome-mplayer** — 开启硬件加速: *Edit > Preferences > Player*, 设置 Video Output 为 `vdpau`.

	|| [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer)

*   **[SMplayer](/index.php/SMplayer "SMplayer")** — 开启硬件加速: *Options > Preferences > General > Video*, 设置 Output driver 为 `vdpau`.

	|| [smplayer](https://www.archlinux.org/packages/?name=smplayer)

*   **bomi** — 硬件加速可以启用: *Preferences > Video > Hardware acceleration*.

	[https://bomi-player.github.io](https://bomi-player.github.io) || [bomi](https://aur.archlinux.org/packages/bomi/) [bomi-git](https://aur.archlinux.org/packages/bomi-git/)

*   **[Mpv](/index.php/Mpv "Mpv")** — 见 [Mpv#Hardware decoding](/index.php/Mpv#Hardware_decoding "Mpv").

	|| [mpv](https://www.archlinux.org/packages/?name=mpv)

*   **[VLC media player](/index.php/VLC_media_player "VLC media player")** — 见 [VLC media player#Hardware acceleration support](/index.php/VLC_media_player#Hardware_acceleration_support "VLC media player").

	|| [vlc](https://www.archlinux.org/packages/?name=vlc)

### [GStreamer](/index.php/GStreamer "GStreamer")

安装 [gstreamer-vaapi](https://www.archlinux.org/packages/?name=gstreamer-vaapi) 软件包，它存在于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")。

 `$ gst-launch-1.0 playbin uri=file://*/path/to/foobar.mpeg*` 

如果发现了支持的格式，VA-API会自动被使用。

基于GStreamer的播放器:

*   [totem](https://www.archlinux.org/packages/?name=totem): 不需要配置。

### [MPlayer](/index.php/MPlayer_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "MPlayer (简体中文)")

安装 [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/) 软件包，它存在于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")。

 `$ mplayer -vo vaapi -va vaapi *foobar.mpeg*` 

*   **-vo** - 指定 vaapi 视频输出驱动
*   **-va** - 指定 vaapi 视频解码驱动

**注意:** 你也可以配合VDPAU后端使用 [mplayer2](https://aur.archlinux.org/packages/mplayer2/) 。详情参看 [MPlayer (简体中文)#启用 VDPAU （适用于新款nVidia显卡）](/index.php/MPlayer_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#启用_VDPAU_（适用于新款nVidia显卡） "MPlayer (简体中文)")。

基于 MPlayer 的播放器:

*   [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer): 开启硬件加速的方法: *编辑 > 首选项 > 播放器*, 并设置*视频输出*为 `vaapi`。
*   [smplayer](https://www.archlinux.org/packages/?name=smplayer): 开启硬件加速的方法: *选项 > 首选项 > 常规 > 视频*, 并设置*输出驱动*为 `vaapi`。

### VLC media player

安装 [vlc](https://www.archlinux.org/packages/?name=vlc) 软件包，它位于官方软件仓库。

开启硬件加速的方法: *工具 > 首选项 > 输入 / 编解码器*, 然后设置 *硬件加速解码* 为 `视频加速 (VA) API`。