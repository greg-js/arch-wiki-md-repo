[snapd](https://github.com/snapcore/snapd) is a REST API daemon for managing snap packages ("snaps"). Users can interact with it by using the *snap* client, which is part of the same package.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Removal](#Removal)
*   [4 Managing snaps](#Managing_snaps)
    *   [4.1 Finding](#Finding)
    *   [4.2 Installing](#Installing)
    *   [4.3 Updating](#Updating)
    *   [4.4 Removing](#Removing)
*   [5 Support](#Support)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [snapd](https://aur.archlinux.org/packages/snapd/) or the [snapd-git](https://aur.archlinux.org/packages/snapd-git/) package, both will remove `snap-confine` if you had `snapd` installed from the [official repositories](/index.php/Official_repositories "Official repositories") previously.

Installing it will install the `snapd` daemon.

**Tip:** `snapd` installs a script in `/etc/profile.d/` to export the paths of binaries installed with the snapd package and desktop entries. Reboot once to make this change take effect.

## Configuration

To launch the `snapd` daemon when *snap* tries to use it, [start](/index.php/Start "Start") the `snapd.socket` and/or [enable](/index.php/Enable "Enable") it to have it started at boot.

The package ships several systemd unit files, which manage several tasks like automatically refreshing all installed snaps once a new version is released.

To start the timer which periodically refreshes snaps when a new version is pushed to the store use:

```
# systemctl start snapd.refresh.timer

```

## Removal

**Tip:** Both [snapd](https://aur.archlinux.org/packages/snapd/) and [snapd-git](https://aur.archlinux.org/packages/snapd-git/) versions 2.30+ will automatically purge all installed snaps when the package is removed, the manual steps are no longer necessary

Uninstalling the [snapd](https://aur.archlinux.org/packages/snapd/) package will not remove directories and files created while using *snap*. It's best to remove your snaps with *snap remove* before uninstalling the package. At this time it is not possible to remove the core snap through the *snap* command. To remove the state, snap package cache and mount unit files completely, you can follow the instructions below.

1\. We unmount any currently active snap that is mounted to `/var/lib/snapd/snap/`.

```
# umount $(mount | grep snap | awk '{print $3}')

```

**Warning:** Your may want to review the output of `mount | grep snap` to avoid accidental unmounts.

2\. We remove the state directory and mount hook.

```
# rm -rf /var/lib/snapd
# rm -rf /var/snap

```

3\. We remove any unit files, that try to mount snaps from `/var/lib/snapd/snaps` to `/var/lib/snapd/snap` at boot.

```
# find /etc/systemd/system -name "*snap-*.mount" -delete
# find /etc/systemd/system -name "snap.*.service" -delete

```

## Managing snaps

The *snap* tool is used to manage the snaps.

### Finding

To find snaps to install, you can query the Ubuntu Store with:

```
$ snap find *searchterm*

```

### Installing

Once you found the snap you are looking for you can install it with:

```
# snap install *snapname*

```

This requires root privileges. Per user installation of snaps is not possible, yet. This will download the snap into `/var/lib/snapd/snaps` and mount it to `/snap/*snapname*` to make it available to the system. At this point you may want to add `/var/lib/snapd/snap/bin`to your $PATH variable in order to execute the installed snaps.

It will also create mount units for each snap and add them to `/etc/systemd/system/multi-user.target.wants/` as symlinks to make all snaps available when the system is booted. Once that is done you should find it in the list of installed snaps together with its version number, revision and developer using:

```
$ snap list

```

You can also sideload snaps from your local hard drive with:

```
# snap install --dangerous */path/to/snap*

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

## Support

Arch Linux related mailing lists and other official Arch Linux support channels aren't an appropriate place to request help with snaps on Arch Linux. An appropriate place to ask for support is the [Snapcraft forum](https://forum.snapcraft.io).

## See also

*   [arstechnica article](http://arstechnica.com/information-technology/2016/06/goodbye-apt-and-yum-ubuntus-snap-apps-are-coming-to-distros-everywhere/) (06/16) about Ubuntu snaps becoming available for Arch and other distros