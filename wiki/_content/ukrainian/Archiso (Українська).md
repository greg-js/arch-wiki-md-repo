## Contents

*   [1 Що це?](#.D0.A9.D0.BE_.D1.86.D0.B5.3F)
*   [2 Установка Archiso](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_Archiso)
*   [3 Конфігурація створюваної системи](#.D0.9A.D0.BE.D0.BD.D1.84.D1.96.D0.B3.D1.83.D1.80.D0.B0.D1.86.D1.96.D1.8F_.D1.81.D1.82.D0.B2.D0.BE.D1.80.D1.8E.D0.B2.D0.B0.D0.BD.D0.BE.D1.97_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B8)
    *   [3.1 Makefile](#Makefile)
    *   [3.2 mkinitcpio.conf](#mkinitcpio.conf)
    *   [3.3 packages.list](#packages.list)
    *   [3.4 isomounts](#isomounts)
    *   [3.5 boot-files](#boot-files)
        *   [3.5.1 Использование isolinux](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_isolinux)
    *   [3.6 overlay](#overlay)
        *   [3.6.1 Добавление fstab](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_fstab)
        *   [3.6.2 Добавление пользователя](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F)
            *   [3.6.2.1 Вручную](#.D0.92.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
            *   [3.6.2.2 Используя useradd](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_useradd)
        *   [3.6.3 Добавление чего-либо в домашнюю директорию пользователя при загрузке](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.87.D0.B5.D0.B3.D0.BE-.D0.BB.D0.B8.D0.B1.D0.BE_.D0.B2_.D0.B4.D0.BE.D0.BC.D0.B0.D1.88.D0.BD.D1.8E.D1.8E_.D0.B4.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D1.8E_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5)
        *   [3.6.4 Закрытие темы оверлея](#.D0.97.D0.B0.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D1.82.D0.B5.D0.BC.D1.8B_.D0.BE.D0.B2.D0.B5.D1.80.D0.BB.D0.B5.D1.8F)
*   [4 Генерация образа](#.D0.93.D0.B5.D0.BD.D0.B5.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0)
*   [5 Links](#Links)

## Що це?

**Archiso** - набір bash скриптів, призначених для створення повністю функціональних Live-CD/DVD і Live-USB на базі Arch Linux. Це досить гнучкий інструмент, який може бути використаний як для створення дисків відновлення або встановлення, так і для спеціалізованих live-CD/DVD/USB систем. Центр Archiso - **mkarchiso**. Для отримання детального опису всіх його опцій досить викликати його без параметрів, так що тут буде описано тільки створення live диска своїми руками.

Завдяки останнім доробкам Archiso тепер створює такі ISO образи, котрі можна записати як на диск, так і на USB flash носій.

## Установка Archiso

Archiso можна встановити двома способами:

*   Через [AUR](https://aur.archlinux.org/packages.php?ID=25996) (рекомендується использовать [yaourt](/index.php/Yaourt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Yaourt (Русский)"))(рекомендований метод)
*   Самостійно поставити з Git:

```
$ git clone [git://projects.archlinux.org/archiso.git](git://projects.archlinux.org/archiso.git)
$ cd archiso/archiso
$ sudo make install
$ sudo pacman -S mkinitcpio cdrkit squashfs-tools devtools syslinux mkinitcpio-nfs-utils nbd

```

**Note:** Зараз Archiso, що міститься в [extra](/index.php/Official_repositories "Official repositories"), застарілий та не відповідає даній статті.

## Конфігурація створюваної системи

### Makefile

Спочатку створимо окрему директорію для роботи і перейдемо до неї.

```
$ mkdir myarch && cd myarch

```

Тепер створимо Makefile та пропишемо туда наступні інструкції.

```
$ vim Makefile

```

Нижче ви знайдете приклад Makefile.

**Warning:** Всі відступи в файлі робити табуляцією. На пробіли буде матюкатись.

**Warning:** В ранніх версіях працювала команда "mkinitcpio -c mkinitcpio.conf..." так чи інакше (можливо, через останні оновлення) тепер, якщо скрипт не может знайти конфіг-файл, вказуйте до нього повний шлях в mkinitcpio.conf, інакше ви можете отримати пустий initcpio на виході, через що отримана система не будет завантажуватись (VFS error, kernel panic)

`

```
#### Редагуйте даний файл для модифікації кінцевої системи.
#  Рабочая директория для построения системы.
**WORKDIR=work**
#  Список устанавливаемых приложений, either space separated in a string or line separated in a file. Может включать группы.
**PACKAGES="$(shell cat packages.list) syslinux"**
# Имя дистрибутива. Не зависит от/не определяет целевую архитектуру.
**NAME=myarch**
# Версия дистрибутива.
**VER=1.00**
# Версия ядра.
**KVER=2.6.32-ARCH**
# Архитектура.
**ARCH?=$(shell uname -m)**
# Директория, в которой находился пользователь, запустивший скрипт
**PWD:=$(shell pwd)**
# Полное (финальное) имя образа.
**FULLNAME="$(PWD)"/$(NAME)-$(VER)-$(ARCH)**

# Умолчальная инструкция make'у, для компиляции всего(?) (оригинал:"Default make instruction to build everything.")
**all: myarch**

# Запуск _base-fs_ перед сборкой финального ISO образа.
**myarch: base-fs**
	**mkarchiso -p syslinux iso "$(WORKDIR)" "$(FULLNAME)".iso**

# Основное правило для процесса создания файловой системы образа. Приложения отрабатывают слева на право.
# Тоесть, сначала _root-image_ в конце - _syslinux_.
**base-fs: root-image boot-files initcpio overlay iso-mounts syslinux**

# _root-image_ всегда запускается первым. 
# Скачивание и установка приложений в _$WORKDIR_.
**root-image: "$(WORKDIR)"/root-image/.arch-chroot**
**"$(WORKDIR)"/root-image/.arch-chroot:**
**root-image:**
	**mkarchiso -p $(PACKAGES) create "$(WORKDIR)"**

# Правило для создания /boot
**boot-files: root-image**
	**cp -r "$(WORKDIR)"/root-image/boot "$(WORKDIR)"/iso/**
	**cp -r boot-files/* "$(WORKDIR)"/iso/boot/**

# Правило для образов initcpio
**initcpio: "$(WORKDIR)"/iso/boot/myarch.img**
**"$(WORKDIR)"/iso/boot/myarch.img: mkinitcpio.conf "$(WORKDIR)"/root-image/.arch-chroot**
	**mkdir -p "$(WORKDIR)"/iso/boot**
	**mkinitcpio -c ./mkinitcpio.conf -b "$(WORKDIR)"/root-image -k $(KVER) -g $@**

# Подробнее см.: [Overlay](#overlay)
**overlay:**
	**mkdir -p "$(WORKDIR)"/overlay/etc/pacman.d**
	**cp -r overlay "$(WORKDIR)"/**
	**wget -O "$(WORKDIR)"/overlay/etc/pacman.d/mirrorlist [https://www.archlinux.org/mirrorlist/$(ARCH)/all/](https://www.archlinux.org/mirrorlist/$(ARCH)/all/)**
	**sed -i "s/#Server/Server/g" "$(WORKDIR)"/overlay/etc/pacman.d/mirrorlist**

# Правило для создания isomounts.
**iso-mounts: "$(WORKDIR)"/isomounts**
**"$(WORKDIR)"/isomounts: isomounts root-image**
	**sed "s|@ARCH@|$(ARCH)|g" isomounts > $@**

# Исполняется перед генерацией финального образа.
**syslinux: root-image**
	**mkdir -p $(WORKDIR)/iso/boot/isolinux**
	**cp $(WORKDIR)/root-image/usr/lib/syslinux/*.c32 $(WORKDIR)/iso/boot/isolinux/**
	**cp $(WORKDIR)/root-image/usr/lib/syslinux/isolinux.bin $(WORKDIR)/iso/boot/isolinux/**

# При вызове "make clean" отчищает систему от вчего, созданного в процессе создания образа.
**clean:**
	**rm -rf "$(WORKDIR)" "$(FULLNAME)".img "$(FULLNAME)".iso**

.PHONY: all myarch
.PHONY: base-fs
.PHONY: root-image boot-files initcpio overlay iso-mounts
.PHONY: syslinux
.PHONY: clean

```

Тоесть, при исполнении "make myarch" из под рута,происходит следующее:

*   **root-image** скачивает и устанавливает выбранные приложения в _$WORKDIR_
*   **boot-files** готовит загрузочные файлы и копирует загрузочные скрипты
*   **initcpio** работает с _initcpio_
*   **overlay** копирует файлы, перекрывающие базовую конфигурацию в _root-image_ в _$WORKDIR_
*   **iso-mounts** немного уличной магии с применением sed, чтобы AUFS знала, куда ей монтироваться при загрузке
*   **syslinux** копирует загрузчик
*   **myarch** создаёт конечный образ, пригодный для записи на CD/DVD/флешку.

`

Одного Makefile буде недостатньо, так що потрібно буде створити файли, описані нижче.

### mkinitcpio.conf

_initcpio_ необходим для создания системы,способной загружаться с CD/DVD/USB.

Создайте mkinitcpio.conf:

```
$ vim mkinitcpio.conf

```

Обычно он содержит следующую информацию:

```
HOOKS="base udev archiso block usb fw filesystems usbinput"

```

Благодаря этому ваша система сможет загружаться с CD/DVD или USB. Стоит отметить, что автоопределение железа и прочее настраивается не здесь.

### packages.list

Вам так-же понадобится список приложений, устанавливаемых на вашу live-систему. Как минимум вам понадобятся **base** и **kernel26**, но, вы вольны дополнять список приложениями на ваше усмотрение.

**Note:** **mkarchiso** использует _/etc/pacman.conf_ из основной системы. Если вы раскоментировали [testing], то приложения из него тоже будут использованы при создании образа.Если вы хотите использовать другой _pacman.conf_, вы можете создать его в папке проекта и использовать командой **mkarchiso -C pacman.conf**Для использования выделенного _pacman.conf_нужно добавить **-C pacman.conf** во все вызовы **mkarchiso** в Makefile.

```
$ vim packages.list

```

В список устанавливаемых пакетов будет разумно вставить, как минимум, следующее:

```
aufs2
aufs2-util
base
bash
coreutils
cpio
dhcpcd
dnsutils
file
fuse
kernel26
syslinux
nano

```

Этот список должен дать вам минимальную рабочую систему. Но не забывайте, что в ней не будет драйверов свыше включённых в ядро (видео, вай-фай, специализированные - их нужно будет добавить в список).

**Tip:** Вы так-же можете создать **[custom local repository](/index.php/Custom_local_repository "Custom local repository")** для подготовки пакетов. Просто поставьте ваш локальный репозитарий на первую позицию в используемом **pacman.conf**.

### isomounts

Вам понадобится файл, содержащий информацию о файловых системах, монтируемых при загрузке системы.

```
$ vim isomounts

```

Пример _isomounts_:

```
# archiso isomounts file
# img - location of image/directory to mount relative to addons directory
# arch - architecture of this image
# mount point - absolute location on the post-initrd root
# type - either 'bind' or 'squashfs' for now
# syntax: <img> <arch> <mount point> <type>
# ORDER MATTERS! Files take top-down precedence. Be careful
overlay.sqfs @ARCH@ / squashfs
root-image.sqfs @ARCH@ / squashfs

```

**Warning:** В конце файла должна быть пустая строка (EOF) иначе ждите, что система упадёт в kernel panic!

### boot-files

Вам нужно будет добавить директорию "boot-files" и поддиректорию "isolinux/" содержащую "isolinux.cfg".

**Warning:** Ввиду последних изменений поддержка [grub](/index.php/Grub "Grub") в Archiso была отменена. Пожалуйста, не используйте grub. Взамен, вы можете использовать isolinux из syslinux'а, при этом вы получите образ, который может быть записан не только на диск, но и на флэшку.

#### Использование isolinux

Использовать _isolinux_ просто:

```
$ mkdir -p boot-files/isolinux/
$ vim boot-files/isolinux/isolinux.cfg

```

Образец:

```
prompt 1
timeout 0
display myarch.msg
DEFAULT myarch

LABEL myarch
KERNEL /boot/vmlinuz26
APPEND initrd=/boot/myarch.img archisolabel=XXX tmpfs_size=75% locale=en_US.UTF-8

LABEL memtest86+
KERNEL /boot/memtest86+-2.10.bin

```

Возможно, вы захотите отображать сообщение над меню загрузки:

```
$ vim boot-files/isolinux/myarch.msg

```

Это может быть любое сообщение в ASCII:

```
HI GENTLEMEN LOL
WELCOME TO MY DISTRO
I HOPE U ENJOY MAKE UR TIME
HA-HA-HA
(ПРЕВЕД ДЖЕНТЕЛЬМЕНЫ Ы
 ДОБРО ПОЖАЛОВАТЬ В МОЙ ДИСТРИБУТИВЧЕГ
 НАДЕЮСЬ, ВАМ ПОНРАВИТСЯ ВРЕМЯ, КОТОРОЕ ВЫ НА НЕГО ПОТРАТИТЕ
 ГЫ-ГЫ-ГЫ)

```

Обратите внимание, что вам нужно будет где-нибудь достать memtest*.bin потому как в "поставку по умолчанию" он не входит. Если вы не хотите его использовать - закоментируйте.

Благодаря модульной структуре isolinux вы можете использовать большое колличество аддонов, потому что все *.c32 файлы скопированны и доступны вам. Подробней можете посмотреть [официальный сайт syslinux](http://syslinux.zytor.com/wiki/index.php/SYSLINUX) и [archiso git-репозитарий](https://projects.archlinux.org/archiso.git/tree/configs/syslinux-iso/boot-files). Использование вышеперечисленных аддонов позволяет создавать красивые и сложные меню. Подробнее см. [тут](http://syslinux.zytor.com/wiki/index.php/Comboot/menu.c32).

### overlay

**overlay** предназначен для включения в дистрибутив бинарных репозитариев, конфигов, отличающихся от умолчальных и прочего. _mkarchiso_ требует помещения всех файлов, предназначенных для оверлея, в одну директорию. Оверлей будет наложен на систему во время загрузки используя _AUFS_. Структура папки, содержащей файлы оверлея, должна повторять корневую систему.

Все файлы и директории, не существующие в оригинальной системе, но существующие в оверлее, будут созданы. Все файлы и директории существующие в оригинальной системе и в оверлее, будут перезаписаны оверлеем.

Создаём _overlay_:

```
$ mkdir overlay && cd overlay/

```

Это было легко, теперь надо наполнить оверлей полезняшками. Несколько примеров:

_**Note:** Важно, чтобы всем файлам в оверлее были назначены правильные права доступа.Поэтому все изменения в директории оврелея рекомендуется производить из под рута._

#### Добавление fstab

Если нужно добавить **fstab**:

```
$ mkdir etc
$ vim etc/fstab

```

```
aufs                   /             aufs      noauto              0      0
none                   /dev/pts      devpts    defaults            0      0
none                   /dev/shm      tmpfs     defaults            0      0

```

#### Добавление пользователя

##### Вручную

Так или иначе, но вам понядобятся пользователи в вашей live-системе. Есть много способов их добавления.Один из - скопировать файлы, для этого требуемые из корневой системы, и привести их в вид, удовлетворяющий вашим требованиям:

```
$ cp /etc/group etc/group
$ cp /etc/passwd etc/passwd
$ cp /etc/shadow etc/shadow

```

_**Note:** Не оставляёте зашифрованный пароль passwd или shadow файле! Пароль находится на второй позиции (после первого ':')._

Пример безпарольного пользователя:

```
root::99999::::::

```

Так-же не забудьте создать домашнюю папку для пользователя (не забудьте изменить домашнюю папку в _passwd_). Для создания домашней папки во время загрузки и добавления туда /etc/skel пользовательской папки можно использовать rc.local. Если про /etc/skel в слышите впервые, вам, и правда, следует об этом прочесть.

```
$ vim etc/rc.local
mkdir /home/archie && chown archie:archie /home/archie
su -c "cp -r /etc/skel/.[a-zA-Z0-9]* /home/archie/" archie

```

##### Используя useradd

Другим способом добавления пользователя является использование _etc/rc.local_ для создания пользователя при загрузке:

```
$ vim etc/rc.local

```

```
useradd -u 1000 -g users -G storage,floppy,optical,audio,video,network,games,wheel,disk -d /home/archie archie

```

```
Это создаст пользователя и домашнюю директорию для него.

```

#### Добавление чего-либо в домашнюю директорию пользователя при загрузке

Возможно, вы захотите добавить какие-то файлы кофигурации для пользователя live-системы.

Вам нужно будет создать следующую директорию, и поместить желаемое туда:

```
$ mkdir etc/skel

```

Для примера:

```
$ vim etc/skel/.bashrc 

```

```
alias ls='ls --color=auto'
PS1='[\u@\h \W]\$ '

```

Описание всего, что можно сделать таким образом, значительно выходит за рамки данной статьи.

_**Note:** Не пытайтесь использовать оверлей для прямого изменения /home/user/, это вызовет ошибки в правах доступа! Используйте /etc/skel/._

#### Закрытие темы оверлея

Некоторые темы, не рассмотренные в данной статье (потому как рассмотрены в вики):

*   Конфигурация _inittab_ для старта Х во время загрузки
*   Конфигурация _hosts_
*   Конфигурация _rc.conf_
*   Конфигурация _sudoers_
*   Конфигурация _rc.local_
*   Добавление большего колличества полезняшек etc/skel
*   Добавление большего колличества графического оформления
*   Добавление разнообраных бинарников в opt/

## Генерация образа

После всего времени, потраченного на конфигурацию, осталась самая приятная часть: Создание образа.

Это легко: Из под рута (это важно!) выполните следующую команду в директории вашего проекта (там, где лежит _Makefile_):

```
$ make all

```

На выходе вы получите .iso, готовый для записи на CD/DVD или USB:

```
dd if=my-image.iso of=/dev/some-usb-drive bs=8M

```

**Note:** Если на флеш носителе более одного раздела, не забудьте присвоить метку разделу, содержащему live-систему. Иначе с него будет не возможно загрузиться.

**Warning:** Осторожней с <tt>dd</tt>! Если вы используете его на не том устройстве, данные будет практически не возможно восстановить. Используйте с осторожностью.

## Links

[Archiso project page](https://projects.archlinux.org/?p=archiso.git;a=summary)

[Arch based distributions (active)](/index.php/Arch_based_distributions_(active) "Arch based distributions (active)")