# VDPAU

Related articles

*   [VA-API](/index.php/VA-API "VA-API")
*   [XvMC](/index.php/XvMC "XvMC")

**[Video Decode and Presentation API for Unix](http://http.download.nvidia.com/XFree86/vdpau/doxygen/html/)** is an open source library and API to offload portions of the video decoding process and video post-processing to the GPU video-hardware.

## Contents

*   [1 Supported hardware](#Supported_hardware)
    *   [1.1 Supported formats](#Supported_formats)
    *   [1.2 Configuration](#Configuration)
        *   [1.2.1 Hybrid graphics](#Hybrid_graphics)
*   [2 Supported software](#Supported_software)

## Supported hardware

**Open source drivers:**

*   [AMD](/index.php/ATI "ATI") Radeon 9500 and newer GPUs are supported by the [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) package.
*   [Intel](/index.php/Intel "Intel") GMA 4500 series and newer GPUs are supported by the [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) package together with the [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) package.
*   [NVIDIA](/index.php/Nouveau "Nouveau") GeForce 8 series and newer GPUs are supported by the [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) package. It [requires](http://nouveau.freedesktop.org/wiki/VideoAcceleration/#firmware) the [nouveau-fw](https://aur.archlinux.org/packages/nouveau-fw/)<sup><small>AUR</small></sup> package, which contains the required firmware to operate that is presently extracted from the NVIDIA binary driver.

**Proprietary drivers:**

*   [AMD](/index.php/AMD_Catalyst "AMD Catalyst") Radeon HD 4000 series and newer GPUs are supported by the [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) package together with the [libva-xvba-driver](https://aur.archlinux.org/packages/libva-xvba-driver/)<sup><small>AUR</small></sup> package. It uses the [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/)<sup><small>AUR</small></sup> driver for Radeon HD 5000 series and newer, and [catalyst-total-hd234k](https://aur.archlinux.org/packages/catalyst-total-hd234k/)<sup><small>AUR</small></sup> for Radeon HD 4000 series.
*   [NVIDIA](/index.php/NVIDIA "NVIDIA") GeForce 400 series and newer GPUs are supported by the [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) package.
    *   GeForce 8/9 and GeForce 100-300 series are supported by the [nvidia-340xx-utils](https://www.archlinux.org/packages/?name=nvidia-340xx-utils) package.

### Supported formats

 Open source | Proprietary |
 AMD | Intel | Nvidia | AMD | Nvidia |
| MPEG2 decoding | Radeon 9500 and newer | 

<center>—<sup>2</sup></center>

 | GeForce 8 and newer | 

<center>—<sup>2</sup></center>

 | GeForce 8 and newer |
| MPEG4 decoding | Radeon HD 6000 and newer | 

<center>—<sup>2</sup></center>

 | GeForce 200 and newer | 

<center>—<sup>2</sup></center>

 | GeForce 200 and newer |
| H.264 decoding | Radeon HD 4000 and newer | GMA 4500<sup>1</sup>, Ironlake Graphics and newer | GeForce 8 and newer | Radeon HD 4000 and newer | GeForce 8 and newer |
| HEVC (H.265) decoding | 

<center>—</center>

 | 

<center>—<sup>2</sup></center>

 | 

<center>—</center>

 | 

<center>—<sup>2</sup></center>

 | GeForce 900<sup>4</sup> and newer |
| VC1 decoding | Radeon HD 4000 and newer | 

<center>—<sup>2</sup></center>

 | GeForce 8<sup>3</sup> and newer | 

<center>—<sup>2</sup></center>

 | GeForce 8<sup>3</sup> and newer |

*   <sup>1</sup> Supported by the [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/)<sup><small>AUR</small></sup> package. See [Intel graphics#H.264 decoding on GMA 4500](/index.php/Intel_graphics#H.264_decoding_on_GMA_4500 "Intel graphics") for instructions and caveats.
*   <sup>2</sup> As of version 0.3, the VA GL driver doesn't support any other hardware decoder than H.264.
*   <sup>3</sup> [Except](https://en.wikipedia.org/wiki/Nvidia_PureVideo "wikipedia:Nvidia PureVideo") GeForce 8800 Ultra, 8800 GTX, 8800 GTS (320/640 MB).
*   <sup>4</sup> Except GeForce GTX 970 and GTX 980.

In order to check what features are supported by your GPU, run the following command, which is provided by the [vdpauinfo](https://www.archlinux.org/packages/?name=vdpauinfo) package:

```
$ vdpauinfo

```

### Configuration

The environment variable `VDPAU_DRIVER` determines the driver file used. See [Environment variables#Defining variables](/index.php/Environment_variables#Defining_variables "Environment variables") for configuration details.

The correct driver name depends on your setup:

*   For Intel Graphics or AMD Catalyst you need to set it to `va_gl`.
*   For the open source AMD/ATI driver, you need to set it to the proper driver version depending on your GPU.
*   For Nvidia's proprietary version set the variable to "nvidia".

The driver name can determined by running:

 `$ grep -i vdpau ~/.local/share/xorg/Xorg.0.log` 

```
(II) RADEON(0): [DRI2] VDPAU driver: r300

```

In this case you want to set `VDPAU_DRIVER=r300`.

#### Hybrid graphics

For hybrid setups (both NVIDIA and AMD), it may be necessary to set following environment variable:

```
$ export DRI_PRIME=1

```

For more information, see the [PRIME](/index.php/PRIME "PRIME") wiki page.

## Supported software

*   **Adobe Flash Player** — see [Browser plugins#Adobe Flash Player](/index.php/Browser_plugins#Adobe_Flash_Player "Browser plugins").

	|| [flashplugin](https://www.archlinux.org/packages/?name=flashplugin)

*   **[MPlayer](/index.php/MPlayer "MPlayer") or [mplayer2](http://www.mplayer2.org/)** — see [MPlayer#Enabling VDPAU](/index.php/MPlayer#Enabling_VDPAU "MPlayer").

	|| [mplayer](https://www.archlinux.org/packages/?name=mplayer) [mplayer2](https://aur.archlinux.org/packages/mplayer2/)<sup><small>AUR</small></sup>

*   **gnome-mplayer** — To enable hardware acceleration: _Edit > Preferences > Player_, then set Video Output to `vdpau`.

	|| [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer)

*   **[SMplayer](/index.php/SMplayer "SMplayer")** — To enable hardware acceleration: _Options > Preferences > General > Video_, then set Output driver to `vdpau`.

	|| [smplayer](https://www.archlinux.org/packages/?name=smplayer)

*   **bomi** — Hardware acceleration can be enabled: _Preferences > Video > Hardware acceleration_.

	[https://bomi-player.github.io](https://bomi-player.github.io) || [bomi](https://aur.archlinux.org/packages/bomi/)<sup><small>AUR</small></sup> [bomi-git](https://aur.archlinux.org/packages/bomi-git/)<sup><small>AUR</small></sup>

*   **[Mpv](/index.php/Mpv "Mpv")** — see [Mpv#Hardware Decoding](/index.php/Mpv#Hardware_Decoding "Mpv").

	|| [mpv](https://www.archlinux.org/packages/?name=mpv)

*   **[VLC media player](/index.php/VLC_media_player "VLC media player")** — see [VLC media player#Hardware acceleration support](/index.php/VLC_media_player#Hardware_acceleration_support "VLC media player").

	|| [vlc](https://www.archlinux.org/packages/?name=vlc)

Retrieved from "[https://wiki.archlinux.org/index.php?title=VDPAU&oldid=413761](https://wiki.archlinux.org/index.php?title=VDPAU&oldid=413761)"