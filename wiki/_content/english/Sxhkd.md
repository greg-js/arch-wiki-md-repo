Related articles

*   [Xbindkeys](/index.php/Xbindkeys "Xbindkeys")
*   [Xmodmap](/index.php/Xmodmap "Xmodmap")

From [sxhkd's Github page](https://github.com/baskerville/sxhkd):

	*sxhkd is a simple X hotkey daemon with a powerful and compact configuration syntax.*

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Sxhkd Config File](#Sxhkd_Config_File)
    *   [2.2 Systemd Service File](#Systemd_Service_File)
*   [3 Usage](#Usage)
*   [4 Example](#Example)
*   [5 See Also](#See_Also)

## Installation

[Install](/index.php/Install "Install") [sxhkd](https://www.archlinux.org/packages/?name=sxhkd) or [sxhkd-git](https://aur.archlinux.org/packages/sxhkd-git/).

## Configuration

### Sxhkd Config File

sxhkd defaults to `$XDG_CONFIG_HOME/sxhkd/sxhkdrc` for its configuration file. An alternate configuration file can be specified with the `-c` option.

Each line of the configuration file is interpreted as so:

*   If it starts with `#`, it is ignored.
*   If it starts with one or more white space commands, it is read as a command.
*   Otherwise, it is parsed as a hotkey: each key name is separated by spaces and/or `+` characters.

General syntax:

```
[MODIFIER + ]*[@|!]KEYSYM
    COMMAND

```

Where `MODIFIER` is one of the following names: `super`, `hyper`, `meta`, `alt`, `control`, `ctrl`, `shift`, `mode_switch`, `lock`, `mod1`, `mod2`, `mod3`, `mod4`, `mod5`. If `@` is added at the beginning of the keysym, the command will be run on key release events, otherwise on key press events. If `!` is added at the beginning of the keysym, the command will be run on motion notify events and must contain two integer conversion specifications which will be replaced by the x and y coordinates of the pointer relative to the root window referential (the only valid button keysyms for this type of hotkeys are: `button1`, ..., `button5`). The `KEYSYM` names are those your will get from `xev`.

Mouse hotkeys can be defined by using one of the following special keysym names: `button1`, `button2`, `button3`, ..., `button24`. The hotkey can contain a sequence of the form (`STRING_1`,…,`STRING_N`), in which case, the command must also contain a sequence with *N* elements: the pairing of the two sequences generates *N* hotkeys. In addition, the sequences can contain ranges of the form `A-Z` where *A* and *Z* are alphanumeric characters.

What is actually executed is `SHELL -c COMMAND`, which means you can use environment variables in `COMMAND`. `SHELL` will be the content of the first defined environment variable in the following list: `SXHKD_SHELL`, `SHELL`. If sxhkd receives a `SIGUSR1` signal, it will reload its configuration file.

### Systemd Service File

Create systemd service file for the user in question

 `%HOME/.config/systemd/user/sxhkd.service` 
```
[Unit]
 Description=Simple X Hotkey Daemon
 Documentation=man:sxhkd(1)
 BindsTo=xorg.service
 After=xorg.service

 [Service]
 ExecStart=/usr/bin/sxhkd
 ExecReload=/usr/bin/kill -SIGUSR1 $MAINPID

 [Install]
 WantedBy=graphical.target
```

Enable and start the service

```
# systemctl --user enable sxhkd.service
# systemctl --user start sxhkd.service

```

## Usage

After configuring it, you may wish to setup sxhkd to [autostart](/index.php/Autostart "Autostart").

**Tip:** An example [systemd](/index.php/Systemd "Systemd") service file is found [here](https://github.com/baskerville/sxhkd/blob/master/contrib/systemd/sxhkd.service).

## Example

Edit `$XDG_CONFIG_HOME/sxhkd/sxhkdrc`

```
# On mouse button 1 press Alt_R+F1
button1
 xte "keydown Alt_R" "keydown F1" "keyup Alt_R" "keyup F1"
# On mosue button 2 pause 3 seconds then press Alt_R+F2
button2
 xte "sleep 3" "keydown Alt_R" "keydown F2" "keyup Alt_R" "keyup F2"

```

Restart user's sxhkd service

```
# systemctl --user restart sxhkd.service

```

## See Also

*   [Official website](https://github.com/baskerville/sxhkd) - includes configuration options, example bindings, and source code.
*   [ArchLinux forum thread](https://bbs.archlinux.org/viewtopic.php?id=155613)