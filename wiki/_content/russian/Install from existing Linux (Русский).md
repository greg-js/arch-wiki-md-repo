Этот документ описывает bootstrapping process, нужный для того, чтобы установить Arch Linux из уже работающего хоста Linux. После bootstrapping, установка продолжается так, как описано в [руководстве по установке](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Installation guide (Русский)") Arch Linux.

Установка Arch Linux из-под другого Linux полезна для:

*   беспроводной установки Arch Linux, например для виртуального сервера
*   замены существующего Linux без LiveCD (смотрите [#Замена уже существующей системы без LiveCD](#.D0.97.D0.B0.D0.BC.D0.B5.D0.BD.D0.B0_.D1.83.D0.B6.D0.B5_.D1.81.D1.83.D1.89.D0.B5.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.89.D0.B5.D0.B9_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B_.D0.B1.D0.B5.D0.B7_LiveCD))
*   создания нового дистрибутива Linux или LiveCD основанного на Arch Linux
*   создания chroot окружения Arch Linux, например для контейнеров Docker
*   [rootfs-over-NFS для бездисковых систем](/index.php/Diskless_network_boot_NFS_root "Diskless network boot NFS root")

Цель процедуры начальной загрузки в том, чтобы настроить окружение, из которого можно будет запустить [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) (содержит такие скрипты как `pacstrap` и `arch-root`). Установить [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) нужно на самой хост-системе или настройкой chroot основанного на Arch Linux.

Если хост работает под Arch Linux, сразу установите [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts).

**Обратите внимание:** Этот гайд расчитан на то, что имеющийся хост может запускать программы архитектуры нового Arch Linux. В случае с x86_64 хостом, можно даже использовать i686-pacman при сборке 32-битного окружения chroot. Смотрите [Arch64 - установка встроенной 32-битной системы](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system").

## Contents

*   [1 Arch Linux-based chroot](#Arch_Linux-based_chroot)
    *   [1.1 Создаём chroot](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D1.91.D0.BC_chroot)
        *   [1.1.1 Способ 1: Использование Bootstrap образа (рекомендуется)](#.D0.A1.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_1:_.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_Bootstrap_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0_.28.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D1.83.D0.B5.D1.82.D1.81.D1.8F.29)
        *   [1.1.2 Способ 2: Используя образ LiveCD](#.D0.A1.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_2:_.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7_LiveCD)
    *   [1.2 Используем наше chroot окружение](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D0.BC_.D0.BD.D0.B0.D1.88.D0.B5_chroot_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5)
        *   [1.2.1 Начальная настройка хранилища ключей pacman](#.D0.9D.D0.B0.D1.87.D0.B0.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.85.D1.80.D0.B0.D0.BD.D0.B8.D0.BB.D0.B8.D1.89.D0.B0_.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.B9_pacman)
        *   [1.2.2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
            *   [1.2.2.1 Хост Debian](#.D0.A5.D0.BE.D1.81.D1.82_Debian)
            *   [1.2.2.2 Хост Fedora](#.D0.A5.D0.BE.D1.81.D1.82_Fedora)
        *   [1.2.3 Настройка системы](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
*   [2 Замена уже существующей системы без LiveCD](#.D0.97.D0.B0.D0.BC.D0.B5.D0.BD.D0.B0_.D1.83.D0.B6.D0.B5_.D1.81.D1.83.D1.89.D0.B5.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.89.D0.B5.D0.B9_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B_.D0.B1.D0.B5.D0.B7_LiveCD)

## Arch Linux-based chroot

Идея состоит в том, чтобы как бы запустить Arch Linux внутри уже имеющейся системы. Настоящая установка, которая будет содержаться внутри chroot, будет затем запущена из этой Arch системы. Есть два способа настроить и войти в chroot, они представлены ниже.

**Обратите внимание:** Хост-система должна использовать Linux 2.6.32 или новее.

**Обратите внимание:** Используйте только один из двух способов, и не забудьте дочитать эту статью до конца, чтобы закончить установку.

### Создаём chroot

#### Способ 1: Использование Bootstrap образа (рекомендуется)

Скачиваем образ bootstrap с [любого желаемого зеркала](https://www.archlinux.org/download), либо сразу используя прямую ссылку на нужный вам образ (с зеркала kernel.org):
Образ x86_64:

```
 $ curl -O [https://mirrors.kernel.org/archlinux/iso/2015.04.01/archlinux-bootstrap-2015.04.01-x86_64.tar.gz](https://mirrors.kernel.org/archlinux/iso/2015.04.01/archlinux-bootstrap-2015.04.01-x86_64.tar.gz)

```

Образ i686:

```
 $ curl -O [https://mirrors.kernel.org/archlinux/iso/2015.04.01/archlinux-bootstrap-2015.04.01-i686.tar.gz](https://mirrors.kernel.org/archlinux/iso/2015.04.01/archlinux-bootstrap-2015.04.01-i686.tar.gz)

```

Распаковываем его:

```
 # cd /tmp
 # tar xzf <путь-к-каталогу-где-образ>/archlinux-bootstrap-2015.02.01-*.tar.gz

```

Выбираем подходящий для вашего интернета сервер, откуда будут загружаться основные репозитории:

```
 # nano /tmp/root.*/etc/pacman.d/mirrorlist

```

**Обратите внимание:** Если ваша хост-система — x86_64, а образ boostrap — i686, то также подправьте `/tmp/root.i686/etc/pacman.conf`, ясно указав `Architecture = i686`, чтобы pacman качал пакеты под архитектуру i686.

Войдём в chroot

*   Если установлен bash 4 или новее, то:

```
  # /tmp/root.*/bin/arch-chroot /tmp/root.*/

```

*   Иначе:

```
  # cd /tmp/root.*
  # cp /etc/resolv.conf etc
  # mount --rbind /proc proc
  # mount --rbind /sys sys
  # mount --rbind /dev dev
  # mount --rbind /run run
    (при условии, что /run существует)
  # chroot /tmp/root.* /bin/bash

```

#### Способ 2: Используя образ LiveCD

Можно смонтировать корневой образ последнего установочного диска Arch Linux и затем заchroot'ить туда. Плюс этого способа в том, что у вас будет сразу рабочий Arch Linux installation прямо внутри хост-системы без надобности в его настройки.

**Обратите внимание:** Перед тем как продолжить, удостоверьтесь, что у вас последняя версия [squashfs](http://squashfs.sourceforge.net/) на хост-системе. Иначе будут ошибки типа: `FATAL ERROR aborting: uncompress_inode_table: failed to read block`.

*   Корневой образ можно скачать с одного из [зеркал](https://www.archlinux.org/download) в папке arch/x86_64/ либо arch/i686/, смотря какую архитектуру хотите. Образ имеет формат squashfs, который является read-only, поэтому нам надо распаковать его и смонтировать корневой образ (root-image.fs).

*   Чтобы распаковать корневой образ, надо

 `# unsquashfs -d /squashfs-root root-image.fs.sfs` 

*   Теперь смонтируем его с помощью опции loop

```
# mkdir /arch
# mount -o loop /squashfs-root/root-image.fs /arch

```

*   Перед тем как [chrooting](/index.php/Change_root "Change root") to it, нужно смонтировать некоторые виртуальные системные разделы, а затем скопировать resolv.conf для интернета.

```
# mount -t proc none /arch/proc
# mount -t sysfs none /arch/sys
# mount -o bind /dev /arch/dev
# mount -o bind /dev/pts /arch/dev/pts # важно для pacman (для проверки подписей)
# cp -L /etc/resolv.conf /arch/etc # а это, чтобы мог работать интернет в chroot

```

*   Теперь всё готово, чтобы to chroot в только что установленное окружение Arch

 `# chroot /arch bash` 

### Используем наше chroot окружение

#### Начальная настройка хранилища ключей pacman

Перед установкой, ключи pacman должны быть настроены. Перед тем как вводить следующие две команды, можете почитать [pacman-key#Initializing the keyring](/index.php/Pacman-key#Initializing_the_keyring "Pacman-key"), чтобы узнать entropy requirements:

```
# pacman-key --init
# pacman-key --populate archlinux

```

#### Установка

Следуйте [Installation guide#Mount the partitions](/index.php/Installation_guide#Mount_the_partitions "Installation guide") и [Installation guide#Install the base packages](/index.php/Installation_guide#Install_the_base_packages "Installation guide").

##### Хост Debian

На хостах Debian `pacstrap` выводит следующую ошибку:

```
# pacstrap /mnt base
# ==> Creating install root at /mnt
# mount: mount point /mnt/dev/shm is a symbolic link to nowhere
# ==> ERROR: failed to setup API filesystems in new root

```

Это потому, что в Debian `/dev/shm` ссылается на `/run/shm`, который в Arch-based chroot не существует, поэтому ссылка не рабочая. Чтобы исправить это, просто создайте каталог `/run/shm`:

```
# mkdir /run/shm

```

##### Хост Fedora

На хостах Fedora и Live USB, если у вас не получается сгенерировать ваш `[fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)")` с помощью `genfstab`, то удалите из fstab одинаковые записи и везде опции `seclabel` (это опция специфична для Fedora и поэтому не даст вам загрузиться).

#### Настройка системы

С этого момента просто следуйте согласно разделам начиная с «[Монтирование разделов](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2 "Installation guide (Русский)")» из [руководства по установке Arch Linux](/index.php/Installation_guide "Installation guide").

## Замена уже существующей системы без LiveCD

Освободите ~650МБ, например, переформатировав существующий swap-раздел (после окончания установки, можете обратно создать swap). Если не можете столько освободить, выясните точно, какие пакеты группы base вам понадобятся для того, чтобы get a system с работающим интернетом and running in the temporary partition. То есть надо будет ясно указать каждый пакет для pacstrap. И ещё надо указать -c, чтобы пакеты скачивались на хост-систему, дабы избежать недостатка свободного места.

После того как установили, перезагрузитесь в свою новую систему, затем [rsync the entire system](/index.php/Full_system_backup_with_rsync#With_a_single_command "Full system backup with rsync") to the primary partition. Fix the bootloader configuration before rebooting.