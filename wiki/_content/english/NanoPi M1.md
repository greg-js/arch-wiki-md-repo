The NanoPi M1 is a small, arm-based computer. It contains an Allwinner H3 processor and either 512 or 1024 MB of RAM. This article is strongly based on Orange Pi.

## Contents

*   [1 Create the base system](#Create_the_base_system)
    *   [1.1 Create development environment](#Create_development_environment)
    *   [1.2 Partition, format and mount SD card](#Partition.2C_format_and_mount_SD_card)
    *   [1.3 Install ArchLinuxArm RootFS](#Install_ArchLinuxArm_RootFS)
    *   [1.4 Configure U-Boot](#Configure_U-Boot)
    *   [1.5 Unmount the SD Card](#Unmount_the_SD_Card)
    *   [1.6 Install U-Boot](#Install_U-Boot)
*   [2 Configure the base system](#Configure_the_base_system)
    *   [2.1 Boot the NanoPi](#Boot_the_NanoPi)
    *   [2.2 Configure Linux](#Configure_Linux)

## Create the base system

This NanoPi M1 boots from a single ext4 partition, imaged with Das U-Boot. An ArchLinuxArm RootFS can then be downloaded to the card.

### Create development environment

Create a directory system to store the development files:

```
$ mkdir nanopi_arch
$ cd nanopi_arch
$ mkdir mnt

```

### Partition, format and mount SD card

Use fdisk to partition the SD card, and use `mkfs.ext4 -O ^metadata_csum,^64bit /dev/sdX1` to format it. The mount the card with:

```
# mount /dev/sdX1 mnt

```

### Install ArchLinuxArm RootFS

Download the RootFS from ArchLinuxArm's website:

```
$ wget [http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz](http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz)

```

Extract the RootFS to the SD card:

```
# bsdtar -xpf ArchLinuxARM-armv7-latest.tar.gz -C mnt/
# sync

```

### Configure U-Boot

Create a file with the following boot script:

 `boot.cmd` 
```
part uuid ${devtype} ${devnum}:${bootpart} uuid
setenv bootargs console=${console} root=PARTUUID=${uuid} rw rootwait

if load ${devtype} ${devnum}:${bootpart} ${kernel_addr_r} /boot/zImage; then
  if load ${devtype} ${devnum}:${bootpart} ${fdt_addr_r} /boot/dtbs/${fdtfile}; then
    if load ${devtype} ${devnum}:${bootpart} ${ramdisk_addr_r} /boot/initramfs-linux.img; then
      bootz ${kernel_addr_r} ${ramdisk_addr_r}:${filesize} ${fdt_addr_r};
    else
      bootz ${kernel_addr_r} - ${fdt_addr_r};
    fi;
  fi;
fi

if load ${devtype} ${devnum}:${bootpart} 0x48000000 /boot/uImage; then
  if load ${devtype} ${devnum}:${bootpart} 0x43000000 /boot/script.bin; then
    setenv bootm_boot_mode sec;
    bootm 0x48000000;
  fi;
fi
```

Compile it and write it to the SD-card using the package [uboot-tools](https://www.archlinux.org/packages/?name=uboot-tools):

```
# mkimage -A arm -O linux -T script -C none -a 0 -e 0 -n "NanoPi M1 Boot Script" -d boot.cmd mnt/boot/boot.scr

```

### Unmount the SD Card

```
# umount mnt

```

### Install U-Boot

The upstream U-Boot repository has no graphics support as of May 2017. Clone U-Boot from the jernejsk git repository:

```
$ git clone --depth 1 [https://github.com/jernejsk/u-boot.git](https://github.com/jernejsk/u-boot.git)

```

There is a bug in the U-Boot code for Arch. Correct this with:

```
$ sed -i -e 's/\#\!\/usr\/bin\/env\ python/\#\!\/usr\/bin\/env\ python2/g' tools/binman/binman

```

The NanoPi shares many similarities with the OrangePi PC, so use this as the target until better support is available. Build U-Boot:

```
$ cd u-boot
$ make -j4 ARCH=arm CROSS_COMPILE=arm-none-eabi- orangepi_pc_defconfig
$ make -j4 ARCH=arm CROSS_COMPILE=arm-none-eabi-

```

This process should have generated an image called `u-boot-sunxi-with-spl.bin`. Write this to your SD card:

```
# dd if=u-boot-sunxi-with-spl.bin of=/dev/sdX bs=1024 seek=8
$ cd ..

```

## Configure the base system

### Boot the NanoPi

Apply 5V power to the NanoPi. It should boot successfully. If not, then attach the UART serial debugger as shown [here](http://linux-sunxi.org/FriendlyARM_NanoPi_M1#Locating_the_UART) and [here](/index.php/Working_with_the_serial_console "Working with the serial console").

Login over SSH with `alarm/alarm`.

Root password: `root`.

### Configure Linux

It is recommended that you install the base-devel group in order to continue. Do this and update the Linux system using:

```
# pacman -Syu base-devel

```