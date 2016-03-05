**System-tar-and-restore** contains two bash scripts, **backup.sh** and **restore.sh**. The former makes a tar backup of your system. The latter restores the backup or transfers your system using [rsync](https://www.archlinux.org/packages/?name=rsync) in desired partition(s). The scripts include two interfaces, **cli** and **dialog** (ncurses). If you plan to use the second, install [dialog](https://www.archlinux.org/packages/?name=dialog) from the [official repositories](/index.php/Official_repositories "Official repositories"). Also a [gui wrapper](https://github.com/tritonas00/system-tar-and-restore#gui) is available. Install [gtkdialog](https://www.archlinux.org/packages/?name=gtkdialog) and run `star-gui.sh` as root in order to use it.

## Installation

Install [system-tar-and-restore](https://aur.archlinux.org/packages/system-tar-and-restore/) from the [AUR](/index.php/AUR "AUR") or from [archlinuxgr-any](/index.php/Unofficial_user_repositories#archlinuxgr-any "Unofficial user repositories") repo.

## Usage

See the [README](https://github.com/tritonas00/system-tar-and-restore/blob/master/README.md).