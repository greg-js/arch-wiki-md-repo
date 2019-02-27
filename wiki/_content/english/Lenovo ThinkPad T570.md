Related articles

*   [Laptop](/index.php/Laptop "Laptop")
*   [Laptop/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 BIOS Update](#BIOS_Update)
        *   [2.1.1 Healing a corrupted BIOS](#Healing_a_corrupted_BIOS)
    *   [2.2 Bumblebee](#Bumblebee)
    *   [2.3 Bluetooth](#Bluetooth)

## Installation

Use the [Installation guide](/index.php/Installation_guide "Installation guide"). Make sure that Secure Boot is disable in BIOS Setup.

## Configuration

### BIOS Update

Install [this BIOS update](https://support.lenovo.com/de/en/downloads/ds120370) (or a newer one) to fix a [serious bug concerning hyperthreading](https://lists.debian.org/debian-devel/2017/06/msg00308.html) and issues with thunderbolt [[1]](https://forums.lenovo.com/t5/ThinkPad-T400-T500-and-newer-T/ThinkPad-T470s-BIOS-bug-WOL-and-Thunderbolt-3/m-p/3707059) [[2]](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1708043/) , which can affect you even if you don't use thunderbolt. [[3]](https://github.com/linrunner/TLP/issues/308) See [Flashing BIOS from Linux](/index.php/Flashing_BIOS_from_Linux "Flashing BIOS from Linux") for details on how to install the BIOS without an optical drive; the [geteltorito](https://aur.archlinux.org/packages/geteltorito/) method is known to work on the T570.

Note: before flashing, you have to disable the Intel BIOS guard or risk bricking your laptop. In the BIOS, set **Security - Intel (R) SGX - Intel (R) SGX Control** to Disabled. Do the same for **Device guard**, if needed. If you corrupt your BIOS, you can fix it by flashing a working ROM directly into the EEPROM chip either with [a Raspberry Pi](http://posts.nadim.computer/2018/10/26/repairing-a-thinkpad.html) or [a specialized programming device](https://www.flashrom.org/Flashrom/1.0/Supported_Hardware#USB_Devices).

#### Healing a corrupted BIOS

If you got bitten by the [Intel BIOS (Boot) Guard](https://github.com/corna/me_cleaner/wiki/Intel-Boot-Guard), you can follow these instructions to reverse the damage.

1.  Open the bottom cover ([see video](https://www.youtube.com/watch?v=46NP0-b_XlM))
2.  Locate the chip containing the BIOS. It is under a black sticker ([see photo](https://i.imgur.com/qWk0ZHH.jpg)). The model of the chip is MXIC MX25L12873F M2I-10G ([see datasheet](http://www.macronix.com/Lists/Datasheet/Attachments/7396/MX25L12873F,%203V,%20128Mb,%20v1.2.pdf)).
3.  Connect your programming device to the chip using a SOIC8 clip. You should probably support the clip and its cable somehow, so it remains completely still.
4.  Read the old BIOS image from the chip using [Flashrom](https://tomvanveen.eu/flashing-bios-chip-raspberry-pi/) or the software that came with your programming device
5.  Open the old BIOS image with [UEFITool](https://aur.archlinux.org/packages/uefitool-git)
6.  In UEFITool, do File - Search - String and systematically input BIOS IDs that are found in the VERSION INFORMATION section of the Lenovo BIOS readme file found on the Lenovo BIOS download page
7.  When you hit the corresponding ID, you will see something like this in the Message section of UEFITool: "Unicode text "N1VET31W" found in PE32 image section at offset 31B0h"
8.  Download the BIOS with the matching ID from Lenovo's site (it has to be the same, because Boot Guard is looking at the specific cryptographic signature)
9.  Install [geteltorito](https://aur.archlinux.org/packages/geteltorito/)
10.  Extract the boot image with a command like `geteltorito.pl -o n1vur04w.img n1vur04w.iso` 
11.  Create a loop device `sudo losetup -P /dev/loop0 n1vur04w.img` 
12.  Mount the partition found in the loop device `sudo mount /dev/loop0p1 /mnt` 
13.  In the mounted partition, navigate into the directory named something like Flash/N1VET31W/
14.  Copy the file with the extension FL1 into your project directory
15.  Unmount
    ```
    sudo umount /mnt
    sudo losetup -d /dev/loop0
    ```

16.  In your old corrupted BIOS, the section with the corruption is pinpointed by UEFITool with a message like "parseSection: GUID defined section can not be processed". Double-clicking the message will show you the volume it belongs to. In the **BIOS region**, you will replace the corrupted volume and all the preceding ones with healthy volumes extracted from the downloaded BIOS image. This type of minimal replacement is needed instead of replacing every volume, because UEFITool is not yet smart enough to preserve all the required Boot Guard data. UEFITool_NE (New Engine) is able to display the Boot Guard keys and signatures, but, as of the writing of this, is not yet able to do volume replacing. It is probably a good idea to use the [NE version](https://github.com/LongSoft/UEFITool/releases) to do the extraction.
17.  Open the FL1 file in UEFITool NE
18.  Do Right-click - Extract as is... or Ctrl-E for each of the needed volumes (save them with names that preserve the order they appear in)
19.  Open the corrupted BIOS in UEFITool (old engine version) and do Right-click - Replace as is... or Ctrl-R for the respective volumes
20.  File - Save image file... under some different name
21.  Flash the healed image back into the chip

If you find your bootloader is gone, install it using a live USB.

### Bumblebee

[Until bbswitch is updated to support the new power management method](/index.php/Bumblebee#Broken_power_management_with_kernel_4.8 "Bumblebee"), add `pcie_port_pm=off` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

### Bluetooth

If you have a very weak bluetooth signal when using wifi, make sure you have a recent [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware). See [https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1721271](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1721271) for more information.