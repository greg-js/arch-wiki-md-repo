[Windows PE](http://technet.microsoft.com/en-us/library/cc766093(v=ws.10).aspx) is a lightweight version of Windows intended to be used for installation of Windows Vista and later versions of Windows, as well as for system maintenance. It runs entirely from memory and can be booted from the network. This page describes how customized Windows PE images can be created, and optionally published on the network, using only free software packages on an Arch Linux machine along with Microsoft's Windows Automated Installation Kit (WAIK). The WAIK can be downloaded at no cost and is only needed to extract the `boot.wim` file that contains the initial copy of Windows PE, along with a couple boot files.

**Warning:**

If you boot Windows PE on a physical computer, you are placing Microsoft's closed-source code in control of that computer. You do so at your own risk.

In addition, by downloading the Windows Automated Installation Kit, you may be bound by its license, which prevents you from, among other things, using Windows PE as a general-purpose operating system.

## Contents

*   [1 Use cases](#Use_cases)
*   [2 Creating a bootable Windows PE ISO](#Creating_a_bootable_Windows_PE_ISO)
*   [3 Booting Windows PE](#Booting_Windows_PE)
    *   [3.1 In virtual machine](#In_virtual_machine)
    *   [3.2 From CD](#From_CD)
    *   [3.3 From Network](#From_Network)
    *   [3.4 Network boot performance](#Network_boot_performance)
*   [4 Customizing Windows PE](#Customizing_Windows_PE)
*   [5 See also](#See_also)

## Use cases

Normally, an image of Windows PE can only be created using the Windows Automated Installation Kit (WAIK) on a Windows machine. However, it is also possible to create and modify images of Windows PE using an (Arch) Linux machine, and optionally publish them on the network for PXE booting. No Windows machine is necessary. You may want to do this if:

*   you need to install Windows from the network, or boot Windows PE from the network for system administration, using an Arch Linux-based server. This may be because you do not have a Windows-based server, or you prefer using a Linux server because of its improved security and configurability, or you are already using a Linux server for other purposes.
*   you need to run a Windows environment to run Win32 programs, you do not have a Windows machine available, and you do not want to use [Wine](/index.php/Wine "Wine") or the programs will not run correctly with [Wine](/index.php/Wine "Wine").

## Creating a bootable Windows PE ISO

Download the Windows Automated Installation Kit (WAIK) from [Microsoft's website](http://www.microsoft.com/en-us/download/details.aspx?id=5753).

**Warning:** The entire download, `KB3AIK_EN.iso`, is 1.7GB.

**Tip:**

*   It may be possible to use [httpfs](http://httpfs.sourceforge.net/) to avoid downloading the entire file. Only around 118MB of it is actually needed.
*   If you have an installation media of Windows 7 or later versions, you can use that iso file / optical disc instead of WAIK. `mkwinpeimg` accepts both WAIK image and Windows installation media. Note that different versions of Windows installation media contains different versions of Windows PE. For the relationship between Windows versions and Windows PE versions, refer to [Wikipedia](https://en.wikipedia.org/wiki/Windows_Preinstallation_Environment#Versions).
*   WAIK has been renamed to WADK since Windows 8 and is now distributed via `adksetup.exe`. In order to get Windows PE 4.0 and later versions, you have to use installation media of Windows 8 and later versions. The installation media iso files are avaiable for MSDN subscribers, but you can download otherwhere and compare the hash value with the those published on MSDN.

[Install](/index.php/Install "Install") [fuse](https://www.archlinux.org/packages/?name=fuse), [cdrkit](https://www.archlinux.org/packages/?name=cdrkit), and [cabextract](https://www.archlinux.org/packages/?name=cabextract) from [official repositories](/index.php/Official_repositories "Official repositories").

Install [wimlib](https://aur.archlinux.org/packages/wimlib/) from the [AUR](/index.php/AUR "AUR").

Mount the WAIK ISO:

```
# mkdir /media/waik
# mount KB3AIK_EN.iso /media/waik

```

Use the `mkwinpeimg` script provided with [wimlib](https://aur.archlinux.org/packages/wimlib/) to create a bootable Windows PE ISO `winpe.iso`:

```
$ mkwinpeimg --iso --waik-dir=/media/waik winpe.iso

```

See the `man mkwinpeimg` for more information.

Unmount the WAIK ISO:

```
# umount /media/waik

```

## Booting Windows PE

After creating a bootable ISO of Windows PE (`winpe.iso`) as described in the previous section, you may want to boot Windows PE in the following ways:

### In virtual machine

Run a virtual machine with `winpe.iso` attached as a CD-ROM. Be sure to give it adequate memory, definitely more than the size of the ISO, since Windows PE runs from memory. See [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors") for a list of available virtualization software.

### From CD

Simply [burn](/index.php/Optical_disc_drive#Burning "Optical disc drive") `winpe.iso` onto a CD, and you can boot from it.

### From Network

Windows PE can be booted from the network using [PXELINUX](http://www.syslinux.org/wiki/index.php/PXELINUX) and its [MEMDISK](http://www.syslinux.org/wiki/index.php/MEMDISK) module.

Install [syslinux](https://www.archlinux.org/packages/?name=syslinux) and [tftp-hpa](https://www.archlinux.org/packages/?name=tftp-hpa).

Copy needed PXELINUX files to the [TFTP server](/index.php/Tftpd_server "Tftpd server") root directory.

```
# cp /usr/lib/syslinux/{pxelinux.0,menu.c32,memdisk} /var/tftpboot

```

Put `winpe.iso` in the [TFTP server](/index.php/Tftpd_server "Tftpd server") root directory.

```
# mv winpe.iso /var/tftpboot

```

Create a [configuration file](/index.php/Syslinux#Configuring_syslinux "Syslinux") for PXELINUX similar to the following:

 `/var/tftpboot/pxelinux.cfg/default` 

```
UI         menu.c32
MENU TITLE Network Boot
TIMEOUT    50

LABEL      winpe
MENU LABEL Boot Windows PE from network
KERNEL     /memdisk
INITRD     winpe.iso
APPEND     iso raw

LABEL      localboot
MENU LABEL Boot from local disk
LOCALBOOT  0

```

Start the [TFTP server](/index.php/Tftpd_server "Tftpd server").

Configure your DHCP server (such as [Dhcpd](/index.php/Dhcpd "Dhcpd") or [Dnsmasq](/index.php/Dnsmasq "Dnsmasq")) to point to `pxelinux.0` as the boot file, with the Linux server's IP address. Beware: if your DHCP server is on a router, it may not be possible to do this without installing custom firmware.

After completing the above steps, you should be able to boot Windows PE from the network.

**Note:** With the given PXELINUX configuration file, Windows PE will start by default after 5 seconds.

### Network boot performance

TFTP is not designed to be used to transfer large files, such as `winpe.iso`, which may be 118MB or more. Performance may be improved by using the `gpxelinux.0` bootloader instead of `pxelinux.0` and loading `winpe.iso` using HTTP rather than TFTP.

## Customizing Windows PE

The `mkwinpeimg` script provided with [wimlib](https://aur.archlinux.org/packages/wimlib/) supports making modifications to Windows PE using the `--start-script` or `--overlay` options. See the manual page for `mkwinpeimg` for more information.

You may want to do this to add additional Windows applications that you want to run in Windows PE, or to add any additional drivers that Windows PE needs (drivers can be loaded using the `drvload` command within Windows PE).

## See also

*   [Microsoft's documentation for Windows PE](http://technet.microsoft.com/en-us/library/cc766093(v=ws.10).aspx)
*   [Another article about making Windows PE images on Linux](http://www.thinkwiki.org/wiki/Windows_PE)