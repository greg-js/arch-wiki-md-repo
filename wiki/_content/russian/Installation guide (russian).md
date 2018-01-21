**Состояние перевода:** На этой странице представлен перевод статьи [Installation guide](/index.php/Installation_guide "Installation guide"). Дата последней синхронизации: 19 июля 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=482303).

Этот документ является руководством по установке [Arch Linux](/index.php/Arch_Linux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Linux (Русский)") из-под системы, запущенной с официального установочного образа. Перед установкой рекомендуется посмотреть [часто задаваемые вопросы](/index.php/%D0%A7%D0%B0%D1%81%D1%82%D0%BE_%D0%B7%D0%B0%D0%B4%D0%B0%D0%B2%D0%B0%D0%B5%D0%BC%D1%8B%D0%B5_%D0%B2%D0%BE%D0%BF%D1%80%D0%BE%D1%81%D1%8B "Часто задаваемые вопросы"). Чтобы получить разъяснения по понятиям, используемым на этой странице, смотрите статью [Help:Чтение](/index.php/Help:%D0%A7%D1%82%D0%B5%D0%BD%D0%B8%D0%B5 "Help:Чтение").

Более подробные инструкции приведены в соответствующих статьях [ArchWiki](/index.php/ArchWiki:About_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki:About (Русский)") и на [страницах справочных руководств (man)](/index.php/Man_page_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Man page (Русский)") различных программ. Ссылки и на то, и на другое присутствуют в этом руководстве. Общий обзор процесса настройки смотрите на странице [archlinux(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/archlinux.7). Также вы можете получить помощь в [IRC-канале](/index.php/IRC_channel_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "IRC channel (Русский)") и на [англоязычном](https://bbs.archlinux.org/) и [русскоязычном](http://archlinux.org.ru/forum/) форумах Arch Linux.

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
    *   [3.4 Локаль](#.D0.9B.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C)
    *   [3.5 Имя хоста](#.D0.98.D0.BC.D1.8F_.D1.85.D0.BE.D1.81.D1.82.D0.B0)
    *   [3.6 Настройка сети](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D0.B5.D1.82.D0.B8)
    *   [3.7 Initramfs](#Initramfs)
    *   [3.8 Пароль суперпользователя](#.D0.9F.D0.B0.D1.80.D0.BE.D0.BB.D1.8C_.D1.81.D1.83.D0.BF.D0.B5.D1.80.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F)
    *   [3.9 Загрузчик](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D1.87.D0.B8.D0.BA)
*   [4 Перезагрузка](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0)
*   [5 После установки](#.D0.9F.D0.BE.D1.81.D0.BB.D0.B5_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)

## Перед установкой

Arch Linux способен работать на любой [x86_64](https://en.wikipedia.org/wiki/ru:X86-64 "w:ru:X86-64")-совместимой машине, имеющей хотя бы 512 MB ОЗУ. Базовая установка со всеми пакетами группы [base](https://www.archlinux.org/groups/x86_64/base/) занимает меньше 800 MB дискового пространства. Поскольку для процесса установки требуется получать пакеты из удаленного репозитория, необходимо работающее интернет-соединение.

Скачайте и запустите установочный образ, как это описано в статьях из категории [Получение и установка Arch](/index.php/Category:Getting_and_installing_Arch_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Getting and installing Arch (Русский)"). Вы автоматически войдете в систему от имени суперпользователя в первой [виртуальной консоли](https://en.wikipedia.org/wiki/ru:%D0%92%D0%B8%D1%80%D1%82%D1%83%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F_%D0%BA%D0%BE%D0%BD%D1%81%D0%BE%D0%BB%D1%8C "w:ru:Виртуальная консоль") и увидите перед собой приглашение интерпретатора [Zsh](/index.php/Zsh_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Zsh (Русский)"). Вы можете использовать [автоматическую подстановку по клавише tab](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion") для часто используемых команд, таких как, например, [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1).

Чтобы в процессе установки переключиться на другую виртуальную консоль, например, чтобы посмотреть это руководство при помощи браузера [ELinks](/index.php/ELinks "ELinks"), используйте [горячие клавиши](/index.php/Keyboard_shortcuts "Keyboard shortcuts") `Alt+*стрелка*`. Для [редактирования](/index.php/Help:Reading_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.B8.D1.82.D1.8C.2C_.D1.81.D0.BE.D0.B7.D0.B4.D0.B0.D1.82.D1.8C.2C_.D1.80.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D1.82.D1.8C "Help:Reading (Русский)") файлов доступны [nano](/index.php/Nano_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5 "Nano (Русский)"), [vi](https://en.wikipedia.org/wiki/ru:vi "w:ru:vi") and [vim](/index.php/Vim_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5 "Vim (Русский)").

### Установка раскладки клавиатуры

По умолчанию используется [раскладка](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "w:File:KB United States-NoAltGr.svg"). Чтобы посмотреть список доступных раскладок, запустите `ls /usr/share/kbd/keymaps/**/*.map.gz`. Чтобы изменить раскладку, добавьте имя соответствующего файла к команде [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), не указывая полного пути и расширения. Например, чтобы выбрать [русскую](https://en.wikipedia.org/wiki/File:KB_Russian.svg "w:File:KB Russian.svg") раскладку, запустите `loadkeys ru`.

[Консольные шрифты](/index.php/Fonts_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A8.D1.80.D0.B8.D1.84.D1.82_.D0.B2_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D0.B8 "Fonts (Русский)") расположены в каталоге `/usr/share/kbd/consolefonts/` и могут быть выбраны при помощи [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### Проверка загруженного режима

Если на материнской плате включен режим [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Unified Extensible Firmware Interface (Русский)"), [Archiso](/index.php/Archiso_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Archiso (Русский)") [загрузит](/index.php/Arch_boot_process_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch boot process (Русский)") Arch Linux соответствующим образом при помощи [systemd-boot](/index.php/Systemd-boot_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd-boot (Русский)"). Чтобы в этом убедиться, посмотрите содержимое каталога [efivars](/index.php/Unified_Extensible_Firmware_Interface_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9F.D1.80.D0.BE.D1.86.D0.B5.D1.81.D1.81_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8_.D0.B2_UEFI "Unified Extensible Firmware Interface (Русский)"):

```
# ls /sys/firmware/efi/efivars

```

Если такого каталога не существует, возможно, система загружена в режиме [BIOS](https://en.wikipedia.org/wiki/ru:BIOS "w:ru:BIOS") или CSM. Для получения дополнительной информации обратитесь к руководству пользователя вашей материнской платы.

### Соединение с Интернетом

Для [проводных](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) сетевых устройств установочный образ во время загрузки автоматически [включает](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") службу [dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)"). Соединение можно проверить:

```
# ping archlinux.org

```

Если узел недоступен, [остановите](/index.php/%D0%9E%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Остановите") службу *dhcpcd* при помощи `systemctl stop dhcpcd@`, `Tab` и обратитесь к разделу [Настройка сети#Драйвер устройства](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8#.D0.94.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0 "Настройка сети").

Для **беспроводных** соединений доступны [iw(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iw.8), [wpa_supplicant(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.8) и [netctl](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Netctl (Русский)"). Также смотрите статью [Настройка беспроводной сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D0%B1%D0%B5%D1%81%D0%BF%D1%80%D0%BE%D0%B2%D0%BE%D0%B4%D0%BD%D0%BE%D0%B9_%D1%81%D0%B5%D1%82%D0%B8 "Настройка беспроводной сети").

### Синхронизация системных часов

Чтобы удостовериться, что время выставлено правильно, используйте [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1):

```
# timedatectl set-ntp true

```

Для проверки статуса службы используйте `timedatectl status`.

### Разбиение дисков на разделы

Когда запущенная система распознает накопители, они становятся доступны как *блочные устройства*, например, `/dev/sda`. Чтобы посмотреть их список, используйте [lsblk](/index.php/Lsblk "Lsblk") или *fdisk*, при этом результаты, оканчивающиеся на `rom`, `loop` и `airoot`, можно игнорировать:

```
# fdisk -l

```

На выбранном накопителе должны присутствовать следующие *разделы* (показываются с цифрой на конце):

*   Раздел для корневого каталога `/`
*   Если включен режим [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Unified Extensible Firmware Interface (Русский)"), необходим [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition")

[Пространство подкачки](/index.php/Swap "Swap") можно расположить на отдельном разделе или в [файле](/index.php/Swap#Swap_file "Swap").

Для редактирования *разметки дисков* используйте [fdisk](/index.php/Fdisk "Fdisk") или [parted](/index.php/Parted "Parted"). Для получения дополнительной информации смотрите статью [Разметка дисков](/index.php/%D0%A0%D0%B0%D0%B7%D0%BC%D0%B5%D1%82%D0%BA%D0%B0_%D0%B4%D0%B8%D1%81%D0%BA%D0%BE%D0%B2 "Разметка дисков").

Если вы хотите создать составное блочное устройство для [LVM](/index.php/LVM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LVM (Русский)"), [шифрования диска](/index.php/Disk_encryption "Disk encryption") или [RAID](/index.php/RAID "RAID"), сделайте это сейчас.

### Форматирование разделов

Когда разделы созданы, каждый из них необходимо отформатировать в подходящую [файловую систему](/index.php/File_systems "File systems"). Например, чтобы отформатировать корневой раздел `/dev/*sda1*` в `*ext4*`, выполните:

```
# mkfs.*ext4* /dev/*sda1*

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

В этой группе содержатся не все инструменты, имеющиеся на установочном носителе, например, в ней нет [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) и специфичных прошивок беспроводных сетевых устройств; список можно посмотреть на странице [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both).

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

Задайте [часовой пояс](/index.php/Time_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A7.D0.B0.D1.81.D0.BE.D0.B2.D0.BE.D0.B9_.D0.BF.D0.BE.D1.8F.D1.81 "Time (Русский)"):

```
# ln -sf /usr/share/zoneinfo/*Регион*/*Город* /etc/localtime

```

Запустите [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8), чтобы сгенерировать `/etc/adjtime`:

```
# hwclock --systohc

```

Эта команда предполагает, что аппаратные часы настроены в формате [UTC](https://en.wikipedia.org/wiki/ru:%D0%92%D1%81%D0%B5%D0%BC%D0%B8%D1%80%D0%BD%D0%BE%D0%B5_%D0%BA%D0%BE%D0%BE%D1%80%D0%B4%D0%B8%D0%BD%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D0%B5_%D0%B2%D1%80%D0%B5%D0%BC%D1%8F "w:ru:Всемирное координированное время"). Для получения дополнительной информации смотрите раздел [Время#Стандарты времени](/index.php/%D0%92%D1%80%D0%B5%D0%BC%D1%8F#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D1.8B_.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.B8 "Время").

### Локаль

Включите `en_US.UTF-8 UTF-8` и другие необходимые [локализации](/index.php/Locale_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Locale (Русский)") (например, `ru_RU.UTF-8 UTF-8`), раскомментировав их в файле `/etc/locale.gen`, после чего сгенерируйте их:

```
# locale-gen

```

Задайте необходимое значение [переменной](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `LANG` в файле [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5), например:

 `/etc/locale.conf`  `LANG=*ru_RU.UTF-8*` 

Если вы [меняли раскладку клавиатуры](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B8_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B), сделайте это изменение постоянным в файле [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5):

 `/etc/vconsole.conf`  `KEYMAP=*ru*` 

### Имя хоста

Создайте файл [hostname(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.5):

 `/etc/hostname` 
```
*моёимяхоста*

```

Рекомендуется также добавить соответствующую запись в файл [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost.localdomain	localhost
::1		localhost.localdomain	localhost
**127.0.1.1	*моёимяхоста*.localdomain	*моёимяхоста***

```

Смотрите также раздел [Настройка сети#Установка имени узла](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8.D0.BC.D0.B5.D0.BD.D0.B8_.D1.83.D0.B7.D0.BB.D0.B0 "Настройка сети").

### Настройка сети

В свежеустановленном окружении нет сетевых соединений, активированных по умолчанию. Чтобы их настроить, обратитесь к разделу [Network configuration#Network managers](/index.php/Network_configuration#Network_managers "Network configuration").

Для [настройки беспроводной сети](/index.php/Wireless_network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wireless network configuration (Русский)") [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакеты [iw](https://www.archlinux.org/packages/?name=iw) и [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), а также требуемые [пакеты прошивок](/index.php/Wireless_network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0.2F.D0.BF.D1.80.D0.BE.D1.88.D0.B8.D0.B2.D0.BA.D0.B8 "Wireless network configuration (Русский)"). Если вы хотите использовать*wifi-menu*, установите пакет [dialog](https://www.archlinux.org/packages/?name=dialog).

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

Чтобы узнать о всех доступных вариантах конфигурации, обратитесь к категории [Загрузчики](/index.php/Category:Boot_loaders_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Boot loaders (Русский)").

Если вы используете процессор Intel, дополнительно установите пакет [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) и [включите обновления микрокода](/index.php/Microcode_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D0.BA.D0.BE.D0.B4.D0.B0 "Microcode (Русский)").

## Перезагрузка

Выйдите из окружения chroot, набрав `exit` или нажав `Ctrl+D`.

Вы можете размонтировать все разделы с помощью команды `umount -R /mnt`, чтобы убедиться в том, что ни один из разделов не остался занят какой-либо программой. Если нужно, для поиска таких программ используйте [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Теперь перезагрузите компьютер, набрав `reboot`: если какие-нибудь разделы остались смонтированными, [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") их размонтирует. Не забудьте извлечь установочный диск. После загрузки войдите в систему в качестве суперпользователя.

## После установки

Дальнейшие указания по настройке системы после установки (например, по настройке графического интерфейса, звука или тачпада) вы можете найти на странице [Основные рекомендации](/index.php/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D0%BD%D1%8B%D0%B5_%D1%80%D0%B5%D0%BA%D0%BE%D0%BC%D0%B5%D0%BD%D0%B4%D0%B0%D1%86%D0%B8%D0%B8 "Основные рекомендации").

Множество интересных и полезных программ вы найдете на странице [Список приложений](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9 "Список приложений").