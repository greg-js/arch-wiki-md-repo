**Состояние перевода:** На этой странице представлен перевод статьи [Installation guide](/index.php/Installation_guide "Installation guide"). Дата последней синхронизации: 26 сентября 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=543745).

Этот документ является руководством по установке [Arch Linux](/index.php/Arch_Linux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Linux (Русский)") из-под системы, запущенной с официального установочного образа. Перед установкой рекомендуется посмотреть [часто задаваемые вопросы](/index.php/%D0%A7%D0%B0%D1%81%D1%82%D0%BE_%D0%B7%D0%B0%D0%B4%D0%B0%D0%B2%D0%B0%D0%B5%D0%BC%D1%8B%D0%B5_%D0%B2%D0%BE%D0%BF%D1%80%D0%BE%D1%81%D1%8B "Часто задаваемые вопросы"). Чтобы получить разъяснения по понятиям, используемым на этой странице, смотрите статью [Help:Чтение](/index.php/Help:%D0%A7%D1%82%D0%B5%D0%BD%D0%B8%D0%B5 "Help:Чтение"). В частности, примеры кода могут содержать заполнители (отформатированные в `*курсиве*`), которые необходимо заменить вручную.

Более подробные инструкции приведены в соответствующих статьях [ArchWiki](/index.php/ArchWiki:About_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki:About (Русский)") и на [страницах справочных руководств (man)](/index.php/Man_page_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Man page (Русский)") различных программ. Ссылки и на то, и на другое присутствуют в этом руководстве. Также вы можете получить помощь в [IRC-канале](/index.php/IRC_channel_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "IRC channel (Русский)") и на [англоязычном](https://bbs.archlinux.org/) и [русскоязычном](http://archlinux.org.ru/forum/) форумах Arch Linux.

Arch Linux способен работать на любой [x86_64](https://en.wikipedia.org/wiki/ru:X86-64 "w:ru:X86-64")-совместимой машине, имеющей хотя бы 512 MB ОЗУ. Базовая установка со всеми пакетами группы [base](https://www.archlinux.org/groups/x86_64/base/) занимает меньше 800 MB дискового пространства. Поскольку для процесса установки требуется получать пакеты из удаленного репозитория, необходимо работающее интернет-соединение.

## Contents

*   [1 Перед установкой](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B4_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.BE.D0.B9)
    *   [1.1 Установка раскладки клавиатуры](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B8_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
    *   [1.2 Проверка загруженного режима](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B0)
    *   [1.3 Соединение с Интернетом](#.D0.A1.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81_.D0.98.D0.BD.D1.82.D0.B5.D1.80.D0.BD.D0.B5.D1.82.D0.BE.D0.BC)
    *   [1.4 Синхронизация системных часов](#.D0.A1.D0.B8.D0.BD.D1.85.D1.80.D0.BE.D0.BD.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D1.8B.D1.85_.D1.87.D0.B0.D1.81.D0.BE.D0.B2)
    *   [1.5 Разбиение дисков на разделы](#.D0.A0.D0.B0.D0.B7.D0.B1.D0.B8.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B4.D0.B8.D1.81.D0.BA.D0.BE.D0.B2_.D0.BD.D0.B0_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D1.8B)
    *   [1.6 Форматирование разделов](#.D0.A4.D0.BE.D1.80.D0.BC.D0.B0.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2)
    *   [1.7 Монтирование разделов](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [2.1 Выбор зеркал](#.D0.92.D1.8B.D0.B1.D0.BE.D1.80_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB)
    *   [2.2 Установка основных пакетов](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
*   [3 Настройка системы](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Часовой пояс](#.D0.A7.D0.B0.D1.81.D0.BE.D0.B2.D0.BE.D0.B9_.D0.BF.D0.BE.D1.8F.D1.81)
    *   [3.4 Локализация](#.D0.9B.D0.BE.D0.BA.D0.B0.D0.BB.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F)
    *   [3.5 Настройка сети](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D0.B5.D1.82.D0.B8)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Пароль суперпользователя](#.D0.9F.D0.B0.D1.80.D0.BE.D0.BB.D1.8C_.D1.81.D1.83.D0.BF.D0.B5.D1.80.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F)
    *   [3.8 Загрузчик](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D1.87.D0.B8.D0.BA)
*   [4 Перезагрузка](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0)
*   [5 После установки](#.D0.9F.D0.BE.D1.81.D0.BB.D0.B5_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)

## Перед установкой

Скачайте и запустите установочный образ, как это описано в статьях из категории [Получение и установка Arch](/index.php/%D0%9F%D0%BE%D0%BB%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D0%B5_%D0%B8_%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_Arch "Получение и установка Arch"). Вы автоматически войдете в систему от имени суперпользователя в первой [виртуальной консоли](https://en.wikipedia.org/wiki/ru:%D0%92%D0%B8%D1%80%D1%82%D1%83%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F_%D0%BA%D0%BE%D0%BD%D1%81%D0%BE%D0%BB%D1%8C "w:ru:Виртуальная консоль") и увидите перед собой приглашение интерпретатора [Zsh](/index.php/Zsh_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Zsh (Русский)").

Чтобы в процессе установки переключиться на другую виртуальную консоль, например, чтобы посмотреть это руководство при помощи браузера [ELinks](/index.php/ELinks "ELinks"), используйте [горячие клавиши](/index.php/%D0%93%D0%BE%D1%80%D1%8F%D1%87%D0%B8%D0%B5_%D0%BA%D0%BB%D0%B0%D0%B2%D0%B8%D1%88%D0%B8 "Горячие клавиши") `Alt+*стрелка*`. Для [редактирования](/index.php/Help:%D0%A7%D1%82%D0%B5%D0%BD%D0%B8%D0%B5#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.B8.D1.82.D1.8C.2C_.D1.81.D0.BE.D0.B7.D0.B4.D0.B0.D1.82.D1.8C.2C_.D1.80.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D1.82.D1.8C "Help:Чтение") файлов доступны [nano](/index.php/Nano_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5 "Nano (Русский)"), [vi](https://en.wikipedia.org/wiki/ru:vi "w:ru:vi") и [vim](/index.php/Vim_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5 "Vim (Русский)").

### Установка раскладки клавиатуры

По умолчанию используется [раскладка консоли](/index.php/%D0%A0%D0%B0%D1%81%D0%BA%D0%BB%D0%B0%D0%B4%D0%BA%D0%B0_%D0%BA%D0%BE%D0%BD%D1%81%D0%BE%D0%BB%D0%B8 "Раскладка консоли") [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "w:File:KB United States-NoAltGr.svg"). Чтобы посмотреть список доступных раскладок, запустите:

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

Чтобы изменить раскладку, добавьте имя соответствующего файла к команде [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), не указывая полного пути и расширения. Например, чтобы выбрать [русскую](https://en.wikipedia.org/wiki/File:KB_Russian.svg "w:File:KB Russian.svg") раскладку, запустите:

```
# loadkeys ru

```

[Консольные шрифты](/index.php/Fonts_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A8.D1.80.D0.B8.D1.84.D1.82_.D0.B2_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D0.B8 "Fonts (Русский)") расположены в каталоге `/usr/share/kbd/consolefonts/` и могут быть выбраны при помощи [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### Проверка загруженного режима

Если на материнской плате включен режим [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Unified Extensible Firmware Interface (Русский)"), [Archiso](/index.php/Archiso_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Archiso (Русский)") [загрузит](/index.php/Arch_boot_process_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch boot process (Русский)") Arch Linux соответствующим образом при помощи [systemd-boot](/index.php/Systemd-boot_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd-boot (Русский)"). Чтобы в этом убедиться, посмотрите содержимое каталога [efivars](/index.php/Unified_Extensible_Firmware_Interface_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9F.D1.80.D0.BE.D1.86.D0.B5.D1.81.D1.81_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8_.D0.B2_UEFI "Unified Extensible Firmware Interface (Русский)"):

```
# ls /sys/firmware/efi/efivars

```

Если такого каталога не существует, возможно, система загружена в режиме [BIOS](https://en.wikipedia.org/wiki/ru:BIOS "w:ru:BIOS") или CSM. Для получения дополнительной информации обратитесь к руководству пользователя вашей материнской платы.

### Соединение с Интернетом

Для [проводных](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) сетевых устройств установочный образ во время загрузки автоматически включает службу [dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)"). Соединение можно проверить с помощью утилиты [ping](https://en.wikipedia.org/wiki/ru:ping "wikipedia:ru:ping"):

```
# ping archlinux.org

```

Если узел недоступен, [остановите](/index.php/%D0%9E%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Остановите") службу *dhcpcd* при помощи команды `systemctl stop dhcpcd@*интерфейс*`, где `*интерфейс*` может быть [завершен по табу](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion"). Потом перейдите к настройке сети, как описано в [Настройка сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8 "Настройка сети").

### Синхронизация системных часов

Чтобы удостовериться, что время выставлено правильно, используйте [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1):

```
# timedatectl set-ntp true

```

Для проверки статуса службы используйте `timedatectl status`.

### Разбиение дисков на разделы

Когда запущенная система распознает накопители, они становятся доступны как [блочные устройства](https://en.wikipedia.org/wiki/Device_file#Naming_conventions "wikipedia:Device file"), например, `/dev/sda` или `/dev/nvme0n1`. Чтобы посмотреть их список, используйте [lsblk](/index.php/Lsblk "Lsblk") или *fdisk*.

```
# fdisk -l

```

Результаты, оканчивающиеся на `rom`, `loop` и `airoot`, можно игнорировать:

На выбранном накопителе **должны присутствовать** следующие *разделы*:

*   Раздел для корневого каталога `/`
*   Если включен режим [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Unified Extensible Firmware Interface (Русский)"), необходим [системный раздел EFI](/index.php/%D0%A1%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%BD%D1%8B%D0%B9_%D1%80%D0%B0%D0%B7%D0%B4%D0%B5%D0%BB_EFI "Системный раздел EFI")

**Примечание:** [Пространство подкачки](/index.php/%D0%9F%D1%80%D0%BE%D1%81%D1%82%D1%80%D0%B0%D0%BD%D1%81%D1%82%D0%B2%D0%BE_%D0%BF%D0%BE%D0%B4%D0%BA%D0%B0%D1%87%D0%BA%D0%B8 "Пространство подкачки") можно расположить на отдельном разделе или в [файле](/index.php/Swap_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A4.D0.B0.D0.B9.D0.BB_.D0.BF.D0.BE.D0.B4.D0.BA.D0.B0.D1.87.D0.BA.D0.B8 "Swap (Русский)").

Для редактирования *таблицы разделов* используйте [fdisk](/index.php/Fdisk_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fdisk (Русский)") или [parted](/index.php/GNU_Parted_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNU Parted (Русский)").

```
# fdisk /dev/*sda*

```

Для получения дополнительной информации смотрите статью [Разметка дисков](/index.php/%D0%A0%D0%B0%D0%B7%D0%BC%D0%B5%D1%82%D0%BA%D0%B0_%D0%B4%D0%B8%D1%81%D0%BA%D0%BE%D0%B2 "Разметка дисков").

**Примечание:** Если вы хотите создать составное блочное устройство для [LVM](/index.php/LVM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LVM (Русский)"), [шифрования диска](/index.php/Disk_encryption "Disk encryption") или [RAID](/index.php/RAID_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "RAID (Русский)"), сделайте это сейчас.

### Форматирование разделов

Когда разделы созданы, каждый из них необходимо отформатировать в подходящую [файловую систему](/index.php/%D0%A4%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D0%B5_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B "Файловые системы"). Например, чтобы отформатировать корневой раздел `/dev/*sda1*` в `*ext4*`, выполните:

```
# mkfs.*ext4* /dev/*sda1*

```

Если вы создали раздел для подкачки (например, `/dev/*sda3*`), инициализируйте его через утилиту *mkswap*:

```
# mkswap /dev/*sda3*
# swapon /dev/*sda3*

```

Для получения дополнительной информации смотрите раздел [Файловые системы#Создание файловой системы](/index.php/%D0%A4%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D0%B5_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.BE.D0.B9_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B "Файловые системы").

### Монтирование разделов

[Смонтируйте](/index.php/%D0%A1%D0%BC%D0%BE%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B9%D1%82%D0%B5 "Смонтируйте") файловую систему корневого раздела в каталог `/mnt`, например:

```
# mount /dev/*sda1* /mnt

```

Создайте точки монтирования для всех остальных разделов и примонтируйте их, например:

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

В дальнейшем [genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) обнаружит смонтированные файловые системы и пространство подкачки.

## Установка

### Выбор зеркал

Пакеты для установки должны скачиваться с [серверов-зеркал](/index.php/Mirrors_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mirrors (Русский)"), прописанных в файле `/etc/pacman.d/mirrorlist`. В установочном образе все зеркала включены и отсортированы по статусу синхронизации и скорости в момент создания этого установочного образа.

Чем выше зеркало расположено в этом списке, тем больший приоритет оно имеет при скачивании пакета. Скорее всего, вы захотите отредактировать этот файл, чтобы передвинуть наверх наиболее географически близкие к вам зеркала. При этом также учитывайте и другие критерии.

Позже *pacstrap* скопирует этот файл в новую систему, так что это действительно стоит сделать.

### Установка основных пакетов

Используйте скрипт [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in), чтобы установить группу пакетов [base](https://www.archlinux.org/groups/x86_64/base/):

```
# pacstrap /mnt base

```

В этой группе содержатся не все инструменты, имеющиеся на установочном носителе, например, в ней нет [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) и специфичных прошивок беспроводных сетевых устройств; список можно посмотреть на странице [packages.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64).

Чтобы [установить](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C "Установить") другие необходимые пакеты или группы, например, [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), добавьте их имена к команде *pacstrap* (разделяя их пробелом) или используйте команды [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") после шага [#Chroot](#Chroot).

## Настройка системы

### Fstab

Сгенерируйте файл [fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)") (используйте ключ `-U` или `-L`, чтобы для идентификации разделов использовались [UUID](/index.php/UUID "UUID") или метки, соответственно):

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

После этого проверьте файл `/mnt/etc/fstab` и отредактируйте его в случае необходимости.

### Chroot

[Перейдите к корневому каталогу](/index.php/Change_root_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Change root (Русский)") новой системы:

```
# arch-chroot /mnt

```

### Часовой пояс

Задайте [часовой пояс](/index.php/%D0%92%D1%80%D0%B5%D0%BC%D1%8F#.D0.A7.D0.B0.D1.81.D0.BE.D0.B2.D0.BE.D0.B9_.D0.BF.D0.BE.D1.8F.D1.81 "Время"):

```
# ln -sf /usr/share/zoneinfo/*Регион*/*Город* /etc/localtime

```

Запустите [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8), чтобы сгенерировать `/etc/adjtime`:

```
# hwclock --systohc

```

Эта команда предполагает, что аппаратные часы настроены в формате [UTC](https://en.wikipedia.org/wiki/ru:%D0%92%D1%81%D0%B5%D0%BC%D0%B8%D1%80%D0%BD%D0%BE%D0%B5_%D0%BA%D0%BE%D0%BE%D1%80%D0%B4%D0%B8%D0%BD%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D0%B5_%D0%B2%D1%80%D0%B5%D0%BC%D1%8F "w:ru:Всемирное координированное время"). Для получения дополнительной информации смотрите раздел [Время#Стандарты времени](/index.php/%D0%92%D1%80%D0%B5%D0%BC%D1%8F#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D1.8B_.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.B8 "Время").

### Локализация

Включите `en_US.UTF-8 UTF-8` и другие необходимые [локали](/index.php/%D0%9B%D0%BE%D0%BA%D0%B0%D0%BB%D0%B8 "Локали") (например, `ru_RU.UTF-8 UTF-8`), раскомментировав их в файле `/etc/locale.gen`, после чего сгенерируйте их:

```
# locale-gen

```

Задайте необходимое значение [переменной](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `LANG` в файле [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5), например:

 `/etc/locale.conf`  `LANG=*ru_RU.UTF-8*` 

Если вы [меняли раскладку клавиатуры](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B8_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B), сделайте это изменение постоянным в файле [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5). Также добавьте шрифт для консоли с поддержкой кириллицы:

 `/etc/vconsole.conf` 
```
KEYMAP=*ru*
FONT=cyr-sun16
```

### Настройка сети

Создайте файл [hostname](/index.php/Hostname "Hostname"):

 `/etc/hostname` 
```
*моёимяхоста*

```

Добавьте соответствующую запись в файл [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost
::1		localhost
127.0.1.1	*моёимяхоста*.localdomain	*моёимяхоста*

```

Если система имеет постоянный IP-адрес, его следует использовать вместо `127.0.1.1`.

Завершите [настройку сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8 "Настройка сети") для вновь установленной среды.

### Initramfs

Как правило, создание нового образа *initramfs* не требуется, поскольку *pacstrap* автоматически запускает [mkinitcpio](/index.php/Mkinitcpio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mkinitcpio (Русский)") после установки пакета [linux](https://www.archlinux.org/packages/?name=linux).

Если вам нужно что-либо изменить, отредактируйте файл [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) и пересоздайте образ *initramfs*:

```
# mkinitcpio -p linux

```

### Пароль суперпользователя

Установите [пароль](/index.php/Users_and_groups_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F.D0.BC.D0.B8 "Users and groups (Русский)") суперпользователя:

```
# passwd

```

### Загрузчик

Для запуска Arch Linux необходимо установить загрузчик с поддержкой Linux. Чтобы узнать о всех доступных вариантах, обратитесь к категории [Загрузчики](/index.php/Category:Boot_loaders_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Boot loaders (Русский)").

Если вы используете процессор Intel или AMD, включите обновление [микрокод](/index.php/%D0%9C%D0%B8%D0%BA%D1%80%D0%BE%D0%BA%D0%BE%D0%B4 "Микрокод")а.

## Перезагрузка

Выйдите из окружения chroot, набрав `exit` или нажав `Ctrl+D`.

Вы можете размонтировать все разделы с помощью команды `umount -R /mnt`, чтобы убедиться в том, что ни один из разделов не остался занят какой-либо программой. Если нужно, для поиска таких программ используйте [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Теперь перезагрузите компьютер, набрав `reboot`: если какие-нибудь разделы остались смонтированными, [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") их размонтирует. Не забудьте извлечь установочный диск. После загрузки войдите в систему в качестве суперпользователя.

## После установки

Дальнейшие указания по настройке системы после установки (например, по настройке графического интерфейса, звука или тачпада) вы можете найти на странице [Основные рекомендации](/index.php/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D0%BD%D1%8B%D0%B5_%D1%80%D0%B5%D0%BA%D0%BE%D0%BC%D0%B5%D0%BD%D0%B4%D0%B0%D1%86%D0%B8%D0%B8 "Основные рекомендации").

Множество интересных и полезных программ вы найдете на странице [Список приложений](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9 "Список приложений").