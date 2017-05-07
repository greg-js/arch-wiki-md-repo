**Note:** RetroArch is not affiliated with [Arch Linux](/index.php/Arch_Linux "Arch Linux").

[RetroArch](http://www.retroarch.com/) is a modular, command-line driven, multi-system emulator that is designed to be fast, lightweight, and portable. Some of its features can be found on few other emulators, such as real-time rewinding and game-aware shading based on the libretro API.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 Paths](#Paths)
*   [4 Online updater](#Online_updater)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 No cores found](#No_cores_found)
    *   [5.2 Input devices do not operate](#Input_devices_do_not_operate)
    *   [5.3 Poor video performance](#Poor_video_performance)
*   [6 See also](#See_also)

## Installation

Install the [retroarch](https://www.archlinux.org/packages/?name=retroarch) package or alternatively [retroarch-git](https://aur.archlinux.org/packages/retroarch-git/) for the development version.

## Usage

RetroArch uses separate libraries, called "emulator cores" or "emulator implementations", available from both [Community](https://www.archlinux.org/packages/?q=libretro) and the [libretro GitHub repository](https://github.com/libretro).

Each libretro core package will install a library to `/usr/lib/libretro`. The syntax to choose one when executing *retroarch* is:

```
$ retroarch --libretro /usr/lib/libretro/libretro-*core*.so *path/to/rom*

```

A default emulation core can be defined in the configuration, obviating the need to specify it on every run.

 `/etc/retroarch.cfg or ~/.config/retroarch/retroarch.cfg`  `libretro_path = "/usr/lib/libretro/libretro-*core*.so"` 

## Configuration

RetroArch provides a very well commented skeleton configuration file located at `/etc/retroarch.cfg`.

Copy the skeleton configuration file to your home directory

```
$ cp /etc/retroarch.cfg ~/.config/retroarch/retroarch.cfg

```

It supports split configuration files using the `#include "foo.cfg"` directive within the main configuration file, `retroarch.cfg`. This can be overridden using the `--appendconfig /path/to/config` parameter and is beneficial if different keybinds, video configurations or audio settings are required for the various implementations.

### Paths

Some modifications are required to use the correct paths for Arch packages:

```
assets_directory = "/usr/share/libretro/assets"
libretro_info_path = "/usr/share/libretro/info"
libretro_directory = "/usr/lib/libretro"
joypad_autoconfig_dir = "/usr/share/libretro/autoconfig"

```

**Tip:** RetroArch is capable of loading *[bsnes xml filters](https://gitorious.org/bsnes/xml-shaders)* and *[cg shaders](https://github.com/libretro/common-shaders)* that can be defined in `retroarch.cfg` as `video_bsnes_shader` and `video_cg_shader` respectively.

**Note:** [retroarch-git](https://aur.archlinux.org/packages/retroarch-git/) requires [nvidia-cg-toolkit](https://www.archlinux.org/packages/?name=nvidia-cg-toolkit) in order to use the *cg shaders*.

**Warning:** When using *[ALSA](/index.php/ALSA "ALSA")* it is necessary for the `audio_out_rate` to be equal to the system's default output rate, usually 48000.

## Online updater

Recent versions of RetroArch have introduced a built-in menu for updating core files and various assets from the [RetroArch Buildbot](https://buildbot.libretro.com/). It can be accessed from the main menu at "Online Updater".

 `Online Updater` 
```
Core Updater
Update Core Info Files
Update Assets
Update Autoconfig Profiles
Update Cheats
Update Databases
Update Overlays
Update GLSL Shaders
```

These cores and assets are kept up to date and can be pulled from the updater at any time.

## Troubleshooting

### No cores found

By default RetroArch will attempt to find cores in `~/.config/retroarch/cores`. The packages in the official repositories install the cores in `/usr/lib/libretro/` and the core info files in `/usr/share/libretro/info`. The settings can be changed to look in these directories; see [#Paths](#Paths) above.

### Input devices do not operate

It is likely to encounter problems if running on a CLI or a display server other than [Xorg](/index.php/Xorg "Xorg"), because /dev/input nodes are limited to root-only access. This is solved by manually adding a rule in `/etc/udev/rules.d/99-evdev.rules`, with `KERNEL=="event*", NAME="input/%k", MODE="666"` as its contents. Reload udev rules by running:

```
# udevadm control --reload-rules

```

If rebooting the system or replugging the devices are not options, permissions may be forced using:

```
# chmod 666 /dev/input/event*

```

Alternatively, add your user to the "input" group, e.g.

```
 # usermod -a -G input user

```

### Poor video performance

If poor video performance is met, RetroArch may be run on a separate thread by setting `video_threaded = true` in `~/.config/retroarch/retroarch.cfg`.

This is, however, a solution that should be not be used if tweaking RetroArch's video resolution/refresh rate fixes the problem, as it makes perfect V-Sync impossible, and slightly increases latency.

## See also

*   [Official Website](http://www.retroarch.com/)
*   [RetroArch wiki on GitHub](https://github.com/libretro/RetroArch/wiki)
*   [Documentation for developers](https://github.com/libretro/libretro.github.com/wiki/Documentation-devs)