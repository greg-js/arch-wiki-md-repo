[Nitrogen](http://projects.l3ib.org/nitrogen/) is a fast and lightweight desktop background browser and setter for X windows.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Setting wallpaper](#Setting_wallpaper)
    *   [2.2 Restoring wallpaper](#Restoring_wallpaper)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Freeze with dual monitors](#Freeze_with_dual_monitors)

## Installation

Nitrogen can be [installed](/index.php/Pacman "Pacman") with the package [nitrogen](https://www.archlinux.org/packages/?name=nitrogen), available in the [official repositories](/index.php/Official_repositories "Official repositories").

## Usage

Run `nitrogen --help` for full details. The following examples will get you started:

### Setting wallpaper

To view and set the desired wallpaper from a specific directory recursively, run:

```
$ nitrogen /path/to/image/directory/

```

To view and set the desired wallpaper from a specific directory non-recursively, run:

```
$ nitrogen --no-recurse /path/to/image/directory/

```

### Restoring wallpaper

To restore the chosen wallpaper during subsequent sessions, [autostart](/index.php/Autostart "Autostart") the following command: `nitrogen --restore &`

## Troubleshooting

### Freeze with dual monitors

Remove the current nitrogen configuration: [[1]](https://bbs.archlinux.org/viewtopic.php?id=46245)

```
$ rm -r ~/.config/nitrogen/

```