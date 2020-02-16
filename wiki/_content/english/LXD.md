**[LXD](https://linuxcontainers.org/lxd/)** is a container and virtual-machine "hypervisor" and a new user experience for [Linux Containers](/index.php/Linux_Containers "Linux Containers").

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
*   [2 Usage](#Usage)
    *   [2.1 Create container](#Create_container)
    *   [2.2 LXD Networking](#LXD_Networking)
    *   [2.3 lxd-agent inside VM](#lxd-agent_inside_VM)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Check kernel config](#Check_kernel_config)
    *   [3.2 Launching container without CONFIG_USER_NS](#Launching_container_without_CONFIG_USER_NS)
    *   [3.3 Resource limits are not applied when viewed from inside a container](#Resource_limits_are_not_applied_when_viewed_from_inside_a_container)
    *   [3.4 Starting a VM fails](#Starting_a_VM_fails)
    *   [3.5 No IPv4 with systemd-networkd](#No_IPv4_with_systemd-networkd)
*   [4 Uninstall](#Uninstall)
*   [5 See also](#See_also)

## Setup

### Required software

Install [LXC](/index.php/LXC "LXC") and the [lxd](https://www.archlinux.org/packages/?name=lxd) package, then [start](/index.php/Start "Start") `lxd.service`.

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

**Warning:** Anyone added to the `lxd` group is root equivalent. More information [here](https://github.com/lxc/lxd#security) and [here](https://bugs.launchpad.net/ubuntu/+source/lxd/+bug/1829071).

## Usage

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

### lxd-agent inside VM

Inside VMs `lxd-agent` is not installed by default on the OS. This can be installed on the host by mounting a `9p` network share. This requires console access with a valid user.

```
   $ lxc console v1
   To detach from the console, press: <ctrl>+a q

   Ubuntu 18.04.3 LTS v1 ttyS0

   v1 login: ubuntu
   Password: 
   Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-74-generic x86_64)

   ubuntu@v1:~$ sudo -i
   root@v1:~# mount -t 9p config /mnt/
   root@v1:~# cd /mnt/
   root@v1:/mnt# ./install.sh 
   Created symlink /etc/systemd/system/multi-user.target.wants/lxd-agent.service → /lib/systemd/system/lxd-agent.service.
   Created symlink /etc/systemd/system/multi-user.target.wants/lxd-agent-9p.service → /lib/systemd/system/lxd-agent-9p.service.

   LXD agent has been installed, reboot to confirm setup.
   To start it now, unmount this filesystem and run: systemctl start lxd-agent-9p lxd-agent
   root@v1:/mnt# reboot

```

Afterwards the `lxd-agent` is available and `lxc exec` works inside the VM.

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

### Resource limits are not applied when viewed from inside a container

The service lxcfs (found in the Community repository) needs to be installed and started :

```
$ systemctl start lxcfs

```

lxd will need to be restarted. Enable lxcfs for the service to be started at boot time.

### Starting a VM fails

Arch Linux does not distribute secure boot signed ovmf firmware, to boot VMs you need to disable secure boot for the time being.

```
$ lxc launch ubuntu:18.04 test-vm --vm -c security.secureboot=false

```

This can also be added to the default profile.

### No IPv4 with systemd-networkd

Starting with version version 244.1, systemd detects if `/sys` is writable by containers. If it is, udev is automatically started and breaks IPv4 in unprivileged containers. See [commit bf331d8](https://github.com/systemd/systemd-stable/commit/96d7083c5499b264ecebd6a30a92e0e8fda14cd5) and [discussion on linuxcontainers](https://discuss.linuxcontainers.org/t/no-ipv4-on-arch-linux-containers/6395).

On containers created past 2020, there should already be a `systemd.networkd.service` override to work around this issue, create it if it is not:

 `/etc/systemd/system/systemd-networkd.service.d/lxc.conf` 
```
[Service]
BindReadOnlyPaths=/sys
```

You could also work around this issue by setting `raw.lxc: lxc.mount.auto = proc:rw sys:ro` in the profile of the container to ensure `/sys` is read-only for the entire container, although this may be problematic, as per the linked discussion above.

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