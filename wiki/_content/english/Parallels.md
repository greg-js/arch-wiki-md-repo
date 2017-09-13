Related articles

*   [VMware](/index.php/VMware "VMware")
*   [VirtualBox](/index.php/VirtualBox "VirtualBox")

[Parallels](http://www.parallels.com/products/desktop) Desktop is a hypervisor for macOS which allows users to install a variety of operating systems as "virtual machines" (guests) on the host system, reducing the need for managing multiple physical machines. A more complete description on virtualization can be found at [Wikipedia](https://en.wikipedia.org/wiki/Hardware_virtualization "wikipedia:Hardware virtualization").

## Contents

*   [1 Installation of Arch as a guest](#Installation_of_Arch_as_a_guest)
*   [2 Parallels Tools](#Parallels_Tools)
    *   [2.1 Overview](#Overview)
    *   [2.2 Required Kernel & Xorg versions](#Required_Kernel_.26_Xorg_versions)
    *   [2.3 Configuring Xorg](#Configuring_Xorg)
    *   [2.4 Preparing dependencies](#Preparing_dependencies)
    *   [2.5 Installing Parallels tools](#Installing_Parallels_tools)
    *   [2.6 Systemd Configuration](#Systemd_Configuration)
    *   [2.7 Using the Tools](#Using_the_Tools)
        *   [2.7.1 Sharing Folders](#Sharing_Folders)
        *   [2.7.2 Dynamic Display Resolution](#Dynamic_Display_Resolution)
    *   [2.8 Future work](#Future_work)

## Installation of Arch as a guest

Parallels Desktop supports Linux guests out of the box, but only offers support for a few Linux distributions - excluding Arch Linux. This means the installation of Parallels tools have not been tested by the vendor, and requires some manual intervention to work under Arch. If you do not wish to use Parallels tools, installation is as simple as choosing "other linux" when creating a new virtual machine and proceeding as you would on any real machine.

In addition to the instructions below, there is an installation guide for Arch Linux in Parallels Knowledgebase [[1]](http://kb.parallels.com/en/124124).

## Parallels Tools

### Overview

To improve interoperability between the host and the guest operating systems, Parallels provides a package called "Parallels tools" which contains kernel modules and userspace utilities. See [Parallels Tools Overview](http://download.parallels.com/desktop/v6/docs/en/Parallels_Desktop_Users_Guide/22272.htm) for a list of its features.

This article assumes users want to make full use of the tools, including Xorg configuration. If you are running a headless server, you can skip over the sections relating to X.

When referring to the version of parallel tools the form is <Parallels.Version>.<Tools Version>. For example: 9.0.24237.1028877 corresponds to Parallels version 9.0.24237 with tools version 1028877

### Required Kernel & Xorg versions

The tools installer uses binaries which can sometimes be incompatible with the latest version of Xorg or kernels in the Arch repository.

Different versions have different software requirements:

*   9.0.24229.991745 needs 3.13.8 (or possibly a later 3.13.y) (3.14 is known to show a black screen and freeze the system) and xorg 1.15.y or earlier
*   9.0.24237.1028877 works with Arch's 3.14.15-1-lts (newer versions may work) and xorg 1.15.y or earlier
*   11.0.0.31193 works on the latest Arch 4.1.6-1 and xorg 1.17.2-4
*   12.1.0.41489 works on latest Arch 4.8.7-1 and Xorg 1.18.4, after removing the PATH statement in the install script (cdrom//Parallels Tools//install), and adding "iomem=relaxed" to kernel boot parameters.

And there are different ways to obtain them:

*   linux 3.13.8 can be obtained from the [Arch Rollback Machine](/index.php/Arch_Rollback_Machine "Arch Rollback Machine")
*   linux 3.14.15 is the current linux-lts, so just install that and regenerate your grub config.
*   xorg 1.15.y can be obtained using the instructions & repo from [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst").

Repository settings for /etc/pacman.conf (for 3.13.8)

```
[core]
#Include = /etc/pacman.d/mirrorlist
SigLevel = PackageRequired
Server = [http://seblu.net/a/arm/2014/04/09/$repo/os/$arch](http://seblu.net/a/arm/2014/04/09/$repo/os/$arch)
[extra]
#Include = /etc/pacman.d/mirrorlist
SigLevel = PackageRequired
Server = [http://seblu.net/a/arm/2014/04/09/$repo/os/$arch](http://seblu.net/a/arm/2014/04/09/$repo/os/$arch)

```

See also [Downgrading packages#Downgrading the kernel](/index.php/Downgrading_packages#Downgrading_the_kernel "Downgrading packages").

### Configuring Xorg

The Parallels tools installer will take care of configuring Xorg, so just follow the instructions at [Xorg](/index.php/Xorg "Xorg") to install the relevant packages on your system. Install the [xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa) package to use the vesa driver.

### Preparing dependencies

The installation script expects to find your init-scripts in `/etc/init.d/` and will fail if it's not present. Since Arch uses systemd, create a symlink to the systemd scripts directory and set the def_sysconfdir variable:

 `# ln -sf /usr/lib/systemd/scripts/ /etc/init.d`  `# export def_sysconfdir=/etc/init.d` 

The installation script also expects the file `/etc/X11/xorg.conf`. We can just create an empty file, as it will automatically be configured by the installer:

 `# touch /etc/X11/xorg.conf` 

Then, you need to install standard build utilities, python2, and kernel headers:

 `# pacman -S base-devel python2 linux-headers` 

depends on your Parallels version, you may have to install `linux-lts-headers` instead of `linux-headers`.

Finally, create a temporary symbolic link to python 2\. Remove this link after the installation process.

 `# ln -sf /usr/bin/python2 /usr/local/bin/python` 

### Installing Parallels tools

Choose "install Parallels Tools" from the "Virtual Machine" menu. Parallels Tools are located on a cd-image, which will be connected to your virtual machine. You have to mount it first:

 `# mount /dev/cdrom /mnt/cdrom` 

Now you can proceed to install Parallels tools using the installation script as follows:

 `# cd /mnt/cdrom`  `# ./install` 

### Systemd Configuration

The Parallels tools daemon should be started at boot, so create a service file like the following:

 `/usr/lib/systemd/system/parallels-tools.service` 
```
[Unit]
Description=Parallels Tools
[Service]
Type=oneshot
ExecStart=/usr/lib/systemd/scripts/prltoolsd start
ExecStop=/usr/lib/systemd/scripts/prltoolsd stop
RemainAfterExit=yes
[Install]
WantedBy=multi-user.target
```

[Enable](/index.php/Enable "Enable") the `parallels-tools.service` service. Reboot the system and Parallels tools should now be installed and working.

### Using the Tools

#### Sharing Folders

You can specify which folders on your hosts system you would like to share with your guests under "virtual machine > configuration > sharing". Then you mount a shared folder like this:

 `# mount -t prl_fs *name_of_share* */mnt/name_of_share*` 

#### Dynamic Display Resolution

A very helpful tool is `prlcc`. It changes the resolution of the display (in the guest - not the host) automatically when your resize your window. If this tool is not running, the contents of the window gets stretched or shrunken. prlcc is usually started automatically and runs in the background. If not, run the following (or place it in a configuration file like /etc/X11/xinit/xinitrc.d/90-prlcc):

 `$ prlcc &` 

### Future work

In general, updating system packages like the linux kernel or Xorg can break Parallels tools and you will need to re-install them. In some cases, new packages will be incompatible with the tools and they will stop working - in that case you will need to roll back the newly installed packages and wait until Parallels releases a new product build before updating your guest (in the hope they have resolved any previous incompatibilities).