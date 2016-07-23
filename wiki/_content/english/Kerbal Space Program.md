Since version 0.19, Kerbal Space Program includes a native Linux version. However, only Ubuntu 12.04 is officialy supported, so it may not work on Arch Linux out of the box.

## Contents

*   [1 Installation](#Installation)
*   [2 Known issues](#Known_issues)
    *   [2.1 Game never progresses past initial loading](#Game_never_progresses_past_initial_loading)
    *   [2.2 Game SegFaults before launching, v1.1+](#Game_SegFaults_before_launching.2C_v1.1.2B)
    *   [2.3 No text display](#No_text_display)
    *   [2.4 In-game menus are blank, v1.1+](#In-game_menus_are_blank.2C_v1.1.2B)
    *   [2.5 Graphics flickering when using primusrun](#Graphics_flickering_when_using_primusrun)
    *   [2.6 Game crashes when accessing settings or saves on 64 bit systems on Steam](#Game_crashes_when_accessing_settings_or_saves_on_64_bit_systems_on_Steam)
    *   [2.7 Game has garbled graphics when running on x86_64 with all lib32 drivers installed](#Game_has_garbled_graphics_when_running_on_x86_64_with_all_lib32_drivers_installed)
    *   [2.8 No audio on 64-bit systems](#No_audio_on_64-bit_systems)
    *   [2.9 Black ingame textures](#Black_ingame_textures)
*   [3 See also](#See_also)

## Installation

Install [kerbalspaceprogram](https://aur.archlinux.org/packages/kerbalspaceprogram/) from the [AUR](/index.php/AUR "AUR") or install it in [Steam](/index.php/Steam "Steam") client if you bought steam version of the game.

## Known issues

### Game never progresses past initial loading

To fix this, set:

```
LC_ALL=C

```

This is also relevant if your rocket's parts do not connect.

### Game SegFaults before launching, v1.1+

The Unity 5 engine expects you to be running PulseAudio. You can use the 'pulsenomore' tool[[1]](http://bugs.kerbalspaceprogram.com/issues/7515#note-28) posted on the KSP bug tracker as a workaround until this is fixed by the Unity devs.

### No text display

The game requires Arial and Arial Black fonts, provided in the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) [AUR](/index.php/AUR "AUR") package.

Another alternative is to try to use [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont), from the [official repositories](/index.php/Official_repositories "Official repositories"). This worked using KSP 0.90.0 on x86_64 Arch Linux. YMMV

### In-game menus are blank, v1.1+

Some resolutions cause menus to appear empty. Try using your settings.cfg file to enable fullscreen and/or change your resolution by a few pixels, e.g. 1366x768 to 1363x768\.

Imperfect resolutions can cause poor font rendering. If this happens you can use the AnyRes mod to change your resolution in-game to find a good one, rather than launching the game for every change.

Another solution that may work on some architectures is to add `-force-glcore` as a launch option, or passed in as a command line flag. For Steam, go to: Library -) right click on KSP -) Proprieties -) Set up launch options and add -force-glcore The game engine will try to run the game with the best OpenGL version possible and all available OpenGL extensions. With this option enabled you may encounter shadow glitches, try few different settings in-game in the setting panel to resolve the problem.

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