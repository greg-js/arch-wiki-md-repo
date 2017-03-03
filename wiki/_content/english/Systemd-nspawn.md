*systemd-nspawn* is like the [chroot](/index.php/Chroot "Chroot") command, but it is a *chroot on steroids*.

*systemd-nspawn* may be used to run a command or OS in a light-weight namespace container. It is more powerful than [chroot](/index.php/Chroot "Chroot") since it fully virtualizes the file system hierarchy, as well as the process tree, the various IPC subsystems and the host and domain name.

*systemd-nspawn* limits access to various kernel interfaces in the container to read-only, such as `/sys`, `/proc/sys` or `/sys/fs/selinux`. Network interfaces and the system clock may not be changed from within the container. Device nodes may not be created. The host system cannot be rebooted and kernel modules may not be loaded from within the container.

This mechanism differs from [Lxc-systemd](/index.php/Lxc-systemd "Lxc-systemd") or [Libvirt](/index.php/Libvirt "Libvirt")-lxc, as it is a much simpler tool to configure.

## Contents

*   [1 Installation](#Installation)
*   [2 Examples](#Examples)
    *   [2.1 Create and boot a minimal Arch Linux distribution in a container](#Create_and_boot_a_minimal_Arch_Linux_distribution_in_a_container)
        *   [2.1.1 Bootstrap Arch Linux i686 inside x86_64 host](#Bootstrap_Arch_Linux_i686_inside_x86_64_host)
    *   [2.2 Create a Debian or Ubuntu environment](#Create_a_Debian_or_Ubuntu_environment)
    *   [2.3 Enable container on boot](#Enable_container_on_boot)
    *   [2.4 Build and test packages](#Build_and_test_packages)
*   [3 Management](#Management)
    *   [3.1 machinectl](#machinectl)
    *   [3.2 systemd toolchain](#systemd_toolchain)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Use an X environment](#Use_an_X_environment)
    *   [4.2 Run Firefox](#Run_Firefox)
    *   [4.3 Access host filesystem](#Access_host_filesystem)
    *   [4.4 Configure networking](#Configure_networking)
        *   [4.4.1 nsswitch.conf](#nsswitch.conf)
        *   [4.4.2 Use host networking](#Use_host_networking)
        *   [4.4.3 Virtual Ethernet interfaces](#Virtual_Ethernet_interfaces)
    *   [4.5 Run on a non-systemd system](#Run_on_a_non-systemd_system)
    *   [4.6 Specify per-container settings](#Specify_per-container_settings)
    *   [4.7 Use Btrfs subvolume as container root](#Use_Btrfs_subvolume_as_container_root)
    *   [4.8 Use temporary Btrfs snapshot of container](#Use_temporary_Btrfs_snapshot_of_container)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 root login fails](#root_login_fails)
    *   [5.2 Unable to upgrade some packages on the container](#Unable_to_upgrade_some_packages_on_the_container)
*   [6 See also](#See_also)

## Installation

*systemd-nspawn* is part of and packaged with [systemd](https://www.archlinux.org/packages/?name=systemd).

## Examples

### Create and boot a minimal Arch Linux distribution in a container

First install [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts).

Next, create a directory to hold the container. In this example we will use `~/MyContainer`.

Next, we use pacstrap to install a basic arch-system into the container. At minimum we need to install the [base](https://www.archlinux.org/groups/x86_64/base/) group.

```
# pacstrap -i -c -d ~/MyContainer base [additional pkgs/groups]

```

**Tip:** The `-i` option will **avoid** auto-confirmation of package selection. As you do not need to install the Linux kernel in the container, you can remove it from the package list selection to save space. See [Pacman#Usage](/index.php/Pacman#Usage "Pacman").

**Note:** The package [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) required by [linux](https://www.archlinux.org/packages/?name=linux), which is included in the [base](https://www.archlinux.org/groups/x86_64/base/) group and isn't necessary to run the container, causes some issues to `systemd-tmpfiles-setup.service` during the booting process with `systemd-nspawn`. It's possible to install the [base](https://www.archlinux.org/groups/x86_64/base/) group but excluding the [linux](https://www.archlinux.org/packages/?name=linux) package and its dependencies when building the container with `# pacstrap -c -d ~/MyContainer base --ignore linux [additional pkgs/groups]`. The `--ignore` flag will be simply passed to [pacman](https://www.archlinux.org/packages/?name=pacman). See [FS#46591](https://bugs.archlinux.org/task/46591) for more information.

Once your installation is finished, boot into the container:

```
# systemd-nspawn -b -D ~/MyContainer

```

The `-b` option will boot the container (i.e. run `systemd` as PID=1), instead of just running a shell, and `-D` specifies the directory that becomes the container's root directory.

After the container starts, log in as "root" with no password.

The container can be powered off by running `poweroff` from within the container. From the host, containers can be controlled by the [machinectl](#machinectl) tool.

**Note:** To terminate the *session* from within the container, hold `Ctrl` and rapidly press `]` three times. Non US keyboard will use `%` instead of `]`

#### Bootstrap Arch Linux i686 inside x86_64 host

It is possible to install a minimal i686 Arch Linux inside a subdirectory and use it as systemd-nspawn container instead of [chroot](/index.php/Chroot "Chroot") or [virtualization](/index.php/Virtualization "Virtualization"). This is useful for testing `PKGBUILD` compilation for i686 and other tasks. Make sure you use a `pacman.conf` **without** `multilib` repository.

```
 # pacman_conf=/tmp/pacman.conf # this is pacman.conf without multilib
 # mkdir /mnt/i686-archlinux
 # linux32 pacstrap -C "$pacman_conf" -di /mnt/i686-archlinux base base-devel

```

You may deselect `linux` from `base` group, since the resulting bootstrap directory is not meant to be booted on real or virtualized hardware.

To start the resulting i686 Arch Linux systemd-nspawn instance, just issue the following command.

```
 # linux32 systemd-nspawn -D /mnt/i686-archlinux

```

### Create a Debian or Ubuntu environment

Install [debootstrap](https://www.archlinux.org/packages/?name=debootstrap), [gnupg1](https://aur.archlinux.org/packages/gnupg1/), and one or both of [debian-archive-keyring](https://aur.archlinux.org/packages/debian-archive-keyring/) and [ubuntu-keyring](https://aur.archlinux.org/packages/ubuntu-keyring/) (obviously install the keyrings for the distros you want).

**Note:** systemd-nspawn requires that the os in the container has systemd running as PID 1, this means Ubuntu before 15.04 will not work out of the box and requires additional configuration to switch from upstart to systemd.

From there it's rather easy to setup Debian or Ubuntu environments:

```
# cd /var/lib/machines
# debootstrap <codename> myContainer <repository-url>

```

For Debian valid code names are either the rolling names like "stable" and "testing" or release names like "stretch" and "sid", for Ubuntu the code name like "wily" or "hardy" should be used. A complete list of codenames is in `/usr/share/debootstrap/scripts`. In case of a Debian image the "repository-url" can be `[http://deb.debian.org/debian/](http://deb.debian.org/debian/)`.

Unlike Arch, Debian and Ubuntu will not let you login without a password on first login. To set the root password login without the '-b' option and set a password:

```
# systemd-nspawn -D myContainer
# passwd
# logout

```

### Enable container on boot

When using a container frequently, you may want to start it on boot.

First [enable](/index.php/Enable "Enable") the `machines.target` target, then `systemd-nspawn@*myContainer*.service`, where `myContainer` is an nspawn container in `/var/lib/machines`.

**Tip:**

*   Symbolic links to containers in `/var/lib/machines` currently do not work, see [[1]](https://github.com/systemd/systemd/issues/2001).
*   To customize the startup of a container, [edit](/index.php/Edit "Edit") the `systemd-nspawn@*myContainer*` unit instance. See `systemd-nspawn(1)` for all options.

### Build and test packages

See [Creating packages for other distributions](/index.php/Creating_packages_for_other_distributions "Creating packages for other distributions") for example uses.

## Management

### machinectl

**Note:** The *machinectl* tool requires [systemd](/index.php/Systemd "Systemd") and [dbus](https://www.archlinux.org/packages/?name=dbus) to be installed in the container. See [[2]](https://github.com/systemd/systemd/issues/685) for detailed discussion.

Managing your containers is essentially done with the `machinectl` command. See `machinectl(1)` for details.

Examples:

Spawn a new shell inside a running container:

```
$ machinectl login *MyContainer*

```

Show detailed information about a container:

```
$ machinectl status *MyContainer*

```

Reboot a container:

```
$ machinectl reboot *MyContainer*

```

Poweroff a container:

```
$ machinectl poweroff *MyContainer*

```

**Tip:** Poweroff and reboot operations can be performed from within a container session using the *systemctl* `poweroff` or `reboot` commands.

Download an image:

```
# machinectl pull-tar *URL* *name*

```

### systemd toolchain

Much of the core systemd toolchain has been updated to work with containers. Tools that do usually provide a `-M, --machine=` option which will take a container name as argument.

Examples:

See journal logs for a particular machine:

```
$ journalctl -M *MyContainer*

```

Show control group contents:

```
$ systemd-cgls -M *MyContainer*

```

See startup time of container:

```
$ systemd-analyze -M *MyContainer*

```

For an overview of resource usage:

```
$ systemd-cgtop

```

## Tips and tricks

### Use an X environment

See [Xhost](/index.php/Xhost "Xhost") and [Change root#Run graphical applications from chroot](/index.php/Change_root#Run_graphical_applications_from_chroot "Change root").

You will need to set the `DISPLAY` environment variable inside your container session to connect to the external X server.

X stores some required files in the `/tmp` directory. In order for your container to display anything, it needs access to those files. To do so, append the `--bind=/tmp/.X11-unix:/tmp/.X11-unix` option when starting the container.

### Run Firefox

See [Firefox tweaks](/index.php/Firefox_tweaks#Run_Firefox_inside_an_nspawn_container "Firefox tweaks").

### Access host filesystem

See `--bind` and `--bind-ro` in `man systemd-nspawn`.

If both the host and the container are Arch Linux, then one could, for example, share the pacman cache:

```
# systemd-nspawn --bind=/var/cache/pacman/pkg

```

### Configure networking

For the most simple setup, allowing outgoing connections to the internet, you can use [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") for network management and DHCP and `systemd-resolved` for DNS.

```
# systemctl enable --now systemd-networkd systemd-resolved
# ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf # let systemd-resolved manage /etc/resolv.conf

```

This assumes you have started `systemd-nspawn` with the `-n` switch, creating a virtual Ethernet link to the host.

Instead of using `systemd-resolved` you can also manually [edit](/index.php/Textedit "Textedit") your container's `/etc/resolv.conf` by adding your DNS server's IP address.

Note the canonical [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") host and container .network files are from [https://github.com/systemd/systemd/tree/master/network](https://github.com/systemd/systemd/tree/master/network) .

See [systemd-networkd#Usage with containers](/index.php/Systemd-networkd#Usage_with_containers "Systemd-networkd") for more complex examples.

#### nsswitch.conf

To make it easier to connect to a container from the host, you can enable local DNS resolution for container names. In `/etc/nsswitch.conf`, add `mymachines` to the `hosts:` section, e.g.

```
hosts: files mymachines dns myhostname

```

Then, any DNS lookup for hostname `foo` on the host will first consult `/etc/hosts`, then the names of local containers, then upstream DNS etc.

#### Use host networking

To disable private networking used by containers started with `machinectl start MyContainer`, [edit](/index.php/Edit "Edit") the configuration of `systemd-nspawn@.service` with `systemctl edit systemd-nspawn@.service` and set the `ExecStart=` option without the `--network-veth` parameter unlike the original service:

 `/etc/systemd/system/systemd-nspawn@.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/systemd-nspawn --quiet --keep-unit --boot --link-journal=try-guest --machine=%I

```

The newly started containers will use the hosts networking.

#### Virtual Ethernet interfaces

If a container is started with `systemd-nspawn ... -n`, systemd will automatically create one virtual Ethernet interface on the host, and one in the container, connected by a virtual Ethernet cable.

If the name of the container is `foo`, the name of the virtual Ethernet interface on the host is `ve-foo`. The name of the virtual Ethernet interface in the container is always `host0`.

When examining the interfaces with `ip link`, interface names will be shown with a suffix, such as `ve-foo@if2` and `host0@if9`. The `@ifN` is not actually part of the name of the interface; instead, `ip link` appends this information to indicate which "slot" the virtual Ethernet cable connects to on the other end.

For example, a host virtual Ethernet interface shown as `ve-foo@if2` will connect to container `foo`, and inside the container to the second network interface -- the one shown with index 2 when running `ip link` inside the container. Similarly, in the container, the interface named `host0@if9` will connect to the 9th slot on the host.

### Run on a non-systemd system

See [Init#systemd-nspawn](/index.php/Init#systemd-nspawn "Init").

### Specify per-container settings

To specify per-container settings and not overrides for all (e.g. bind a directory to only one container)[[3]](https://github.com/systemd/systemd/issues/3442#issuecomment-223837408), the ".nspawn" file definition can be used [[4]](https://www.freedesktop.org/software/systemd/man/systemd.nspawn.html#)

```
 man systemd.nspawn

```

### Use Btrfs subvolume as container root

To use a [Btrfs subvolume](/index.php/Btrfs#Subvolumes "Btrfs") as a template for the container's root, use the `--template` flag. This takes a snapshot of the subvolume and populates the root directory for the container with it.

**Note:** If the template path specified is not the root of a subvolume, the **entire** tree is copied. This will be very time consuming.

For example, to use a snapshot located at `/.snapshots/403/snapshot`:

```
# systemd-nspawn --template=/.snapshots/403/snapshots -b -D *my-container*

```

where `*my-container*` is the name of the directory that will be created for the container. After powering off, the newly created subvolume is retained.

### Use temporary Btrfs snapshot of container

One can use the `--ephemeral` or `-x` flag to create a temporary btrfs snapshot of the container and use it as the container root. Any changes made while booted in the container will be lost. For example:

```
# systemd-nspawn -D *my-container* -xb

```

where *my-container* is the directory of an **existing** container or system. For example, if `/` is a btrfs subvolume one could create an ephemeral container of the currently running host system by doing:

```
# systemd-nspawn -D / -xb 

```

After powering off the container, the btrfs subvolume that was created is immediately removed.

## Troubleshooting

### root login fails

If you get the following error when you try to login (i.e. using `machinectl login <name>`):

```
arch-nspawn login: root
Login incorrect

```

And `journalctl` shows:

```
pam_securetty(login:auth): access denied: tty 'pts/0' is not secure !

```

Add `pts/0` to the list of terminal names in `/etc/securetty` on the **container** filesystem, see [[5]](http://unix.stackexchange.com/questions/41840/effect-of-entries-in-etc-securetty/41939#41939). You can also opt to delete `/etc/securetty` on the **container** to allow root to login to any tty, see [[6]](https://github.com/systemd/systemd/issues/852).

### Unable to upgrade some packages on the container

It can sometimes be impossible to upgrade some packages on the container, [filesystem](https://www.archlinux.org/packages/?name=filesystem) being a perfect example. The issue is due to `/sys` being mounted as Read Only. The workaround is to remount the directory in Read Write when running `mount -o remount,rw -t sysfs sysfs /sys`, do the upgrade then reboot the container.

## See also

*   [Automatic console login](/index.php/Getty#Nspawn_console "Getty")
*   [machinectl man page](http://www.freedesktop.org/software/systemd/man/machinectl.html)
*   [systemd-nspawn man page](http://www.freedesktop.org/software/systemd/man/systemd-nspawn.html)
*   [Creating containers with systemd-nspawn](http://lwn.net/Articles/572957/)
*   [Presentation by Lennart Pottering on systemd-nspawn](https://www.youtube.com/results?search_query=systemd-nspawn&aq=f)
*   [Running Firefox in a systemd-nspawn container](http://dabase.com/e/12009/)