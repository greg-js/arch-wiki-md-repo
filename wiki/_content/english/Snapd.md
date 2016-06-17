[snapd](https://github.com/snapcore/snapd) is a REST API daemon for managing snap packages ("snaps"). Users can interact with it by using the *snap* client, which is part of the same package.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Managing snaps](#Managing_snaps)
    *   [3.1 Finding](#Finding)
    *   [3.2 Installing](#Installing)
    *   [3.3 Updating](#Updating)
    *   [3.4 Removing](#Removing)
*   [4 See also](#See_also)

## Installation

The stable version is available as [snapd](https://aur.archlinux.org/packages/snapd/).

Installing it will install the `snapd` daemon as well as *snap-confine*, which mounts, confines and launches snap packages.

**Tip:** `snapd` installs a script in `/etc/profile.d/` to export the paths of binaries installed with the snapd package and desktop entries. Reboot once to make this change take effect.

## Configuration

The package ships several systemd unit files, which manage several tasks like automatically refreshing all installed snaps once a new version is released.

To launch the `snapd` daemon when *snap* tries to use it, [start](/index.php/Start "Start") the `snapd.socket` and/or [enable](/index.php/Enable "Enable") it to have it started at boot.

To start the timer which periodically refreshes snaps when a new version is pushed to the store use:

```
# systemctl start snapd.refresh.timer

```

## Managing snaps

The *snap* tool is used to manage the snaps.

### Finding

To find snaps to install, you can query the Ubuntu Store with:

```
$ snap find

```

which will list every snap that is available to install. To search for a specific snap use:

```
$ snap find *searchterm*

```

### Installing

Once you found the snap you are looking for you can install it with:

```
# snap install *snapname*

```

This requires root privileges. Per user installation of snaps is not possible, yet. This will download the snap into `/var/lib/snapd/snaps` and mount it to `/snap/*snapname*` to make it available to the system.

It will also create mount units for each snap and add them to `/etc/systemd/system/multi-user.target.wants/` as symlinks to make all snaps available when the system is booted. Once that is done you should find it in the list of installed snaps together with its version number, revision and developer using:

```
$ snap list

```

You can also sideload snaps from your local hard drive with:

```
# snap install --devmode */path/to/snap*

```

### Updating

To update your snaps use:

```
# snap refresh

```

### Removing

Snaps can be removed by executing:

```
# snap remove *snapname*

```

## See also

*   [arstechnica article](http://arstechnica.com/information-technology/2016/06/goodbye-apt-and-yum-ubuntus-snap-apps-are-coming-to-distros-everywhere/) (06/16) about Ubuntu snaps becoming available for Arch and other distros