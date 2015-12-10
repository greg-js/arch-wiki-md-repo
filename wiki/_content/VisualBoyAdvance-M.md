# VisualBoyAdvance-M

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**VisualBoyAdvance-M** (commonly abbreviated as **VBA-M**) is a cross-platform emulator for the (Super-) Game Boy/Colour/Advance portable game consoles.

It is a fork of VisualBoyAdvance, a now closed project. VBA-M combines features from several other VBA forks. It is licensed under the GPLv2, and is available in the Community repository.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 OpenGL crashes](#OpenGL_crashes)
    *   [3.2 Directories randomly reverted](#Directories_randomly_reverted)

## Installation

*   **VBA-M (GTK)** — Nintendo GameBoy Advance emulator - GTK version

[http://vba-m.com/](http://vba-m.com/) || [vbam-gtk](https://www.archlinux.org/packages/?name=vbam-gtk)

*   **VBA-M (wx)** — Nintendo GameBoy Advance emulator - wx version

[http://vba-m.com/](http://vba-m.com/) || [vbam-wx](https://www.archlinux.org/packages/?name=vbam-wx)

*   **VBA-M (SDL)** — Nintendo GameBoy Advance emulator - SDL version

[http://vba-m.com/](http://vba-m.com/) || [vbam-sdl](https://www.archlinux.org/packages/?name=vbam-sdl)

*   **VBA-M (GTK) (development version)** — Gameboy Advance Emulator combining features of all VBA forks - GTK GUI - SVN version

[http://vba-m.com/](http://vba-m.com/) || [vbam-gtk-svn](https://aur.archlinux.org/packages/vbam-gtk-svn/)<sup><small>AUR</small></sup>

*   **VBA-M (wx) (development version)** — Improved (Super) Game Boy Color/Advance emulator - wxWidgets GUI, SVN version

[http://vba-m.com/](http://vba-m.com/) || [vbam-wx-svn](https://aur.archlinux.org/packages/vbam-wx-svn/)<sup><small>AUR</small></sup>

## Usage

For VBA-M, execute `gvbam ~/path/to/foo.*` or `gvbam` to load the ROM from the interface.

**Tip:** File extensions differ between emulated platforms. VBA-M also supports compressed ROMs.

<table class="wikitable"><caption>Default controls</caption>

<tbody>

<tr>

<th>Emulated</th>

<th>Real</th>

</tr>

<tr>

<td>Left</td>

<td>Left Arrow (0114)</td>

</tr>

<tr>

<td>Right</td>

<td>Right Arrow (0113)</td>

</tr>

<tr>

<td>Up</td>

<td>Up Arrow (0111)</td>

</tr>

<tr>

<td>Down</td>

<td>Down Arrow (0112)</td>

</tr>

<tr>

<td>A</td>

<td>Z (007a)</td>

</tr>

<tr>

<td>B</td>

<td>X (0078)</td>

</tr>

<tr>

<td>L</td>

<td>A (0061)</td>

</tr>

<tr>

<td>R</td>

<td>S (0073)</td>

</tr>

<tr>

<td>Start</td>

<td>Enter (000d)</td>

</tr>

<tr>

<td>Select</td>

<td>Backspace (0008)</td>

</tr>

<tr>

<td>Speed up</td>

<td>Space (0020)</td>

</tr>

<tr>

<td>Capture</td>

<td>F12 (0125)</td>

</tr>

</tbody>

</table>

## Troubleshooting

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Old advice needs to be verified as still useful, if it is to be kept. (Discuss in [Talk:VisualBoyAdvance-M#Please try to reproduce the problems described in Troubleshooting](https://wiki.archlinux.org/index.php/Talk:VisualBoyAdvance-M#Please_try_to_reproduce_the_problems_described_in_Troubleshooting))

### OpenGL crashes

In case of OpenGL errors, it is possible that the video output is set to an invalid display. Editing the `Display` section in `~/.config/gvbam/config`, and changing `output=1` to `output=2` or `output=0`

### Directories randomly reverted

VBA may randomly revert the ROM directories to the defaults. Changing permissions for `~/.config/gvbam/config` to read-only will prevent VBA from doing so.

**Warning:** This also prevents any other configuration from being saved.

To manually set the directories, edit the `[Directories]` section of `~/.config/gvbam/config`.

```
[Directories]
gb_roms=
gba_roms=
batteries=
cheats=
saves=
captures=

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=VisualBoyAdvance-M&oldid=377161](https://wiki.archlinux.org/index.php?title=VisualBoyAdvance-M&oldid=377161)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Gaming](/index.php/Category:Gaming "Category:Gaming")
*   [Emulators](/index.php/Category:Emulators "Category:Emulators")