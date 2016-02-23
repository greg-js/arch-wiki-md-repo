## Contents

*   [1 System Specifications](#System_Specifications)
    *   [1.1 What works/What doesn't](#What_works.2FWhat_doesn.27t)
*   [2 Pre-installation notes](#Pre-installation_notes)
*   [3 Accessing the recovery partition with GRUB](#Accessing_the_recovery_partition_with_GRUB)
*   [4 Configuration](#Configuration)
    *   [4.1 Video Driver](#Video_Driver)
        *   [4.1.1 Nvidia](#Nvidia)
    *   [4.2 Network](#Network)
        *   [4.2.1 Wireless](#Wireless)
    *   [4.3 Mouse settings](#Mouse_settings)
    *   [4.4 ThinkFinger](#ThinkFinger)
    *   [4.5 Hotswap UltraBay devices](#Hotswap_UltraBay_devices)
    *   [4.6 Multimedia Keys](#Multimedia_Keys)
    *   [4.7 HDAPS](#HDAPS)
*   [5 Other Tweaks](#Other_Tweaks)
    *   [5.1 HDD clicks](#HDD_clicks)
*   [6 See also](#See_also)

## System Specifications

Lenovo ThinkPad T61 - Intel Centrino Pro

*   Intel(R) Core(TM)2 Duo CPU T7300 (2.00GHz, 4MB, 800MHz)
*   Mobile Intel 965GM Express Chipset
*   2GB PC2-5300/677MHz
*   80-GB 5400 rpm SATA Harddrive
*   14.1-inch color TFT WXGA+ (1440 x 900, 200 nit)
*   Intel® Graphics Media Accelerator GM965 (128MB)
*   82801H ICH8 Family HD Audio Controller
*   DVD-ROM, CD-RW/DVD Combo, Multi-Burner Plus
*   Modem; Gigabit Ethernet
*   Intel® Wireless Wi-Fi Link 4965AG
*   1 Type II PC Card slot
*   1 ExpressCard 34/54
*   Dual pointing devices (both Pointstick and Touchpad)

Output of lshwd

```
00:00.0 Class 0600: Intel Corporation|Mobile Memory Controller Hub (unknown)
00:02.0 Class 0300: Intel Corporation|Mobile Integrated Graphics Controller (vesa)
00:02.1 Class 0380: Intel Corporation|Mobile Integrated Graphics Controller (vesa)
00:19.0 Class 0200: Intel Corporation|Mobile Integrated Graphics Controller (unknown)
00:1a.0 Class 0c03: Intel Corporation|USB UHCI Controller #4 (unknown)
00:1a.1 Class 0c03: Intel Corporation|USB UHCI Controller #5 (unknown)
00:1a.7 Class 0c03: Intel Corporation|USB2 EHCI Controller #2 (unknown)
00:1b.0 Class 0403: Intel Corp.|ICH8 HD Audio DID (snd-hda-intel)
00:1c.0 Class 0604: Intel Corporation|PCI Express Port 1 (unknown)
00:1c.1 Class 0604: Intel Corporation|PCI Express Port 2 (unknown)
00:1c.2 Class 0604: Intel Corporation|PCI Express Port 3 (unknown)
00:1c.3 Class 0604: Intel Corporation|PCI Express Port 4 (unknown)
00:1c.4 Class 0604: Intel Corporation|PCI Express Port 5 (unknown)
00:1d.0 Class 0c03: Intel Corporation|USB UHCI Controller #1 (unknown)
00:1d.1 Class 0c03: Intel Corporation|USB UHCI Controller #2 (unknown)
00:1d.2 Class 0c03: Intel Corporation|USB UHCI Controller #3 (unknown)
00:1d.7 Class 0c03: Intel Corporation|USB2 EHCI Controller #1 (unknown)
00:1e.0 Class 0604: Intel Corp.|82801 Hub Interface to PCI Bridge (hw_random)
00:1f.0 Class 0601: Intel Corporation|Mobile LPC Interface Controller (unknown)
00:1f.2 Class 0101: Intel Corporation|Mobile SATA Controller cc=IDE (ata_piix)
00:1f.3 Class 0c05: Intel Corporation|SMBus Controller (i2c-i801)
03:00.0 Class 0280: Intel Corporation|SMBus Controller (unknown)
15:00.0 Class 0607: Ricoh Co Ltd.|RL5c476 II (yenta_socket)
15:00.1 Class 0c00: Ricoh Co Ltd.|RL5c476 II (unknown)
15:00.2 Class 0805: Ricoh Co Ltd.|SD Card reader (unknown)
15:00.3 Class ffff: Ricoh Co Ltd.|SD Card reader (unknown)
15:00.4 Class 0880: Ricoh Co Ltd.|R5C592 Memory Stick Bus Host Adapter (unknown)
15:00.5 Class 0880: Ricoh Co Ltd.|xD-Picture Card Controller (unknown)

```

### What works/What doesn't

Pretty much everything works on this laptop. The modem is untested.

## Pre-installation notes

Remember to back up the restore partition if you plan to restore it, or leave it.

Follow the [official Arch Linux install guide](/index.php/Installation_guide "Installation guide")

## Accessing the recovery partition with GRUB

Edit your **/boot/grub/menu.lst** file and add the following:

```
# booting "Rescue and Recovery" partition from Lenovo
title Thinkpad Maintenance
unhide (hd0,0)
rootnoverify (hd0,0)
chainloader +1

```

## Configuration

### Video Driver

#### Nvidia

Follow the instructions in [NVIDIA](/index.php/NVIDIA "NVIDIA").

**Note:** If you're following the [Beginners Guide](/index.php/Beginners_Guide "Beginners Guide") and you're not seeing the cursor after the NVIDIA logo, you should try the simple baseline X test.

### Network

#### Wireless

Uses either module, varies with different setups:

*   iwl3945
*   iwl4965

Requires firmware be installed to work.

Refer to [Wireless network configuration#Intel](/index.php/Wireless_network_configuration#Intel "Wireless network configuration")

### Mouse settings

See [TrackPoint](/index.php/TrackPoint "TrackPoint") and [Synaptics](/index.php/Synaptics "Synaptics").

### ThinkFinger

See [ThinkFinger](/index.php/ThinkFinger "ThinkFinger").

### Hotswap UltraBay devices

If you want to be able to eject devices from the Thinkpad's UltraBay using Fn+F9 create a script named for example "tp_ultrabay_eject.sh" with the content from [[1]](http://www.thinkwiki.org/wiki/How_to_hotswap_Ultrabay_devices#Script_for_Ultrabay_eject).

As stated at the top of the script, the variable "DEVPATH" (near the top of the script) has to be changed to match your system. Insert the UltraBay optical drive and run:

```
udevadm info --query=path --name=/dev/sr0 | perl -pe 's!/block/...$!!'

```

Replace the value of "DEVPATH" with the output of that command.

Now change ownership and permissions of the script:

```
chown root:root tp_ultrabay_eject.sh
chmod 555 tp_ultrabay_eject.sh

```

Move it somewhere save and add it to your /etc/acpi/handler.sh (under section "ibm/hotkey)"):

```
              00001009) # Eject from dock
                  DISPLAY=:0.0 /path/to/tp_ultrabay_eject.sh
                  ;;

```

"DISPLAY=:0.0" is necessary to tell X where to send notifications to.

Now, pressing Fn+F9 unmounts the relevant filesystems, powers off the UltraBay and notifies you (using notify-send) about what's happening. If a filesystem can't be unmounted you get a warning message.

It is also possible to achieve the above by just releasing the UltraBay eject lever (without pressing Fn+F9 before). Consult [http://www.thinkwiki.org/wiki/How_to_hotswap_Ultrabay_devices](http://www.thinkwiki.org/wiki/How_to_hotswap_Ultrabay_devices) for detailed instructions on how to get it working.

### Multimedia Keys

See [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys").

### HDAPS

See [HDAPS](/index.php/HDAPS "HDAPS").

## Other Tweaks

### HDD clicks

Install [hdparm](/index.php/Hdparm "Hdparm") and run the following command on system startup:

```
# hdparm -B 244 /dev/sda

```

Details: [http://www.thinkwiki.org/wiki/Problem_with_hard_drive_clicking](http://www.thinkwiki.org/wiki/Problem_with_hard_drive_clicking)

## See also

*   [http://www.thinkwiki.org/wiki/ThinkWiki](http://www.thinkwiki.org/wiki/ThinkWiki)
*   This report is listed at the [TuxMobil: Linux Laptop and Notebook Installation Guides Survey: Fujitsu-Siemens - FSC](http://tuxmobil.org/fujitsu.html).