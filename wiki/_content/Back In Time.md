# Back In Time

**Back In Time** is a simple backup tool for Linux inspired by “flyback project” and “TimeVault”. The backup is done by taking snapshots of a specified set of directories.

Back In Time provides a Qt4 GUI which will run on Gnome, KDE and all other DE's.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Can't find snapshots folder](#Can.27t_find_snapshots_folder)
*   [4 See also](#See_also)

## Installation

Stable releases of Back In Time can be installed as [backintime](https://aur.archlinux.org/packages/backintime/) from the [AUR](/index.php/AUR "AUR"). An unstable branch exists with [backintime-git](https://aur.archlinux.org/packages/backintime-git/).

Alternatively, pre-compiled binary packages can be installed from [coderkun’s repo](http://arch.coderkun.de/).

As Back In Time uses [rsync](/index.php/Rsync "Rsync") internally make sure the [rsync](https://www.archlinux.org/packages/?name=rsync) package is installed.

Back In Time will automatically install a startup entry in `/etc/xdg/autostart`. If you want to launch the GUI, then run `backintime-qt4`. If you want to backup files other than your home user files, then consider starting Back In Time with `pkexec backintime-qt4` instead.

## Configuration

The configuration can be done entirely via the GUI. All you have to do is configure:

*   Where to save snapshot
*   What directories to backup
*   When backup should be done (manual, every hour, every day, every week, every month)

## Troubleshooting

### Can't find snapshots folder

If you see the error message in the status bar that BIT cannot find the snapshots folder although the snapshots are visible in the sidebar and the backup process is working correctly, then you are likely to have leftovers from a previous failed backup cron job. The status bar displays the content of the file `~/.local/share/backintime/worker.message`. Thus deleting or renaming this file will remove the error message.

## See also

*   [Back In Time website](https://github.com/bit-team/backintime)
*   [Upstream Bug Tracker](https://github.com/bit-team/backintime/issues)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Back_In_Time&oldid=416185](https://wiki.archlinux.org/index.php?title=Back_In_Time&oldid=416185)"