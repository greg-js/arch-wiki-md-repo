Related articles

*   [File manager functionality](/index.php/File_manager_functionality "File manager functionality")
*   [ranger](/index.php/Ranger "Ranger")

[Midnight Commander](https://en.wikipedia.org/wiki/Midnight_Commander "wikipedia:Midnight Commander") is an orthodox (two-pane) file manager, supporting standard file operations, virtual filesystems, panelizing of external commands, and user menus. It also includes an internal viewer, editor, and visual diff tool.

As it is based on versatile text interfaces, such as Ncurses or S-Lang, it works on a regular console, inside an X Window terminal, over [SSH](/index.php/SSH "SSH") connections and all kinds of remote shells.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Skins](#Skins)
*   [2 Usage](#Usage)
    *   [2.1 Interface](#Interface)
    *   [2.2 Modules](#Modules)
*   [3 Configuration](#Configuration)
    *   [3.1 extfs](#extfs)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Start from the menu](#Start_from_the_menu)
    *   [4.2 Trash support](#Trash_support)
        *   [4.2.1 Using libtrash](#Using_libtrash)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Exit to the current directory](#Exit_to_the_current_directory)
    *   [5.2 Garbled screen](#Garbled_screen)
    *   [5.3 Opening files](#Opening_files)
    *   [5.4 Find file shows no results](#Find_file_shows_no_results)
    *   [5.5 Broken shortcuts](#Broken_shortcuts)
    *   [5.6 No bold text in urxvt](#No_bold_text_in_urxvt)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [mc](https://www.archlinux.org/packages/?name=mc) package, or [mc-git](https://aur.archlinux.org/packages/mc-git/) for the development version.

### Skins

*   **mc-solarized-git** — Solarized color scheme for Midnight Commander

	[https://github.com/nkulikov/mc-solarized-skin](https://github.com/nkulikov/mc-solarized-skin) || [mc-solarized-git](https://aur.archlinux.org/packages/mc-solarized-git/)

*   **mc-skin-modarin-debian** — Thin versions of the modarin theme

	[https://launchpad.net/debian/+source/mc/3:4.8.13-3](https://launchpad.net/debian/+source/mc/3:4.8.13-3) || [mc-skin-modarin-debian](https://aur.archlinux.org/packages/mc-skin-modarin-debian/)

*   **mc-skin-candy** — Candy color scheme (256color)

	[candy256.ini](https://raw.githubusercontent.com/izmntuk/archiso/testing/configs/alter/airootfs/usr/share/mc/skins/candy256.ini) ||

See also `**Skins**` in mc(1).

## Usage

The below section provides a short overview on usage of Midnight commander. References to mc(1) and the Help function (`F1`, available in every dialog) are made in this article as `**Section**`.

**Tip:** All hints are available in `/usr/share/mc/hints/`.

### Interface

In prominent view are two vertical panes. Either can list directory contents, show a plain text preview, file details, or a directory tree (see `**Directory Tree**`). File operations are accessible through the function keys or the mouse. More options are visible in a dynamic user menu (`F2`) and option menu (`F9`). Keys above `F12` (`F13` up to `F20`) are accessible through `Shift`. Menu and dialog options have one letter highlighted - pressing this letter (or `Alt+*Letter*` inside a text entry) directly activates the respective option.

Below, a command line is visible, connected to a subshell. This shell is generally of the same type *mc* was launched from, and may be switched to at will (`Ctrl-O`), see `**The subshell support**`. On this command line, *cd* is interpreted by Midnight Commander, and not passed to the shell for execution. As such, special completion (such as from [Zsh](/index.php/Zsh "Zsh")) is unavailable. Files in the pane interact with the command line; for example, `Alt+Enter` copies the name of a (selected) file to the command line.

Keybindings are generally similar to [GNU Emacs](/index.php/GNU_Emacs "GNU Emacs"). A more strict emacs keymap can be enabled (see `**Redefine hotkey bindings**`). New users may however use Lynx-like (arrow) keybindings (enabled in `F9 > Options > Panel options`) and mouse clicks for navigation.

### Modules

These can be called via the *mc* interface (with *Use internal* enabled in `F9 > Options > Configuration`), or separately as symbolic links to the *mc* binary.

*   *mcedit* - Text and binary file editor, with regex replace, syntax highlighting, macros and shell piping, see [mcedit(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mcedit.1)
*   *mcview* - Text and hex viewer with goto marks and regex search
*   *mcdiff* - Compares and edits two files in-place (`C-x d`)

Per `mc` instance, multiple modules can be run concurrently (`Ctrl-``) (see `**Screen selector**`). External editors may be used instead, and parameters configured accordingly.

## Configuration

Most of the Midnight Commander settings can be changed from the menus. However, a small number of settings such as clipboard commands, codeset detection and parameters for external editors can only be changed from `~/.config/mc/ini`. See `**Special Settings**` and following for a complete description of options.

Additionally, the following environment variables are respected: `MC_SKIN`, `MC_KEYMAP`, `MC_XDG_OPEN`, `MC_COLOR_TABLE`, `MC_DATADIR`, `MC_HOME`, `KEYBOARD_KEY_TIMEOUT_US`, `PAGER`, `EDITOR`, `VIEWER`.

See also `**Files**`.

### extfs

extfs allows to easily create new virtual filesystems for mc. See `/usr/lib/mc/extfs.d/README` for details.

## Tips and tricks

### Start from the menu

Midnight commander can be run from a menu with the correct [Desktop entry](/index.php/Desktop_entry "Desktop entry"). For example:

```
[Desktop Entry]
Type=Application
Version=1.0
Name=Midnight Commander
Comment=Visual file manager
Exec=mc
Icon=folder
MimeType=inode/directory
Terminal=true
Categories=Utility;

```

### Trash support

Midnight Commander does [not support](https://www.midnight-commander.org/ticket/3072) a trash can by default.

#### Using libtrash

Install the [libtrash](https://aur.archlinux.org/packages/libtrash/) package, and create an *mc* alias in the initialization file of your shell (e.g., `~/.bashrc` or `~/.zshrc`):

```
alias mc='LD_PRELOAD=/usr/lib/libtrash.so.3.3 mc'

```

To apply the changes, reopen your shell session or `source` the shell initialization file.

Default settings are defined in `/etc/libtrash.conf.sys`. You can overwrite these settings per-user in `~/.libtrash`, for example:

```
TRASH_CAN = .Trash
INTERCEPT_RENAME = NO
IGNORE_EXTENSIONS= o;exe;com
UNCOVER_DIRS=/dev

```

Now files deleted by Midnight Commander (launched with *mc*) will be moved to the `~/.Trash` directory.

**Warning:**

*   Applications launched from *mc* inherit `LD_PRELOAD`, which may cause problems with some applications. [[1]](http://pages.stern.nyu.edu/~marriaga/software/libtrash/)
*   With `GLOBAL_PROTECTION = YES` set (default), files deleted outside the home directory are moved to the trash, even if they are on a different partition. Depending on the file, this may cause a significant delay.

See also [[2]](https://mail.gnome.org/archives/mc/2010-March/msg00041.html).

## Troubleshooting

### Exit to the current directory

On exit, the shell returns to the directory Midnight Commander was started from, instead of the last active directory. A wrapper script is included, which can be used by adding this line to your `~/.bashrc` or `~/.zshrc`:

```
source /usr/lib/mc/mc.sh

```

This will alias `mc` to the wrapper script.

Another simple workaround is to use the subshell (`Ctrl+o`). This may however interfere with other terminal applications.

### Garbled screen

Press `Ctrl+l` to redraw the display. This only redraws, but does not refresh (`Ctrl+r`) the file list.

### Opening files

*mc* reads the `MC_XDG_OPEN` [environment variable](/index.php/Environment_variable "Environment variable") to open files, which defaults to [xdg-open](/index.php/Xdg-open "Xdg-open") when unset. [[3]](https://github.com/MidnightCommander/mc/blob/master/misc/ext.d/misc.sh.in)

if *mc* is blocked until the resulting process ends, or the process exits together with mc, use `nohup &`:

 `~/bin/nohup-open` 
```
#!/bin/bash
**nohup** xdg-open "$@" **&**

```

and set `MC_XDG_OPEN` accordingly:

```
export MC_XDG_OPEN=~/bin/nohup-open

```

**Tip:** When [#Using libtrash](#Using_libtrash), add `unset LD_PRELOAD` before *xdg-open* in the script.

### Find file shows no results

If the *Find file* dialog (accessible with `Alt+?`) shows no results, check the current directory for symbolic links. *Find file* does not follow symbolic links, so use bind mounts (see [mount(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8)) instead, or the *External panelize* command.

### Broken shortcuts

With certain terminal definitions such as `screen-256color` or `xterm-termite`, shortcuts such as `Shift+F6` may not work or act as different combinations. To remedy his, assign the terminal sequences manually with the `**Learn keys**` dialog.

Settings will be stored in the `~/.config/mc/ini` file, for example for `screen-256color`:

**Note:** The following example assumes F13–F20 are bound to `Shift+F3`–`Shift+F10`.

```
[terminal:screen-256color]
f1=\\eOP
f2=\\eOQ
f3=\\eOR
f4=\\eOS
f5=\\e[15~
f6=\\e[17~
f7=\\e[18~
f8=\\e[19~
f9=\\e[20~
f10=\\e[21~
f11=\\e[23~
f12=\\e[24~
f13=\\e[1\;2R
f14=\\e[1\;2S
f15=\\e[15\;2~
f16=\\e[17\;2~
f17=\\e[18\;2~
f18=\\e[19\;2~
f19=\\e[20\;2~
f20=\\e[21\;2~
complete=\\e^i
backtab=\\e[Z
backspace=^?
```

### No bold text in urxvt

If started under [urxvt](/index.php/Urxvt "Urxvt") with the default `TERM` setting, text that is usually bold in many other terminals will not appear so. The root of the issue is because xterm couples bright text color with the bold attribute (thus, bright colors will always appear as bold in xterm).

urxvt does not have this limitation, which Slang (the library mc uses for text display by default) honors. Because Slang can decouple the bold attribute from bright colors on urxvt, mc would need to explicitly specify the bold attribute as appropriate ([which it does not](https://bugzilla.redhat.com/show_bug.cgi?id=474108#c3)).

The solution is to configure mc to explicitly use bold colors as desired, e.g. by editing the default skin as follows:

```
mkdir ~/.local/share/mc/skins 
cp /usr/share/mc/skins/default.ini ~/.local/share/mc/skins/
sed -i -E 's/^(.* = (gray|brightred|brightgreen|yellow|brightblue|brightmagenta|brightcyan|white);.*)$/\0;bold/' ~/.local/share/mc/skins/default.ini

```

The above will create a copy of the default skin, but with all bright colors having an explicit bold attribute added.

Another common workaround is to set `TERM=xterm`, however this causes other issues due to mismatching termcap/terminfo, such as certain keys not working.

## See also

*   [man mc(1)](https://linux.die.net/man/1/mc)
*   [Draft of documentation](https://www.midnight-commander.org/wiki/doc)