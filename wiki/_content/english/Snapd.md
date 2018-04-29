Related articles

*   [Flatpak](/index.php/Flatpak "Flatpak")

[snapd](https://github.com/snapcore/snapd) is a REST API daemon for managing snap packages ("snaps"). Users can interact with it by using the *snap* client, which is part of the same package.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Finding](#Finding)
    *   [3.2 Installing](#Installing)
    *   [3.3 Updating](#Updating)
    *   [3.4 Removing](#Removing)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Classic snaps](#Classic_snaps)
*   [5 Support](#Support)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [snapd](https://aur.archlinux.org/packages/snapd/) or the [snapd-git](https://aur.archlinux.org/packages/snapd-git/) package.

**Tip:** `snapd` installs a script in `/etc/profile.d/snapd.sh` to export the paths of binaries installed with the snapd package and desktop entries. Reboot once to make this change take effect.

## Configuration

To launch the `snapd` daemon when *snap* tries to use it, [start](/index.php/Start "Start") and/or [enable](/index.php/Enable "Enable") the `snapd.socket`.

## Usage

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

This requires root privileges. Per user installation of snaps is not possible, yet. This will download the snap into `/var/lib/snapd/snaps` and mount it to `/var/lib/snapd/snap/*snapname*` to make it available to the system.

It will also create mount units for each snap and add them to `/etc/systemd/system/multi-user.target.wants/` as symlinks to make all snaps available when the system is booted. Once that is done you should find it in the list of installed snaps together with its version number, revision and developer using:

```
$ snap list

```

You can also sideload snaps from your local hard drive with:

```
# snap install --dangerous */path/to/snap*

```

### Updating

To update your snaps manually use:

```
# snap refresh

```

Snaps are refreshed automatically according to snap `refresh.timer` setting.

To view the next/last refresh times use:

```
# snap refresh --time

```

To set a different refresh time, eg. twice a day:

```
# snap set core refresh.timer=0:00~24:00/2

```

See [system options documentation page](https://forum.snapcraft.io/t/system-options/87) for details on customizing the refresh time.

### Removing

Snaps can be removed by executing:

```
# snap remove *snapname*

```

## Tips and tricks

### Classic snaps

Some snaps (e.g. Skype and Pycharm) use classic confinement. However, classic confinement requires the `/snap` directory, which is not FHS-compliant. Therefore, the snapd package doesn't ship this directory. However, if the user wants to, they can manually create a symlink from `/snap` to `/var/lib/snapd/snap`, to allow the installation of classic snaps:

```
# ln -s /var/lib/snapd/snap /snap

```

## Support

Arch Linux related mailing lists and other official Arch Linux support channels aren't an appropriate place to request help with snaps on Arch Linux. An appropriate place to ask for support is the [Snapcraft forum](https://forum.snapcraft.io).

## See also

*   [Official site](https://snapcraft.io/)
*   [GitHub repository](https://github.com/snapcore/snapd)
*   [arstechnica article](http://arstechnica.com/information-technology/2016/06/goodbye-apt-and-yum-ubuntus-snap-apps-are-coming-to-distros-everywhere/) (06/16) about Ubuntu snaps becoming available for Arch and other distros