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

## Usage

For VBA-M, execute `gvbam ~/path/to/foo.*` or `gvbam` to load the ROM from the interface.

**Tip:** File extensions differ between emulated platforms. VBA-M also supports compressed ROMs.

<caption>Default controls</caption>
| Emulated | Real |
| Left | Left Arrow (0114) |
| Right | Right Arrow (0113) |
| Up | Up Arrow (0111) |
| Down | Down Arrow (0112) |
| A | Z (007a) |
| B | X (0078) |
| L | A (0061) |
| R | S (0073) |
| Start | Enter (000d) |
| Select | Backspace (0008) |
| Speed up | Space (0020) |
| Capture | F12 (0125) |

## Troubleshooting

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