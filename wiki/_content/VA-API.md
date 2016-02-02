# VA-API

**[Video Acceleration API](http://www.freedesktop.org/wiki/Software/vaapi)** is a specification and open source library to provide hardware accelerated video encoding and decoding.

## Contents

*   [1 Supported hardware](#Supported_hardware)
    *   [1.1 Supported formats](#Supported_formats)
    *   [1.2 Configuration](#Configuration)
    *   [1.3 Verifying](#Verifying)
*   [2 Supported software](#Supported_software)

## Supported hardware

**Open source drivers:**

*   [AMD](/index.php/ATI "ATI") Radeon 9500 and newer GPUs are supported by the [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) package together with the [mesa](https://www.archlinux.org/packages/?name=mesa) package.
*   [Intel](/index.php/Intel "Intel") GMA 4500 series and newer GPUs are supported by the [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) package together with the [mesa](https://www.archlinux.org/packages/?name=mesa) package.
*   [NVIDIA](/index.php/Nouveau "Nouveau") GeForce 8 series and newer GPUs are supported by the [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) package together with the [mesa](https://www.archlinux.org/packages/?name=mesa) package. It uses the [nouveau-fw](https://aur.archlinux.org/packages/nouveau-fw/) package, which contains the required firmware to operate that is presently extracted from the NVIDIA binary driver.

**Proprietary drivers:**

*   [AMD](/index.php/AMD_Catalyst "AMD Catalyst") Radeon HD 4000 series and newer GPUs are supported by the [libva-xvba-driver](https://aur.archlinux.org/packages/libva-xvba-driver/) package. It uses the [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) driver for Radeon HD 5000 series and newer, and [catalyst-total-hd234k](https://aur.archlinux.org/packages/catalyst-total-hd234k/) for Radeon HD 4000 series.
*   [NVIDIA](/index.php/NVIDIA "NVIDIA") GeForce 8 series and newer GPUs are supported by the [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) package together with the [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) driver.

### Supported formats

 Open source | Proprietary |
 AMD | Intel | Nvidia | AMD | Nvidia |
| MPEG2 decoding | Radeon 9500 and newer | GMA 4500 and newer | GeForce 8 and newer | Radeon HD 4000 and newer | GeForce 8 and newer |
| MPEG4 decoding | Radeon HD 6000 and newer | 

<center>—</center>

 | GeForce 200 and newer | Radeon HD 6000 and newer | GeForce 200 and newer |
| H264 decoding | Radeon HD 4000 and newer | GMA 4500, Ironlake Graphics and newer | GeForce 8 and newer | Radeon HD 4000 and newer | GeForce 8 and newer |
| VC1 decoding | Radeon HD 4000 and newer | Sandy Bridge Graphics and newer | GeForce 8200, 8300, 8400, 9300, 200 and newer | Radeon HD 4000 and newer | GeForce 8 and newer |
| MPEG2 encoding | 

<center>—</center>

 | Ivy Bridge Graphics and newer | 

<center>—</center>

 | 

<center>—</center>

 | 

<center>—</center>

 |
| H264 encoding | 

<center>—</center>

 | Sandy Bridge Graphics and newer | 

<center>—</center>

 | 

<center>—</center>

 | 

<center>—</center>

 |

Supported by the [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/) package. See [H.264 decoding on GMA 4500](/index.php/Intel_graphics#H.264_decoding_on_GMA_4500 "Intel graphics") for instructions and caveats.

In order to check what profiles (features) are supported by your GPU, you may want to read the [#Verifying](#Verifying) section.

### Configuration

The [driver](http://www.freedesktop.org/wiki/Software/vaapi/#driversback-endsthatimplementva-api) used by VA-API is autodetected, but sometimes it may be necessary to configure it manually by setting the [environment variable](/index.php/Environment_variable "Environment variable") `LIBVA_DRIVER_NAME`, for example:

```
export LIBVA_DRIVER_NAME=vdpau

```

### Verifying

Verify the settings for VAAPI by running `vainfo`, which is provided by the [libva](https://www.archlinux.org/packages/?name=libva) package:

 `$ vainfo` 

```
libva info: VA-API version 0.38.0
libva info: va_getDriverName() returns 0
libva info: User requested driver 'vdpau'
libva info: Trying to open /usr/lib/dri/vdpau_drv_video.so
libva info: Found init function __vaDriverInit_0_35
libva info: va_openDriver() returns 0
vainfo: VA-API version: 0.38 (libva 1.6.1)
vainfo: Driver version: Splitted-Desktop Systems VDPAU backend for VA-API - 0.7.4
vainfo: Supported profile and entrypoints
      VAProfileMPEG2Simple            : VAEntrypointVLD
      VAProfileMPEG2Main              : VAEntrypointVLD
      VAProfileMPEG4Simple            : VAEntrypointVLD
      VAProfileMPEG4AdvancedSimple    : VAEntrypointVLD
      VAProfileH264Baseline           : VAEntrypointVLD
      VAProfileH264Main               : VAEntrypointVLD
      VAProfileH264High               : VAEntrypointVLD
      VAProfileVC1Simple              : VAEntrypointVLD
      VAProfileVC1Main                : VAEntrypointVLD
      VAProfileVC1Advanced            : VAEntrypointVLD
```

_VAEntrypointVLD_ means that your card is capable to decode this format, _VAEntrypointEncSlice_ means that you can encode to this format.

## Supported software

*   [GStreamer](/index.php/GStreamer "GStreamer") based players - VA-API is used automatically, if supported format found.

	See more at [http://docs.gstreamer.com/display/GstSDK/Playback+tutorial+8%3A+Hardware-accelerated+video+decoding](http://docs.gstreamer.com/display/GstSDK/Playback+tutorial+8%3A+Hardware-accelerated+video+decoding).

*   VLC media player: see [VLC media player#Hardware acceleration support](/index.php/VLC_media_player#Hardware_acceleration_support "VLC media player").
*   Mpv: see [Mpv#Hardware Decoding](/index.php/Mpv#Hardware_Decoding "Mpv").
*   MPlayer: see [MPlayer#Enabling VA-API](/index.php/MPlayer#Enabling_VA-API "MPlayer").

Retrieved from "[https://wiki.archlinux.org/index.php?title=VA-API&oldid=413762](https://wiki.archlinux.org/index.php?title=VA-API&oldid=413762)"