Plank is a lightweight and minimal dock. Plank will not work if you are using Wayland.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Running Plank](#Running_Plank)
*   [2 Configuration](#Configuration)
    *   [2.1 Setting themes](#Setting_themes)
    *   [2.2 Multiple Docks](#Multiple_Docks)

## Installation

Install [plank](https://www.archlinux.org/packages/?name=plank) from the official repositories or [plank-git](https://aur.archlinux.org/packages/plank-git/) from the AUR.

### Running Plank

```
$ plank

```

## Configuration

Preferences can be opened by pressing `Ctrl + Right Click` on the dock and selecting *Preferences* in the submenu that opens.

Although the preferences of each dock is stored in the [dconf](https://www.archlinux.org/packages/?name=dconf) database and not in plain text, sometimes it makes sense to get and store that information anyway and then feed it back at some point. *Eg. backing up the settings or migrating the settings, etc.*

Therefore one may want to save all the docks:

```
$ dconf dump /net/launchpad/plank/docks/ > /path/where/to/save/plank/docks.ini

```

And then one may want to reload the saved settings:

```
$ cat /path/where/saved/plank/docks.ini | dconf load /net/launchpad/plank/docks/

```

### Setting themes

The theme can be changed by selecting a choice in the drop-down menu of *Preferences > Appearance > Theme*. Themes are stored globally under `/usr/share/plank/themes/` or locally under `~/.local/share/plank/themes/`.

These custom themes can be installed to give your plank dock an eyecandy touch :

[plank-theme-numix](https://aur.archlinux.org/packages/plank-theme-numix/): Numix theme for Plank

[plank-theme-pantheon-bzr](https://aur.archlinux.org/packages/plank-theme-pantheon-bzr/): Pantheon Plank theme

[plank-theme-arc](https://aur.archlinux.org/packages/plank-theme-arc/): Arc theme for Plank

[unity-like-plank-theme](https://aur.archlinux.org/packages/unity-like-plank-theme/): A plank dock theme that give an interface similar to that of Unity.

### Multiple Docks

It is possible to run multiple plank docks at once.

Directories for each dock are stored under `~/.config/plank/`. Under these directories, there is a directory named 'launchers'. Going further, under this directory, docklets are stored. When the *plank* command is run, it either defaults to the dock1 directory or creates it if it is non-existent. If you were to run:

```
$ plank -n newdock

```

A new directory named 'newdock' would be created under `~/.config/plank` and docklets stored under `~/.config/plank/newdock/launchers/` is displayed on the dock, unless a directory under that name has already been created. This makes it possible to have multiple docks each with their own settings and preferences by specifying the name under the `-n` flag.

For example:

```
$ plank -n primdock 
$ plank -n secondock

```