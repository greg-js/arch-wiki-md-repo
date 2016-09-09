[GNU nano](https://www.nano-editor.org/) (or nano) is a text editor which aims to introduce a simple interface and intuitive command options to console based text editing. *nano* supports features including colorized syntax highlighting, DOS/Mac file type conversions, spellchecking and [UTF-8](https://en.wikipedia.org/wiki/UTF-8 "wikipedia:UTF-8") encoding. *nano* opened with an empty buffer typically occupies under 1.5 MB of resident memory.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Syntax highlighting](#Syntax_highlighting)
        *   [2.1.1 PKGBUILD](#PKGBUILD)
    *   [2.2 Suspension](#Suspension)
    *   [2.3 Text wrapping](#Text_wrapping)
*   [3 Usage](#Usage)
    *   [3.1 Special functions](#Special_functions)
        *   [3.1.1 Shortcut lists overview](#Shortcut_lists_overview)
        *   [3.1.2 Selected toggle functions](#Selected_toggle_functions)
*   [4 Tips & tricks](#Tips_.26_tricks)
    *   [4.1 Replacing vi with nano](#Replacing_vi_with_nano)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Hijacked keybindings](#Hijacked_keybindings)
*   [6 See also](#See_also)

## Installation

*nano* is available in the [nano](https://www.archlinux.org/packages/?name=nano) package. It is likely that is already on your system, as it is included in the [base](https://www.archlinux.org/groups/x86_64/base/) group.

## Configuration

The look, feel, and function of nano is typically controlled by way of either command-line arguments, or configuration commands within the file `~/.nanorc`.

A sample configuration file is installed upon program installation and is located at `/etc/nanorc`. To customize your nano configuration, first create a local copy at `~/.nanorc`:

```
$ cp /etc/nanorc ~/.nanorc

```

Proceed to establish the nano console environment by setting and/or unsetting commands within `~/.nanorc` file.

**Tip:** [nanorc(5)](https://www.nano-editor.org/dist/latest/nanorc.5.html) details the complete list configuration commands available for nano.

**Note:** Command-line arguments override and take precedence over the configuration commands established in `~/.nanorc`

### Syntax highlighting

**Nano** ships with predefined [syntax highlighting](https://en.wikipedia.org/wiki/Syntax_highlighting "wikipedia:Syntax highlighting") rules, defined in `/usr/share/nano/*.nanorc`. To enable them, add the following line to your `~/.nanorc` or to `/etc/nanorc`:

```
include "/usr/share/nano/*.nanorc"

```

Syntax highlighting enhancements which replace and expand the defaults can be found in the AUR, [nano-syntax-highlighting-git](https://aur.archlinux.org/packages/nano-syntax-highlighting-git/). See [[1]](https://paste.xinu.at/wc17YG/) for [Forth](https://en.wikipedia.org/wiki/Forth_(programming_language) "w:Forth (programming language)") highlighting.

#### PKGBUILD

*   Save [https://paste.xinu.at/4ss/](https://paste.xinu.at/4ss/) (similar to [svntogit-server](https://projects.archlinux.org/svntogit/packages.git/tree)) to `/etc/nano/pkgbuild.nanorc` and include it:

```
include "/etc/nano/pkgbuild.nanorc"

```

*   [nano-syntax-highlighting-git](https://aur.archlinux.org/packages/nano-syntax-highlighting-git/) has an alternate version

### Suspension

Unlike most interactive programs, suspension is not enabled by default. To change this, uncomment the 'set suspend' line in `/etc/nanorc`. This will allow you to use the keys `Ctrl+z` to send nano to the background.

### Text wrapping

Unlike many text editors, *nano* wraps text. To disable this put this in your `~/.nanorc`

```
set nowrap

```

## Usage

### Special functions

*   `Ctrl` key modified shortcuts (`^`) representing commonly used functions are listed along the bottom two lines of the nano screen.
*   Additional functions can be interactively toggled by way of `Meta` (typically `Alt`) and/or `Esc` key modified sequences.

#### Shortcut lists overview

| Key1 | Key2 | Command | Description |
| ^G | F1 | Get Help | Displays the online help files within the session window. A suggested read for nano users of all levels |
| ^X | F2 | Exit | Close and exit nano |
| ^O | F3 | WriteOut | Save the contents of the current file buffer to a file on the disk |
| ^J | F4 | Justify | Aligns text according to the geometry of the console window |
| ^R | F5 | Read File | Inserts another file into the current one at the cursor location |
| ^W | F6 | Where | Perform a case-insensitive string, or regular expression search |
| ^Y | F7 | Prev Page | Display the previous buffered screen |
| ^V | F8 | Next Page | Display the next buffered screen |
| ^K | F9 | Cut Text | Cut and store the current line from the beginning of the line to the end of the line |
| ^U | F10 | UnCut Text | Paste the contents of the cut buffer to the current cursor location |
| ^C | F11 | Cur Pos | Display line, column and character position information at the current location of the cursor |
| ^T | F12 | To Spell | Spellcheck the contents of the buffer with the built-in `spell`, if available |

**Tip:** See the nano online help files via `Ctrl+g` within nano and the [nano Command Manual](https://www.nano-editor.org/dist/latest/nano.html) for complete descriptions and additional support.

#### Selected toggle functions

| Key1 | Key2 | Description |
| Meta+c | Esc+c | Toggles support for line, column and character position information |
| Meta+i | Esc+i | Toggles support for the auto indentation of lines |
| Meta+k | Esc+k | Toggles support for cutting text from the current cursor position to the end of the line |
| Meta+m | Esc+m | Toggles mouse support for cursor placement, marking and shortcut execution |
| Meta+x | Esc+x | Toggles the display of the shortcut list at the bottom of the nano screen for additional screen space |

**Tip:** [Feature Toggles](https://www.nano-editor.org/dist/latest/nano.html#Feature-Toggles) lists the global toggles available for nano.

## Tips & tricks

### Replacing vi with nano

Casual users may prefer to use `nano` over `vi` for its simplicity and ease of use, and may opt to replace vi with nano as the default text editor for commands such as [visudo](/index.php/Sudo#Using_visudo "Sudo").

Setting the `VISUAL` and `EDITOR` [environment variables](/index.php/Environment_variable#Defining_variables "Environment variable") will work for many applications, for example:

```
export VISUAL=nano
export EDITOR=nano

```

## Troubleshooting

### Hijacked keybindings

Some window managers have keybindings that conflict with nano, for example `Alt+Enter`. Remove or remap them to e.g `Super` (with [dconf](https://www.archlinux.org/packages/?name=dconf) for [mutter](https://www.archlinux.org/packages/?name=mutter), [muffin](https://www.archlinux.org/packages/?name=muffin) and [marco](https://www.archlinux.org/packages/?name=marco)) and restart the window manager.

## See also

*   [nano (text editor)](https://en.wikipedia.org/wiki/Nano_(text_editor) - Wikipedia Entry
*   [GNU nano Homepage](https://www.nano-editor.org/) - Official Site
*   [GNU nano Bugs](https://savannah.gnu.org/bugs/?group=nano) Bug Reporting
*   [Better syntax highlighting definitions](https://github.com/craigbarnes/nanorc)