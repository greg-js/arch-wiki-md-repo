Davinci Resolve is a proprietary video editor, color correction and compositing application.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 BlackMagic Design Cards](#BlackMagic_Design_Cards)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Application window misses title bar](#Application_window_misses_title_bar)
    *   [2.2 My .mp4 clips are shown as audio clips and even its sound is not working](#My_.mp4_clips_are_shown_as_audio_clips_and_even_its_sound_is_not_working)
    *   [2.3 HiDPI](#HiDPI)
    *   [2.4 Wine version](#Wine_version)
    *   [2.5 Wrong OpenCL Version](#Wrong_OpenCL_Version)
*   [3 See also](#See_also)

## Installation

There is a free version and a paid version (a.k.a. Studio).
For the free version, [install](/index.php/Install "Install") [davinci-resolve](https://aur.archlinux.org/packages/davinci-resolve/) or [davinci-resolve-beta](https://aur.archlinux.org/packages/davinci-resolve-beta/).
For the Studio version, install [davinci-resolve-studio](https://aur.archlinux.org/packages/davinci-resolve-studio/) or [davinci-resolve-studio-beta](https://aur.archlinux.org/packages/davinci-resolve-studio-beta/).

To run DaVinci Resolve, it is required to use suitable OpenGL and OpenCL drivers. Open-source OpenCL drivers are currently unsupported. Please notice that incompatible OpenCL drivers should be uninstalled as they may cause Resolve to crash (e.g. uninstall [opencl-mesa](https://www.archlinux.org/packages/?name=opencl-mesa) if you're using a proprietary equivalent).

Standalone Intel GPUs are currently unsupported. If using hybrid AMD + Intel setups, you can use the Intel GPU as the primary graphics card and use an proprietary OpenCL driver for the AMD GPU.

<caption>Table of OpenGL drivers</caption>
| GPU vendor | Type | Driver | OpenGL | Documentation | Works with DaVinci Resolve |
| AMD / ATI | Open source | [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [AMDGPU](/index.php/AMDGPU "AMDGPU") | No |
| [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [ATI](/index.php/ATI "ATI") | Not tested |
| Proprietary | [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) | [amdgpu-pro-libgl](https://aur.archlinux.org/packages/amdgpu-pro-libgl/) | [AMDGPU PRO](/index.php/AMDGPU_PRO "AMDGPU PRO") | Yes |
| Intel | Open source | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| NVIDIA | Open source | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [Nouveau](/index.php/Nouveau "Nouveau") | No |
| Proprietary | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) | [NVIDIA](/index.php/NVIDIA "NVIDIA") | Yes |

<caption>Table of tested [OpenCL](/index.php/OpenCL "OpenCL") drivers</caption>
| GPU Vendor | OpenCL driver | Tested version | Works with DaVinci Resolve |
| Neutral | [opencl-mesa](https://www.archlinux.org/packages/?name=opencl-mesa) | No |
| AMD | [opencl-amdgpu-pro-orca](https://aur.archlinux.org/packages/opencl-amdgpu-pro-orca/) | 19.30_838629-1 | Yes |
| [opencl-amdgpu-pro-pal](https://aur.archlinux.org/packages/opencl-amdgpu-pro-pal/) | 19.30_838629-1 | Yes |
| Intel | [intel-compute-runtime](https://www.archlinux.org/packages/?name=intel-compute-runtime) | 19.27.13361-1 | Core dumped |
| [beignet](https://www.archlinux.org/packages/?name=beignet) | 1.3.2+12+gfc5f430c-2 | Core dumped |
| [intel-opencl](https://aur.archlinux.org/packages/intel-opencl/) | 5.0.r63503-2 | Core dumped |
| [intel-opencl-runtime](https://aur.archlinux.org/packages/intel-opencl-runtime/) | 1:18.1.0.013-2 | Core dumped |
| Nvidia | [opencl-nvidia](https://www.archlinux.org/packages/?name=opencl-nvidia) | Suitable, but working on cuda instead? |

### BlackMagic Design Cards

If using DeckLink, UltraStudio or Intensity cards for video capture and playback, install Desktop Video Software with [decklink](https://aur.archlinux.org/packages/decklink/) package.

## Troubleshooting

### Application window misses title bar

It is a problem of a Linux version of D.R. There is a workaround for KDE - a window rule to force enable title bar. See [[1]](https://forum.blackmagicdesign.com/viewtopic.php?=21&t=56878&p=456990#p456990)

### My .mp4 clips are shown as audio clips and even its sound is not working

This problem only affects a free version of D.R. for Linux. MP4 containers are not supported, also AAC audio is not supported. To workaround, you may convert your video file to another format or purchase a studio version. Transcoding command may look like this:

```
ffmpeg -i input.mp4 -c:v dnxhd -profile:v dnxhr_hq -pix_fmt yuv422p -c:a pcm_s16le -f mov output.mov

```

### HiDPI

To enable compatibility with high-resolution displays, set the following environment variables accordingly:

```
export QT_DEVICE_PIXEL_RATIO=2
export QT_AUTO_SCREEN_SCALE_FACTOR=true

```

Source: [https://forum.blackmagicdesign.com/viewtopic.php?f=21&t=84614&p=469009&hilit=hidpi#wrapper](https://forum.blackmagicdesign.com/viewtopic.php?f=21&t=84614&p=469009&hilit=hidpi#wrapper)

### Wine version

Some plugins are available for Windows, but not available for Linux, so you may want to use Davinci Resolve via wine. Unfortunately, as of wine 4.13-1, it is not working. Splash screen stucks at "Looking for control surface" and in terminal there is such error message:

```
 wine: Call from 0x7bc6c52c to unimplemented function OpenCL.dll.clReleaseDevice, aborting

```

### Wrong OpenCL Version

If the Application simply is not starting, even after showing installer and "tour" successfully your OpenCl Version may not match your NVIDIA driver. If you have installed nvidia-440xx make sure to install opencl-nvidia-440xx as well. A possible error message:

 `~/.local/share/DaVinciResolve/logs/LogArchive/ResolveDebug_C1.txt` 
```
...
OpenCL error -1001: 'Unspecified Error', GPUPropertiesUtilUnix.cpp:338
...
```

## See also

[Post](https://forum.blackmagicdesign.com/viewtopic.php?f=21&t=56878&p=456990#p456924) on Davinci Resolve forum with tested configurations.