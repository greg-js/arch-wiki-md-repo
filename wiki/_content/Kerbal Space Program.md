# Kerbal Space Program

Since version 0.19, Kerbal Space Program includes a native Linux version. However, only Ubuntu 12.04 is officialy supported, so it may not work on Arch Linux out of the box.

## Contents

*   [1 Installation](#Installation)
*   [2 Known issues](#Known_issues)
    *   [2.1 Game never progresses past initial loading](#Game_never_progresses_past_initial_loading)
    *   [2.2 No text display](#No_text_display)
    *   [2.3 Graphics flickering when using primusrun](#Graphics_flickering_when_using_primusrun)
    *   [2.4 Game crashes when accessing settings or saves on 64 bit systems on Steam](#Game_crashes_when_accessing_settings_or_saves_on_64_bit_systems_on_Steam)
    *   [2.5 Game has garbled graphics when running on x86_64 with all lib32 drivers installed](#Game_has_garbled_graphics_when_running_on_x86_64_with_all_lib32_drivers_installed)
    *   [2.6 No audio on 64-bit systems](#No_audio_on_64-bit_systems)
    *   [2.7 Black ingame textures](#Black_ingame_textures)
*   [3 See also](#See_also)

## Installation

Install [kerbalspaceprogram](https://aur.archlinux.org/packages/kerbalspaceprogram/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kerbalspaceprogram)]</sup> from the [AUR](/index.php/AUR "AUR") or install it in [Steam](/index.php/Steam "Steam") client if you bought steam version of the game.

## Known issues

### Game never progresses past initial loading

To fix this, set:

```
LC_ALL=C

```

This is also relevant if your rocket's parts do not connect.

### No text display

The game requires Arial and Arial Black fonts, provided in the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup> [AUR](/index.php/AUR "AUR") package.

Another alternative is to try to use [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont), from the [official repositories](/index.php/Official_repositories "Official repositories"). This worked using KSP 0.90.0 on x86_64 Arch Linux. YMMV

### Graphics flickering when using primusrun

Run with PRIMUS_SYNC=2 (but you will get reduced frame rate this way)

### Game crashes when accessing settings or saves on 64 bit systems on Steam

In the properties for Kerbal Space program, set a launch option of:

```
LC_ALL=C %command%_64

```

### Game has garbled graphics when running on x86_64 with all lib32 drivers installed

Steam launches the KSP.x86 executable vs the KSP.x86_64 executable. Navigate to

```
/home/$USER/.local/share/Steam/SteamApps/common/Kerbal\ Space\ Program/ 

```

Launch with

```
./KSP.x86_64

```

Alternatively, to launch it from steam, set the following launch option:

```
 %command%_64

```

### No audio on 64-bit systems

Run the 64-bit Executable.

Steam launches the KSP.x86 executable vs the KSP.x86_64 executable. Navigate to

```
/home/$USER/.local/share/Steam/SteamApps/common/Kerbal\ Space\ Program/ 

```

Launch with

```
./KSP.x86_64

```

Or you can simply right click on Kerbal Space Program on your game list, click on Properties, click on SET LAUNCH OPTIONS, then add this:

```
LD_LIBRARY_PATH="/usr/lib:$LD_LIBRARY_PATH" LC_ALL=C %command%_64

```

### Black ingame textures

Disable "Edge Highlighting (PPFX)" in graphics settings ingame.

## See also

*   [http://forum.kerbalspaceprogram.com/showthread.php/24529-The-Linux-compatibility-thread](http://forum.kerbalspaceprogram.com/showthread.php/24529-The-Linux-compatibility-thread)!

Retrieved from "[https://wiki.archlinux.org/index.php?title=Kerbal_Space_Program&oldid=392308](https://wiki.archlinux.org/index.php?title=Kerbal_Space_Program&oldid=392308)"