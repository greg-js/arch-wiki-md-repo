pkgstats sends a list of all installed packages, [kernel modules](https://www.archlinux.org/news/pkgstats-now-collects-modules-usage/), the architecture and the mirror you are using to the Arch Linux project. This information is anonymous and cannot be used to identify the user, but it will help Arch developers prioritize their efforts ([source code](https://git.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/pkgstats)).

## Installation

[Install](/index.php/Install "Install") the [pkgstats](https://www.archlinux.org/packages/?name=pkgstats) package.

## Usage

*pkgstats* is set up to automatically run every week using [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers"). Once installed, it will be activated after the next reboot.

If you do not want to wait for a reboot cycle, you can manually [start](/index.php/Start "Start") `pkgstats.timer`.

*pkgstats* can also be run manually: see `pkgstats -h` for usage information.

## Results and reference

Statistics are available at [https://www.archlinux.de/?page=Statistics](https://www.archlinux.de/?page=Statistics).

The following open source project allows you to get the statistics data as JSON: [ArchLinuxPkgStatsScraper](https://github.com/chrissound/ArchLinuxPkgStatsScraper)

You can read the official [forum thread](https://bbs.archlinux.org/viewtopic.php?id=105431) for more info.