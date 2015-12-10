# Midnight Commander

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

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
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [mc](https://www.archlinux.org/packages/?name=mc) package, or [mc-git](https://aur.archlinux.org/packages/mc-git/)<sup><small>AUR</small></sup> for the development version.

### Skins

*   **mc-solarized-git** — Solarized color scheme for Midnight Commander

[https://github.com/nkulikov/mc-solarized-skin](https://github.com/nkulikov/mc-solarized-skin) || [mc-solarized-git](https://aur.archlinux.org/packages/mc-solarized-git/)<sup><small>AUR</small></sup>

*   **mc-skin-candy** — Candy color scheme (256color)

[candy256.ini](https://raw.githubusercontent.com/izmntuk/archiso/testing/configs/alter/airootfs/usr/share/mc/skins/candy256.ini) ||

See also `**Skins**` in `man mc`.

## Usage

The below section provides a short overview on usage of Midnight commander. References to `man mc` and the Help function (`F1`, available in every dialog) are made in this article as `**Section**`.

**Tip:** All hints are available in `/usr/share/mc/hints/`.

### Interface

In prominent view are two vertical panes. Either can list directory contents, show a plain text preview, file details, or a directory tree (see `**Directory Tree**`). File operations are accessible through the function keys or the mouse. More options are visible in a dynamic user menu (`F2`) and option menu (`F9`). Keys above `F12` (`F13` up to `F20`) are accessible through `Shift`. Menu and dialog options have one letter highlighted - pressing this letter (or `Alt+_Letter_` inside a text entry) directly activates the respective option.

Below, a command line is visible, connected to a subshell. This shell is generally of the same type _mc_ was launched from, and may be switched to at will (`Ctrl-O`), see `**The subshell support**`. On this command line, _cd_ is interpreted by Midnight Commander, and not passed to the shell for execution. As such, special completion (such as from [Zsh](/index.php/Zsh "Zsh")) is unavailable. Files in the pane interact with the command line; for example, `Alt+Enter` copies the name of a (selected) file to the command line.

Keybindings are generally similar to [GNU Emacs](/index.php/GNU_Emacs "GNU Emacs"). A more strict emacs keymap can be enabled (see `**Redefine hotkey bindings**`). New users may however use Lynx-like (arrow) keybindings (enabled in `F9 > Options > Panel options`) and mouse clicks for navigation.

### Modules

These can be called via the _mc_ interface (with _Use internal_ enabled in `F9 > Options > Configuration`), or separately as symbolic links to the _mc_ binary.

*   _mcedit_ - Text and binary file editor, with regex replace, syntax highlighting, macros and shell piping, see `man mcedit`
*   _mcview_ - Text and hex viewer with goto marks and regex search
*   _mcdiff_ - Compares and edits two files in-place (`C-x d`)

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

Install the [libtrash](https://aur.archlinux.org/packages/libtrash/)<sup><small>AUR</small></sup> package, and create an _mc_ alias in the initialization file of your shell (e.g., `~/.bashrc` or `~/.zshrc`):

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

Now files deleted by Midnight Commander (launched with _mc_) will be moved to the `~/.Trash` directory.

**Warning:**

*   Applications launched from _mc_ inherit `LD_PRELOAD`, which may cause problems with some applications. [[1]](http://pages.stern.nyu.edu/~marriaga/software/libtrash/)
*   With `GLOBAL_PROTECTION = YES` set (default), files deleted outside the home directory are moved to the trash, even if they are on a different partition. Depending on the file, this may cause a significant delay.

See also [[2]](https://mail.gnome.org/archives/mc/2010-March/msg00041.html).

## Troubleshooting

### Exit to the current directory

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Check how to get mc-wrapper.sh working (Discuss in [Talk:mc#Wrapper](https://wiki.archlinux.org/index.php/Talk:Mc#Wrapper))

On exit, the shell returns to the directory Midnight Commander was started from, instead of the last active directory. A simple workaround is to switch to the subshell (`Ctrl+o`). This may however interfere with other terminal applications.

### Garbled screen

Press `Ctrl+l` to redraw the display. This only redraws, but does not refresh (`Ctrl+r`) the file list.

### Opening files

_mc_ uses [xdg-open](/index.php/Xdg-open "Xdg-open") to open files by default, as shown in `/usr/lib/mc/ext.d/`. While _stderr_ is redirected, _stdout_ is not, which may result in a garbled screen.

 `/usr/lib/mc/ext.d/*.sh` 

```
[ -n "${MC_XDG_OPEN}" ] || MC_XDG_OPEN="xdg-open"
...
open)
    "${MC_XDG_OPEN}" "${MC_EXT_FILENAME}" **2>/dev/null** || \
        do_open_action "${filetype}"
```

Create a script to wrap _xdg-open_:

 `~/bin/xdg-open-null` 

```
#!/bin/bash
xdg-open "$@" **>/dev/null**

```

If _mc_ is blocked until _xdg-open_ ends, detach the process:

 `~/bin/xdg-open-null` 

```
#!/bin/bash
nohup xdg-open "$@" >/dev/null &

```

and make _mc_ aware of it by setting the `MC_XDG_OPEN` [environment variable](/index.php/Environment_variable "Environment variable"):

```
export MC_XDG_OPEN=~/bin/xdg-open-null

```

**Tip:** When [#Using libtrash](#Using_libtrash), add `unset LD_PRELOAD` before _xdg-open_ in the script.

### Find file shows no results

If the _Find file_ dialog (accessible with `Alt+?`) shows no results, check the current directory for symbolic links. Find file does not follow symbolic links, so use bind mounts (see `man mount`) instead, or the _External panelize_ command.

## See also

*   [man mc(1)](http://linux.die.net/man/1/mc)
*   [Draft of documentation](https://www.midnight-commander.org/wiki/doc)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Midnight_Commander&oldid=410944](https://wiki.archlinux.org/index.php?title=Midnight_Commander&oldid=410944)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [File managers](/index.php/Category:File_managers "Category:File managers")