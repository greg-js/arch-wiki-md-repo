[Hardware video acceleration](https://en.wikipedia.org/wiki/Graphics_processing_unit#GPU_accelerated_video_decoding "wikipedia:Graphics processing unit") makes it possible for the video card to decode/encode video, thus offloading the CPU and saving power.

There are several ways to achieve this on Linux:

*   [Video Acceleration API](https://www.freedesktop.org/wiki/Software/vaapi/) (VA-API) is a specification and open source library to provide both hardware accelerated video encoding and decoding, developed by Intel.
*   [Video Decode and Presentation API for Unix](https://www.freedesktop.org/wiki/Software/VDPAU/) (VDPAU) is an open source library and API to offload portions of the video decoding process and video post-processing to the GPU video-hardware, developed by NVIDIA.
*   [NVDECODE/NVENCODE](https://developer.nvidia.com/nvidia-video-codec-sdk) - proprietary APIs for hardware video acceleration used by NVIDIA Fermi, Kepler, Maxwell and Pascal generation GPUs.

For pre-2007 video cards see [XvMC](/index.php/XvMC "XvMC"). For comprehensive overview of driver and application support see [#Comparison tables](#Comparison_tables).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Intel](#Intel)
    *   [1.2 NVIDIA](#NVIDIA)
    *   [1.3 ATI/AMD](#ATI/AMD)
    *   [1.4 Translation layers](#Translation_layers)
*   [2 Verification](#Verification)
    *   [2.1 Verifying VA-API](#Verifying_VA-API)
    *   [2.2 Verifying VDPAU](#Verifying_VDPAU)
*   [3 Configuration](#Configuration)
    *   [3.1 Configuring VA-API](#Configuring_VA-API)
    *   [3.2 Configuring VDPAU](#Configuring_VDPAU)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Failed to open VDPAU backend](#Failed_to_open_VDPAU_backend)
    *   [4.2 VAAPI init failed](#VAAPI_init_failed)
*   [5 Comparison tables](#Comparison_tables)
    *   [5.1 VA-API drivers](#VA-API_drivers)
    *   [5.2 VDPAU drivers](#VDPAU_drivers)
    *   [5.3 NVIDIA driver only](#NVIDIA_driver_only)
    *   [5.4 Application support](#Application_support)

## Installation

### Intel

[Intel graphics](/index.php/Intel_graphics "Intel graphics") open-source drivers support VA-API:

*   HD Graphics series starting from [Broadwell](https://github.com/intel/media-driver/#supported-platforms) [(~2015)](https://en.wikipedia.org/wiki/Template:Intel_processor_roadmap "wikipedia:Template:Intel processor roadmap") and newer are supported by [intel-media-driver](https://www.archlinux.org/packages/?name=intel-media-driver).
*   GMA 4500 [series](https://01.org/linuxmedia/vaapi) and newer GPUs up to [Coffee Lake](https://en.wikipedia.org/wiki/Coffee_Lake "wikipedia:Coffee Lake") are supported by [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver).
*   GMA 4500 H.264 decoding is supported by [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/), see [Intel#Hardware accelerated H.264 decoding on GMA 4500](/index.php/Intel#Hardware_accelerated_H.264_decoding_on_GMA_4500 "Intel").
*   Broadwell to Skylake VP9 decoding and Haswell to Skylake hybrid VP8 encoding is supported by [intel-hybrid-codec-driver](https://aur.archlinux.org/packages/intel-hybrid-codec-driver/). [VP9 decoding on Haswell crashes](https://github.com/intel/intel-hybrid-driver/issues/21).

### NVIDIA

[Nouveau](/index.php/Nouveau "Nouveau") open-source driver supports both VA-API and VDPAU:

*   GeForce 8 series and newer GPUs up until GeForce GTX 750 are supported by [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver) and [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau).
*   [Requires](https://nouveau.freedesktop.org/wiki/VideoAcceleration/#firmware) [nouveau-fw](https://aur.archlinux.org/packages/nouveau-fw/) firmware package, presently extracted from the NVIDIA binary driver.

[NVIDIA](/index.php/NVIDIA "NVIDIA") proprietary driver supports via [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils):

*   VDPAU on [GeForce 8 series](https://en.wikipedia.org/wiki/GeForce_8_series "wikipedia:GeForce 8 series") and newer GPUs;
*   NVDECODE on [Fermi](https://en.wikipedia.org/wiki/Fermi_(microarchitecture) and newer GPUs [[1]](https://developer.download.nvidia.com/assets/cuda/files/NVIDIA_Video_Decoder.pdf);
*   NVENCODE on [Kepler](https://en.wikipedia.org/wiki/Kepler_(microarchitecture) and newer GPUs.

### ATI/AMD

[ATI](/index.php/ATI "ATI") and [AMDGPU](/index.php/AMDGPU "AMDGPU") open-source drivers support both VA-API and VDPAU:

*   VA-API on Radeon HD 2000 and newer GPUs is supported by [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver).
*   VDPAU on Radeon R300 and newer GPUs is supported by [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau).

[AMDGPU PRO](/index.php/AMDGPU_PRO "AMDGPU PRO") proprietary driver is built on top of AMDGPU driver and supports both VA-API and VDPAU.

### Translation layers

To get VA-API support when device driver provides none:

*   [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) – VDPAU backend for VA-API.
*   [libva-vdpau-driver-chromium](https://aur.archlinux.org/packages/libva-vdpau-driver-chromium/) – VDPAU backend for VA-API, patched to work with [Chromium](/index.php/Chromium "Chromium").

To get VDPAU support when device driver provides none:

*   [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) – VA-API backend for VDPAU, [only H.264 support](https://github.com/i-rinat/libvdpau-va-gl/issues/67#issuecomment-318470175).

## Verification

Your system may work perfectly out-of-the-box without needing any configuration. Therefore it is a good idea to start with this section to see that it is the case.

**Tip:** [mpv](/index.php/Mpv#Hardware_video_acceleration "Mpv") is great for testing hardware acceleration in practice.

### Verifying VA-API

Verify the settings for VA-API by running `vainfo`, which is provided by [libva-utils](https://www.archlinux.org/packages/?name=libva-utils):

 `$ vainfo` 
```
libva info: VA-API version 0.39.4
libva info: va_getDriverName() returns 0
libva info: Trying to open /usr/lib/dri/i965_drv_video.so
libva info: Found init function __vaDriverInit_0_39
libva info: va_openDriver() returns 0
vainfo: VA-API version: 0.39 (libva 1.7.3)
vainfo: Driver version: Intel i965 driver for Intel(R) Skylake - 1.7.3
vainfo: Supported profile and entrypoints
      VAProfileMPEG2Simple            :	VAEntrypointVLD
      VAProfileMPEG2Simple            :	VAEntrypointEncSlice
      VAProfileMPEG2Main              :	VAEntrypointVLD
      VAProfileMPEG2Main              :	VAEntrypointEncSlice
      VAProfileH264ConstrainedBaseline:	VAEntrypointVLD
      VAProfileH264ConstrainedBaseline:	VAEntrypointEncSlice
      VAProfileH264ConstrainedBaseline:	VAEntrypointEncSliceLP
      VAProfileH264Main               :	VAEntrypointVLD
      VAProfileH264Main               :	VAEntrypointEncSlice
      VAProfileH264Main               :	VAEntrypointEncSliceLP
      VAProfileH264High               :	VAEntrypointVLD
      VAProfileH264High               :	VAEntrypointEncSlice
      VAProfileH264High               :	VAEntrypointEncSliceLP
      VAProfileH264MultiviewHigh      :	VAEntrypointVLD
      VAProfileH264MultiviewHigh      :	VAEntrypointEncSlice
      VAProfileH264StereoHigh         :	VAEntrypointVLD
      VAProfileH264StereoHigh         :	VAEntrypointEncSlice
      VAProfileVC1Simple              :	VAEntrypointVLD
      VAProfileVC1Main                :	VAEntrypointVLD
      VAProfileVC1Advanced            :	VAEntrypointVLD
      VAProfileNone                   :	VAEntrypointVideoProc
      VAProfileJPEGBaseline           :	VAEntrypointVLD
      VAProfileJPEGBaseline           :	VAEntrypointEncPicture
      VAProfileVP8Version0_3          :	VAEntrypointVLD
      VAProfileVP8Version0_3          :	VAEntrypointEncSlice
      VAProfileHEVCMain               :	VAEntrypointVLD
      VAProfileHEVCMain               :	VAEntrypointEncSlice

```

`VAEntrypointVLD` means that your card is capable to decode this format, `VAEntrypointEncSlice` means that you can encode to this format.

In this example the `i965` driver is used, as you can see in this line:

```
libva info: Trying to open /usr/lib/dri/**i965**_drv_video.so

```

If the following error is displayed when running `vainfo`:

```
libva info: va_openDriver() returns -1
vaInitialize failed with error code -1 (unknown libva error),exit

```

You need to configure the correct driver, see [#Configuring VA-API](#Configuring_VA-API).

**Note:** The [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") GM108 cards does not support video decoding as it is expected to be offloaded to the integrated [Intel graphics](/index.php/Intel_graphics "Intel graphics") GPU.

### Verifying VDPAU

Install [vdpauinfo](https://www.archlinux.org/packages/?name=vdpauinfo) to verify if the VDPAU driver is loaded correctly and retrieve a full report of the configuration:

 `$ vdpauinfo` 
```
display: :0   screen: 0
API version: 1
Information string: G3DVL VDPAU Driver Shared Library version 1.0

Video surface:

name   width height types

* * *

420    16384 16384  NV12 YV12 
422    16384 16384  UYVY YUYV 
444    16384 16384  Y8U8V8A8 V8U8Y8A8 

Decoder capabilities:

name                        level macbs width height

* * *

MPEG1                          --- not supported ---
MPEG2_SIMPLE                    3  9216  2048  1152
MPEG2_MAIN                      3  9216  2048  1152
H264_BASELINE                  41  9216  2048  1152
H264_MAIN                      41  9216  2048  1152
H264_HIGH                      41  9216  2048  1152
VC1_SIMPLE                      1  9216  2048  1152
VC1_MAIN                        2  9216  2048  1152
VC1_ADVANCED                    4  9216  2048  1152

..

```

## Configuration

Although the video driver should automatically enable hardware video acceleration support for both VA-API and VDPAU, it may be needed to configure VA-API/VDPAU manually. Only continue to this section if you went through [#Verification](#Verification).

The default driver names, used if there is no other configuration present, are guess by the system. However, they are often hacked together and may not work. You can see the guessed values by running:

 `$ grep -iE 'vdpau | dri driver' /var/log/Xorg.0.log` 
```
(II) RADEON(0): [DRI2] DRI driver: radeonsi
(II) RADEON(0): [DRI2] VDPAU driver: radeonsi

```

In this case `radeonsi` is the default for both VA-API and VDPAU.

**Note:** If you use [GDM](/index.php/GDM "GDM"), run `journalctl -b | grep -iE 'vdpau | dri driver'` instead.

This does not represent the *configuration* however. The values above will not change even if you override them.

### Configuring VA-API

You can override the [driver](https://www.freedesktop.org/wiki/Software/vaapi/#driversback-endsthatimplementva-api) for VA-API by using the `LIBVA_DRIVER_NAME` [environment variable](/index.php/Environment_variable "Environment variable"):

*   [Intel graphics](/index.php/Intel_graphics "Intel graphics"):
    *   For [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) use `i965`.
    *   For [intel-media-driver](https://www.archlinux.org/packages/?name=intel-media-driver) use `iHD`.
*   NVIDIA:
    *   For [Nouveau](/index.php/Nouveau "Nouveau") use `nouveau`.
    *   For [NVIDIA](/index.php/NVIDIA "NVIDIA") use `vdpau`.
*   ATI/AMD:
    *   For [AMDGPU](/index.php/AMDGPU "AMDGPU") driver use `radeonsi`.
    *   For [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") use `fglrx`.

**Note:**

*   You can find the installed drivers in `/usr/lib/dri/`. They are used as `/usr/lib/dri/**${LIBVA_DRIVER_NAME}**_drv_video.so`.
*   Some drivers are installed several times under different names for compatibility reasons. You can see which by running `sha1sum /usr/lib/dri/*`.
*   `LIBVA_DRIVERS_PATH` can be used to overrule the VA-API drivers location.
*   Since version 12.0.1 [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver) provides `radeonsi` instead of `gallium`.

### Configuring VDPAU

You can override the driver for VDPAU by using the `VDPAU_DRIVER` [environment variable](/index.php/Environment_variable "Environment variable").

The correct driver name depends on your setup:

*   For Intel Graphics or AMD Catalyst you [need](#Failed_to_open_VDPAU_backend) to set it to `va_gl`.
*   For the open source AMD/ATI driver set it to the proper driver version depending on your GPU, see [#Verification](#Verification).
*   For the open source Nouveau driver set it to `nouveau`.
*   For NVIDIA's proprietary version set it to `nvidia`.

**Note:**

*   You can find the installed drivers in `/usr/lib/vdpau/`. They are used as `/usr/lib/vdpau/libvdpau_**${VDPAU_DRIVER}**.so`.
*   Some drivers are installed several times under different names for compatibility reasons. You can see which by running `sha1sum /usr/lib/vdpau/*`.
*   For hybrid setups (both NVIDIA and AMD), it may be necessary to [set](/index.php/Environment_variable "Environment variable") `DRI_PRIME=1`. For more information see [PRIME](/index.php/PRIME "PRIME").

## Troubleshooting

### Failed to open VDPAU backend

You need to set `VDPAU_DRIVER` variable to point to correct driver. See [#Configuring VDPAU](#Configuring_VDPAU).

### VAAPI init failed

An error along the lines of `libva: /usr/lib/dri/i965_drv_video.so init failed` is encountered. This can happen because of improper detection of Wayland. One solution is to unset `$DISPLAY` so that mpv, MPlayer, VLC, etc. do not assume it is X11\. Another mpv-specific solution is to add the parameter `--gpu-context=wayland`.

## Comparison tables

### VA-API drivers

| Codec | [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) [[2]](https://github.com/01org/intel-vaapi-driver/blob/master/README) | [intel-media-driver](https://www.archlinux.org/packages/?name=intel-media-driver) [[3]](https://github.com/intel/media-driver/blob/master/README.md) | [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver) [[4]](https://www.x.org/wiki/RadeonFeature/) [[5]](https://nouveau.freedesktop.org/wiki/VideoAcceleration/) | [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver)
(VDPAU adapter) |
| Decoding |
| MPEG-2 | GMA 4500 and newer | Broadwell and newer | Radeon HD 6000 and newer
GeForce 8 and newer | See [#VDPAU drivers](#VDPAU_drivers) |
| MPEG-4 | No | No | Radeon HD 6000 and newer |
| VC-1 | Sandy Bridge and newer | Broadwell and newer | Radeon HD 2000 and newer
GeForce 9300 and newer |
| H.264/MPEG-4 AVC | GMA 4500, Ironlake and newer | Radeon HD 2000 and newer
GeForce 8 and newer |
| H.265/HEVC 8bit | Cherryview/Braswell and newer | Skylake and newer | Radeon R9 Fury and newer |
| H.265/HEVC 10bit | Broxton and newer | Broxton/Apollo Lake and newer | Radeon 400 and newer |
| VP8 | Broadwell and newer | Broadwell and newer | No | No |
| VP9 8bit | Broxton and newer
Hybrid: Broadwell to Skylake | Broxton/Apollo Lake and newer | Raven Ridge and newer | No |
| VP9 10bit | Kaby Lake and newer | Kaby Lake and newer | No |
| Encoding |
| MPEG-2 | Ivy Bridge and newer | Broadwell and newer
except Broxton/Apollo Lake | No | No |
| H.264/MPEG-4 AVC | Sandy Bridge and newer | Broadwell and newer | Radeon HD 7000 and newer |
| H.265/HEVC 8bit | Skylake and newer | Skylake and newer | Radeon 400 and newer |
| H.265/HEVC 10bit | Kaby Lake and newer | Kaby Lake and newer | Raven Ridge and newer |
| VP8 | Cherryview/Braswell and newer
Hybrid: Haswell to Skylake | No |
| VP9 8bit | Kaby Lake and newer | Icelake and newer |
| VP9 10bit | No |

*   Up until GeForce GTX 750.
*   Supported by [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/) instead.
*   Hybrid VP8 encoder and VP9 decoder supported by [intel-hybrid-codec-driver](https://aur.archlinux.org/packages/intel-hybrid-codec-driver/). [VP9 decoding on Haswell crashes](https://github.com/intel/intel-hybrid-driver/issues/21).
*   MPEG-4 is disabled by default due to VAAPI limitations. Set the [environment variable](/index.php/Environment_variable "Environment variable") `VAAPI_MPEG4_ENABLED=true` to try to use it anyway.
*   Not implemented in [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver), since it is not maintained by anyone upstream. See [#VDPAU drivers](#VDPAU_drivers).

### VDPAU drivers

| Codec | [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) [[6]](https://www.x.org/wiki/RadeonFeature/) [[7]](https://nouveau.freedesktop.org/wiki/VideoAcceleration/) | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) [wikipedia:Nvidia_PureVideo](https://en.wikipedia.org/wiki/Nvidia_PureVideo "wikipedia:Nvidia PureVideo") | [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl)
(VA-API adapter) |
| Decoding |
| MPEG-2 | Radeon R300 and newer
GeForce 8 and newer | GeForce 8 and newer | No |
| MPEG-4 | Radeon HD 6000 and newer
GeForce 200 and newer | GeForce 200 and newer |
| VC-1 | Radeon HD 2000 and newer
GeForce 9300 and newer | GeForce 8 and newer |
| H.264/MPEG-4 AVC | Radeon HD 2000 and newer
GeForce 8 and newer | GeForce 8 and newer | See [#VA-API drivers](#VA-API_drivers) |
| H.265/HEVC 8bit | Radeon R9 Fury and newer | GeForce 900 and newer | No |
| H.265/HEVC 10bit | Radeon 400 and newer | No |
| VP9 8bit | No | GeForce 900 and newer |
| VP9 10bit | No | No |

*   Up until GeForce GTX 750.
*   [Except](https://en.wikipedia.org/wiki/Nvidia_PureVideo "wikipedia:Nvidia PureVideo") GeForce 8800 Ultra, 8800 GTX, 8800 GTS (320/640 MB).
*   Except GeForce GTX 970 and GTX 980.
*   NVIDIA implementation is limited to 8-bit streams [[8]](https://devtalk.nvidia.com/default/topic/940228/vdpau-expose-hevc-main10-support-where-available-on-die/) [[9]](https://us.download.nvidia.com/XFree86/Linux-x86_64/410.57/README/vdpausupport.html#vdpau-implementation-limits).

### NVIDIA driver only

| Codec | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) [[10]](https://developer.nvidia.com/nvidia-video-codec-sdk) |
| NVDECODE | NVENCODE |
| MPEG-2 | Fermi and newer | No |
| VC-1 |
| H.264/MPEG-4 AVC | Kepler and newer |
| H.265/HEVC 8bit | Maxwell (GM206) and newer | Maxwell (2nd Gen) and newer |
| H.265/HEVC 10bit | Pascal and newer |
| VP8 | Maxwell (2nd Gen) and newer | No |
| VP9 8bit | Maxwell (GM206) and newer |
| VP9 10bit | Pascal and newer |

*   Except GM108 (not supported)
*   Except GM108 and GP108 (not supported)

### Application support

**Tip:** Every new [codec](/index.php/Codec "Codec") tends to utilize more and more CPU time ([x264](https://en.wikipedia.org/wiki/en:x264 "wikipedia:en:x264") < [VP9](https://en.wikipedia.org/wiki/en:VP9 "wikipedia:en:VP9") < [AV1](https://en.wikipedia.org/wiki/en:AV1 "wikipedia:en:AV1")), which results in heating and energy consuming, if no hardware acceleration available. So it may be beneficial to use an older codec (like x264) to reduce CPU load by cost of network bandwidth. E.g. for YouTube one can use *h264ify* extension ([Firefox](https://addons.mozilla.org/firefox/addon/h264ify/), [Chromium](https://chrome.google.com/webstore/detail/h264ify/aleakchihdccplidncghkekgioiakgal)) or the *enhanced-h264ify* extension ([Firefox](https://addons.mozilla.org/firefox/addon/enhanced-h264ify/), [Chromium](https://chrome.google.com/webstore/detail/enhanced-h264ify/omkfmpieigblcllmkgbflkikinpkodlk)).

| Application | Decoding | Encoding | Documentation |
| VA-API | VDPAU | NVDECODE | VA-API | NVENCODE |
| [FFmpeg](/index.php/FFmpeg "FFmpeg") | Yes | Yes | Yes | Yes | Yes | [FFmpeg#Hardware video acceleration](/index.php/FFmpeg#Hardware_video_acceleration "FFmpeg") |
| [GStreamer](/index.php/GStreamer "GStreamer") | Yes | Yes | Yes | Yes | Yes | [GStreamer#Hardware video acceleration](/index.php/GStreamer#Hardware_video_acceleration "GStreamer") |
| [Kodi](/index.php/Kodi "Kodi") | Yes | Yes | Yes | – | – | [Kodi#Hardware video acceleration](/index.php/Kodi#Hardware_video_acceleration "Kodi") |
| [mpv](/index.php/Mpv "Mpv") | Yes | Yes | Yes | – | – | [mpv#Hardware video acceleration](/index.php/Mpv#Hardware_video_acceleration "Mpv") |
| [VLC media player](/index.php/VLC_media_player "VLC media player") | Yes | Yes | No | – | – | [VLC media player#Hardware video acceleration](/index.php/VLC_media_player#Hardware_video_acceleration "VLC media player") |
| [MPlayer](/index.php/MPlayer "MPlayer") | Yes | Yes | No | – | – | [MPlayer#Hardware video acceleration](/index.php/MPlayer#Hardware_video_acceleration "MPlayer") |
| [Flash](/index.php/Flash "Flash") | No | Yes | No | – | – | [Browser plugins#Adobe Flash Player](/index.php/Browser_plugins#Adobe_Flash_Player "Browser plugins") |
| [Chromium](/index.php/Chromium "Chromium") | Yes | No | No | – | – | [Chromium#Hardware video acceleration](/index.php/Chromium#Hardware_video_acceleration "Chromium") |
| [Firefox](/index.php/Firefox "Firefox") | No | No | No | – | – | [Bug report](https://bugzilla.mozilla.org/show_bug.cgi?id=1210726) |

*   GStreamer [uses a whitelist](https://blogs.igalia.com/vjaquez/2018/03/28/gstreamer-va-api-troubleshooting/) of VA-API drivers. To use other drivers like [intel-media-driver](https://www.archlinux.org/packages/?name=intel-media-driver), set [environment variable](/index.php/Environment_variable "Environment variable") `GST_VAAPI_ALL_DRIVERS=1`.
*   NVDECODE/NVENCODE is [disabled in the Arch package](https://git.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/gst-plugins-bad#n45).
*   Not supported officially by developers, alternative packages available.
*   VDPAU is supported only by NPAPI plugin. PPAPI plugin to NPAPI browser experimental adapter is available that provides partial VA-API and VDPAU acceleration.