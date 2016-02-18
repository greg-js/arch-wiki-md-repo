**Состояние перевода:** На этой странице представлен перевод статьи [REFInd](/index.php/REFInd "REFInd"). Дата последней синхронизации: 2015-07-29\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=REFInd&diff=0&oldid=384524).

rEFInd - это менеджер загрузки для [UEFI](/index.php/UEFI_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "UEFI (Русский)"). Является форком более неподдерживаемого [rEFIt](http://refit.sourceforge.net/) и исправляет многие проблемы, связанные с UEFI загрузкой на не-Mac системах. Он является платформонезависимым и облегчает загрузку нескольких ОС.

**Обратите внимание:** В этой статье под `$esp` будем подразумевать точку монтирования [системного раздела EFI](/index.php/UEFI#EFI_System_Partition "UEFI") также называемого ESP.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Настройка с помощью скрипта](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_.D1.81.D0.BA.D1.80.D0.B8.D0.BF.D1.82.D0.B0)
    *   [1.2 Настройка вручную](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B2.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
    *   [1.3 Драйвера файловых систем](#.D0.94.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D1.8B.D1.85_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC)
        *   [1.3.1 Установка драйверов для rEFInd](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.BE.D0.B2_.D0.B4.D0.BB.D1.8F_rEFInd)
        *   [1.3.2 Использование драйверов в UEFI shell](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.BE.D0.B2_.D0.B2_UEFI_shell)
*   [2 Передача параметров ядру](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B4.D0.B0.D1.87.D0.B0_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2_.D1.8F.D0.B4.D1.80.D1.83)
    *   [2.1 Для ядер, автоматически обнаруженных rEFInd'ом](#.D0.94.D0.BB.D1.8F_.D1.8F.D0.B4.D0.B5.D1.80.2C_.D0.B0.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8_.D0.BE.D0.B1.D0.BD.D0.B0.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_rEFInd.27.D0.BE.D0.BC)
    *   [2.2 Ручные загрузочные блоки](#.D0.A0.D1.83.D1.87.D0.BD.D1.8B.D0.B5_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BE.D1.87.D0.BD.D1.8B.D0.B5_.D0.B1.D0.BB.D0.BE.D0.BA.D0.B8)
*   [3 Установка rEFInd при установленном UEFI Windows](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_rEFInd_.D0.BF.D1.80.D0.B8_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D0.BE.D0.BC_UEFI_Windows)
*   [4 Обновление rEFInd](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_rEFInd)
    *   [4.1 Автоматизация с помощью Systemd](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_Systemd)
*   [5 Apple Маки](#Apple_.D0.9C.D0.B0.D0.BA.D0.B8)
*   [6 VirtualBox](#VirtualBox)
*   [7 Утилиты](#.D0.A3.D1.82.D0.B8.D0.BB.D0.B8.D1.82.D1.8B)
    *   [7.1 UEFI shell](#UEFI_shell)
    *   [7.2 Memtest86](#Memtest86)
    *   [7.3 iPXE](#iPXE)
*   [8 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [refind-efi](https://www.archlinux.org/packages/?name=refind-efi) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

### Настройка с помощью скрипта

Пакет rEFInd содержит скрипт `/usr/bin/refind-install`, который упрощает процесс настройки rEFInd в качестве вашей загрузочной EFI записи по умолчанию. У скрипта есть несколько вариаций для обработки различных установок и реализаций UEFI, но для большинства систем подойдёт обычная команда

```
# refind-install

```

Он попытается найти и смонтировать ваш [ESP раздел](/index.php/UEFI#EFI_System_Partition "UEFI"), скопировать файлы rEFInd'а в `/EFI/refind/` на ESP и добавить rEFInd как загрузочную EFI запись по умолчанию с помощью [UEFI#efibootmgr](/index.php/UEFI#efibootmgr "UEFI").

**Обратите внимание:** По умолчанию `refind-install` устанавливает только драйвер для вашей корневой файловой системы, если вы хотите установить дополнительные драйвера, перейдите к разделу [#Драйвера файловых систем](#.D0.94.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D1.8B.D1.85_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC).

Вы также можете установить rEFInd в загрузочный путь по умолчанию/аварийный `/EFI/BOOT/BOOT*.EFI`. Это может пригодиться для загрузочных USB flash накопителей или для систем, у которых наблюдаются проблемы с изменениеми NVRAM при использовании утилиты efibootmgr:

```
# refind-install --usedefault **/dev/sdXY**

```

Где **/dev/sdXY** - это ваш раздел ESP.

Для разъяснения каждой опции можете прочитать комментарии в установочном скрипте.

После установки файлов rEFInd'а на ESP, проверьте, что rEFInd создал `refind_linux.conf`, содержащий необходимые [параметры ядра](/index.php/%D0%9F%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D1%8B_%D1%8F%D0%B4%D1%80%D0%B0 "Параметры ядра") (например, `root=`) в той же директории, где находится ваше ядро. Если он не создал этот файл, вам необходимо будет установить [#Передача параметров ядру](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B4.D0.B0.D1.87.D0.B0_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2_.D1.8F.D0.B4.D1.80.D1.83) вручную иначе скорее всего вы получите панику ядра при следующей загрузке.

По умолчанию rEFInd будет сканировать все ваши носители (для которых у него есть драйвера) и добавит загрузочную запись для каждого EFI загрузчика, что он найдёт, то есть он должен добавить и ваше ядро (так как в Arch используется [EFISTUB](/index.php/EFISTUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "EFISTUB (Русский)") по умолчанию). Поэтому на данный момент у вас уже может быть загружаемая система.

**Совет:** Хорошей идеей будет правка конфигурации по умолчанию в `/EFI/refind/refind.conf` на ESP, для того, чтобы убедиться, что опции по умолчанию у вас работают.

### Настройка вручную

**Совет:** rEFInd может загружать Linux различными способами. Смотрите [The rEFInd Boot Manager: Methods of Booting Linux](http://www.rodsbooks.com/refind/linux.html) для обзора различных способов.

**Обратите внимание:** Для 32-битных EFI замените **x64** на **ia32** в нижеследующих командах.

Если у вас не работает скрипт `refind-install`, rEFInd можно установить вручную.

Сперва скопируйте исполняемый файл на ESP:

```
# cp /usr/share/refind/refind_x64.efi $esp/EFI/refind/

```

Затем используйте [UEFI#efibootmgr](/index.php/UEFI#efibootmgr "UEFI"), чтобы создать загрузочную запись в UEFI NVRAM (замените X и Y на соответствующий номер вашего носителя и раздела, где расположен ESP). Если вы устанавливаете rEFInd в расположение UEFI загрузчика по умолчанию `/EFI/BOOT/BOOTX64.EFI`, возможно, вы можете пропустить данный шаг.

```
# efibootmgr -c -d /dev/sdX -p Y -l /EFI/refind/refind_x64.efi -L "rEFInd Boot Manager"

```

С этого момента вы сможете загрузиться в rEFInd, но он пока не сможет загружать ваше ядро. Если ваше ядро расположено не на ESP, rEFInd может смонтировать ваши разделы, чтобы найти его, при условии что у него есть нужные драйвера:

```
# mkdir $esp/EFI/refind/drivers
# cp /usr/share/refind/drivers_x64/myrootfs_x64.efi $esp/EFI/refind/drivers

```

Теперь у rEFInd есть загрузочная запись с вашим ядром, но он не будет передавать необходимые параметры ядра. Следуйте инструкциям [#Передача параметров ядру](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B4.D0.B0.D1.87.D0.B0_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2_.D1.8F.D0.B4.D1.80.D1.83). Теперь вы можете загружать ваше ядро с помощью rEFInd. Если же вы всё ещё не можете загрузиться или вы хотите поиграться с настройками rEFInd'а, многие опции можно менять в конфигурационном файле:

```
# cp /usr/share/refind/refind.conf-sample $esp/EFI/refind/refind.conf

```

Пример настройки подробно прокомментирован и не требует разъяснений.

Если вы не используете `textonly` в конфигурационном файле, вы должны скопировать иконки для rEFInd'а, чтобы избавиться от уродливых заглушек:

```
# cp -r /usr/share/refind/icons $esp/EFI/refind/

```

Также вы можете попробовать разнообразные шрифты, скопировав их и изменив опцию `font` в `refind.conf`:

```
# cp -r /usr/share/refind/fonts $esp/EFI/refind/

```

**Совет:** Нажатие F10 в rEFInd сохранит скриншот в директории верхнего уровня ESP раздела.

### Драйвера файловых систем

**Обратите внимание:** rEFInd'у не требуется, чтобы ваше ядро располагалось в каком-то определённом месте, однако если оно будет не на ESP, вам понадобится использовать драйвера файловых систем, чтобы rEFInd мог читать его.

На данный момент в rEFInd есть **read-only** драйвера для следующих файловых систем:

*   ReiserFS
*   Ext2
*   [Ext4](/index.php/Ext4_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Ext4 (Русский)")
*   [Btrfs](/index.php/Btrfs "Btrfs")
*   ISO-9660
*   HFS+
*   [NTFS](/index.php/NTFS-3G_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NTFS-3G (Русский)")

**Совет:** Чтобы найти дополнительные драйвера, смотрите [The rEFInd Boot Manager: Using EFI Drivers: Finding Additional EFI Drivers](http://www.rodsbooks.com/refind/drivers.html#finding).

#### Установка драйверов для rEFInd

rEFInd автоматически загружает все драйвера из поддиректорий `drivers` и `drivers_*arch*` (например, `drivers_x64`) в его директории установки.

```
# cp /usr/share/refind/drivers_x64/**drivername**_x64.efi $esp/EFI/refind/drivers_x64/

```

**Совет:** Есди вы используете скрипт rEFInd'а для установки, вы можете установить все драйвера с помощью опции `--alldrivers`. Это полезно например для загрузочных USB flash накопителей.
```
# refind-install --usedefault /dev/sdXY --alldrivers

```

#### Использование драйверов в UEFI shell

Чтобы использовать драйвера rEFInd'а в UEFI шелле, загрузите их с помощью команды `load` и обновите подключенные носители командой `map -r`.

```
# load FS0:\EFI\refind\drivers\ext4_x64.efi
# map -r

```

Теперь вы можете получить доступ к вашей файловой системе из UEFI шелла.

## Передача параметров ядру

Существует два метода для установки [параметров ядра](/index.php/%D0%9F%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D1%8B_%D1%8F%D0%B4%D1%80%D0%B0 "Параметры ядра"), которые rEFInd передаст ядру.

### Для ядер, автоматически обнаруженных rEFInd'ом

Если rEFInd автоматически обнаружил ваше ядро, вы можете положить файл `refind_linux.conf`, содержащий параметры ядра в ту же директорию, где находится ядро. В качестве шаблона вы можете взять `/usr/share/refind/refind_linux.conf-sample`. Первой незакомментированной строкой файла `refind_linux.conf` и будет параметры ядра по умолчанию. Остальные строки будут задавать параметры, которые вы сможете выбрать в подменю с помощью `+`, `F2` или `Insert`.

Также вы можете попробовать:

```
# refind-mkrlconf

```

Эта команда попытается найти ваше ядро в `/boot` и автоматически сгенерирует `refind_linux.conf`. Скрипт установит только самые базовые параметры ядра, поэтому лучше проверьте, что созданный файл корректен.

Если вы не зададите параметр `initrd=`, rEFInd автоматически добавит его, увидя стандартное название файлов RAM disk в директории с ядром. Если вам нужно несколько `initrd=` параметров (например для [Микрокода](/index.php/Microcode_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Microcode (Русский)")), вы должны задать их вручную в файле `refind_linux.conf`.

### Ручные загрузочные блоки

Если ваше ядро не обнаружилось автоматически, или же вы просто хотите получить больше контроля над опциями для меню загрузки, вы можете вручную создать загрузочные записи, используя блоки в файле `refind.conf`. Убедитесь, что `scanfor` содержит `manual`, иначе эти записи не появятся в меню rEFInd'а. Параметры ядра передаются с помощью ключевого слова `options`. rEFInd добавит параметр `initrd=`, используя файл, заданный ключевым словом `initrd` в блоке. Если вам нужны дополнительные initrd (например, для [Микрокода](/index.php/%D0%9C%D0%B8%D0%BA%D1%80%D0%BE%D0%BA%D0%BE%D0%B4 "Микрокод")), вы можете задать их в `options` (а тот, который задан ключевым словом `initrd`, будет добавлен в конце).

 `$esp/EFI/refind/refind.conf` 
```
...

menuentry "Arch Linux" {
        icon     /EFI/refind/icons/os_arch.png
        volume   Boot
        loader   /boot/vmlinuz-linux
        initrd   /boot/initramfs-linux.img
        options  "root=PARTUUID=XXXXXXXX rootfstype=XXXX rw add_efi_memmap"
        submenuentry "Boot using fallback initramfs" {
                initrd /boot/initramfs-linux-fallback.img
        }
}

```

Возможно, вам понадобится изменить `volume` на соответствующий либо метке тома файловой сисьтемы, либо названию раздела, либо UUID раздела, либо же номеру раздела (например, `0:`), в котором находится образ ядра. Смотрите [Ext3#Assigning a label](/index.php/Ext3#Assigning_a_label "Ext3") в качестве примера назначения метки тома.

## Установка rEFInd при установленном UEFI Windows

**Обратите внимание:** Соблюдайте советы из [Windows and Arch dual boot (Русский)](/index.php/Windows_and_Arch_dual_boot_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Windows and Arch dual boot (Русский)").

rEFInd совместим с системным разделом EFI, созданным при установке UEFI Windows, поэтому нет необходимости создавать или форматировать другой FAT32 раздел, если вы устанавливаете Arch рядом с Windows. Просто смонтируйте Windows'овый ESP и установите rEFInd как обычно. По умолчанию, функция автообнаружения rEFInd'а должна распознать любые существующие Windows/recovery загрузчики.

## Обновление rEFInd

Pacman обновляет rEFInd файлы в `/usr/share/refind`, но не копирует эти новые файлы на ESP за вас. Если при установке rEFInd вы использовали `refind-install`, вы можете выполнить эту команду заново, чтобы скопировались новые файлы. Новый конфигурационный файл скопируется как `refind.conf-sample`, так что вы сможете интегрировать изменения в ваш конфигурационный файл, воспользовавшись утилитой diff. Если вы использовали [ручную](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B2.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E) установку rEFInd, вам нужно будет скопировать новые файлы самостоятельно.

### Автоматизация с помощью Systemd

Чтобы автоматизировать данный процесс, вам понадобится .path файл для наблюдения за обновлениями rEFInd и .service файл для копирования новых файлов и обновления nvram.

 `/etc/systemd/system/refind_update.path` 
```
[Unit]
Description=path monitor for rEFInd updates

[Path]
PathChanged=/usr/share/refind

[Install]
WantedBy=multi-user.target

```
 `/etc/systemd/system/refind_update.service` 
```
[Unit]
Description=rEFInd boot manager update

[Service]
Type=oneshot
ExecStart=/usr/bin/refind-install

```

Затем [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") `refind_update.path`.

## Apple Маки

[mactel-boot](https://aur.archlinux.org/packages/mactel-boot/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") - это экспериментальная "благословительная" утилита для Linux. Если она не работает, используйте "благословление" изнутри OSX, чтобы установить rEFInd в качестве загрузочной записи по умолчанию. Предполагая, что ваш UEFISYS раздел смонтирован в `/mnt/efi`, находясь в OSX выполните:

```
# bless --setBoot --folder /mnt/efi/EFI/refind --file /mnt/efi/EFI/refind/refind_x64.efi

```

## VirtualBox

На данный момент VirtualBox умеет загружать только запись по умолчанию, расположенную в `/EFI/BOOT/BOOT*.EFI`, поэтому `refind-install` нужно как минимум использовать с опцией `--usedefault`. Смотрите [VirtualBox (Русский)#Установка в режиме EFI](/index.php/VirtualBox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B2_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5_EFI "VirtualBox (Русский)") для дополнительной информации.

## Утилиты

rEFInd поддерживает запуск некоторых сторонних утилит. Утилиты нужно устанавливать отдельно. Отредактируйте `showtools` в `refind.conf`, чтобы выбрать, какие будут отображаться.

 `$esp/EFI/refind/refind.conf` 
```
...
# Какие внешние не относящиеся к загрузчику утилиты будут показаны в строке с утилитами
#   и в каком порядке отображать их:
#  shell            - EFI shell (требуется внешняя программа; смотрите документацию rEFInd
#                     для подробностей)
#  memtest          - программа memtest86, в EFI/tools, EFI/memtest86,
#                     EFI/memtest, EFI/tools/memtest86 или EFI/tools/memtest
#  gptsync          - утилита gptsync.efi (опасная) (требуется внешняя программа;
#                     смотрите документацию rEFInd для подробностей)
#  gdisk            - программа gdisk для управления разделами
#  apple_recovery   - загружает раздел Apple Recovery HD, если такой есть
#  windows_recovery - загружает OEM утилиту восстановления Windows, если такая есть
#                     (смотрите также опцию windows_recovery_files)
#  mok_tool         - активирует возможность управления утилитой Machine Owner Key (MOK),
#                     MokManager.efi, использующейся на Secure Boot системах
#  about            - опция отображения "об этой программе"
#  exit             - тег для выхода из rEFInd
#  shutdown         - выключает компьютер (она ошибочно может приводить к перезагрузке
#                     на многих UEFI системах)
#  reboot           - тег для перезагрузки компьютера
#  firmware         - тег для перезагрузки компьютера и входа в интерфейс прошивки
#                     (игнорируется на старых компьютерах)
#  netboot          - запускает утилиту ipxe.efi для сетевой (PXE) загрузки
# По умолчанию включены shell,memtest,gdisk,apple_recovery,windows_recovery,mok_tool,about,shutdown,reboot,firmware
#
**showtools** **shell**, **memtest**, **netboot**, about, reboot, firmware
...

```

### UEFI shell

Смотрите [UEFI shell](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface").

Скопируйте `shellx64.efi` в корень [Системного Раздела EFI](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface")

### Memtest86

Установите [memtest86-efi](https://aur.archlinux.org/packages/memtest86-efi/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") и скопируйте его в `$esp/EFI/tools/`.

```
# cp /usr/share/memtest86-efi/bootx64.efi $esp/EFI/tools/memtest86.efi

```

### iPXE

**Обратите внимание:** Поддержка PXE в rEFInd является **экспериментальной**.

[refind-efi](https://www.archlinux.org/packages/?name=refind-efi) содержит бинарники iPXE UEFI, вам просто нужно скопировать их в `$esp/EFI/tools/`.

```
# cp /usr/share/refind/tools_x64/ipxe_discovery_x64.efi $esp/EFI/tools/ipxe_discovery.efi
# cp /usr/share/refind/tools_x64/ipxe_x64.efi $esp/EFI/tools/ipxe.efi

```

## Смотрите также

*   [The rEFInd Boot Manager](http://www.rodsbooks.com/refind/) by Roderick W. Smith.
*   `/usr/share/refind/docs/README.txt`