Related articles

*   [XvMC](/index.php/XvMC "XvMC")

Hardware video acceleration makes it possible for the video card to decode/encode video, thus offloading the CPU and saving power.

There are several ways to achieve this on Linux:

*   **[Video Acceleration API](http://www.freedesktop.org/wiki/Software/vaapi)** (VA-API) is a specification and open source library to provide both hardware accelerated video encoding and decoding, developed by Intel.
*   **[Video Decode and Presentation API for Unix](http://http.download.nvidia.com/XFree86/vdpau/doxygen/html/)** (VDPAU) is an open source library and API to offload portions of the video decoding process and video post-processing to the GPU video-hardware, developed by NVIDIA.
*   X-Video Motion Compensation ([XvMC](/index.php/XvMC "XvMC")) is an extension for the X.Org Server, allowing video programs to offload portions of the video decoding process to the GPU video-hardware.

## Contents

*   [1 Support](#Support)
    *   [1.1 Formats](#Formats)
    *   [1.2 Software](#Software)
*   [2 Installation](#Installation)
    *   [2.1 Installing VA-API](#Installing_VA-API)
    *   [2.2 Installing VDPAU](#Installing_VDPAU)
*   [3 Verification](#Verification)
    *   [3.1 Verifying VA-API](#Verifying_VA-API)
    *   [3.2 Verifying VDPAU](#Verifying_VDPAU)
*   [4 Configuration](#Configuration)
    *   [4.1 Configuring VA-API](#Configuring_VA-API)
    *   [4.2 Configuring VDPAU](#Configuring_VDPAU)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Failed to open VDPAU backend](#Failed_to_open_VDPAU_backend)
    *   [5.2 VAAPI init failed](#VAAPI_init_failed)

## Support

### Formats

**Note:**

*   To choose the correct driver see [#Installation](#Installation).
*   The features supported by your GPU may vary. To see what your GPU supports see [#Verification](#Verification).

<caption>VA-API</caption>
 [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) [[1]](https://github.com/01org/intel-vaapi-driver/blob/master/README) | [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver) | [Catalyst XvBA](/index.php/AMD_Catalyst#Video_acceleration "AMD Catalyst") | [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver)

(VDPAU adapter)

 |
| Decoding |
| MPEG2 | GMA 4500 and newer | Radeon HD 4000 and newer? | Radeon HD 4000 and newer | See VDPAU. |
| MPEG4 | ✗ |  ? | Radeon HD 6000 and newer |
| H.264 | GMA 4500, Ironlake Graphics and newer | Radeon HD 4000 and newer? | Radeon HD 4000 and newer |
| HEVC (H.265) | Cherryview/Braswell and newer | Radeon HD 6000 and newer? | ✗ |
| VC1 | Sandy Bridge Graphics and newer | Radeon HD 4000 and newer? | Radeon HD 4000 and newer |
| VP8 | Broadwell and newer |  ? | ✗ | ✗ |
| VP9 | Broxton and newer |  ? | ✗ |
| Encoding |
| MPEG2 | Ivy Bridge Graphics and newer |  ? | ✗ | ✗ |
| H.264 | Sandy Bridge Graphics and newer | Radeon HD 4000 and newer? |
| HEVC (H.265) | Skylake and newer |  ? |
| VP8 | Cherryview/Braswell and newer |  ? |
| VP9 | Kaby Lake and newer |  ? |

<caption>VDPAU</caption>
 [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) | [amdgpu-pro-vdpau](https://aur.archlinux.org/packages/amdgpu-pro-vdpau/)
([AMDGPU PRO](/index.php/AMDGPU_PRO "AMDGPU PRO") only) | [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl)
(VA-API adapter) |
| Decoding |
| MPEG2 | Radeon 9500 and newer, GeForce 8 and newer | GeForce 8 and newer |  ? | ✗ |
| MPEG4 | Radeon HD 6000 and newer, GeForce 200 and newer | GeForce 200 and newer |
| H.264 | Radeon HD 4000 and newer, GeForce 8 and newer | GeForce 8 and newer | See VA-API. |
| HEVC (H.265) | [yes](https://cgit.freedesktop.org/mesa/mesa/commit/src/gallium/state_trackers/vdpau/decode.c?id=5609a6986f3eb3c452d66d373b6081df5c6fb34c) | GeForce 900 and newer | ✗ |
| VC1 | Radeon HD 4000 and newer, GeForce 8 and newer | GeForce 8 and newer |

*   Supported by [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/) instead.
*   As of version 0.3, the VA GL driver does not support any other hardware decoder than H.264.
*   [Except](https://en.wikipedia.org/wiki/Nvidia_PureVideo "wikipedia:Nvidia PureVideo") GeForce 8800 Ultra, 8800 GTX, 8800 GTS (320/640 MB).
*   Except GeForce GTX 970 and GTX 980.

<caption>Nvidia NVDEC/NVENC ([NVIDIA](/index.php/NVIDIA "NVIDIA") only)</caption>
 Decoding (NVDEC) | Encoding (NVENC) |
| MPEG-2 | ✓ | ✗ |
| VC-1 | ✓ | ✗ |
| H.264 | ✓ | ✓ |
| HEVC (H.265) | Pascal and newer | Pascal and newer |
| VP8 | Maxwell2 and newer | ✗ |
| VP9 | Pascal and newer | ✗ |

### Software

 VA-API | VDPAU | NVDEC/NVENC |
| [GStreamer](/index.php/GStreamer "GStreamer") | ✓ (with [gstreamer-vaapi](https://www.archlinux.org/packages/?name=gstreamer-vaapi), see [GStreamer#Hardware acceleration](/index.php/GStreamer#Hardware_acceleration "GStreamer")) | ✓ (with [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad), see [GStreamer#Hardware acceleration](/index.php/GStreamer#Hardware_acceleration "GStreamer")) | ✓ (with [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad), see [GStreamer#Hardware acceleration](/index.php/GStreamer#Hardware_acceleration "GStreamer")) |
| [VLC media player](/index.php/VLC_media_player "VLC media player") | ✓ (see [VLC media player#Hardware acceleration support](/index.php/VLC_media_player#Hardware_acceleration_support "VLC media player")) | ✓ (see [VLC media player#Hardware acceleration support](/index.php/VLC_media_player#Hardware_acceleration_support "VLC media player")) | ✗ |
| [mpv](/index.php/Mpv "Mpv") | ✓ (see [mpv#Hardware decoding](/index.php/Mpv#Hardware_decoding "Mpv")) | ✓ (see [mpv#Hardware decoding](/index.php/Mpv#Hardware_decoding "Mpv")) | ✓ |
| [MPlayer](/index.php/MPlayer "MPlayer") | ✓ (with [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/), see [MPlayer#Enabling VA-API](/index.php/MPlayer#Enabling_VA-API "MPlayer")) | ✓ (see [MPlayer#Enabling VDPAU](/index.php/MPlayer#Enabling_VDPAU "MPlayer")) | ✗ |
| [Flash](/index.php/Flash "Flash") | ✓ (with [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl), see [Flash#Configuration](/index.php/Flash#Configuration "Flash")) | ✓ (see [Flash#Configuration](/index.php/Flash#Configuration "Flash")) | ✗ |
| [Kodi](/index.php/Kodi "Kodi") | ✓ | ✓ | ✓ |
| [Firefox](/index.php/Firefox "Firefox") | ✗ [[2]](https://bugzilla.mozilla.org/show_bug.cgi?id=1210726) [[3]](https://bugzilla.mozilla.org/show_bug.cgi?id=1210727) [[4]](https://bugzilla.mozilla.org/show_bug.cgi?id=563206) | ✗ |
| [Chromium](/index.php/Chromium "Chromium") | [WIP](https://chromium-review.googlesource.com/c/chromium/src/+/532294) ([chromium-vaapi](https://aur.archlinux.org/packages/chromium-vaapi/)) | ✗ | ✗ |
| [FFmpeg](/index.php/FFmpeg "FFmpeg") | ✓ | ✓ | ✓ |

## Installation

The choice varies depending on your video card vendor:

*   For Intel Graphics use VA-API.
*   For NVIDIA cards use VDPAU.
*   For AMD cards you can use both (with [mesa](https://www.archlinux.org/packages/?name=mesa)). The difference is really only in the application implementation [[5]](https://www.phoronix.com/forums/forum/linux-graphics-x-org-drivers/open-source-amd-linux/887994-vaapi-or-vdpau).

There are also two specific types of drivers for VA-API and VDPAU:

*   [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver), which uses VDPAU as a backend for VA-API.
*   [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl), which uses VA-API as a backend for VDPAU.

For pre-2007 cards see [XvMC](/index.php/XvMC "XvMC").

**Tip:** It is recommended to install and configure both VA-API and VDPAU to achieve support in different scenarios, e.g. [Flash](/index.php/Flash "Flash") does not support VA-API but can use the VDPAU VA-API backend.

### Installing VA-API

**Open source drivers:**

*   [ATI](/index.php/ATI "ATI")/[AMDGPU](/index.php/AMDGPU "AMDGPU") Radeon 9500 and newer GPUs are supported by either [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver) with [mesa](https://www.archlinux.org/packages/?name=mesa) or [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) (see [#Installing VDPAU](#Installing_VDPAU)).
*   [Intel](/index.php/Intel "Intel") GMA 4500 series and newer GPUs are supported by [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) with [mesa](https://www.archlinux.org/packages/?name=mesa).
    *   To get better support on GMA 4500 consider using [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/) instead, see [Intel#Hardware accelerated H.264 decoding on GMA 4500](/index.php/Intel#Hardware_accelerated_H.264_decoding_on_GMA_4500 "Intel") for instructions and caveats.
    *   A new usermode driver being developed by Intel is available for Broadwell, Skylake, Kabylake, Apollolake and Canonlake: [intel-media-driver](https://aur.archlinux.org/packages/intel-media-driver/)
*   [NVIDIA](/index.php/Nouveau "Nouveau") GeForce 8 series and newer GPUs are supported by [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) (see [#Installing VDPAU](#Installing_VDPAU)).

**Proprietary drivers:**

*   AMD cards depend on the driver:
    *   [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") uses [xvba](/index.php/AMD_Catalyst#Video_acceleration "AMD Catalyst").
    *   [AMDGPU PRO](/index.php/AMDGPU_PRO "AMDGPU PRO") uses [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) + [amdgpu-pro-vdpau](https://aur.archlinux.org/packages/amdgpu-pro-vdpau/) (see [AMDGPU#AMDGPU PRO](/index.php/AMDGPU#AMDGPU_PRO "AMDGPU")).
*   [NVIDIA](/index.php/NVIDIA "NVIDIA") GeForce 8 series and newer GPUs are supported by [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) (see [#Installing VDPAU](#Installing_VDPAU)).

### Installing VDPAU

**Open source drivers:**

*   [ATI](/index.php/ATI "ATI")/[AMDGPU](/index.php/AMDGPU "AMDGPU") Radeon 9500 and newer GPUs are supported by [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau).
*   [Intel](/index.php/Intel "Intel") GMA 4500 series and newer GPUs are supported by [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) (see [#Installing VA-API](#Installing_VA-API)).
*   [NVIDIA](/index.php/Nouveau "Nouveau") GeForce 8 series and newer GPUs are supported by [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau). It [requires](http://nouveau.freedesktop.org/wiki/VideoAcceleration/#firmware) [nouveau-fw](https://aur.archlinux.org/packages/nouveau-fw/), which contains the required firmware to operate that is presently extracted from the NVIDIA binary driver.

**Proprietary drivers:**

*   AMD cards depend on the driver:
    *   [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") uses [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) (see [#Installing VA-API](#Installing_VA-API)).
    *   [AMDGPU PRO](/index.php/AMDGPU_PRO "AMDGPU PRO") uses [amdgpu-pro-vdpau](https://aur.archlinux.org/packages/amdgpu-pro-vdpau/) (see [AMDGPU#AMDGPU PRO](/index.php/AMDGPU#AMDGPU_PRO "AMDGPU")).
*   [NVIDIA](/index.php/NVIDIA "NVIDIA") GeForce 600 series and newer GPUs are supported by [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils).
    *   GeForce 400/500 series are supported by [nvidia-390xx-utils](https://www.archlinux.org/packages/?name=nvidia-390xx-utils).
    *   GeForce 8/9 and GeForce 100-300 series are supported by [nvidia-340xx-utils](https://www.archlinux.org/packages/?name=nvidia-340xx-utils).

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

*   For Intel Graphics use `i965`.
*   For NVIDIA use `vdpau`.
*   For AMD use either `radeonsi` or `vdpau`.

**Note:**

*   You can find the installed drivers in `/usr/lib/dri/`. They are used as `/usr/lib/dri/**${LIBVA_DRIVER_NAME}**_drv_video.so`.
*   Some drivers are installed several times under different names for compatibility reasons. You can see which by running `sha1sum /usr/lib/dri/*`.
*   Since version 12.0.1 [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver) provides `radeonsi` instead of `gallium`.

### Configuring VDPAU

You can override the driver for VDPAU by using the `VDPAU_DRIVER` [environment variable](/index.php/Environment_variable "Environment variable").

The correct driver name depends on your setup:

*   For Intel Graphics or AMD Catalyst you [need](#Failed_to_open_VDPAU_backend) to set it to `va_gl`.
*   For the open source AMD/ATI driver set it to the proper driver version depending on your GPU, see [#Verification](#Verification).
*   For NVIDIA's proprietary version set it to `nvidia`.

**Note:**

*   You can find the installed drivers in `/usr/lib/vdpau/`. They are used as `/usr/lib/vdpau/libvdpau_**${VDPAU_DRIVER}**.so`.
*   Some drivers are installed several times under different names for compatibility reasons. You can see which by running `sha1sum /usr/lib/vdpau/*`.
*   For hybrid setups (both NVIDIA and AMD), it may be necessary to [set](/index.php/Environment_variable "Environment variable") `DRI_PRIME=1`. For more information see [PRIME](/index.php/PRIME "PRIME").

## Troubleshooting

### Failed to open VDPAU backend

This happens when you use [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) without overriding `VDPAU_DRIVER`. VDPAU does not know what driver to use in this case for some reason and guesses wrongly. See [#Configuring VDPAU](#Configuring_VDPAU).

However you may want to configure your media player to use VA-API instead, getting far better results. See [#Software](#Software).

### VAAPI init failed

An error along the lines of `libva: /usr/lib/dri/i965_drv_video.so init failed` is encountered. This can happen because of improper detection of Wayland. One solution is to unset `$DISPLAY` so that mpv, mplayer, VLC, etc. do not assume it is X11\. Another mpv-specific solution is to add the parameter `--opengl-backend=wayland`.