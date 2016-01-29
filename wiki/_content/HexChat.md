# HexChat

[HexChat](http://hexchat.github.io/) is a multi-platform IRC client for [GTK+](/index.php/GTK%2B "GTK+").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Freenode SSL and SASL](#Freenode_SSL_and_SASL)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 GNOME integration](#GNOME_integration)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Spell check does not work](#Spell_check_does_not_work)
    *   [4.2 Missing tray icon](#Missing_tray_icon)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Pacman#Installing_packages "Pacman") [hexchat](https://www.archlinux.org/packages/?name=hexchat). The development version [hexchat-git](https://aur.archlinux.org/packages/hexchat-git/)<sup><small>AUR</small></sup> is available in the [AUR](/index.php/AUR "AUR"). For the legacy version, install [xchat](https://www.archlinux.org/packages/?name=xchat).

## Configuration

HexChat stores configuration files in `~/.config/hexchat`, XChat does so in `~/.xchat2`.

### Freenode SSL and SASL

In HexChat, enable SSL and SASL in Network List (`Ctrl+S`) > Freenode > Edit.

In XChat, enable SSL and change the server address from `chat.freenode.net` to `chat.freenode.net/+6697`. To enable SASL, follow [Configuring SASL for XChat](https://freenode.net/sasl/sasl-xchat.shtml).

## Tips and tricks

### GNOME integration

To use the new Notifications and messaging tray, activate the following options in Settings > Preferences > Chatting > Alerts:

*   Show tray balloons
*   Blink tray icon (optional)
*   Enable system tray icon: unchecked (the icon appears automatically if you have pending notifications)

## Troubleshooting

### Spell check does not work

To fully enable spell-check, you need to install the correct dictionary besides [enchant](https://www.archlinux.org/packages/?name=enchant). Find your correct dictionary by [searching](/index.php/Pacman#Querying_package_databases "Pacman") for [hunspell](https://www.archlinux.org/packages/?name=hunspell).

For English this is [hunspell-en](https://www.archlinux.org/packages/?name=hunspell-en). Restart XChat after installation.

### Missing tray icon

If XChat was loaded _before_ the panel containing its icon, for example when the panel is forcibly reloaded, the icon may be invisible. [[1]](https://bugs.launchpad.net/ubuntu/+source/xchat/+bug/410525) To restore the icon, run:

```
$ xchat --existing --command="set gui_tray 0"
$ xchat --existing --command="gui apply"
$ xchat --existing --command="set gui_tray 1"
$ xchat --existing --command="gui apply"

```

Or restore the main window with:

```
$ xchat --existing --command="gui show"

```

## See also

*   [HexChat documentation](http://hexchat.readthedocs.org/en/latest/index.html)
*   [Toxin XChat Themes](http://toxin.jottit.com/xchat_themes)
*   [XChat command line options](https://xchatdata.net/Using/CommandLineOptions)

Retrieved from "[https://wiki.archlinux.org/index.php?title=HexChat&oldid=382652](https://wiki.archlinux.org/index.php?title=HexChat&oldid=382652)"