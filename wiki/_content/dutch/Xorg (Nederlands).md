**Xorg** is een open-source implementatie van het X Window Systeem, versie 11\. Omdat X zeer populair is bij GNU/Linux gebruikers, maken veel distributies en graphische applicaties hier gebruik van. Zie voor meer details het [Wikipedia artikel](http://nl.wikipedia.org/wiki/X_Window_System) of de [Xorg Wiki](http://www.x.org/wiki).

## Contents

*   [1 Installatie](#Installatie)
    *   [1.1 Inputapparaten](#Inputapparaten)
        *   [1.1.1 Touchpad](#Touchpad)
    *   [1.2 Graphics](#Graphics)
    *   [1.3 Xorg zonder display manager](#Xorg_zonder_display_manager)
*   [2 Configuratie](#Configuratie)

## Installatie

De makkelijkste manier om Xorg te installeren is met

```
 pacman -S xorg

```

maar dan worden alle packages (ook de onnodige) geinstalleerd. Een moeilijkere manier is door eerst de x-server te installeren met

```
 pacman -S xorg-server

```

En dan een aantal handige utiliteiten met:

```
 pacman -S xorg-apps

```

### Inputapparaten

Meestal is het niet nodig drivers te installeren voor Xorg. Als dit wel moet, geeft

```
 pacman -sg xorg-drivers

```

een lijst van beschikbare drivers.

#### Touchpad

Laptopgebruikers zullen waarschijnlijk een touchpaddriver willen installeren:

```
 pacman -S [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics)

```

De config file is /etc/X11/xorg.conf.d/10-synaptics.conf

### Graphics

De standaard videodriver is [xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa). Deze werkt met bijna alle chipsets maar geeft geen 2d of 3d accelleratie, hiervoor is een videokaartspecifieke driver nodig. Identificeer eerst de videokaart met

```
 lspci | grep VGA

```

Veelvoorkomende open-source drivers zijn:

*   NVIDIA: [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau)
*   Intel: [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)
*   ATI: [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati)

Veelvoorkomende proprietaire drivers zijn:

*   NVIDIA: [nvidia](https://www.archlinux.org/packages/?name=nvidia)
*   ATI: [catalyst](https://aur.archlinux.org/packages/catalyst/)

Proprietaire drivers zijn alleen nodig voor meerdere schermen, tv-out of 3d acceleratie voor games.

### Xorg zonder display manager

Om Xorg zonder display manager te gebruiken is [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit) nodig. Een window manager, zoals [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm) is ook handig:

```
 pacman -S xorg-xinit
 pacman -S xorg-twm

```

[xorg-xclock](https://www.archlinux.org/packages/?name=xorg-xclock) en [xterm](https://www.archlinux.org/packages/?name=xterm) zijn ook erg handg:

```
 pacman -S xorg-xclock xterm
 startx

```

geeft nu een een simpele X omgeving met [twm](/index.php/Twm "Twm"), [Xterm](/index.php/Xterm "Xterm") en [Xclock](/index.php?title=Xclock&action=edit&redlink=1 "Xclock (page does not exist)").

## Configuratie

Xorg kan geconfigureerd worden met /etc/X11/xorg.conf of /etc/xorg.conf en config files in /etc/X11/xorg.conf.d/

* * *

Dit artikel is gebaseerd op het artikel [Xorg](https://wiki.archlinux.org/index.php/Xorg) op de engelstalige ArchWiki.