Related articles

*   [Docker](/index.php/Docker "Docker")
*   [KVM](/index.php/KVM "KVM")
*   [Libvirt](/index.php/Libvirt "Libvirt")
*   [VirtualBox](/index.php/VirtualBox "VirtualBox")

[Vagrant](http://www.vagrantup.com) is a tool for managing and configuring virtualised development environments.

Vagrant has a concept of 'providers', which map to the virtualisation engine and its API. The most popular and well-supported provider is Virtualbox; plugins exist for `libvirt`, `kvm`, `lxc`, `vmware` and more.

Vagrant uses a mostly declarative `Vagrantfile` to define virtualised machines. A single Vagrantfile can define multiple machines.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Plugins](#Plugins)
    *   [2.1 vagrant-libvirt](#vagrant-libvirt)
    *   [2.2 vagrant-lxc](#vagrant-lxc)
    *   [2.3 vagrant-kvm (deprecated)](#vagrant-kvm_(deprecated))
*   [3 Provisioning](#Provisioning)
*   [4 Base Boxes for Vagrant](#Base_Boxes_for_Vagrant)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 No ping between host and vagrant box (host-only networking)](#No_ping_between_host_and_vagrant_box_(host-only_networking))
    *   [5.2 Virtual machine is not network accessible from the Arch host OS](#Virtual_machine_is_not_network_accessible_from_the_Arch_host_OS)
    *   [5.3 'vagrant up' hangs on NFS mounting (Mounting NFS shared folders...)](#'vagrant_up'_hangs_on_NFS_mounting_(Mounting_NFS_shared_folders...))
    *   [5.4 Mounting NFS shared folders: mount.nfs: requested NFS version or transport protocol is not supported](#Mounting_NFS_shared_folders:_mount.nfs:_requested_NFS_version_or_transport_protocol_is_not_supported)
    *   [5.5 Error starting network 'default': internal error: Failed to initialize a valid firewall backend](#Error_starting_network_'default':_internal_error:_Failed_to_initialize_a_valid_firewall_backend)
    *   [5.6 Unable to ssh to vagrant guest](#Unable_to_ssh_to_vagrant_guest)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [vagrant](https://www.archlinux.org/packages/?name=vagrant) package.

## Plugins

Vagrant [has a middleware architecture](https://news.ycombinator.com/item?id=4408754) providing support for powerful plugins.

Plugins can be installed with Vagrant's built-in plugin manager. You can specify multiple plugins to install:

```
$ vagrant plugin install vagrant-vbguest vagrant-share

```

### vagrant-libvirt

This plugin adds a [libvirt](/index.php/Libvirt "Libvirt") provider to Vagrant. [libvirt](/index.php/Libvirt "Libvirt") and related packages (e.g. [QEMU](/index.php/QEMU "QEMU")) must be installed and configured before using the provider.

To install the plugin, make sure [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) is installed and `libvirtd.service` has been [started](/index.php/Started "Started"). Then run

```
$ vagrant plugin install vagrant-libvirt

```

Once the plugin is installed the `libvirt` provider will be available:

```
$ vagrant up --provider=libvirt

```

### vagrant-lxc

First install [lxc](https://www.archlinux.org/packages/?name=lxc) from the official repositories, then:

```
$ vagrant plugin install vagrant-lxc

```

Next, configure lxc as directed in the [official repository](https://github.com/fgrehm/vagrant-lxc/wiki/Usage-on-Arch-Linux-hosts). The plugin can now be used with a `Vagrantfile` like so:

```
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure("2") do |config|

    config.vm.define "main" do |config|
        config.vm.box = 'http://bit.ly/vagrant-lxc-wheezy64-2013-10-23'

        config.vm.provider :lxc do |lxc|
            lxc.customize 'cgroup.memory.limit_in_bytes', '512M'
        end

        config.vm.provision :shell do |shell|
            shell.path = 'provision.sh'
        end
    end
end

```

The `provision.sh` file should be a shell script beside the `Vagrantfile`. Do whatever setup is appropriate; for example, to remove puppet, which is packaged in the above box:

```
rm /etc/apt/sources.list.d/puppetlabs.list
apt-get purge -y puppet facter hiera puppet-common puppetlabs-release ruby-rgen

```

### vagrant-kvm (deprecated)

This plugin supports [KVM](/index.php/KVM "KVM") as the virtualisation provider.

Vagrant installs a self-contained rainbow environment in /opt which interacts with the system Ruby and other libraries in Arch in confusing ways ([Issue with Ruby](https://github.com/adrahon/vagrant-kvm/issues/14), [Issue with Curl library](https://github.com/adrahon/vagrant-kvm/issues/161#issuecomment-38834996)).

Please see and follow [the complete installation guide for Arch Linux](https://github.com/adrahon/vagrant-kvm/wiki/Install_on_ArchLinux) at vagrant-kvm wiki.

## Provisioning

*Provisioners* allow you to automatically install software, alter and automate configurations as part of the vagrant up process. The most common provisioner is [puppet](https://www.archlinux.org/packages/?name=puppet).

## Base Boxes for Vagrant

Here is a list of places to get all sorts of vagrant base boxes for different purposes: development, testing, or even production.

*   The [official Arch Linux vagrant boxes](https://app.vagrantup.com/archlinux/boxes/archlinux). The corresponding [GitHub project](https://github.com/archlinux/arch-boxes) contains the packerfile used for building along with provisioning scripts.

*   A well maintained up-to-date [Arch Linux x86_64](https://github.com/terrywang/vagrantboxes/blob/master/archlinux-x86_64.md) base box for Vagrant.

*   [Vagrant Cloud](https://vagrantcloud.com/) is HashiCorp's official site for Vagrant boxes. You can browse user-submitted boxes or upload your own. A single Vagrant Cloud box can support multiple providers with versioning.

*   [vagrantbox.es](http://vagrantbox.es/)
    A List of vagrant base boxes. Initiated by Gareth Rushgrove [@garethr](https://twitter.com/garethr) hosted on Heroku using Nginx. See the story here: [The Vagrantbox.es Story](http://www.morethanseven.net/2012/07/01/The-vagrantbox.es-story/).

*   Opscode [bento](https://github.com/opscode/bento)
    We all know what bento means in Japanese, right? In this case, they are **NOT** lunch boxes **BUT** extremely useful base boxes which can be used to test cookbooks or private chef (Chef Server and Client). Distributions included: Ubuntu Server, Debian, CentOS, Fedora and FreeBSD.

*   [Puppet Labs Vagrant Boxes](http://puppet-vagrant-boxes.puppetlabs.com/)
    Pre-rolled vagrant boxes, ready for use. Made by the folks at Puppet Labs.

*   [Vagrant Ubuntu Cloud Images](http://cloud-images.ubuntu.com/vagrant/)
    It has been there since Jan, 2013\. For some reason Canonical has NOT officially promoted it yet, may be still in beta. Remember these are vanilla images, NOT very useful without Chef or Puppet.

*   [packer-arch project on Github](https://github.com/elasticdog/packer-arch) provides configuration files to build light Arch Linux Vagrant images from the official iso image, using [packer](https://www.archlinux.org/packages/?name=packer).

## Troubleshooting

### No ping between host and vagrant box (host-only networking)

Sometimes there are troubles with host-only networking not functioning. Host have no ip on vboxnet interface, host cannot ping vagrant boxes and cannot be pinged from them. This is solved by installing good old [net-tools](https://www.archlinux.org/packages/?name=net-tools) as mentioned in [this thread](https://bbs.archlinux.org/viewtopic.php?pid=1178607#p1178607) by kevin1024

### Virtual machine is not network accessible from the Arch host OS

As of version 1.8.4, Vagrant appears to use the deprecated `route` command to configure routing to the virtual network interface which bridges to the virtual machine(s). If `route` is not installed, you will not be able to access the virtual machine from the host OS due to the lack of suitable route. The solution, as mentioned above, is to install the [net-tools](https://www.archlinux.org/packages/?name=net-tools) package, which includes the route command.

### 'vagrant up' hangs on NFS mounting (Mounting NFS shared folders...)

Installing [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) package may solve this problem.

Make sure the connection isn't blocked by [iptables](https://www.archlinux.org/packages/?name=iptables) or [nftables](https://www.archlinux.org/packages/?name=nftables). If you're using [libvirt](/index.php/Libvirt "Libvirt") along with [firewalld](/index.php/Firewalld "Firewalld"), enable `nfs` (`nfs3`), `rpc-bind` and `mountd` for the libvirt zone.

### Mounting NFS shared folders: mount.nfs: requested NFS version or transport protocol is not supported

[Install](/index.php/Install "Install") the [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) package. Enable (v3 and) UDP support by editing `/etc/nfs.conf` and uncommenting the following lines:

```
[nfsd]
vers3=y
udp=y

```

[Restart](/index.php/Restart "Restart") `nfs-server.service` to apply the changes immediately.

### Error starting network 'default': internal error: Failed to initialize a valid firewall backend

Most likely the firewall dependencies were not installed. [Install](/index.php/Install "Install") the [ebtables](https://www.archlinux.org/packages/?name=ebtables) and [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) packages and [restart](/index.php/Restart "Restart") the `libvirtd` systemd service.

### Unable to ssh to vagrant guest

Check that virtualization is enabled in your BIOS. Because vagrant reports that the vm guest is booted, you would think that all was well with virtualization, but some vagrant boxes (e.g. tantegerda1/archlinux) allow you to get all the way to the ssh stage before the lack of cpu virtualization capabilities bites you.

## See also

*   [official Vagrant documentation](http://docs.vagrantup.com/v2/getting-started/project_setup.html)
*   [Wikipedia:Vagrant (software)](https://en.wikipedia.org/wiki/Vagrant_(software) "wikipedia:Vagrant (software)")