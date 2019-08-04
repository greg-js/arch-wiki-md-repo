Related articles

*   [feh](/index.php/Feh "Feh")

[Nitrogen](https://github.com/l3ib/nitrogen/) is a fast and lightweight desktop background browser and setter for X Window.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Setting wallpaper](#Setting_wallpaper)
    *   [2.2 Restoring wallpaper](#Restoring_wallpaper)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Freeze with dual monitors](#Freeze_with_dual_monitors)

## Installation

[Install](/index.php/Install "Install") the [nitrogen](https://www.archlinux.org/packages/?name=nitrogen) package.

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