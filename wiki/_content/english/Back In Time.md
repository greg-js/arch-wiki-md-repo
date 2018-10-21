From the [documentation](https://backintime.readthedocs.io/en/latest/):

	Back In Time is a simple backup solution for Linux desktops. It is based on rsync and uses hard-links to reduce space used for unchanged files. It comes with a Qt4 GUI which will run on both Gnome and KDE based Desktops. Back In Time is written in Python3 and is licensed under GPL2.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Can't find snapshots folder](#Can.27t_find_snapshots_folder)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [backintime](https://aur.archlinux.org/packages/backintime/), [backintime-cli](https://aur.archlinux.org/packages/backintime-cli/) for a CLI-only version, or [backintime-git](https://aur.archlinux.org/packages/backintime-git/) for the development version.

Alternatively, pre-compiled binary packages can be installed from [coderkun's repo](https://coderkun.de/arch/).

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

*   [GitHub repository](https://github.com/bit-team/backintime)
*   [Documentation](https://backintime.readthedocs.io/en/latest/)