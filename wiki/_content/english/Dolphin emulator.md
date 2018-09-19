Dolphin is a Nintendo GameCube and Wii emulator, currently supporting the x86_64 and AArch64 architectures. Dolphin is available for Linux, macOS, Windows, and Android. It is a free and open source, community-developed project. Dolphin was the first GameCube and Wii emulator, and currently the only one capable of playing commercial games.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Config section](#Config_section)
    *   [2.2 Graphics section](#Graphics_section)
    *   [2.3 DSP section](#DSP_section)
*   [3 Playing](#Playing)
    *   [3.1 Dolphin's Wiki](#Dolphin.27s_Wiki)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Incompatibility with Wayland](#Incompatibility_with_Wayland)
    *   [4.2 Launching games fails with "WriteRest Op" error](#Launching_games_fails_with_.22WriteRest_Op.22_error)
    *   [4.3 Games play too fast](#Games_play_too_fast)
    *   [4.4 Emulation is too slow](#Emulation_is_too_slow)
    *   [4.5 Games frequently stutter on first playthrough, but subsequent runs are smooth](#Games_frequently_stutter_on_first_playthrough.2C_but_subsequent_runs_are_smooth)
*   [5 See also](#See_also)

## Installation

Install one of the following:

*   **[Dolphin emu](/index.php/Dolphin_emu "Dolphin emu")** — A GameCube / Wii emulator

	[https://dolphin-emu.org/](https://dolphin-emu.org/) || [dolphin-emu](https://www.archlinux.org/packages/?name=dolphin-emu)

*   **Dolphin emu (git)** — A GameCube / Wii emulator (development version)

	[https://github.com/dolphin-emu/dolphin](https://github.com/dolphin-emu/dolphin) || [dolphin-emu-git](https://aur.archlinux.org/packages/dolphin-emu-git/)

**Tip:**

*   Stable releases of Dolphin tend to grow old between releases, and are potentially outclassed by the development versions, which feature many speed improvements and bug fixes in comparison. If low performance or glitches are encountered, consider installing the [dolphin-emu-git](https://aur.archlinux.org/packages/dolphin-emu-git/) package.
*   Reinstalling the [dolphin-emu-git](https://aur.archlinux.org/packages/dolphin-emu-git/) package will upgrade Dolphin to the latest development version at any time.

## Configuration

**Tip:** Run `dolphin-emu -h` for help Dolphin's options.

**Note:** Dolphin may override these settings on a per-game basis, such as when a setting is know to break a certain game. If absolutely sure a specific setting will not crash the game, you can disable or change these overrides by right-clicking the game and selecting *Properties*. Likewise, you can set per-game settings using this method.

While no additional configuration is needed for the emulator to run (it is preconfigured with the default settings), altering the settings can improve performance and graphics alike. Settings are split to three main sections, *Config*, *Graphics* and *DSP*.

### Config section

**Tip:** Recent versions of Dolphin remove the *Audio* frameskip option, so *Auto* is now recommended.

On the General tab, check *Enable Dual Core* and *Enable Idle Skipping*. The frame limit should be set to "Auto", so that it works with games from all regions. The CPU emulation engine should be left as JIT Recompiler. Only check "Force console as NTSC-J" if intending to play imported Japanese discs.

All options on the "Interface" tab are personal choices.

The Audio tab is the DSP section's screen; setting it up now means there will be no need to do it later. See the [DSP settings paragraph](#DSP_section) below.

The next two tabs are not very important; the Gamecube tab has settings about connected accessories, such as memory cards, and the only remarkable Wii tab option is the "Aspect Ratio" drop-down list. Set it to either 16:9 or 4:3, depending on the display's [aspect ratio](https://en.wikipedia.org/wiki/Aspect_ratio "wikipedia:Aspect ratio").

On the final tab, "Paths", ISO directories can be set. The directory of game ISOs can also be set by clicking browse from the home screen, but here more options are available, such as *Search Subfolders*.

### Graphics section

On the "General" tab, choose OpenGL from the backend drop-down list for the currently most compatible renderer. Set the "Display" and "Other" settings to the desired configuration. V-sync is useful, but it can lead to slowdowns. The "render to main window" option improves the experience aesthetically.

If your graphics card supports [Vulkan](/index.php/Vulkan "Vulkan"), using the Vulkan backend may give you higher performance than OpenGL. Note that the Vulkan backend might not be compatible with certain titles, so if you run into issues with a game, try switching back to OpenGL before giving up. The official [compatibility list](https://dolphin-emu.org/compat/) often has hints about how each renderer handles a title.

On the "Enhancements" tab are the options that can improve graphics. While they result to great output, they can slow the emulation down to the point of making games unplayable. Choose the best settings possible, as long as speed remains 100%.

<caption>Comparison of options</caption>
| Option | Performance | Quality |
| **Internal resolution** | 1x Native | Auto (Window size) |
| **Anti-aliasing** | None | at least 2x |
| **Anisotropic filtering** | 1x | at least 2x |
| **Post-Processing Effect** | (off) | your choice
(see tip below) |
| **Scaled EFB copy** | unchecked | checked |
| **Per-Pixel Lightning** | unchecked | checked |
| **Force texture filtering,
Widescreen Hack,
Disable fog** | off | your option
(recommended: off) |

**Tip:** Dolphin is able to render games that were developed for 2D in anaglyph 3D. To enable this, set *Post-Processing Effect* to *stereoscopic* (default, for red-cyan mode) or *stereoscopic2* (blue-yellow). It is also **necessary** to uncheck "*Fast Depth Calculation*" on the *Hacks* tab (*see below*).

**Warning:** Using filters and other ways to improve graphics might break a few games or cause graphical glitches of any level.

Unless sure, the *Hacks* tab is best left untouched.

<caption>Defaults</caption>
| Option | Value |
| Skip EFB access from CPU | unchecked |
| Ignore format changes | checked |
| EFB copies | texture |
| Texture cache/ Accuracy | Fast |
| External frame buffer | disable |
| Cache display lists | unchecked |
| Disable destination alpha | unchecked |
| OpenCL texture decoder | unchecked |
| OpenMP texture decoder | unchecked |
| Fast depth calculation | checked
(Should uncheck for anaglyph 3D) |
| Vertex streaming hack | unchecked |

Similarly, unless sure, leave **everything** in the *Advanced* tab unchecked.

### DSP section

Set the DSP emulation engine to

*   DSP HLE for speed over accuracy,
*   DSP LLE recompiler for better accuracy with the cost of some speed,
*   DSP LLE interpreter; accurate but makes **everything** unplayable. Too slow.

*DSP LLE on separate thread* improves speed on computers with multi-core CPUs, but might cause audio glitches, and is known to break [Zelda ucode games](https://wiki.dolphin-emu.org/index.php?title=Category:Zelda_ucode_games). Audio backend is best set to [ALSA](/index.php/ALSA "ALSA"). For `pulseaudio`, Dolphin's optional dependency [PulseAudio](/index.php/PulseAudio "PulseAudio") needs to be installed.

**Note:** If you came here from the [Config section's](#Config_section) link, you should go back now.

## Playing

**Note:** Dolphin is a resource-heavy application, so expect not all games to run properly. See the reason [here](https://dolphin-emu.org/docs/faq/#why-do-i-need-such-powerful-computer-emulate-old-c).

**Warning:** Make sure you **only** use Dolphin for legally obtained self-made disc dumps of games you legally bought. Dolphin was not developed for unlawful use. Act legally as applying laws define. You are responsible for any usage of the emulator that you make. No links, instructions or tips for obtaining illegal content will be provided on this wiki. No copyright infringement intended.

Click on browse to set a directory of ISOs so that they are shown as a library on Dolphin's default screen. Otherwise just click *Open* and select the file.

### Dolphin's Wiki

Whenever a game doesn't work properly, try reading its page on [Dolphin's wiki](https://wiki.dolphin-emu.org). Listed there are tips on setting up the emulator for each game, version compatibility charts, testing entries, troubleshooting and video previews. Contributions, such as testing entries and workarounds are welcome and help other users.

Here's a [xfce4-whiskermenu-plugin](https://www.archlinux.org/packages/?name=xfce4-whiskermenu-plugin) search action command for searching on Dolphin's wiki:

```
exo-open --launch WebBrowser [https://wiki.dolphin-emu.org/index.php?search=%u](https://wiki.dolphin-emu.org/index.php?search=%u)

```

**Tip:** Setting up keymaps is recommended. Prefer a gamepad with analogue features to a keyboard and a mouse. See this [map of the GameCube gamepad](http://upload.wikimedia.org/wikipedia/commons/thumb/3/32/GCController_Layout.svg/1000px-GCController_Layout.svg.png). Having fun while playing is also recommended.

## Troubleshooting

### Incompatibility with Wayland

Dolphin 5.0 is not compatible with Wayland. Force it to run as X11 application via this command:

```
GDK_BACKEND=x11 dolphin-emu

```

### Launching games fails with "WriteRest Op" error

Add "-fno-pie" to "CXX_FLAGS" when building Dolphin.

### Games play too fast

Make sure the framelimit is set to a proper value for the game's region; 60 for NTSC games or 50 for PAL ones. *Auto* is recommended. Avoid playing other media simultaneously with Dolphin.

### Emulation is too slow

Double-check the [CPU scaling governor](/index.php/Cpu_scaling#Scaling_governors "Cpu scaling"). If using an NVidia graphics card, on nvidia-settings changing the powermizer setting to "Prefer maximum performance"; check its temperature to make sure the card does not overheat, though. Change Dolphin's priority using *nice*. Killing unnecessary processes and disabling compositing also helps. Configuring Dolphin correctly, as described above, is the most important part.

Many systems have more than one GPU, like an integrated low-performance one by Intel and a dedicated graphics card. Run `DRI_PRIME=1 dolphin-emu` to execute Dolphin on your dedicated GPU. See [PRIME](/index.php/PRIME "PRIME") for details.

### Games frequently stutter on first playthrough, but subsequent runs are smooth

This stutter is likely introduced because graphics rendering has to pause due to shader compilation. Dolphin has gained advanced techniques for minimizing such stutter, called Ubershaders. They require strong GPUs to work best and thus aren't enabled by default. In the graphics configuration dialog under "Shader Compilation", try one of the options "Synchronous (Ubershaders)" or "Asynchronous (Ubershaders)". Hover over the radio buttons to see a more detailed explanation text in the dialog. Using the option "Compile Shaders Before Starting" may also reduce stutter, but at the cost of a longer delay before the game starts.

*See also: [Improving performance](/index.php/Improving_performance "Improving performance") – most of the advice should be helpful.*

## See also

**Note:** The Arch Linux wiki and its users are not responsible for any damage, misuse or illegal action caused, directly or not, by following instructions from webpages hyperlinked bellow.

*   [Dolphin's performance guide.](https://dolphin-emu.org/docs/guides/performance-guide/)
*   [Dolphin's FAQ](https://dolphin-emu.org/docs/faq/)
*   [Dolphin's wiki entry for legally obtaining game dumps.](https://wiki.dolphin-emu.org/index.php?title=Ripping_Game_Discs)