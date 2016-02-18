**翻译状态：** 本文是英文页面 [XvMC](/index.php/XvMC "XvMC") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-01-27，点击[这里](https://wiki.archlinux.org/index.php?title=XvMC&diff=0&oldid=294620)可以查看翻译后英文页面的改动。

**X-视频运动补偿 (XvMC)** 是一个X.Org Server的扩展。XvMC API可以让视频程序转移部分解码工作到GPU。Particularly, features that have the tendency of heavily depending on the processor. Since XvMC acceleration takes the load off the CPU, thereby reducing processor requirements for video playback, it is an ideal solution for HDTV video playback scenarios.

**注意:** XvMC 如今已被 [VA-API](/index.php/VA-API_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "VA-API (简体中文)") 和 [VDPAU](/index.php/VDPAU_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "VDPAU (简体中文)") 淘汰。它们对新款的GPU有着更好的支持。

## Contents

*   [1 支持的硬件](#.E6.94.AF.E6.8C.81.E7.9A.84.E7.A1.AC.E4.BB.B6)
    *   [1.1 配置](#.E9.85.8D.E7.BD.AE)
*   [2 支持的软件](#.E6.94.AF.E6.8C.81.E7.9A.84.E8.BD.AF.E4.BB.B6)
    *   [2.1 MPlayer](#MPlayer)
    *   [2.2 xine](#xine)
*   [3 References](#References)

## 支持的硬件

Only MPEG-1 and MPEG-2 videos are supported by all driver.

*   [NVIDIA](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)") GeForce 6 and GeForce 7 series cards are supported by the proprietary [nvidia-304xx-utils](https://www.archlinux.org/packages/?name=nvidia-304xx-utils) package, available in the [官方软件仓库](/index.php/Official_Repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official Repositories (简体中文)").
*   NVIDIA GeForce 5 FX series cards are supported by the proprietary [nvidia-173xx-utils](https://aur.archlinux.org/packages/nvidia-173xx-utils/) package, available in the [AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)").
*   NVIDIA GeForce4 series cards are supported by the proprietary [nvidia-96xx-utils](https://aur.archlinux.org/packages/nvidia-96xx-utils/) package, available in the [AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)").
*   [Intel](/index.php/Intel_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel (简体中文)") 810, GMA 950, GMA 3100, GMA 3000, GMA 4500 series and Ironlake GPUs are supported by the open source [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package, available in the [官方软件仓库](/index.php/Official_Repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official Repositories (简体中文)").
*   [AMD](/index.php?title=ATI_Catalyst_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "ATI Catalyst (简体中文) (page does not exist)") Radeon HD 5000 series and newer GPUs are supported by the proprietary [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) package, available in the [AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)").
*   AMD Radeon HD 4000 series GPUs are supported by the proprietary [catalyst-total-hd234k](https://aur.archlinux.org/packages/catalyst-total-hd234k/) package, available in the [AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)").
*   [S3 Graphics](/index.php?title=Via_Unichrome_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Via Unichrome (简体中文) (page does not exist)") UniChrome GPUs are supported by the open source [xf86-video-openchrome](https://www.archlinux.org/packages/?name=xf86-video-openchrome) package, available in the [官方软件仓库](/index.php/Official_Repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official Repositories (简体中文)").

### 配置

The open source drivers should work without any configuration. For the proprietary drivers create a new file `/etc/X11/XvMCConfig` and add:

*   For NVIDIA GPUs:

	 `libXvMCNVIDIA_dynamic.so.1` 

*   For AMD GPUs:

	 `libAMDXvBA.so.1` 

## 支持的软件

**Tip:** Using full screen mode and disabling GUI elements may prevent flickering while playing the video.

### [MPlayer](/index.php/MPlayer_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "MPlayer (简体中文)")

Install [mplayer](https://www.archlinux.org/packages/?name=mplayer) package, available in the [官方软件仓库](/index.php/Official_Repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official Repositories (简体中文)").

 `$ mplayer -vo xvmc -fs *foobar.mpeg*` 

*   **-vo** - Select xvmc video output driver
*   **-fs** - Fullscreen playback (optional)

MPlayer based players:

*   [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer): open preferences and set the video output to "xvmc", and select "Enable Video Hardware Support".
*   [smplayer](https://www.archlinux.org/packages/?name=smplayer): open preferences and set the video driver to "xvmc", and deselect "Enable screenshots".

### xine

Install [xine-ui](https://www.archlinux.org/packages/?name=xine-ui) package, available in the [官方软件仓库](/index.php/Official_Repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official Repositories (简体中文)").

 `$ xine -V xvmc -f -g --no-splash *foobar.mpeg*` 

or

 `$ xine -V xxmc -f -g --no-splash *foobar.mpeg*` 

*   **-V** - Select the xvmc or xxmc video driver
*   **-f** - Start in fullscreen mode (optional)
*   **-g** - Hide GUI (optional)
*   **--no-splash** - Don't display the splash screen (optional)

## References

*   [XvMC (from MythTV wiki)](http://www.mythtv.org/wiki/XvMC)
*   [MPlayer 1.0rc1 + XvMC Nov 2006](http://www.murga-linux.com/puppy/viewtopic.php?t=13216)
*   [Using older machines for HDTV video playback](http://www.penlug.org/twiki/bin/view/Main/LinuxHardwareInfoNvidia5200)
*   [Xine's xxmc plugin](http://www.grogy.com/local_doc/share/doc/xine-lib/README_xxmc.html)