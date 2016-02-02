# Putty

## Installation

[Install](/index.php/Install "Install") [putty](https://www.archlinux.org/packages/?name=putty). For a menu item and icon, install [putty-freedesktop](https://aur.archlinux.org/packages/putty-freedesktop/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

## 256 color support

_Settings > Connection > Data : Terminal-type string = xterm-256color_

To test color support, execute the following command: [reference](http://www.commandlinefu.com/commands/view/5879/show-numerical-values-for-each-of-the-256-colors-in-bash)

```
for code in {0..255}; do echo -e "\e[38;05;${code}m $code: Test"; done

```

See [256colours](http://www.robmeerman.co.uk/unix/256colours) for details.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Putty&oldid=399113](https://wiki.archlinux.org/index.php?title=Putty&oldid=399113)"