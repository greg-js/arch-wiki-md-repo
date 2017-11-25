Ссылки по теме

*   [Процесс загрузки Arch](/index.php/Arch_Boot_Process_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Boot Process (Русский)")
*   [Загрузчики](/index.php/Boot_loaders "Boot loaders")

**Состояние перевода:** На этой странице представлен перевод статьи [Syslinux](/index.php/Syslinux "Syslinux"). Дата последней синхронизации: 2014-10-16\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Syslinux&diff=0&oldid=340289).

[Syslinux](https://en.wikipedia.org/wiki/SYSLINUX и [Btrfs](/index.php/Btrfs "Btrfs").

**Примечание:** Syslinux не может получить доступ к файлам с разделов, которыми он не "владеет". Вы можете использовать альтернативный загрузчик, в котором нет такого ограничения, например, [GRUB](/index.php/GRUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB (Русский)")

## Contents

*   [1 Системы с BIOS](#.D0.A1.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B_.D1.81_BIOS)
    *   [1.1 Обзор процесса загрузки](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D1.81.D1.81.D0.B0_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8)
    *   [1.2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
        *   [1.2.1 Автоматическая установка](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
        *   [1.2.2 Ручная установка](#.D0.A0.D1.83.D1.87.D0.BD.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
            *   [1.2.2.1 Таблица разделов MBR](#.D0.A2.D0.B0.D0.B1.D0.BB.D0.B8.D1.86.D0.B0_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2_MBR)
            *   [1.2.2.2 Таблица разделов GUID (GPT)](#.D0.A2.D0.B0.D0.B1.D0.BB.D0.B8.D1.86.D0.B0_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2_GUID_.28GPT.29)
*   [2 Системы с UEFI](#.D0.A1.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B_.D1.81_UEFI)
    *   [2.1 Недостатки UEFI Syslinux](#.D0.9D.D0.B5.D0.B4.D0.BE.D1.81.D1.82.D0.B0.D1.82.D0.BA.D0.B8_UEFI_Syslinux)
    *   [2.2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_2)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 Примеры](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B)
        *   [3.1.1 Приглашение командной строки](#.D0.9F.D1.80.D0.B8.D0.B3.D0.BB.D0.B0.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.BD.D0.BE.D0.B9_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B8)
        *   [3.1.2 Текстовое меню загрузки](#.D0.A2.D0.B5.D0.BA.D1.81.D1.82.D0.BE.D0.B2.D0.BE.D0.B5_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8)
        *   [3.1.3 Графическое меню загрузки](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8)
    *   [3.2 Параметры ядра](#.D0.9F.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D1.8B_.D1.8F.D0.B4.D1.80.D0.B0)
    *   [3.3 Автозагрузка](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0)
    *   [3.4 Безопасность](#.D0.91.D0.B5.D0.B7.D0.BE.D0.BF.D0.B0.D1.81.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
    *   [3.5 Передача управления другому загрузчику (chainloading)](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B4.D0.B0.D1.87.D0.B0_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B4.D1.80.D1.83.D0.B3.D0.BE.D0.BC.D1.83_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D1.87.D0.B8.D0.BA.D1.83_.28chainloading.29)
    *   [3.6 Chainloading для других систем Linux](#Chainloading_.D0.B4.D0.BB.D1.8F_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D1.85_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC_Linux)
    *   [3.7 Использование memtest](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_memtest)
    *   [3.8 HDT](#HDT)
    *   [3.9 Перезагрузка и выключение](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.B8_.D0.B2.D1.8B.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [3.10 Очистка экрана](#.D0.9E.D1.87.D0.B8.D1.81.D1.82.D0.BA.D0.B0_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0)
    *   [3.11 Раскладка клавиатуры](#.D0.A0.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
    *   [3.12 Скрытие меню](#.D0.A1.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D0.BC.D0.B5.D0.BD.D1.8E)
    *   [3.13 Pxelinux](#Pxelinux)
    *   [3.14 Загрузка файлов образа ISO9660 при помощи memdisk](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0_ISO9660_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_memdisk)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Использование приглашения Syslinux](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8.D0.B3.D0.BB.D0.B0.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_Syslinux)
    *   [4.2 Fsck не работает на корневом разделе](#Fsck_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.BD.D0.B0_.D0.BA.D0.BE.D1.80.D0.BD.D0.B5.D0.B2.D0.BE.D0.BC_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B5)
    *   [4.3 No Default or UI found on some computers](#No_Default_or_UI_found_on_some_computers)
    *   [4.4 Missing operating system](#Missing_operating_system)
    *   [4.5 Windows загружается, игнорируя Syslinux](#Windows_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F.2C_.D0.B8.D0.B3.D0.BD.D0.BE.D1.80.D0.B8.D1.80.D1.83.D1.8F_Syslinux)
    *   [4.6 После выбора пункта меню ничего не происходит](#.D0.9F.D0.BE.D1.81.D0.BB.D0.B5_.D0.B2.D1.8B.D0.B1.D0.BE.D1.80.D0.B0_.D0.BF.D1.83.D0.BD.D0.BA.D1.82.D0.B0_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.BD.D0.B8.D1.87.D0.B5.D0.B3.D0.BE_.D0.BD.D0.B5_.D0.BF.D1.80.D0.BE.D0.B8.D1.81.D1.85.D0.BE.D0.B4.D0.B8.D1.82)
    *   [4.7 Невозможно удалить ldlinux.sys](#.D0.9D.D0.B5.D0.B2.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE_.D1.83.D0.B4.D0.B0.D0.BB.D0.B8.D1.82.D1.8C_ldlinux.sys)
    *   [4.8 Белый блок в верхнем левом углу при использовании vesamenu](#.D0.91.D0.B5.D0.BB.D1.8B.D0.B9_.D0.B1.D0.BB.D0.BE.D0.BA_.D0.B2_.D0.B2.D0.B5.D1.80.D1.85.D0.BD.D0.B5.D0.BC_.D0.BB.D0.B5.D0.B2.D0.BE.D0.BC_.D1.83.D0.B3.D0.BB.D1.83_.D0.BF.D1.80.D0.B8_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8_vesamenu)
    *   [4.9 Chainloading Windows не работает, когда она установлена на другом диске](#Chainloading_Windows_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82.2C_.D0.BA.D0.BE.D0.B3.D0.B4.D0.B0_.D0.BE.D0.BD.D0.B0_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B0_.D0.BD.D0.B0_.D0.B4.D1.80.D1.83.D0.B3.D0.BE.D0.BC_.D0.B4.D0.B8.D1.81.D0.BA.D0.B5)
    *   [4.10 Чтение логов загрузчика](#.D0.A7.D1.82.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BB.D0.BE.D0.B3.D0.BE.D0.B2_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D1.87.D0.B8.D0.BA.D0.B0)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Системы с BIOS

### Обзор процесса загрузки

1.  **Этап 1 : Часть 1** - **Загрузка MBR** - При запуске BIOS загружает 440 байт загрузочного кода [MBR](/index.php/Master_Boot_Record_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Master Boot Record (Русский)"), расположенного в начале диска (`/usr/lib/syslinux/bios/mbr.bin` или `/usr/lib/syslinux/bios/gptmbr.bin`)
2.  **Этап 1 : Часть 2** - **Поиск активного раздела**. **На первом этапе загрузки MBR** ищет раздел, помеченный, как активный (с установленным boot-флагом). Предположим, это раздел `/boot`
3.  **Этап 2 : Часть 1** - **Выполнение загрузочной записи тома** - **Первый этап загрузочной записи MBR** начинает выполнение Загрузочной Записи Тома (VBR) с раздела `/boot`. При использовании syslinux загрузочный код VBR находится в стартовом секторе `/boot/syslinux/ldlinux.sys`, который был создан командой `extlinux --install`. Обратите внимание, что `ldlinux.sys` — не то же самое, что `ldlinux.c32`
4.  **Этап 2 : Часть 2** - **Выполнение `/boot/syslinux/ldlinux.sys`** - VBR загрузит остальную часть `/boot/syslinux/ldlinux.sys`. Расположение сектора `/boot/syslinux/ldlinux.sys` не должно измениться, иначе syslinux не выполнит загрузку
    **Примечание:** В случае использования [Btrfs](/index.php/Btrfs "Btrfs") указанный выше способ не сработает, поскольку файлы переместятся в результате изменения расположения сектора `ldlinux.sys`. Поэтому в BTRFS весь код `ldlinux.sys` укладывается в пространство после VBR, а не устанавливается в `/boot/syslinux/ldlinux.sys`, в отличие от тех случаев, когда используются другие файловые системы

5.  **Этап 3** - **Загрузка `/boot/syslinux/ldlinux.c32`** - `/boot/syslinux/ldlinux.sys` загрузит `/boot/syslinux/ldlinux.c32` (основной модуль), который содержит остаток **основной** части syslinux, не умещающейся в `ldlinux.sys` (из-за ограничений на размер файла). `ldlinux.c32` должен присутствовать в каждой установке syslinux/extlinux и соответствовать версии `ldlinux.sys`, установленной на раздел. В противном случае, syslinux не выполнит загрузку. Смотрите [http://bugzilla.syslinux.org/show_bug.cgi?id=7](http://bugzilla.syslinux.org/show_bug.cgi?id=7) для получения дополнительной информации
6.  **Этап 4** - **Поиск и загрузка файла конфигурации** - После того, как Syslinux загрузится полностью, он ищет файл `/boot/syslinux/syslinux.cfg` (или `/boot/syslinux/extlinux.conf` в некоторых случаях) и загружает его, если он найден. Если нет, появится приглашение командной строки `boot:`. Этот шаг и остаток **неосновной** части syslinux (модули `/boot/syslinux/*.c32`, за исключением `lib*.c32` и `ldlinux.c32`) требуют наличия модулей `/boot/syslinux/lib*.c32` (библиотек) ([http://www.syslinux.org/wiki/index.php/Common_Problems#ELF](http://www.syslinux.org/wiki/index.php/Common_Problems#ELF)). Модули библиотек `lib*.c32` и неосновные модули `*.c32` должны соответствовать версии `ldlinux.sys`, установленной на раздел

### Установка

Установите пакет [syslinux](https://www.archlinux.org/packages/?name=syslinux) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

**Примечание:**

*   Начиная с версии Syslinux 4, Extlinux и Syslinux являются одним и тем же
*   Пакет [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) необходим для поддержки [GPT](https://en.wikipedia.org/wiki/GUID_Partition_Table "wikipedia:GUID Partition Table") с использованием автоматического скрипта
*   Если ваш загрузочный раздел отформатирован в FAT, вам также потребуется пакет [mtools](https://www.archlinux.org/packages/?name=mtools)

#### Автоматическая установка

**Примечание:**

*   Скрипт `syslinux-install_update` является специфичным для Archlinux, и по этой причине не предоставляется/поддерживается разработчиками Syslinux. Пожалуйста, направляйте все багрепорты, связанные с этим скриптом, в Arch Bug Tracker, а не в upstream
*   Если вы обновляете Syslinux с версии 5.xx (или старше) до версии 6.xx, пожалуйста, переустановите (а не обновите) Syslinux BIOS вручную (без использования установочного скрипта) один раз, следуя указаниям из раздела [#Ручная установка](#.D0.A0.D1.83.D1.87.D0.BD.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0). Установочный скрипт не способен корректно обновить Syslinux до версии 6.xx

Скрипт `syslinux-install_update` установит Syslinux, скопирует модули `*.c32` в `/boot/syslinux`, установит boot-флаг и загрузочный код в MBR. Он может работать с дисками [MBR](/index.php/Master_Boot_Record_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Master Boot Record (Русский)") и [GPT](/index.php/GUID_Partition_Table "GUID Partition Table") с программным RAID:

1.  Если вы используете отдельный раздел /boot, удостоверьтесь, что он примонтирован. Используйте для этого команду `lsblk`; если вы не видите точку монтирования `/boot`, примонтируйте раздел до того, как вы приступите к следующему шагу
2.  Запустите `syslinux-install_update` с опциями `-i` (установить файлы), `-a` (пометить раздел, как *активный*, при помощи *boot-флага*) и `-m` (установить загрузочный код *MBR*): `# syslinux-install_update -i -a -m` Если эта команда выдает ошибку *Установка Syslinux BIOS не удалась* (Syslinux BIOS install failed), вероятно, проблема в том, что исполняемый файл `extlinux` не может найти раздел, содержащий `/boot`:
    ```
    # extlinux --install /boot/syslinux
     extlinux: cannot find device for path /boot/syslinux
     extlinux: cannot open device (null)

    ```
    Это может случиться, например, при обновлении с [LILO](/index.php/LILO "LILO"), который при загрузке текущего пользовательского (custom) ядра изменил параметр ядра в командной строке с, допустим, `root=/dev/sda1` на его числовой эквивалент `root=801`, о чем свидетельствуют `/proc/cmdline` и вывод команды `mount`. Исправьте ситуацию либо используя ручную установку, как описано ниже, с указанием `--device=/dev/sda1` для `extlinux`, либо просто перезагрузившись на обычное ядро Arch Linux, поскольку оно использует initramfs, благодаря чему проблема исчезнет.
3.  Создайте или отредактируйте файл `/boot/syslinux/syslinux.cfg`, следуя указаниям из раздела [#Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0).

**Примечание:**

*   Если вы перезагрузите вашу систему сейчас, вы по-прежнему получите приглашение командной строки Syslinux. Для автоматической загрузки вашей системы или появления меню загрузки необходимо создать конфигурационный файл
*   Если вы находитесь в другом корневом каталоге (например, при загрузке с установочного носителя), установите Syslinux следующей командой:

```
# syslinux-install_update.sh -i -a -m -c /mnt/

```

#### Ручная установка

**Примечание:**

*   Если вы не уверены в том, какой тип таблицы разделов используете (MBR или GPT), вы можете это проверить следующей командой:

```
# blkid -s PTTYPE -o value /dev/sda
gpt

```

*   Если вы пытаетесь восстановить ранее установленную систему при помощи live CD, выполните [chroot](/index.php/Change_root_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Change root (Русский)") перед тем, как использовать эти команды. Если вы этого не сделаете, вы должны добавлять путь (не пути `/dev/`) до точки монтирования в каждой команде

Загрузочный раздел, на который вы планируете установить Syslinux, должен содержать файловую систему FAT, ext2, ext3, ext4 или Btrfs. Вы должны устанавливать его по пути точки монтирования, а не на устройство `/dev/sdXY`. Вы не должны устанавливать его в корневой каталог файловой системы, например, устройства `/dev/sda1`, примонтированного в `/boot`. Вы можете установить Syslinux в каталог `syslinux`:

```
# mkdir /boot/syslinux
# cp -r /usr/lib/syslinux/bios/*.c32 /boot/syslinux/                           ## скопируйте ВСЕ файлы *.c32 из /usr/lib/syslinux/bios/, А НЕ СОЗДАВАЙТЕ СИМВОЛЬНЫЕ ССЫЛКИ
# extlinux --install /boot/syslinux

```

После этого установите загрузочный код Syslinux (`mbr.bin` или `gptmbr.bin`) в 440-байтную область загрузочного кода MBR (не путать с MBR как таблицей разделов msdos) диска, как описано в следующем разделе.

##### Таблица разделов MBR

Загляните в основную статью: [Master Boot Record (Русский)](/index.php/Master_Boot_Record_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Master Boot Record (Русский)").

Теперь вам необходимо пометить ваш загрузочный раздел как активный в вашей таблице разделов. Вот несколько приложений, способных это сделать: `fdisk`, `cfdisk`, `sfdisk`, `parted/gparted` ("boot-флаг"). Должно получиться примерно следующее:

 `# fdisk -l /dev/sda` 
```
[...]
  Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048      104447       51200   83  Linux
/dev/sda2          104448   625142447   312519000   83  Linux

```

Установите MBR:

```
# dd bs=440 count=1 conv=notrunc if=/usr/lib/syslinux/bios/mbr.bin of=/dev/sda

```

Альтернативная MBR, которую предоставляет Syslinux: `altmbr.bin`. Эта MBR *не* сканирует диск на наличие загрузочного раздела; вместо этого, последнему байту MBR присваивается значение, отображающее то, с какого раздела необходимо выполнять загрузку. Вот пример того, как `altmbr.bin` может быть скопирован:

```
# printf '\x5' | cat /usr/lib/syslinux/bios/altmbr.bin - | \
dd bs=440 count=1 iflag=fullblock conv=notrunc of=/dev/sda

```

В этом случае один байт со значением 5 добавляется к содержимому `altmbr.bin` и итоговые 440 байт пишутся в MBR устройства `sda`. Syslinux был установлен на первый логический раздел (`/dev/sda5`) диска.

##### Таблица разделов GUID (GPT)

Загляните в основную статью: [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table").

Второй бит атрибутов (атрибут "legacy_boot") должен быть установлен для раздела `/boot`:.

```
# sgdisk /dev/sda --attributes=1:set:2

```

Это переключит атрибут *legacy BIOS bootable* на разделе 1\. Для проверки:

 `# sgdisk /dev/sda --attributes=1:show` 
```
 1:2:1 (legacy BIOS bootable)

```

Установите MBR:

```
# dd bs=440 conv=notrunc count=1 if=/usr/lib/syslinux/bios/gptmbr.bin of=/dev/sda

```

Если это не сработает, вы также можете попробовать:

```
# syslinux-install_update -i -m

```

## Системы с UEFI

**Примечание:**

*   В приведенных ниже командах `$esp` — это точка монтирования ESP (Системного Раздела EFI)
*   `efi64` обозначает x86_64 UEFI системы, для IA32 (32-bit) замены EFI `efi64` с `efi32` в приведенных ниже командах
*   Для syslinux файлы ядра и initramfs должны быть в ESP, поскольку syslinux (на данный момент) не имеет возможности получать доступ к файлам вне раздела, которым он "владеет" (например, вне ESP в данном случае). По этой причине рекомендуется монтировать ESP в `/boot`
*   Автоматический установочный скрипт `/usr/bin/syslinux-install_update` не поддерживает установку на системы с UEFI
*   Синтаксис конфигурации в `syslinux.cfg` для UEFI такой же, как и для BIOS

### Недостатки UEFI Syslinux

*   UEFI Syslinux `syslinux.efi` не может быть подписан `sbsign` (из sbsigntool) для UEFI Secure Boot. Багрепорт: [http://bugzilla.syslinux.org/show_bug.cgi?id=8](http://bugzilla.syslinux.org/show_bug.cgi?id=8)

*   Использование TAB при редактировании параметров ядра в меню UEFI Syslinux ведет к "нечитаемому тексту" (строки текста накладываются друг на друга). Багрепорт: [http://bugzilla.syslinux.org/show_bug.cgi?id=9](http://bugzilla.syslinux.org/show_bug.cgi?id=9)

*   UEFI Syslinux не поддерживает chainloading других приложений EFI, таких как `UEFI Shell` или `Windows Boot Manager`. Багрепорт: [http://bugzilla.syslinux.org/show_bug.cgi?id=17](http://bugzilla.syslinux.org/show_bug.cgi?id=17)

*   UEFI Syslinux может не загружаться в некоторых виртуальных машинах вроде QEMU/OVMF или VirtualBox, в продуктах/версиях VMware, а также в некоторых эмуляторах окружения UEFI, таких как DUET. Участник проекта Syslinux не подтвердил наличие этой проблемы при использовании VMware Workstation 10.0.2 и Syslinux-6.02\. Отчеты об ошибках: [http://bugzilla.syslinux.org/show_bug.cgi?id=21](http://bugzilla.syslinux.org/show_bug.cgi?id=21) и [http://bugzilla.syslinux.org/show_bug.cgi?id=23](http://bugzilla.syslinux.org/show_bug.cgi?id=23)

*   Memdisk недоступен для UEFI. Багрепорт: [http://bugzilla.syslinux.org/show_bug.cgi?id=30](http://bugzilla.syslinux.org/show_bug.cgi?id=30)

### Установка

*   Установите пакеты [syslinux](https://www.archlinux.org/packages/?name=syslinux) и [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Затем настройте syslinux в Системном Разделе EFI (ESP), как показано ниже

*   Скопируйте файлы syslinux в ESP (замените `$esp` на точку монтирования ESP, обычно это `/boot`):

```
# mkdir -p $esp/EFI/syslinux
# cp -r /usr/lib/syslinux/efi64/* $esp/EFI/syslinux

```

*   Настройте загрузочную запись для Syslinux, используя [efibootmgr](/index.php/Unified_Extensible_Firmware_Interface_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#efibootmgr "Unified Extensible Firmware Interface (Русский)"):

```
# efibootmgr -c -d /dev/sdX -p 1 -l /EFI/syslinux/syslinux.efi -L "Syslinux"

```

*   Создайте или отредактируйте файл `$esp/EFI/syslinux/syslinux.cfg`, следуя указаниям из раздела [#Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)

**Примечание:** Файл конфигурации для UEFI — `$esp/EFI/syslinux/syslinux.cfg`, а не `/boot/syslinux/syslinux.cfg`. Файлы в каталоге `/boot/syslinux/` являются специфичными для BIOS и не имеют никакого отношения к UEFI syslinux

## Настройка

Конфигурационный файл Syslinux, `syslinux.cfg`, должен быть создан в том же каталоге, в котором установлен Syslinux. В нашем случае это `/boot/syslinux/` для систем с BIOS и `$esp/EFI/syslinux/` для систем с UEFI.

Загрузчик будет искать как `syslinux.cfg` (предпочтительно), так и `extlinux.conf`

**Tip:**

*   Взамен `LINUX`, ключевое слово `KERNEL` также может быть использовано. `KERNEL` пытается определить тип файла, в то время как `LINUX` всегда ожидает ядро Linux
*   Одна единица в параметре `TIMEOUT` читается как **0.1** секунды

### Примеры

**Примечание:** Любые конфигурационные файлы, приведенные здесь, должны быть отредактированы, чтобы установить правильные параметры ядра. Смотрите раздел [#Параметры ядра](#.D0.9F.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D1.8B_.D1.8F.D0.B4.D1.80.D0.B0)

#### Приглашение командной строки

Это простой конфигурационный файл, который отобразит приглашение командной строки `boot:` и выполнит автоматическую загрузку через 5 секунд. Если вы хотите, чтобы загрузка начиналась сразу же, без вывода приглашения, установите параметр `PROMPT` в значение `0`.

Конфигурация:

 `/boot/syslinux/syslinux.cfg` 
```
 PROMPT 1
 TIMEOUT 50
 DEFAULT arch

 LABEL arch
         LINUX ../vmlinuz-linux
         APPEND root=/dev/sda2 rw
         INITRD ../initramfs-linux.img

 LABEL archfallback
         LINUX ../vmlinuz-linux
         APPEND root=/dev/sda2 rw
         INITRD ../initramfs-linux-fallback.img

```

#### Текстовое меню загрузки

Syslinux также позволяет вам использовать меню загрузки. Для этого скопируйте модуль `menu` в ваш каталог Syslinux:

```
# cp /usr/lib/syslinux/bios/menu.c32 /boot/syslinux/

```

Конфигурация:

 `/boot/syslinux/syslinux.cfg` 
```
 UI menu.c32
 PROMPT 0

 MENU TITLE Boot Menu
 TIMEOUT 50
 DEFAULT arch

 LABEL arch
         MENU LABEL Arch Linux
         LINUX ../vmlinuz-linux
         APPEND root=/dev/sda2 rw
         INITRD ../initramfs-linux.img

 LABEL archfallback
         MENU LABEL Arch Linux Fallback
         LINUX ../vmlinuz-linux
         APPEND root=/dev/sda2 rw
         INITRD ../initramfs-linux-fallback.img

```

Для получения дополнительных подробностей смотрите [документацию по Syslinux](http://git.kernel.org/?p=boot/syslinux/syslinux.git;a=blob;f=doc/menu.txt) или [Syslinux wiki](http://www.syslinux.org/wiki/index.php/Menu).

#### Графическое меню загрузки

Syslinux также позволяет вам использовать графическое меню загрузки. Для этого скопируйте COM32 модуль `vesamenu` в ваш каталог Syslinux:

```
# cp /usr/lib/syslinux/bios/vesamenu.c32 /boot/syslinux/

```

**Примечание:** Если вы используете [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Unified Extensible Firmware Interface (Русский)"), необходимо копировать модуль из каталога `/usr/lib/syslinux/efi64/` (`efi32` для систем i686), иначе вместо меню загрузки вы увидите черный экран. Если это случилось, произведите загрузку с установочного носителя и используйте [chroot](/index.php/Chroot "Chroot"), чтобы внести в систему необходимые изменения

В этой конфигурации используется такой же дизайн меню, как и на установочном образе Arch. Ее можно найти по адресу [projects.archlinux.org](https://projects.archlinux.org/archiso.git/tree/configs/releng/syslinux). [Фоновое изображение Arch Linux](https://projects.archlinux.org/archiso.git/plain/configs/releng/syslinux/splash.png) можно скачать там же. Скопируйте его в `/boot/syslinux/splash.png`.

Конфигурация:

 `/boot/syslinux/syslinux.cfg` 
```
 UI vesamenu.c32
 DEFAULT arch
 PROMPT 0
 MENU TITLE Boot Menu
 MENU BACKGROUND splash.png
 TIMEOUT 50

 MENU WIDTH 78
 MENU MARGIN 4
 MENU ROWS 5
 MENU VSHIFT 10
 MENU TIMEOUTROW 13
 MENU TABMSGROW 11
 MENU CMDLINEROW 11
 MENU HELPMSGROW 16
 MENU HELPMSGENDROW 29

 # Смотрите http://www.syslinux.org/wiki/index.php/Comboot/menu.c32

 MENU COLOR border       30;44   #40ffffff #a0000000 std
 MENU COLOR title        1;36;44 #9033ccff #a0000000 std
 MENU COLOR sel          7;37;40 #e0ffffff #20ffffff all
 MENU COLOR unsel        37;44   #50ffffff #a0000000 std
 MENU COLOR help         37;40   #c0ffffff #a0000000 std
 MENU COLOR timeout_msg  37;40   #80ffffff #00000000 std
 MENU COLOR timeout      1;37;40 #c0ffffff #00000000 std
 MENU COLOR msg07        37;40   #90ffffff #a0000000 std
 MENU COLOR tabmsg       31;40   #30ffffff #00000000 std

 LABEL arch
         MENU LABEL Arch Linux
         LINUX ../vmlinuz-linux
         APPEND root=/dev/sda2 rw
         INITRD ../initramfs-linux.img

 LABEL archfallback
         MENU LABEL Arch Linux Fallback
         LINUX ../vmlinuz-linux
         APPEND root=/dev/sda2 rw
         INITRD ../initramfs-linux-fallback.img

```

С версии Syslinux 3.84, `vesamenu.c32` поддерживает указание необходимого разрешения через параметр `MENU RESOLUTION $WIDTH $HEIGHT`. Для этого вставьте строку `MENU RESOLUTION 1440 900` в ваш файл конфигурации (в данном примере используется разрешение 1440x900). Фоновое изображение должно иметь такое же разрешение, в противном случае Syslinux откажется загружать меню.

### Параметры ядра

[Параметры ядра](/index.php/Kernel_parameters "Kernel parameters") устанавливаются при помощи строки `APPEND` файла `syslinux.cfg`. Рекомендуется внести эти изменения, в том числе, и для режима fallback.

В самых простых случаях должно быть изменено лишь имя раздела в параметре `root`. Измените `/dev/sda2` на то, что необходимо для указания на верный корневой раздел.

```
APPEND root=/dev/sda2

```

Если вы хотите использовать [UUID](/index.php/UUID "UUID") для [точного именования устройств](/index.php/Persistent_block_device_naming "Persistent block device naming"), а не их номера, измените значение строки `APPEND`, как показано ниже, заменив `1234` на `UUID` вашего корневого раздела:

```
APPEND root=UUID=*1234* rw

```

Если вы используете шифрование [LUKS](/index.php/LUKS "LUKS"), измените строку `APPEND` для использования вашего шифрованного тома:

```
APPEND root=/dev/mapper/*group*-*name* cryptdevice=/dev/sda2:*name* rw

```

Если вы используете программный [RAID](https://en.wikipedia.org/wiki/RAID "wikipedia:RAID") с [mdadm](http://neil.brown.name/blog/mdadm), измените строку `APPEND` для указания вашего RAID-массива. В приведенном ниже примере указывается три массива RAID 1, и один из них устанавливается в качестве корневого:

```
APPEND root=/dev/md1 rw md=0,/dev/sda2,/dev/sdb2 md=1,/dev/sda3,/dev/sdb3 md=2,/dev/sda4,/dev/sdb4

```

Если загрузка с раздела raid проваливается с использованием kernel device node method, более надежным способом является использование меток разделов:

```
APPEND root=МЕТКА=МЕТКА_КОРНЕВОГО_РАЗДЕЛА rw

```

### Автозагрузка

Если вы не хотите, чтобы выводилось меню Syslinux, используйте [#Приглашение командной строки](#.D0.9F.D1.80.D0.B8.D0.B3.D0.BB.D0.B0.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.BD.D0.BE.D0.B9_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B8), при этом установив параметр `PROMPT` в значение `0`. Убедитесь, что в вашем `syslinux.cfg` указана опция `DEFAULT`.

### Безопасность

Syslinux имеет два уровня безопасности загрузчика: мастер-пароль для всего меню и отдельные пароли для пунктов. В файле `syslinux.cfg` используйте

```
MENU MASTER PASSWD пароль 

```

чтобы установить мастер-пароль загрузчика, и

```
MENU PASSWD пароль 

```

внутри блока `LABEL`, чтобы установить пароль на отдельные пункты загрузки.

### Передача управления другому загрузчику (chainloading)

**Примечание:** Syslinux BIOS не может сам загружать файлы с других разделов, однако модуль `chain.c32` способен производить загрузку загрузочного сектора раздела (VBR)

Если вам необходимо передать управление другому загрузчику (например, для загрузки Windows), скопируйте модуль `chain.c32` в ваш каталог Syslinux (для получения подробностей прочитайте инструкции из предыдущих разделов). Затем создайте секцию в конфигурационном файле:

 `/boot/syslinux/syslinux.cfg` 
```
...
 LABEL windows
         MENU LABEL Windows
         COM32 chain.c32
         APPEND hd0 3
...

```

`hd0 3` — это третий раздел на первом устройстве BIOS. Счет устройств ведется с нуля, а счет разделов на устройствах — с единицы.

**Примечание:** В этом случае будет пропущен вызов собственного менеджера загрузки Windows (`bootmgr`), который необходим для завершения установки некоторых важных обновлений (например, [этого](http://support.microsoft.com/kb/2883200)). В подобных ситуациях рекомендуется временно установить загрузочный флаг MBR на раздел с Windows (например, при помощи [GParted](/index.php/GParted "GParted")), дать обновлениям завершить установку, после чего вернуть флаг на раздел с syslinux (например, при помощи программы для Windows [DiskPart](http://www.online-tech-tips.com/computer-tips/set-active-partition-vista-xp))

Если вы не уверены в том, какое устройство в BIOS считается "первым", вы можете использовать идентификатор MBR, или же, если вы используете GPT, метки файловой системы. Чтобы использовать идентификатор MBR, выполните команду

 `# fdisk -l /dev/sdb` 
```
 Disk /dev/sdb: 128.0 GB, 128035676160 bytes 
 255 heads, 63 sectors/track, 15566 cylinders, total 250069680 sectors
 Units = sectors of 1 * 512 = 512 bytes
 Sector size (logical/physical): 512 bytes / 512 bytes
 I/O size (minimum/optimal): 512 bytes / 512 bytes
 Disk identifier: 0xf00f1fd3

 Device Boot      Start         End      Blocks   Id  System
 /dev/sdb1            2048     4196351     2097152    7  HPFS/NTFS/exFAT
 /dev/sdb2         4196352   250066943   122935296    7  HPFS/NTFS/exFAT

```

заменив `/dev/sdb` на то устройство, которое вам необходимо. Использование шестнадцатеричного идентификатора диска (Disk identifier) `0xf00f1fd3` в этом случае в файле `syslinux.cfg` будет выглядеть так:

 `/boot/syslinux/syslinux.cfg` 
```
...
 LABEL windows
         MENU LABEL Windows
         COM32 chain.c32
         APPEND mbr:0xf00f1fd3
...

```

Для получения дополнительных подробностей про chainloading смотрите [Syslinux wiki](http://www.syslinux.org/wiki/index.php/Comboot/chain.c32).

Если на том же разделе у вас установлен [GRUB](/index.php/GRUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB (Русский)"), вы можете передать ему управление, используя:

 `/boot/syslinux/syslinux.cfg` 
```
...
 LABEL grub2
        MENU LABEL Grub2
        COM32 chain.c32
        append file=../grub/boot.img
...

```

Это может быть необходимо для загрузки из образов ISO.

### Chainloading для других систем Linux

Передача управления другому загрузчику, такому, как в Windows, является достаточно тривиальной задачей. Но в Syslinux возможна только загрузка файлов, находящихся на том же разделе, что и конфигурационный файл. Таким образом, если у вас установлена другая система Linux на другом разделе без отдельного `/boot`, появляется необходимость в применении Extlinux. По существу, Extlinux может быть установлен в "суперблок" раздела и обозначен, как отдельный загрузчик. Extlinux является частью проекта Syslinux и включен в пакет [syslinux](https://www.archlinux.org/packages/?name=syslinux).

Следующие инструкции подразумевают, что Syslinux у вас уже установлен. Также они подразумевают, что используется типичный путь к конфигурации Arch Linux `/boot/syslinux` и разделом для передачи управления `/` является раздел `/dev/sda3`.

Загрузитесь в имеющийся Linux (вероятно, на разделе, который указан в Syslinux для загрузки), примонтируйте другой корневой раздел в желаемую точку монтирования. В данном примере будет использоваться `/mnt`. Также, если вы используете отдельный раздел `/boot` во второй операционной системе, он также должен быть примонтирован. В приведенном примере предполагается, что это `/dev/sda2`.

```
# mount /dev/sda3 /mnt
# mount /dev/sda2 /mnt/boot (необходимо только в случае отдельного /boot)

```

Установите Extlinux и скопируйте необходимые файлы `*.c32`:

```
# extlinux -i /mnt/boot/syslinux
# cp /usr/lib/syslinux/bios/*.c32 /mnt/boot/syslinux

```

Создайте файл `/mnt/boot/syslinux/syslinux.cfg`. Вот пример файла конфигурации:

 `/boot/syslinux/syslinux.cfg **на /dev/sda3**` 
```
timeout 10

ui menu.c32

label Other Linux
    linux /boot/vmlinuz-linux
    initrd /boot/initramfs-linux.img
    append root=/dev/sda3 rw quiet

label MAIN
    com32 chain.c32
    append hd0 0

```

Взято со [страницы пользователя Djgera](/index.php/User:Djgera "User:Djgera").

### Использование memtest

Установите пакет [memtest86+](https://www.archlinux.org/packages/?name=memtest86%2B) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Используйте такую секцию `LABEL` для запуска [memtest](https://en.wikipedia.org/wiki/Memtest86 "wikipedia:Memtest86"):

 `/boot/syslinux/syslinux.cfg` 
```
...
 LABEL memtest
         MENU LABEL Memtest86+
         LINUX ../memtest86+/memtest.bin
...

```

**Примечание:** Если вы используете pxelinux, измените имя с *memtest.bin* на *memtest*, поскольку pxelinux интерпретирует файлы с расширением .bin как загрузочные секторы и загружает только 2KB из них

### HDT

[HDT (Hardware Detection Tool)](http://hdt-project.org/) отображает информацию об аппаратном обеспечении. Как и раньше, файл `.c32` должен быть скопирован из каталога `/boot/syslinux/`. Для информации PCI скопируйте файл `/usr/share/hwdata/pci.ids` в `/boot/syslinux/pci.ids` и добавьте следующее в ваш конфигурационный файл:

 `/boot/syslinux/syslinux.cfg` 
```
 LABEL hdt
         MENU LABEL Hardware Info
         COM32 hdt.c32

```

### Перезагрузка и выключение

Используйте следующие секции для возможности перезагрузки или выключения вашей машины:

 `/boot/syslinux/syslinux.cfg` 
```
 LABEL reboot
         MENU LABEL Reboot
         COM32 reboot.c32

 LABEL poweroff
         MENU LABEL Power Off
         COM32 poweroff.c32

```

### Очистка экрана

Для очистки экрана при выходе из меню добавьте следующую строку:

 `/boot/syslinux/syslinux.cfg` 
```
 MENU CLEAR

```

### Раскладка клавиатуры

Если вам часто приходится редактировать параметры загрузки, вы можете захотеть изменить раскладку клавиатуры. Это позволит вам проще вводить "=", "/" и другие символы.

Сначала вы должны создать совместимую раскладку (в данном примере — немецкая):

**Примечание:** Необходимо обязательно создать раскладку `us.kmap`, иначе эти действия ничего не дадут

```
$ cp /usr/share/kbd/keymaps/i386/qwertz/de.map.gz .
$ cp /usr/share/kbd/keymaps/i386/qwerty/us.map.gz .
$ gunzip de.map.gz
$ gunzip us.map.gz
$ mv de.map de.kmap
$ mv us.map us.kmap
# keytab-lilo de > de.ktl

```

Скопируйте файл `de.ktl` от имени суперпользователя в каталог `/boot/syslinux/` и назначьте root'a владельцем:

```
# chown root:root /boot/syslinux/de.ktl

```

Теперь отредактируйте `syslinux.conf`, добавив:

 `/boot/syslinux/syslinux.cfg` 
```
KBDMAP de.ktl

```

### Скрытие меню

Используйте опцию:

 `/boot/syslinux/syslinux.cfg` 
```
 MENU HIDDEN

```

чтобы скрыть меню и отображать только таймер. Нажмите любую клавишу в это время, и меню появится на экране.

### Pxelinux

**Примечание:** При наличии UEFI Syslinux использует один и тот же двоичный файл как для загрузки с диска, так и для загрузки по сети. Для загрузки файлов по TFTP или другим сетевым протоколам требуется функция загрузки по сети

**PXELINUX** предоставляется пакетом [syslinux](https://www.archlinux.org/packages/?name=syslinux).

Скопируйте загрузчик `{l,}pxelinux.0` (предоставляемый пакетом syslinux) в boot-каталог клиента. При использовании версии 5.00 (и более новых) также скопируйте `ldlinux.c32` из того же пакета:

```
# cp /usr/lib/syslinux/bios/pxelinux.0 "$root/boot"
# cp /usr/lib/syslinux/bios/ldlinux.c32 "$root/boot"
# mkdir "$root/boot/pxelinux.cfg"

```

Мы также создали каталог `pxelinux.cfg`, в котором PXELINUX по умолчанию ищет конфигурационные файлы. Поскольку мы не хотим иметь различий между разными MAC хоста, мы создаем конфигурацию `по умолчанию`:

 `# vim "$root/boot/pxelinux.cfg/default"` 
```
default linux

label linux
kernel vmlinuz-linux
append initrd=initramfs-linux.img quiet ip=:::::eth0:dhcp nfsroot=10.0.0.1:/arch

```

Или, если вы используете NBD, пропишите следующую строку:

 `append ro initrd=initramfs-linux.img ip=:::::eth0:dhcp nbd_host=10.0.0.1 nbd_name=arch root=/dev/nbd0` 
**Примечание:** Необходимо будет изменить параметры `nbd_host` и/или `nfsroot` таким образом, чтобы они соответствовали конфигурации вашей сети (адресу сервера NFS/NBD)

PXELINUX использует тот же синтаксис конфигурации, что и SYSLINUX; обратитесь к upstream-документации для получения дополнительной информации.

Ядро и initramfs будут переданы через TFTP, так что пути к ним должны быть прописаны относительно корня TFTP.

Для загрузки pxelinux замените `filename "/grub/i386-pc/core.0";` в `/etc/dhcpd.conf` на `filename "/pxelinux.0"`

### Загрузка файлов образа ISO9660 при помощи memdisk

Syslinux поддерживает прямую загрузку из ISO-образов при помощи модуля [memdisk](http://www.syslinux.org/wiki/index.php/MEMDISK). Для просмотра примеров обратитесь к разделу [Использование Syslinux и memdisk](/index.php/Multiboot_USB_drive#Using_Syslinux_and_memdisk "Multiboot USB drive").

## Решение проблем

### Использование приглашения Syslinux

Вы можете ввести имя блока `LABEL` записи, которую вы хотите загрузить (из тех, что указаны в файле `syslinux.cfg`). Если вы использовали конфигурации из приведенных примеров, просто напишите:

```
boot: arch

```

Если вы получите ошибку о том, что конфигурационный файл не может быть загружен (configuration file could not be loaded), вы можете передать необходимые параметры загрузки, например:

```
boot: ../vmlinuz-linux root=/dev/sda2 rw initrd=../initramfs-linux.img

```

Если у вас нет доступа к `boot:` в [ramfs](/index.php/Ramdisk "Ramdisk"), и, следовательно, временно не можете загрузить ядро:

	1\. Создайте временный каталог, чтобы примонтировать ваш корневой раздел (если он еще не существует):

```
 # mkdir -p /new_root

```

	2\. Примонтируйте `/` в `/new_root` (в случае, если `/boot/` находится на том же разделе; иначе вам придется монтировать и то, и другое):

**Примечание:** Busybox не может примонтировать `/boot`, если он находится на собственном разделе с ext2

```
 # mount /dev/sd[a-z][1-9] /new_root

```

	3\. Используя `vim`, отредактируйте `syslinux.cfg` опять, чтобы он удовлетворял вашим потребностям, и сохраните файл

	4\. Выполните перезагрузку

### Fsck не работает на корневом разделе

Если журнал корневой файловой системы поврежден, в ramfs emergency shell примонтируйте корневую файловую систему:

```
# mount /dev/*корневой раздел* /new_root

```

И возьмите оттуда двоичный файл tune2fs (он не включен в состав Syslinux):

```
# cp /new_root/sbin/tune2fs /sbin/

```

Следуйте инструкциям в [ext2fs: no external journal](/index.php/Fsck#ext2fs_:_no_external_journal "Fsck") для создания нового журнала корневого раздела.

### No Default or UI found on some computers

Некоторые производители материнских плат предоставляют меньшую совместимость загрузки с устройств USB, чем другие. В то время, как устройства USB, отформатированные в ext4, могут загружаться на более свежих компьютерах, некоторые машины могут зависнуть, если загрузочный раздел, содержащий *ядро* и *initrd*, не является разделом FAT16\. Для предотвращения загрузки `ldlinux` на более старых машинах и провала чтения `syslinux.cfg`, используйте `cfdisk`, чтобы создать раздел FAT16 (<=2GB), и отформатируйте его при помощи пакета [dosfstools](https://www.archlinux.org/packages/?name=dosfstools):

```
# mkfs.msdos -F 16 /dev/sda1

```

Затем установите и настройте Syslinux.

### Missing operating system

Если вы видите это сообщение, удостоверьтесь, что разделу, содержащему `/boot`, присвоен boot-флаг. Если флаг включен, возможно, раздел начинается с сектора 1, а не с 63 или 2048\. Проверьте это с помощью `fdisk -l`. Если предположение верно, вы можете передвинуть раздел(ы) при помощи `gparted` с диска восстановления. Или же, если у вас отдельный загрузочный раздел, вы можете создать резервную копию `/boot` при помощи

```
# cp -a /boot /boot.bak

```

а затем загрузиться с установочного образа Arch. Далее используйте `cfdisk`, чтобы удалить раздел `/boot` и создать его заново. Теперь он должен начинаться с правильного сектора, **63**. Примонтируйте ваши разделы и выполните [chroot](/index.php/Change_root_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Change root (Русский)"). Восстановите `/boot` следующей командой:

```
# cp -a /boot.bak/* /boot

```

Проверьте правильность файла `/etc/fstab`, выполните:

```
# syslinux-install_update -iam

```

и перезагрузитесь.

Вы также получите это сообщение об ошибке, если пытаетесь загрузиться с массива [RAID](/index.php/RAID "RAID") 1 и создали массив с слишком новой версией метаданных, которую Syslinux не понимает. По состоянию на август 2013 года по умолчанию mdadm создаст массив с версией 1.2 метаданных, но Syslinux не понимает версии, новее 1.0\. В этом случае вам необходимо пересоздать массив [RAID](/index.php/RAID "RAID"), используя флаг `--metadata=1.0` в mdadm.

### Windows загружается, игнорируя Syslinux

**Решение:** Убедитесь, что разделу, содержащему `/boot`, присвоен boot-флаг. Также убедитесь, что этот флаг не включен на разделе с Windows. Смотрите раздел установки выше.

MBR, идущий в Syslinux, ищет первый активный раздел, имеющий boot-флаг. Раздел с Windows, вероятно, был найден первым и имел этот флаг.

### После выбора пункта меню ничего не происходит

Вы выбираете пункт меню, и ничего не происходит, экран только *"обновляется"*. Обычно это означает, что в файле `syslinux.cfg` имеется ошибка. Нажмите `Tab` для редактирования параметров загрузки. В качестве альтернативы, вы можете нажать `Esc` и прописать имя блока `LABEL` вашей загрузочной записи (например, *arch*). Другой причиной может быть то, что у вас не установлено ядро. Найдите способ получить доступ к вашей файловой системе (например, используя live CD), удостоверьтесь, что файл `/mount/vmlinuz-linux` существует и имеет ненулевой размер. Если это не так, [переустановите ядро](/index.php/Kernel_Panics#Option_2:_Reinstall_kernel "Kernel Panics").

### Невозможно удалить ldlinux.sys

Файл `ldlinux.sys` имеет защитный атрибут, предотвращающий его удаление или перезапись. Это сделано потому, что расположение файла не должно меняться, иначе Syslinux должен быть переустановлен. Чтобы удалить его, выполните:

```
# chattr -i /boot/syslinux/ldlinux.sys
# rm /boot/syslinux/ldlinux.sys

```

### Белый блок в верхнем левом углу при использовании vesamenu

Проблема: *По состоянию на linux-3.0, драйвер modesetting пытается сохранять текущее содержимое экрана после смены разрешения (по крайней мере, это происходит с моим Intel, когда Syslinux работает в текстовом режиме). Возникает ошибка с комбинированием модуля vesamenu в Syslinux (белый блок — попытка сохранить меню Syslinux, но драйвер не может "ухватить" картинку из графического режима vesa).*

Если у вас прописано свое разрешение и `vesamenu` с ранним modesetting, попробуйте проделать следующее с вашим `syslinux.cfg` для удаления белого блока и продолжения вывода графического режима:

```
APPEND root=/dev/sda6 rw 5 **vga=current** quiet splash

```

### Chainloading Windows не работает, когда она установлена на другом диске

Если Windows установлена не на том диске, на котором установлен Arch, и у вас возникает проблема с передачей управления другому загрузчику, попробуйте следующую конфигурацию:

```
LABEL Windows
       MENU LABEL Windows
       COM32 chain.c32
       APPEND mbr:0xdfc1ba9e swap

```

Замените код mbr тем, что есть на диске с windows (детали [выше](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B4.D0.B0.D1.87.D0.B0_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B4.D1.80.D1.83.D0.B3.D0.BE.D0.BC.D1.83_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D1.87.D0.B8.D0.BA.D1.83_.28chainloading.29)), и добавьте `swap` в опции.

### Чтение логов загрузчика

В некоторых случаях, например, когда загрузчику не удается загрузить ядро, крайне желательно узнать дополнительную информацию о процессе загрузки. *Syslinux* отображает сообщения об ошибках на экране, но появляющееся меню быстро их скрывает. Чтобы избежать этого, необходимо отключить `menu UI` в `syslinux.cfg` и использовать приглашение по умолчанию — "command-line". Это означает:

*   Отменить указание UI
*   Отменить ONTIMEOUT
*   Отменить ONERROR
*   Отменить MENU CLEAR
*   Использовать больший TIMEOUT
*   Использовать PROMPT 1
*   Использовать DEFAULT <problematic_label>

Для получения более информативных отладочных сообщений необходимо перекомпилировать пакет [syslinux](https://www.archlinux.org/packages/?name=syslinux) с дополнительными CFLAGS:

```
-DDEBUG_STDIO=1 -DCORE_DEBUG=1

```

## Смотрите также

*   [Официальный сайт](http://www.syslinux.org)
*   [Конфигурация PXELinux](http://www.josephn.net/scrapbook/pxelinux_stuff)
*   [Мультизагрузка USB с использованием Syslinux](http://blog.jak.me/2013/01/03/creating-a-multiboot-usb-stick-using-syslinux/)