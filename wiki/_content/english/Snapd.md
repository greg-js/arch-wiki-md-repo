[snapd](https://github.com/snapcore/snapd) is a REST API daemon for managing snap packages. Users can interact with it by using the `snap` client, which is part of the same package.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Finding snaps](#Finding_snaps)
*   [4 Installing snaps](#Installing_snaps)
*   [5 Updating snaps](#Updating_snaps)
*   [6 Removing snaps](#Removing_snaps)

## Installation

The stable version can be found here [snapd](https://aur.archlinux.org/packages/snapd/).

Installing it will install the snapd daemon as well as snap-confine, which mounts, confines and launches snap packages.

**Tip:** snapd installs a script in /etc/profile.d/ to export the paths of binaries installed with snapd and desktop entries. Reboot once to make this change take effect.

## Configuration

snapd ships several systemd unit files, which manage several tasks like automatically refreshing all installed snaps once a new version is released.

To launch the snapd daemon when `snap` tries to use it, start the snapd.socket and/or enable it to have it started at boot.

 ` # systemctl start snapd.socket` 

To start the timer which periodically refreshes snaps when a new version is pushed to the store use:

 ` # systemctl start snapd.refresh.timer` 

## Finding snaps

You can query the Ubuntu Store with:

 ` $ snap find` 

which will list every snap that is available to install. To search for a specific snap use:

 ` $ snap find <searchterm>` 

## Installing snaps

Once you found the snap you are looking for you can install it with:

 ` # snap install <snapname>` 

This requires root privileges. Per user installation of snaps is not possible, yet. This will download the snap into `/var/lib/snapd/snaps` and mount it to `/snap/<snapname>` to make it available to the system.

It will also create mount units for each snap and add them to `/etc/systemd/system/multi-user.target.wants/` as symlinks to make all snaps available when the system is booted. Once that is done you should find it in the list of installed snaps together with its version number, revision and developer using:

 ` $ snap list` 

You can also sideload snaps from your local hard drive with:

 ` # snap install --devmode /path/to/snap` 

## Updating snaps

To update your snaps use:

 ` # snap refresh` 

## Removing snaps

Snaps can be removed by executing:

 ` # snap remove <snapname>`