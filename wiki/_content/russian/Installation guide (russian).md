**Состояние перевода:** На этой странице представлен перевод статьи [Installation guide](/index.php/Installation_guide "Installation guide"). Дата последней синхронизации: 14 октября 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=585451).

Этот документ является руководством по установке [Arch Linux](/index.php/Arch_Linux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Linux (Русский)") из-под системы, запущенной с официального установочного образа. Перед установкой рекомендуется посмотреть [часто задаваемые вопросы](/index.php/%D0%A7%D0%B0%D1%81%D1%82%D0%BE_%D0%B7%D0%B0%D0%B4%D0%B0%D0%B2%D0%B0%D0%B5%D0%BC%D1%8B%D0%B5_%D0%B2%D0%BE%D0%BF%D1%80%D0%BE%D1%81%D1%8B "Часто задаваемые вопросы"). Чтобы получить разъяснения по понятиям, используемым на этой странице, смотрите статью [Help:Чтение](/index.php/Help:%D0%A7%D1%82%D0%B5%D0%BD%D0%B8%D0%B5 "Help:Чтение"). В частности, примеры кода могут содержать заполнители (отформатированные в `*курсиве*`), которые необходимо заменить вручную.

Более подробные инструкции приведены в соответствующих статьях [ArchWiki](/index.php/ArchWiki:About_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki:About (Русский)") и на [страницах справочных руководств (man)](/index.php/Man_page_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Man page (Русский)") различных программ. Ссылки и на то, и на другое присутствуют в этом руководстве. Также вы можете получить помощь в [IRC-канале](/index.php/IRC_channel_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "IRC channel (Русский)") и на [англоязычном](https://bbs.archlinux.org/) и [русскоязычном](http://archlinux.org.ru/forum/) форумах Arch Linux.

Arch Linux способен работать на любой [x86_64](https://en.wikipedia.org/wiki/ru:X86-64 "w:ru:X86-64")-совместимой машине, имеющей хотя бы 512 MiB ОЗУ. Базовая установка занимает меньше 800 MiB дискового пространства. Поскольку для процесса установки требуется получать пакеты из удалённого репозитория, необходимо работающее интернет-соединение.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Перед установкой](#Перед_установкой)
    *   [1.1 Проверка подписи](#Проверка_подписи)
    *   [1.2 Загрузка live-окружения](#Загрузка_live-окружения)
    *   [1.3 Установка раскладки клавиатуры](#Установка_раскладки_клавиатуры)
    *   [1.4 Проверка загруженного режима](#Проверка_загруженного_режима)
    *   [1.5 Соединение с Интернетом](#Соединение_с_Интернетом)
    *   [1.6 Синхронизация системных часов](#Синхронизация_системных_часов)
    *   [1.7 Разметка дисков](#Разметка_дисков)
        *   [1.7.1 Примеры схем](#Примеры_схем)
    *   [1.8 Форматирование разделов](#Форматирование_разделов)
    *   [1.9 Монтирование разделов](#Монтирование_разделов)
*   [2 Установка](#Установка)
    *   [2.1 Выбор зеркал](#Выбор_зеркал)
    *   [2.2 Установка основных пакетов](#Установка_основных_пакетов)
*   [3 Настройка системы](#Настройка_системы)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Часовой пояс](#Часовой_пояс)
    *   [3.4 Локализация](#Локализация)
    *   [3.5 Настройка сети](#Настройка_сети)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Пароль суперпользователя](#Пароль_суперпользователя)
    *   [3.8 Загрузчик](#Загрузчик)
*   [4 Перезагрузка](#Перезагрузка)
*   [5 После установки](#После_установки)

## Перед установкой

Установочный образ и его подпись [GnuPG](/index.php/GnuPG "GnuPG") можно получить с страницы [Загрузки](https://archlinux.org/download/).

### Проверка подписи

Рекомендуется проверять подпись образа перед его использование, особенно когда он был загружен с *зеркала HTTP*, где загрузки обычно подвержены перехвату для [подмены образа на вредоносный](https://www2.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html).

На системах с установленным [GnuPG](/index.php/GnuPG_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GnuPG (Русский)") это можно сделать, поместив *PGP signature* (находится на сайте загрузки в разделе *Checksums*) в каталог с образом и выполнив [команду](/index.php/GnuPG#Verify_a_signature "GnuPG"):

```
$ gpg --keyserver-options auto-key-retrieve --verify archlinux-*версия*-x86_64.iso.sig

```

В качестве альтернативы, можно проверить подпись из установленного Arch Linux:

```
$ pacman-key -v archlinux-*версия*-x86_64.iso.sig

```

**Примечание:**

*   Самой подписью можно манипулировать, если загрузить ее с зеркала, а не с [archlinux.org](https://archlinux.org/download/), как указано выше. В этом случае убедитесь, что открытый ключ, который используется для декодирования подписи, подписан другим надежным ключом. Команда `gpg` выведет fingerprint открытого ключа.
*   Еще один метод проверки подлинности подписи — убедиться, что fingerprint открытого ключа идентичен fingerprint ключа [разработчиков Arch Linux](https://www.archlinux.org/people/developers/), которые подписали ISO-образ. Для получения дополнительной информации о процессе проверки подлинности открытых ключей смотрите [Wikipedia:ru:Криптосистема с открытым ключом](https://en.wikipedia.org/wiki/ru:%D0%9A%D1%80%D0%B8%D0%BF%D1%82%D0%BE%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0_%D1%81_%D0%BE%D1%82%D0%BA%D1%80%D1%8B%D1%82%D1%8B%D0%BC_%D0%BA%D0%BB%D1%8E%D1%87%D0%BE%D0%BC "wikipedia:ru:Криптосистема с открытым ключом").

### Загрузка live-окружения

live-окружение может быть загружено с [USB-накопителя](/index.php/USB_flash_installation_media_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "USB flash installation media (Русский)"), [оптического диска](/index.php/Optical_disc_drive_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Optical disc drive (Русский)") или из сети через [PXE](/index.php/PXE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PXE (Русский)"). Для получения информации о других способах установки смотрите категорию [Category:Installation process (Русский)](/index.php/Category:Installation_process_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Installation process (Русский)").

*   Сделайте установочный носитель с Arch загрузочным. Обычно при включение компьютера нажимается специальная клавиша (иногда она указывается на заставке) во время фазы [POST](https://en.wikipedia.org/wiki/ru:POST_(%D0%B0%D0%BF%D0%BF%D0%B0%D1%80%D0%B0%D1%82%D0%BD%D0%BE%D0%B5_%D0%BE%D0%B1%D0%B5%D1%81%D0%BF%D0%B5%D1%87%D0%B5%D0%BD%D0%B8%D0%B5) для выбора загрузочного устройства. Обратитесь к руководству вашей материнской платы для точных инструкций.
*   Когда появится меню Arch, выберите *Boot Arch Linux* и нажмите `Enter` для входа в установочное окружение.
*   Для получения списка [параметров загрузки](/index.php/Kernel_parameters_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#_Настройка "Kernel parameters (Русский)") смотрите [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams). А для списка включенных пакетов — [packages.x86_64](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64).
*   Вы войдёте в систему от имени суперпользователя в первой [виртуальной консоли](https://en.wikipedia.org/wiki/ru:%D0%92%D0%B8%D1%80%D1%82%D1%83%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F_%D0%BA%D0%BE%D0%BD%D1%81%D0%BE%D0%BB%D1%8C "w:ru:Виртуальная консоль") и увидите перед собой приглашение интерпретатора [Zsh](/index.php/Zsh_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Zsh (Русский)").

Чтобы в процессе установки переключиться на другую виртуальную консоль, например, чтобы посмотреть это руководство при помощи браузера [ELinks](/index.php/ELinks "ELinks"), используйте [горячие клавиши](/index.php/%D0%93%D0%BE%D1%80%D1%8F%D1%87%D0%B8%D0%B5_%D0%BA%D0%BB%D0%B0%D0%B2%D0%B8%D1%88%D0%B8 "Горячие клавиши") `Alt+*стрелка*`. Для [редактирования](/index.php/Help:%D0%A7%D1%82%D0%B5%D0%BD%D0%B8%D0%B5#Добавить,_создать,_редактировать "Help:Чтение") файлов доступны [nano](/index.php/Nano_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Использование "Nano (Русский)"), [vi](https://en.wikipedia.org/wiki/ru:vi "wikipedia:ru:vi") и [vim](/index.php/Vim_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Использование "Vim (Русский)").

### Установка раскладки клавиатуры

По умолчанию используется [раскладка консоли](/index.php/%D0%A0%D0%B0%D1%81%D0%BA%D0%BB%D0%B0%D0%B4%D0%BA%D0%B0_%D0%BA%D0%BE%D0%BD%D1%81%D0%BE%D0%BB%D0%B8 "Раскладка консоли") [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "w:File:KB United States-NoAltGr.svg"). Чтобы посмотреть список доступных раскладок, запустите:

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

Чтобы изменить раскладку, добавьте имя соответствующего файла к команде [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), не указывая полного пути и расширения. Например, чтобы выбрать [русскую](https://en.wikipedia.org/wiki/File:KB_Russian.svg "wikipedia:File:KB Russian.svg") раскладку, запустите:

```
# loadkeys ru

```

[Консольные шрифты](/index.php/Fonts_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Шрифт_в_консоли "Fonts (Русский)") расположены в каталоге `/usr/share/kbd/consolefonts/` и могут быть выбраны при помощи [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### Проверка загруженного режима

Если на материнской плате включён режим [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Unified Extensible Firmware Interface (Русский)"), [Archiso](/index.php/Archiso_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Archiso (Русский)") [загрузит](/index.php/Arch_boot_process "Arch boot process") Arch Linux соответствующим образом при помощи [systemd-boot](/index.php/Systemd-boot_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd-boot (Русский)"). Чтобы убедиться в этом, посмотрите содержимое каталога [efivars](/index.php/Unified_Extensible_Firmware_Interface_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Процесс_загрузки_в_UEFI "Unified Extensible Firmware Interface (Русский)"):

```
# ls /sys/firmware/efi/efivars

```

Если такого каталога не существует, возможно, система загружена в режиме [BIOS](https://en.wikipedia.org/wiki/ru:BIOS "wikipedia:ru:BIOS") или CSM. Для получения дополнительной информации обратитесь к руководству пользователя вашей материнской платы.

### Соединение с Интернетом

Для настройки сетевого соединения, выполните следующие действия:

*   Убедитесь, что ваш [сетевой интерфейс](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8#Сетевые_интерфейсы "Настройка сети") в списке и включён, например, с помощью [ip-link(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-link.8): `# ip link` 
*   Подключитесь к сети. Вставьте кабель Ethernet или [включите беспроводную сеть](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D0%B1%D0%B5%D1%81%D0%BF%D1%80%D0%BE%D0%B2%D0%BE%D0%B4%D0%BD%D0%BE%D0%B9_%D1%81%D0%B5%D1%82%D0%B8 "Настройка беспроводной сети").
*   Настройте ваши сетевые соединения:
    *   [Статический IP-адрес](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8#Статический_IP-адрес "Настройка сети")
    *   Динамический IP-адрес: используя [DHCP](/index.php/DHCP_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "DHCP (Русский)").

    **Примечание:** Установочный образ включает [dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)") (`dhcpcd@*interface*.service`) при загрузке для [проводных сетевых устройств](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules).

*   Соединение может быть проверено с помощью утилиты [ping](https://en.wikipedia.org/wiki/ping "wikipedia:ping"): `# ping archlinux.org` 

### Синхронизация системных часов

Чтобы удостовериться, что время выставлено правильно, используйте [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1):

```
# timedatectl set-ntp true

```

Для проверки статуса службы используйте `timedatectl status`.

### Разметка дисков

Когда запущенная система распознает накопители, они становятся доступны как [блочные устройства](/index.php/Block_device "Block device"), например, `/dev/sda` или `/dev/nvme0n1`. Чтобы посмотреть их список, используйте [lsblk](/index.php/Lsblk "Lsblk") или *fdisk*.

```
# fdisk -l

```

Результаты, оканчивающиеся на `rom`, `loop` и `airoot`, можно игнорировать:

На выбранном накопителе **должны присутствовать** следующие [раздел](/index.php/%D0%A0%D0%B0%D0%B7%D0%B4%D0%B5%D0%BB "Раздел")ы:

*   Раздел для корневого каталога `/`
*   Если включён режим [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Unified Extensible Firmware Interface (Русский)"), необходим [системный раздел EFI](/index.php/%D0%A1%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%BD%D1%8B%D0%B9_%D1%80%D0%B0%D0%B7%D0%B4%D0%B5%D0%BB_EFI "Системный раздел EFI")

Если вы хотите создать составное блочное устройство для [LVM](/index.php/LVM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LVM (Русский)"), [шифрование диска](/index.php/Disk_encryption "Disk encryption") или [RAID](/index.php/RAID "RAID"), сделайте это сейчас.

#### Примеры схем

| BIOS с [MBR](/index.php/MBR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MBR (Русский)") |
| Точка монтирования | Раздел | [Тип раздела](https://en.wikipedia.org/wiki/Partition_type "wikipedia:Partition type") | Рекомендуемый размер |
| `/mnt` | `/dev/sd*X*1` | Linux | Остаток |
| [SWAP] | `/dev/sd*X*2` | Linux swap | Более 512 МБ |
| UEFI с [GPT](/index.php/GPT_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GPT (Русский)") |
| Точка монтирования | Раздел | [Тип раздела](https://en.wikipedia.org/wiki/ru:%D0%A2%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0_%D1%80%D0%B0%D0%B7%D0%B4%D0%B5%D0%BB%D0%BE%D0%B2_GUID#.D0.98.D0.B4.D0.B5.D0.BD.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.D0.BE.D1.80.D1.8B_.28GUID.29_.D1.80.D0.B0.D0.B7.D0.BB.D0.B8.D1.87.D0.BD.D1.8B.D1.85_.D1.82.D0.B8.D0.BF.D0.BE.D0.B2_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2 "wikipedia:ru:Таблица разделов GUID") | Рекомендуемый размер |
| `/mnt/boot` или `/mnt/efi` | `/dev/sd*X*1` | [системный раздел EFI](/index.php/%D0%A1%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%BD%D1%8B%D0%B9_%D1%80%D0%B0%D0%B7%D0%B4%D0%B5%D0%BB_EFI "Системный раздел EFI") | 260–512 МБ |
| `/mnt` | `/dev/sd*X*2` | Linux x86-64 root (/) | Остаток |
| [SWAP] | `/dev/sd*X*3` | Linux swap | Более 512 МБ |

Также смотрите [Разметка дисков#Примеры схем](/index.php/%D0%A0%D0%B0%D0%B7%D0%BC%D0%B5%D1%82%D0%BA%D0%B0_%D0%B4%D0%B8%D1%81%D0%BA%D0%BE%D0%B2#Примеры_схем "Разметка дисков").

**Примечание:**

*   Для редактирования таблицы разделов используйте [fdisk](/index.php/Fdisk_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fdisk (Русский)") или [parted](/index.php/Parted "Parted"), например, `fdisk /dev/sd*X*`.
*   [Пространство подкачки](/index.php/%D0%9F%D1%80%D0%BE%D1%81%D1%82%D1%80%D0%B0%D0%BD%D1%81%D1%82%D0%B2%D0%BE_%D0%BF%D0%BE%D0%B4%D0%BA%D0%B0%D1%87%D0%BA%D0%B8 "Пространство подкачки") можно расположить в [файле](/index.php/Swap_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Файл_подкачки "Swap (Русский)") для файловых систем, поддерживающих его.

### Форматирование разделов

Когда разделы созданы, каждый из них необходимо отформатировать в подходящую [файловую систему](/index.php/%D0%A4%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D0%B5_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B "Файловые системы"). Например, если корневой раздел надо отформатировать в файловую систему `*ext4*` и он обозначен как `/dev/sd*X*1`, выполните:

```
# mkfs.*ext4* /dev/sd*X1*

```

Если вы создали раздел для подкачки, инициализируйте его через утилиту *mkswap*:

```
# mkswap /dev/sd*X2*
# swapon /dev/sd*X2*

```

Для получения дополнительной информации смотрите раздел [Файловые системы#Создание файловой системы](/index.php/%D0%A4%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D0%B5_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B#Создание_файловой_системы "Файловые системы").

### Монтирование разделов

[Смонтируйте](/index.php/%D0%A1%D0%BC%D0%BE%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B9%D1%82%D0%B5 "Смонтируйте") файловую систему корневого раздела в каталог `/mnt`, например:

```
# mount /dev/sd*X1* /mnt

```

Создайте точки монтирования для всех остальных разделов (например, для `/mnt/efi`) и примонтируйте их в соответствующие разделы.

В дальнейшем [genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) обнаружит смонтированные файловые системы и пространство подкачки.

## Установка

### Выбор зеркал

Пакеты для установки должны скачиваться с [серверов-зеркал](/index.php/Mirrors_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mirrors (Русский)"), прописанных в файле `/etc/pacman.d/mirrorlist`. В установочном образе все зеркала включены и отсортированы по статусу синхронизации и скорости в момент создания этого установочного образа.

Чем выше зеркало расположено в этом списке, тем больший приоритет оно имеет при скачивании пакета. Скорее всего, вы захотите отредактировать этот файл, чтобы передвинуть наверх наиболее географически близкие к вам зеркала. При этом также учитывайте и другие критерии.

Позже *pacstrap* скопирует этот файл в новую систему, так что это действительно стоит сделать.

### Установка основных пакетов

Используйте скрипт [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in), чтобы установить пакет [base](https://www.archlinux.org/packages/?name=base), [ядро](/index.php/%D0%AF%D0%B4%D1%80%D0%BE "Ядро") Linux и прошивки часто встречающихся устройств:

```
 # pacstrap /mnt base linux linux-firmware

```

**Совет:** [linux](https://www.archlinux.org/packages/?name=linux) можно заменить на другой желаемый пакет [ядра](/index.php/%D0%AF%D0%B4%D1%80%D0%B0 "Ядра"). Также можно совсем пропустить установку ядра или прошивок, если вы знаете, что делаете.

Пакет [base](https://www.archlinux.org/packages/?name=base) не содержит все инструменты, имеющиеся на установочном носителе, из-за чего может потребоваться установка других пакетов для получения полностью функциональной базовой системы. В частности, рассмотрите возможность установки следующего программного обеспечения:

*   утилиты для управления [файловыми системами](/index.php/File_systems_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "File systems (Русский)") в пользовательском пространстве, которые будут использоваться в системе
*   утилиты для доступа к [RAID](/index.php/RAID "RAID")- или [LVM](/index.php/LVM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LVM (Русский)")-разделам
*   специфические прошивки других устройств, не включённых в [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware)
*   ПО, необходимое для [организации сети](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Network configuration (Русский)")
*   [текстовый редактор](/index.php/%D0%A2%D0%B5%D0%BA%D1%81%D1%82%D0%BE%D0%B2%D1%8B%D0%B9_%D1%80%D0%B5%D0%B4%D0%B0%D0%BA%D1%82%D0%BE%D1%80 "Текстовый редактор")
*   пакеты для доступа к документации в [man](/index.php/Man_page_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Man page (Русский)") и [info](/index.php/Info "Info"): [man-db](https://www.archlinux.org/packages/?name=man-db), [man-pages](https://www.archlinux.org/packages/?name=man-pages) и [texinfo](https://www.archlinux.org/packages/?name=texinfo)

Чтобы [установить](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C "Установить") другие пакеты или группы, добавьте их названия к команде *pacstrap* (разделяя их пробелом) или используйте [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") после шага [#Chroot](#Chroot). Список пакетов на установочном носителе доступен на странице [packages.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64).

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

Задайте [часовой пояс](/index.php/%D0%92%D1%80%D0%B5%D0%BC%D1%8F#Часовой_пояс "Время"):

```
# ln -sf /usr/share/zoneinfo/*Регион*/*Город* /etc/localtime

```

Запустите [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8), чтобы сгенерировать `/etc/adjtime`:

```
# hwclock --systohc

```

Эта команда предполагает, что аппаратные часы настроены в формате [UTC](https://en.wikipedia.org/wiki/ru:%D0%92%D1%81%D0%B5%D0%BC%D0%B8%D1%80%D0%BD%D0%BE%D0%B5_%D0%BA%D0%BE%D0%BE%D1%80%D0%B4%D0%B8%D0%BD%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D0%B5_%D0%B2%D1%80%D0%B5%D0%BC%D1%8F "w:ru:Всемирное координированное время"). Для получения дополнительной информации смотрите раздел [Время#Стандарты времени](/index.php/%D0%92%D1%80%D0%B5%D0%BC%D1%8F#Стандарты_времени "Время").

### Локализация

Включите `en_US.UTF-8 UTF-8` и другие необходимые [локали](/index.php/%D0%9B%D0%BE%D0%BA%D0%B0%D0%BB%D0%B8 "Локали") (например, `ru_RU.UTF-8 UTF-8`), раскомментировав их в файле `/etc/locale.gen`, после чего сгенерируйте их:

```
# locale-gen

```

Создайте файл [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) и задайте необходимое значение в нем для [переменной](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `LANG`:

 `/etc/locale.conf`  `LANG=*ru_RU.UTF-8*` 

Если вы [меняли раскладку клавиатуры](#Установка_раскладки_клавиатуры), сделайте это изменение постоянным в файле [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5). Также добавьте шрифт для консоли с поддержкой кириллицы:

 `/etc/vconsole.conf` 
```
KEYMAP=*ru*
FONT=cyr-sun16
```

### Настройка сети

Создайте файл [hostname](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_имени_хоста "Network configuration (Русский)"):

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

Завершите [настройку сети](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Network configuration (Русский)") для вновь установленной среды, что включает в себя [установку](/index.php/Help:Reading_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_пакетов "Help:Reading (Русский)") [iputils](https://www.archlinux.org/packages/?name=iputils) и предпочитаемого ПО для [управления сетевым подключением](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Управление_сетевым_подключением "Network configuration (Русский)").

### Initramfs

Как правило, создание нового образа *initramfs* не требуется, поскольку *pacstrap* автоматически запускает [mkinitcpio](/index.php/Mkinitcpio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mkinitcpio (Русский)") после установки пакета [ядра](/index.php/%D0%AF%D0%B4%D1%80%D0%B0 "Ядра").

Если вы используете [LVM](/index.php/LVM#Configure_mkinitcpio "LVM"), [системное шифрование](/index.php/Dm-crypt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dm-crypt (Русский)") или [RAID](/index.php/RAID#Configure_mkinitcpio "RAID"), отредактируйте файл [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) и пересоздайте образ *initramfs*:

```
# mkinitcpio -p linux

```

### Пароль суперпользователя

Установите [пароль](/index.php/Users_and_groups_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Управление_пользователями "Users and groups (Русский)") суперпользователя:

```
# passwd

```

### Загрузчик

Выберите и установите [загрузчик](/index.php/%D0%97%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D1%87%D0%B8%D0%BA "Загрузчик") с поддержкой Linux. Если вы используете процессор Intel или AMD, включите также обновление [микрокода](/index.php/%D0%9C%D0%B8%D0%BA%D1%80%D0%BE%D0%BA%D0%BE%D0%B4 "Микрокод").

## Перезагрузка

Выйдите из окружения chroot, набрав `exit` или нажав `Ctrl+D`.

Вы можете размонтировать все разделы с помощью команды `umount -R /mnt`, чтобы убедиться в том, что ни один из разделов не остался занят какой-либо программой. Если нужно, для поиска таких программ используйте [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Теперь перезагрузите компьютер, набрав `reboot`: если какие-нибудь разделы остались смонтированными, [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") их размонтирует. Не забудьте извлечь установочный диск. После загрузки войдите в систему в качестве суперпользователя.

## После установки

Дальнейшие указания по настройке системы после установки (например, по настройке графического интерфейса, звука или тачпада) вы можете найти на странице [Основные рекомендации](/index.php/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D0%BD%D1%8B%D0%B5_%D1%80%D0%B5%D0%BA%D0%BE%D0%BC%D0%B5%D0%BD%D0%B4%D0%B0%D1%86%D0%B8%D0%B8 "Основные рекомендации").

Множество интересных и полезных программ вы найдете на странице [Список приложений](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9 "Список приложений").