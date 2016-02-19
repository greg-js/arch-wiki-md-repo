**X-Video Motion Compensation (XvMC)** is an extension for the X.Org Server. The XvMC API allows video programs to offload portions of the video decoding process to the GPU video-hardware. Particularly, features that have the tendency of heavily depending on the processor. Since XvMC acceleration takes the load off the CPU, thereby reducing processor requirements for video playback, it is an ideal solution for HDTV video playback scenarios.

**Note:** XvMC is obsoleted by [VA-API](/index.php/VA-API "VA-API") and [VDPAU](/index.php/VDPAU "VDPAU") nowadays, which have better support for recent GPUs.

## Contents

*   [1 Supported hardware](#Supported_hardware)
    *   [1.1 Configuration](#Configuration)
*   [2 Supported software](#Supported_software)
    *   [2.1 MPlayer](#MPlayer)
    *   [2.2 xine](#xine)
*   [3 References](#References)

## Supported hardware

Only MPEG-1 and MPEG-2 videos are supported by all driver.

*   [NVIDIA](/index.php/NVIDIA "NVIDIA") GeForce 6 and GeForce 7 series cards are supported by the proprietary [nvidia-304xx-utils](https://www.archlinux.org/packages/?name=nvidia-304xx-utils) package, available in the [official repositories](/index.php/Official_repositories "Official repositories").
*   NVIDIA GeForce 5 FX series cards are supported by the proprietary [nvidia-173xx-utils](https://aur.archlinux.org/packages/nvidia-173xx-utils/) package, available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").
*   NVIDIA GeForce4 series cards are supported by the proprietary [nvidia-96xx-utils](https://aur.archlinux.org/packages/nvidia-96xx-utils/) package, available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").
*   [Intel](/index.php/Intel "Intel") 810, GMA 950, GMA 3100, GMA 3000, GMA 4500 series and Ironlake GPUs are supported by the open source [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package, available in the [official repositories](/index.php/Official_repositories "Official repositories").
*   [AMD](/index.php/ATI_Catalyst "ATI Catalyst") Radeon HD 5000 series and newer GPUs are supported by the proprietary [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) package, available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").
*   AMD Radeon HD 4000 series GPUs are supported by the proprietary [catalyst-total-hd234k](https://aur.archlinux.org/packages/catalyst-total-hd234k/) package, available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").
*   [S3 Graphics](/index.php/Via_Unichrome "Via Unichrome") UniChrome GPUs are supported by the open source [xf86-video-openchrome](https://www.archlinux.org/packages/?name=xf86-video-openchrome) package, available in the [official repositories](/index.php/Official_repositories "Official repositories").

### Configuration

The open source drivers should work without any configuration. For the proprietary drivers create a new file `/etc/X11/XvMCConfig` and add:

*   For NVIDIA GPUs:

	 `libXvMCNVIDIA_dynamic.so.1` 

*   For AMD GPUs:

	 `libAMDXvBA.so.1` 

## Supported software

**Tip:** Using full screen mode and disabling GUI elements may prevent flickering while playing the video.

### [MPlayer](/index.php/MPlayer "MPlayer")

Install [mplayer](https://www.archlinux.org/packages/?name=mplayer) package, available in the [official repositories](/index.php/Official_repositories "Official repositories").

 `$ mplayer -vo xvmc -fs *foobar.mpeg*` 

*   **-vo** - Select xvmc video output driver
*   **-fs** - Fullscreen playback (optional)

MPlayer based players:

*   [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer): open preferences and set the video output to "xvmc", and select "Enable Video Hardware Support".
*   [smplayer](https://www.archlinux.org/packages/?name=smplayer): open preferences and set the video driver to "xvmc", and deselect "Enable screenshots".

### xine

Install [xine-ui](https://www.archlinux.org/packages/?name=xine-ui) package, available in the [official repositories](/index.php/Official_repositories "Official repositories").

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