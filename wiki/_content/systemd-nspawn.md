# systemd-nspawn

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [systemd](/index.php/Systemd "Systemd")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")
*   [Docker](/index.php/Docker "Docker")
*   [Lxc-systemd](/index.php/Lxc-systemd "Lxc-systemd")

_systemd-nspawn_ is like the [chroot](/index.php/Chroot "Chroot") command, but it is a _chroot on steroids_.

_systemd-nspawn_ may be used to run a command or OS in a light-weight namespace container. It is more powerful than [chroot](/index.php/Chroot "Chroot") since it fully virtualizes the file system hierarchy, as well as the process tree, the various IPC subsystems and the host and domain name.

_systemd-nspawn_ limits access to various kernel interfaces in the container to read-only, such as `/sys`, `/proc/sys` or `/sys/fs/selinux`. Network interfaces and the system clock may not be changed from within the container. Device nodes may not be created. The host system cannot be rebooted and kernel modules may not be loaded from within the container.

This mechanism differs from [Lxc-systemd](/index.php/Lxc-systemd "Lxc-systemd") or [Libvirt](/index.php/Libvirt "Libvirt")-lxc, as it is a much simpler tool to configure.

## Contents

*   [1 Installation](#Installation)
*   [2 Examples](#Examples)
    *   [2.1 Create and boot a minimal Arch Linux distribution in a container](#Create_and_boot_a_minimal_Arch_Linux_distribution_in_a_container)
    *   [2.2 Enable Container on boot](#Enable_Container_on_boot)
    *   [2.3 Building and Testing packages](#Building_and_Testing_packages)
*   [3 Management](#Management)
    *   [3.1 machinectl](#machinectl)
    *   [3.2 systemd toolchain](#systemd_toolchain)
*   [4 Tips](#Tips)
    *   [4.1 X environment](#X_environment)
    *   [4.2 Run Firefox inside an nspawn container](#Run_Firefox_inside_an_nspawn_container)
    *   [4.3 Networking](#Networking)
        *   [4.3.1 nsswitch.conf](#nsswitch.conf)
        *   [4.3.2 use host networking](#use_host_networking)
        *   [4.3.3 Virtual Ethernet interfaces](#Virtual_Ethernet_interfaces)
    *   [4.4 Running on a non-systemd system](#Running_on_a_non-systemd_system)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 root login fails](#root_login_fails)
    *   [5.2 unable to upgrade some packages on the container](#unable_to_upgrade_some_packages_on_the_container)
*   [6 See also](#See_also)

## Installation

_systemd-nspawn_ is part of and packaged with [systemd](https://www.archlinux.org/packages/?name=systemd).

## Examples

### Create and boot a minimal Arch Linux distribution in a container

First install [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts).

Next, create a directory to hold the container. In this example we will use `~/MyContainer`.

Next, we use pacstrap to install a basic arch-system into the container. At minimum we need to install the [base](https://www.archlinux.org/groups/x86_64/base/) group.

```
# pacstrap -i -c -d ~/MyContainer base [additional pkgs/groups]

```

**Tip:** The `-i` option will **avoid** auto-confirmation of package selection. As you do not need to install the Linux kernel in the container, you can remove it from the package list selection to save space. See [Pacman#Usage](/index.php/Pacman#Usage "Pacman").

**Note:** The package [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) required by [linux](https://www.archlinux.org/packages/?name=linux) which is included in the [base](https://www.archlinux.org/groups/x86_64/base/) group and it isn't necessary to run the container, causes some issues to `systemd-tmpfiles-setup.service` during the booting process with `systemd-nspawn`. It's possible to install the [base](https://www.archlinux.org/groups/x86_64/base/) group but excluding the [linux](https://www.archlinux.org/packages/?name=linux) package and its dependencies when building the container with `# pacstrap -i -c -d ~/MyContainer base --ignore linux [additional pkgs/groups]`. The `--ignore` flag will be simply passed to [pacman](https://www.archlinux.org/packages/?name=pacman). See the next bug report for more information: [https://bugs.archlinux.org/task/46591](https://bugs.archlinux.org/task/46591).

Once your installation is finished, boot into the container:

```
# systemd-nspawn -b -D ~/MyContainer -n

```

The `-b` option will boot the container (i.e. run `systemd` as PID=1), instead of just running a shell. `-D` specifies the directory that becomes the container's root directory and `-n` will set up a private network between host and container.

After the container starts, log in as "root" with no password.

The container can be powered off by running `poweroff` from within the container. From the host, containers can be controlled by the [machinectl](#machinectl) tool.

**Note:** To terminate the _session_ from within the container, hold `Ctrl` and rapidly press `]` three times. Non US keyboard will use `%` instead of `]`

### Enable Container on boot

If you want to use a container frequently, you can have systemd start it on boot. First you have to enable the `systemd` target `machines.target`

```
# systemctl enable machines.target

```

then you can

```
# mv ~/MyContainer /var/lib/machines/MyContainer
# systemctl enable systemd-nspawn@MyContainer.service
# systemctl start systemd-nspawn@MyContainer.service

```

**Note:** _systemd-nspawn@.service_ is a template unit that expects nspawn containers to be under `/var/lib/machines`.

**Tip:**

*   Instead of moving your container, as above, you can just _symlink_ it to where it is expected to be,

```
# ln -s ~/MyContainer /var/lib/machines/MyContainer

```

*   To customize the startup of a container, [edit](/index.php/Systemd#Editing_provided_units "Systemd") the `systemd-nspawn@_MyContainer_` unit instance. See `systemd-nspawn(1)` for all options.

### Building and Testing packages

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Please share how systemd-nspawn fits into your build environment (Discuss in [Talk:Systemd-nspawn#](https://wiki.archlinux.org/index.php/Talk:Systemd-nspawn))

## Management

### machinectl

Managing your containers is essentially done with the `machinectl` command. See `machinectl(1)` for more detail then listed here.

Examples:

*   Spawn a new shell inside a running container: `$ machinectl login MyContainer` 
*   Show detailed information about a container: `$ machinectl status MyContainer` 
*   Reboot a container: `$ machinectl reboot MyContainer` 
*   Poweroff a container: `$ machinectl poweroff MyContainer` 

**Tip:** Poweroff and reboot operations can be performed from within a container session using the _systemctl_ `poweroff` or `reboot` commands.

### systemd toolchain

Much of the core systemd toolchain has been updated to work with containers. Tools that do usually provide a `-M, --machine=` option which will take a container name as argument.

Examples:

*   See journal logs for a particular machine: ` $ journalctl -M MyContainer` 
*   Show control group contents: `$ systemd-cgls -M MyContainer` 
*   See startup time of container: `$ systemd-analyze -M MyContainer` 
*   For an overview of resource usage: `$ systemd-cgtop` 

## Tips

### X environment

See [Xhost](/index.php/Xhost "Xhost") and [Change root#Run graphical applications from chroot](/index.php/Change_root#Run_graphical_applications_from_chroot "Change root").

You will need to set the `DISPLAY` environment variable inside your container session to connect to the external X server.

X stores some required files in the `/tmp` directory. In order for your container to display anything, it needs access to those files. To do so, append the `--bind=/tmp/.X11-unix:/tmp/.X11-unix` option when starting the container.

### Run Firefox inside an nspawn container

See [Firefox tweaks](/index.php/Firefox_tweaks#Run_Firefox_inside_an_nspawn_container "Firefox tweaks").

### Networking

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Systemd-nspawn#](https://wiki.archlinux.org/index.php/Talk:Systemd-nspawn))

Note the canonical [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") host and container .network files are from [https://github.com/systemd/systemd/tree/master/network](https://github.com/systemd/systemd/tree/master/network)

You need to set up the container .network manually after pacstrapping and `# systemctl enable [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")` (your dhcp client) with systemd-nspawn's -n switch to ensure a virtual Ethernet link is setup. Don't forget to set up DNS, e.g. by either 1) edit your container's `/etc/resolv.conf` by adding your DNS server's IP address, or have 2) [systemd-resolved](/index.php?title=Systemd-resolved&action=edit&redlink=1 "Systemd-resolved (page does not exist)") manage `/etc/resolv.conf` for you.

See [systemd-networkd#Usage with containers](/index.php/Systemd-networkd#Usage_with_containers "Systemd-networkd") for more complex examples.

#### nsswitch.conf

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Systemd-nspawn#](https://wiki.archlinux.org/index.php/Talk:Systemd-nspawn))

To make it easier to connect to a container from the host, you can enable local DNS resolution for container names. In `/etc/nsswitch.conf`, add `mymachines` to the `hosts:` section, e.g.

```
hosts: files mymachines dns myhostname

```

Then, any DNS lookup for hostname `foo` on the host will first consult `/etc/hosts`, then the names of local containers, then upstream DNS etc.

#### use host networking

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

### Running on a non-systemd system

See [Init#systemd-nspawn](/index.php/Init#systemd-nspawn "Init").

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

Add `pts/0` to the list of terminal names in `/etc/securetty` on the **container** filesystem, see [[1]](http://unix.stackexchange.com/questions/41840/effect-of-entries-in-etc-securetty/41939#41939). You can also opt to delete `/etc/securetty` on the **container** to allow always root to login, see [[2]](https://github.com/systemd/systemd/issues/852).

### unable to upgrade some packages on the container

It can sometimes be impossible to upgrade some packages on the container, [filesystem](https://www.archlinux.org/packages/?name=filesystem) being a perfect example. The issue is due to `/sys` being mounted as Read Only. The workaround is to remount the directory in Read Write when running `mount -o remount,rw -t sysfs sysfs /sys`, do the upgrade then reboot the container.

## See also

*   [machinectl man page](http://www.freedesktop.org/software/systemd/man/machinectl.html)
*   [systemd-nspawn man page](http://www.freedesktop.org/software/systemd/man/systemd-nspawn.html)
*   [Creating containers with systemd-nspawn](http://lwn.net/Articles/572957/)
*   [Presentation by Lennart Pottering on systemd-nspawn](https://www.youtube.com/results?search_query=systemd-nspawn&aq=f)
*   [Running Firefox in a systemd-nspawn container](http://dabase.com/e/12009/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Systemd-nspawn&oldid=412459](https://wiki.archlinux.org/index.php?title=Systemd-nspawn&oldid=412459)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Virtualization](/index.php/Category:Virtualization "Category:Virtualization")