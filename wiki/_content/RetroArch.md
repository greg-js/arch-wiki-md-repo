# RetroArch

**Note:** RetroArch is not affiliated with [Arch Linux](/index.php/Arch_Linux "Arch Linux").

RetroArch is a modular, command-line driven, multi-system emulator that is designed to be fast, lightweight, and portable. Some of its features can be found on few other emulators, such as real-time rewinding and game-aware shading based on the libretro API.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Input devices do not operate](#Input_devices_do_not_operate)
    *   [4.2 Poor video performance](#Poor_video_performance)
*   [5 See also](#See_also)

## Installation

**RetroArch** — Stable version.

	[http://www.libretro.com/](http://www.libretro.com/) || [retroarch](https://aur.archlinux.org/packages/retroarch/)<sup><small>AUR</small></sup>

**RetroArch (git)** — Development version.

	[http://www.libretro.com/](http://www.libretro.com/) || [retroarch-git](https://aur.archlinux.org/packages/retroarch-git/)<sup><small>AUR</small></sup>

**RetroArch-Phoenix (git)** — GTK+ front-end, development version.

	[https://github.com/Themaister/RetroArch-Phoenix](https://github.com/Themaister/RetroArch-Phoenix) || [retroarch-phoenix-git](https://aur.archlinux.org/packages/retroarch-phoenix-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/retroarch-phoenix-git)]</sup>, or [retroarch-phoenix-qt-git](https://aur.archlinux.org/packages/retroarch-phoenix-qt-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/retroarch-phoenix-qt-git)]</sup> (qt build)

## Usage

RetroArch uses separate libraries, called _emulator cores_ or _emulator implementations_, available from both the [AUR](https://aur.archlinux.org/packages/?O=0&K=libretro) and the [libretro github repository](http://github.com/libretro).

Each package from the [AUR](/index.php/AUR "AUR") will install a library to `/usr/lib/libretro/`. The syntax to choose one when executing _retroarch_ is:

```
$ retroarch -L /usr/lib/libretro/libretro-(emulation core).so ~/path/to/foo

```

**Tip:** RetroArch can work with `*.zip` files using the [retroarch-zip](https://github.com/ToadKing/RetroArch-Rpi/blob/master/retroarch-zip) shell wrapper, although this method is not properly implemented and can be unstable.

A default emulation core can be defined in `retroarch.cfg`, obviating the need to specify it on every run.

Example:

 `/etc/retroarch.cfg or ~/.retroarch.cfg`  `libretro_path = "/usr/lib/libretro/libretro-foo.so"` 

## Configuration

RetroArch provides a very well commented skeleton configuration file located at `/etc/retroarch.cfg`.

It supports split configuration files using the `#include "foo.cfg"` directive within the main configuration file, `retroarch.cfg`. This can be overridden using the `--appendconfig /path/to/config` parameter and is beneficial if different keybinds, video configurations or audio settings are required for the various implementations.

**Tip:** RetroArch is capable of loading _[bsnes xml filters](https://gitorious.org/bsnes/xml-shaders)_ and _[cg shaders](https://github.com/libretro/common-shaders)_ that can be defined in `retroarch.cfg` as `video_bsnes_shader` and `video_cg_shader` respectively.

**Note:** [retroarch-git](https://aur.archlinux.org/packages/retroarch-git/)<sup><small>AUR</small></sup> requires [nvidia-cg-toolkit](https://www.archlinux.org/packages/?name=nvidia-cg-toolkit) in order to use the _cg shaders_.

**Warning:** When using _[ALSA](/index.php/ALSA "ALSA")_ it is necessary for the `audio_out_rate` to be equal to the system's default output rate, usually 48000.

## Troubleshooting

### Input devices do not operate

It is likely to encounter problems if running on a CLI or a display server other than [Xorg](/index.php/Xorg "Xorg"), because /dev/input nodes are limited to root-only access. This is solved by manually adding a rule in `/etc/udev/rules.d/99-evdev.rules`, with `KERNEL=="event*", NAME="input/%k", MODE="666"` as its contents. Reload udev rules by running:

```
# udevadm control --reload-rules

```

If rebooting the system or replugging the devices are not options, permissions may be forced using:

```
# chmod 666 /dev/input/event*

```

### Poor video performance

If poor video performance is met, RetroArch may be run on a separate thread by setting `video_threaded = true` in `~/.config/retroarch/retroarch.cfg`.

This is, however, a solution that should be not be used if tweaking RetroArch's video resolution/refresh rate fixes the problem, as it makes perfect V-Sync impossible, and slightly increases latency.

## See also

*   [RetroArch wiki on Github](https://github.com/libretro/RetroArch/wiki)
*   [Documentation for developers](http://github.com/libretro/libretro.github.com/wiki/Documentation-devs)

Retrieved from "[https://wiki.archlinux.org/index.php?title=RetroArch&oldid=407580](https://wiki.archlinux.org/index.php?title=RetroArch&oldid=407580)"