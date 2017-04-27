[Dwarf Fortress](http://www.bay12games.com/dwarves/) is a single-player fantasy game. You can control a dwarven outpost or an adventurer in a randomly generated, persistent world. It is renowned for its highly customizable, complex indepth gameplay.

The game is played with keyboard only, though there exist [mods](http://dwarffortresswiki.org/index.php/DF2014:Utilities#DFHack) which enable mouse support via plugins. Without any graphic mods ([[1]](http://dwarffortresswiki.org/index.php/DF2014:Tilesets)) the game is displayed in a terminal-like window with ASCII characters ([screenshots](http://www.bay12games.com/dwarves/screens.html)).

## Contents

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
*   [3 Tools](#Tools)
    *   [3.1 Dwarf Therapist](#Dwarf_Therapist)
    *   [3.2 SoundSense](#SoundSense)
    *   [3.3 quickfort](#quickfort)
    *   [3.4 StoneSense](#StoneSense)

## Installation

[Install](/index.php/Install "Install") package [dwarffortress](https://www.archlinux.org/packages/?name=dwarffortress) from the [official repositories](/index.php/Official_repositories "Official repositories").

Alternatively there are some [AUR](/index.php/AUR "AUR") packages coming with bitmap tilesets:

*   [dwarffortress-ironhand](https://aur.archlinux.org/packages/dwarffortress-ironhand/)
*   [dwarffortress-mayday](https://aur.archlinux.org/packages/dwarffortress-mayday/)
*   [dwarffortress-myne](https://aur.archlinux.org/packages/dwarffortress-myne/)
*   [dwarffortress-obsidian](https://aur.archlinux.org/packages/dwarffortress-obsidian/)
*   [dwarffortress-phoebus](https://aur.archlinux.org/packages/dwarffortress-phoebus/)
*   [dwarffortress-spacefox](https://aur.archlinux.org/packages/dwarffortress-spacefox/)

**Note:** Enabling [multilib](/index.php/Multilib "Multilib") repositories on x86_64 systems is no longer required for the basic game since 0.43.05 release.

You will need to be in the games group to run Dwarf Fortress. If you are not in the games group, add yourself, then log out and back in again:

```
# gpasswd -a USERNAME games

```

## Troubleshooting

If you get an error stating 'The file "index" must be in the "data" folder' then you may find a solution [here](http://robertqualls.com/2013/06/24/getting-dwarf-fortress-to-work-on-linux.html).

## Tools

### Dwarf Therapist

[Dwarf Therapist](http://dwarffortresswiki.org/index.php/DF2014:Utilities#Dwarf_Therapist) ([dwarftherapist-git](https://aur.archlinux.org/packages/dwarftherapist-git/) in [AUR](/index.php/AUR "AUR")) is an almost essential mod to tune dwarvish behaviour (makes life a lot easier). For it to work on current kernels you will need to disable a kernel security feature, since dwarf therapist directly accesses and modifies the memory of a running dwarf fortress instance. This setting is called `kernel.yama.ptrace_scope` and defaults to `1`. You need to set it to `0` for dwarf therapist to work:

```
# sysctl -w kernel.yama.ptrace_scope=0

```

and then

```
# sysctl -w kernel.yama.ptrace_scope=1

```

when you're done playing and have closed dwarf fortress and dwarf therapist.

For more information see [sysctl](/index.php/Sysctl "Sysctl").

**Warning:** You **should not** set this to `0` in `/etc/sysctl.d/` by default since it is an **important security feature in the kernel**! It is best to set it manually whenever you play dwarf fortress and reset it back to `1` when you are done playing.

Alternatively, you can just give that permission to dwarftherapist:

```
# setcap cap_sys_ptrace=eip /usr/bin/dwarftherapist

```

### SoundSense

[SoundSense](http://dwarffortresswiki.org/index.php/DF2014:Utilities#SoundSense) ([soundsense](https://aur.archlinux.org/packages/soundsense/) in [AUR](/index.php/AUR "AUR")) adds various sound effects and music via analysing the gamelog.txt.

### quickfort

Quickfort is a utility for Dwarf Fortress that helps you build fortresses from "blueprint" .CSV, .XLS, and .XLSX files.

*   [quickfort](https://aur.archlinux.org/packages/quickfort/)
*   [quickfort-git](https://aur.archlinux.org/packages/quickfort-git/)

### StoneSense

StoneSense is an isometric world visualizer for Dwarf Fortress, and can be installed with the [dfhack](https://aur.archlinux.org/packages/dfhack/) [AUR](/index.php/AUR "AUR") package.

If you choose to install StoneSense manually instead of using the AUR package, you'll need the following dependencies:

*   [lib32-libjpeg6-turbo](https://www.archlinux.org/packages/?name=lib32-libjpeg6-turbo)
*   [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12)
*   [lib32-allegro](https://aur.archlinux.org/packages/lib32-allegro/)