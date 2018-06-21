[Inkscape](http://inkscape.org/) is a vector graphics editor application. It is distributed under a free software license, the GNU GPL. Its stated goal is to become a powerful graphics tool while being fully compliant with the XML, SVG, and CSS standards.[wikipedia:Inkscape](https://en.wikipedia.org/wiki/Inkscape "wikipedia:Inkscape")

## Contents

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Tooltips unreadable with KDE Plasma](#Tooltips_unreadable_with_KDE_Plasma)
    *   [2.2 Pan using spacebar and mouse does not work](#Pan_using_spacebar_and_mouse_does_not_work)
    *   [2.3 Cannot change keyboard shortcuts](#Cannot_change_keyboard_shortcuts)
*   [3 See also](#See_also)

## Installation

[inkscape](https://www.archlinux.org/packages/?name=inkscape) can be installed from the [official repositories](/index.php/Official_repositories "Official repositories"). The development version is available in the [AUR](/index.php/AUR "AUR") as [inkscape-git](https://aur.archlinux.org/packages/inkscape-git/).

## Troubleshooting

### Tooltips unreadable with KDE Plasma

Under KDE's system settings go to colors > options and disable "Apply colors to non-QT-applications". Restart Inkscape if was running before the change.

### Pan using spacebar and mouse does not work

By default, [libinput](/index.php/Libinput "Libinput") disables the mousepad when typing. You can disable this by adding the following line to the `InputClass` section of `/etc/X11/xorg.conf.d/30-touchpad.conf`:

```
Section "InputClass"
    ...
    ...
    Option "DisableWhileTyping" "0"
EndSection

```

### Cannot change keyboard shortcuts

To be able to change keyboard shortcuts, create a copy of the shortcut file that you can edit:

```
mkdir -p ~/.config/inkscape/keys
cp /usr/share/inkscape/keys/default.xml ~/.config/inkscape/keys/

```

and restart the application.

## See also

*   [Multimedia in Arch Linux](/index.php/Multimedia_in_Arch_Linux "Multimedia in Arch Linux")
*   [Inkscape Homepage](http://inkscape.org/)
*   [Inkscape at Wikipedia](https://en.wikipedia.org/wiki/Inkscape "wikipedia:Inkscape")