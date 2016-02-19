[BMPanel](https://code.google.com/p/bmpanel2/) (*BitMap Panel*) is a lightweight, NETWM compliant panel for X11 Window System, which contains a desktop switcher, taskbar, system tray and clock. The application is inspired by simplicity of fspanel. BMPanel has a modern look and feel, while keeping itself tiny and small.

## Installation

BMPanel is available as [bmpanel2](https://aur.archlinux.org/packages/bmpanel2/) in the [AUR](/index.php/AUR "AUR"). If you prefer the legacy version not mantained anymore install [bmpanel](https://aur.archlinux.org/packages/bmpanel/).

## Themes

BMPanel2 themes are available in the [bmpanel2-themes](https://aur.archlinux.org/packages/bmpanel2-themes/) package. Further information about available themes can be found [here](http://code.google.com/p/bmpanel2/wiki/ThemeGallery). Here you can find more themes. Extract them to `~/.local/share/bmpanel2/themes` (respectively `~/.bmpanel/themes` for bmpanel legacy). Altering design of the theme can be done by adapting the `~/.local/share/bmpanel2/themes/*theme name*/theme` file (respectively `~/.bmpanel/themes/*theme name*/theme`). More information on this can be found [here](https://code.google.com/p/bmpanel2/).

## Starting bmpanel

To start BMPanel automatically after the login you need to write this to your `~/.xinitrc` file:

```
bmpanel *theme_name* &

```

or:

```
bmpanel2 --theme=*theme_name* &

```