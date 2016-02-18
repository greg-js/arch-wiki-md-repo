Most mature terminal emulators permit users to copy or save their contents.

## Contents

*   [1 General approach](#General_approach)
    *   [1.1 Terminals without CLIPBOARD selection](#Terminals_without_CLIPBOARD_selection)
    *   [1.2 Intercepting commands’s output](#Intercepting_commands.E2.80.99s_output)
    *   [1.3 Accessing Linux terminal backlog](#Accessing_Linux_terminal_backlog)
*   [2 A cheatsheet for common emulators](#A_cheatsheet_for_common_emulators)
*   [3 Special cases](#Special_cases)
    *   [3.1 putty](#putty)
    *   [3.2 urxvt](#urxvt)
    *   [3.3 xterm](#xterm)

## General approach

In graphical terminal emulators, contents are typically selectable by mouse, and can then be copied using the context menu, *Edit* menu or a key combination such as `Ctrl+Shift+C`.

### Terminals without CLIPBOARD selection

Some emulators do not support the [CLIPBOARD selection](/index.php/Clipboard#Background "Clipboard") natively, and copy data to the PRIMARY selection. For them [xclip](https://www.archlinux.org/packages/?name=xclip) may be used:

```
$ xclip -o | xclip -selection clipboard -i

```

### Intercepting commands’s output

Use *tee* to intercept the output of a command.

```
$ command 2>&1 | tee output-file

```

After the `command` is executed, `output-file` will contain its output.

### Accessing Linux terminal backlog

The backlog of a native terminal named `/dev/ttyN` may be accessed via `/dev/vcsN`. Hence, if one is working in `/dev/tty1`, the following snippet will let store the backlog in a file `output-file`:

```
# cat /dev/vcs1 >output-file

```

## A cheatsheet for common emulators

Until the "Notes" column states otherwise, the keys combination is `Ctrl+Shift+c`.

| Emulator | Selection → CLIPBOARD | Selection → PRIMARY | Keys combination | Context menu → Copy | Window menu → Copy | Notes |
| [aterm](https://aur.archlinux.org/packages/aterm/) | No | Yes | No | No | No |
| [ETerm](https://aur.archlinux.org/packages/ETerm/) | No | Yes | No | No | No |
| [germinal](https://aur.archlinux.org/packages/germinal/) | No | Yes | Yes | Yes | No |
| [guake](/index.php/Guake "Guake") | No | Yes | Yes | Yes | No |
| [Konsole](https://www.archlinux.org/packages/?name=Konsole) | No | No | Yes | Yes | Yes |
| [lilyterm](https://www.archlinux.org/packages/?name=lilyterm) | No | Yes | Yes | Yes | No | `Ctrl+Delete` |
| [lxterminal](https://www.archlinux.org/packages/?name=lxterminal) | No | Yes | Yes | Yes | Yes |
| [mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal) | No | Yes | Yes | Yes | Yes |
| [mlterm](https://aur.archlinux.org/packages/mlterm/) | Yes | Yes | No | No | No |
| [pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal) | No | Yes | Yes | Yes | No |
| [putty](https://www.archlinux.org/packages/?name=putty) | No | Yes | No | No | No |
| [qterminal](https://aur.archlinux.org/packages/qterminal/) | No | Yes | Yes | Yes | Yes |
| [roxterm](https://www.archlinux.org/packages/?name=roxterm) | No | Yes | Yes | Yes | Yes |
| [rxvt](https://www.archlinux.org/packages/?name=rxvt) | No | Yes | No | No | No |
| [sakura](https://www.archlinux.org/packages/?name=sakura) | No | Yes | Yes | Yes | Yes |
| [st](/index.php/St "St") | No | Yes | No | No | No |
| [terminator](/index.php/Terminator "Terminator") | No | Yes | Yes | Yes | No |
| [terminology](https://www.archlinux.org/packages/?name=terminology) | No | Yes | Yes | Yes | No |
| [termite](/index.php/Termite "Termite") | No | Yes | Yes | No | No |
| [tilda](/index.php/Tilda "Tilda") | No | Yes | Yes | Yes | No |
| tinyterm ([tinyterm-git](https://aur.archlinux.org/packages/tinyterm-git/)) | No | Yes | Yes | No | No |
| [urxvt](/index.php/Rxvt-unicode "Rxvt-unicode") | Optional | Yes | Yes | No | No | `Ctrl+Alt+c` |
| XFCE Terminal ([xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal)) | No | Yes | Yes | Yes | Yes |
| [xterm](/index.php/Xterm "Xterm") | Yes | Yes | Optional | No | No | [[1]](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=588785) |
| [yakuake](/index.php/Yakuake "Yakuake") | No | Yes | Yes | Yes | No |

## Special cases

### putty

The [xclip approach](#Terminals_without_CLIPBOARD_selection) works for *putty*: one just has to remember that the *xclip* invocation should be done on the local computer (in another terminal), not on the remote machine to which *putty* is connected.

### urxvt

Selecting text to CLIPBOARD requires the `selection-to-clipboard` perl extension. See [Rxvt-unicode#Cut_and_paste](/index.php/Rxvt-unicode#Cut_and_paste "Rxvt-unicode") for details.

### xterm

Access to the CLIPBOARD selection in *xterm* requires [additional steps](/index.php/Xterm#PRIMARY_or_CLIPBOARD "Xterm").