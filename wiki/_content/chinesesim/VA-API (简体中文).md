**翻译状态：** 本文是英文页面 [VA-API](/index.php/VA-API "VA-API") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-01-27，点击[这里](https://wiki.archlinux.org/index.php?title=VA-API&diff=0&oldid=294616)可以查看翻译后英文页面的改动。

**[视频加速API (Video Acceleration API, 缩写为VA-API)](http://www.freedesktop.org/wiki/Software/vaapi)** 是一套提供视频硬件编解码的开源库和标准。

## Contents

*   [1 支持的硬件](#.E6.94.AF.E6.8C.81.E7.9A.84.E7.A1.AC.E4.BB.B6)
    *   [1.1 支持的格式](#.E6.94.AF.E6.8C.81.E7.9A.84.E6.A0.BC.E5.BC.8F)
    *   [1.2 配置](#.E9.85.8D.E7.BD.AE)
*   [2 支持的软件](#.E6.94.AF.E6.8C.81.E7.9A.84.E8.BD.AF.E4.BB.B6)
    *   [2.1 GStreamer](#GStreamer)
    *   [2.2 MPlayer](#MPlayer)
    *   [2.3 VLC media player](#VLC_media_player)

## 支持的硬件

**开源驱动:**

*   [AMD](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)"): 位于[官方软件仓库](/index.php/Official_Repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official Repositories (简体中文)")的[libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver)和[ati-dri](https://www.archlinux.org/packages/?name=ati-dri)两者为 Radeon 9500 或更新的GPU提供支持。

*   [Intel](/index.php/Intel_Graphics_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel Graphics (简体中文)"): 位于[官方软件仓库](/index.php/Official_Repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official Repositories (简体中文)")的[libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver)软件包为 GMA 4500 系列或者更新的GPU提供支持。

*   [NVIDIA](/index.php/Nouveau_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Nouveau (简体中文)"): 位于[官方软件仓库](/index.php/Official_Repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official Repositories (简体中文)")的[libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver)和[nouveau-dri](https://www.archlinux.org/packages/?name=nouveau-dri)两者为 GeForce 8 系列和更新的GPU提供支持。位于AUR的 [nouveau-fw](https://aur.archlinux.org/packages/nouveau-fw/) 软件包包含从NVIDIA闭源驱动中提取出的必要的固件文件。

**闭源驱动:**

*   [AMD](/index.php/AMD_Catalyst_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AMD Catalyst (简体中文)"): 位于[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")的[libva-xvba-driver](https://aur.archlinux.org/packages/libva-xvba-driver/)软件包为 Radeon HD 4000 系列或更新的GPU提供支持。在 Radeon HD 5000 系列或者更新的GPU上请使用 [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) 驱动；在 Radeon HD 4000 系列上使用 [catalyst-total-hd234k](https://aur.archlinux.org/packages/catalyst-total-hd234k/) 作为驱动程序。

*   [NVIDIA](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)"): 位于[官方软件仓库](/index.php/Official_Repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official Repositories (简体中文)")的[libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver)软件包和 [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) 驱动为 GeForce 8 系列或更新的GPU提供支持。

### 支持的格式

 [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) 和 [ati-dri](https://www.archlinux.org/packages/?name=ati-dri) | [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) | [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) 和 [nouveau-dri](https://www.archlinux.org/packages/?name=nouveau-dri) | [libva-xvba-driver](https://aur.archlinux.org/packages/libva-xvba-driver/) | [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) 和 [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) |
| MPEG2 解码 | AMD Radeon 9500 或更新 | Intel GMA 4500 或更新 | Nvidia GeForce 8 或更新 | AMD Radeon HD 4000 或更新 | Nvidia GeForce 8 或更新 |
| MPEG4 解码 | AMD Radeon HD 6000 或更新 | -- | Nvidia GeForce 200 或更新 | AMD Radeon HD 6000 或更新 | Nvidia GeForce 200 或更新 |
| H264 解码 | AMD Radeon HD 4000 或更新 | Intel GMA 4500, Ironlake Graphics 或更新 | Nvidia GeForce 8 或更新 | AMD Radeon HD 4000 或更新 | Nvidia GeForce 8 或更新 |
| VC1 解码 | AMD Radeon HD 4000 或更新 | Intel Sandy Bridge Graphics 或更新 | Nvidia GeForce 8200, 8300, 8400, 9300, 200 或更新 | AMD Radeon HD 4000 或更新 | Nvidia GeForce 8 或更新 |
| MPEG2 编码 | -- | Intel Ivy Bridge Graphics 或更新 | -- | -- | -- |
| H264 编码 | -- | Intel Sandy Bridge Graphics 或更新 | -- | -- | -- |

位于[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")的[libva-driver-intel-g45-h264](https://aur.archlinux.org/packages/libva-driver-intel-g45-h264/)软件包为其提供支持。具体方法和注意事项参看： [在 GMA 4500 硬解 H.264](/index.php/Intel_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.9C.A8_GMA_4500_.E7.A1.AC.E8.A7.A3_H.264 "Intel (简体中文)")。

运行下面的命令以查看你的GPU支持哪些功能。这个命令由 [libva](https://www.archlinux.org/packages/?name=libva) 软件包提供:

 `$ vainfo` 

_VAEntrypointVLD_ 表示你可以解码该格式，_VAEntrypointEncSlice_ 表示你可以编码该格式。

### 配置

[libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) 必须手动通过设置环境变量手动开启。参看[环境变量](/index.php?title=Environment_Variables_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Environment Variables (简体中文) (page does not exist)") [定义全局环境变量](/index.php?title=Environment_Variables_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Environment Variables (简体中文) (page does not exist)") 或 [定义本地环境变量](/index.php?title=Environment_Variables_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Environment Variables (简体中文) (page does not exist)")。

```
export LIBVA_DRIVER_NAME=vdpau

```

## 支持的软件

### [GStreamer](/index.php/GStreamer "GStreamer")

安装 [gst-vaapi](https://www.archlinux.org/packages/?name=gst-vaapi) 软件包，它存在于[官方软件仓库](/index.php/Official_Repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official Repositories (简体中文)")。

 `$ gst-launch-1.0 playbin uri=file://_/path/to/foobar.mpeg_` 

如果发现了支持的格式，VA-API会自动被使用。

基于GStreamer的播放器:

*   [totem](https://www.archlinux.org/packages/?name=totem): 不需要配置。

### [MPlayer](/index.php/MPlayer_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "MPlayer (简体中文)")

安装 [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/) 软件包，它存在于[官方软件仓库](/index.php/Official_Repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official Repositories (简体中文)")。

 `$ mplayer -vo vaapi -va vaapi _foobar.mpeg_` 

*   **-vo** - 指定 vaapi 视频输出驱动
*   **-va** - 指定 vaapi 视频解码驱动

**注意:** 你也可以配合VDPAU后端使用 [mplayer2](https://aur.archlinux.org/packages/mplayer2/) 。详情参看 [MPlayer (简体中文)#启用 VDPAU （适用于新款nVidia显卡）](/index.php/MPlayer_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.90.AF.E7.94.A8_VDPAU_.EF.BC.88.E9.80.82.E7.94.A8.E4.BA.8E.E6.96.B0.E6.AC.BEnVidia.E6.98.BE.E5.8D.A1.EF.BC.89 "MPlayer (简体中文)")。

基于 MPlayer 的播放器:

*   [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer): 开启硬件加速的方法: _编辑 > 首选项 > 播放器_, 并设置_视频输出_为 `vaapi`。
*   [smplayer](https://www.archlinux.org/packages/?name=smplayer): 开启硬件加速的方法: _选项 > 首选项 > 常规 > 视频_, 并设置_输出驱动_为 `vaapi`。

### VLC media player

安装 [vlc](https://www.archlinux.org/packages/?name=vlc) 软件包，它位于官方软件仓库。

开启硬件加速的方法: _工具 > 首选项 > 输入 / 编解码器_, 然后设置 _硬件加速解码_ 为 `视频加速 (VA) API`。