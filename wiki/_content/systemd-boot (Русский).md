# systemd-boot (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Ссылки по теме

*   [Arch boot process (Русский)](/index.php/Arch_boot_process_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch boot process (Русский)")
*   [Загрузчики](/index.php/%D0%97%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D1%87%D0%B8%D0%BA%D0%B8 "Загрузчики")
*   [Unified Extensible Firmware Interface (Русский)](/index.php/Unified_Extensible_Firmware_Interface_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Unified Extensible Firmware Interface (Русский)")

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

**Состояние перевода:** На этой странице представлен перевод статьи [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). Дата последней синхронизации: 2016-01-22\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Systemd-boot&diff=0&oldid=416510).

**systemd-boot** (ранее назывался **gummiboot**) - это простой UEFI менеджер загрузки, который запускает настроенные EFI образы. Записью по умолчанию является настроенный паттерн (glob) или меню на экране. Включен в systemd с версии [systemd](https://www.archlinux.org/packages/?name=systemd) 220-2.

Его легко настраивать, но от умеет только запускать исполняемые EFI файлы, ядро Linux [EFISTUB](/index.php/EFISTUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "EFISTUB (Русский)"), UEFI Shell, grub.efi, Windows Boot Manager и тому подобные.

**Важно:** systemd-boot всего лишь предоставляет меню для загрузки EFISTUB ядер. В случае, если у вас возникают проблемы с загрузкой EFISTUB ядер, как в [FS#33745](https://bugs.archlinux.org/task/33745), вы можете использовать загрузчик, который не использует EFISTUB, например [GRUB (Русский)](/index.php/GRUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB (Русский)"), [Syslinux (Русский)](/index.php/Syslinux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Syslinux (Русский)") или [ELILO](/index.php/%D0%97%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D1%87%D0%B8%D0%BA%D0%B8#ELILO "Загрузчики").

**Обратите внимание:** В этой статье точку монтирования [Системного Раздела EFI](/index.php/UEFI#EFI_System_Partition "UEFI") (также известного как ESP) будем обозначать как `$esp`.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Загрузка в режиме EFI](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.B2_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5_EFI)
    *   [1.2 Загрузка в режиме Legacy](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.B2_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5_Legacy)
    *   [1.3 Обновления](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Базовая настройка](#.D0.91.D0.B0.D0.B7.D0.BE.D0.B2.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.2 Добавление загрузочных записей](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BE.D1.87.D0.BD.D1.8B.D1.85_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D0.B5.D0.B9)
        *   [2.2.1 Установки со стандартной корневой директорией](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8_.D1.81.D0.BE_.D1.81.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D0.BD.D0.BE.D0.B9_.D0.BA.D0.BE.D1.80.D0.BD.D0.B5.D0.B2.D0.BE.D0.B9_.D0.B4.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B5.D0.B9)
        *   [2.2.2 Установки с LVM корневой директорией](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8_.D1.81_LVM_.D0.BA.D0.BE.D1.80.D0.BD.D0.B5.D0.B2.D0.BE.D0.B9_.D0.B4.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B5.D0.B9)
        *   [2.2.3 Установки с зашифрованной корневой директорией](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8_.D1.81_.D0.B7.D0.B0.D1.88.D0.B8.D1.84.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.BD.D0.BE.D0.B9_.D0.BA.D0.BE.D1.80.D0.BD.D0.B5.D0.B2.D0.BE.D0.B9_.D0.B4.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B5.D0.B9)
        *   [2.2.4 Установка корневого подраздела btrfs](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BA.D0.BE.D1.80.D0.BD.D0.B5.D0.B2.D0.BE.D0.B3.D0.BE_.D0.BF.D0.BE.D0.B4.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B0_btrfs)
        *   [2.2.5 EFI Shells или другие EFI приложения](#EFI_Shells_.D0.B8.D0.BB.D0.B8_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D0.B5_EFI_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [2.3 Дополнительная безопасность](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.B1.D0.B5.D0.B7.D0.BE.D0.BF.D0.B0.D1.81.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
    *   [2.4 Поддержка гибернации](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_.D0.B3.D0.B8.D0.B1.D0.B5.D1.80.D0.BD.D0.B0.D1.86.D0.B8.D0.B8)
*   [3 Клавиши в загрузочном меню](#.D0.9A.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_.D0.B2_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BE.D1.87.D0.BD.D0.BE.D0.BC_.D0.BC.D0.B5.D0.BD.D1.8E)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Создание записи вручную с помощью efibootmgr](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D0.B8_.D0.B2.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_efibootmgr)
    *   [4.2 Меню не отображается после обновления Windows](#.D0.9C.D0.B5.D0.BD.D1.8E_.D0.BD.D0.B5_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_Windows)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

### Загрузка в режиме EFI

1.  Для начала убедитесь, что вы загружены в режиме UEFI
2.  Проверьте [есть доступ к вашим переменным EFI](/index.php/UEFI#Requirements_for_UEFI_Variables_support_to_work_properly "UEFI")
3.  Убедитесь, что ваш Системный Раздел EFI правильно примонтирован. `$esp` используется для обозначения точки монтирования в этой статье.

    **Обратите внимание:** systemd-boot не умеет загружать EFI приложения из других разделов. Поэтому настоятельно рекомендуется монтировать ваш ESP в `/boot`. Смотрите [#Обновления](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F) для более подробной информации или если вы хотите отделить `/boot` от ESP.

4.  Скопируйте ваше ядро и initramfs на этот раздел.

    **Обратите внимание:** Для того, что-бы автоматически держать ядро обновленным в ESP, смотрите [EFISTUB](/index.php/EFISTUB#Using_systemd "EFISTUB") для использования предназначенных для этого юнитов systemd.

5.  Наконец, введите следующую команду для установки systemd-boot: `# bootctl --path=_$esp_ install` Она скопирует образ systemd-boot на Системный Раздел EFI (`$esp/EFI/systemd/systemd-bootx64.efi` и `$esp/EFI/Boot/BOOTX64.EFI` - оба идентичны - на x64 системах) и добавьте systemd-boot как приложение EFI для загрузки по умолчанию.

### Загрузка в режиме Legacy

**Обратите внимание:** Это нерекомендованный процесс

Вы с таким же успехом можете установить systemd-boot, если загружаетесь в режиме legacy OS. Тем не менее, от вас всё равно требуется позже сказать прошивке запускать EFI файл systemd-boot'а при загрузке:

*   у вас есть работающие EFI shell где-нибудь;
*   ваш интерфейс прошивки предоставляет вам способ правильной настройки EFI файла, который будет загружен во время загрузки.

**Обратите внимание:** Например, это возможно на Dell Latitude сериях, так как EFI Shell не может записывать в ПЗУ компьютера.

Если вы можете это сделать, то установка проще: перейдите в ваш EFI shell или в ваш интерфейс настройки прошивки и измените EFI файл по умолчанию вашей машины на `$esp/EFI/systemd/systemd-bootx64.efi`(`systemd-bootia32.efi` на i686 системах).

### Обновления

systemd-boot (bootctl(1), systemd-efi-boot-generator(8)) подразумевает, что ваша ESP смонтирована в `/boot`. В отличие от предыдущего пакета _gummiboot_, который автоматически обновляется с помощью `post_install` скрипта, обновления systemd-boot теперь обрабатываются пользователем вручную:

```
# bootctl update  

```

Если ESP не смонтирован на `/boot`, опция `--path=` может передать его, например:

```
# bootctl --path=/boot/$esp update

```

## Настройка

### Базовая настройка

Базовая конфигурация хранится в `$esp/loader/loader.conf`, в которой доступно всего три опции:

*   `default` – выбираемая по умолчанию запись (без суффикса `.conf`); может быть звёздочкой, например `arch-*`

*   `timeout` – задержка меню в секундах. Если таймаут не задан, то меню будет отображаться только если удерживать клавишу пробел при загрузке.

*   `editor` - следует ли включить редактор параметров ядра или нет. `1` (по умолчанию) - включить, `0` - отключить. Пользователь может добавить `init=/bin/bash` что-бы обойти пароль администратора и получить полный доступ, поэтому настоятельно рекомендуется установить этот параметр в `0`.

Пример:

 `$esp/loader/loader.conf` 

```
default  arch
timeout  4
editor   0

```

Обратите внимание, что первые 2 опции могут быть изменены в самом меню загрузки, которое будет хранить их как переменные EFI.

**Обратите внимание:** Если таймаут не настроен, что является настройкой по умолчанию и не нажата клавиша при загрузке, опция по умолчанию выполняется сразу же.

### Добавление загрузочных записей

**Обратите внимание:** bootctl будет автоматически проверять наличие "**Windows Boot Manager**" (`\EFI\Microsoft\Boot\Bootmgfw.efi`), "**EFI Shell**" (`\shellx64.efi`) и "**EFI Default Loader**" (`\EFI\Boot\bootx64.efi`). Для тех, что будут найдены, записи также будут автоматически сгенерированы. Тем не менее, он не будет автоматически искать другие EFI приложения (в отличие от [rEFInd (Русский)](/index.php/REFInd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "REFInd (Русский)")), поэтому для загрузки ядра записи должны быть созданы вручную. Если вы используете двойную загрузку с Windows, настоятельно рекомендуется отключить [Быстрый запуск](/index.php/Dual_boot_with_Windows_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.91.D1.8B.D1.81.D1.82.D1.80.D1.8B.D0.B9_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA "Dual boot with Windows (Русский)")

**Совет:** Вы можете узнать PARTUUID вашего корневого раздела с помощью команды `blkid -s PARTUUID -o value /dev/sdxY`, где 'x' - это буква устройства, а 'Y' - это номер раздела. Это нужно только для вашего корневого раздела, а не для $esp.

Для загрузки bootctl составляет пункты меню из `$esp/loader/entries/*.conf` файлов – каждый найденный файл должен содержать только одну загрузочную запись. Возможными опциями являются:

*   `title` – название операционной системы. **Обязательная.**

*   `version` – версия ядра, отображаемая только если существуют несколько записей с одинаковым названием. Не обязательная.

*   `machine-id` – идентификатор машины из `/etc/machine-id`, отображаемый только если существуют несколько записей с одинаковым названием и одинаковой версией. Не обязательная.

*   `efi` – EFI программа для запуска, относительно вашего ESP (`$esp`); например, `/vmlinuz-linux`. Либо это, либо `linux` (смотрите ниже) является **обязательным.**

*   `options` – опции командной строки для передачи EFI приложению. Не обязательная, но вам нужно будет передать как минимум `initrd=_efipath_` и `root=_dev_` если загружаете Linux.

Для Linux вы можете задать `linux _path-to-vmlinuz_` и `initrd _path-to-initramfs_`; это автоматически преобразуется в `efi _path_` и `options initrd=_path_` – этот синтаксис поддерживается только для удобства и не имеет различий по функциональности.

#### Установки со стандартной корневой директорией

Вот пример записи для корневого раздела без LVM или LUKS:

 `$esp/loader/entries/arch.conf` 

```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=PARTUUID=14420948-2cea-4de7-b042-40f67c618660 rw
```

Пожалуйста, обратите внимание, что в вышеприведённом примере PARTUUID/PARTLABEL идентифицируют GPT раздел, а это не то же самое, что UUID/LABEL, которые идентифицируют файловую систему. Использование PARTUUID/PARTLABEL бывает полезным, потому что они инвариантны (то есть неизменяемы), если вы переформатируете раздел в другую файловую систему или если по какой-то причине изменятся обозначения /dev/sd*. Также оно может быть полезно, если у вас нет файловой системы на разделе (или вы используете LUKS, который не поддерживает метки томов).

#### Установки с LVM корневой директорией

Вот пример для корневой директории, использующей [логический менеджер разделов](/index.php/LVM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LVM (Русский)"):

 `$esp/loader/entries/arch-lvm.conf` 

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

Вот пример конфигурационного файла для зашифрованного корневого раздела ([DM-Crypt / LUKS](/index.php/System_Encryption_with_LUKS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "System Encryption with LUKS (Русский)")):

 `$esp/loader/entries/arch-encrypted.conf` 

```
title Arch Linux Encrypted
linux /vmlinuz-linux
initrd /initramfs-linux.img
options cryptdevice=UUID=<UUID>:<mapped-name> root=UUID=<luks-UUID> quiet ro
```

В этом примере используется UUID; если хотите, можете заменить UUID на PARTUUID. Обратите внимание, что `<luks-UUID>` обозначает UUID актуальной расшифрованой корневой файловой системы (тот, что находится в `/dev/mapper/<mapped-name>`), а не UUID устройства. Смотрите [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration").

Вы также можете добавить другие EFI приложения, такие как `\EFI\arch\grub.efi`.

#### Установка корневого подраздела btrfs

При загрузке с подраздела [btrfs](/index.php/Btrfs "Btrfs") как корневого, замените `options` строку на `rootflags=subvol=<root subvolume>`. В примере ниже, корневой раздел монтируется как btrfs подраздел с именем 'ROOT' (например, `mount -o subvol=ROOT /dev/sdxY /mnt`):

 `$esp/loader/entries/arch-btrfs-subvol.conf` 

```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=PARTUUID=14420948-2cea-4de7-b042-40f67c618660 rw rootflags=subvol=ROOT
```

Если это невозможно сделать, то это приведет к ошибке: `ERROR: Root device mounted successfully, but /sbin/init does not exist.`

#### EFI Shells или другие EFI приложения

В случае, если вы установили EEFI Shells или другие EFI приложения в ESP, вы можете использовать следующие фрагменты:

 `$esp/loader/entries/uefi-shell-v1-x86_64.conf` 

```
title  UEFI Shell x86_64 v1
efi    /EFI/shellx64_v1.efi
```

 `$esp/loader/entries/uefi-shell-v2-x86_64.conf` 

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

**Обратите внимание:** Windows 8.x+, включая Windows 10, будут перезаписывать любой выбор порядка загрузки, который вы делаете и устанавливать себя в качестве приоритетной загрузки после каждого запуска. Изменение порядка загрузки в прошивке UEFI продлится только до следующей Windows 10 загрузки. Вы должны знать _Change Boot Option_ ключ для вашей материнской платы.

Для того, чтобы Windows 8.X не изменяли порядок загрузки, вы должны настроить групповые политики для Windows и выполнить скрипт (_.bat_) при запуске. В Windows:

1.  Откройте командную строку с правами администратора. Выполните `bcdedit /enum firmware`
2.  Найдите приложение, в котором в описании "Linux", например "Linux Boot Manager"
3.  Скопируйте ID, включая скобки, например `{31d0d5f4-22ad-11e5-b30b-806e6f6e6963}`.
4.  Создайте bat-файл (например, `bootorder.bat`) со следующим содержанием: `bcdedit /set {fwbootmgr} DEFAULT {_скопированный_ID_}` (например, `bcdedit /set {fwbootmgr} DEFAULT {31d0d5f4-22ad-11e5-b30b-806e6f6e6963}`).
5.  Откройте _gpedit_ и в _Local Computer Policy > Computer Configuration > Windows Settings > Scripts(Startup/Shutdown)_, выберите _Startup_. Должно открыться окно с заголовком _Startup Properties_.
6.  Во вкладке _Scripts_, нажмите кнопку _Add_
7.  Нажмите _Browse_ и выберите созданный bat-файл.

## Смотрите также

*   [http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/](http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Systemd-boot_(Русский)&oldid=416868](https://wiki.archlinux.org/index.php?title=Systemd-boot_(Русский)&oldid=416868)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Boot loaders (Русский)](/index.php/Category:Boot_loaders_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Boot loaders (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")