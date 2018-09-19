**Note:** RetroArch is not affiliated with [Arch Linux](/index.php/Arch_Linux "Arch Linux").

[RetroArch](http://www.retroarch.com/) is the reference implementation of the libretro API. It is a modular front-end for video game system emulators, game engines, video games, media players and other applications that offers several uncommon technical features such as multi-pass shader support, real-time rewinding and video recording (using [FFmpeg](/index.php/FFmpeg "FFmpeg")), it also features a gamepad-driven UI on top of a full-featured command-line interface.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Disabling the *Online Updater*](#Disabling_the_Online_Updater)
    *   [4.2 Enabling *SaveRAM Autosave Interval*](#Enabling_SaveRAM_Autosave_Interval)
    *   [4.3 Filters and shaders](#Filters_and_shaders)
    *   [4.4 Reset settings to their default value](#Reset_settings_to_their_default_value)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 No cores found](#No_cores_found)
    *   [5.2 Input devices do not operate](#Input_devices_do_not_operate)
    *   [5.3 Poor video performance](#Poor_video_performance)
    *   [5.4 Audio issues with ALSA](#Audio_issues_with_ALSA)
    *   [5.5 Save data is lost whenever RetroArch crashes](#Save_data_is_lost_whenever_RetroArch_crashes)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [retroarch](https://www.archlinux.org/packages/?name=retroarch) or alternatively [retroarch-git](https://aur.archlinux.org/packages/retroarch-git/) for the development version.

**Tip:** [Install](/index.php/Install "Install") [retroarch-assets-xmb](https://www.archlinux.org/packages/?name=retroarch-assets-xmb) to get the fonts and icons for the RetroArch GUI. You need to edit RetroArch's [#Configuration](#Configuration) to load them.

## Usage

RetroArch relies on separate libraries, called "cores", for most of its functionality. These can be downloaded per-user within RetroArch itself (via the [libretro Buildbot](https://buildbot.libretro.com/)) or you can [install](/index.php/Install "Install") them system-wide via [Community](https://www.archlinux.org/groups/x86_64/libretro/) or [AUR](https://aur.archlinux.org/packages/?O=0&K=libretro).

By default RetroArch is configured to load the per-user cores that it downloads. Change your [#Configuration](#Configuration) if you install them elsewhere.

The command to run a particular core is

```
$ retroarch --libretro */path/to/some_core_libretro.so* */path/to/rom*

```

## Configuration

When you first run RetroArch it will create the user configuration file `~/.config/retroarch/retroarch.cfg`. If you install any RetroArch components system-wide with [pacman](/index.php/Pacman "Pacman"), you should specify these in the global configuration file and include them in your user file. For example,

 `/etc/retroarch.cfg` 
```
# for retroarch-assets-xmb
assets_directory = "/usr/share/retroarch/assets"
# for libretro-core-info
libretro_info_path = "/usr/share/libretro/info"
# for libretro cores
libretro_directory = "/usr/lib/libretro"
```
 `~/.config/retroarch/retroarch.cfg`  `#include "/etc/retroarch.cfg"` 
**Note:** RetroArch does not support multiple search paths for these components. For example, if you install cores with [pacman](/index.php/Pacman "Pacman") **and** download cores using RetroArch's GUI, you cannot configure RetroArch to show all of them at once since they are installed in different directories.

If you want to override your configuration (for example when running certain cores) you can use the `--appendconfig */path/to/config*` command line option.

## Tips and tricks

### Disabling the *Online Updater*

If you prefer to install all RetroArch components with [pacman](/index.php/Pacman "Pacman"), you can disable RetroArch's built-in updater to prevent accidentally installing components the wrong way.

 `~/.config/retroarch/retroarch.cfg`  `menu_show_core_updater = "false"` 

### Enabling *SaveRAM Autosave Interval*

By default, RetroArch only writes SRAM onto disk when it exits without error, which means that there's a risk of losing save data when using crash-prone cores. To change this behavior, open `~/.config/retroarch/retroarch.cfg` and set `autosave_interval` to *n*.

 `~/.config/retroarch/retroarch.cfg`  `autosave_interval = "600"` 

With the example above, RetroArch will write SRAM changes onto disk every 600 seconds.

**Warning:** Setting this value too low will cause all sorts of issue, most notably hardware degradation. See [[1]](https://github.com/libretro/RetroArch/issues/4901#issuecomment-300888019)

### Filters and shaders

RetroArch can load [BSNES XML filters](https://gitorious.org/bsnes/xml-shaders) and [CG shaders](https://github.com/libretro/common-shaders). These are set in `retroarch.cfg` with `video_bsnes_shader` and `video_cg_shader` respectively. The shaders can also be obtained and updated directly inside RetroArch using the online updater.

**Note:** [retroarch-git](https://aur.archlinux.org/packages/retroarch-git/) requires [nvidia-cg-toolkit](https://www.archlinux.org/packages/?name=nvidia-cg-toolkit) in order to use the *cg shaders*.

### Reset settings to their default value

To reset a setting or keybind to its default value through the GUI, highlight it and press `Start`. To remove a button from a keybind, highlight the keybind and press `Y`.

## Troubleshooting

### No cores found

By default RetroArch searches for cores in `~/.config/retroarch/cores`, which is where the Online Updater installs them. Cores installed with [pacman](/index.php/Pacman "Pacman") are placed in `/usr/lib/libretro` and thus will not appear in RetroArch's GUI. You should choose one method of installing cores (pacman or the Online Updater) and change your [#Configuration](#Configuration) to match.

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

### Audio issues with ALSA

When using [ALSA](/index.php/ALSA "ALSA") the `audio_out_rate` must match the system's default output rate, usually `48000`.

### Save data is lost whenever RetroArch crashes

See [#Enabling SaveRAM Autosave Interval](#Enabling_SaveRAM_Autosave_Interval).

## See also

*   [Official Website](http://www.retroarch.com/)
*   [RetroArch wiki on GitHub](https://github.com/libretro/RetroArch/wiki)
*   [Documentation for developers](https://github.com/libretro/libretro.github.com/wiki/Documentation-devs)