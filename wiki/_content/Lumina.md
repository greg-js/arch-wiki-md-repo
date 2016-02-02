# Lumina

Related articles

*   [AUR](/index.php/AUR "AUR")
*   [ZFS](/index.php/ZFS "ZFS")
*   [Fluxbox](/index.php/Fluxbox "Fluxbox")

The Lumina Desktop Environment (Lumina for short) is a lightweight, XDG-compliant, BSD-licensed desktop environment that focuses specifically on streamlining the ability to get work done while minimizing system overhead. As of version 0.8.0+, it requres Qt 5, the Fluxbox window manager, and uses a small number of X utilities for various tasks, such as numlockx and xscreensaver.

Lumina's features include:

*   Very little system overhead.

*   Intelligent "favorites" system for creating quick shortcuts to applications, files, and directories.

*   ZFS file restore functionality through the "Insight" file manager.

*   Desktop system is plugin-based, which is similar to Android or other modern operating systems.

*   Simple access to operating system-specific functionality such as screen brightness, audio volume, and battery status.

## Contents

*   [1 Installation](#Installation)
*   [2 Launching the Lumina Desktop Environment](#Launching_the_Lumina_Desktop_Environment)
    *   [2.1 Via .xinitrc](#Via_.xinitrc)
*   [3 Reporting bugs](#Reporting_bugs)
*   [4 See also](#See_also)

## Installation

**Warning:** Lumina is still beta software and thus potentially unstable. Additionally, the DE is primarily targeted at FreeBSD, not Linux.

To install the Lumina Desktop environment, simply install [lumina-desktop](https://aur.archlinux.org/packages/lumina-desktop/)<sup><small>AUR</small></sup> or [lumina-desktop-git](https://aur.archlinux.org/packages/lumina-desktop-git/)<sup><small>AUR</small></sup> from the AUR.

## Launching the Lumina Desktop Environment

### Via .xinitrc

_For information visit the [xinitrc](/index.php/Xinitrc "Xinitrc") wiki page_

 ` ~/.xinitrc` 

```
exec Lumina-DE

```

## Reporting bugs

Bugs should be reported to Lumina's repository on [Github](https://github.com/pcbsd/lumina).

## See also

*   [About Lumina](http://lumina-desktop.org/)
*   [Lumina Handbook](http://lumina-desktop.org/handbook/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lumina&oldid=413269](https://wiki.archlinux.org/index.php?title=Lumina&oldid=413269)"