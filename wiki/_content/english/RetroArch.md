**Note:** RetroArch is not affiliated with [Arch Linux](/index.php/Arch_Linux "Arch Linux").

[RetroArch](http://www.retroarch.com/) is the reference implementation of the libretro API. It is a modular front-end for video game system emulators, game engines, video games, media players and other applications that offers several uncommon technical features such as multi-pass shader support, real-time rewinding and video recording (using [FFmpeg](/index.php/FFmpeg "FFmpeg")), it also features a gamepad-driven UI on top of a full-featured command-line interface.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Enabling the *Online Updater*](#Enabling_the_Online_Updater)
    *   [4.2 Enabling *SaveRAM Autosave Interval*](#Enabling_SaveRAM_Autosave_Interval)
    *   [4.3 Reset settings to their default value](#Reset_settings_to_their_default_value)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 No cores found](#No_cores_found)
    *   [5.2 Input devices do not operate](#Input_devices_do_not_operate)
    *   [5.3 Poor video performance](#Poor_video_performance)
    *   [5.4 Save data is lost whenever RetroArch crashes](#Save_data_is_lost_whenever_RetroArch_crashes)
*   [6 See also](#See_also)

## Installation

Install the [retroarch](https://www.archlinux.org/packages/?name=retroarch) package or alternatively [retroarch-git](https://aur.archlinux.org/packages/retroarch-git/) for the development version.

**Tip:** Install [retroarch-assets-xmb](https://www.archlinux.org/packages/?name=retroarch-assets-xmb) to allow the default menu driver (XMB) to work properly. Additionally, install [retroarch-autoconfig-udev](https://www.archlinux.org/packages/?name=retroarch-autoconfig-udev) to enable RetroArch to automatically map buttons to joypads when they are plugged.

## Usage

RetroArch relies on separate libraries, called "cores", available from the [Community](https://www.archlinux.org/packages/?q=libretro) repository, the [AUR](https://aur.archlinux.org/packages/?O=0&K=libretro) and the [libretro Buildbot](https://buildbot.libretro.com/), for most of its functionalities.

Each libretro core package will install a library to `/usr/lib/libretro/`. The syntax to choose one when executing *retroarch* is:

```
$ retroarch --libretro /usr/lib/libretro/*core*-libretro.so */path/to/rom*

```

A default core can be defined in the configuration, obviating the need to specify it on every run.

 `~/.config/retroarch/retroarch.cfg`  `libretro_path = "/usr/lib/libretro/*core*-libretro.so"` 

## Configuration

RetroArch provides a very well commented skeleton configuration file located at `/etc/retroarch.cfg`.

Copy the skeleton configuration file to your home directory

```
$ cp /etc/retroarch.cfg ~/.config/retroarch/retroarch.cfg

```

It supports split configuration files using the `#include "foo.cfg"` directive within the main configuration file, `retroarch.cfg`. This can be overridden using the `--appendconfig */path/to/config*` parameter and is beneficial if different keybinds, video configurations or audio settings are required for the various cores.

**Tip:** RetroArch is capable of loading [bsnes xml filters](https://gitorious.org/bsnes/xml-shaders) and [cg shaders](https://github.com/libretro/common-shaders) that can be defined in `retroarch.cfg` as `video_bsnes_shader` and `video_cg_shader` respectively.

**Note:**

*   [retroarch-git](https://aur.archlinux.org/packages/retroarch-git/) requires [nvidia-cg-toolkit](https://www.archlinux.org/packages/?name=nvidia-cg-toolkit) in order to use the *cg shaders*.
*   When using [ALSA](/index.php/ALSA "ALSA") it is necessary for the `audio_out_rate` to be equal to the system's default output rate, usually `48000`.

## Tips and tricks

### Enabling the *Online Updater*

Recent versions of RetroArch have introduced a built-in menu for updating and downloading core files and various assets from the [libretro Buildbot](https://buildbot.libretro.com/). To enable it, open `~/.config/retroarch/retroarch.cfg` and set `menu_show_core_updater` to `"true"`.

 `~/.config/retroarch/retroarch.cfg`  `menu_show_core_updater = "true"`  `Online Updater` 
```
Core Updater
Thumbnails Updater
Content Downloader
Update Core Info Files
Update Assets
Update Joypad Profiles
Update Cheats
Update Databases
Update Overlays
Update GLSL Shaders
Update Slang Shaders
```

These cores and assets are kept up to date and can be pulled from the updater any time there's an update.

### Enabling *SaveRAM Autosave Interval*

By default, RetroArch only writes SRAM onto disk when it exits without error, which means that there's a risk of losing save data when using crash-prone cores. To change this behavior, open `~/.config/retroarch/retroarch.cfg` and set `autosave_interval` to *n*.

 `~/.config/retroarch/retroarch.cfg`  `autosave_interval = "600"` 

With the example above, RetroArch will write SRAM changes onto disk every 600 seconds.

**Warning:** Setting this value too low will cause all sorts of issue, most notably hardware degradation. See [[1]](https://github.com/libretro/RetroArch/issues/4901#issuecomment-300888019)

### Reset settings to their default value

To reset a setting or keybind to its default value through the GUI, highlight it and press `Start`. To remove a button from a keybind, highlight the keybind and press `Y`.

## Troubleshooting

### No cores found

By default RetroArch will attempt to find cores in `/usr/lib/libretro/`. Cores downloaded using the built-in *Online Updater* will fail to save unless RetroArch is run as root (not recommended, as it may overwrite cores installed by [pacman](/index.php/Pacman "Pacman") and also because it poses a security risk.[[2]](https://bugzilla.gnome.org//show_bug.cgi?id=772875#c5)) because users do not normally have permission to modify this directory. To use a user-owned directory instead, edit these lines:

 `~/.config/retroarch/retroarch.cfg` 
```
libretro_directory = "~/.config/retroarch/cores"
libretro_info_path = "~/.config/retroarch/cores/info"
```

**Note:** Cores obtained from the [Community](https://www.archlinux.org/packages/?q=libretro) repository or the [AUR](https://aur.archlinux.org/packages/?O=0&K=libretro) will be installed to `/usr/lib/libretro/` regardless of this setting, because of this, it's recommended to stick to one method of obtaining cores, use the default directory when obtaining cores from the Community repository or the AUR or a user-owned directory (such as `~/.config/retroarch/cores`) when using the *Online Updater*.

### Input devices do not operate

You may encounter problems if running on a CLI or a display server other than [Xorg](/index.php/Xorg "Xorg") or if you use the [udev](/index.php/Udev "Udev") input driver, because `/dev/input` nodes are limited to root-only access. Try adding your user to the "input" [group](/index.php/Group "Group") then logging in again.

Alternatively, manually add a rule in `/etc/udev/rules.d/99-evdev.rules`, with `KERNEL=="event*", NAME="input/%k", MODE="666"` as its contents. Reload [udev rules](/index.php/Udev_rules "Udev rules") by running:

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

### Save data is lost whenever RetroArch crashes

See [#Enabling SaveRAM Autosave Interval](#Enabling_SaveRAM_Autosave_Interval).

## See also

*   [Official Website](http://www.retroarch.com/)
*   [RetroArch wiki on GitHub](https://github.com/libretro/RetroArch/wiki)
*   [Documentation for developers](https://github.com/libretro/libretro.github.com/wiki/Documentation-devs)