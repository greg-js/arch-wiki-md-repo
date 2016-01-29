# Deepin Desktop Environment

[DDE](http://www.deepin.org/?language=en) (Deepin Desktop Environment) is the default desktop environment originally created for the linux Deepin distribution.

## Contents

*   [1 Installation](#Installation)
*   [2 Launching Deepin Desktop Environment](#Launching_Deepin_Desktop_Environment)
    *   [2.1 Via a Display Manager](#Via_a_Display_Manager)
    *   [2.2 Using xinitrc](#Using_xinitrc)
*   [3 Bug Reporting](#Bug_Reporting)

## Installation

To get a minimal desktop interface, you may start by [installing](/index.php/Installing "Installing") [deepin](https://www.archlinux.org/groups/x86_64/deepin/) group. This will pull all the basic components.

However, it is recommended to also install [deepin-extra](https://www.archlinux.org/groups/x86_64/deepin-extra/) group to get a fully working DDE:

*   [deepin-game](https://www.archlinux.org/packages/?name=deepin-game): Deepin game center to play flash games
*   [deepin-movie](https://www.archlinux.org/packages/?name=deepin-movie): Deepin video player
*   [deepin-music](https://www.archlinux.org/packages/?name=deepin-music): Deepin music player
*   [deepin-screenshot](https://www.archlinux.org/packages/?name=deepin-screenshot): Deepin screen-shot tools
*   [deepin-terminal](https://www.archlinux.org/packages/?name=deepin-terminal): Deepin terminal

## Launching Deepin Desktop Environment

### Via a Display Manager

To use the default DDE's lightdm greeter you have to modify the configuration file under the `[SeatDefaults]` section, to state:.

 `/etc/lightdm/lightdm.conf` 

```
[SeatDefaults]
...
greeter-session=lightdm-deepin-greeter
```

### Using xinitrc

_See the [xinitrc](/index.php/Xinitrc "Xinitrc") page for more information._

 `~/.xinitrc` 

```
exec startdde

```

Execute `startx` or `xinit` to start DDE.

**Note:** If you want to start Xorg at boot, please read the [Start X at login](/index.php/Start_X_at_login "Start X at login") article.

## Bug Reporting

Any upstream or arch packaging related bugs should be reported [here](https://github.com/fasheng/arch-deepin/issues). FaSheng is one of the Deepin developers and also a contributor/maintainer for arch-deepin and if you file bug reports on his github page then there's much greater chance that the bug will be fixed. ;-)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Deepin_Desktop_Environment&oldid=415876](https://wiki.archlinux.org/index.php?title=Deepin_Desktop_Environment&oldid=415876)"