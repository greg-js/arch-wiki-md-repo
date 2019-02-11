[GNU nano](https://www.nano-editor.org/) (or nano) is a text editor which aims to introduce a simple interface and intuitive command options to console based text editing. *nano* supports features including colorized syntax highlighting, DOS/Mac file type conversions, spellchecking and [UTF-8](https://en.wikipedia.org/wiki/UTF-8 "wikipedia:UTF-8") encoding. *nano* opened with an empty buffer typically occupies under 4 MB of resident memory.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Syntax highlighting](#Syntax_highlighting)
        *   [2.1.1 PKGBUILD](#PKGBUILD)
    *   [2.2 Suspension](#Suspension)
    *   [2.3 Text wrapping](#Text_wrapping)
*   [3 Usage](#Usage)
    *   [3.1 Special functions](#Special_functions)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Replacing vi with nano](#Replacing_vi_with_nano)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Hijacked keybindings](#Hijacked_keybindings)
*   [6 See also](#See_also)

## Installation

*nano* is available in the [nano](https://www.archlinux.org/packages/?name=nano) package. It is likely that is already on your system, as it is included in the [base](https://www.archlinux.org/groups/x86_64/base/) group.

## Configuration

The look, feel, and function of nano is typically controlled by way of either command-line arguments, or configuration commands within the file `~/.config/nano/nanorc`.

A sample configuration file is installed upon program installation and is located at `/etc/nanorc`. To customize your nano configuration, first create a local copy at `~/.config/nano/nanorc`:

```
$ cp /etc/nanorc ~/.config/nano/nanorc

```

Proceed to establish the nano console environment by setting and/or unsetting commands within `~/.config/nano/nanorc` file.

**Tip:** [nanorc(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nanorc.5) details the complete list configuration commands available for nano.

**Note:** Command-line arguments override and take precedence over the configuration commands established in `~/.config/nano/nanorc`

### Syntax highlighting

Nano ships with predefined [syntax highlighting](https://en.wikipedia.org/wiki/Syntax_highlighting "wikipedia:Syntax highlighting") rules, defined in `/usr/share/nano/*.nanorc`. To enable them, add the following line to your `~/.config/nano/nanorc` or to `/etc/nanorc`:

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

Unlike most interactive programs, suspension is not enabled by default. To change this, uncomment the `set suspend` line in `/etc/nanorc`. This will allow you to use the keys `Ctrl+z` to send nano to the background.

### Text wrapping

Unlike many text editors, *nano* wraps text. To disable this put this in your `~/.config/nano/nanorc`

```
set nowrap

```

## Usage

Shortcuts can be viewed from inside *nano*. See the nano online help files via `Ctrl+g` within nano and the [nano Command Manual](https://www.nano-editor.org/dist/latest/nano.html) for complete descriptions and additional support.

### Special functions

Keyboard shortcuts representing commonly used functions are listed along the bottom two lines of the nano screen.

They can be toggled by:

*   `Ctrl` for `^` based shortcuts
*   *`Meta`* (typically `Alt`) or `Esc` for `M-` based shortcuts

**Tip:** [Feature Toggles](https://www.nano-editor.org/dist/latest/nano.html#Feature-Toggles) lists the global toggles available for nano.

## Tips and tricks

### Replacing vi with nano

To replace vi with nano as the default text editor for commands such as [visudo](/index.php/Sudo#Using_visudo "Sudo"), set the `VISUAL` and `EDITOR` [environment variables](/index.php/Environment_variable#Defining_variables "Environment variable"), for example:

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
*   [Improved Nano Syntax Highlighting Files](https://github.com/scopatz/nanorc)