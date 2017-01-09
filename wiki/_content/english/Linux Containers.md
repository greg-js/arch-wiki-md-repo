Linux Containers (LXC) is an operating-system-level virtualization method for running multiple isolated Linux systems (containers) on a single control host (LXC host). It does not provide a virtual machine, but rather provides a virtual environment that has its own CPU, memory, block I/O, network, etc. space and the resource control mechanism. This is provided by [namespaces](https://en.wikipedia.org/wiki/Linux_namespaces "wikipedia:Linux namespaces") and [cgroups](/index.php/Cgroups "Cgroups") features in Linux kernel on LXC host. It is similar to a chroot, but offers much more isolation.

Alternatives for using containers are [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") and [docker](/index.php/Docker "Docker").

## Contents

*   [1 Setup](#Setup)
    *   [1.1 Required software](#Required_software)
    *   [1.2 Host network configuration](#Host_network_configuration)
    *   [1.3 Container creation](#Container_creation)
    *   [1.4 Container configuration](#Container_configuration)
        *   [1.4.1 Basic config with networking](#Basic_config_with_networking)
        *   [1.4.2 Xorg program considerations (optional)](#Xorg_program_considerations_.28optional.29)
        *   [1.4.3 OpenVPN considerations](#OpenVPN_considerations)
*   [2 Managing Containers](#Managing_Containers)
    *   [2.1 Basic usage](#Basic_usage)
    *   [2.2 Advanced usage](#Advanced_usage)
        *   [2.2.1 LXC clones](#LXC_clones)
*   [3 Running Xorg programs](#Running_Xorg_programs)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 root login fails](#root_login_fails)
    *   [4.2 no network-connection with veth in container config](#no_network-connection_with_veth_in_container_config)
*   [5 See also](#See_also)

## Setup

### Required software

Install the [lxc](https://www.archlinux.org/packages/?name=lxc) and [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) packages.

Verify that the running kernel is properly configured to run a container:

```
$ lxc-checkconfig

```

Due to security concerns, the default Arch kernel does **not** ship with the ability to run containers as an unprivileged user; therefore, it is normal to see a **missing** status for "User namespaces" when running the check. See [FS#36969](https://bugs.archlinux.org/task/36969) for this feature request.

### Host network configuration

LXCs support different virtual network types and devices (see [lxc.container.conf(5)](https://linuxcontainers.org/lxc/manpages//man5/lxc.container.conf.5.html)). A bridge device on the host is required for most types of virtual networking. Users are referred to the [Network bridge](/index.php/Network_bridge "Network bridge") article.

### Container creation

Select a template from `/usr/share/lxc/templates` that matches the target distro to containerize. Users wishing to containerize non-Arch distros will need additional packages on the host depending on the target distro:

*   Debian-based: [debootstrap](https://www.archlinux.org/packages/?name=debootstrap)
*   Fedora-based: [yum](https://aur.archlinux.org/packages/yum/)

Run `lxc-create` to create the container, which installs the root filesystem of the LXC to `/var/lib/lxc/CONTAINER_NAME/rootfs` by default. Example creating an Arch Linux LXC named "playtime":

```
# lxc-create -n playtime -t /usr/share/lxc/templates/lxc-archlinux

```

**Tip:** Users may optionally install [haveged](https://www.archlinux.org/packages/?name=haveged) and [start](/index.php/Start "Start") `haveged.service` to avoid a perceived hang during the setup process while waiting for system entropy to be seeded. Without it, the generation of private/GPG keys can add a lengthy wait to the process.

**Tip:** Users of [Btrfs](/index.php/Btrfs "Btrfs") can append `-B btrfs` to create a Btrfs subvolume for storing containerized rootfs. This comes in handy if cloning containers with the help of `lxc-clone` command. [ZFS](/index.php/ZFS "ZFS") users may use `-B zfs`, correspondingly.

**Tip:** As of July 2015, creating an empty container using `-t none` does not work, see the [bug report](https://bugs.launchpad.net/bugs/1466458). As a workaround one can use `-t /bin/true`.

### Container configuration

#### Basic config with networking

System resources to be virtualized/isolated when a process is using the container are defined in `/var/lib/lxc/CONTAINER_NAME/config`. By default, the creation process will make a minimum setup without networking support. Below is an example config with networking:

 `/var/lib/lxc/playtime/config` 
```
# Template used to create this container: /usr/share/lxc/templates/lxc-archlinux
# Parameters passed to the template:
# For additional config options, please look at lxc.container.conf(5)

## default values
lxc.rootfs = /var/lib/lxc/playtime/rootfs
lxc.utsname = playtime
lxc.arch = x86_64
lxc.include = /usr/share/lxc/config/archlinux.common.conf

## network
lxc.network.type = veth
lxc.network.link = br0
lxc.network.flags = up
lxc.network.ipv4 = 192.168.0.3/24
lxc.network.ipv4.gateway = 192.168.0.1
lxc.network.name = eth0

## mounts
## specify shared filesystem paths in the format below
## make sure that the mount point exists on the lxc
#lxc.mount.entry = /mnt/data/share mnt/data none bind 0 0
#
# if running the same Arch linux on the same architecture it may be
# adventitious to share the package cache directory
#lxc.mount.entry = /var/cache/pacman/pkg var/cache/pacman/pkg none bind 0 0

```

#### Xorg program considerations (optional)

In order to run programs on the host's display, some bind mounts need to be defined so that the containerized programs can access the host's resources. Add the following section to `/var/lib/lxc/playtime/config`:

```
## for xorg
## fix overmounting see: [https://github.com/lxc/lxc/issues/434](https://github.com/lxc/lxc/issues/434)
lxc.mount.entry = tmpfs tmp tmpfs defaults
lxc.mount.entry = /dev/dri dev/dri none bind,optional,create=dir
lxc.mount.entry = /dev/snd dev/snd none bind,optional,create=dir
lxc.mount.entry = /tmp/.X11-unix tmp/.X11-unix none bind,optional,create=dir
lxc.mount.entry = /dev/video0 dev/video0 none bind,optional,create=file

```

If you still get a permission denied error in your LXC guest, then you may need to call `xhost +` in your host to allow the guest to connect to the host's display server. Take note of the security concerns of opening up your display server by doing this.

#### OpenVPN considerations

Users wishing to run [OpenVPN](/index.php/OpenVPN "OpenVPN") within the container should read the [OpenVPN (client) in Linux containers](/index.php/OpenVPN_(client)_in_Linux_containers "OpenVPN (client) in Linux containers") article.

## Managing Containers

### Basic usage

To list all installed LXC containers:

```
# lxc-ls -f

```

Systemd can be used to [start](/index.php/Start "Start") and to [stop](/index.php/Stop "Stop") LXCs via `lxc@CONTAINER_NAME.service`. [Enable](/index.php/Enable "Enable") `lxc@CONTAINER_NAME.service` to have it start when the host system boots.

Users can also start/stop LXCs without systemd. Start a container:

```
# lxc-start -n CONTAINER_NAME

```

Stop a container:

```
# lxc-stop -n CONTAINER_NAME

```

To login into a container:

```
# lxc-console -n CONTAINER_NAME

```

Once logged, treat the container like any other linux system, set the root password, create users, install packages, etc.

To attach to a container:

```
# lxc-attach -n CONTAINER_NAME

```

It works nearly the same as lxc-console, but you are automatically accessing root prompt inside the container, bypassing login.

### Advanced usage

#### LXC clones

Users with a need to run multiple containers can simplify administrative overhead (user management, system updates, etc.) by using snapshots. The strategy is to setup and keep up-to-date a single base container, then, as needed, clone (snapshot) it. The power in this strategy is that the disk space and system overhead are truly minimized since the snapshots use an overlayfs mount to only write out to disk, only the differences in data. The base system is read-only but changes to it in the snapshots are allowed via the overlayfs.

One caveat to this setup is that the base lxc cannot be running when snapshots are taken.

For example, setup a container as outlined above. We'll call it "base" for the purposes of this guide. Now create 2 snapshots of "base" which we'll call "snap1" and "snap2" with these commands:

```
# lxc-copy -n base -N snap1 -B overlayfs -s
# lxc-copy -n base -N snap2 -B overlayfs -s

```

**Note:** If a static IP was defined for the "base" lxc, that will need to manually changed in the config for "snap1" and for "snap2" before starting them. If the process is to be automated, a script using sed can do this automatically although this is beyond the scope of this wiki section.

The snapshots can be started/stopped like any other container. Users can optionally destroy the snapshots and all new data therein with the following command. Note that the underlying "base" lxc is untouched:

```
# lxc-destroy -n snap1 -f

```

## Running Xorg programs

Either attach to or [SSH](/index.php/SSH "SSH") into the target container and prefix the call to the program with the DISPLAY ID of the host's X session. For most simple setups, the display is always 0.

An example of running Firefox from the container in the host's display:

```
$ DISPLAY=:0 firefox

```

Alternatively, to avoid directly attaching to or connecting to the container, the following can be used on the host to automate the process:

```
# lxc-attach -n playtime --clear-env -- sudo -u YOURUSER env DISPLAY=:0 firefox

```

## Troubleshooting

### root login fails

If you get the following error when you try to login using lxc-console:

```
login: root
Login incorrect

```

And the container's `journalctl` shows:

```
pam_securetty(login:auth): access denied: tty 'pts/0' is not secure !

```

Add `pts/0` to the list of terminal names in `/etc/securetty` on the **container** filesystem, see [[1]](http://unix.stackexchange.com/questions/41840/effect-of-entries-in-etc-securetty/41939#41939). You can also opt to delete `/etc/securetty` on the **container** to allow always root to login, see [[2]](https://github.com/systemd/systemd/issues/852).

Alternatively, create a new user in lxc-attach and use it for logging in to the system, then switch to root.

```
# lxc-attach -n playtime
[root@playtime]# useradd -m -Gwheel newuser
[root@playtime]# passwd newuser
[root@playtime]# passwd root
[root@playtime]# exit
# lxc-console -n playtime
[newuser@playtime]$ su

```

### no network-connection with veth in container config

If you can't access your LAN or WAN with a networking interface configured as **veth** and setup through `/etc/lxc/*containername*/config`. If the virtual interface gets the ip assigned and should be connected to the network correctly.

```
ip addr show veth0 
inet 192.168.1.111/24

```

You may disable all the relevant static ip formulas and try setting the ip through the booted container-os like you would normaly do.

Example `*container*/config`

```
...
lxc.network.type = veth
lxc.network.name = veth0
lxc.network.flags = up
lxc.network.link = `bridge`
...

```

And then assign your IP through your preferred method **inside** the container, see also [Network configuration#Configure the IP address](/index.php/Network_configuration#Configure_the_IP_address "Network configuration").

## See also

*   [LXC 1.0 Blog Post Series](https://www.stgraber.org/2013/12/20/lxc-1-0-blog-post-series/)
*   [LXC@developerWorks](http://www.ibm.com/developerworks/linux/library/l-lxc-containers/)
*   [Docker Installation on ArchLinux](http://docs.docker.io/en/latest/installation/archlinux/)