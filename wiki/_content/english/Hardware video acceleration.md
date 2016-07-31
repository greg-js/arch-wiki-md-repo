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
    *   [5.2 VA-API vaInitialize failed](#VA-API_vaInitialize_failed)

## Support

### Formats

**Note:** To choose the correct driver see [#Installation](#Installation).

<caption>VA-API</caption>
 [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) | [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver) | [libva-xvba-driver](https://aur.archlinux.org/packages/libva-xvba-driver/) | [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) |
| MPEG2 decoding | GMA 4500 and newer | 

<center>?</center>

 | Radeon HD 4000 and newer | 

<center>See VDPAU.</center>

 |
| MPEG4 decoding | 

<center>✗</center>

 | 

<center>?</center>

 | Radeon HD 6000 and newer |
| H.264 decoding | GMA 4500, Ironlake Graphics and newer | 

<center>?</center>

 | Radeon HD 4000 and newer |
| VC1 decoding | Sandy Bridge Graphics and newer | 

<center>?</center>

 | Radeon HD 4000 and newer |
| MPEG2 encoding | Ivy Bridge Graphics and newer | 

<center>?</center>

 | 

<center>✗</center>

 | 

<center>✗</center>

 |
| H.264 encoding | Sandy Bridge Graphics and newer | 

<center>?</center>

 | 

<center>✗</center>

 | 

<center>✗</center>

 |

<caption>VDPAU</caption>
 [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) | [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) | [libvdpau-amdgpu-pro](https://aur.archlinux.org/packages/libvdpau-amdgpu-pro/) | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) |
| MPEG2 decoding | Radeon 9500 and newer, GeForce 8 and newer | 

<center>✗</center>

 | 

<center>?</center>

 | GeForce 8 and newer |
| MPEG4 decoding | Radeon HD 6000 and newer, GeForce 200 and newer | 

<center>✗</center>

 | 

<center>?</center>

 | GeForce 200 and newer |
| H.264 decoding | Radeon HD 4000 and newer, GeForce 8 and newer | 

<center>See VA-API.</center>

 | 

<center>?</center>

 | GeForce 8 and newer |
| VC1 decoding | Radeon HD 4000 and newer, GeForce 8 and newer | 

<center>✗</center>

 | 

<center>?</center>

 | GeForce 8 and newer |
| HEVC (H.265) decoding | 

<center>✗</center>

 | 

<center>✗</center>

 | 

<center>?</center>

 | GeForce 900 and newer |

*   Supported by [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/) instead.
*   As of version 0.3, the VA GL driver doesn't support any other hardware decoder than H.264.
*   [Except](https://en.wikipedia.org/wiki/Nvidia_PureVideo "wikipedia:Nvidia PureVideo") GeForce 8800 Ultra, 8800 GTX, 8800 GTS (320/640 MB).
*   Except GeForce GTX 970 and GTX 980.

The features supported by your GPU may vary. To see what your GPU supports see [#Verification](#Verification).

Regarding the [libvdpau-amdgpu-pro](https://aur.archlinux.org/packages/libvdpau-amdgpu-pro/) package, see also: [AMD Radeon™ Software AMD GPU-PRO Beta Driver – Linux® for Vulkan™ Release Notes](https://support.amd.com/en-us/kb-articles/Pages/AMDGPU-PRO-Beta-Driver-for-Vulkan-Release-Notes.aspx). Loosely, this VDPAU driver is for the Radeon R9 family.

### Software

 VA-API | VDPAU |
| [GStreamer](/index.php/GStreamer "GStreamer") | ✓ (with [gstreamer-vaapi](https://www.archlinux.org/packages/?name=gstreamer-vaapi), see [GStreamer#Hardware acceleration](/index.php/GStreamer#Hardware_acceleration "GStreamer")) | ✓ (with [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad), see [GStreamer#Hardware acceleration](/index.php/GStreamer#Hardware_acceleration "GStreamer")) |
| [VLC media player](/index.php/VLC_media_player "VLC media player") | ✓ (see [VLC media player#Hardware acceleration support](/index.php/VLC_media_player#Hardware_acceleration_support "VLC media player")) | ✓ (see [VLC media player#Hardware acceleration support](/index.php/VLC_media_player#Hardware_acceleration_support "VLC media player")) |
| [mpv](/index.php/Mpv "Mpv") | ✓ (see [mpv#Hardware Decoding](/index.php/Mpv#Hardware_Decoding "Mpv")) | ✓ (see [mpv#Hardware Decoding](/index.php/Mpv#Hardware_Decoding "Mpv")) |
| [MPlayer](/index.php/MPlayer "MPlayer") | ✓ (with [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/), see [MPlayer#Enabling VA-API](/index.php/MPlayer#Enabling_VA-API "MPlayer")) | ✓ (see [MPlayer#Enabling VDPAU](/index.php/MPlayer#Enabling_VDPAU "MPlayer")) |
| [Flash](/index.php/Flash "Flash") | ✓ (with [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl), see [Flash#Configuration](/index.php/Flash#Configuration "Flash")) | ✓ (see [Flash#Configuration](/index.php/Flash#Configuration "Flash")) |
| [Kodi](/index.php/Kodi "Kodi") | ✓ | ✓ |
| [Firefox](/index.php/Firefox "Firefox") | ✗ [[1]](https://bugzilla.mozilla.org/show_bug.cgi?id=1210726) [[2]](https://bugzilla.mozilla.org/show_bug.cgi?id=1210727) [[3]](https://bugzilla.mozilla.org/show_bug.cgi?id=563206) |

## Installation

The choice varies depending on your video card vendor:

*   For Intel Graphics use VA-API.
*   For NVIDIA cards use VDPAU.
*   For AMD cards you can use both (with [mesa](https://www.archlinux.org/packages/?name=mesa)).

There are also two specific types of drivers for VA-API and VDPAU:

*   [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver), which uses VDPAU as a backend for VA-API.
*   [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl), which uses VA-API as a backend for VDPAU.

For pre-2007 cards see [XvMC](/index.php/XvMC "XvMC").

**Tip:** It is recommended to install and configure both VA-API and VDPAU to achieve support in different scenarios, e.g. [Flash](/index.php/Flash "Flash") doesn't support VA-API but can use the VDPAU VA-API backend.

**Warning:** Do not use [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) and [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) together as it will create an (infinite) loop between VA-API and VDPAU, which will result in something either really bad or really fun. But if you try it anyway please share your experiences.

### Installing VA-API

**Open source drivers:**

*   [AMD](/index.php/ATI "ATI") Radeon 9500 and newer GPUs are supported by either [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver) with [mesa](https://www.archlinux.org/packages/?name=mesa) or [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) (see [#Installing VDPAU](#Installing_VDPAU)).
*   [Intel](/index.php/Intel "Intel") GMA 4500 series and newer GPUs are supported by [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) with [mesa](https://www.archlinux.org/packages/?name=mesa).
    *   To get better support on GMA 4500 consider using [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/) instead, see [Intel#H.264 decoding on GMA 4500](/index.php/Intel#H.264_decoding_on_GMA_4500 "Intel") for instructions and caveats.
*   [NVIDIA](/index.php/Nouveau "Nouveau") GeForce 8 series and newer GPUs are supported by [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) (see [#Installing VDPAU](#Installing_VDPAU)).

**Proprietary drivers:**

*   [AMD](/index.php/AMD_Catalyst "AMD Catalyst") Radeon HD 4000 series and newer GPUs are supported by [libva-xvba-driver](https://aur.archlinux.org/packages/libva-xvba-driver/). It uses the [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) driver for Radeon HD 5000 series and newer, and [catalyst-total-hd234k](https://aur.archlinux.org/packages/catalyst-total-hd234k/) for Radeon HD 4000 series.
*   [NVIDIA](/index.php/NVIDIA "NVIDIA") GeForce 8 series and newer GPUs are supported by [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) (see [#Installing VDPAU](#Installing_VDPAU)).

### Installing VDPAU

**Open source drivers:**

*   [AMD](/index.php/ATI "ATI") Radeon 9500 and newer GPUs are supported by [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau).
*   [Intel](/index.php/Intel "Intel") GMA 4500 series and newer GPUs are supported by [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) (see [#Installing VA-API](#Installing_VA-API)).
*   [NVIDIA](/index.php/Nouveau "Nouveau") GeForce 8 series and newer GPUs are supported by [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau). It [requires](http://nouveau.freedesktop.org/wiki/VideoAcceleration/#firmware) [nouveau-fw](https://aur.archlinux.org/packages/nouveau-fw/), which contains the required firmware to operate that is presently extracted from the NVIDIA binary driver.

**Proprietary drivers:**

*   [AMD](/index.php/AMD_Catalyst "AMD Catalyst") Radeon HD 4000 series and newer GPUs are supported by [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) (see [#Installing VA-API](#Installing_VA-API)).
*   [NVIDIA](/index.php/NVIDIA "NVIDIA") GeForce 400 series and newer GPUs are supported by [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils).
    *   GeForce 8/9 and GeForce 100-300 series are supported by [nvidia-340xx-utils](https://www.archlinux.org/packages/?name=nvidia-340xx-utils).

## Verification

**Tip:** [mpv](/index.php/Mpv#Hardware_Decoding "Mpv") is great for testing hardware acceleration in practice.

### Verifying VA-API

Verify the settings for VA-API by running `vainfo`, which is provided by [libva](https://www.archlinux.org/packages/?name=libva):

 `$ vainfo` 
```
libva info: VA-API version 0.39.0
libva info: va_getDriverName() returns 0
libva info: Trying to open /usr/lib/dri/i965_drv_video.so
libva info: Found init function __vaDriverInit_0_39
libva info: va_openDriver() returns 0
vainfo: VA-API version: 0.39 (libva 1.7.0)
vainfo: Driver version: Intel i965 driver for Intel(R) Sandybridge Mobile - 1.7.0
vainfo: Supported profile and entrypoints
      VAProfileMPEG2Simple            : VAEntrypointVLD
      VAProfileMPEG2Main              : VAEntrypointVLD
      VAProfileH264ConstrainedBaseline: VAEntrypointVLD
      VAProfileH264ConstrainedBaseline: VAEntrypointEncSlice
      VAProfileH264Main               : VAEntrypointVLD
      VAProfileH264Main               : VAEntrypointEncSlice
      VAProfileH264High               : VAEntrypointVLD
      VAProfileH264High               : VAEntrypointEncSlice
      VAProfileH264StereoHigh         : VAEntrypointVLD
      VAProfileVC1Simple              : VAEntrypointVLD
      VAProfileVC1Main                : VAEntrypointVLD
      VAProfileVC1Advanced            : VAEntrypointVLD
      VAProfileNone                   : VAEntrypointVideoProc

```

*VAEntrypointVLD* means that your card is capable to decode this format, *VAEntrypointEncSlice* means that you can encode to this format.

In this example the `i965` driver is used, as you can see in this line:

 `libva info: Trying to open /usr/lib/dri/**i965**_drv_video.so` 

### Verifying VDPAU

You can verify that the VDPAU driver is loaded correctly using [vdpauinfo](https://www.archlinux.org/packages/?name=vdpauinfo):

 `$ vdpauinfo | grep "Information string:"` 
```
Information string: NVIDIA VDPAU Driver Shared Library  364.19  Tue Apr 19 14:14:26 PDT 2016

```

## Configuration

### Configuring VA-API

The [driver](http://www.freedesktop.org/wiki/Software/vaapi/#driversback-endsthatimplementva-api) for VA-API is autodetected. To determine which one is used see [#Verifying](#Verifying). You can override it by setting the `LIBVA_DRIVER_NAME` [environment variable](/index.php/Environment_variable "Environment variable"):

*   For Intel Graphics use `i965`.
*   For NVIDIA use `vdpau`.
*   For AMD use either `gallium` (for [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver)) or `vdpau` (for [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver)).

**Note:** You can find the installed drivers in `/usr/lib/dri/`.

### Configuring VDPAU

The driver for use with VDPAU is auto-detected, but you may need to override it by using the `VDPAU_DRIVER` [environment variable](/index.php/Environment_variable "Environment variable").

The correct driver name depends on your setup:

*   For Intel Graphics or AMD Catalyst you [need](#Failed_to_open_VDPAU_backend) to set it to `va_gl`.
*   For the open source AMD/ATI driver set it to the proper driver version depending on your GPU (see below).
*   For NVIDIA's proprietary version set it to `nvidia`.

The driver name can determined by running:

 `$ grep -i vdpau ~/.local/share/xorg/Xorg.0.log` 
```
(II) RADEON(0): [DRI2] VDPAU driver: r300

```

In this case you want to set `VDPAU_DRIVER=r300`.

**Note:** You can find the installed drivers in `/usr/lib/vdpau/`.

For hybrid setups (both NVIDIA and AMD), it may be necessary to [set](/index.php/Environment_variable "Environment variable") `DRI_PRIME=1`. For more information see [PRIME](/index.php/PRIME "PRIME").

## Troubleshooting

### Failed to open VDPAU backend

This happens when you use [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) without overriding `VDPAU_DRIVER`. VDPAU doesn't know what driver to use in this case for some reason and guesses wrongly. See [#Configuring VDPAU](#Configuring_VDPAU).

However you may want to configure your media player to use VA-API instead, getting far better results. See [#Software](#Software).

### VA-API vaInitialize failed

If vainfo gives you this error:

```
libva info: va_openDriver() returns -1
vaInitialize failed with error code -1 (unknown libva error),exit

```

You may need to set the `LIBVA_DRIVER_NAME` environment variable to `vdpau` or `gallium`, see [#Configuring VA-API](#Configuring_VA-API).