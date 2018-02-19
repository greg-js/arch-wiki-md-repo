Related articles

*   [pacman](/index.php/Pacman "Pacman")

**pkgfile** is a tool for searching files from packages in the [official repositories](/index.php/Official_repositories "Official repositories").

**Tip:** [pacman](https://www.archlinux.org/packages/?name=pacman) has [a similar functionality built in](/index.php/Pacman#Search_for_a_package_that_contains_a_specific_file "Pacman").

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Command not found](#Command_not_found)
*   [4 Automatic updates](#Automatic_updates)

## Installation

[Install](/index.php/Install "Install") the [pkgfile](https://www.archlinux.org/packages/?name=pkgfile) package. Alternatively, install the development version with the [pkgfile-git](https://aur.archlinux.org/packages/pkgfile-git/) package.

The *pkgfile* database can then be synced with:

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

See [Bash#Command not found](/index.php/Bash#Command_not_found "Bash"), [Zsh#The "command not found" hook](/index.php/Zsh#The_.22command_not_found.22_hook "Zsh") and [Fish#The "command not found" hook](/index.php/Fish#The_.22command_not_found.22_hook "Fish").

## Automatic updates

**pkgfile** ships with a [systemd](/index.php/Systemd "Systemd") service and [timer](/index.php/Systemd/Timers "Systemd/Timers") for automatically synchronizing the pkgfile database. To activate automatic updates [enable](/index.php/Enable "Enable") `pkgfile-update.timer`.

By default, pkgfile will be updated daily. To change this schedule, [edit the unit file](/index.php/Systemd#Editing_provided_units "Systemd").