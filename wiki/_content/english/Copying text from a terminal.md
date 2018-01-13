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

The above command reads data from the PRIMARY selection and writes it to CLIPBOARD selection.

Other [clipboard managers](/index.php/Clipboard#List_of_clipboard_managers "Clipboard") such as [autocutsel](https://www.archlinux.org/packages/?name=autocutsel) provide automatic synchronization between selection buffers.

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

Unless the "Notes" column states otherwise, the keys combination is `Ctrl+Shift+c`.

| Emulator | Selection → PRIMARY | Selection → CLIPBOARD |
| Automatic | Keys combination | Context menu → Copy | Window menu → Copy | Notes |
| [aterm](https://aur.archlinux.org/packages/aterm/) | Yes | No | No | No | No |
| [ETerm](https://aur.archlinux.org/packages/ETerm/) | Yes | No | No | No | No |
| [germinal](https://aur.archlinux.org/packages/germinal/) | Yes | No | Yes | Yes | No |
| [guake](/index.php/Guake "Guake") | Yes | No | Yes | Yes | No |
| [konsole](https://www.archlinux.org/packages/?name=konsole) | Yes | No | Yes | Yes | Yes |
| [lilyterm](https://www.archlinux.org/packages/?name=lilyterm) | Yes | No | Yes | Yes | No | `Ctrl+Delete` |
| [lxterminal](https://www.archlinux.org/packages/?name=lxterminal) | Yes | No | Yes | Yes | Yes |
| [mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal) | Yes | No | Yes | Yes | Yes |
| [mlterm](https://aur.archlinux.org/packages/mlterm/) | Yes | Yes | No | No | No |
| [pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal) | Yes | No | Yes | Yes | No |
| [putty](https://www.archlinux.org/packages/?name=putty) | Yes | No | No | No | No |
| [qterminal](https://www.archlinux.org/packages/?name=qterminal) | Yes | No | Yes | Yes | Yes |
| [roxterm](https://aur.archlinux.org/packages/roxterm/) | Yes | No | Yes | Yes | Yes |
| [rxvt](https://aur.archlinux.org/packages/rxvt/) | Yes | No | No | No | No |
| [sakura](https://www.archlinux.org/packages/?name=sakura) | Yes | No | Yes | Yes | Yes |
| [st](/index.php/St "St") | Yes | No | No | No | No |
| [terminator](/index.php/Terminator "Terminator") | Yes | No | Yes | Yes | No |
| [terminology](https://www.archlinux.org/packages/?name=terminology) | Yes | No | Yes | Yes | No |
| [termite](/index.php/Termite "Termite") | Yes | No | Yes | No | No |
| [tilda](/index.php/Tilda "Tilda") | Yes | No | Yes | Yes | No |
| [tinyterm-git](https://aur.archlinux.org/packages/tinyterm-git/) | Yes | No | Yes | No | No |
| [urxvt](/index.php/Urxvt "Urxvt") | Yes | Optional | Yes | No | No | `Ctrl+Alt+c` |
| [xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal) | Yes | No | Yes | Yes | Yes |
| [xterm](/index.php/Xterm "Xterm") | Yes | Yes | Optional | No | No | [[1]](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=588785) |
| [yakuake](/index.php/Yakuake "Yakuake") | Yes | No | Yes | Yes | No |

## Special cases

### putty

The [xclip approach](#Terminals_without_CLIPBOARD_selection) works for *putty*: one just has to remember that the *xclip* invocation should be done on the local computer (in another terminal), not on the remote machine to which *putty* is connected.

### urxvt

Selecting text to CLIPBOARD requires the `selection-to-clipboard` perl extension. See [Rxvt-unicode#Cut and paste](/index.php/Rxvt-unicode#Cut_and_paste "Rxvt-unicode") for details.

### xterm

Access to the CLIPBOARD selection in *xterm* requires [additional steps](/index.php/Xterm#PRIMARY_or_CLIPBOARD "Xterm").