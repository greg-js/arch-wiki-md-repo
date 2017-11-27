[PCSX-Reloaded](https://pcsxr.codeplex.com/), also known as PCSXR, PCSXr or PCSX-r, is a plugin based console emulator built on top of the [PSEmu Pro](https://en.wikipedia.org/wiki/PSEmu_Pro "wikipedia:PSEmu Pro") plugin interface, which allows playing Play Station 1 games on a PC.

Being a plugin based emulator allows more configurability, including setting screen resolutions and texture qualities higher than those supported by the original console.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 BIOS](#BIOS)
    *   [2.2 Plugins](#Plugins)
*   [3 Configuration](#Configuration)
*   [4 Playing](#Playing)
    *   [4.1 Save States](#Save_States)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 wrong ELF class: ELFCLASS32](#wrong_ELF_class:_ELFCLASS32)
    *   [5.2 cfgPeteXGL2, cfgPeteMesaGL or cfgPeopsOSS not found](#cfgPeteXGL2.2C_cfgPeteMesaGL_or_cfgPeopsOSS_not_found)
    *   [5.3 PE.Op.S OSS Audio Driver outputs no sound](#PE.Op.S_OSS_Audio_Driver_outputs_no_sound)
    *   [5.4 PCSXR segfaults when launching a game or the BIOS](#PCSXR_segfaults_when_launching_a_game_or_the_BIOS)
    *   [5.5 Opening the Pete's plugin interface doesn't work: error while loading shared libraries: libgtk-1.2.so.0](#Opening_the_Pete.27s_plugin_interface_doesn.27t_work:_error_while_loading_shared_libraries:_libgtk-1.2.so.0)
*   [6 See also](#See_also)

## Installation

Install the stable [pcsxr](https://www.archlinux.org/packages/?name=pcsxr) package or alternately the [pcsxr-git](https://aur.archlinux.org/packages/pcsxr-git/) for the development version.

Additionally, you can also install the [pcsxr-gtk2](https://aur.archlinux.org/packages/pcsxr-gtk2/) package for the GTK2 version, which allows to run GTK based plugin interfaces without having to install [lib32-gtk](https://aur.archlinux.org/packages/lib32-gtk/) from the [AUR](/index.php/AUR "AUR").

Notice, however, that if you have a 64 bit machine and you choose to grab one of the [AUR](/index.php/AUR "AUR") versions, PCSXR will be compiled to 64 bit architecture, rendering it incompatible with the vast majority of the plugins, which are 32bit only. If you intend to use any plugins other than the ones that come with the emulator, you should install the 32 bit package from the [Multilib](/index.php/Multilib "Multilib") repositories.

## Usage

Upon the first launch PCSXR will create a hidden directory named `.pcsxr` into your home directory, where all the configurations, plugins, savedata and the console bios will be stored. Deleting this directory will reset PCSXR's configuration to it's original state.

### BIOS

**Warning:** The installation and use of this emulator requires a Sony PlayStation BIOS file. You may not use such a file to play games in a PSX emulator if you do not own a Sony PlayStation, Sony PSOne or Sony PlayStation 2 console. Owning the BIOS image without owning the actual console is a violation of copyright law. You have been warned.

The emulator needs a dump of the bios of a real console to run. That's not provided by PCSXR since using or distributing the bios infringes Sony's Copyrights and is illegal.

The bios dump must be put into the `~/.pcsxr/bios/` directory.
PCSXR can also emulate an internal bios, but it is not compatible with all games and presents issues. PCSXR provides an [incomplete compatibility list](https://pcsxr.codeplex.com/wikipage?title=PCSX-Reloaded%20incomplete%20HLE%20compatibility%20list&referringTitle=Documentation) on their site.

### Plugins

PCSXR already comes with a set of plugins that allows to play out-of-the-box, however, if you wish to install plugins for extra video/sound/joystick/configurability you'll need to put the respective plugins and their configuration files at the `~/.pcsxr/plugins/` directory. Most of the Linux compatible plugins can be found at [Pete's Domain](http://www.pbernert.com/index.htm).

Be aware that some of the plugins will require [lib32-gtk](https://aur.archlinux.org/packages/lib32-gtk/) to show their configuration interface.

## Configuration

Configure your Video, Sound, Controllers, CDROM and BIOS by going to `Configuration > Plugins & Bios`.

## Playing

Run a game from CDROM by clicking `File > Run CD` or by pressing `Ctrl+O`.

Run a game from an ISO or BIN file by clicking `File > Run ISO` or by pressing `Ctrl+I`.

Run the Play Station BIOS and manage your memory cards and savedata by clicking `File > Run BIOS` or by pressing `Ctrl + B`.

### Save States

PCSXR supports save states, which allows you to save your game progress in any moment, regardless of you being in a savepoint or not and without the need of attaching a new memory card.

There are 9 slots available for save states, meaning that for each different game you can have up to nine different states saved.

Save a state by clicking `Emulator > Save States` and selecting a slot or by pressing `Ctrl+Slot Number` eg. `Ctrl+1` for slot 1.

Load a state by clicking `Emulator > Load States` and selecting a state previously saved to a slot or by pressing `Alt+Slot Number` eg. `Alt+1` for slot 1.

## Troubleshooting

### wrong ELF class: ELFCLASS32

You installed a 64 bit version of the emulator and is trying to run a 32 bit plugin. Install the 32 bit version of [pcsxr](https://www.archlinux.org/packages/?name=pcsxr) found on the [Multilib](/index.php/Multilib "Multilib") repository

### cfgPeteXGL2, cfgPeteMesaGL or cfgPeopsOSS not found

This issue happens because the latest Linux version of [Pete's plugins](http://www.pbernert.com/html/gpu.htm) don't provide the configuration files with them. To solve the problem go to [Pete's GPU Plugins page](http://www.pbernert.com/html/gpu.htm) and find the **Linux GPU Configs** section, download the configuration files - they will come all together in a .tar.gz file. Fetch the missing ones from the Gzip file and put them on the `~/.pcsxr/plugins/` folder and the problem will be solved.

### PE.Op.S OSS Audio Driver outputs no sound

OSS is dated, use the SDL Sound 1.1.0 plugin that comes included with the emulator.

### PCSXR segfaults when launching a game or the BIOS

Segfaults are [confirmed to happen](https://bbs.archlinux.org/viewtopic.php?pid=1742975) in computers that have an Intel HD Graphics 965 installed on them, but the bug is reportedly happening on AMD and NVidia powered PC's as well.

Open the file `~/.pcsxr/pcsxr.cfg` and change the `Cpu` property's value from `0` to `1` to fix it.

You may also want to investigate the cause of the segfault by examining the [Core dump](/index.php/Core_dump "Core dump") with [coredumpctl](/index.php/Core_dump#Examining_a_core_dump "Core dump").

### Opening the Pete's plugin interface doesn't work: error while loading shared libraries: libgtk-1.2.so.0

Install [lib32-gtk](https://aur.archlinux.org/packages/lib32-gtk/). If pacman fails to resolve the dependencies, it's because they're not available on the official repos. Check the dependencies with `less PKGBUILD` and install them manually from the [AUR](/index.php/AUR "AUR").

## See also

*   [Wikipedia:PCSX-Reloaded](https://en.wikipedia.org/wiki/PCSX-Reloaded "wikipedia:PCSX-Reloaded")
*   [Emulation General wiki - Playstation emulators](http://emulation.gametechwiki.com/index.php/PlayStation_emulators)