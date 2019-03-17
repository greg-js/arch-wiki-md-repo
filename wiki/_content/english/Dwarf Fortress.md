[Dwarf Fortress](http://www.bay12games.com/dwarves/) is a single-player fantasy game. You can control a dwarven outpost or an adventurer in a randomly generated, persistent world. It is renowned for its highly customizable, complex indepth gameplay.

The game is played with keyboard only, though there exist [mods](http://dwarffortresswiki.org/index.php/DF2014:Utilities#DFHack) which enable mouse support via plugins. Without any graphic mods (also known as [tilesets](http://dwarffortresswiki.org/index.php/DF2014:Tilesets)) the game is displayed in a terminal-like window with ASCII characters ([screenshots](http://www.bay12games.com/dwarves/screens.html)).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Tools](#Tools)
    *   [2.1 Dwarf Therapist](#Dwarf_Therapist)
    *   [2.2 Manipulator](#Manipulator)
    *   [2.3 SoundSense](#SoundSense)
    *   [2.4 quickfort](#quickfort)
    *   [2.5 StoneSense](#StoneSense)

## Installation

[Install](/index.php/Install "Install") the [dwarffortress](https://www.archlinux.org/packages/?name=dwarffortress) package.

Alternatively there are some [AUR](/index.php/AUR "AUR") packages coming with bitmap tilesets:

*   [dwarffortress-ironhand](https://aur.archlinux.org/packages/dwarffortress-ironhand/)
*   [dwarffortress-phoebus](https://aur.archlinux.org/packages/dwarffortress-phoebus/)
*   [dwarffortress-obsidian](https://aur.archlinux.org/packages/dwarffortress-obsidian/) (outdated: requires enabling the [multilib](/index.php/Multilib "Multilib") repository)
*   [dwarffortress-spacefox](https://aur.archlinux.org/packages/dwarffortress-spacefox/) (outdated: requires enabling the [multilib](/index.php/Multilib "Multilib") repository)

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

**Note:** The permissions will reset after an update to Dwarf Therapist. Consider using [pacman hooks](/index.php/Pacman_hooks "Pacman hooks") to automatically configure the permissions after an update.

### Manipulator

[Manipulator](https://dfhack.readthedocs.io/en/stable/docs/Plugins.html#manipulator) is an in-game alternative to Dwarf Therapist with most of its functionality, which does not require extra permissions. It is enabled by default in the [dfhack](https://aur.archlinux.org/packages/dfhack/) package.

### SoundSense

[SoundSense](http://dwarffortresswiki.org/index.php/DF2014:Utilities#SoundSense) ([soundsense](https://aur.archlinux.org/packages/soundsense/) in [AUR](/index.php/AUR "AUR")) adds various sound effects and music via analysing the gamelog.txt.

### quickfort

[Quickfort](http://www.joelpt.net/quickfort/) is a utility for Dwarf Fortress that helps you build fortresses from "blueprint" .CSV, .XLS, and .XLSX files.

### StoneSense

[StoneSense](http://dwarffortresswiki.org/index.php/Utility:Stonesense) is an isometric world visualizer for Dwarf Fortress, and can be [installed](/index.php/Install "Install") with the [dfhack](https://aur.archlinux.org/packages/dfhack/) package.