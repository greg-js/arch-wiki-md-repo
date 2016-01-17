# Xen

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

From [Xen Overview](http://wiki.xen.org/wiki/Xen_Overview):

_Xen is an open-source type-1 or baremetal hypervisor, which makes it possible to run many instances of an operating system or indeed different operating systems in parallel on a single machine (or host). Xen is the only type-1 hypervisor that is available as open source. Xen is used as the basis for a number of different commercial and open source applications, such as: server virtualization, Infrastructure as a Service (IaaS), desktop virtualization, security applications, embedded and hardware appliances._

**Warning:** Do not run other virtualization software such as [VirtualBox](/index.php/VirtualBox "VirtualBox") when running Xen hypervisor, it might hang your system. See this [bug report (wontfix)](https://www.virtualbox.org/ticket/12146).

## Contents

*   [1 Introduction](#Introduction)
*   [2 System requirements](#System_requirements)
*   [3 Configuring dom0](#Configuring_dom0)
    *   [3.1 Installation of the Xen hypervisor](#Installation_of_the_Xen_hypervisor)
        *   [3.1.1 With UEFI support](#With_UEFI_support)
    *   [3.2 Modification of the bootloader](#Modification_of_the_bootloader)
        *   [3.2.1 UEFI](#UEFI)
        *   [3.2.2 GRUB](#GRUB)
        *   [3.2.3 Syslinux](#Syslinux)
    *   [3.3 Creation of a network bridge](#Creation_of_a_network_bridge)
    *   [3.4 Creating bridge with Network Manager](#Creating_bridge_with_Network_Manager)
*   [4 Installation of Xen systemd services](#Installation_of_Xen_systemd_services)
*   [5 Confirming successful installation](#Confirming_successful_installation)
*   [6 Using Xen](#Using_Xen)
    *   [6.1 Create a domU "hard disk"](#Create_a_domU_.22hard_disk.22)
    *   [6.2 Create a domU configuration](#Create_a_domU_configuration)
    *   [6.3 Managing a domU](#Managing_a_domU)
*   [7 Configuring a hardware virtualized (HVM) Arch domU](#Configuring_a_hardware_virtualized_.28HVM.29_Arch_domU)
*   [8 Configuring a paravirtualized (PV) Arch domU](#Configuring_a_paravirtualized_.28PV.29_Arch_domU)
*   [9 Common Errors](#Common_Errors)
    *   [9.1 "xl list" complains about libxl](#.22xl_list.22_complains_about_libxl)
    *   [9.2 "xl create" fails](#.22xl_create.22_fails)
    *   [9.3 Arch Linux guest hangs with a ctrl-d message](#Arch_Linux_guest_hangs_with_a_ctrl-d_message)
    *   [9.4 Error message "failed to execute '/usr/lib/udev/socket:/org/xen/xend/udev_event' 'socket:/org/xen/xend/udev_event': No such file or directory"](#Error_message_.22failed_to_execute_.27.2Fusr.2Flib.2Fudev.2Fsocket:.2Forg.2Fxen.2Fxend.2Fudev_event.27_.27socket:.2Forg.2Fxen.2Fxend.2Fudev_event.27:_No_such_file_or_directory.22)
*   [10 Resources](#Resources)

## Introduction

The Xen hypervisor is a thin layer of software which emulates a computer architecture allowing multiple operating systems to run simultaneously. The hypervisor is started by the boot loader of the computer it is installed on. Once the hypervisor is loaded, it starts the [dom0](http://wiki.xen.org/wiki/Dom0) (short for "domain 0", sometimes called the host or privileged domain) which in our case runs Arch Linux. Once the _dom0_ has started, one or more [domU](http://wiki.xen.org/wiki/DomU) (short for user domains, sometimes called VMs or guests) can be started and controlled from the _dom0_. Xen supports both paravirtualized (PV) and hardware virtualized (HVM) _domU_. See [Xen.org](http://wiki.xen.org/wiki/Xen_Overview) for a full overview.

## System requirements

The Xen hypervisor requires kernel level support which is included in recent Linux kernels and is built into the [linux](https://www.archlinux.org/packages/?name=linux) and [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) Arch kernel packages. To run HVM _domU_, the physical hardware must have either Intel VT-x or AMD-V (SVM) virtualization support. In order to verify this, run the following command when the Xen hypervisor is not running:

```
$ grep -E "(vmx|svm)" --color=always /proc/cpuinfo

```

If the above command does not produce output, then hardware virtualization support is unavailable and your hardware is unable to run HVM _domU_ (or you are already running the Xen hypervisor). If you believe the CPU supports one of these features you should access the host system's BIOS configuration menu during the boot process and look if options related to virtualization support have been disabled. If such an option exists and is disabled, then enable it, boot the system and repeat the above command. The Xen hypervisor also supports PCI passthrough where PCI devices can be passed directly to the _domU_ even in the absence of _dom0_ support for the device. In order to use PCI passthrough, the CPU must support IOMMU/VT-d.

## Configuring dom0

The Xen hypervisor relies on a full install of the base operating system. Before attempting to install the Xen hypervisor, the host machine should have a fully operational and up-to-date install of Arch Linux. This installation can be a minimal install with only the base package and does not require a [Desktop environment](/index.php/Desktop_environment "Desktop environment") or even [Xorg](/index.php/Xorg "Xorg"). If you are building a new host from scratch, see the [Installation guide](/index.php/Installation_guide "Installation guide") for instructions on installing Arch Linux. The following configuration steps are required to convert a standard installation into a working _dom0_ running on top of the Xen hypervisor:

1.  Installation of the Xen hypervisor
2.  Modification of the bootloader to boot the Xen hypervisor
3.  Creation of a network bridge
4.  Installation of Xen systemd services

### Installation of the Xen hypervisor

To install the Xen hypervisor install either the current stable [xen](https://aur.archlinux.org/packages/xen/)<sup><small>AUR</small></sup> or the bleeding edge unstable [xen-git](https://aur.archlinux.org/packages/xen-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xen-git)]</sup> packages available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). Both packages provide the Xen hypervisor, current xl interface and all configuration and support files, including systemd services. The [multilib](/index.php/Multilib "Multilib") repository needs to be enabled and the `multilib-devel` package group installed to compile Xen. Install the [xen-docs](https://aur.archlinux.org/packages/xen-docs/)<sup><small>AUR</small></sup> package from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") for the man pages and documentation.

#### With UEFI support

It's possible to boot the Xen hypervisor though the bare UEFI system on a modern computer but requires you to first recompile binutils to add support for x86_64-pep emulation. Using the archway of doing things you would use the [Arch Build System](/index.php/Arch_Build_System "Arch Build System") and add `--enable-targets=x86_64-pep` to the build options of the binutils PKGBUILD file:

```
--disable-werror **--enable-targets=x86_64-pep**

```

**Note:**

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** This Note is not very meaningful without a link to a bug report. (Discuss in [Talk:Xen#](https://wiki.archlinux.org/index.php/Talk:Xen))

This will not work on the newest version of binutils you will need to downgrade to an older version from the svn:

```
$ svn checkout --depth empty svn://svn.archlinux.org/packages
$ cd packages
$ svn update -r 215066 binutils

```

Then compile and install. See [[1]](https://nims11.wordpress.com/2013/02/17/downgrading-packages-in-arch-linux-the-worst-case-scenario/) for details of the procedure.

The next time binutils gets updated on your system it will be overwritten with the official version again. However, you only need this change to (re-)compile the UEFI aware Xen hypervisor, it is not needed at either boot or run time.

Now when you compile Xen with your x86_64-pep aware binutils a UEFI kernel will be built and installed by default. It is located at `/usr/lib/efi/xen-?.?.?.efi` where "?" represent the version digits. The other files you find that also begin with "xen" are simply symlinks back to the real file and can be ignored. However, the efi-binary needs to be manually copied to `/boot`, e.g.:

```
# cp /usr/lib/efi/xen-4.4.0.efi /boot

```

### Modification of the bootloader

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Lots of other boot loaders could/should be covered, at least the most common like Gummiboot. (Discuss in [Talk:Xen#](https://wiki.archlinux.org/index.php/Talk:Xen))

**Warning:** Never assume your system will boot after changes to the boot system. This might be the most common error new as well as old users do. Make sure you have a alternative way to boot your system like a USB stick or other livemedia **BEFORE** you make changes to your boot system.

The boot loader must be modified to load a special Xen kernel (`xen.gz` or in the case of UEFI `xen.efi`) which is then used to boot the normal kernel. To do this a new bootloader entry is needed.

#### UEFI

There are several ways UEFI can be involved in booting Xen but this section will cover the most simple way to get Xen to boot with help of EFI-stub.

Make sure that you have compiled Xen with UEFI support enabled accoring to [#With UEFI support](#With_UEFI_support).

It is possible to boot a kernel from UEFI just by placing it on the EFI partition, but since Xen at least needs to know what kernel should be booted as dom0, a minimum configuration file is required. Create or edit a `/boot/xen.cfg` file according to system requirements, for example:

 `/boot/xen.cfg` 

```
[global]
default=xen

[xen]
options=console=vga loglvl=all noreboot
kernel=vmlinuz-linux root=/dev/sda2 rw ignore_loglevel #earlyprintk=xen
ramdisk=initramfs-linux.img

```

It might be necessary to use [efibootmgr](/index.php/UEFI#efibootmgr "UEFI") to set boot order and other parameters. If booting fails, drop to the build-in [UEFI shell](/index.php/UEFI#Launching_UEFI_Shell "UEFI") and try to launch manually. For example:

```
Shell> fs0:
FS0:\> xen-4.4.0.efi

```

#### GRUB

For [GRUB](/index.php/GRUB "GRUB") users, the Xen package provides the `/etc/grub.d/09_xen` generator file. The file `/etc/xen/grub.conf` can be edited to customize the Xen boot commands. For example, to allocate 512 MiB of RAM to _dom0_ at boot, modify `/etc/xen/grub.conf` by replacing the line:

```
#XEN_HYPERVISOR_CMDLINE="xsave=1"

```

with

```
XEN_HYPERVISOR_CMDLINE="dom0_mem=512M xsave=1"

```

After customizing the options, update the bootloader configuration with the following command:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

More information on using the GRUB bootloader is available at [GRUB](/index.php/GRUB "GRUB").

#### Syslinux

For [syslinux](/index.php/Syslinux "Syslinux") users, add a stanza like this to your `/boot/syslinux/syslinux.cfg`:

```
LABEL xen
    MENU LABEL Xen
    KERNEL mboot.c32
    APPEND ../xen-X.Y.Z.gz --- ../vmlinuz-linux console=tty0 root=/dev/sdaX ro --- ../initramfs-linux.img

```

where `X.Y.Z` is your xen version and `/dev/sdaX` is your [root partition](/index.php/Fstab#Identifying_filesystems "Fstab").

This also requires `mboot.c32` to be in the same directory as `syslinux.cfg`. If you do not have `mboot.c32` in `/boot/syslinux`, copy it from:

```
# cp /usr/lib/syslinux/bios/mboot.c32 /boot/syslinux

```

### Creation of a network bridge

Xen requires that network communications between _domU_ and the _dom0_ (and beyond) be set up manually. The use of both DHCP and static addressing is possible, and the choice should be determined by the network topology. Complex setups are possible, see the [Networking](http://wiki.xen.org/wiki/Xen_Networking) article on the Xen wiki for details and `/etc/xen/scripts` for scripts for various networking configurations. A basic bridged network, in which a virtual switch is created in _dom0_ that every _domU_ is attached to, can be set up by creating a [network bridge](/index.php/Network_bridge "Network bridge") with the expected name `xenbr0`.

See [Network bridge#Creating a bridge](/index.php/Network_bridge#Creating_a_bridge "Network bridge") for details.

### Creating bridge with Network Manager

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Network_bridge#With_NetworkManager](/index.php/Network_bridge#With_NetworkManager "Network bridge").**

**Notes:** Duplicates the main page. (Discuss in [Talk:Xen#](https://wiki.archlinux.org/index.php/Talk:Xen))

Gnome's Network Manager can sometime be troublesome. If following the bridge creation section outlined in the [bridges](https://wiki.archlinux.org/index.php/Network_bridge) section of the wiki are unclear or do not work, then the following steps may work.

Open the Network Settings and disable the interface you wish to use in your bridge (ex enp5s0). Edit the setting to off and uncheck "connect automatically."

Create a new bridge connection profile by clicking on the "+" symbol in the bottom left of the network settings. Optionally, run:

```
# nm-connection-editor

```

to bring up the window immediately. Once the window opens, select Bridge.

Click "Add" next to the "Bridged Connections" and select the interface you wished to use in your bridge (ex. Ethernet). Select the device mac address that corresponds to the interface you intend to use and save the settings

If your bridge is going to receive an IP address via DHCP, leave the IPv4/IPv6 sections as they are. If DHCP is not running for this particular connection, make sure to give your bridge an IP address. Needless to say, all connections will fail if an IP address is not assigned to the bridge. If you forget to add the IP address when you first create the bridge, it can always be edited later.

Now, as root, run:

```
# nmcli con show

```

You should see a connection that matches the name of the bridge you just created. Highlight and copy the UUID on that connection, and then run (again as root):

```
# nmcli con up <UUID OF CONNECTION>

```

A new connection should appear under the network settings. It may take 30 seconds to a minute. To confirm that it is up and running, run:

```
# brctl show

```

to show a list of active bridges.

Reboot. If everything works properly after a reboot (ie. bridge starts automatically), then you are all set.

<optional> In your network settings, remove the connection profile on your bridge interface that does NOT connect to the bridge. This just keeps things from being confusing later on.

## Installation of Xen systemd services

The Xen _dom0_ requires the `xenstored`, `xenconsoled`, `xendomains` and `xen-init-dom0` [services](/index.php/Systemd#Using_units "Systemd") to be started and possibly enabled.

## Confirming successful installation

Reboot your _dom0_ host and ensure that the Xen kernel boots correctly and that all settings survive a reboot. A properly set up _dom0_ should report the following when you run `xl list` as root:

 `# xl list` 

```
Name                                        ID   Mem VCPUs	State	Time(s)
Domain-0                                     0   511     2     r-----   41652.9
```

Of course, the Mem, VCPUs and Time columns will be different depending on machine configuration and uptime. The important thing is that _dom0_ is listed.

In addition to the required steps above, see [best practices for running Xen](http://wiki.xen.org/wiki/Xen_Best_Practices) which includes information on allocating a fixed amount of memory and how to dedicate (pin) a CPU core for _dom0_ use. It also may be beneficial to create a xenfs filesystem mount point by including in `/etc/fstab`

```
none /proc/xen xenfs defaults 0 0

```

## Using Xen

Xen supports both paravirtualized (PV) and hardware virtualized (HVM) _domU_. In the following sections the steps for creating HVM and PV _domU_ running Arch Linux are described. In general, the steps for creating an HVM _domU_ are independent of the _domU_ OS and HVM _domU_ support a wide range of operating systems including Microsoft Windows. To use HVM _domU_ the _dom0_ hardware must have virtualization support. Paravirtualized _domU_ do not require virtualization support, but instead require modifications to the guest operating system making the installation procedure different for each operating system (see the [Guest Install](http://wiki.xen.org/wiki/Category:Guest_Install) page of the Xen wiki for links to instructions). Some operating systems (e.g., Microsoft Windows) cannot be installed as a PV _domU_. In general, HVM _domU_ often run slower than PV _domU_ since HVMs run on emulated hardware. While there are some common steps involved in setting up PV and HVM _domU_, the processes are substantially different. In both cases, for each _domU_, a "hard disk" will need to be created and a configuration file needs to be written. Additionally, for installation each _domU_ will need access to a copy of the installation ISO stored on the _dom0_ (see the [Download Page](https://www.archlinux.org/download/) to obtain the Arch Linux ISO).

### Create a domU "hard disk"

Xen supports a number of different types of "hard disks" including [Logical Volumes](/index.php/LVM "LVM"), [raw partitions](/index.php/Partitioning "Partitioning"), and image files. To create a [sparse file](https://en.wikipedia.org/wiki/Sparse_file "wikipedia:Sparse file"), that will grow to a maximum of 10GiB, called `domU.img`, use:

```
$ truncate -s 10G domU.img

```

If file IO speed is of greater importance than domain portability, using [Logical Volumes](/index.php/LVM "LVM") or [raw partitions](/index.php/Partitioning "Partitioning") may be a better choice.

Xen may present any partition / disk available to the host machine to a domain as either a partition or disk. This means that, for example, an LVM partition on the host can appear as a hard drive (and hold multiple partitions) to a domain. Note that making sub-partitons on a partition will make accessing those partitions on the host machine more difficult. See the kpartx man page for information on how to map out partitions within a partition.

### Create a domU configuration

Each _domU_ requires a separate configuration file that is used to create the virtual machine. Full details about the configuration files can be found at the [Xen Wiki](http://wiki.xenproject.org/wiki/XenConfigurationFileOptions) or the `xl.cfg` man page. Both HVM and PV _domU_ share some components of the configuration file. These include

```
name = "domU"
memory = 256
disk = [ "file:/path/to/ISO,sdb,r", "phy:/path/to/partition,sda1,w" ]
vif = [ 'mac=00:16:3e:XX:XX:XX,bridge=xenbr0' ]

```

The `name=` is the name by which the xl tools manage the _domU_ and needs to be unique across all _domU_. The `disk=` includes information about both the the installation media (`file:`) and the partition created for the _domU_ `phy`. If an image file is being used instead of a physical partition, the `phy:` needs to be changed to `file:`. The `vif=` defines a network controller. The `00:16:3e` MAC block is reserved for Xen domains, so the last three digits of the `mac=` must be randomly filled in (hex values 0-9 and a-f only).

### Managing a domU

If a _domU_ should be started on boot, create a symlink to the configuration file in `/etc/xen/auto` and ensure the `xendomains` service is set up correctly. Some useful commands for managing _domU_ are:

```
# xl top
# xl list
# xl console domUname
# xl shutdown domUname
# xl destroy domUname

```

## Configuring a hardware virtualized (HVM) Arch domU

In order to use HVM _domU_ install the [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl) and [bluez-libs](https://www.archlinux.org/packages/?name=bluez-libs) packages.

A minimal configuration file for a HVM Arch _domU_ is:

```
name = 'HVM_domU'
builder = 'hvm'
memory = 256
vcpus = 2
disk = [ 'phy:/dev/mapper/vg0-hvm_arch,xvda,w', 'file:/path/to/ISO,hdc:cdrom,r' ]
vif = [ 'mac=00:16:3e:00:00:00,bridge=xenbr0' ]
vnc = 1
vnclisten = '0.0.0.0'
vncdisplay = 1

```

Since HVM machines do not have a console, they can only be connected to via a [vncviewer](/index.php/Vncserver "Vncserver"). The configuration file allows for unauthenticated remote access of the _domU_ vncserver and is not suitable for unsecured networks. The vncserver will be available on port `590X`, where X is the value of `vncdisplay`, of the _dom0_. The _domU_ can be created with:

```
# xl create /path/to/config/file

```

and its status can be checked with

```
# xl list

```

Once the _domU_ is created, connect to it via the vncserver and install Arch Linux as described in the [Installation guide](/index.php/Installation_guide "Installation guide").

## Configuring a paravirtualized (PV) Arch domU

A minimal configuration file for a PV Arch _domU_ is:

```
name = "PV_domU"
kernel = "/mnt/arch/boot/x86_64/vmlinuz"
ramdisk = "/mnt/arch/boot/x86_64/archiso.img"
extra = "archisobasedir=arch archisolabel=ARCH_201301"
memory = 256
disk = [ "phy:/path/to/partition,sda1,w", "file:/path/to/ISO,sdb,r" ]
vif = [ 'mac=00:16:3e:XX:XX:XX,bridge=xenbr0' ]

```

This file needs to tweaked for your specific use. Most importantly, the `archisolabel=ARCH_201301` line must be edited to use the release year/month of the ISO being used. If you want to install 32-bit Arch, change the kernel and ramdisk paths from `x86_64` to `i686`.

Before creating the _domU_, the installation ISO must be loop-mounted. To do this, ensure the directory `/mnt` exists and is empty, then run the following command (being sure to fill in the correct ISO path):

```
# mount -o loop /path/to/iso /mnt

```

Once the ISO is mounted, the _domU_ can be created with:

```
# xl create -c /path/to/config/file

```

The "-c" option will enter the _domU'_s console when successfully created. Then you can install Arch Linux as described in the [Installation guide](/index.php/Installation_guide "Installation guide"), but with the following deviations. The block devices listed in the disks line of the cfg file will show up as `/dev/xvd*`. Use these devices when partitioning the _domU_. After installation and before the _domU_ is rebooted, the `xen-blkfront`, `xen-fbfront`, `xen-netfront`, `xen-kbdfront` modules must be added to [Mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"). Without these modules, the _domU_ will not boot correctly. For booting, it is not necessary to install Grub. Xen has a Python-based grub emulator, so all that is needed to boot is a `grub.cfg` file: (It may be necessary to create the `/boot/grub` directory)

 `/boot/grub/grub.cfg` 

```
menuentry 'Arch GNU/Linux, with Linux core repo kernel' --class arch --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-core repo kernel-true-__UUID__' {
        insmod gzio
        insmod part_msdos
        insmod ext2
        set root='hd0,msdos1'
        if [ x$feature_platform_search_hint = xy ]; then
          search --no-floppy --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1  __UUID__
        else
          search --no-floppy --fs-uuid --set=root __UUID__
        fi
        echo    'Loading Linux core repo kernel ...'
        linux   /boot/vmlinuz-linux root=UUID=__UUID__ ro
        echo    'Loading initial ramdisk ...'
        initrd  /boot/initramfs-linux.img
}
```

This file must be edited to match the UUID of the root partition. From within the _domU_, run the following command:

```
# blkid

```

Replace all instances of `__UUID__` with the real UUID of the root partition (the one that mounts as `/`).:

```
# sed -i 's/__UUID__/12345678-1234-1234-1234-123456789abcd/g' /boot/grub/grub.cfg

```

Shutdown the _domU_ with the `poweroff` command. The console will be returned to the hypervisor when the domain is fully shut down, and the domain will no longer appear in the xl domains list. Now the ISO file may be unmounted:

```
# umount /mnt

```

The _domU_ cfg file should now be edited. Delete the `kernel =`, `ramdisk =`, and `extra =` lines and replace them with the following line:

```
bootloader = "pygrub"

```

Also remove the ISO disk from the `disk =` line.

The Arch _domU_ is now set up. It may be started with the same line as before:

```
# xl create -c /etc/xen/archdomu.cfg

```

## Common Errors

### "xl list" complains about libxl

Either you have not booted into the Xen system, or xen modules listed in `xencommons` script are not installed.

### "xl create" fails

Check the guest's kernel is located correctly, check the `pv-xxx.cfg` file for spelling mistakes (like using `initrd` instead of `ramdisk`).

### Arch Linux guest hangs with a ctrl-d message

Press `ctrl-d` until you get back to a prompt, rebuild its initramfs described

### Error message "failed to execute '/usr/lib/udev/socket:/org/xen/xend/udev_event' 'socket:/org/xen/xend/udev_event': No such file or directory"

This is caused by `/etc/udev/rules.d/xend.rules`. Xend is deprecated and not used, so it is safe to remove that file.

## Resources

*   [The homepage at xen.org](http://www.xen.org/)
*   [The wiki at xen.org](http://wiki.xen.org/wiki/Main_Page)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Xen&oldid=415503](https://wiki.archlinux.org/index.php?title=Xen&oldid=415503)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")
*   [Kernel](/index.php/Category:Kernel "Category:Kernel")

Hidden categories:

*   [Pages or sections flagged with Template:Accuracy](/index.php/Category:Pages_or_sections_flagged_with_Template:Accuracy "Category:Pages or sections flagged with Template:Accuracy")
*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")
*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")