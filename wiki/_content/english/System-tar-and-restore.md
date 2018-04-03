**System-tar-and-restore** contains two bash scripts, the main program **star.sh** and a gui wrapper **star-gui.sh**. Three modes are available:

*   **Backup**: With this mode you can make a tar backup archive of your system.

*   **Restore/Transfer**: Restore mode uses the above created archive to extract it in desired partition(s). Transfer mode transfers your system in desired partition(s) using [rsync](https://www.archlinux.org/packages/?name=rsync). Then, in both cases, the script generates the target system's fstab, rebuilds initramfs for every available kernel, generates locales and finally installs and configures the selected bootloader.

If you plan to use the gui, install [gtkdialog](https://aur.archlinux.org/packages/gtkdialog/) from the [AUR](/index.php/AUR "AUR").

## Installation

Install [system-tar-and-restore](https://aur.archlinux.org/packages/system-tar-and-restore/).

## Usage

See the [README](https://github.com/tritonas00/system-tar-and-restore/blob/master/README.md).