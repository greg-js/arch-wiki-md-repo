[Windows PE](http://technet.microsoft.com/en-us/library/cc766093(v=ws.10).aspx) is a lightweight version of Windows intended to be used for installation of Windows Vista and later versions of Windows, as well as for system maintenance. It runs entirely from memory and can be booted from the network. This page describes how customized Windows PE images can be created, and optionally published on the network, using only free software packages on an Arch Linux machine along with Microsoft's Windows Automated Installation Kit (WAIK). The WAIK can be downloaded at no cost and is only needed to extract the `boot.wim` file that contains the initial copy of Windows PE, along with a couple boot files.

**Warning:** By downloading the Windows Automated Installation Kit, you may be bound by its license, which prevents you from, among other things, using Windows PE as a general-purpose operating system.

## Contents

*   [1 Use cases](#Use_cases)
*   [2 Creating a bootable Windows PE image](#Creating_a_bootable_Windows_PE_image)
    *   [2.1 Configure the Windows PE image](#Configure_the_Windows_PE_image)
    *   [2.2 Make the bootable Windows PE ISO](#Make_the_bootable_Windows_PE_ISO)
*   [3 Booting Windows PE](#Booting_Windows_PE)
    *   [3.1 In virtual machine](#In_virtual_machine)
    *   [3.2 From CD](#From_CD)
    *   [3.3 From Network](#From_Network)
*   [4 Installing Windows from Windows PE](#Installing_Windows_from_Windows_PE)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 System error 58 has occurred. The specified server cannot perform the requested operation](#System_error_58_has_occurred._The_specified_server_cannot_perform_the_requested_operation)
*   [6 See also](#See_also)

## Use cases

Normally, an image of Windows PE can only be created using the Windows Automated Installation Kit (WAIK) on a Windows machine. However, it is also possible to create and modify images of Windows PE using an (Arch) Linux machine, and optionally publish them on the network for PXE booting. No Windows machine is necessary. You may want to do this if:

*   you need to install Windows from the network, or boot Windows PE from the network for system administration, using an Arch Linux-based server. This may be because you do not have a Windows-based server, or you prefer using a Linux server because of its improved security and configurability, or you are already using a Linux server for other purposes.
*   you need to run a Windows environment to run Win32 programs, you do not have a Windows machine available, and you do not want to use [Wine](/index.php/Wine "Wine") or the programs will not run correctly with [Wine](/index.php/Wine "Wine").

## Creating a bootable Windows PE image

Install [wimlib](https://www.archlinux.org/packages/?name=wimlib).

### Configure the Windows PE image

To boot into a command prompt, create a startup script, which will be included into the bootable image in the next step:

 `start.cmd` 
```
cmd.exe
pause

```

The `mkwinpeimg` script supports making further modifications to Windows PE using `--overlay` option. See the manual page for `mkwinpeimg` for more information. You may want to do this to add additional Windows applications that you want to run in Windows PE, or to add any additional drivers that Windows PE needs (drivers can be loaded using the `drvload` command within Windows PE).

### Make the bootable Windows PE ISO

`mkwinpeimg` can create a bootable Windows PE ISO from either Windows installation image / disk for Windows 7 or later or from Windows Automated Installation Kit (WAIK) image. In order to get Windows PE 4.0 and later versions, you have to use installation media of Windows 8 and later versions. Earlier versions of Windows PE can be obtained from [standalone WAIK distribution from Microsoft](http://www.microsoft.com/en-us/download/details.aspx?id=5753). Since Windows 8, WAIK has been renamed to WADK and is distributed via `adksetup.exe`.

The installation media iso files are avaiable for MSDN subscribers, but you can download otherwhere and compare the hash value with the those published on MSDN. Different versions of Windows installation media contains different versions of Windows PE. For the relationship between Windows versions and Windows PE versions, refer to [Wikipedia](https://en.wikipedia.org/wiki/Windows_Preinstallation_Environment#Versions "wikipedia:Windows Preinstallation Environment").

**Tip:** It may be possible to use [httpfs](http://httpfs.sourceforge.net/) to avoid downloading the entire image file. Windows PE occupies only around 118MB of the image.

Mount the source ISO, either Windows installation image or WAIK/WADK, named winimg.iso:

```
# mkdir /media/winimg
# mount winimg.iso /media/winimg

```

Use the `mkwinpeimg` script provided with [wimlib](https://www.archlinux.org/packages/?name=wimlib) to create a bootable Windows PE ISO `winpe.iso`, with the startup script created in the previous section:

**Option A**: source image is Windows installation media

```
$ mkwinpeimg --iso --windows-dir=/media/winimg --start-script=start.cmd winpe.iso

```

**Option B**: source image is WAIK/WADK:

```
$ mkwinpeimg --iso --waik-dir=/media/winimg --start-script=start.cmd winpe.iso

```

See the [mkwinpeimg(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mkwinpeimg.1) for more information.

Unmount the source ISO:

```
# umount /media/winimg

```

## Booting Windows PE

After creating a bootable ISO of Windows PE (`winpe.iso`) as described in the previous section, you may want to boot Windows PE in the following ways:

### In virtual machine

Run a virtual machine with `winpe.iso` attached as a CD-ROM. Be sure to give it adequate memory, definitely more than the size of the ISO, since Windows PE runs from memory. See [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors") for a list of available virtualization software.

### From CD

Simply [burn](/index.php/Optical_disc_drive#Burning "Optical disc drive") `winpe.iso` onto a CD, and you can boot from it.

### From Network

Windows PE can be booted from the network using [PXELINUX](http://www.syslinux.org/wiki/index.php/PXELINUX) and its [MEMDISK](http://www.syslinux.org/wiki/index.php/MEMDISK) module on BIOS systems. For UEFI systems, [wimboot](http://ipxe.org/wimboot) and [iPXE](http://ipxe.org) can be used.

Install [syslinux](https://www.archlinux.org/packages/?name=syslinux) and [tftp-hpa](https://www.archlinux.org/packages/?name=tftp-hpa).

Copy needed PXELINUX files to the [TFTP server](/index.php/Tftpd_server "Tftpd server") root directory.

```
# rsync -aq /usr/lib/syslinux/bios/ /var/tftpboot/

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

**Tip:** TFTP is not designed to be used to transfer large files, such as `winpe.iso`, which may be 118MB or more and take about 30 seconds to load. Performance may be improved by using the `gpxelinux.0` bootloader instead of `pxelinux.0` and loading `winpe.iso` using HTTP rather than TFTP.

## Installing Windows from Windows PE

Once booted into Windows PE, you can install Windows from an installation media.

The installation media can be a network share (Samba). See [Samba](/index.php/Samba "Samba") for seting up a Samba server on another machine on the LAN. To share the installation image mounted at `/media/winimg`, add the following share definition to `/etc/samba/smb.conf`:

 `/etc/samba/smb.conf` 
```
[REMINST]
browsable = true
read only = no
guest ok = yes
path = /media/winimg

```

Once booted into Windows PE command prompt, run the following command to initialize the network interface, obtain the IP of the Samba server (assuming Windows PE was booted over PXE from a machine that runs the DHCP, TFTP, and Samba server, the server IP will usually be the Gateway IP), mount the share, and launch the GUI setup:

```
 > wpeinit
 > ipconfig
 > net use I: \\IP.ADDRESS.OF.SAMBA.SERVER\REMINST
 > I:\setup.exe

```

## Troubleshooting

### System error 58 has occurred. The specified server cannot perform the requested operation

If you are getting the following error when using the `net use` command:

```
System error 58 has occurred.

The specified server cannot perform the requested operation.

```

1\. Make sure you haven't accidentally unmounted the `/media/winimg` directory.

2\. Add a `map to guest` to `/etc/samba/smb.conf`. Add the following at the top of the file:

 `/etc/samba/smb.conf` 
```
[global]
map to guest = Bad User
...

```

3\. Restart the `smbd.service`.

4\. Specify any username/password in the net use command:

```
net use I: \\IP.ADDRESS.OF.SAMBA.SERVER\REMINST /user:user pass

```

This is happening because Windows 10 connects to anonymous shares by checking some username and password to see if it is able to log in, and if so it allows an anonymous connection. Apparently whatever part hides this from the user didn't make it into the PE build.

## See also

*   [Microsoft's documentation for Windows PE](http://technet.microsoft.com/en-us/library/cc766093(v=ws.10).aspx)
*   [Another article about making Windows PE images on Linux](http://www.thinkwiki.org/wiki/Windows_PE)
*   [A guide with scripts for unattended installation of Windows 7 from Linux using Windows PE](http://www.ultimatedeployment.org/win7pxelinux1.html)
*   [Windows 10 PE Unable to map network drive anonymously](https://serverfault.com/a/858269/206710)