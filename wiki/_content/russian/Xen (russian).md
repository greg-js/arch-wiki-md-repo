Этот документ описывает установку Xen внутри Arch Linux.

## Contents

*   [1 Что такое Xen?](#.D0.A7.D1.82.D0.BE_.D1.82.D0.B0.D0.BA.D0.BE.D0.B5_Xen.3F)
*   [2 Установка Xen](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_Xen)
    *   [2.1 Установка необходимых пакетов](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BD.D0.B5.D0.BE.D0.B1.D1.85.D0.BE.D0.B4.D0.B8.D0.BC.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
    *   [2.2 Настройка GRUB](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_GRUB)
    *   [2.3 Настройка GRUB2](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_GRUB2)
    *   [2.4 Примеры добавления domU](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_.D0.B4.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_domU)
    *   [2.5 Аппаратная Виртуализация](#.D0.90.D0.BF.D0.BF.D0.B0.D1.80.D0.B0.D1.82.D0.BD.D0.B0.D1.8F_.D0.92.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F)
*   [3 Arch как гостевая система (режим паравиртуализации)](#Arch_.D0.BA.D0.B0.D0.BA_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D0.B0.D1.8F_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0_.28.D1.80.D0.B5.D0.B6.D0.B8.D0.BC_.D0.BF.D0.B0.D1.80.D0.B0.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8.29)
    *   [3.1 xe-guest-utilities](#xe-guest-utilities)
    *   [3.2 Примечания](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.87.D0.B0.D0.BD.D0.B8.D1.8F)
*   [4 Инструменты Управления Xen](#.D0.98.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D1.8B_.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_Xen)
*   [5 Полезные Пакеты](#.D0.9F.D0.BE.D0.BB.D0.B5.D0.B7.D0.BD.D1.8B.D0.B5_.D0.9F.D0.B0.D0.BA.D0.B5.D1.82.D1.8B)
*   [6 Ресурсы](#.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B)

## Что такое Xen?

По утверждению команды разработки Xen: "Xen, мощный гипервизор промышленного стандарта с открытым кодом для виртуализации, предлагает мощный, эффективный и безопасный набор возможностей для виртуализации в архитектурах x86, x86_64, IA64, PowerPC, и других. Он поддерживает широкий диапазон гостевых операционных систем включая Windows®, Linux®, Solaris®, и различные версии BSD."

Гипервизор Xen - это тонкий уровень программного обеспечения, которое эмулирует компьютерную архитектуру. Он запускается загрузчиком и позволяет нескольким операционным системам работать одновременно поверх него. После загрузки гипервизор Xen запускает "dom0" (означает "домен 0"), или привилегированный домен, на котором в нашем случае запущено модифицированное ядро Linux (другие возможные операционные системы для dom0 NetBSD и OpenSolaris). [Ядро dom0 в AUR](https://aur.archlinux.org/packages.php?ID=29023) в настоящее время базируется на ближайшей версии ядра Linux 2.6, а еще есть [более нестабильная -dev версия](https://aur.archlinux.org/packages.php?ID=38175); аппаратное обеспечение, конечно, должно поддерживаться этим ядром для того чтобы запускать Xen. После запуска dom0, один или больше "domU" (непривилегированный) доменов могут быть запущены и управляться из dom0.

## Установка Xen

### Установка необходимых пакетов

Перед компиляцией xen убедитесь, что у вас установлены gcc, make, patch, и python2.

 `pacman -S gcc make patch python2` 

Новый пакет xen содержит Xen 4 и разрешает практически все необходимые зависимости автоматически. Но вследствие изменений в официальной версии Python для Arch Linux, некоторые старые скрипты выдают ошибки при запуске. Для решения этого загрузите python2.5 из [AUR](/index.php/AUR "AUR").

И когда Вам будет предложено редактировать PKGBUILD (предпочтительнее nano), не следует забывать заменить вот это:

```
make PYTHON=python2 DESTDIR=$pkgdir  install-xen
make PYTHON=python2 DESTDIR=$pkgdir  install-tools
make PYTHON=python2 DESTDIR=$pkgdir  install-docs
```

на вот это:

```
make PYTHON=python2.5 DESTDIR=$pkgdir  install-xen
make PYTHON=python2.5 DESTDIR=$pkgdir  install-tools
make PYTHON=python2.5 DESTDIR=$pkgdir  install-docs

sed -i -e "s|#![ ]*/usr/bin/python$|#!/usr/bin/python2.5|" \
-e "s|#![ ]*/usr/bin/env python$|#!/usr/bin/env python2.5|" \
$(find $pkgdir -name '*.py')
```

Xen-tools - это набор простых perl-скриптов, который позволяет легко создавать новые гостевые домены Xen. [xen-tools](https://aur.archlinux.org/packages/xen-tools/) также есть в AUR.

Следующий шаг - скомпилировать и установить ядро dom0\. Для этого скомпилируйте пакет [kernel26-xen-dom0](https://aur.archlinux.org/packages.php?ID=29023) из AUR.

**Обратите внимание:** в настоящее время kernel26-xen-dom0 отмечен в AUR как устаревший и не обновляется до 2.6.36\. Так что Вам следует пройтись по новым параметрам 2.6.36 и согласиться использовать значения по умолчанию (или что еще Вы захотите) - так что просто нажмимайте enter всякий раз когда Вас спросят.

Установка закончена. Теперь Вы можете настроить Grub и загрузиться в ядро, которое только что было построено.

### Настройка GRUB

Grub должен быть настроен так, чтобы после загрузки гипервизора Xen загружалось ядро dom0\. Добавьте следующие строки в /boot/grub/menu.lst:

```
title Xen with Arch Linux
root (hd0,X)
kernel /xen.gz dom0_mem=524288
module /vmlinuz26-xen-dom0 root=/dev/sdaY ro console=tty0
module /kernel26-xen-dom0.img

```

здесь X и Y - соответствующие номера для Вашего диска; а dom0_mem, console и vga - опциональные настраиваемые параметры. Одна примечательная деталь: Вы также можете использовать LVM. Так что вместо /dev/sdaY Вы также можете указать /dev/mapper/такойто_lvm.

Стандартное ядро arch можно использовать для загрузки доменов domU. Для того чтобы это сделать следует добавить 'xen-blkfront' в раздел модулей в /etc/mkinitcpio.conf:

```
MODULES="... xen-blkfront ..."

```

Теперь, следующий шаг - загрузка в ядро xen.

Следующий шаг: запуск xend:

```
# /etc/rc.d/xend start

```

При использовании xen рекомендуется назначать фиксированный объем памяти. Также, если гостевые системы активно используют ввод-вывод, может быть полезным выделить (зафиксировать) один из процессорос только для dom0\. Пожалуйста посмотрите другую [XenCommonProblems](http://wiki.xensource.com/xenwiki/XenCommonProblems) секцию вики страницы "Как выделить одно ядро процессора (или ядра)только для dom0?" для дополнительной информации.

### Настройка GRUB2

Работает точно так же как с Grub, но здесь Вам нужно использовать команду 'multiboot' вместо использования 'kernel'. Так что это будет:

```
# (2) Arch Linux(XEN)
menuentry "Arch Linux(XEN)" {
    set root=(hd0,X)
    multiboot /boot/xen.gz dom0_mem=2048M
    module /boot/vmlinuz26-xen-dom0 root=/dev/sdaY ro
    module /boot/kernel26-xen-dom0.gz
}

```

Если у Вас получилось загрузиться в ядро dom0, тогда можно продолжать.

### Примеры добавления domU

Основная идея добавления domU такова. Мы должны получить ядра domU, выделить пространство для виртуального жесткого диска, создать файл конфигурации для domU, и затем запустить domU с помощью xm.

```
$ mkfs.ext4 /dev/sdb1    ## форматировать раздел
$ mkdir /tmp/install
$ mount /dev/sdb1 /tmp/install
$ mkdir -p /tmp/install/{dev,proc,sys} /tmp/install/var/lib/pacman /tmp/install/var/cache/pacman/pkg
$ mount -o bind /dev /tmp/install/dev
$ mount -t proc none /tmp/install/proc
$ mount -o bind /sys /tmp/install/sys
$ pacman -Sy -r /tmp/install --cachedir /tmp/install/var/cache/pacman/pkg -b /tmp/install/var/lib/pacman base
$ cp -r /etc/pacman* /tmp/install/etc
$ chroot /tmp/install /bin/bash
$ vi /etc/resolv.conf
$ vi /etc/fstab
    /dev/xvda               /           ext4    defaults                0       1

$ vi /etc/inittab
    c1:2345:respawn:/sbin/agetty -8 38400 hvc0 linux
    #c1:2345:respawn:/sbin/agetty -8 38400 tty1 linux
    #c2:2345:respawn:/sbin/agetty -8 38400 tty2 linux
    #c3:2345:respawn:/sbin/agetty -8 38400 tty3 linux
    #c4:2345:respawn:/sbin/agetty -8 38400 tty4 linux
    #c5:2345:respawn:/sbin/agetty -8 38400 tty5 linux
    #c6:2345:respawn:/sbin/agetty -8 38400 tty6 linux

$ exit  ## exit chroot
$ umount /tmp/install/dev
$ umount /tmp/install/proc
$ umount /tmp/install/sys
$ umount /tmp/install

```

If not starting from a fresh install and one wants to rsync from an existing system:

```
$ mkfs.ext4 /dev/sdb1    ## форматировать раздел lv
$ mkdir /tmp/install
$ mount /dev/sdb1 /tmp/install
$ mkdir /tmp/install/{proc,sys}
$ chmod 555 /tmp/install/proc
$ rsync -avzH --delete --exclude=proc/ --exclude=sys/ old_ooga:/ /tmp/install/

$ vi /etc/xen/dom01     ## создаем конфиг-файл
    #  -*- mode: python; -*-
    kernel = "/boot/vmlinuz26"
    ramdisk = "/boot/kernel26.img"
    memory = 1024
    name = "dom01"
    vif = [ 'mac=00:16:3e:00:01:01' ]
    disk = [ 'phy:/dev/sdb1,xvda,w' ]
    dhcp="dhcp"
    hostname = "ooga"
    root = "/dev/xvda ro"

$ xm create -c dom01

```

### Аппаратная Виртуализация

Если мы хотим для наших domUs аппаратную виртуализацию, хост-машина должна поддерживать виртуализацию либо Intel-VT либо AMD-V. Для того чтобы проверить это, запустите следующие команды на хост-машине:

Для процессоров Intel:

 `grep vmx /proc/cpuinfo` 

Для процессоров AMD:

 `grep svm /proc/cpuinfo` 

Если ни одна из вышеуказанных команд не дает вывода, тогда скорее всего эти возможности не поддерживаются и Ваше оборудование неспособно запускать гостевые ОС с аппаратной виртуализацией (HVM). Также может быть что процессор на хост-машине поддерживает одну из этих возможностей, но функциональность запрещена по умолчанию в системном БИОСе. Чтобы проверитьь это, откройте меню БИОС во время загрузки и поищите опции связанные с поддержкой виртуализации. Если такая опция есть и запрещена, то разрешите ее, загрузите систему и повторите предыдущие команды.

## Arch как гостевая система (режим паравиртуализации)

Чтобы использовать паравиртуализацию нужно установить:

*   [kernel26-xen](https://aur.archlinux.org/packages.php?ID=16087)
*   (optional) [xe-guest-utilities](https://aur.archlinux.org/packages/xe-guest-utilities/)

Измените режим на PV с помощью команд: (в dom0):

```
 xe vm-param-set uuid=<vm uuid> HVM-boot-policy=""
 xe vm-param-set uuid=<vm uuid> PV-bootloader=pygrub

```

Отредактируйте /boot/grub/menu.lst и добавьте kernel26-xen:

```
 # (1) Arch Linux (domU)
 title  Arch Linux (domU)
 root   (hd0,0)
 kernel /boot/vmlinuz26-xen root=/dev/xvda1 ro console=hvc0
 initrd /boot/kernel26-xen.img

```

Добавьте следующие модули xen в Ваш initcpio, добавив в MODULES в /etc/mkinitcpio.conf: "xen-blkfront xen-fbfront xenfs xen-netfront xen-kbdfront" и перекомпилируйте Ваш initcpio:

```
 mkinitcpio -p kernel26-xen

```

Раскомментируйте следующую строку в файле /etc/inittab для того чтобы разрешить консольный вход:

```
 h0:2345:respawn:/sbin/agetty -8 38400 hvc0 linux

```

### xe-guest-utilities

ЧТобы использовать xe-guest-utilities, добавьте точку монтирования xenfs в /etc/fstab:

```
 xenfs                  /proc/xen     xenfs     defaults            0      0

```

и добавьте xe-linux-distribution в раздел DAEMONS файла /etc/rc.conf.

### Примечания

*   pygrub не показывает меню загрузки. И некоторые версии pygrub не поддерживают сжатые lzma обычные ядра. Смотрите [https://bbs.archlinux.org/viewtopic.php?id=118525](https://bbs.archlinux.org/viewtopic.php?id=118525)
*   обычное ядро i686 не поддерживает xen вследствие highmem, но ядро x86_64 поддерживает. Смотрите [https://bugs.archlinux.org/task/24207?project=1](https://bugs.archlinux.org/task/24207?project=1). Но все же Вы можете использовать i686/x86_64 kernel26-xen как показано выше, если о но сжато gzip, а не lzma или xz
*   Чтобы избежать ошибок связанных с hwclock, установите HARDWARECLOCK="xen" в /etc/rc.conf (вообще Вы можете использовать здесь любое значение кроме "UTC" and "localtime")
*   Если Вы хотите вернуться к аппаратной виртуальной машине, установите HVM-boot-policy="BIOS order"
*   Если при загрузке Xen ядро вылетает в panic, и предлагает 'use apic="debug" and send an error report', попробуйте установить noapic в строке kernel в menu.lst

## Инструменты Управления Xen

The "Virtual Machine Manager" application is a desktop user interface for managing virtual machines. It presents a summary view of running domains, their live performance & resource utilization statistics. The detailed view graphs performance & utilization over time. Wizards enable the creation of new domains, and configuration & adjustment of a domain's resource allocation & virtual hardware. An embedded VNC client viewer presents a full graphical console to the guest domain.

[virt-manager-light](https://aur.archlinux.org/packages/virt-manager-light/)

## Полезные Пакеты

Поскольку в AUR много разных пакетов, и Вы можете потратить много времени, понимая, какие из них нужны, вот маленький набор самых (интересных) пакетов *xen*:

*   Мультиплатформенный клон интерфейса XenCenter с открытым кодом: [openxencenter](https://aur.archlinux.org/packages/openxencenter/)
*   Мультиплатформенный клон интерфейса XenCenter с открытым кодом (версия [svn](/index.php/Svn "Svn")): [openxencenter-svn](https://aur.archlinux.org/packages.php?ID=36074)
*   Интерфейс к облачной платформе Xen (Xen Cloud Platform): [xvp](https://aur.archlinux.org/packages/xvp/)

## Ресурсы

*   Домашняя страница Xen: [[1]](http://www.xen.org/)
*   Xen Вики: [[2]](http://wiki.xensource.com/xenwiki/)
*   Патчи ядра Xen: [[3]](http://code.google.com/p/gentoo-xen-kernel/)
*   Руководство Виртуатопии как заставить Windows Server 2008 работать с Xen: [[4]](http://www.virtuatopia.com/index.php/Virtualizing_Windows_Server_2008_with_Xen)