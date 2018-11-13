**Состояние перевода:** На этой странице представлен перевод статьи [Microcode](/index.php/Microcode "Microcode"). Дата последней синхронизации: 2 сентября 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Microcode&diff=0&oldid=539324).

Производители процессоров выпускают обновления стабильности и безопасности для [микрокода](https://en.wikipedia.org/wiki/ru:%D0%9C%D0%B8%D0%BA%D1%80%D0%BE%D0%BA%D0%BE%D0%B4 "wikipedia:ru:Микрокод") процессора. Несмотря на то, что микрокод можно обновить с помощью BIOS, ядро Linux также может применять эти обновления во время загрузки. Эти обновления предоставляют исправления ошибок, которые могут быть критичны для стабильности вашей системы. Без этих обновлений вы можете наблюдать ложные падения или неожиданные зависания системы, которые может быть сложно отследить.

Особенно пользователи процессоров семейства Intel Haswell и Broadwell должны установить эти обновления, чтобы обеспечить стабильность системы. Но, понятное дело, все пользователи должны устанавливать эти обновления.

## Contents

*   [1 Установка](#Установка)
*   [2 Включение раннего обновления микрокода](#Включение_раннего_обновления_микрокода)
    *   [2.1 GRUB](#GRUB)
        *   [2.1.1 Автоматический способ](#Автоматический_способ)
        *   [2.1.2 Ручной способ](#Ручной_способ)
    *   [2.2 systemd-boot](#systemd-boot)
    *   [2.3 EFI boot stub / EFI handover](#EFI_boot_stub_/_EFI_handover)
    *   [2.4 rEFInd](#rEFInd)
    *   [2.5 Syslinux](#Syslinux)
    *   [2.6 LILO](#LILO)
*   [3 Позднее обновление микрокода](#Позднее_обновление_микрокода)
    *   [3.1 Включение позднего обновления микрокода](#Включение_позднего_обновления_микрокода)
    *   [3.2 Отключение позднего обновления микрокода](#Отключение_позднего_обновления_микрокода)
*   [4 Проверим, обновился ли microcode при загрузке](#Проверим,_обновился_ли_microcode_при_загрузке)
*   [5 Каким ЦП нужны обновления микрокода](#Каким_ЦП_нужны_обновления_микрокода)
    *   [5.1 Обнаружение доступного обновления микрокода](#Обнаружение_доступного_обновления_микрокода)
*   [6 Применение ранней загрузки микрокода в кастомных ядрах](#Применение_ранней_загрузки_микрокода_в_кастомных_ядрах)
*   [7 Смотрите также](#Смотрите_также)

## Установка

Для процессоров AMD [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [amd-ucode](https://www.archlinux.org/packages/?name=amd-ucode).

Для процессоров Intel [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode).

## Включение раннего обновления микрокода

Микрокод должен быть загружен [загрузчик](/index.php/%D0%97%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D1%87%D0%B8%D0%BA "Загрузчик")ом. Из-за большого разнообразия конфигураций ранней загрузки у пользователей обновления микрокода могут быть не применены автоматически конфигурацией Arch по умолчанию. Многие [ядра](/index.php/%D0%AF%D0%B4%D1%80%D0%B0 "Ядра") в AUR пошли по пути официальных ядер Arch в этом вопросе.

Чтобы применить эти обновления, добавьте `/boot/amd-ucode.img` или `/boot/intel-ucode.img` в качестве **первого initrd в конфигурационном файле загрузчика**. Это в дополнение к обычному initrd файлу. Смотрите ниже инструкции для популярных загрузчиков.

**Примечание:** В следующих разделах замените строку `*производитель_цп*` вашим производителем, например, `amd` или `intel`.

### GRUB

#### Автоматический способ

Утилита *grub-mkconfig* автоматически определит обновления микрокода и настроит соответственным образом [GRUB](/index.php/GRUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB (Русский)"). После установки пакета микрокода, перегенерируйте настройки GRUB, чтобы включить обновление микрокода при запуске:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

#### Ручной способ

Альтернативно пользователи, управляющие настройками GRUB вручную, могут добавить `/boot/*производитель_цп*-ucode.img` (или `/*производитель_цп*-ucode.img`, если есть отдельный раздел `/boot`) следующим образом:

 `/boot/grub/grub.cfg` 
```
...
echo 'Loading initial ramdisk'
initrd **/boot/*производитель_цп*-ucode.img** /boot/initramfs-linux.img
...

```

Повторите это для каждой записи в меню.

### systemd-boot

Используйте параметры `initrd` для загрузки микрокода перед исходным ramdisk следующим образом:

 `/boot/loader/entries/*запись*.conf` 
```
title   Arch Linux
linux   /vmlinuz-linux
**initrd  /*производитель_цп*-ucode.img**
initrd  /initramfs-linux.img
...

```

Самый последний микрокод `*производитель_цп*-ucode.img` должен быть доступен во время загрузки вашего [системного раздела EFI](/index.php/%D0%A1%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%BD%D1%8B%D0%B9_%D1%80%D0%B0%D0%B7%D0%B4%D0%B5%D0%BB_EFI "Системный раздел EFI") (ESP). ESP должен быть смонтирован как `/boot`, чтобы обновлять микрокод каждый раз, когда обновляется [amd-ucode](https://www.archlinux.org/packages/?name=amd-ucode) или [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode). В противном случае копируйте `/boot/*производитель_цп*-ucode.img` в ваш ESP при каждом обновлении пакета микрокода.

### EFI boot stub / EFI handover

Добавьте два параметра `initrd=`:

```
**initrd=/*производитель_цп*-ucode.img** initrd=/initramfs-linux.img

```

Для ядер, которые были сгенерированы как один файл, содержащий все initrd, cmdline и ядро, сначала сгенерируйте initrd для интеграции, создав новый, следующим образом:

```
cat /boot/*производитель_цп*-ucode.img /boot/initramfs-linux.img > my_new_initrd
objcopy ... --add-section .initrd=my_new_initrd
```

### rEFInd

Отредактируйте опции загрузки в `/boot/refind_linux.conf` также как в примере EFI boot stub выше, например:

```
"Boot with standard options" "rw root=UUID=(...) **initrd=/boot/*производитель_цп*-ucode.img** initrd=/boot/initramfs-linux.img"

```

Пользователи, использующие [ручные строфы](/index.php/REFInd#Manual_boot_stanzas "REFInd") в `*esp*/EFI/refind/refind.conf` для определения ядер, должны просто добавить `initrd=/boot/*производитель_цп*-ucode.img` (или `/*производитель_цп*-ucode.img`, если есть отдельный раздел `/boot`), как требуется для строки опций, а не в основной части строфы. Например:

```
options  "root=root=UUID=(...) rw add_efi_memmap **initrd=/boot/*производитель_цп*-ucode.img**"

```

### Syslinux

**Примечание:** Между указаниями файлов initrd `*производитель_цп*-ucode.img` и `initramfs-linux.img` не должно быть пробелов. Точки здесь вовсе не означают каких-либо сокращений или пропущенного кода: строка `INITRD` должна быть точно такой, как показано ниже.

Несколько файлов initrd могут быть разделены запятыми в `/boot/syslinux/syslinux.cfg`:

```
LABEL arch
    MENU LABEL Arch Linux
    LINUX ../vmlinuz-linux
    INITRD **../*производитель_цп*-ucode.img**,../initramfs-linux.img
...

```

### LILO

LILO и потенциально другие старые загрузчики не поддерживают несколько образов initrd. В этом случае необходимо объединить `*производитель_цп*-ucode.img` и `initramfs-linux.img` в один образ.

**Важно:** Объединенный образ нужно пересоздавать после каждого обновления ядра!

**Примечание:** Порядок важен. Исходный образ `initramfs-linux.img` должен находиться **сверху** над образом `*производитель_цп*-ucode.img`.

Чтобы объединить образы в один `initramfs-merged.img`, можно использовать следующую команду:

```
# cat /boot/*производитель_цп*-ucode.img /boot/initramfs-linux.img > /boot/initramfs-merged.img

```

Теперь отредактируйте `/etc/lilo.conf` для загрузки нового образа.

```
...
initrd=/boot/initramfs-merged.img
...

```

И запустите `lilo` от суперпользователя:

```
# lilo

```

## Позднее обновление микрокода

Поздняя загрузка обновления микрокода происходит после запуска системы. Для этого используются файлы в `/usr/lib/firmware/amd-ucode/` и `/usr/lib/firmware/intel-ucode/`.

Для процессоров AMD файлы обновления микрокода предоставляются пакетом [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

Для процессоров Intel ни один пакет не предоставляет файлы обновления микрокода ([FS#59841](https://bugs.archlinux.org/task/59841)). Чтобы использовать позднюю загрузку, вам необходимо вручную извлечь `intel-ucode/` из предоставленного Intel архива.

### Включение позднего обновления микрокода

В отличие от ранней загрузки, поздняя загрузка обновлений микрокода в Arch Linux включена по умолчанию, используя `/usr/lib/tmpfiles.d/linux-firmware.conf`. После загрузки файл анализируется с помощью [systemd-tmpfiles-setup.service(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-tmpfiles-setup.service.8), а микрокод ЦП обновляется.

Для ручного обновления микрокода на запущенной системе запустите:

```
# echo 1 > /sys/devices/system/cpu/microcode/reload

```

Это позволяет применять обновления микрокода после обновления [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) без перезагрузки системы. Вы можете даже автоматизировать это с помощью [pacman hook](/index.php/Pacman_hook "Pacman hook"), например:

 `/etc/pacman.d/hooks/microcode_reload.hook` 
```
[Trigger]
Operation = Install
Operation = Upgrade
Operation = Remove
Type = File
Target = usr/lib/firmware/amd-ucode/*	

[Action]
Description = Applying CPU microcode updates...
When = PostTransaction
Depends = sh
Exec = /bin/sh -c 'echo 1 > /sys/devices/system/cpu/microcode/reload'
```

### Отключение позднего обновления микрокода

Для систем AMD микрокод процессора будет обновляться, даже если пакет [amd-ucode](https://www.archlinux.org/packages/?name=amd-ucode) не установлен, так как файлы предоставлены [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) ([FS#59840](https://bugs.archlinux.org/task/59840)). Чтобы отключить позднюю загрузку, вы должны переопределить [временные файлы](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Временные_файлы "Systemd (Русский)") `/usr/lib/tmpfiles.d/linux-firmware.conf`. Это можно сделать, создав файл с тем же именем в `/etc/tmpfiles.d/`:

```
# ln -s /dev/null /etc/tmpfiles.d/linux-firmware.conf

```

## Проверим, обновился ли microcode при загрузке

Чтобы убедиться, что микрокод обновился, воспользуемся *dmesg*:

```
$ dmesg | grep microcode

```

На системах Intel вы должны увидеть что-то похожее на это при каждой загрузке, что говорит о том, что микрокод обновился рано:

```
[    0.000000] CPU0 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.221951] CPU1 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.242064] CPU2 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.262349] CPU3 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.507267] microcode: CPU0 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507272] microcode: CPU1 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507276] microcode: CPU2 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507281] microcode: CPU3 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507286] microcode: CPU4 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507292] microcode: CPU5 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507296] microcode: CPU6 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507300] microcode: CPU7 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507335] microcode: Microcode Update Driver: v2.2.

```

**Примечание:** Отображаемая дата отвечает не за версию установленного пакета [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode). Это дата последнего обновления микрокода от Intel для вашего конкретного процессора.

Вполне возможно, особенно с новым аппаратным обеспечением, что для вашего CPU нет обновления микрокода. В этом случае вы можете увидеть примерно следующее:

```
[    0.292893] microcode: CPU0 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292899] microcode: CPU1 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292906] microcode: CPU2 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292912] microcode: CPU3 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292956] microcode: Microcode Update Driver: v2.2.

```

На системах AMD, использующих раннюю загрузку, вывод будет выглядеть примерно так:

```
[    2.119089] microcode: microcode updated early to new patch_level=0x0700010f
[    2.119157] microcode: CPU0: patch_level=0x0700010f
[    2.119171] microcode: CPU1: patch_level=0x0700010f
[    2.119183] microcode: CPU2: patch_level=0x0700010f
[    2.119189] microcode: CPU3: patch_lev
[    2.119269] microcode: Microcode Update Driver: v2.2.

```

На системах AMD, использующих позднюю загрузку, в выводе будет отображаться версия старого микрокода перед перезагрузкой микрокода, а новая - после перезагрузки. Это будет выглядеть примерно так:

```
[    2.112919] microcode: CPU0: patch_level=0x0700010b
[    2.112931] microcode: CPU1: patch_level=0x0700010b
[    2.112940] microcode: CPU2: patch_level=0x0700010b
[    2.112951] microcode: CPU3: patch_level=0x0700010b
[    2.113043] microcode: Microcode Update Driver: v2.2.
[    6.429109] microcode: CPU2: new patch_level=0x0700010f
[    6.430416] microcode: CPU0: new patch_level=0x0700010f
[    6.431722] microcode: CPU1: new patch_level=0x0700010f
[    6.433029] microcode: CPU3: new patch_level=0x0700010f
[    6.433073] x86/CPU: CPU features have changed after loading microcode, but might not take effect.

```

## Каким ЦП нужны обновления микрокода

Пользователи могут проконсультироваться как у Intel, так и у AMD насчёт поддержки конкретной модели процессора, перейдя по следующим ссылкам:

*   [Исследовательский центр операционной системы AMD (англ)](http://www.amd64.org/microcode.html).
*   [Центр загрузки Intel](https://downloadcenter.intel.com/SearchResult.aspx?lang=ru&keyword=processor%20microcode%20data%20file).

### Обнаружение доступного обновления микрокода

Вы можете узнать, содержит ли `intel-ucode.img` образ микрокода для вашего процессора с помощью [iucode-tool](https://www.archlinux.org/packages/?name=iucode-tool).

1.  Установите [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) (для обнаружения обновления не требуется менять initrd)
2.  Установите [iucode-tool](https://www.archlinux.org/packages/?name=iucode-tool)
3.  `# modprobe cpuid` 
4.  Извлекает образ микрокода и ищет в нём ваш cpuid:
     `# bsdtar -Oxf /boot/intel-ucode.img | iucode_tool -tb -lS -` 
5.  Если обновление доступно, оно должно отобразиться под *selected microcodes*
6.  Микрокод может уже быть в вашем биосе и его загрузка может не отображаться в dmesg. Сравните с текущим запуском микрокода {ic|grep microcode /proc/cpuinfo}}

## Применение ранней загрузки микрокода в кастомных ядрах

Для того, чтобы ранняя загрузка работала в кастомных ядрах, "CPU microcode loading support" должен быть вкомпилирован в ядро, а **не** скомпилирован как модуль. Это включает приглашение "Early load microcode", которое должно быть установлено в `Y`.

```
CONFIG_BLK_DEV_INITRD=Y
CONFIG_MICROCODE=y
CONFIG_MICROCODE_INTEL=Y
CONFIG_MICROCODE_AMD=y

```

## Смотрите также

*   [Обновление микрокодов - Опыт сообщества (англ)](https://flossexperiences.wordpress.com/2013/11/17/updating-microcodes/)
*   [Замечания по обновлению микрокода Intel - Ben Hawkes (англ)](http://inertiawar.com/microcode/)
*   [Загрузчик микрокода ядра - документация ядра (англ)](https://www.kernel.org/doc/Documentation/x86/microcode.txt)
*   [Erratum найден в Haswell/Broadwell – AnandTech (англ)](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly)
*   [проект iucode-tool на GitLab (англ)](https://gitlab.com/iucode-tool/iucode-tool)