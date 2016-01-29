# Dolphin emulator

Dolphin is a Nintendo Gamecube, Wii and Triforce emulator, currently supporting the x86, AMD64 and ARM architectures. Dolphin is available for Linux, MacOSX (intel-based), MS Windows and Android. It is a free and open source, community-developed project. Dolphin was the first Gamecube and Wii emulator, and currently the only one capable of playing commercial games.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Config section](#Config_section)
    *   [2.2 Graphics section](#Graphics_section)
    *   [2.3 DSP section](#DSP_section)
*   [3 Playing](#Playing)
    *   [3.1 Dolphin's Wiki](#Dolphin.27s_Wiki)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Launching games fails with "WriteRest Op" error](#Launching_games_fails_with_.22WriteRest_Op.22_error)
    *   [4.2 Games play too fast](#Games_play_too_fast)
    *   [4.3 Emulation is too slow](#Emulation_is_too_slow)
*   [5 See also](#See_also)

## Installation

Install one of the following:

*   **[Dolphin emu](/index.php/Dolphin_emu "Dolphin emu")** — A Gamecube / Wii / Triforce emulator

NaN

*   **Dolphin emu (git)** — A Gamecube / Wii / Triforce emulator (development version)

NaN

**Tip:**

*   Stable releases of Dolphin tend to grow old between releases, and are potentially outclassed by the development versions, which feature many speed improvements and bug fixes in comparison. If low performance or glitches are encountered, consider installing the [dolphin-emu-git](https://aur.archlinux.org/packages/dolphin-emu-git/)<sup><small>AUR</small></sup> package.
*   Reinstalling the [dolphin-emu-git](https://aur.archlinux.org/packages/dolphin-emu-git/)<sup><small>AUR</small></sup> package will upgrade Dolphin to the latest development version at any time.

## Configuration

**Tip:** Run `dolphin-emu -h` for help Dolphin's options.

**Note:** Dolphin may override these settings on a per-game basis, such as when a setting is know to break a certain game. If absolutely sure a specific setting will not crash the game, you can disable or change these overrides by right-clicking the game and selecting _Properties_. Likewise, you can set per-game settings using this method.

While no additional configuration is needed for the emulator to run (it is preconfigured with the default settings), altering the settings can improve performance and graphics alike. Settings are split to three main sections, _Config_, _Graphics_ and _DSP_.

### Config section

**Tip:** Recent versions of Dolphin remove the _Audio_ frameskip option, so _Auto_ is now recommended.

On the General tab, check _Enable Dual Core_ and _Enable Idle Skipping_. The frame limit should be set to "Auto", so that it works with games from all regions. The CPU emulation engine should be left as JIT Recompiler. Only check "Force console as NTSC-J" if intending to play imported Japanese discs.

All options on the "Interface" tab are personal choices.

The Audio tab is the DSP section's screen; setting it up now means there will be no need to do it later. See the [DSP settings paragraph](#DSP_section) below.

The next two tabs are not very important; the Gamecube tab has settings about connected accessories, such as memory cards, and the only remarkable Wii tab option is the "Aspect Ratio" drop-down list. Set it to either 16:9 or 4:3, depending on the display's [aspect ratio](https://en.wikipedia.org/wiki/Aspect_ratio "wikipedia:Aspect ratio").

On the final tab, "Paths", ISO directories can be set. The directory of game ISOs can also be set by clicking browse from the home screen, but here more options are available, such as _Search Subfolders_.

### Graphics section

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** New 3D options available. (Discuss in [Talk:Dolphin emulator#](https://wiki.archlinux.org/index.php/Talk:Dolphin_emulator))

On the "General" tab, choose OpenGL from the backend drop-down list. Set the "Display" and "Other" settings to the desired configuration. V-sync is useful, but it can lead to slowdowns. The "render to main window" option improves the experience aesthetically.

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

**Tip:** Dolphin is able to render games that were developed for 2D in anaglyph 3D. To enable this, set _Post-Processing Effect_ to _stereoscopic_ (default, for red-cyan mode) or _stereoscopic2_ (blue-yellow). It is also **necessary** to uncheck "_Fast Depth Calculation_" on the _Hacks_ tab (_see below_).

**Warning:** Using filters and other ways to improve graphics might break a few games or cause graphical glitches of any level.

Unless sure, the _Hacks_ tab is best left untouched.

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

Similarly, unless sure, leave **everything** in the _Advanced_ tab unchecked.

### DSP section

Set the DSP emulation engine to

*   DSP HLE for speed over accuracy,
*   DSP LLE recompiler for better accuracy with the cost of some speed,
*   DSP LLE interpreter; accurate but makes **everything** unplayable. Too slow.

_DSP LLE on separate thread_ improves speed on computers with multi-core CPUs, but might cause audio glitches, and is known to break [Zelda ucode games](https://wiki.dolphin-emu.org/index.php?title=Category:Zelda_ucode_games). Audio backend is best set to [ALSA](/index.php/ALSA "ALSA"). For `pulseaudio`, Dolphin's optional dependency [PulseAudio](/index.php/PulseAudio "PulseAudio") needs to be installed.

**Note:** If you came here from the [Config section's](#Config_section) link, you should go back now.

## Playing

**Note:** Dolphin is a resource-heavy application, so expect not all games to run properly. See the reason [here](https://dolphin-emu.org/docs/faq/#why-do-i-need-such-powerful-computer-emulate-old-c).

**Warning:** Make sure you **only** use Dolphin for legally obtained self-made disc dumps of games you legally bought. Dolphin was not developed for unlawful use. Act legally as applying laws define. You are responsible for any usage of the emulator that you make. No links, instructions or tips for obtaining illegal content will be provided on this wiki. No copyright infringement intended.

Click on browse to set a directory of ISOs so that they are shown as a library on Dolphin's default screen. Otherwise just click _Open_ and select the file.

### Dolphin's Wiki

Whenever a game doesn't work properly, try reading its page on [Dolphin's wiki](https://wiki.dolphin-emu.org). Listed there are tips on setting up the emulator for each game, version compatibility charts, testing entries, troubleshooting and video previews. Contributions, such as testing entries and workarounds are welcome and help other users.

Here's a [xfce4-whiskermenu-plugin](https://www.archlinux.org/packages/?name=xfce4-whiskermenu-plugin) search action command for searching on Dolphin's wiki:

```
exo-open --launch WebBrowser [https://wiki.dolphin-emu.org/index.php?search=%u](https://wiki.dolphin-emu.org/index.php?search=%u)

```

**Tip:** Setting up keymaps is recommended. Prefer a gamepad with analogue features to a keyboard and a mouse. See this [map of the GameCube gamepad](http://upload.wikimedia.org/wikipedia/commons/thumb/3/32/GCController_Layout.svg/1000px-GCController_Layout.svg.png). Having fun while playing is also recommended.

## Troubleshooting

### Launching games fails with "WriteRest Op" error

Add "-fno-pie" to "CXX_FLAGS" when building Dolphin.

### Games play too fast

Make sure the framelimit is set to a proper value for the game's region; 60 for NTSC games or 50 for PAL ones. _Auto_ is recommended. Avoid playing other media simultaneously with Dolphin.

### Emulation is too slow

Double-check the [CPU scaling governor](/index.php/Cpu_scaling#Scaling_governors "Cpu scaling"). If using an nvidia graphics card, on nvidia-settings changing the powermizer setting to "Prefer maximum performance"; check its temperature to make sure the card does not overheat, though. Change Dolphin's priority using _nice_. Killing unnecessary processes and disabling compositing also helps. Configuring Dolphin correctly, as described above, is the most important part.

_See also: [Maximizing performance](/index.php/Maximizing_performance "Maximizing performance") - most of the advice should be helpful._

## See also

**Note:** The Arch Linux wiki and its users are not responsible for any damage, misuse or illegal action caused, directly or not, by following instructions from webpages hyperlinked bellow.

*   [Dolphin's performance guide.](https://dolphin-emu.org/docs/guides/performance-guide/)
*   [Dolphin's FAQ](https://dolphin-emu.org/docs/faq/)
*   [Dolphin's wiki entry for legally obtaining game dumps.](https://wiki.dolphin-emu.org/index.php?title=Ripping_Game_Discs)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dolphin_emulator&oldid=393045](https://wiki.archlinux.org/index.php?title=Dolphin_emulator&oldid=393045)"