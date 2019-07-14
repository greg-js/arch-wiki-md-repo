**Note:** This page refers to the 7590 revision of the XPS 15\. Most of it also applies to the Precision 5540.

| **Device/Functionality** | **Status** |
| [Suspend](#Suspend) | Working |
| [Hibernate](#Hibernate) | Working |
| [Integrated Graphics](#Graphics) | Working |
| [Discrete Nvidia Graphics](#Graphics) | Modify |
| [Wifi](#Wifi_and_Bluetooth) | Modify |
| [Bluetooth](#Wifi_and_Bluetooth) | Working |
| [rfkill](#Wifi_and_Bluetooth) | Working |
| Audio | Working |
| [Touchpad](#Touchpad_and_Touchscreen) | Working |
| [Touchscreen](#Touchpad_and_Touchscreen) | Working |
| Webcam | Working |
| Card Reader | Working |
| Function/Multimedia Keys | Working |
| [Power Management](#Power_Management) | Working |
| [EFI firmware updates](#EFI_firmware_updates) | Working |
| [Fingerprint reader](#Fingerprint_reader) | Not working |

This page contains recommendations for running Arch Linux on the Dell XPS 15 7590 (2019).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 UEFI](#UEFI)
    *   [1.1 Firmware Update](#Firmware_Update)
*   [2 Power Management](#Power_Management)
    *   [2.1 Suspend](#Suspend)
    *   [2.2 Hibernate](#Hibernate)
    *   [2.3 Powertop](#Powertop)
*   [3 Graphics](#Graphics)
    *   [3.1 kernel modules](#kernel_modules)
    *   [3.2 NVIDIA Optimus](#NVIDIA_Optimus)
*   [4 Wifi and Bluetooth](#Wifi_and_Bluetooth)
    *   [4.1 WIFI](#WIFI)
*   [5 Touchpad and Touchscreen](#Touchpad_and_Touchscreen)
*   [6 Docks](#Docks)
*   [7 EFI firmware updates](#EFI_firmware_updates)
*   [8 Thermal management](#Thermal_management)
*   [9 Tips and Tricks](#Tips_and_Tricks)

## UEFI

Before installing it is necessary to modify some UEFI Settings. They can be accessed by pressing the F2 key repeatedly when booting.

*   Change the SATA Mode from the default "RAID" to "AHCI". This will allow Linux to detect the NVME SSD. If dual booting with an existing Windows installation, Windows will not boot after the * change but [this can be fixed without a reinstallation](https://triplescomputers.com/blog/uncategorized/solution-switch-windows-10-from-raidide-to-ahci-operation/).
*   Change Fastboot to "Thorough" in "POST Behaviour". This prevents intermittent boot failures.
*   Disable secure boot to allow Linux to boot.

The WIFI will not be working out of the box, a internet connection via cable or USB tethering is needed. To get it working, a manual installation of the driver is required, see [Dell XPS 15 7590#WIFI](/index.php/Dell_XPS_15_7590#WIFI "Dell XPS 15 7590").

### Firmware Update

Firmware images can be found at [Dell support page](https://www.dell.com/support/home/us/en/04/product-support/product/xps-15-7590-laptop/drivers). Keeping an existing Windows system will make updates of BIOS much simpler. If a clean Arch Linux install is the case in order to install:

*   Download the desired firmware from section "Dell XPS 15 7590 System BIOS"
*   Save it in `/boot/EFI/Dell/Bios/` (this path may vary, depending on your installation)
*   Reboot the system, and enter the boot menu by pressing repeatedly `F12` on Dell logo
*   Choose "Bios Flash Update"
*   Select the file previously saved, and start the process

The process will take about five minutes, during which the system will have some reboots and push fans at maximum speed. Finally the system will reboot normally.

## Power Management

### Suspend

### Hibernate

### Powertop

## Graphics

### kernel modules

### NVIDIA Optimus

## Wifi and Bluetooth

### WIFI

WIFI will not be working out of the box, a manual installation is required. Connect to the internet via a cable or via USB tethering, then consult [this page](https://support.killernetworking.com/knowledge-base/killer-ax1650-in-debian-ubuntu-16-04/), i.e.

```
$ pacman -S git
$ git clone [https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git](https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git)
$ cd backport-iwlwifi
$ make defconfig-iwlwifi-public
$ make -j4
$ sudo make install

```

Additionally, you will need to ensure you have the latest iwlwifi firmware:

```
$ sudo git clone [git://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git](git://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git)
$ cd linux-firmware
$ sudo cp iwlwifi-* /lib/firmware/

```

Reboot.

## Touchpad and Touchscreen

## Docks

## EFI firmware updates

## Thermal management

## Tips and Tricks