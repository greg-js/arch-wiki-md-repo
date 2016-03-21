Budgie is the default desktop of Solus Operating System, written from scratch. Besides a more modern design, Budgie can emulate the look and feel of the GNOME 2 desktop.

At this time Budgie is heavily under development, so you can expect minor bugs and new features to be added as time goes on.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Starting](#Starting)
*   [2 Usage](#Usage)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop) package for the latest stable or [budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/) for current git master. It's recommended to install its optional dependencies also to get a more complete desktop environment. It's recommended also to install the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group, which contains applications required for the standard GNOME experience.

### Starting

Choose *Budgie Desktop* session from a [display manager](/index.php/Display_manager "Display manager") of choice, or modify [xinitrc](/index.php/Xinitrc "Xinitrc") to include Budgie Desktop:

 `~/.xinitrc` 
```
export XDG_CURRENT_DESKTOP=Budgie:GNOME
exec budgie-desktop

```

## Usage

You can see the notification messages, set volume, and modify the look and feel of the desktop with the sidebar called "Raven". It can be accessed with `Super+N` key or by clicking on the Status Indicator applet.

## See also

*   [Official Solus Project website](https://solus-project.com/)
*   [Official git repositories for Solus development](https://git.solus-project.com/)
*   [Build status for Solus projects](https://build.solus-project.com/)