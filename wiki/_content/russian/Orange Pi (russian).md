Orange Pi (One) - это миниатюрный компьютер, созданный для [ARMv7-A архитектуры](https://en.wikipedia.org/wiki/ARMv7-A "wikipedia:ARMv7-A"). [Подробнее об этом проекте](http://www.orangepi.org/).

**Примечание:** Устройство официально не поддерживается проектом ALARM, то есть, пожалуйста, воздержитесь от отправки исправлений, запросов функций или отчетов об ошибках для него.

Эта статья основана на [Banana Pi](/index.php/Banana_Pi "Banana Pi"). Более того, эта статья не является исчерпывающим руководством по установке и предполагает, что читатель уже настраивал систему Arch ранее.

## Contents

*   [1 Установка](#Установка)
    *   [1.1 Использование оригинального архива ArchLinuxARM](#Использование_оригинального_архива_ArchLinuxARM)
        *   [1.1.1 Установить базовую систему на SD-карту](#Установить_базовую_систему_на_SD-карту)
        *   [1.1.2 Скомпилируйте и скопируйте загрузчик U-Boot](#Скомпилируйте_и_скопируйте_загрузчик_U-Boot)
        *   [1.1.3 Использование предварительно скомпилированных бинарных файлов U-Boot](#Использование_предварительно_скомпилированных_бинарных_файлов_U-Boot)
        *   [1.1.4 Логин / SSH](#Логин_/_SSH)
    *   [1.2 Дополнительный шаг, Wi-Fi Driver (RTL8189ES / ETV)](#Дополнительный_шаг,_Wi-Fi_Driver_(RTL8189ES_/_ETV))
*   [2 Orange Pi PC2](#Orange_Pi_PC2)
    *   [2.1 UBoot](#UBoot)
    *   [2.2 Kernel](#Kernel)
*   [3 Смотрите также](#Смотрите_также)

## Установка

### Использование оригинального архива ArchLinuxARM

Этот метод установит неизмененную базовую систему ArchLinuxARM armv7 на ваш Orange Pi One, что означает, что у вас будет запущено последнее ядро mainline. Вероятно, это также будет работать и для других H3 Orange Pi с поддержкой mainline.

#### Установить базовую систему на SD-карту

Запись нолей в начало SD-карты:

```
dd if=/dev/zero of=/dev/sdX bs=1M count=8

```

Используйте [fdisk](/index.php/Fdisk "Fdisk") для создания разделов на SD-карте и [форматирование](/index.php/%D0%A4%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D0%B5_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B "Файловые системы") с помощью `mkfs.ext4 -O ^metadata_csum,^64bit /dev/sdX1`.

Смонтируйте файловую систему ext4, заменив `sdX1` на отформатированный раздел:

```
# mkdir mnt
# mount /dev/*sdX1* /mnt

```

Загрузка и извлечение корневой файловой системы:

```
# wget [http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz](http://archlinuxarm.org/os/ArchLinuxARM-armv7-latest.tar.gz)
# bsdtar -xpf ArchLinuxARM-armv7-latest.tar.gz -C /mnt/

```

Создайте файл со следующим содержимым загрузочного скрипта:

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

Скомпилируйте его и запишите на SD-карту, используя пакет [uboot-tools](https://www.archlinux.org/packages/?name=uboot-tools)

```
# mkimage -A arm -O linux -T script -C none -a 0 -e 0 -n "Orange Pi One boot script" -d boot.cmd /mnt/boot/boot.scr
# umount /mnt

```

#### Скомпилируйте и скопируйте загрузчик U-Boot

Следующим шаг это создание образа загрузки. Убедитесь, что у вас [arm-none-eabi-gcc](https://www.archlinux.org/packages/?name=arm-none-eabi-gcc), [dtc](https://www.archlinux.org/packages/?name=dtc), [git](https://www.archlinux.org/packages/?name=git), [swig](https://www.archlinux.org/packages/?name=swig) и [uboot-tools](https://www.archlinux.org/packages/?name=uboot-tools) установлены в вашей системе. Если вы компилируете H3 Orange Pi, отличный от One, замените orangepi_one_config соответственно. Затем клонируйте исходный код u-boot и скомпилируйте образ Orange Pi:

```
$ git clone [git://git.denx.de/u-boot.git](git://git.denx.de/u-boot.git)
$ cd u-boot
$ git checkout tags/v2018.07
$ make -j4 ARCH=arm CROSS_COMPILE=arm-none-eabi- orangepi_one_defconfig
$ make -j4 ARCH=arm CROSS_COMPILE=arm-none-eabi-

```

Если все прошло нормально, у вас должен быть создан образ U-Boot: u-boot-sunxi-with-spl.bin. Теперь добавьте образ на вашу SD-карту, где /dev/sdX - ваша SD-карта.

```
# dd if=u-boot-sunxi-with-spl.bin of=/dev/sdX bs=1024 seek=8

```

#### Использование предварительно скомпилированных бинарных файлов U-Boot

Если вы не можете скомпилировать их на своем компьютере AMD64, просто возьмите их отсюда: [https://gitlab.com/vinibali/orangepi_uboot](https://gitlab.com/vinibali/orangepi_uboot)

Используйте ту же команду для размещения ее на SDCard:

```
# dd if=u-boot-sunxi-with-spl.bin of=/dev/sdX bs=1024 seek=8

```

#### Логин / SSH

Вход по SSH для пользователя root по умолчанию отключен. Войдите в систему с учетной записью пользователя по умолчанию и используйте [su](/index.php/Su "Su").

| Тип | Имя пользователя | Пароль |
| Root | `root` | `root` |
| User | `alarm` | `alarm` |

### Дополнительный шаг, Wi-Fi Driver (RTL8189ES / ETV)

Этот драйвер потребуется для Orange Pi Plus / Plus 2.

Сначала установите утилиты и заголовки ядра.

```
# sudo pacman -S base-devel git linux-armv7-headers

```

Затем соберите драйвер из исходников.

**Примечание:** Замените KSRC для вашей версии ядра.

```
# git clone [https://github.com/jwrdegoede/rtl8189ES_linux.git](https://github.com/jwrdegoede/rtl8189ES_linux.git)
# cd rtl8189ES_linux
# make -j4 ARCH=arm KSRC=/usr/lib/modules/4.18.11-1-ARCH/build/ 

```

И установить вручную.

**Примечание:** Замените каталог модулей на собственную версию ядра.

```
# cp 8189es.ko /usr/lib/modules/4.18.11-1-ARCH/kernel/drivers/net/wireless/realtek/
# depmod -a
# modprobe 8189es

```

## Orange Pi PC2

Allwinner H5 @ 1.20Ghz 64bit system AArch64

[Общая информация об устройстве](http://linux-sunxi.org/Xunlong_Orange_Pi_PC_2)

**Примечание:** Устройство также официально не поддерживается проектом ALARM

Следуйте общей инструкции по установке выше. Отличия:

### UBoot

```
# git clone [https://github.com/ARM-software/arm-trusted-firmware.git](https://github.com/ARM-software/arm-trusted-firmware.git)
# git clone [git://git.denx.de/u-boot.git](git://git.denx.de/u-boot.git)
# cd arm-trusted-firmware
# make CROSS_COMPILE=aarch64-linux-gnu- PLAT=sun50i_a64 DEBUG=1 -j4 bl31
# cp build/sun50i_a64/debug/bl31.bin ../u-boot/
# cd ../u-boot
# git checkout v2018.11
# make ARCH=arm CROSS_COMPILE=aarch64-linux-gnu- -j4 orangepi_pc2_defconfig
# make ARCH=arm CROSS_COMPILE=aarch64-linux-gnu- -j4
# dd if=u-boot-sunxi-with-spl.bin of=/dev/sdX bs=8k seek=1

```

### Kernel

Для AARCH64 вам понадобится еще один rootfs

```
# wget [http://archlinuxarm.org/os/ArchLinuxARM-aarch64-latest.tar.gz](http://archlinuxarm.org/os/ArchLinuxARM-aarch64-latest.tar.gz)
# bsdtar -xpf ArchLinuxARM-aarch64-latest.tar.gz -C mnt/

```

Вам нужно скомпилировать собственное ядро. Загрузите последний основной выпуск с:

```
[https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/)

```

или загрузите этот репозиторий ядра с уже включенными новыми патчами:

```
git clone [https://github.com/megous/linux.git](https://github.com/megous/linux.git)

```

```
# cd linux

```

Вот базовый конфигурационный файл для начала:

```
# wget [https://github.com/armbian/build/raw/master/config/kernel/linux-sunxi-next.config](https://github.com/armbian/build/raw/master/config/kernel/linux-sunxi-next.config) -O .config
# make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j4
# make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- INSTALL_MOD_PATH=/mnt  -j4 modules_install
# cp arch/arm64/boot/Image /mnt/boot
# cp arch/arm64/boot/dts/allwinner/sun50i-h5-orangepi-pc2.dtb /mnt/boot/dtbs/allwinner/sun50i-h5-orangepi-pc2.dtb

```

измените /mnt/boot/boot.cmd на

 `boot.cmd` 
```
part uuid ${devtype} ${devnum}:${bootpart} uuid
setenv bootargs console=${console} root=PARTUUID=${uuid} rw rootwait
setenv fdtfile allwinner/sun50i-h5-orangepi-pc2.dtb

if load ${devtype} ${devnum}:${bootpart} ${kernel_addr_r} /boot/Image; then
  if load ${devtype} ${devnum}:${bootpart} ${fdt_addr_r} /boot/dtbs/${fdtfile}; then
    if load ${devtype} ${devnum}:${bootpart} ${ramdisk_addr_r} /boot/initramfs-linux.img; then
      booti ${kernel_addr_r} ${ramdisk_addr_r}:${filesize} ${fdt_addr_r};
    else
      booti ${kernel_addr_r} - ${fdt_addr_r};
    fi;
  fi;
fi
```

создать образ /mnt/boot/boot.scr для:

```
# mkimage -C none -A arm64 -T script -d /mnt/boot/boot.cmd /mnt/boot/boot.scr

```

## Смотрите также

*   ["Just another Geek's" blog about installing Linux](https://blog.christophersmart.com/2016/10/23/building-and-booting-upstream-linux-and-u-boot-for-orange-pi-one-arm-board/)