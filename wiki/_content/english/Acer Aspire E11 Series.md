| **Device** | **Working** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Network](/index.php/Network "Network") | Yes |
| [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") | Manual |
| Atheros Wireless | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Manual |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| Card Reader | Yes |
| [Power management](/index.php/Power_management "Power management") | No |

[Aspire E11 Series](http://us.acer.com/ac/en/US/content/models/laptops/aspire-e11)

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Create a recovery drive](#Create_a_recovery_drive)
    *   [1.2 Booting](#Booting)
        *   [1.2.1 Using UEFI](#Using_UEFI)
*   [2 Configuration](#Configuration)
    *   [2.1 Wireless](#Wireless)
    *   [2.2 Touchpad](#Touchpad)
    *   [2.3 Power Management](#Power_Management)
        *   [2.3.1 Suspend and Hibernate](#Suspend_and_Hibernate)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 GPU](#GPU)
    *   [3.2 Start up and shutdown freeze](#Start_up_and_shutdown_freeze)
    *   [3.3 Bluetooth can't find any devices](#Bluetooth_can.27t_find_any_devices)
*   [4 See also](#See_also)

## Installation

**Warning:** Should you wish to return to *Windows 8.1 with Bing*, it is imperative to [#Create a recovery drive](#Create_a_recovery_drive). The correct installation medium is only available to system manufacturers, and you will have to either use this recovery drive, or send the device back for repair to return to the original state.

**Warning:** The BIOS firmware in Legacy mode (including latest versions) has several bugs (inability to turn off or suspend the computer, kernel panics, etc). Use UEFI instead.

Prior to installation, download and install the latest firmware update from [Acer](http://us.acer.com/ac/en/US/content/drivers) under Windows. Older versions of the firmware can only boot from the (black) USB 2.0 port.

To recover the Windows key at a later stage, run:

```
$ hexdump -C /sys/firmware/acpi/tables/MSDM

```

Note that this key is tied to the particular laptop model and [unusable elsewhere](http://arstechnica.com/civis/viewtopic.php?p=26623117#p26623117). See also [[1]](https://msdn.microsoft.com/en-us/library/windows/hardware/dn653305%28v=vs.85%29.aspx).

### Create a recovery drive

A recovery drive can made with the preinstalled *Acer eRecovery Management* application. This requires a USB-attached flash drive or hard disk with at least 16 GB free space available, and presence of the `C:/OEM` directory. All present data on the target drive will be lost.

Choose the option *Create Factory Default Backup*, select the partition Windows is installed on, and click *start*. Remove the drive afterwards - booting from the device will now start the recovery software. See [[2]](http://acer--uk.custhelp.com/app/answers/detail/a_id/14303/~/create-a-recovery-usb-flash-drive-with-acer-erecovery-management-5.x) for more information.

### Booting

The Acer E3-111 does not have an optical drive. See [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") for alternative methods.

Both [UEFI](/index.php/UEFI "UEFI") and Legacy (BIOS) boot are supported. To switch modes, press `F2` at the boot splash screen to enter the EFI setup, then select the *Boot* tab. Alternatively, access the EFI setup by [rebooting in Windows](http://acer-au.custhelp.com/app/answers/detail/a_id/32048/~/accessing-uefi-in-windows-8.1).

Follow the [installation guide](/index.php/Installation_guide "Installation guide"). An Ethernet connection is recommended, as the needed [wireless drivers](#Wireless) are not included in the installation medium.

**Note:**

*   Installation images prior to `archlinux-2015.05.01-dual.iso` return a row of errors when accessing the RPMB (Replay Protected Memory Block) partition from the eMMC. [[3]](https://bugs.launchpad.net/ubuntu/+source/systemd/+bug/1333140)
*   eMMC device names start with `/dev/mmcblk` instead of the typical `/dev/sda`.
*   Due to limited RAM, it is recommended to create a [swap](/index.php/Swap "Swap") partition of at least 2 GB in size.

#### Using UEFI

**Note:** **gummiboot** is now called [systemd-boot](/index.php/Systemd-boot "Systemd-boot").

To use Arch Linux with UEFI, activate the F12 boot menu option in the EFI setup and disable 'Secure' Boot. To do the latter, you must set a supervisor password beforehand. After disabling 'Secure' Boot, save the settings and reboot, then press F12 and select the USB drive with the Arch Linux setup files.

The first partition should be an EFI system partition. Make sure that the initramfs and vmlinuz-linux files are on the EFI partition, and that it is mounted at /boot. There is no way to specify kernel boot parameters in this computer's EFI setup so you have to go with a boot loader. Simple way is to install **gummiboot** and create a boot entry:

```
/boot/loader/entries/archlinux.conf:
title		Arch Linux
linux		/vmlinuz-linux
initrd		/intel-ucode.img
initrd		/initramfs-linux.img
options		root=/dev/mmcblk0p2 rootwait

```

This assumes that your root is on the second partition (first partition is the EFI partition) and states **rootwait** because the integrated flash storage is not available instantly after kernel startup. When you are done with the Arch setup, reboot and press F2 to enter the EFI setup. Enable 'secure' boot again, then choose the option 'select an UEFI file as trusted for executing' and browse to the gummiboot/gummibootx64.efi file, then press ENTER. Now disable 'secure' boot again, put the gummiboot loader on top of the list in the boot priority menu, and remove the supervisor password. Save the settings and reboot into your fresh Arch system.

**Note:** A UEFI boot entry may not appear upon booting the device. The solution is to copy the `.efi` file to the location Windows uses. See [UEFI#UEFI boot loader does not show up in firmware menu](/index.php/UEFI#UEFI_boot_loader_does_not_show_up_in_firmware_menu "UEFI") for details.

## Configuration

### Wireless

To use the Broadcom BCM43142 chipset is, install [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) from the [AUR](/index.php/AUR "AUR"), and load the module:

```
# modprobe wl

```

The system will now recognize the interface as `wlp2s0`. See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") and [Wireless](/index.php/Wireless "Wireless") for details.

### Touchpad

The E11 series include a [Precision Touchpad](http://windows.microsoft.com/en-us/windows-8/touchpad), which supports a variety of touch gestures. To enable the touchpad, append the `i8042.nopnp` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") for configuration details.

### Power Management

You may need to use the linux-lst kernel for full support.

#### Suspend and Hibernate

Suspend and Hibernate should work after following [Power management/Suspend and hibernate](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate").

## Troubleshooting

### GPU

See [Intel graphics#SNA issues](/index.php/Intel_graphics#SNA_issues "Intel graphics").

### Start up and shutdown freeze

If you have an issue where the computer freezes during start up and shutdown, requiring multiple reboots, try adding the following to `/etc/modprobe.d/blacklist.conf`

```
blacklist dw_dmac
blacklist dw_dmac_core

```

See also [[4]](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1341925) [[5]](https://bugzilla.redhat.com/show_bug.cgi?id=1213216)

### Bluetooth can't find any devices

Some laptops have an Atheros AR9565 Wifi/Bluetooth controller built in:

```
# lsusb
...
Bus 001 Device 005: ID 04ca:3014 Lite-On Technology Corp. Qualcoom Atheros Bluetooth
...

```

Wifi works fine, the bluetooth controller is recognized but no bluetooth devices are found. The problem is that as of Linux 4.3.3 this devices is not listed in `ath9k.ko` which loads the firmware files and patches into the Atheros bluetooth controllers.

Quick and dirty fix, patching this USB ID into the modules (from: [https://bbs.archlinux.org/viewtopic.php?pid=1433352](https://bbs.archlinux.org/viewtopic.php?pid=1433352)):

```
cp -i ath3k.ko.gz ath3k.ko.gz.ori
cp -i btusb.ko.gz btusb.ko.gz.ori
gunzip ath3k.ko.gz btusb.ko.gz
sed -e 's/\xca\x04\x10\x30/\xca\x04\x14\x30/g' ath3k.ko > a
sed -e 's/\xca\x04\x10\x30/\xca\x04\x14\x30/g' btusb.ko > b
mv a ath3k.ko
mv b btusb.ko
gzip ath3k.ko btusb.ko

```

You will still need to copy two firmware files (`AthrBT_0x31010100.dfu` and `ramps_0x31010100_40.dfu`) under `/lib/firmware/ar3k`.

Fortunately, Ubuntu Forums user Ephialta links to a Windows driver update archive (.cab) containing the missing firmware files: [http://ubuntuforums.org/showthread.php?t=2260501&p=13207809#post13207809](http://ubuntuforums.org/showthread.php?t=2260501&p=13207809#post13207809)

## See also

*   [Disassembly Acer E11 (RAM, HDD upgrade)](https://www.youtube.com/watch?v=5OT_RnjMess)
*   [Installing Linux on Acer E11-111 (ES1-111-C3NT)](http://blog.mdda.net/oss/2014/11/16/acer-e11-es1-111-c3nt-linux/)