Most mature terminal emulators permit users to copy or save their contents.

## Contents

*   [1 General approach](#General_approach)
    *   [1.1 Terminals without CLIPBOARD selection](#Terminals_without_CLIPBOARD_selection)
    *   [1.2 Intercepting commands’s output](#Intercepting_commands.E2.80.99s_output)
    *   [1.3 Accessing Linux terminal backlog](#Accessing_Linux_terminal_backlog)
*   [2 Comparison of common emulators](#Comparison_of_common_emulators)
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

Other [clipboard managers](/index.php/Clipboard_manager "Clipboard manager") such as [autocutsel](https://www.archlinux.org/packages/?name=autocutsel) provide automatic synchronization between selection buffers.

### Intercepting commands’s output

Use [tee](https://en.wikipedia.org/wiki/Tee_(command)) to intercept the output of a command.

```
$ command 2>&1 | tee output-file

```

After the `command` is executed, `output-file` will contain its output.

### Accessing Linux terminal backlog

The backlog of a native terminal named `/dev/ttyN` may be accessed via `/dev/vcsN`. Hence, if one is working in `/dev/tty1`, the following snippet will let store the backlog in a file `output-file`:

```
# cat /dev/vcs1 >output-file

```

## Comparison of common emulators

Unless the *Key combination* column states otherwise, the key combination is `Ctrl+Shift+c`.

| Emulator | Select to PRIMARY | CLIPBOARD |
| Key combination | Context menu | Window menu | Select |
| [aterm](https://aur.archlinux.org/packages/aterm/) | Yes | No | No | No | No |
| [eterm](https://aur.archlinux.org/packages/eterm/) | Yes | No | No | No | No |
| [germinal](https://aur.archlinux.org/packages/germinal/) | Yes | Yes | Yes | No | No |
| [Guake](/index.php/Guake "Guake") | Yes | Yes | Yes | No | No |
| [konsole](https://www.archlinux.org/packages/?name=konsole) | Yes | Yes | Yes | Yes | Optional |
| [lilyterm-git](https://aur.archlinux.org/packages/lilyterm-git/) | Yes | Yes `Ctrl+Delete` | Yes | No | No |
| [lxterminal](https://www.archlinux.org/packages/?name=lxterminal) | Yes | Yes | Yes | Yes | No |
| [mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal) | Yes | Yes | Yes | Yes | No |
| [mlterm](https://aur.archlinux.org/packages/mlterm/) | Yes | No | No | No | Yes |
| [pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal) | Yes | Yes | Yes | No | No |
| [PuTTY](/index.php/PuTTY "PuTTY") | Yes | No | No | No | No |
| [qterminal](https://www.archlinux.org/packages/?name=qterminal) | Yes | Yes | Yes | Yes | No |
| [roxterm](https://aur.archlinux.org/packages/roxterm/) | Yes | Yes | Yes | Yes | No |
| [rxvt](https://aur.archlinux.org/packages/rxvt/) | Yes | No | No | No | No |
| [sakura](https://www.archlinux.org/packages/?name=sakura) | Yes | Yes | Yes | Yes | No |
| [st](/index.php/St "St") | Yes | Yes | No | No | No |
| [Terminator](/index.php/Terminator "Terminator") | Yes | Yes | Yes | No | No |
| [terminology](https://www.archlinux.org/packages/?name=terminology) | Yes | Yes | Yes | No | No |
| [Termite](/index.php/Termite "Termite") | Yes | Yes | No | No | No |
| [Tilda](/index.php/Tilda "Tilda") | Yes | Yes | Yes | No | No |
| [tinyterm-git](https://aur.archlinux.org/packages/tinyterm-git/) | Yes | Yes | No | No | No |
| [urxvt](/index.php/Urxvt "Urxvt") | Yes | Yes `Ctrl+Alt+c` | No | No | Optional |
| [xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal) | Yes | Yes | Yes | Yes | No |
| [xterm](/index.php/Xterm "Xterm") | Yes | Optional[[1]](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=588785) | No | No | Yes |
| [Yakuake](/index.php/Yakuake "Yakuake") | Yes | Yes | Yes | No | Optional |

## Special cases

### putty

The [xclip approach](#Terminals_without_CLIPBOARD_selection) works for *putty*: one just has to remember that the *xclip* invocation should be done on the local computer (in another terminal), not on the remote machine to which *putty* is connected.

### urxvt

Selecting text to CLIPBOARD requires the `selection-to-clipboard` perl extension. See [Rxvt-unicode#Cut and paste](/index.php/Rxvt-unicode#Cut_and_paste "Rxvt-unicode") for details.

### xterm

Access to the CLIPBOARD selection in *xterm* requires [additional steps](/index.php/Xterm#PRIMARY_or_CLIPBOARD "Xterm").