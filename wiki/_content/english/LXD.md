**[LXD](https://linuxcontainers.org/lxd/)** is a container "hypervisor" and a new user experience for [Linux Containers](/index.php/Linux_Containers "Linux Containers").

Related articles

*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Setup](#Setup)
    *   [1.1 Required software](#Required_software)
    *   [1.2 Alternative installation method](#Alternative_installation_method)
    *   [1.3 Configure LXD](#Configure_LXD)
    *   [1.4 Accessing LXD as a unprivileged user](#Accessing_LXD_as_a_unprivileged_user)
*   [2 Basic usage](#Basic_usage)
    *   [2.1 Create container](#Create_container)
*   [3 Advance usage](#Advance_usage)
    *   [3.1 LXD Networking](#LXD_Networking)
        *   [3.1.1 Example network configuration](#Example_network_configuration)
    *   [3.2 Modify processes and files limit](#Modify_processes_and_files_limit)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Check kernel config](#Check_kernel_config)
    *   [4.2 Launching container without CONFIG_USER_NS](#Launching_container_without_CONFIG_USER_NS)
    *   [4.3 No ipv4 on unprivileged Arch container](#No_ipv4_on_unprivileged_Arch_container)
    *   [4.4 Resource limits are not applied when viewed from inside a container](#Resource_limits_are_not_applied_when_viewed_from_inside_a_container)
*   [5 Uninstall](#Uninstall)
*   [6 See also](#See_also)

## Setup

### Required software

Install [LXC](/index.php/LXC "LXC") and the [lxd](https://aur.archlinux.org/packages/lxd/) package, then [start](/index.php/Start "Start") `lxd.service`.

See [Linux Containers#Enable support to run unprivileged containers (optional)](/index.php/Linux_Containers#Enable_support_to_run_unprivileged_containers_(optional) "Linux Containers") if you want to run *unprivileged* containers. Otherwise see [#Launching container without CONFIG_USER_NS](#Launching_container_without_CONFIG_USER_NS).

### Alternative installation method

An alternative method of installation is via [snapd](/index.php/Snapd "Snapd"), by installing the [snapd](https://aur.archlinux.org/packages/snapd/) package and running:

```
# snap install lxd

```

### Configure LXD

LXD needs to configure a storage pool, and (if you want internet access) network configuration. To do so, run the following as root:

```
# lxd init

```

### Accessing LXD as a unprivileged user

By default the LXD daemon allows users in the `lxd` group access, so add your user to the group:

```
# usermod -a -G lxd <user>

```

## Basic usage

### Create container

LXD has two parts, the daemon (the lxd binary), and the client (the lxc binary). Now that the daemon is all configured and running, you can create a container:

```
$ lxc launch ubuntu:16.04

```

Alternatively, you can also use a remote LXD host as a source of images. One comes pre-configured in LXD, called "images" (images.linuxcontainers.org)

```
$ lxc launch images:centos/7/amd64 centos

```

To create an amd64 Arch container:

```
$ lxc launch images:archlinux/current/amd64 arch

```

## Advance usage

### LXD Networking

LXD uses LXC's networking capabilities. By default it connects containers to the `lxcbr0` network device. Refer to the LXC documentation on [network configuration](/index.php/Linux_Containers#Host_network_configuration "Linux Containers") to set up a bridge for your containers.

If you want to use a different interface than `lxcbr0` edit the default using the lxc command line tool:

```
$ lxc profile edit default

```

An editor will open with a config file that by default contains:

```
name: default
config: {}
devices:
  eth0:
    name: eth0
    nictype: bridged
    parent: lxcbr0
    type: nic

```

You can set the `parent` parameter to whichever bridge you want LXD to attach the containers to by default.

#### Example network configuration

Thanks to @jpic, the LXD package now provides some example networking configuration in `/usr/share/lxd/`. To use this configuration run the following commands:

```
$ ln -s /usr/share/lxd/dnsmasq-lxd.conf /etc/dnsmasq-lxd.conf
$ ln -s /usr/share/lxd/systemd/system/dnsmasq@lxd.service /etc/systemd/system/dnsmasq@lxd.service 
$ ln -s /usr/share/lxd/netctl/lxd  /etc/netctl/lxd
$ ln -s /usr/share/lxd/dbus-1/system.d/dnsmasq-lxd.conf /etc/dbus-1/system.d/dnsmasq-lxd.conf

```

If you use [NetworkManager](/index.php/NetworkManager "NetworkManager"), also symlink the following file:

```
$ ln -s /usr/share/lxd/NetworkManager/dnsmasq.d/lxd.conf /etc/NetworkManager/dnsmasq.d/lxd.conf

```

Change `parent: lxcbr0` to `parent: lxd`:

```
$ lxc profile edit default

```

Finally, [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `dnsmasq@lxd.service` and `netctl@lxd.service`.

If you encounter issue with the provided example configuration, or have suggestions to improve it, please leave a comment on the [lxd](https://aur.archlinux.org/packages/lxd/) page.

### Modify processes and files limit

You may want to increase file descriptor limit or max user processes limit, since default file descriptor limit is 1024 on Arch Linux.

[Edit](/index.php/Edit "Edit") the `lxd.service`:

 `# systemctl edit lxd.service` 
```
[Service]
LimitNOFILE=infinity
LimitNPROC=infinity
TasksMax=infinity
```

## Troubleshooting

### Check kernel config

By default Arch Linux kernel is compiled correctly for Linux Containers and its frontend LXD. However, if you're using a custom kernel, or changed kernel options the kernel might be configured incorrectly. Verify that the running kernel is properly configured to run a container:

```
$ lxc-checkconfig

```

### Launching container without CONFIG_USER_NS

For launching images you must provide `security.privileged=true` during image creation:

```
$ lxc launch ubuntu:16.04 ubuntu -c security.privileged=true

```

Or for already existed image you may edit config:

 `$ lxc config edit ubuntu` 
```
name: ubuntu
profiles:
- default
config:
  ...
  security.privileged: "true"
  ...
devices:
  root:
    path: /
    type: disk
ephemeral: false

```

Or to enable `security.privileged=true` for new containers, edit the config for the default profile:

```
$ lxc profile edit default

```

### No ipv4 on unprivileged Arch container

This was tested and validated on LXD v.2.20\. The container can not start the `systemd-networkd` service so does not get a valid ipv4 address. A work-around was suggested by Stéphane Graber ([Github Issue](https://github.com/lxc/lxd/issues/4071)), execute on the host and restart the container:

```
$ lxc profile set default security.syscalls.blacklist "keyctl errno 38"

```

	stgraber: "The reason is that the networkd systemd unit somehow makes use of the kernel keyring, which doesn't work inside unprivileged containers right now. The line above makes that system call return not-implemented which is enough of a workaround to get things going again."

### Resource limits are not applied when viewed from inside a container

The service lxcfs (found in the Community repository) needs to be installed and started :

```
$ systemctl start lxcfs

```

lxd will need to be restarted. Enable lxcfs for the service to be started at boot time.

## Uninstall

[Stop](/index.php/Stop "Stop") and disable `lxd.service` and `lxd.socket`:

Then uninstall the package via pacman:

```
 # pacman -R lxd

```

If you uninstalled the package without disabling the service, you might have a lingering broken symlink at `/etc/systemd/system/multi-user.wants/lxd.service`.

If you want to remove all data:

```
 # rm -r /var/lib/lxd

```

If you used any of the example networking configs, you should remove those as well.

## See also

*   [Official documentation](https://lxd.readthedocs.io)
*   [The official LXD homepage](https://linuxcontainers.org/lxd/)
*   [The LXD GitHub page](https://github.com/lxc/lxd)