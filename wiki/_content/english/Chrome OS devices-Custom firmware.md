**Warning:** This article relies on third-party scripts and modifications, and may irreparably damage your hardware or data. Proceed at your own risk.

## Contents

*   [1 Introduction](#Introduction)
    *   [1.1 Why flash a custom firmware?](#Why_flash_a_custom_firmware.3F)
        *   [1.1.1 Pros](#Pros)
        *   [1.1.2 Cons](#Cons)
*   [2 Flashing the custom firmware](#Flashing_the_custom_firmware)
    *   [2.1 Disable the hardware write protection](#Disable_the_hardware_write_protection)
    *   [2.2 Flashing with John Lewis' script](#Flashing_with_John_Lewis.27_script)
        *   [2.2.1 Understanding the script](#Understanding_the_script)
            *   [2.2.1.1 What John Lewis' getnflash_johnlewis_rom.sh script does ?](#What_John_Lewis.27_getnflash_johnlewis_rom.sh_script_does_.3F)
            *   [2.2.1.2 What the script does not do ?](#What_the_script_does_not_do_.3F)
            *   [2.2.1.3 Conclusions](#Conclusions)
        *   [2.2.2 Running the script in Chrome OS](#Running_the_script_in_Chrome_OS)
        *   [2.2.3 Running the script in Arch Linux](#Running_the_script_in_Arch_Linux)
    *   [2.3 Flashing with ezScript](#Flashing_with_ezScript)
    *   [2.4 Manually with flashrom](#Manually_with_flashrom)
        *   [2.4.1 Get flashrom for Arch Linux](#Get_flashrom_for_Arch_Linux)
        *   [2.4.2 Get flashrom for Chrome OS](#Get_flashrom_for_Chrome_OS)
        *   [2.4.3 Basic use of flashrom](#Basic_use_of_flashrom)
*   [3 Flashing back stock firmware](#Flashing_back_stock_firmware)
*   [4 Unbricking your Chrome OS device](#Unbricking_your_Chrome_OS_device)
    *   [4.1 Required tools](#Required_tools)
    *   [4.2 General idea on the unbricking process](#General_idea_on_the_unbricking_process)
    *   [4.3 Recommended reading about unbricking](#Recommended_reading_about_unbricking)
*   [5 Firmware write protection](#Firmware_write_protection)
    *   [5.1 Hardware write protection](#Hardware_write_protection)
    *   [5.2 Software write protection](#Software_write_protection)
    *   [5.3 Understanding the Process of Disabling the Write Protection](#Understanding_the_Process_of_Disabling_the_Write_Protection)
        *   [5.3.1 Disabling the hardware write protection](#Disabling_the_hardware_write_protection)
        *   [5.3.2 Disabling the software write protection](#Disabling_the_software_write_protection)

## Introduction

### Why flash a custom firmware?

#### Pros

*   Adds a much recent version of SeaBIOS
*   Adds SeaBIOS payload of coreboot to Chrome OS devices that did not shipped with SeaBIOS.
*   Reduce boot time.
*   Remove developer Mode screen.
*   Enables VMX.
*   Fixes some issues (like suspend) without further modifications.

#### Cons

*   Dangerous, might brick your device.
*   Cannot boot stock Chrome OS (you can install [Arnold the Bat’s Chromium OS build](http://arnoldthebat.co.uk/wordpress/chromium-os/) and it should be possible upgrade it to full blown Chrome OS with a script).
*   It is possible that some quirks will be added, [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1460520#p1460520).

## Flashing the custom firmware

There are several approaches for flashing a custom firmware:

*   Use John Lewis' script which will save you time finding the correct firmware.
*   Use Matt DeVillier's [ezScript](http://forum.kodi.tv/showthread.php?tid=194362) (currently supports only Chromeboxes).
*   Manually with `flashrom`, in this case you will need to obtain the firmware by yourself or to compile it from the Coreboot sources ([official](http://www.coreboot.org/Download_coreboot) or [Chromium OS fork](https://chromium.googlesource.com/chromiumos/third_party/coreboot/)).

**Note:** With Linux kernel versions greater than 4.4, CONFIG_IO_STRICT_DEVMEM a new kernel security measure can make flashrom stop working, in that case you can try adding "iomem=relaxed" to your kernel parameters. [[2]](https://www.flashrom.org/FAQ﻿).

### Disable the hardware write protection

See the [Disabling the hardware write protection](#Disabling_the_hardware_write_protection) at the [Firmware write protection](#Firmware_write_protection).

### Flashing with John Lewis' script

**Warning:** Do not run the script before disabling the hardware write protection.

#### Understanding the script

##### What John Lewis' `getnflash_johnlewis_rom.sh` script does ?

*   Automatically downloads Chromium OS 32bit version of `flashrom`.
*   Backup your current firmware.
*   Disables software write protection by running `# ./flashrom --wp-disable`.
*   Checks the Chromebook product name with [dmidecode](https://www.archlinux.org/packages/?name=dmidecode) and download the proper custom firmware.
*   Writes the custom firmware.

##### What the script does not do ?

*   Does not ask for confirmation.
*   Does not check if the hardware write protection is disabled.
*   Does not confirm the compatibility of a custom firmware to a specific Chromebook sub-model.

##### Conclusions

*   Make sure you disabled the hardware write protection.
*   Read the [FAQ](https://johnlewis.ie/custom-chromebook-firmware/faq/).
*   [Confirm that your Chromebook model is supported](https://johnlewis.ie/custom-chromebook-firmware/rom-download/), if your model is untested then visit the [coreboot on Chromebooks Google+ community](https://plus.google.com/communities/112479827373921524726) and ask for advice.

**Warning:** If you are flashing a custom firmware be prepared to the possibility that you might brick your device and make yourself familiar with the [unbricking methods](#Unbricking_Your_Chromebook).

#### Running the script in Chrome OS

*   Access your command prompt via VT-2\. `Ctrl + Alt + =>`
*   Enter the command shown on the [Download ROM page at John Lewis site](https://johnlewis.ie/custom-chromebook-firmware/rom-download/).

**Note:** The reason for not posting here is to force you to visit the site and read the page before proceeding.

*   After the script exited copy the backed up firmware to an external storage before rebooting the system.

You should now have a custom firmware installed on your device, cross your fingers and reboot.

If you flashed the firmware as part of the installation process then continue by following [Installing Arch Linux](#Installing_Arch_Linux), if the custom firmware boots the installation media correctly then you might want to enable back the hardware write protection.

#### Running the script in Arch Linux

*   In Arch Linux on 64bit environment you will need to enable the Multilib repository (if it is not already enabled) in pacman.conf and install [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc).

```
# pacman -S lib32-glibc

```

*   Install [dmidecode](https://www.archlinux.org/packages/?name=dmidecode).

```
# pacman -S dmidecode

```

*   Enter the command shown on the [Download ROM page at John Lewis site](https://johnlewis.ie/custom-chromebook-firmware/rom-download/).

**Note:** The reason for not posting here is to force you to visit the site and read the page before proceeding.

*   After the script exited copy the backed up firmware to an external storage before rebooting the system.

You should now have a custom firmware installed on your device, cross you fingers and reboot.

If the custom firmware boots Arch Linux correctly then you might want to enable back the hardware write protection, although [John Lewis states](https://blogs.fsfe.org/the_unconventional/2014/09/19/c720-coreboot/) that it's not necessary and will only make upgrading more difficult later. However, if you do not re-enable it you want to be careful not to use flashrom.

### Flashing with ezScript

Currently ezScript supports only Intel based Chromeboxes.

Before installing this custom firmware carefully read instructions at [ezScript official page](http://forum.kodi.tv/showthread.php?tid=194362). To install firmware only use install option #5 (`Install/update: custom coreboot Firmware`).

### Manually with flashrom

The use of the upstream [flashrom](https://www.archlinux.org/packages/?name=flashrom) package is discouraged as it's missing operations like `--wp-disable`, `--wp-status` and it will not write firmware successfully to the ROM of the Chromebook unless it already been programmed externally (i.e. flashing by another device over SPI with SOIC clip), this is why it's recommended to use Chromium OS's `flashrom`.

#### Get flashrom for Arch Linux

*   Download a 64-bit statically linked Chromium OS's `flashrom` version.

```
# wget --no-check-certificate [https://johnlewis.ie/flashrom](https://johnlewis.ie/flashrom)
# chmod +x flashrom

```

Do not forget that `flashrom`'s location is not in `$PATH`, to execute it you will need to precede the command with `./`, e.g. `# ./flashrom`.

#### Get flashrom for Chrome OS

Chrome OS already includes `flashrom`.

#### Basic use of flashrom

*   Disable software write protection before writing to the firmware chip.

```
# flashrom --wp-disable

```

*   Backup firmware from the firmware chip.

```
# flashrom -r old_firmware.bin

```

*   Write firmware to the firmware chip.

```
# flashrom -w new_firmware.bin

```

**Tip:** Find your firmware chip by running the command `flashrom -V|grep 'Found' |grep 'flash chip'`

## Flashing back stock firmware

**Note:** The following assumes that your device is not bricked, if it does bricked then jump to [Unbricking your Chrome OS device](#Unbricking_your_Chrome_OS_device)

[Disable the hardware write protection](#Disabling_the_hardware_write_protection) and follow the how to [manually flash firmware with `flashrom`](#Manually_with_flashrom) to flash the backup of your stock firmware.

## Unbricking your Chrome OS device

**Note:** This does not intended to be a thorough guide but just give you a basic understanding of the process of flashing a firmware to a bricked Chromebook. The ArchWiki is not the place for detailed hardware hacking guides so there is no sense in expanding this topic.

### Required tools

*   Programmer, both the [Raspberry Pi](http://flashrom.org/RaspberryPi) and the [Bus Pirate](http://flashrom.org/Bus_Pirate) are mentioned as compatible devices on the [flashrom wiki](http://flashrom.org/). The [Bus Pirate](http://flashrom.org/Bus_Pirate) is preferable as it will allow you to use Chromium OS's version of `flashrom` that supports `--wp-disable` and `--wp-status` flags.
*   SOIC clip is recommended, see [[3]](http://flashrom.org/ISP).
*   Female jumper wires.
*   If you want to use Chromium OS's `flashrom` another Linux machine (32bit or 64bit) is required.

### General idea on the unbricking process

*   Connect the jumper wires to the programmer and the SOIC clip.
*   Connect the SOIC clip to the ROM chip.
*   If your programmer is running Linux (Raspberry Pi) then modprobe the spi modules.
*   If your programmer is not running Linux then connect it to your Linux machine.
*   Write the firmware with `flashrom`, you might need to disable software write protection by running `flashrom` with the `--wp-disable` flag (this is why Chromium OS's `flashrom` is handy).

### Recommended reading about unbricking

*   Flashrom's wiki pages on [ISP](http://flashrom.org/ISP), [Bus Pirate](http://flashrom.org/Bus_Pirate), [Raspberry Pi](http://flashrom.org/RaspberryPi) and [SOIC8](http://flashrom.org/Technology#SO8.2FSOIC8:_Small-Outline_Integrated_Circuit.2C_8_pins).
*   [Coreboot's wiki page on Chromebooks](http://www.coreboot.org/Chromebooks).
*   Examples of unbricking the C720: [guide](http://www.tnhh.net/2014/08/25/unbricking-chromebook-with-beaglebone.html), [pictures](https://drive.google.com/folderview?id=0B9f62MH0umbmRTA2Xzd5WHhjWEU&usp=sharing).
*   Example of unbricking HP Chromebox: [guide](https://pomozok.wordpress.com/2015/01/10/chromebook-vivisection-readingwriting-rom-chip-data/)

## Firmware write protection

**Note:** The information on this topic only intended to give you the basic understanding on the write protection feature in your Chromebook. The ArchWiki is not the place for detailed hardware hacking guides so there is no sense in expanding this topic.

The firmware (Coreboot and its payloads) stored on a SPI chip (usually SOIC8) that some of its storage is protected from writing (mostly Coreboot).

As long as the write protection was not disabled or the protected range was not set to (0,0) any change made to the unprotected part of the firmware (mainly SeaBIOS) should be recoverable with Chrome OS recovery media.

There are two parts of the write protection: hardware and software.

### Hardware write protection

The hardware write protection is an electrical circuit that when it's closed or open it prevent writing to the software protection special registers, thus the hardware write protection only protect directly these special registers but indirectly also the data in the firmware chip.

To disable the hardware write protection you may need to remove a screw, press a switch or short a jumper.

### Software write protection

The software write protection are special registers which determining if the data stored in the firmware chip is protected and also holds the range of addresses of the protected data.

### Understanding the Process of Disabling the Write Protection

To disable the write protection one would need to:

*   Disable the hardware write protection of the special software register.
*   Change the value of the special software register to disable software write protection or change the range of the protected addresses so no data will be protected (start and end at 0).

Conclusion: If we will disable the software write protection and will not enable it back, then even if we will enable the hardware write protection the firmware chip will stay unprotected.

#### Disabling the hardware write protection

To find the location of the hardware write-protect screw/switch/jumper and how to disable it visit the ArchWiki page for your Chromebook model (see [Chromebook Models](/index.php/Chromebook#Chromebook_Models "Chromebook")). If there is no information about your device on the ArchWiki then turn to [Developer Information for Chrome OS Devices](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices) and [Coreboot's Chromebooks page](http://www.coreboot.org/Chromebooks).

#### Disabling the software write protection

Chromium OS's `flashrom` can manipulate the software write protection special registers.

*   Read the status of the software write protection special registers.

```
# flashrom --wp-status

```

*   Disable or enable the software write protection.

```
# flashrom --wp-disable

```

*   Change software write protection addresses range.

```
# flashrom --wp-range 0 0

```

For more details on Chromium OS's `flashrom` and how to obtain it, see [Manually Flash Custom Firmware with `flashrom`](#Manually_with_flashrom).