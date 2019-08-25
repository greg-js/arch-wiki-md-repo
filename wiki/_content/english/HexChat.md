[HexChat](http://hexchat.github.io/) is a multi-platform IRC client for [GTK](/index.php/GTK "GTK").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Freenode SSL and SASL](#Freenode_SSL_and_SASL)
    *   [2.2 GNOME integration](#GNOME_integration)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Missing tray icon](#Missing_tray_icon)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Pacman#Installing_packages "Pacman") [hexchat](https://www.archlinux.org/packages/?name=hexchat). The development version [hexchat-git](https://aur.archlinux.org/packages/hexchat-git/) is available in the [AUR](/index.php/AUR "AUR"). For another fork of the legacy version, install [xchat-se](https://aur.archlinux.org/packages/xchat-se/).

For spell checking install [enchant](https://www.archlinux.org/packages/?name=enchant), see [Language checking](/index.php/Language_checking "Language checking") for available dictionaries. Restart HexChat for changes to take an effect.

## Configuration

HexChat stores configuration files in `~/.config/hexchat`, XChat does so in `~/.xchat2`.

### Freenode SSL and SASL

In HexChat, enable SSL and SASL in Network List (`Ctrl+S`) > Freenode > Edit.

In XChat, enable SSL and change the server address from `chat.freenode.net` to `chat.freenode.net/+6697`. To enable SASL, follow [Configuring SASL for XChat](https://freenode.net/sasl/sasl-xchat.shtml).

### GNOME integration

To use the new Notifications and messaging tray, activate the following options in Settings > Preferences > Chatting > Alerts:

*   Show tray balloons
*   Blink tray icon (optional)
*   Enable system tray icon: unchecked (the icon appears automatically if you have pending notifications)

## Troubleshooting

### Missing tray icon

If HexChat was loaded *before* the panel containing its icon, for example when the panel is forcibly reloaded, the icon may be invisible. [[1]](https://bugs.launchpad.net/ubuntu/+source/xchat/+bug/410525) To restore the icon, run:

```
$ hexchat --existing --command="set gui_tray 0"
$ hexchat --existing --command="gui apply"
$ hexchat --existing --command="set gui_tray 1"
$ hexchat --existing --command="gui apply"

```

Or restore the main window with:

```
$ hexchat --existing --command="gui show"

```

## See also

*   [HexChat documentation](http://hexchat.readthedocs.org/en/latest/index.html)
*   [Toxin XChat Themes](http://toxin.jottit.com/xchat_themes)
*   [XChat command line options](https://xchatdata.net/Using/CommandLineOptions)