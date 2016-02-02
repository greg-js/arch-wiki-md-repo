# pkgfile

**pkgfile** is a tool for searching files from packages in the [official repositories](/index.php/Official_repositories "Official repositories").

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Command not found](#Command_not_found)
    *   [3.1 Bash](#Bash)
    *   [3.2 Zsh](#Zsh)
    *   [3.3 Fish](#Fish)
*   [4 Automatic updates](#Automatic_updates)

## Installation

[Install](/index.php/Install "Install") [pkgfile](https://www.archlinux.org/packages/?name=pkgfile) from the official repositories, or [pkgfile-git](https://aur.archlinux.org/packages/pkgfile-git/) from the [AUR](/index.php/AUR "AUR").

The _pkgfile_ database can then be synced with:

```
# pkgfile -u

```

## Usage

To search for a package that owns the file `makepkg`:

 `$ pkgfile makepkg`  `core/pacman` 

To list all files provided by [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring):

 `$ pkgfile -l archlinux-keyring` 

```
core/archlinux-keyring usr/
core/archlinux-keyring usr/share/
core/archlinux-keyring usr/share/pacman/
core/archlinux-keyring usr/share/pacman/keyrings/
core/archlinux-keyring usr/share/pacman/keyrings/archlinux-revoked
core/archlinux-keyring usr/share/pacman/keyrings/archlinux-trusted
core/archlinux-keyring usr/share/pacman/keyrings/archlinux.gpg
```

Latter is comparable to `pacman -Ql` (see [pacman#Querying package databases](/index.php/Pacman#Querying_package_databases "Pacman")), except it applies to remote packages.

## Command not found

[pkgfile](https://www.archlinux.org/packages/?name=pkgfile) includes a "command not found" hook for [Bash](/index.php/Bash "Bash") and [Zsh](/index.php/Zsh "Zsh") that will automatically search the official repositories, when entering an unrecognized command:

 `$ abiword` 

```
abiword may be found in the following packages:
  extra/abiword 2.8.6-7 usr/bin/abiword

```

To enable it in all children shells, you need to source the hook from one of your shell initialization files.

### Bash

 `~/.bashrc`  `source /usr/share/doc/pkgfile/command-not-found.bash` 

### Zsh

 `~/.zshrc`  `source /usr/share/doc/pkgfile/command-not-found.zsh` 

### Fish

Since [version 2.2](https://github.com/fish-shell/fish-shell/releases/tag/2.2.0) [Fish](/index.php/Fish "Fish") has provided its own "command not found" hook for [pkgfile](https://www.archlinux.org/packages/?name=pkgfile): [Add command-not-found handler for Arch Linux #1925](https://github.com/fish-shell/fish-shell/pull/1925)

## Automatic updates

**pkgfile** ships with a [systemd](/index.php/Systemd "Systemd") service and [timer](/index.php/Systemd/Timers "Systemd/Timers") for automatically synchronizing the pkgfile database. To activate automatic updates [enable](/index.php/Enable "Enable") `pkgfile-update.timer`.

By default, pkgfile will be updated daily. To change this schedule, [edit the unit file](/index.php/Systemd#Editing_provided_units "Systemd").

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pkgfile&oldid=412007](https://wiki.archlinux.org/index.php?title=Pkgfile&oldid=412007)"