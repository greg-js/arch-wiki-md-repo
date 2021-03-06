Related articles

*   [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

From [Xen Overview](http://wiki.xen.org/wiki/Xen_Overview):

	*Xen is an open-source type-1 or baremetal hypervisor, which makes it possible to run many instances of an operating system or indeed different operating systems in parallel on a single machine (or host). Xen is the only type-1 hypervisor that is available as open source.*

The Xen hypervisor is a thin layer of software which emulates a computer architecture allowing multiple operating systems to run simultaneously. The hypervisor is started by the boot loader of the computer it is installed on. Once the hypervisor is loaded, it starts the [dom0](http://wiki.xen.org/wiki/Dom0) (short for "domain 0", sometimes called the host or privileged domain) which in our case runs Arch Linux. Once the *dom0* has started, one or more [domU](http://wiki.xen.org/wiki/DomU) (short for user domains, sometimes called VMs or guests) can be started and controlled from the *dom0*. Xen supports both paravirtualized (PV) and hardware virtualized (HVM) *domU*. See [Xen.org](http://wiki.xen.org/wiki/Xen_Overview) for a full overview.

**Warning:** Do not run other virtualization software such as [VirtualBox](/index.php/VirtualBox "VirtualBox") when running Xen hypervisor, it might hang your system. See this [bug report (wontfix)](https://www.virtualbox.org/ticket/12146).

## Contents

*   [1 System requirements](#System_requirements)
*   [2 Configuring dom0](#Configuring_dom0)
    *   [2.1 Installation of the Xen hypervisor](#Installation_of_the_Xen_hypervisor)
    *   [2.2 Modification of the bootloader](#Modification_of_the_bootloader)
        *   [2.2.1 UEFI](#UEFI)
            *   [2.2.1.1 Systemd-boot](#Systemd-boot)
            *   [2.2.1.2 EFISTUB](#EFISTUB)
        *   [2.2.2 BIOS](#BIOS)
            *   [2.2.2.1 GRUB](#GRUB)
        *   [2.2.3 Syslinux](#Syslinux)
    *   [2.3 Creation of a network bridge](#Creation_of_a_network_bridge)
        *   [2.3.1 Systemd-networkd](#Systemd-networkd)
        *   [2.3.2 Network Manager](#Network_Manager)
    *   [2.4 Installation of Xen systemd services](#Installation_of_Xen_systemd_services)
    *   [2.5 Confirming successful installation](#Confirming_successful_installation)
    *   [2.6 Configure Best Practices](#Configure_Best_Practices)
*   [3 Using Xen](#Using_Xen)
    *   [3.1 Create a domU "hard disk"](#Create_a_domU_"hard_disk")
    *   [3.2 Create a domU configuration](#Create_a_domU_configuration)
    *   [3.3 Managing a domU](#Managing_a_domU)
*   [4 Configuring a hardware virtualized (HVM) Arch domU](#Configuring_a_hardware_virtualized_(HVM)_Arch_domU)
*   [5 Configuring a paravirtualized (PV) Arch domU](#Configuring_a_paravirtualized_(PV)_Arch_domU)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 "xl list" complains about libxl](#"xl_list"_complains_about_libxl)
    *   [6.2 "xl create" fails](#"xl_create"_fails)
    *   [6.3 Arch Linux guest hangs with a ctrl-d message](#Arch_Linux_guest_hangs_with_a_ctrl-d_message)
    *   [6.4 Error message "failed to execute '/usr/lib/udev/socket:/org/xen/xend/udev_event' 'socket:/org/xen/xend/udev_event': No such file or directory"](#Error_message_"failed_to_execute_'/usr/lib/udev/socket:/org/xen/xend/udev_event'_'socket:/org/xen/xend/udev_event':_No_such_file_or_directory")
*   [7 See also](#See_also)

## System requirements

The Xen hypervisor requires kernel level support which is included in recent Linux kernels and is built into the [linux](https://www.archlinux.org/packages/?name=linux) and [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) Arch kernel packages. To run HVM *domU*, the physical hardware must have either Intel VT-x or AMD-V (SVM) virtualization support. In order to verify this, run the following command when the Xen hypervisor is not running:

```
$ grep -E "(vmx|svm)" --color=always /proc/cpuinfo

```

If the above command does not produce output, then hardware virtualization support is unavailable and your hardware is unable to run HVM *domU* (or you are already running the Xen hypervisor). If you believe the CPU supports one of these features you should access the host system's BIOS configuration menu during the boot process and look if options related to virtualization support have been disabled. If such an option exists and is disabled, then enable it, boot the system and repeat the above command. The Xen hypervisor also supports PCI passthrough where PCI devices can be passed directly to the *domU* even in the absence of *dom0* support for the device. In order to use PCI passthrough, the CPU must support IOMMU/VT-d.

## Configuring dom0

The Xen hypervisor relies on a full install of the base operating system. Before attempting to install the Xen hypervisor, the host machine should have a fully operational and up-to-date install of Arch Linux. This installation can be a minimal install with only the base package and does not require a [Desktop environment](/index.php/Desktop_environment "Desktop environment") or even [Xorg](/index.php/Xorg "Xorg"). If you are building a new host from scratch, see the [Installation guide](/index.php/Installation_guide "Installation guide") for instructions on installing Arch Linux. The following configuration steps are required to convert a standard installation into a working *dom0* running on top of the Xen hypervisor:

1.  Installation of the Xen hypervisor
2.  Modification of the bootloader to boot the Xen hypervisor
3.  Creation of a network bridge
4.  Installation of Xen systemd services

### Installation of the Xen hypervisor

To install the Xen hypervisor, [install](/index.php/Install "Install") the [xen](https://aur.archlinux.org/packages/xen/) package. It provides the Xen hypervisor, current xl interface and all configuration and support files, including systemd services. The [multilib](/index.php/Multilib "Multilib") repository needs to be enabled and the [multilib-devel](https://www.archlinux.org/groups/x86_64/multilib-devel/) package group installed to compile Xen. Install the [xen-docs](https://aur.archlinux.org/packages/xen-docs/) package for the man pages and documentation.

You also need to install the [seabios](https://www.archlinux.org/packages/?name=seabios) and/or the [ovmf](https://www.archlinux.org/packages/?name=ovmf) package to boot VMs with BIOS or UEFI respectively.

### Modification of the bootloader

**Warning:** Never assume your system will boot after changes to the boot system. This might be the most common error new as well as old users do. Make sure you have a alternative way to boot your system like a USB stick or other livemedia **BEFORE** you make changes to your boot system.

The boot loader must be modified to load a special Xen kernel (`xen.gz` or in the case of UEFI `xen.efi`) which is then used to boot the normal kernel. To do this a new bootloader entry is needed.

#### UEFI

Xen supports booting from UEFI as specified in [Xen EFI systems](https://xenbits.xen.org/docs/unstable/misc/efi.html). It also might be necessary to use [efibootmgr](/index.php/UEFI#efibootmgr "UEFI") to set boot order and other parameters.

First, ensure the `xen-X.Y.Z.efi` file is in the [EFI system partition](/index.php/EFI_system_partition "EFI system partition") along with your kernel and ramdisk files.

Second, Xen requires an ASCII (no UTF-8, UTC-16, etc) configuration file that specifies what kernel should be booted as [dom0](https://wiki.xen.org/wiki/Dom0). This file must be placed in the same [EFI system partition](/index.php/EFI_system_partition "EFI system partition") as the binary. Xen looks for several configuration files and uses the first one it finds. The order of search starts with the `.efi` extension of the binary's name replaced by `.cfg`, then drops trailing name components at `.`, `-` and `_` until a match is found. Typically, a single file named `xen.cfg` is used with the system requirements, such as:

 `xen.cfg` 
```
[global]
default=xen

[xen]
options=console=vga iommu=force:true,qinval:true,debug:true loglvl=all noreboot=true reboot=no vga=ask ucode=scan
kernel=vmlinuz-linux root=/dev/sdaX rw add_efi_memmap #earlyprintk=xen
ramdisk=initramfs-linux.img

```

**Tip:** See [Xen efi.cfg](https://xenbits.xen.org/docs/unstable/misc/efi.html) for additional parameters in this file. For the options line, see [Xen Command Line options](https://xenbits.xen.org/docs/unstable/misc/xen-command-line.html) for a full list of options available such as serial console, limiting dom0 vCPU and memory, scheduling, Intel and AMD microcode and more. For example, [Xen Project Best Practices](https://wiki.xen.org/wiki/Xen_Project_Best_Practices) dictates to disabling memory ballooning for dom0\. To do that, edit the `xen.cfg` line for `options` to specify the additional parameters.

##### Systemd-boot

**Tip:** You can continue to boot the [dom0](https://wiki.xen.org/wiki/Dom0) kernel directly even after Xen is installed and configured. This can be useful in the event that an Xen installation becomes unbootable or misconfigured. Therefore, it is recommended to keep the original systemd-boot loader entries configured on the system as rescue boot options and just add additional entries for Xen.

**Note:** At the time of the system's [Systemd-boot](/index.php/Systemd-boot "Systemd-boot") installation, the ESP partition should have been mounted to `/boot` as this is where the [Xen](https://aur.archlinux.org/packages/Xen/) package and EFI binaries were configured and built for, not `/boot/efi`.

Add a new EFI-type loader entry. See [Systemd-boot#EFI Shells or other EFI apps](/index.php/Systemd-boot#EFI_Shells_or_other_EFI_apps "Systemd-boot") for more details. For example:

 `/boot/loader/entries/10-xen.conf` 
```
title   Xen Hypervisor
efi     /xen-X.Y.Z.efi

```

**Note:** The current [systemd-boot](/index.php/Systemd-boot "Systemd-boot") and Xen efi binary combination does not allow parameters passed on the `efi` line of the loader's entry. However, the Xen documentation states that `-cfg=file.cfg` can be used as an UEFI Shell parameter which is not true for the efi line option. For now, you can only have one Xen EFI entry which limits you to only one config file.

##### EFISTUB

It is possible to boot an EFI kernel directly from UEFI by using [EFISTUB](/index.php/EFISTUB "EFISTUB").

Drop to the build-in [UEFI shell](/index.php/UEFI#Launching_UEFI_Shell "UEFI") and call the EFI file directly. For example:

```
Shell> fs0:
FS0:\> xen-X.Y.Z.efi

```

Note that a `xen.cfg` configuration file in the [EFI system partition](/index.php/EFI_system_partition "EFI system partition") is still required as outlined above. In addition, a different configuration file may be specified with the `-cfg=file.cfg` parameter. For example:

```
Shell> fs0:
FS0:\> xen-X.Y.Z.efi -cfg=xen-rescue.cfg

```

These additional configuration files must reside in the same directory as the Xen EFI binary and linux stub files.

#### BIOS

Xen supports booting from system firmware configured as BIOS.

##### GRUB

For [GRUB](/index.php/GRUB "GRUB") users, the Xen package provides the `/etc/grub.d/09_xen` generator file. The file `/etc/xen/grub.conf` can be edited to customize the Xen boot commands. For example, to allocate 512 MiB of RAM to *dom0* at boot, modify `/etc/xen/grub.conf` by replacing the line:

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

For [Syslinux](/index.php/Syslinux "Syslinux") users, add a stanza like this to your `/boot/syslinux/syslinux.cfg`:

```
LABEL xen
    MENU LABEL Xen
    KERNEL mboot.c32
    APPEND ../xen-X.Y.Z.gz --- ../vmlinuz-linux console=tty0 root=/dev/sdaX ro --- ../initramfs-linux.img

```

where `X.Y.Z` is your xen version and `/dev/sdaX` is your [root partition](/index.php/Fstab#Identifying_filesystems "Fstab").

This also requires `mboot.c32` (and `libcom32.c32`) to be in the same directory as `syslinux.cfg`. If you do not have `mboot.c32` in `/boot/syslinux`, copy it from:

```
# cp /usr/lib/syslinux/bios/mboot.c32 /boot/syslinux

```

### Creation of a network bridge

Xen requires that network communications between *domU* and the *dom0* (and beyond) be set up manually. The use of both DHCP and static addressing is possible, and the choice should be determined by the network topology. Complex setups are possible, see the [Networking](http://wiki.xen.org/wiki/Xen_Networking) article on the Xen wiki for details and `/etc/xen/scripts` for scripts for various networking configurations. A basic bridged network, in which a virtual switch is created in *dom0* that every *domU* is attached to, can be set up by creating a [network bridge](/index.php/Network_bridge "Network bridge") with the expected name `xenbr0`.

See [Network bridge#Creating a bridge](/index.php/Network_bridge#Creating_a_bridge "Network bridge") for details.

#### Systemd-networkd

See [Systemd-networkd#Bridge interface](/index.php/Systemd-networkd#Bridge_interface "Systemd-networkd") for details.

#### Network Manager

Gnome's Network Manager can sometime be troublesome. If following the bridge creation section outlined in the [bridges](/index.php/Network_bridge "Network bridge") section of the wiki are unclear or do not work, then the following steps may work.

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

### Installation of Xen systemd services

The Xen *dom0* requires the `xenstored.service`, `xenconsoled.service`, `xendomains.service` and `xen-init-dom0.service` to be [started](/index.php/Started "Started") and possibly [enabled](/index.php/Enabled "Enabled").

### Confirming successful installation

Reboot your *dom0* host and ensure that the Xen kernel boots correctly and that all settings survive a reboot. A properly set up *dom0* should report the following when you run `xl list` as root:

 `# xl list` 
```
Name                                        ID   Mem VCPUs	State	Time(s)
Domain-0                                     0   511     2     r-----   41652.9

```

Of course, the Mem, VCPUs and Time columns will be different depending on machine configuration and uptime. The important thing is that *dom0* is listed.

In addition to the required steps above, see [best practices for running Xen](http://wiki.xen.org/wiki/Xen_Best_Practices) which includes information on allocating a fixed amount of memory and how to dedicate (pin) a CPU core for *dom0* use. It also may be beneficial to create a xenfs filesystem mount point by including in `/etc/fstab`

```
none /proc/xen xenfs defaults 0 0

```

### Configure Best Practices

Review [Xen Project Best Practices](https://wiki.xen.org/wiki/Xen_Project_Best_Practices) before using Xen.

## Using Xen

Xen supports both paravirtualized (PV) and hardware virtualized (HVM) *domU*. In the following sections the steps for creating HVM and PV *domU* running Arch Linux are described. In general, the steps for creating an HVM *domU* are independent of the *domU* OS and HVM *domU* support a wide range of operating systems including Microsoft Windows. To use HVM *domU* the *dom0* hardware must have virtualization support. Paravirtualized *domU* do not require virtualization support, but instead require modifications to the guest operating system making the installation procedure different for each operating system (see the [Guest Install](http://wiki.xen.org/wiki/Category:Guest_Install) page of the Xen wiki for links to instructions). Some operating systems (e.g., Microsoft Windows) cannot be installed as a PV *domU*. In general, HVM *domU* often run slower than PV *domU* since HVMs run on emulated hardware. While there are some common steps involved in setting up PV and HVM *domU*, the processes are substantially different. In both cases, for each *domU*, a "hard disk" will need to be created and a configuration file needs to be written. Additionally, for installation each *domU* will need access to a copy of the installation ISO stored on the *dom0* (see the [Download Page](https://www.archlinux.org/download/) to obtain the Arch Linux ISO).

### Create a domU "hard disk"

Xen supports a number of different types of "hard disks" including [Logical Volumes](/index.php/LVM "LVM"), [raw partitions](/index.php/Partitioning "Partitioning"), and image files. To create a [sparse file](https://en.wikipedia.org/wiki/Sparse_file "wikipedia:Sparse file"), that will grow to a maximum of 10GiB, called `domU.img`, use:

```
$ truncate -s 10G domU.img

```

If file IO speed is of greater importance than domain portability, using [Logical Volumes](/index.php/LVM "LVM") or [raw partitions](/index.php/Partitioning "Partitioning") may be a better choice.

Xen may present any partition / disk available to the host machine to a domain as either a partition or disk. This means that, for example, an LVM partition on the host can appear as a hard drive (and hold multiple partitions) to a domain. Note that making sub-partitons on a partition will make accessing those partitions on the host machine more difficult. See the kpartx man page for information on how to map out partitions within a partition.

### Create a domU configuration

Each *domU* requires a separate configuration file that is used to create the virtual machine. Full details about the configuration files can be found at the [Xen Wiki](http://wiki.xenproject.org/wiki/XenConfigurationFileOptions) or the `xl.cfg` man page. Both HVM and PV *domU* share some components of the configuration file. These include

```
name = "domU"
memory = 512
disk = [ "file:/path/to/ISO,sdb,r", "phy:/path/to/partition,sda1,w" ]
vif = [ 'mac=00:16:3e:XX:XX:XX,bridge=xenbr0' ]

```

The `name=` is the name by which the xl tools manage the *domU* and needs to be unique across all *domU*. The `disk=` includes information about both the the installation media (`file:`) and the partition created for the *domU* `phy`. If an image file is being used instead of a physical partition, the `phy:` needs to be changed to `file:`. The `vif=` defines a network controller. The `00:16:3e` MAC block is reserved for Xen domains, so the last three digits of the `mac=` must be randomly filled in (hex values 0-9 and a-f only).

### Managing a domU

If a *domU* should be started on boot, create a symlink to the configuration file in `/etc/xen/auto` and ensure the `xendomains` service is set up correctly. Some useful commands for managing *domU* are:

```
# xl top
# xl list
# xl console domUname
# xl shutdown domUname
# xl destroy domUname

```

## Configuring a hardware virtualized (HVM) Arch domU

In order to use HVM *domU* install the [mesa](https://www.archlinux.org/packages/?name=mesa) and [bluez-libs](https://www.archlinux.org/packages/?name=bluez-libs) packages.

A minimal configuration file for a HVM Arch *domU* is:

```
name = 'HVM_domU'
builder = 'hvm'
memory = 512
vcpus = 2
disk = [ 'phy:/dev/vg0/hvm_arch,xvda,w', 'file:/path/to/ISO,hdc:cdrom,r' ]
vif = [ 'mac=00:16:3e:00:00:00,bridge=xenbr0' ]
vnc = 1
vnclisten = '0.0.0.0'
vncdisplay = 1

```

Since HVM machines do not have a console, they can only be connected to via a [vncviewer](/index.php/Vncserver "Vncserver"). The configuration file allows for unauthenticated remote access of the *domU* vncserver and is not suitable for unsecured networks. The vncserver will be available on port `590X`, where X is the value of `vncdisplay`, of the *dom0*. The *domU* can be created with:

```
# xl create /path/to/config/file

```

and its status can be checked with

```
# xl list

```

Once the *domU* is created, connect to it via the vncserver and install Arch Linux as described in the [Installation guide](/index.php/Installation_guide "Installation guide").

## Configuring a paravirtualized (PV) Arch domU

A minimal configuration file for a PV Arch *domU* is:

```
name = "PV_domU"
kernel = "/mnt/arch/boot/x86_64/vmlinuz"
ramdisk = "/mnt/arch/boot/x86_64/archiso.img"
extra = "archisobasedir=arch archisolabel=ARCH_201301"
memory = 512
disk = [ "phy:/path/to/partition,sda1,w", "file:/path/to/ISO,sdb,r" ]
vif = [ 'mac=00:16:3e:XX:XX:XX,bridge=xenbr0' ]

```

This file needs to tweaked for your specific use. Most importantly, the `archisolabel=ARCH_201301` line must be edited to use the release year/month of the ISO being used. If you want to install 32-bit Arch, change the kernel and ramdisk paths from `x86_64` to `i686`.

Before creating the *domU*, the installation ISO must be loop-mounted. To do this, ensure the directory `/mnt` exists and is empty, then run the following command (being sure to fill in the correct ISO path):

```
# mount -o loop /path/to/iso /mnt

```

Once the ISO is mounted, the *domU* can be created with:

```
# xl create -c /path/to/config/file

```

The "-c" option will enter the *domU'*s console when successfully created. Then you can install Arch Linux as described in the [Installation guide](/index.php/Installation_guide "Installation guide"), but with the following deviations. The block devices listed in the disks line of the cfg file will show up as `/dev/xvd*`. Use these devices when partitioning the *domU*. After installation and before the *domU* is rebooted, the `xen-blkfront`, `xen-fbfront`, `xen-netfront`, `xen-kbdfront` modules must be added to [Mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"). Without these modules, the *domU* will not boot correctly. For booting, it is not necessary to install Grub. Xen has a Python-based grub emulator, so all that is needed to boot is a `grub.cfg` file: (It may be necessary to create the `/boot/grub` directory)

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

This file must be edited to match the UUID of the root partition. From within the *domU*, run the following command:

```
# blkid

```

Replace all instances of `__UUID__` with the real UUID of the root partition (the one that mounts as `/`).:

```
# sed -i 's/__UUID__/12345678-1234-1234-1234-123456789abcd/g' /boot/grub/grub.cfg

```

Shutdown the *domU* with the `poweroff` command. The console will be returned to the hypervisor when the domain is fully shut down, and the domain will no longer appear in the xl domains list. Now the ISO file may be unmounted:

```
# umount /mnt

```

The *domU* cfg file should now be edited. Delete the `kernel =`, `ramdisk =`, and `extra =` lines and replace them with the following line:

```
bootloader = "pygrub"

```

Also remove the ISO disk from the `disk =` line.

The Arch *domU* is now set up. It may be started with the same line as before:

```
# xl create -c /etc/xen/archdomu.cfg

```

## Troubleshooting

### "xl list" complains about libxl

Either you have not booted into the Xen system, or xen modules listed in `xencommons` script are not installed.

### "xl create" fails

Check the guest's kernel is located correctly, check the `pv-xxx.cfg` file for spelling mistakes (like using `initrd` instead of `ramdisk`).

### Arch Linux guest hangs with a ctrl-d message

Press `ctrl-d` until you get back to a prompt, rebuild its initramfs described

### Error message "failed to execute '/usr/lib/udev/socket:/org/xen/xend/udev_event' 'socket:/org/xen/xend/udev_event': No such file or directory"

This is caused by `/etc/udev/rules.d/xend.rules`. Xend is deprecated and not used, so it is safe to remove that file.

## See also

*   [The homepage at xen.org](http://www.xen.org/)
*   [The wiki at xen.org](http://wiki.xen.org/wiki/Main_Page)