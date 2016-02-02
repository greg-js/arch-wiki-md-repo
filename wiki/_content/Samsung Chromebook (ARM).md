# Samsung Chromebook (ARM)

The Samsung Chromebook (model XE303C12) is a laptop intended work in the cloud. It provides a powerful Cortex-A15 Dual Core Exynos 5 processor at 1.7 GHz with Mali-T604 GPU, 2 GiB of DDR3, 16 GiB of internal flash storage, WiFi a/b/g/n, SD and USB ports, HDMI connector and a 11.6" display. It is visually like the MacBook Air 11\. With stock firmware it runs a heavily modified Gentoo-Linux, which means that nearly all the source code is [available](https://chromium.googlesource.com/chromiumos) from Google. **It is possible to install ArchLinux ARM (ALARM) on this device**.

More information at dedicated pages by [Google](http://www.google.com/intl/en/chrome/devices/samsung-chromebook.html#ss-cb) and [Samsung](http://www.samsung.com/us/computer/chrome-os-devices/XE303C12-A01US).

## Contents

*   [1 Article Preface](#Article_Preface)
*   [2 Installing Arch Linux ARM](#Installing_Arch_Linux_ARM)
*   [3 Stop Here If You're Not 100% Sure](#Stop_Here_If_You.27re_Not_100.25_Sure)
*   [4 Flashing non-verified U-boot](#Flashing_non-verified_U-boot)
    *   [4.1 Boot process](#Boot_process)
    *   [4.2 Removing RO protection](#Removing_RO_protection)
    *   [4.3 Precompiled U-Boot](#Precompiled_U-Boot)
    *   [4.4 How to compile U-Boot](#How_to_compile_U-Boot)
    *   [4.5 How to flash U-Boot](#How_to_flash_U-Boot)
        *   [4.5.1 Required Equipment](#Required_Equipment)
        *   [4.5.2 Steps](#Steps)
*   [5 Booting from SD](#Booting_from_SD)
*   [6 Related Links](#Related_Links)

## Article Preface

This article is not meant to be an exhaustive setup guide and assumes that the reader has setup an Arch system before. Arch newbies are encouraged to read the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") if unsure how to preform standard tasks such as creating users, managing the system, etc.

**Note:** Support for the ARM architecture is provided on [http://archlinuxarm.org](http://archlinuxarm.org) not through posts to the official Arch Linux Forum. Any posts related to ARM specific issues will be promptly closed per the [Arch Linux Distrubution Support ONLY](/index.php/Forum_etiquette#Arch_Linux_distribution_support_ONLY "Forum etiquette") policy.

## Installing Arch Linux ARM

See the instructions at the [archlinuxarm site](http://archlinuxarm.org/platforms/armv7/samsung-chromebook#qt-platform_tabs-ui-tabs2). This is a fully supported platform at Arch Linux ARM (wholly separate entity)

You can install to:

*   SD Card
*   USB 2.0 Flash stick
*   eMMC (after installing one of the prior)

To install to SD or USB, follow the instructions linked above. To install to eMMC, install to one of the prior medias, then install to /dev/mmcblk0, a simple edit from the install instructions from SD. You must boot onto a different media prior to this however.

## Stop Here If You're Not 100% Sure

**Installation to the eMMC can be removed via the USB Restore method that is a part of all Chromebook devices, when installing with official method.**

**Flashing of non-verified uboot is _not required_ for eMMC install.**

## Flashing non-verified U-boot

**Warning:** This process is very dangerous and shall not be carried out unless all the risks are known and understood. You are the only responsible of any damage which may occur

**Warning:** Arch Linux ARM will not support you if you do this and screw it up.

### Boot process

The boot process of this Chromebook has several stages. The very first stages are burnt into the SoC (probably read-only although unconfirmed). Then, the SoC jumps to the starting of the 4 MiB SPI flash, which contains basically U-Boot.

This flash is split into a read-only half (first half) and read-write half. The read-only (RO) is loaded at the factory and contains several signature verifications (it is really a known-to-be-good U-Boot). The read-write (RW) is a signed U-Boot which also loads signed kernel and so on.

As you probably know (that is why you are reading this) you can load non-signed kernels by entering developer mode. But it has two drawbacks: you have to make a non-trivial process to install your bootloader and you have to hit Ctrl+D or Ctrl+U on every boot.

### Removing RO protection

The good news is that you can disable the RO protection. The bad news is that you have to open your device. The recommended guide to open your Chromebook is the one at [iFixit](http://www.ifixit.com/Teardown/Samsung+Chromebook+11.6+Teardown/12225/1); stop at step 4, then jump to [step 9](http://www.ifixit.com/Teardown/Samsung+Chromebook+11.6+Teardown/12225/2#s45950). If you have a multimeter, ensure that after removal of the metallic sticker both parts of the ring are **not** in short-circuit.

Now you can write your U-Boot.

### Precompiled U-Boot

Source: [nv_image-snow.bin.gz](https://www.dropbox.com/s/6pzvraf3ko14sz9/nv_image-snow.bin.gz)

### How to compile U-Boot

WIP

### How to flash U-Boot

#### Required Equipment

*   1 X Samsung ARM Chromebook

*   1 X SD card 4 -> 16 GB

*   2 X USB 2 thumb drive 4 -> 16 GB

We will call these USB drives MAIN and TAR. The reason we have the TAR USB is so we can tar up the root filesystem on MAIN without it actively being mounted as the current root file system.

Notes:

You may have difficulty booting USB/SD-Cards > 16 GB.

You can only boot from the USB 2 port NOT the USB 3 port.

#### Steps

<u>PREPARATION</u>

*   Follow the [ifixit instructions](http://www.ifixit.com/Teardown/Samsung+Chromebook+11.6+Teardown/12225), to ensure the metallic ring-shaped sticker is removed.

*   On both the USB thumb drives, MAIN and TAR, install and boot Arch using the [already established method](http://archlinuxarm.org/platforms/armv7/samsung/samsung-chromebook#qt-platform_tabs-ui-tabs2).

**Note:** You can copy from chrome OS web page with Ctrl-C and then paste into the Chrome OS shell with Ctrl-Shift-V. (This will save you time!!!)

*   Update your install with:

```
# pacman -Syu

```

*   On only the 'MAIN' USB install these required packages.

```
# pacman -S flashroom-google linux-chromebook gptfdisk wget libftdi-compat

```

*   download this file:

```
# wget [http://goo.gl/RZ7THP](http://goo.gl/RZ7THP)

```

This is a shortened URL for:

[https://www.dropbox.com/s/6pzvraf3ko14sz9/nv_image-snow.bin.gz](https://www.dropbox.com/s/6pzvraf3ko14sz9/nv_image-snow.bin.gz)

*   rename it:

```
# mv RZ7THP nv_image-snow.bin.gz

```

*   uncompress it:

```
# gunzip nv_image-snow.bin.gz

```

*   read and save off your original image:

```
# flashrom.google -p linux_spi:dev=/dev/spidev1.0 -r origial_image-snow.bin

```

<u>MAKE SD CARD</u>

*   Insert your SD card, and check which device it is:

```
# lsblk

```

*   _Mine is mmcblk1_, now zero/clean it out:

```
# sgdisk -Z /dev/mmcblk1

```

*   Confirm no partitions:

```
# lsblk

```

*   Create two partitions, the first 16M, the other the rest of the size:

```
# sgdisk -n 1:0:+16m /dev/mmcblk1

```

```
# sgdisk -n 2:0 /dev/mmcblk1

```

*   Make the filesystems:

```
# mkfs.ext2 /dev/mmcblk1p1

```

```
# mkfs.jfs /dev/mmcblk1p2

```

*   Copy vmlinux.uimg

```
# cd /tmp; mkdir mnt
# mount /dev/mmcblk1p1 mnt
# cp /boot/vmlinux.uimg mnt
# umount mnt

```

*   Shutdown your system and boot up with your 'TAR' USB drive.

*   After booted, plug in your first 'MAIN' USB and follow the below procedure to tar your rootfs system:

```
# mkdir tar-root
# mount /dev/sdb3 tar-root

```

*   Mount the SD card too:

```
# mkdir sd-card
# mount /dev/mmcblk1p2 sd-card

```

*   Create an excludes file: (after entering 'dev' hit Ctrl-d to end 'cat' command)

```
# cd tar-root
# cat > excludes-file
opt/backup/arch-full*
tmp/*
var/cache/pacman/pkg/
proc
sys
dev

```

*   tar up the MAIN USB root filesystem

```
# tar cpfz ../root.tgz -X excludes-file .

```

*   untar to SD card:

```
# cd ..
# tar xfz root.tgz -C sd-card

```

The above will take a long time so go have a beer/coffee/milk.

*   unmount the partitions:

```
# umount sd-card
# umount tar-root

```

*   Make sure you copy the modules and firmware from linux-chromebook in the proper place on the rootfs.

**not sure how to do this**

**DO NOT FOLLOW DIRECTIONS BELOW, THEY ARE NOT COMPLETE**

*   go back to where your `nv_image-show.bin` was and flash the new image:

```
# flashrom.google -p linux_spi:dev=/dev/spidev1.0 -w nv_image-snow.bin

```

*   Powercycle. Hold down `a` while powering up to get into a u-boot prompt.

Once you are flashed with u-boot, you will need to create a SD card that boots.

*   From the u-boot prompt, enter the following to boot from SD card:

```
# setenv bootargs root=/dev/mmcblk1p2 rootfstype=jfs rootwait rw
# mmc dev 1
# ext2load mmc 1:1 42000000 vmlinux.uimg
# bootm 42000000

```

You should now be booted into your SD card.

<u>Write to eMMC</u>

After you are booted into your SD card from the above steps you will want to repeat the steps so you can boot from your eMMC, and not need an SD or USB hanging out from your computer.

Keep in mind the steps you did above to device: `mmcblk1`, aka, your SD card. You will want to change the device to: `mmcblk0`, aka, your eMMC.

In quick summary do:

*   zero out the device
*   create the two partitions
*   format the two partitions
*   setup the boot partition
*   setup the root partition
*   reboot into the u-boot prompt

```
# setenv arch_boot 'setenv bootargs root=/dev/mmcblk0p2 rootfstype=jfs rootwait ro; mmc dev 0; ext2load mmc 0:1 42000000 vmlinux.uimg; bootm 42000000'
# setenv bootcmd 'run arch_boot'
# saveenv

```

This should now boot into your eMMC, and also on every future reboot.

<u>To be able to fix the random power-on issue of the chromebook you have to change a bit the enviroment variables shown before.</u>

```
# setenv 1 'setenv bootargs root=/dev/mmcblk0p2 rootfstype=jfs rootwait ro; mmc dev 0; ext2load mmc 0:1 42000000 vmlinux.uimg; bootm 42000000'
# setenv bootcmd 'if sleep 5; then vboot_test poweroff; fi'
# saveenv

```

Now the Chromebook should power-off after 5 secs of power-on. To successfully boot your Chromebook you should press `Ctrl + c`, and then type `run 1`.

## Booting from SD

If you ever screw things up by burning a wrong bootloader, there is a recovery mechanism. The SoC built-in bootloader (known as BL0 and BL1) can be configured to boot from SPI, USB, SD and probably other options. This is known because of the Arndale development board (and previous Exynos models behave the same as well).

This is configured at the factory to boot from SPI, but this is done with a bunch of resistors located at the bottom of the PCB (link to image). User (name) experimented and got the working configuration (link to image).

**Warning:** If you are unsure about how to short-circuit pads, you should definitely go away and experiment a bit with other electronics. A wrong short-circuit may permanently damage your board.

By short-circuiting the pads as per the diagram linked, your SoC will boot from SD. You have to (confirm this and complete the information) load a U-Boot with BL2 incorporated.

## Related Links

*   [http://archlinuxarm.org/platforms/armv7/samsung/samsung-chromebook](http://archlinuxarm.org/platforms/armv7/samsung/samsung-chromebook)
*   [http://archlinuxarm.org/forum/viewtopic.php?t=4016](http://archlinuxarm.org/forum/viewtopic.php?t=4016)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Samsung_Chromebook_(ARM)&oldid=400993](https://wiki.archlinux.org/index.php?title=Samsung_Chromebook_(ARM)&oldid=400993)"