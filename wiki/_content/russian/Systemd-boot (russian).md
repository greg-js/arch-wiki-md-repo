Ссылки по теме

*   [Arch boot process (Русский)](/index.php/Arch_boot_process_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch boot process (Русский)")
*   [Загрузчики](/index.php/%D0%97%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D1%87%D0%B8%D0%BA%D0%B8 "Загрузчики")
*   [Unified Extensible Firmware Interface (Русский)](/index.php/Unified_Extensible_Firmware_Interface_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Unified Extensible Firmware Interface (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). Дата последней синхронизации: 2016-01-22\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Systemd-boot&diff=0&oldid=416510).

**systemd-boot**, ранее известный как **gummiboot** - это простой UEFI менеджер загрузки, который исполняет настроенные EFI образы. Запись по умолчанию выбирается с помощью настроенного шаблона (glob) или меню на экране. Включен в пакет [systemd](https://www.archlinux.org/packages/?name=systemd), который устанавливается на системе Arch по умолчанию.

Прост в настройке, но способен только на запуск исполняемых EFI файлов, таких как ядро Linux [EFISTUB](/index.php/EFISTUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "EFISTUB (Русский)"), UEFI Shell, GRUB, Windows Boot Manager.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Загрузка в режиме EFI](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.B2_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5_EFI)
    *   [1.2 Загрузка в режиме BIOS](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.B2_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5_BIOS)
    *   [1.3 Обновлениe](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8e)
        *   [1.3.1 Вручную](#.D0.92.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
        *   [1.3.2 Автоматически](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Базовая настройка](#.D0.91.D0.B0.D0.B7.D0.BE.D0.B2.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.2 Добавление загрузочных записей](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BE.D1.87.D0.BD.D1.8B.D1.85_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D0.B5.D0.B9)
        *   [2.2.1 Установки со стандартной корневой директорией](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8_.D1.81.D0.BE_.D1.81.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D0.BD.D0.BE.D0.B9_.D0.BA.D0.BE.D1.80.D0.BD.D0.B5.D0.B2.D0.BE.D0.B9_.D0.B4.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B5.D0.B9)
        *   [2.2.2 Установки с LVM корневой директорией](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8_.D1.81_LVM_.D0.BA.D0.BE.D1.80.D0.BD.D0.B5.D0.B2.D0.BE.D0.B9_.D0.B4.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B5.D0.B9)
        *   [2.2.3 Установки с зашифрованной корневой директорией](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8_.D1.81_.D0.B7.D0.B0.D1.88.D0.B8.D1.84.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.BD.D0.BE.D0.B9_.D0.BA.D0.BE.D1.80.D0.BD.D0.B5.D0.B2.D0.BE.D0.B9_.D0.B4.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B5.D0.B9)
        *   [2.2.4 Установка корневого подраздела btrfs](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BA.D0.BE.D1.80.D0.BD.D0.B5.D0.B2.D0.BE.D0.B3.D0.BE_.D0.BF.D0.BE.D0.B4.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B0_btrfs)
        *   [2.2.5 Установки с ZFS корневой директорией](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8_.D1.81_ZFS_.D0.BA.D0.BE.D1.80.D0.BD.D0.B5.D0.B2.D0.BE.D0.B9_.D0.B4.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B5.D0.B9)
        *   [2.2.6 EFI Shells или другие EFI приложения](#EFI_Shells_.D0.B8.D0.BB.D0.B8_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D0.B5_EFI_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [2.3 Дополнительная безопасность](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.B1.D0.B5.D0.B7.D0.BE.D0.BF.D0.B0.D1.81.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
    *   [2.4 Поддержка гибернации](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_.D0.B3.D0.B8.D0.B1.D0.B5.D1.80.D0.BD.D0.B0.D1.86.D0.B8.D0.B8)
*   [3 Клавиши в загрузочном меню](#.D0.9A.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_.D0.B2_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BE.D1.87.D0.BD.D0.BE.D0.BC_.D0.BC.D0.B5.D0.BD.D1.8E)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Создание записи вручную с помощью efibootmgr](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D0.B8_.D0.B2.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_efibootmgr)
    *   [4.2 Меню не отображается после обновления Windows](#.D0.9C.D0.B5.D0.BD.D1.8E_.D0.BD.D0.B5_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_Windows)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

### Загрузка в режиме EFI

1.  Убедитесь, что вы загружены в режиме UEFI.
2.  Проверьте [доступны ли EFI переменные](/index.php/Unified_Extensible_Firmware_Interface#Requirements_for_UEFI_variable_support "Unified Extensible Firmware Interface").
3.  Корректно примонтируйте [Системный Раздел EFI](/index.php/EFI_System_Partition "EFI System Partition") (ESP). В этой статье `*esp*` используется для обозначения точки монтирования.
    **Примечание:** *systemd-boot* EFI не может загружать бинарные файлы из других разделов. По этой причине, рекомендуется монтировать ваш ESP в `/boot`. В случае, если вы хотите разделить `/boot` с ESP, обратитесь к [#Обновления](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F) для большей информации.

4.  Если ESP **не** примонтирован к `/boot`, копируйте ваше ядро и initramfs в ESP.
    **Примечание:** Чтобы сохранить автоматическое обновление ядра в ESP, взгляните на [EFISTUB#Using systemd](/index.php/EFISTUB#Using_systemd "EFISTUB") для адаптации некоторых юнитов systemd. Если ваш Системный Раздел EFI монтируется автоматически, вам, вероятно, потребуется добавить `vfat` в файл внутри `/etc/modules-load.d/`. Тогда в текущем запущенном ядре во время загрузки будет установлен модуль `vfat`, до того, как произойдет обновление ядра, которое может заменить модуль для текущей версии, что сделает невозможным монтирование `/boot/efi` до перезагрузки.

5.  Введите следующую команду для установки *systemd-boot*: `# bootctl --path=*esp* install` Она скопирует двоичный файл *systemd-boot* на Системный Раздел EFI (`*esp*/EFI/systemd/systemd-bootx64.efi` и `*esp*/EFI/Boot/BOOTX64.EFI` - оба идентичны на x86-64 системах) и добавит *systemd-boot* как EFI приложение по умолчанию (загрузочная запись по умолчанию), загружаемое с помощью EFI Boot Manager.
6.  Наконец, для правильного функционирования вы должны [настроить](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0) загрузчик.

### Загрузка в режиме BIOS

**Важно:** Это нерекомендованный процесс

Вы с таким же успехом можете установить systemd-boot, если загружаетесь в режиме BIOS. Тем не менее, от вас всё равно требуется сообщить прошивке запускать EFI файл *systemd-boot* при загрузке:

*   у вас есть работающий EFI shell где-нибудь.
*   ваш интерфейс прошивки предоставляет вам соответствующий способ настройки EFI файла, который будет загружен во время загрузки.

Если вы имеете такую возможность, процесс установки будет проще: перейдите в ваш EFI shell или интерфейс настройки вашей прошивки и измените EFI файл по умолчанию вашей машины на `esp/EFI/systemd/systemd-bootx64.efi` ( или `systemd-bootia32.efi` если у вас 32 битная системная прошивка).

**Примечание:** интерфейс прошивки в Dell Latitude сериях предоставляет все необходимое, чтобы установить EFI загрузку, но EFI Shell не сможет осуществить запись в ПЗУ компьютера.

### Обновлениe

В отличие от предыдущего отдельного пакета *gummiboot*, который автоматически обновляется с помощью `post_install` скрипта, обновления systemd-boot теперь должны производиться пользователем вручную. Однако, эта процедура может быть автоматизирована с использованием pacman hooks.

#### Вручную

*systemd-boot* (bootctl(1)) предполагает, что ваш Системный Раздел EFI примонтирован в `/boot`.

```
# bootctl update

```

Если ESP не примонтирован в `/boot`, опцией `--path=` можно явно указать точку монтирования, например:

```
# bootctl --path=*esp* update

```

**Примечание:** Также эту команду следует использовать при переходе с *gummiboot*, перед удалением этого пакета. Однако, если этот пакет уже был удален, выполните `bootctl --path=*esp* install`.

#### Автоматически

[AUR (Русский)](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") пакет [systemd-boot-pacman-hook](https://aur.archlinux.org/packages/systemd-boot-pacman-hook/) предоставляет [Pacman hook](/index.php/Pacman#Hooks "Pacman") для автоматизации процесса обновления. [Установка](/index.php/Install "Install") этого пакета добавит hook, который будет выполняться при каждом обновлении пакета [systemd](https://www.archlinux.org/packages/?name=systemd).

В качестве альтернативы, вы можете разместить следующий pacman hook в каталоге /etc/pacman.d/hooks/:

Alternatively, place the following pacman hook in the /etc/pacman.d/hooks/ directory:

 `/etc/pacman.d/hooks/systemd-boot.hook` 
```
[Trigger]
Type = Package
Operation = Upgrade
Target = systemd

[Action]
Description = Updating systemd-boot...
When = PostTransaction
Exec = /usr/bin/bootctl update
```

## Настройка

### Базовая настройка

Базовая конфигурация хранится в файле `*esp*/loader/loader.conf` и состоит из трех опций:

*   `default` – выбираемая по умолчанию запись (без суффикса `.conf`); можно использовать подстановку, например `arch-*`

*   `timeout` – задержка меню в секундах. Если таймаут не задан, то меню будет отображаться, только если удерживать клавишу `Space` (другие клавиши тоже могут работать) при загрузке.

*   `editor` - следует ли включить редактор параметров ядра. `1` (по умолчанию) - включить, `0` - отключить; Поскольку пользователь может добавить `init=/bin/bash` для обхода пароля администратора и получить полный доступ, настоятельно рекомендуется установить эту опцию в `0`.

Пример:

 `*esp*/loader/loader.conf` 
```
default  arch
timeout  4
editor   0

```

**Примечание:** Обратите внимание, что первые 2 опции могут быть изменены в самом меню загрузки, эти изменения будут храниться как переменные EFI.

**Совет:** Пример базового конфигурационного файла расположен как `/usr/share/systemd/bootctl/loader.conf`.

### Добавление загрузочных записей

**Примечание:**

*   *bootctl* будет автоматически проверять наличие "**Windows Boot Manager**" (`\EFI\Microsoft\Boot\Bootmgfw.efi`), "**EFI Shell**" (`\shellx64.efi`) и "**EFI Default Loader**" (`\EFI\Boot\bootx64.efi`) во время загрузки, так же как специально подготовленные файлы ядра, найденные в `\EFI\Linux`. После обнаружения соответствующие записи с заголовками `auto-windows`, `auto-efi-shell` и `auto-efi-default` будут автоматически сгенерированы. Эти записи не требуют ручной настройки загрузчика. Однако, другие EFI приложения не будут обнаружены автоматически (не в случае с [rEFInd (Русский)](/index.php/REFInd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "REFInd (Русский)")), поэтому для зарузки ядра Linux, записи должны быть созданы вручную.
*   Если вы используете двойную загрузку с Windows, настоятельно рекомендуется отключить [Быстрый запуск](/index.php/Dual_boot_with_Windows_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.91.D1.8B.D1.81.D1.82.D1.80.D1.8B.D0.B9_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA "Dual boot with Windows (Русский)")
*   Не забудте загрузить intel [microcode](/index.php/Microcode "Microcode") с `initrd` если это применимо в вашем случае.
*   Вы можете узнать PARTUUID вашего корневого раздела с помощью команды `blkid -s PARTUUID -o value /dev/sd*xY*`, где `*x*` - это буква устройства, а `*Y*` - это номер раздела. Это нужно только для вашего корневого раздела, не для `*esp*`.

*bootctl* ищет элементы для загрузочного меню в `*esp*/loader/entries/*.conf` – каждый найденный файл должен содержать точно одну загрузочную запись. Возможными опциями являются:

*   `title` – название операционной системы. **Обязательная.**

*   `version` – версия ядра, отображаемая только если существуют несколько записей с одинаковым названием. Не обязательная.

*   `machine-id` – идентификатор машины из `/etc/machine-id`, отображаемый только если существуют несколько записей с одинаковым названием и одинаковой версией. Не обязательная.

*   `efi` – EFI программа для запуска, относительно вашего ESP (`$esp`); например, `/vmlinuz-linux`. Либо это, либо `linux` (смотрите ниже) является **обязательным.**

*   `options` – опции командной строки для передачи EFI приложению. Не обязательная, но вам нужно будет передать как минимум `initrd=*efipath*` и `root=*dev*` если загружаете Linux.

Для Linux вы можете задать `linux *path-to-vmlinuz*` и `initrd *path-to-initramfs*`; это автоматически преобразуется в `efi *path*` и `options initrd=*path*` – этот синтаксис поддерживается только для удобства и не имеет различий по функциональности.

#### Установки со стандартной корневой директорией

Вот пример записи для корневого раздела без LVM или LUKS:

 `*esp*/loader/entries/arch.conf` 
```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=PARTUUID=14420948-2cea-4de7-b042-40f67c618660 rw
```

Пожалуйста, обратите внимание, что в вышеприведённом примере `PARTUUID`/`PARTLABEL` идентифицируют GPT раздел, а это не то же самое, что UUID/LABEL, которые идентифицируют файловую систему. Использование `PARTUUID`/`PARTLABEL` бывает полезным, потому что они инвариантны (то есть неизменяемы), если вы переформатируете раздел в другую файловую систему или если по какой-то причине изменятся обозначения /dev/sd*. Также оно может быть полезно, если у вас нет файловой системы на разделе (или вы используете LUKS, который не поддерживает метки `LABEL`).

**Совет:** Пример файла записи расположен как `/usr/share/systemd/bootctl`.

#### Установки с LVM корневой директорией

**Важно:** *systemd-boot* не может использоваться без отдельной `/boot` файловой системы вне LVM.

Вот пример для корневой директории, использующей [логический менеджер разделов](/index.php/LVM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LVM (Русский)"):

 `*esp*/loader/entries/arch-lvm.conf` 
```
title          Arch Linux (LVM)
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=/dev/mapper/<VolumeGroup-LogicalVolume> rw
```

Замените `<VolumeGroup-LogicalVolume>` на актуальные названия VG и LV (например, `root=/dev/mapper/volgroup00-lvolroot`). Кроме того, вместо них можно использовать UUID:

```
....
options  root=UUID=<UUID identifier> rw

```

Обратите внимание, что `root=**UUID**=` используется вместо `root=**PARTUUID**=`, который используется для корневых разделов без LVM или LUKS.

#### Установки с зашифрованной корневой директорией

Ниже приведен пример конфигурационного файла для зашифрованного корневого раздела ([DM-Crypt / LUKS](/index.php/Dm-crypt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dm-crypt (Русский)")) с использованием `encrypt` [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") hook:

 `*esp*/loader/entries/arch-encrypted.conf` 
```
title Arch Linux Encrypted
linux /vmlinuz-linux
initrd /initramfs-linux.img
options cryptdevice=UUID=<UUID>:<mapped-name> root=/dev/mapper/<mapped-name> quiet rw
```

В этом примере используется UUID; если хотите, можете заменить UUID на `PARTUUID`. Вы можете также заменить `/dev` путь на регулярный UUID. `mapped-name` - название, которое вы желаете использовать. See [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration").

Если вы используете LVM, ваша опция cryptdevice будет выглядеть следующим образом:

 `*esp*/loader/entries/arch-encrypted-lvm.conf` 
```
title Arch Linux Encrypted LVM
linux /vmlinuz-linux
initrd /initramfs-linux.img
options cryptdevice=UUID=<UUID>:MyVolGroup root=/dev/mapper/MyVolGroup-MyVolRoot quiet rw
```

Вы также можете добавить другие EFI приложения, такие как `\EFI\arch\grub.efi`.

#### Установка корневого подраздела btrfs

При загрузке с подраздела [btrfs](/index.php/Btrfs "Btrfs") как корневого, замените `options` строку на `rootflags=subvol=<root subvolume>`. В примере ниже, корневой раздел монтируется как btrfs подраздел с именем 'ROOT' (например, `mount -o subvol=ROOT /dev/sdxY /mnt`):

 `*esp*/loader/entries/arch-btrfs-subvol.conf` 
```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=PARTUUID=14420948-2cea-4de7-b042-40f67c618660 rw rootflags=subvol=ROOT
```

Если это невозможно сделать, то это приведет к ошибке: `ERROR: Root device mounted successfully, but /sbin/init does not exist.`

#### Установки с ZFS корневой директорией

В случае загрузки из [ZFS](/index.php/ZFS "ZFS") dataset, добавьте `zfs=<root dataset>` к строке `options`. Здесь в корневом dataset установлено значение 'zroot/ROOT/default':

 `*esp*/loader/entries/arch-zfs.conf` 
```
title          Arch Linux ZFS
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        zfs=zroot/ROOT/default rw
```

When booting off of a ZFS dataset ensure that it has had the `bootfs` property set with `zpool set bootfs=<root dataset> <zpool>`.

#### EFI Shells или другие EFI приложения

В случае, если вы установили EEFI Shells или другие EFI приложения в ESP, вы можете использовать следующие фрагменты:

 `*esp*/loader/entries/uefi-shell-v1-x86_64.conf` 
```
title  UEFI Shell x86_64 v1
efi    /EFI/shellx64_v1.efi
```
 `*esp*/loader/entries/uefi-shell-v2-x86_64.conf` 
```
title  UEFI Shell x86_64 v2
efi    /EFI/shellx64_v2.efi
```

### Дополнительная безопасность

Вы должны знать, что параметры командной строки для ядра могут быть отредактированы с помощью меню загрузки systemd-boot'а (смотрите [#Клавиши в загрузочном меню](#.D0.9A.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_.D0.B2_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BE.D1.87.D0.BD.D0.BE.D0.BC_.D0.BC.D0.B5.D0.BD.D1.8E)) при нажатии `e`. Это главная дыра в безопасности, так как если вы переопределите аргумент ядра `init=`, например на `init=/bin/bash`, это загрузит вашу машину непосредственно с правами root без каких либо паролей, легко обходя существующий пароль root'а! Поскольку gummiboot в настоящий момент не имеет функциии защиты паролем и не имеет возможности предотвратить изменения параметров ядра, вы должны убедиться в том, что вы задали пароль на аппаратном уровне (UEFI/BIOS), который предотвратит загрузку компьютера до того, как введён правильный пароль.

Поскольку безопасность состоит из нескольких уровней, а физический доступ сразу же обходит любые системы безопасности, возможно вам пригодится шифрование вашего диска с помощью [dm-crypt](/index.php/Dm-crypt "Dm-crypt"), особенно если ваша машина является ноутбуком. Однако, это уже другой вопрос, не относящийся к systemd-boot.

### Поддержка гибернации

Пожалуйста, прочтите статью [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

## Клавиши в загрузочном меню

В меню используются следующие клавиши:

*   `Вверх/Вниз` - выбор записи
*   `Enter` - загрузить выбранную запись
*   `d` - выбрать загрузочную запись по умолчанию (хранится в энергонезависимой EFI переменной)
*   `-/T` - уменьшить таймаут (хранится в энергонезависимой EFI переменной)
*   `+/t` - увеличить таймаут (хранится в энергонезависимой EFI переменной)
*   `e` - редактировать командную строку ядра
*   `v` - показать версию gummiboot и UEFI
*   `Q` - выйти
*   `P` - отобразить текущую конфигурацию
*   `h/?` - помощь

А эти клавиши, нажатые в меню в процессе загрузки, сразу загрузят определённую запись:

*   `l` - Linux
*   `w` - Windows
*   `a` - OS X
*   `s` - EFI Shell
*   `1-9` - порядковый номер записи

## Решение проблем

### Создание записи вручную с помощью efibootmgr

Если команда `bootctl install` не сработала, вы можете создать загрузочную EFI запись самостоятельно с помощью утилиты `efibootmgr`:

```
# efibootmgr -c -d /dev/sdX -p Y -l /EFI/systemd/systemd-bootx64.efi -L "Linux Boot Manager"

```

где `/dev/sdXY` - это ваш EFISYS раздел.

### Меню не отображается после обновления Windows

Допустим, если вы обновились с Windows 8 до Windows 8.1 и вы больше не видите загрузочного меню после этого обновления, (то есть сразу грузится Windows):

*   Убедитесь, что как Secure Boot (настраивается в UEFI), так и Fast Startup (настраивается в опциях питания в Windows) отключены.
*   Убедитесь, что в вашем UEFI Linux Boot Manager первичнее, чем Windows Boot Manager (настраивается в UEFI настройках, таких как Hard Disk Drive Priority).

**Примечание:** Windows 8.x+, включая Windows 10, будут перезаписывать любой выбор порядка загрузки, который вы делаете и устанавливать себя в качестве приоритетной загрузки после каждого запуска. Изменение порядка загрузки в прошивке UEFI продлится только до следующей Windows 10 загрузки. Вы должны знать *Change Boot Option* ключ для вашей материнской платы.

Для того, чтобы Windows 8.X не изменяли порядок загрузки, вы должны настроить групповые политики для Windows и выполнить скрипт (*.bat*) при запуске. В Windows:

1.  Откройте командную строку с правами администратора. Выполните `bcdedit /enum firmware`
2.  Найдите приложение, в котором в описании "Linux", например "Linux Boot Manager"
3.  Скопируйте ID, включая скобки, например `{31d0d5f4-22ad-11e5-b30b-806e6f6e6963}`.
4.  Создайте bat-файл (например, `bootorder.bat`) со следующим содержанием: `bcdedit /set {fwbootmgr} DEFAULT {*скопированный_ID*}` (например, `bcdedit /set {fwbootmgr} DEFAULT {31d0d5f4-22ad-11e5-b30b-806e6f6e6963}`).
5.  Откройте *gpedit* и в *Local Computer Policy > Computer Configuration > Windows Settings > Scripts(Startup/Shutdown)*, выберите *Startup*. Должно открыться окно с заголовком *Startup Properties*.
6.  Во вкладке *Scripts*, нажмите кнопку *Add*
7.  Нажмите *Browse* и выберите созданный bat-файл.

## Смотрите также

*   [http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/](http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/)