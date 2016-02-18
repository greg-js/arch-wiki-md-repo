[Vagrant](http://www.vagrantup.com) is a tool for managing and configuring virtualised development environments.

Vagrant has a concept of 'providers', which map to the virtualisation engine and its API. The most popular and well-supported provider is Virtualbox; plugins exist for `libvirt`, `kvm`, `lxc`, `vmware` and more.

Vagrant uses a mostly declarative `Vagrantfile` to define virtualised machines. A single Vagrantfile can define multiple machines.

See also [Wikipedia:Vagrant (software)](https://en.wikipedia.org/wiki/Vagrant_(software) "wikipedia:Vagrant (software)").

## Contents

*   [1 Installing Vagrant](#Installing_Vagrant)
*   [2 Plugins](#Plugins)
    *   [2.1 vagrant-libvirt](#vagrant-libvirt)
    *   [2.2 vagrant-lxc](#vagrant-lxc)
    *   [2.3 vagrant-kvm (deprecated)](#vagrant-kvm_.28deprecated.29)
*   [3 Provisioning](#Provisioning)
*   [4 Base Boxes for Vagrant](#Base_Boxes_for_Vagrant)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 No ping between host and vagrant box (host-only networking)](#No_ping_between_host_and_vagrant_box_.28host-only_networking.29)
    *   [5.2 'vagrant up' hangs on NFS mounting (Mounting NFS shared folders...)](#.27vagrant_up.27_hangs_on_NFS_mounting_.28Mounting_NFS_shared_folders....29)
*   [6 See also](#See_also)

## Installing Vagrant

Install [vagrant](https://www.archlinux.org/packages/?name=vagrant) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Plugins

Vagrant [has a middleware architecture](https://news.ycombinator.com/item?id=4408754) providing support for powerful plugins.

Plugins can be installed with Vagrant's built-in plugin manager. You can specify multiple plugins to install:

```
vagrant plugin install vagrant-vbguest vagrant-share

```

### vagrant-libvirt

This plugin adds [Libvirt](/index.php/Libvirt "Libvirt") support.

It currently has the same issue with ruby as the vagrant-kvm plugin. As of vagrant 1.7.2, this invocation will install vagrant-libvirt successfully:

```
 # in case it's already installled
 vagrant plugin uninstall vagrant-libvirt

 # vagrant's copy of curl prevents the proper installation of ruby-libvirt
 sudo mv /opt/vagrant/embedded/lib/libcurl.so{,.backup}
 sudo mv /opt/vagrant/embedded/lib/libcurl.so.4{,.backup}
 sudo mv /opt/vagrant/embedded/lib/libcurl.so.4.3.0{,.backup}
 sudo mv /opt/vagrant/embedded/lib/pkgconfig/libcurl.pc{,.backup}

 CONFIGURE_ARGS="with-libvirt-include=/usr/include/libvirt with-libvirt-lib=/usr/lib" vagrant plugin install vagrant-libvirt

 # put vagrant's copy of curl back
 sudo mv /opt/vagrant/embedded/lib/libcurl.so{.backup,}
 sudo mv /opt/vagrant/embedded/lib/libcurl.so.4{.backup,}
 sudo mv /opt/vagrant/embedded/lib/libcurl.so.4.3.0{.backup,}
 sudo mv /opt/vagrant/embedded/lib/pkgconfig/libcurl.pc{.backup,}

```

If starting a box with vagrant-libvirt still gives you errors it can help to replace the `ruby-libvirt` gem located in `~/.vagrant.d` with the one from the [AUR](/index.php/AUR "AUR"). First install [ruby-libvirt](https://aur.archlinux.org/packages/ruby-libvirt/) from the [AUR](/index.php/AUR "AUR") Arch User repository. Then copy `/usr/lib/ruby/gems/2.2.0/gems/ruby-libvirt-*` to `~/.vagrant.d/gems/gems/` (make sure to remove the `ruby-libvirt-*` directory under `~/.vagrant.d/gems/gems/` beforehand).

### vagrant-lxc

First install [lxc](https://www.archlinux.org/packages/?name=lxc) from the official repositories, then:

```
vagrant plugin install vagrant-lxc

```

Next, configure lxc and some systemd unit files per [this comment](https://github.com/fgrehm/vagrant-lxc/issues/109#issuecomment-21274392). The plugin can now be used with a `Vagrantfile` like so:

```
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure("2") do |config|

    config.vm.define "main" do |config|
        config.vm.box = 'http://bit.ly/vagrant-lxc-wheezy64-2013-10-23'

        config.vm.provider :lxc do |lxc|
            lxc.customize 'cgroup.memory.limit_in_bytes', '512M'
        end

        config.vm.provision :shell do |shell|
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

*Provisioners* allow you to automatically install software, alter and automate configurations as part of the vagrant up process. The two most common provisioners are [puppet](https://www.archlinux.org/packages/?name=puppet) from [official repositories](/index.php/Official_repositories "Official repositories") and [chef](https://aur.archlinux.org/packages/chef/) from the [AUR](/index.php/AUR "AUR") Arch User Repository.

## Base Boxes for Vagrant

Here is a list of places to get all sorts of vagrant base boxes for different purposes: development, testing, or even production.

*   A well maintained up-to-date [Arch Linux x86_64](https://github.com/terrywang/vagrantboxes/blob/master/archlinux-x86_64.md) base box for Vagrant

*   The same Arch Linux x86_64 base box can also be obtained via Vagrant Cloud by running: `vagrant init terrywang/archlinux`

*   [Vagrant Cloud](https://vagrantcloud.com/) is HashiCorp's official site for Vagrant boxes. You can browse user-submitted boxes or upload your own. A single Vagrant Cloud box can support multiple providers with versioning.

*   [vagrantbox.es](http://vagrantbox.es/)
    A List of vagrant base boxes. Initiated by Gareth Rushgrove [@garethr](https://twitter.com/garethr) hosted on Heroku using Nginx. See the story here: [The Vagrantbox.es Story](http://www.morethanseven.net/2012/07/01/The-vagrantbox.es-story/).

*   Opscode [bento](https://github.com/opscode/bento)
    We all know what bento means in Japanese, right? In this case, they are **NOT** lunch boxes **BUT** extremely useful base boxes which can be used to test cookbooks or private chef (Chef Server and Client). Distributions included: Ubuntu Server, Debian, CentOS, Fedora and FreeBSD.

*   [Puppet Labs Vagrant Boxes](http://puppet-vagrant-boxes.puppetlabs.com/)
    Pre-rolled vagrant boxes, ready for use. Made by the folks at Puppet Labs.

*   [Vagrant Ubuntu Cloud Images](http://cloud-images.ubuntu.com/vagrant/)
    It has been there since Jan, 2013\. For some reason Canonical has NOT officially promoted it yet, may be still in beta. Remember these are vanilla images, NOT very useful without Chef or Puppet.

## Troubleshooting

### No ping between host and vagrant box (host-only networking)

Sometimes there are troubles with host-only networking not functioning. Host have no ip on vboxnet interface, host cannot ping vagrant boxes and cannot be pinged from them. This is solved by installing good old [net-tools](https://www.archlinux.org/packages/?name=net-tools) as mentioned in [this thread](https://bbs.archlinux.org/viewtopic.php?pid=1178607#p1178607) by kevin1024

### 'vagrant up' hangs on NFS mounting (Mounting NFS shared folders...)

Installing [net-tools](https://www.archlinux.org/packages/?name=net-tools) package may solve this problem.

## See also

*   [official Vagrant documentation](http://docs.vagrantup.com/v2/getting-started/project_setup.html)