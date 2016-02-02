# Xephyr

**Xephyr** is a nested X server that runs as an X application.

## Installation

[xorg-server-xephyr](https://www.archlinux.org/packages/?name=xorg-server-xephyr) is available from [official repositories](/index.php/Official_repositories "Official repositories"). Install it with [pacman](/index.php/Pacman "Pacman").

## Execution

If you wish to run a nested X window, you'll need to specify a display.

```
$ Xephyr -br -ac -noreset -screen 800x600 :1

```

This will launch a new Xephyr window with a DISPLAY of ":1". In order to launch an application in that window, you would need to specify that display.

```
$ DISPLAY=:1 xterm

```

If you want to launch another WM, [spectrwm](/index.php/Spectrwm "Spectrwm") for example, you would type:

```
$ DISPLAY=:1 spectrwm

```

You can also launch Xephyr with your [xinitrc](/index.php/Xinitrc "Xinitrc") using startx:

```
 $ startx -- /usr/bin/Xephyr :1

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Xephyr&oldid=387994](https://wiki.archlinux.org/index.php?title=Xephyr&oldid=387994)"