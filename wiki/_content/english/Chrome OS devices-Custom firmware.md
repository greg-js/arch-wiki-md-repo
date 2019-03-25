Related articles

*   [Chromebook](/index.php/Chromebook "Chromebook")
*   [Chromebook Pixel 2](/index.php/Chromebook_Pixel_2 "Chromebook Pixel 2")

**Warning:** This article relies on third-party scripts and modifications, and may irreparably damage your hardware or data. Proceed at your own risk.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Why flash a custom firmware?](#Why_flash_a_custom_firmware?)
    *   [1.1 Pros](#Pros)
    *   [1.2 Cons](#Cons)
*   [2 Flashing the custom firmware](#Flashing_the_custom_firmware)
    *   [2.1 Disable the hardware write protection](#Disable_the_hardware_write_protection)
    *   [2.2 Flashing with MrChromebox's Firmware Utility Script](#Flashing_with_MrChromebox's_Firmware_Utility_Script)
        *   [2.2.1 Introduction to the firmware](#Introduction_to_the_firmware)
        *   [2.2.2 Understanding the script](#Understanding_the_script)
            *   [2.2.2.1 What MrChromebox's Firmware Utility Script script does ?](#What_MrChromebox's_Firmware_Utility_Script_script_does_?)
            *   [2.2.2.2 What the script does not do ?](#What_the_script_does_not_do_?)
        *   [2.2.3 Flashing the firmware](#Flashing_the_firmware)
        *   [2.2.4 Using the script from Arch Linux](#Using_the_script_from_Arch_Linux)
    *   [2.3 Flashing with John Lewis' script](#Flashing_with_John_Lewis'_script)
        *   [2.3.1 Understanding the script](#Understanding_the_script_2)
            *   [2.3.1.1 What John Lewis' flash_chromebook_rom.sh script does ?](#What_John_Lewis'_flash_chromebook_rom.sh_script_does_?)
            *   [2.3.1.2 What the script does not do ?](#What_the_script_does_not_do_?_2)
            *   [2.3.1.3 Conclusions](#Conclusions)
        *   [2.3.2 Running the script in Chrome OS](#Running_the_script_in_Chrome_OS)
        *   [2.3.3 Running the script in Arch Linux](#Running_the_script_in_Arch_Linux)
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

## Why flash a custom firmware?

### Pros

*   Allows the use of a [UEFI](/index.php/UEFI "UEFI") coreboot payload (with MrChromebox's custom firmware).
*   May reduce boot time.
*   Removes the Developer Mode screen that some users find annoying.
*   Enables VMX in models in which it is not active by default.
*   Fixes some issues (like suspend).

### Cons

*   Dangerous, and has the potential to render a device unusable.
*   Cannot boot stock Chrome OS (you can install [Arnold the Bat’s Chromium OS build](https://arnoldthebat.co.uk/wordpress/chromium-os/) and it should be possible to upgrade it to full blown Chrome OS with a script if the user desires).
*   Custom-BIOS specific bugs may occur.

## Flashing the custom firmware

There are several approaches for flashing a custom firmware:

*   Use MrChromebox's [Firmware Utility Script](https://mrchromebox.tech/#fwscript).
*   Use John Lewis' script.
*   Manually with `flashrom`, in this case you will need to obtain the firmware by yourself or to compile it from the coreboot sources ([official](http://www.coreboot.org/Download_coreboot) or [Chromium OS fork](https://chromium.googlesource.com/chromiumos/third_party/coreboot/)).

**Note:** With Linux kernel versions greater than 4.4, CONFIG_IO_STRICT_DEVMEM a new kernel security measure can make flashrom stop working, in that case you can try adding "iomem=relaxed" to your kernel parameters. [[1]](https://www.flashrom.org/FAQ#What_can_I_do_about_.2Fdev.2Fmem_errors.3F﻿).

### Disable the hardware write protection

See the [Disabling the hardware write protection](#Disabling_the_hardware_write_protection) at the [Firmware write protection](#Firmware_write_protection).

### Flashing with MrChromebox's Firmware Utility Script

#### Introduction to the firmware

MrChromebox's firmware for Chromebooks and Chromeboxes has some differences compared to other third-party custom firmware, namely:

*   A [UEFI](/index.php/UEFI "UEFI") implementation via the Tianocore coreboot payload.

*   Updates for the Embedded Controller (EC) of some of the devices it supports, solving some bugs associated with other custom firmware.

*   Built based on the latest coreboot upstream, rather than on the frozen source snapshot provided by Google.

*   Source code and build scripts available on [github](https://github.com/MrChromebox)

The current major limitation of this firmware is the lack of proper UEFI NVRAM support, resulting in the impossibility of modifying [UEFI Variables](/index.php/Unified_Extensible_Firmware_Interface#UEFI_variables "Unified Extensible Firmware Interface"). This means that it defaults to booting from external devices if a valid EFI partition with a boot EFI program at the default path is detected, and that it defaults to booting from `*esp*/EFI/Boot/BOOTX64.EFI` (`*esp*` being the [EFI system partition](/index.php/EFI_system_partition "EFI system partition")) with no option of changing this behaviour.

#### Understanding the script

##### What MrChromebox's Firmware Utility Script script does ?

*   Automatically downloads statically compiled 64-bit versions of chromium `flashrom`, `cbfstool`, and `gbb_utility`.
*   Automatically detects your device/board name, current firmware, and hardware write-protect state
*   Provides the option to backup your current firmware on USB (when flashing full/custom UEFI firmware).
*   Automatically disables, clears, sets, and enables the software write protection as needed.
*   Provides choice between RW_LEGACY, BOOT_STUB, and UEFI Full ROM firmware (types available vary based on device).
*   Provides the ability to set the stock firmware's GBB flags outside of ChromeOS
*   Provides the ability to remove the white Developer Mode splash screen (select models only)
*   Writes and verifies the custom firmware.

##### What the script does not do ?

*   Does not make you a sandwich.

**Warning:** If you are flashing a custom firmware be prepared to the possibility that you might brick your device and make yourself familiar with the [unbricking methods](#Unbricking_your_Chrome_OS_device).

#### Flashing the firmware

Ensure that your device is supported by looking at the [supported device list](https://mrchromebox.tech/#devices). For some devices there is a legacy SeaBIOS (non-UEFI) firmware also available, although those are [deprecated](https://github.com/MrChromebox/firmware/issues/46) and will generally not receive further updates. Legacy firmware images also do not provide Embedded Controller updates.

If a UEFI ROM for your device is available, you can flash the Full ROM firmware using the [Firmware Utility Script](https://mrchromebox.tech/#fwscript) (after ensuring that you have removed your device's firmware write-protection screw). After successfully flashing the firmware, you can follow the [Installation guide](/index.php/Installation_guide "Installation guide") and install Arch Linux just like on any UEFI computer. [Systemd-boot](/index.php/Systemd-boot "Systemd-boot") is the recommended bootloader since it installs itself by default in `*esp*/EFI/Boot/BOOTX64.EFI`, the path that this firmware tries to boot from by default.

#### Using the script from Arch Linux

You will need to install [dmidecode](https://www.archlinux.org/packages/?name=dmidecode). Furthermore, to ensure that `flashrom` can correctly flash the firmware it is necessary to boot with both the `nopat` and the `iomem=relaxed` [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). This is due to an [issue](https://www.flashrom.org/FAQ#What_can_I_do_about_.2Fdev.2Fmem_errors.3F) with the chromium build of `flashrom` used by the script, which is required since upstream `flashrom` can't be used to set/clear the software write-protect state or range.

### Flashing with John Lewis' script

**Warning:** Do not run the script before disabling the hardware write protection.

#### Understanding the script

##### What John Lewis' `flash_chromebook_rom.sh` script does ?

*   Automatically downloads Chromium OS 64bit version of `flashrom`.
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

**Note:** John Lewis shut down his Google+ community in December 2017; his firmware is presumed to now be unsupported.

**Warning:** If you are flashing a custom firmware be prepared to the possibility that you might brick your device and make yourself familiar with the [unbricking methods](#Unbricking_your_Chrome_OS_device).

#### Running the script in Chrome OS

*   Access your command prompt via VT-2\. `Ctrl + Alt + =>`
*   Enter the command shown on the [Download ROM page at John Lewis site](https://johnlewis.ie/custom-chromebook-firmware/rom-download/).

**Note:** The reason for not posting here is to force you to visit the site and read the page before proceeding.

*   After the script exited copy the backed up firmware to an external storage before rebooting the system.

You should now have a custom firmware installed on your device, cross your fingers and reboot.

If you flashed the firmware as part of the installation process then continue by following [Installing Arch Linux](/index.php/Chrome_OS_devices#Installing_Arch_Linux "Chrome OS devices"), if the custom firmware boots the installation media correctly then you might want to enable back the hardware write protection.

#### Running the script in Arch Linux

*   Install [dmidecode](https://www.archlinux.org/packages/?name=dmidecode).

*   Enter the command shown on the [Download ROM page at John Lewis site](https://johnlewis.ie/custom-chromebook-firmware/rom-download/).

**Note:** The reason for not posting here is to force you to visit the site and read the page before proceeding.

*   After the script exited copy the backed up firmware to an external storage before rebooting the system.

You should now have a custom firmware installed on your device, cross you fingers and reboot.

If the custom firmware boots Arch Linux correctly then you might want to enable back the hardware write protection, although [John Lewis states](https://blogs.fsfe.org/the_unconventional/2014/09/19/c720-coreboot/) that it's not necessary and will only make upgrading more difficult later. However, if you do not re-enable it you want to be careful not to use flashrom.

### Manually with flashrom

The use of the upstream [flashrom](https://www.archlinux.org/packages/?name=flashrom) package is discouraged as it's missing operations like `--wp-disable`, `--wp-status` and it will not write firmware successfully to the ROM of the Chromebook unless it already been programmed externally (i.e. flashing by another device over SPI with SOIC clip), this is why it's recommended to use Chromium OS's `flashrom`.

#### Get flashrom for Arch Linux

*   Download a 64-bit statically linked Chromium OS's `flashrom` version.

```
# wget [https://johnlewis.ie/flashrom](https://johnlewis.ie/flashrom)
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
*   SOIC clip is recommended, see [[2]](http://flashrom.org/ISP).
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
*   [coreboot's wiki page on Chromebooks](http://www.coreboot.org/Chromebooks).
*   Examples of unbricking the C720: [guide](http://www.tnhh.net/2014/08/25/unbricking-chromebook-with-beaglebone.html), [pictures](https://drive.google.com/folderview?id=0B9f62MH0umbmRTA2Xzd5WHhjWEU&usp=sharing).
*   Example of unbricking HP Chromebox: [guide](https://pomozok.wordpress.com/2015/01/10/chromebook-vivisection-readingwriting-rom-chip-data/)

## Firmware write protection

**Note:** The information on this topic only intended to give you the basic understanding on the write protection feature in your Chromebook. The ArchWiki is not the place for detailed hardware hacking guides so there is no sense in expanding this topic.

The firmware (coreboot and its payloads) is stored on a SPI flash chip (usually SOIC8), portions of which are protected from writing by a combination of hardware and software measures.

As long as the write protection has not been disabled and the protected range not cleared (set to 0,0), any changes made to the unprotected (RW) parts of the firmware (mainly SeaBIOS) can be reverted via either a booted Chrome OS install or Chrome OS recovery media.

There are two parts to the firmware write protection: hardware and software.

### Hardware write protection

The hardware write protection is an electrical circuit which prevents writing to the software protection special registers; it's normally enforced by the grounding of the !WP pin on the SOIC8 chip. Thus the hardware write protection only protects directly these special registers, but indirectly also the data in the firmware chip.

Early Chromebook models (2012-2013) used a jumper or switch to implement hardware write protection. Most models from 2014-2017 used a screw, and Kabylake/Apollolake (and newer) models from 2017 on use the battery sense line (so disconnecting the battery is necessary to disable the hardware write protect).

### Software write protection

The software write protection is implemented via a special register on the firmware chip, which contain an enabled/disabled flag, as well as one or more ranges of addresses to be protected / marked as read-only.

### Understanding the Process of Disabling the Write Protection

To fully disable the write protection one would need to:

*   Disable the hardware write protection of the special software register.
*   Change the value of the special software register to disable software write protection, and clear the range of the protected addresses so no data will be protected (start and end at 0).

Conclusion: If one disables the software write protection and does not enable it back, then even if the hardware write protection is re-enabled, the firmware chip will remain unprotected.

#### Disabling the hardware write protection

To find the location of the hardware write-protect screw/switch/jumper and how to disable it visit the ArchWiki page for your Chromebook model (see [Chromebook Models](/index.php/Chromebook#Chromebook_Models "Chromebook")). If there is no information about your device on the ArchWiki then turn to [Developer Information for Chrome OS Devices](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices) and [coreboot's Chromebooks page](http://www.coreboot.org/Chromebooks).

#### Disabling the software write protection

**Note:** If using MrChromebox's Firmware Utility Script to flash the firmware or set the GBB flags on your device, it is not necessary (nor recommended) to manually disable the software write protection. The Firmware Utility Script will automatically disable/clear/set/enable the software write protection as required.

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