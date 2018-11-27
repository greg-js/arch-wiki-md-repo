NanoPi NEO Plus2 is a minimalist computer built for the [ARMv8-A architecture](https://en.wikipedia.org/wiki/ARMv8-A "wikipedia:ARMv8-A"). [More information about this project](http://wiki.friendlyarm.com/wiki/index.php/NanoPi_NEO_Plus2).

**Note:** The device is not officially supported by the ALARM project, i.e. please refrain from submitting patches, feature requests or bug reports for it.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Boot order](#Boot_order)
    *   [1.2 Using stock kernel](#Using_stock_kernel)
    *   [1.3 Compiling custom kernel](#Compiling_custom_kernel)
    *   [1.4 Fixing WIFI support](#Fixing_WIFI_support)

## Installation

### Boot order

The NanoPi will try to boot from SD-card and, if not available, it will boot from eMMC. Booting from SD-card is usefull to recover the device.

### Using stock kernel

A simple way to boot archlinux in the NanoPi is to first install the official image by following the instruction at [http://wiki.friendlyarm.com/wiki/index.php/NanoPi_NEO_Plus2#Install_OS](http://wiki.friendlyarm.com/wiki/index.php/NanoPi_NEO_Plus2#Install_OS) and then reuse existing kernel image, modules, and uboot to boot archlinux. After installing the stock image, archlinux can be installed as follows.

Insert the SD-card with stock image into a linux pc. The following instructions suppose that it's root fs is located at /dev/sdc2, whereas the uboot partition is localted at /dev/sdc1.

Backup the original modules:

```
 # mount /dev/sdc2 /mnt
 # bsdtar -czf orig_modules.tar.gz -C /mnt /lib/modules /lib/modprobe.d

```

Also backup some firmware modules, they will be needed to fix WIFI support.

```
 # bsdtar -czf orig_firmware.tar.gz -C /lib/firmware brcm ap6212

```

Download the generic archlinux armv8 image from [https://archlinuxarm.org/platforms/armv8/generic](https://archlinuxarm.org/platforms/armv8/generic) . Then unpack it:

```
 # umount /dev/sdc2
 # mkfs.ext4 /dev/sdc2 # add -f to force overwrite of existing fs
 # mount /dev/sdc2 /mnt
 # bsdtar -xpf ArchLinuxARM-aarch64-latest.tar.gz -C /mnt

```

Unpack the original modules

```
 # rm -rf /mnt/lib/modules /mnt/lib/modprobe.d
 # bsdtar -xpf orig_modules.tar.gz -C /mnt

```

Clean the boot partition:

```
 # rm -rf /mnt/boot/*

```

Populate the fstab:

 `/mnt/etc/fstab` 
```
# <file system> <dir> <type> <options> <dump> <pass>
/dev/mmcblk0p2       /               ext4            rw,relatime,data=ordered,noatime   0 1
tmpfs   /tmp         tmpfs   nodev,nosuid            0  0
/dev/mmcblk0p1       /boot           vfat            rw,defaults 0 1

```

Insert the SD-card into the NanoPi and it should now boot the stock linux kernel with archlinux.

### Compiling custom kernel

Full instructions for cross compilation are available at [http://wiki.friendlyarm.com/wiki/index.php/Building_U-boot_and_Linux_for_H5/H3/H2%2B#How_to_Compile_Mainline_BSP_for_H5](http://wiki.friendlyarm.com/wiki/index.php/Building_U-boot_and_Linux_for_H5/H3/H2%2B#How_to_Compile_Mainline_BSP_for_H5) .

Another option is to compile the kernel on the NanoPi itself:

```
 $ git clone [https://github.com/friendlyarm/linux.git](https://github.com/friendlyarm/linux.git) -b sunxi-4.x.y --depth 1
 $ cd linux
 $ touch .scmversion
 $ make sunxi_arm64_defconfig ARCH=arm64
 $ make -j4 Image dtbs ARCH=arm64

```

Then install the new kernel manually:

```
 # cp arch/arm64/boot/Image /boot/Image
 # cp arch/arm64/boot/dts/allwinner/sun50i-h5-nanopi*.dtb /boot/
 # make modules_install INSTALL_MOD_PATH=/

```

### Fixing WIFI support

When the wifi interface disappears, the following messages are printed in dmesg:

 `dmesg` 
```
[   12.020670] brcmfmac: brcmf_fw_map_chip_to_name: using brcm/brcmfmac43430a1-sdio.bin for chip 0x00a9a6(43430) rev 0x000001
[   12.039285] brcmfmac mmc2:0001:1: Direct firmware load for brcm/brcmfmac43430a1-sdio.bin failed with error -2
[   13.081285] brcmfmac: brcmf_sdio_htclk: HT Avail timeout (1000000): clkctl 0x50
[   13.081285] brcmfmac: brcmf_sdio_htclk: HT Avail timeout (1000000): clkctl 0x50

```

In order to fix this, the stock wifi firmware must be used.

Upload the firmware modules to the NanoPi:

```
 $ scp orig_firmware.tar.gz alarm@nanopi_ip:

```

On NanoPi, unpack them:

```
 # bsdtar -xpf orig_firmware.tar.gz -C /lib/firmware

```

After reboot, the wifi interface should appear and work again.