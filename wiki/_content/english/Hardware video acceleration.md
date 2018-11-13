Related articles

*   [XvMC](/index.php/XvMC "XvMC")

Hardware video acceleration makes it possible for the video card to decode/encode video, thus offloading the CPU and saving power.

There are several ways to achieve this on Linux:

*   [Video Acceleration API](https://www.freedesktop.org/wiki/Software/vaapi/) (VA-API) is a specification and open source library to provide both hardware accelerated video encoding and decoding, developed by Intel.
*   [Video Decode and Presentation API for Unix](https://www.freedesktop.org/wiki/Software/VDPAU/) (VDPAU) is an open source library and API to offload portions of the video decoding process and video post-processing to the GPU video-hardware, developed by NVIDIA.
*   [NVDECODE/NVENCODE](https://developer.nvidia.com/nvidia-video-codec-sdk) - proprietary APIs for hardware video acceleration used by NVIDIA Fermi, Kepler, Maxwell and Pascal generation GPUs.

For pre-2007 video cards see [XvMC](/index.php/XvMC "XvMC").

## Contents

*   [1 Driver support](#Driver_support)
    *   [1.1 VA-API](#VA-API)
    *   [1.2 VDPAU](#VDPAU)
    *   [1.3 NVDEC/NVENC](#NVDEC/NVENC)
*   [2 Software support](#Software_support)
*   [3 Installation](#Installation)
    *   [3.1 Intel](#Intel)
    *   [3.2 NVIDIA](#NVIDIA)
    *   [3.3 ATI/AMD](#ATI/AMD)
    *   [3.4 Translation layers](#Translation_layers)
*   [4 Verification](#Verification)
    *   [4.1 Verifying VA-API](#Verifying_VA-API)
    *   [4.2 Verifying VDPAU](#Verifying_VDPAU)
*   [5 Configuration](#Configuration)
    *   [5.1 Configuring VA-API](#Configuring_VA-API)
    *   [5.2 Configuring VDPAU](#Configuring_VDPAU)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Failed to open VDPAU backend](#Failed_to_open_VDPAU_backend)
    *   [6.2 VAAPI init failed](#VAAPI_init_failed)

## Driver support

### VA-API

| Codec | [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) [[1]](https://github.com/01org/intel-vaapi-driver/blob/master/README) | [intel-media-driver](https://www.archlinux.org/packages/?name=intel-media-driver) [[2]](https://github.com/intel/media-driver/blob/master/README.md) | [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver) [[3]](https://www.x.org/wiki/RadeonFeature/) [[4]](https://nouveau.freedesktop.org/wiki/VideoAcceleration/) | [Catalyst XvBA](/index.php/AMD_Catalyst#Video_acceleration "AMD Catalyst") | [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver)

(VDPAU adapter)

 |
| Decoding |
| MPEG2 | GMA 4500 and newer | Broadwell and newer | Radeon HD 6000 and newer
GeForce 8 and newer | Radeon HD 4000 and newer | See [#VDPAU](#VDPAU) |
| MPEG4 | No | No | Radeon HD 6000 and newer | Radeon HD 6000 and newer |
| AVC (H.264) | GMA 4500, Ironlake and newer | Broadwell and newer | Radeon HD 2000 and newer
GeForce 8 and newer | Radeon HD 4000 and newer |
| HEVC (H.265) 8bit | Cherryview/Braswell and newer | Skylake and newer | Radeon R9 Fury and newer | No |
| HEVC (H.265) 10bit | Broxton and newer | Broxton/Apollo Lake and newer | Radeon 400 and newer |
| VC1 | Sandy Bridge and newer | Broadwell and newer | Radeon HD 2000 and newer
GeForce 9300 and newer | Radeon HD 4000 and newer |
| VP8 | Broadwell and newer | No | No | No |
| VP9 8bit | Broxton and newer
Hybrid: Haswell to Skylake | Broxton/Apollo Lake and newer | Raven Ridge and newer |
| VP9 10bit | Kaby Lake and newer | Kaby Lake and newer |
| Encoding |
| MPEG2 | Ivy Bridge and newer | Broadwell and newer
except Broxton/Apollo Lake | No | No | No |
| AVC (H.264) | Sandy Bridge and newer | Broadwell and newer | Radeon HD 7000 and newer |
| HEVC (H.265) 8bit | Skylake and newer | Skylake and newer | Raven Ridge and newer |
| HEVC (H.265) 10bit | Kaby Lake and newer | Cannonlake and newer |
| VP8 | Cherryview/Braswell and newer
Hybrid: Haswell to Skylake | No |
| VP9 8bit | Kaby Lake and newer | Icelake and newer |
| VP9 10bit | No |

*   Up until GeForce GTX 750.
*   Supported by [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/) instead.
*   Hybrid VP8 encoder and VP9 decoder supported by [intel-hybrid-codec-driver](https://aur.archlinux.org/packages/intel-hybrid-codec-driver/). [[5]](https://github.com/01org/intel-hybrid-driver/blob/master/README)

### VDPAU

**Note:** VDPAU is not updated since September 2015 and is missing VP8 and VP9 support [[6]](https://gitlab.freedesktop.org/vdpau/libvdpau).

| Codec | [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) [[7]](https://www.x.org/wiki/RadeonFeature/) [[8]](https://nouveau.freedesktop.org/wiki/VideoAcceleration/) | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) [[9]](https://www.nvidia.com/page/purevideo_support.html) | [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl)
(VA-API adapter) |
| Decoding |
| MPEG2 | Radeon R300 and newer
GeForce 8 and newer | GeForce 8 and newer | No |
| MPEG4 | Radeon HD 6000 and newer
GeForce 200 and newer | GeForce 200 and newer |
| AVC (H.264) | Radeon HD 2000 and newer
GeForce 8 and newer | GeForce 8 and newer | See [#VA-API](#VA-API) |
| HEVC (H.265) 8bit | Radeon R9 Fury and newer | GeForce 900 and newer | No |
| HEVC (H.265) 10bit | Radeon 400 and newer | No |
| VC1 | Radeon HD 2000 and newer
GeForce 9300 and newer | GeForce 8 and newer |

*   Up until GeForce GTX 750.
*   Except GeForce GTX 970 and GTX 980.
*   NVIDIA implementation is limited to 8-bit streams [[10]](https://devtalk.nvidia.com/default/topic/940228/vdpau-expose-hevc-main10-support-where-available-on-die/) [[11]](https://us.download.nvidia.com/XFree86/Linux-x86_64/410.57/README/vdpausupport.html#vdpau-implementation-limits).
*   [Except](https://en.wikipedia.org/wiki/Nvidia_PureVideo "wikipedia:Nvidia PureVideo") GeForce 8800 Ultra, 8800 GTX, 8800 GTS (320/640 MB).

### NVDEC/NVENC

| Codec | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) |
| [Decoding (NVDEC)](https://developer.nvidia.com/nvidia-video-codec-sdk#NVDECFeatures) | [Encoding (NVENC)](https://developer.nvidia.com/nvidia-video-codec-sdk#NVENCFeatures) |
| MPEG-2 | Kepler and newer | No |
| VC-1 |
| AVC (H.264) | Kepler and newer |
| HEVC (H.265) 8bit | Maxwell (GM206) and newer | Maxwell (2nd Gen) and newer |
| HEVC (H.265) 10bit | Pascal and newer |
| VP8 | Maxwell (2nd Gen) and newer | No |
| VP9 8bit | Maxwell (GM206) and newer |
| VP9 10bit | Pascal and newer |

*   Except GM108 (not supported)
*   Except GM108 and GP108 (not supported)

## Software support

 VA-API | VDPAU | NVDEC/NVENC | Documentation |
| [FFmpeg](/index.php/FFmpeg "FFmpeg") | Yes | Yes | Yes | [FFmpeg#Hardware video acceleration](/index.php/FFmpeg#Hardware_video_acceleration "FFmpeg") |
| [GStreamer](/index.php/GStreamer "GStreamer") | Yes, via [gstreamer-vaapi](https://www.archlinux.org/packages/?name=gstreamer-vaapi) | Yes, via [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad) | Yes, via [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad) | [GStreamer#Hardware video acceleration](/index.php/GStreamer#Hardware_video_acceleration "GStreamer") |
| [Kodi](/index.php/Kodi "Kodi") | Yes | Yes | Yes | [Kodi#Hardware video acceleration](/index.php/Kodi#Hardware_video_acceleration "Kodi") |
| [mpv](/index.php/Mpv "Mpv") | Yes | Yes | Yes | [mpv#Hardware decoding](/index.php/Mpv#Hardware_decoding "Mpv") |
| [VLC media player](/index.php/VLC_media_player "VLC media player") | Yes | Yes | No | [VLC media player#Hardware video acceleration](/index.php/VLC_media_player#Hardware_video_acceleration "VLC media player") |
| [MPlayer](/index.php/MPlayer "MPlayer") | [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/) | Yes | No | [MPlayer#Hardware video acceleration](/index.php/MPlayer#Hardware_video_acceleration "MPlayer") |
| [Flash](/index.php/Flash "Flash") | NPAPI only:
[freshplayerplugin](https://aur.archlinux.org/packages/freshplayerplugin/) | NPAPI only:
[flashplugin](https://www.archlinux.org/packages/?name=flashplugin) or
[freshplayerplugin](https://aur.archlinux.org/packages/freshplayerplugin/) | No | [Browser plugins#Adobe Flash Player](/index.php/Browser_plugins#Adobe_Flash_Player "Browser plugins") |
| [Chromium](/index.php/Chromium "Chromium") | [chromium-vaapi](https://aur.archlinux.org/packages/chromium-vaapi/) | No | No | [Chromium#Hardware video acceleration](/index.php/Chromium#Hardware_video_acceleration "Chromium") |
| [Firefox](/index.php/Firefox "Firefox") | No | No | No | [Bug report](https://bugzilla.mozilla.org/show_bug.cgi?id=1210726) |

**Tip:** To reduce CPU usage while watching YouTube where VP8/VP9 hardware decoding is not available use h264ify extension for [Firefox](https://addons.mozilla.org/en-US/firefox/addon/h264ify/) and [Chromium](https://chrome.google.com/webstore/detail/h264ify/aleakchihdccplidncghkekgioiakgal).

## Installation

### Intel

[Intel graphics](/index.php/Intel_graphics "Intel graphics") open-source drivers support VA-API:

*   HD Graphics series starting from CannonLake (or optionally from Broadwell) and newer are supported by [intel-media-driver](https://www.archlinux.org/packages/?name=intel-media-driver).
*   GMA 4500 series and newer GPUs up to Coffee Lake are supported by [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver).
*   GMA 4500 H.264 decoding is supported by [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/), see [Intel#Hardware accelerated H.264 decoding on GMA 4500](/index.php/Intel#Hardware_accelerated_H.264_decoding_on_GMA_4500 "Intel").
*   Haswell to Skylake hybrid VP8 encoding and VP9 decoding is supported by [intel-hybrid-codec-driver](https://aur.archlinux.org/packages/intel-hybrid-codec-driver/).

### NVIDIA

[Nouveau](/index.php/Nouveau "Nouveau") open-source driver supports both VA-API and VDPAU:

*   GeForce 8 series and newer GPUs up until GeForce GTX 750 are supported by [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver) and [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau).
*   [Requires](https://nouveau.freedesktop.org/wiki/VideoAcceleration/#firmware) [nouveau-fw](https://aur.archlinux.org/packages/nouveau-fw/) firmware package, presently extracted from the NVIDIA binary driver.

[NVIDIA](/index.php/NVIDIA "NVIDIA") proprietary driver supports VDPAU and NVDECODE/NVENCODE:

*   VDPAU is supported on GeForce 8 series and newer via [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils).
*   NVDECODE/NVENCODE are supported on Kepler and newer via [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils).

### ATI/AMD

[ATI](/index.php/ATI "ATI") and [AMDGPU](/index.php/AMDGPU "AMDGPU") open-source drivers support both VA-API and VDPAU:

*   VDPAU on Radeon R300 and newer GPUs is supported by [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau).
*   VA-API on Radeon HD 2000 and newer GPUs is supported by [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver).

[AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") proprietary driver supports VA-API via [XvBA](/index.php/AMD_Catalyst#Video_acceleration "AMD Catalyst").

[AMDGPU PRO](/index.php/AMDGPU_PRO "AMDGPU PRO") proprietary driver is built on top of AMDGPU driver and supports both VA-API and VDPAU.

### Translation layers

To get VA-API support when device driver provides none:

*   [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) – VDPAU backend for VA-API.
*   [libva-vdpau-driver-chromium](https://aur.archlinux.org/packages/libva-vdpau-driver-chromium/) – VDPAU backend for VA-API, patched to work with Chromium.

To get VDPAU support when device driver provides none:

*   [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) – VA-API backend for VDPAU, [only H.264 support](https://github.com/i-rinat/libvdpau-va-gl/issues/67#issuecomment-318470175).

## Verification

Your system may work perfectly out-of-the-box without needing any configuration. Therefore it is a good idea to start with this section to see that it is the case.

**Tip:** [mpv](/index.php/Mpv#Hardware_decoding "Mpv") is great for testing hardware acceleration in practice.

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

### Verifying VDPAU

Install [vdpauinfo](https://www.archlinux.org/packages/?name=vdpauinfo) to verify if the VDPAU driver is loaded correctly and retrieve a full report of the configuration:

 `$ vdpauinfo` 
```
display: :0   screen: 0
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

 `$ grep -iE 'vdpau | dri driver' ~/.local/share/xorg/Xorg.0.log` 
```
(II) RADEON(0): [DRI2] DRI driver: radeonsi
(II) RADEON(0): [DRI2] VDPAU driver: radeonsi

```

In this case `radeonsi` is the default for both VA-API and VDPAU.

**Note:** If you use [GDM](/index.php/GDM "GDM"), run `journalctl -b | grep -iE 'vdpau | dri driver'` instead.

This does not represent the *configuration* however. The values above will not change even if you override them.

### Configuring VA-API

You can override the [driver](http://www.freedesktop.org/wiki/Software/vaapi/#driversback-endsthatimplementva-api) for VA-API by using the `LIBVA_DRIVER_NAME` [environment variable](/index.php/Environment_variable "Environment variable"):

*   For Intel Graphics use `i965` or `iHD`.
*   For the open source Nouveau driver use `nouveau`.
*   For the proprietary NVIDIA driver use `vdpau`.
*   For the open source AMD driver use `radeonsi`.
*   For the proprietary AMD Catalyst use `fglrx`.

**Note:**

*   You can find the installed drivers in `/usr/lib/dri/`. They are used as `/usr/lib/dri/**${LIBVA_DRIVER_NAME}**_drv_video.so`.
*   Some drivers are installed several times under different names for compatibility reasons. You can see which by running `sha1sum /usr/lib/dri/*`.
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

This happens when you use [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) without overriding `VDPAU_DRIVER`. VDPAU does not know what driver to use in this case for some reason and guesses wrongly. See [#Configuring VDPAU](#Configuring_VDPAU).

However you may want to configure your media player to use VA-API instead, getting far better results. See [#Software support](#Software_support).

### VAAPI init failed

An error along the lines of `libva: /usr/lib/dri/i965_drv_video.so init failed` is encountered. This can happen because of improper detection of Wayland. One solution is to unset `$DISPLAY` so that mpv, mplayer, VLC, etc. do not assume it is X11\. Another mpv-specific solution is to add the parameter `--opengl-backend=wayland`.