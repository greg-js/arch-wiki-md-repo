Related articles

*   [Flatpak](/index.php/Flatpak "Flatpak")
*   [AppArmor](/index.php/AppArmor "AppArmor")

[Snap](https://snapcraft.io/) is a software deployment and package management system. The packages are called 'snaps' and the tool for using them is 'snapd', which works across a range of Linux distributions and allows, therefore, distro-agnostic upstream software deployment. Snap was originally designed and built by Canonical.

[snapd](https://github.com/snapcore/snapd) is a REST API daemon for managing snap packages. Users can interact with it by using the *snap* client, which is part of the same package.

Snaps can be confined using [AppArmor](/index.php/AppArmor "AppArmor") which is now enabled in the default kernel. Consult relevant wiki pages to find steps for enabling [AppArmor](/index.php/AppArmor "AppArmor") in your system.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Finding](#Finding)
    *   [3.2 Installing](#Installing)
    *   [3.3 Updating](#Updating)
    *   [3.4 Removing](#Removing)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Classic snaps](#Classic_snaps)
    *   [4.2 Confinement](#Confinement)
*   [5 Graphical management](#Graphical_management)
*   [6 Support](#Support)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [snapd](https://aur.archlinux.org/packages/snapd/) or the [snapd-git](https://aur.archlinux.org/packages/snapd-git/) package.

**Tip:** `snapd` installs a script in `/etc/profile.d/snapd.sh` to export the paths of binaries installed with the snapd package and desktop entries. Reboot once to make this change take effect.

Since version 2.36, `snapd` enabled AppArmor support for Arch Linux. In order to use it, you have to enable AppArmor in your system, see [AppArmor#Installation](/index.php/AppArmor#Installation "AppArmor").

**Note:** If AppArmor isn't enabled in your system then all snaps will run in `devel` mode which mean they will have same, unrestricted access to your system as apps installed from Arch Linux repositories.

If you are using [AppArmor](/index.php/AppArmor "AppArmor"):

```
 $ systemctl enable --now apparmor.service
 $ systemctl enable --now snapd.apparmor.service

```

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

### Confinement

When using [AppArmor](/index.php/AppArmor "AppArmor"), snapd (2.36+) will generate the same profiles for snaps as on Ubuntu. The [AppArmor](/index.php/AppArmor "AppArmor") parser is smart enough to drop the rules that are not yet supported by the mainline kernel.

To verify that basic confinement is working, install *hello-world* snap. Then run the following:

```
 $ hello-world.evil
 Hello Evil World!
 This example demonstrates the app confinement
 You should see a permission denied error next
 /snap/hello-world/27/bin/evil: 9: /snap/hello-world/27/bin/evil: cannot create /var/tmp/myevil.txt: Permission denied

```

The denial was caused by AppArmor and should have been logged:

```
 $ dmesg
 ...
 [  +0.000003] audit: type=1327 audit(1540469583.966:257): proctitle=2F62696E2F7368002F736E61702F68656C6C6F2D776F726C642F32372F62696E2F6576696C
 [ +12.268939] audit: type=1400 audit(1540469596.236:258): apparmor="DENIED" operation="open" profile="snap.hello-world.evil" name="/var/tmp/myevil.txt" pid=10835 comm="evil" requested_mask="wc" denied_mask="wc" fsuid=1000 ouid=1000
 [  +0.000006] audit: type=1300 audit(1540469596.236:258): arch=c000003e syscall=2 success=no exit=-13 a0=55d991ba6bc8 a1=241 a2=1b6 a3=55d991ba6be0 items=0 ppid=31349 pid=10835 auid=1000 uid=1000 gid=1000 euid=1000 suid=1000 fsuid=1000 egid=1000 sgid=1000 fsgid=1000 tty=pts2 ses=3 comm="evil" exe="/bin/dash" subj==snap.hello-world.evil (enforce)
 ...

```

If you do not see the denial, verify that the profiles were loaded:

```
  $ sudo aa-status |grep snap.hello-world
    snap.hello-world.env
    snap.hello-world.evil
    snap.hello-world.hello-world
    snap.hello-world.sh

```

Also, you can check what sandbox features are available in the system according to snapd:

```
 $ snap debug sandbox-features
 apparmor:             kernel:caps kernel:domain kernel:file kernel:mount kernel:namespaces kernel:network_v8 kernel:policy kernel:ptrace kernel:query kernel:rlimit kernel:signal parser:unsafe policy:default support-level:partial
 confinement-options:  devmode
 dbus:                 mediated-bus-access
 kmod:                 mediated-modprobe
 mount:                freezer-cgroup-v1 layouts mount-namespace per-snap-persistency per-snap-profiles per-snap-updates per-snap-user-profiles stale-base-invalidation
 seccomp:              bpf-argument-filtering kernel:allow kernel:errno kernel:kill_process kernel:kill_thread kernel:log kernel:trace kernel:trap

```

## Graphical management

Both Gnome Software Center and KDE Discover can provide native snap support with the [gnome-software-snap](https://aur.archlinux.org/packages/gnome-software-snap/) or [discover-snap](https://aur.archlinux.org/packages/discover-snap/) packages.

## Support

Arch Linux related mailing lists and other official Arch Linux support channels aren't an appropriate place to request help with snaps on Arch Linux. An appropriate place to ask for support is the [Snapcraft forum](https://forum.snapcraft.io).

## See also

*   [Official site](https://snapcraft.io/)
*   [GitHub repository](https://github.com/snapcore/snapd)
*   [arstechnica article](http://arstechnica.com/information-technology/2016/06/goodbye-apt-and-yum-ubuntus-snap-apps-are-coming-to-distros-everywhere/) (06/16) about Ubuntu snaps becoming available for Arch and other distros