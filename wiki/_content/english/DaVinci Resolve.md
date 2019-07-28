Davinci Resolve is a proprietary video editor, color correction and compositing application.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Application window misses title bar](#Application_window_misses_title_bar)
    *   [2.2 My .mp4 clips are shown as audio clips and even its sound is not working](#My_.mp4_clips_are_shown_as_audio_clips_and_even_its_sound_is_not_working)
*   [3 See also](#See_also)

## Installation

There is a free version and a paid version (a.k.a. Studio).
For free version [Install](/index.php/Install "Install") the [davinci-resolve](https://aur.archlinux.org/packages/davinci-resolve/) or [davinci-resolve-beta](https://aur.archlinux.org/packages/davinci-resolve-beta/) package.
For studio version install [davinci-resolve-studio](https://aur.archlinux.org/packages/davinci-resolve-studio/) or [davinci-resolve-studio-beta](https://aur.archlinux.org/packages/davinci-resolve-studio-beta/) package.

To run Davinci Resolve it is required to have suitable OpenGL driver and suitable OpenCL driver.

<caption>Table of OpenGL drivers</caption>
| GPU vendor | Type | Driver | OpenGL | Documentation | Works with Davinci Resolve |
| AMD / ATI | Open source | [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [AMDGPU](/index.php/AMDGPU "AMDGPU") | No |
| [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [ATI](/index.php/ATI "ATI") | Not tested |
| Proprietary | [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) | [amdgpu-pro-libgl](https://aur.archlinux.org/packages/amdgpu-pro-libgl/) | [AMDGPU PRO](/index.php/AMDGPU_PRO "AMDGPU PRO") | Yes |
| Intel | Open source | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| NVIDIA | Open source | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [Nouveau](/index.php/Nouveau "Nouveau") | No |
| Proprietary | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) | [NVIDIA](/index.php/NVIDIA "NVIDIA") | Yes |

<caption>Table of tested [OpenCL](/index.php/OpenCL "OpenCL") drivers</caption>
| GPU Vendor | OpenCL driver | Tested version | Works with D.R. 16.0b6-1 |
| Neutral | opencl-mesa | No |
| AMD | [opencl-amdgpu-pro-orca](https://aur.archlinux.org/packages/opencl-amdgpu-pro-orca/) | 19.30_838629-1 | Yes |
| [opencl-amdgpu-pro-pal](https://aur.archlinux.org/packages/opencl-amdgpu-pro-pal/) | Not tested |
| Intel | [intel-compute-runtime](https://www.archlinux.org/packages/?name=intel-compute-runtime) | 19.27.13361-1 | Core dumped |
| [beignet](https://www.archlinux.org/packages/?name=beignet) | 1.3.2+12+gfc5f430c-2 | Core dumped |
| [intel-opencl](https://aur.archlinux.org/packages/intel-opencl/) | 5.0.r63503-2 | Core dumped |
| [intel-opencl-runtime](https://aur.archlinux.org/packages/intel-opencl-runtime/) | 1:18.1.0.013-2 | Core dumped |
| Nvidia | [opencl-nvidia](https://www.archlinux.org/packages/?name=opencl-nvidia) | Suitable, but working on cuda instead? |

So currently it is not possible to use intel gpu alone. If using AMD + Intel setups, you can render on intel (set it as primary in uefi setup) and install proprietary opencl driver for amd gpu.

## Troubleshooting

### Application window misses title bar

It is a problem of a Linux version of D.R. There is a workaround for KDE - a window rule to force enable title bar. See [[1]](https://forum.blackmagicdesign.com/viewtopic.php?=21&t=56878&p=456990#p456990)

### My .mp4 clips are shown as audio clips and even its sound is not working

This problem only affects a free version of D.R. for Linux. To workaround, you may convert your video file to another format or purchase a studio version.

## See also

[Post](https://forum.blackmagicdesign.com/viewtopic.php?f=21&t=56878&p=456990#p456924) on Davinci Resolve forum with tested configurations.