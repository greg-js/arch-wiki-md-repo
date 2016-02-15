**Состояние перевода:** На этой странице представлен перевод статьи [Microcode](/index.php/Microcode "Microcode"). Дата последней синхронизации: 2015-07-29\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Microcode&diff=0&oldid=387099).

Производители процессоров выпускают обновления стабильности и безопасности для [микрокода](https://en.wikipedia.org/wiki/ru:%D0%9C%D0%B8%D0%BA%D1%80%D0%BE%D0%BA%D0%BE%D0%B4 "wikipedia:ru:Микрокод") процессора. Несмотря на то, что микрокод можно обновить с помощью BIOS, ядро Linux также может применять эти обновления во время загрузки. Эти обновления предоставляют исправления ошибок, которые могут быть критичны для стабильности вашей системы. Без этих обновлений вы можете наблюдать ложные падения или неожиданные зависания системы, которые может быть сложно отследить.

Особенно пользователи процессоров семейства Intel Haswell и Broadwell должны установить эти обновления, чтобы обеспечить стабильность системы. Но, понятное дело, все пользователи Intel должны устанавливать эти обновления.

## Contents

*   [1 Обновление микрокода](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D0.BA.D0.BE.D0.B4.D0.B0)
    *   [1.1 Применение обновлений микрокода Intel](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D0.BA.D0.BE.D0.B4.D0.B0_Intel)
    *   [1.2 Конкретные примеры](#.D0.9A.D0.BE.D0.BD.D0.BA.D1.80.D0.B5.D1.82.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B)
        *   [1.2.1 EFI boot stub / EFI handover](#EFI_boot_stub_.2F_EFI_handover)
        *   [1.2.2 systemd-boot](#systemd-boot)
        *   [1.2.3 rEFInd](#rEFInd)
        *   [1.2.4 Grub](#Grub)
        *   [1.2.5 Syslinux](#Syslinux)
*   [2 Проверим, обновился ли microcode при загрузке](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.B8.D0.BC.2C_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.B8.D0.BB.D1.81.D1.8F_.D0.BB.D0.B8_microcode_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5)
*   [3 Каким CPU нужны обновления микрокода](#.D0.9A.D0.B0.D0.BA.D0.B8.D0.BC_CPU_.D0.BD.D1.83.D0.B6.D0.BD.D1.8B_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D0.BA.D0.BE.D0.B4.D0.B0)
    *   [3.1 Обнаружение доступного обновления микрокода](#.D0.9E.D0.B1.D0.BD.D0.B0.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D0.BA.D0.BE.D0.B4.D0.B0)
*   [4 Применение ранней загрузки микрокода Intel в кастомных ядрах](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.BD.D0.BD.D0.B5.D0.B9_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D0.BA.D0.BE.D0.B4.D0.B0_Intel_.D0.B2_.D0.BA.D0.B0.D1.81.D1.82.D0.BE.D0.BC.D0.BD.D1.8B.D1.85_.D1.8F.D0.B4.D1.80.D0.B0.D1.85)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Обновление микрокода

Для процессоров AMD обновления микрокода поставляются в пакете [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware), который был установлен как часть базовой системы. Дальнейших действий не требуется.

Для процессоров Intel [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) и продолжайте читать.

### Применение обновлений микрокода Intel

Микрокод должен быть загружен загрузчиком. Из-за большого разнообразия конфигураций ранней загрузки у пользователей обновления микрокода Intel могут быть не применены автоматически конфигурацией Arch по умолчанию. Многие ядра в AUR пошли по пути официальных Arch ядер в этом вопросе.

Чтобы применить эти обновления, добавьте `/boot/intel-ucode.img` в качестве первого initrd в конфигурационном файле загрузчика. Это в дополнение к обычному initrd файлу. Смотрите ниже инструкции для популярных загрузчиков.

### Конкретные примеры

#### EFI boot stub / EFI handover

Добавьте две `initrd=` опции:

 `initrd=/intel-ucode.img initrd=/initramfs-linux.img` 

#### systemd-boot

Используйте `initrd` опцию дважды в `/boot/loader/entries/*.conf`:

```
title   Arch Linux
linux   /vmlinuz-linux
initrd  /intel-ucode.img
initrd  /initramfs-linux.img
options ...

```

#### rEFInd

Отредактируйте опции загрузки в `/boot/refind_linux.conf` также как в примере EFI boot stub выше:

```
"Boot with standard options" "ro root=UUID=(...) quiet initrd=intel-ucode.img initrd=initramfs-linux.img"

```

Пользователи, которые создают строфы вручную в `/boot/refind.conf` для определения ядер должны просто добавить `initrd=/intel-ucode.img` или `/boot/intel-ucode.img` как это требуется в строке опций, а не в главной части строфы.

#### Grub

_grub-mkconfig_ автоматически обнаружит обновление микрокода и соответствующе сконфигурирует grub. После установки пакета [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) пользователи должны пересоздать конфигурацию grub для активации загрузки обновления микрокода, выполнив команду:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

В качестве альтернативы, пользователи, которые вручную управляют файлом конфигурации grub могут добавить `/intel-ucode.img` или `/boot/intel-ucode.img` в `grub.cfg` как показано ниже:

```
[...]
    echo	'Loading initial ramdisk ...'
    initrd	/intel-ucode.img /initramfs-linux.img
[...]

```

Проделайте это для всех пунктов меню.

**Важно:** Этот файл будет автоматически перезаписан `/usr/bin/grub-mkconfig`'ом во время определённых обновлений, затирая ваши изменения. Настоятельно рекомендуется использовать директорию конфигурации в `/etc/grub.d` для управления нужной вам конфигурацией grub.

#### Syslinux

**Обратите внимание:** Между указаниями файлов initrd (`intel-ucode` и `initramfs-linux`) не должно быть пробелов. Точки здесь вовсе не означают каких-либо сокращений или пропущенного кода: все должно быть указано ровно так, как показано в примере.

Несколько файлов initrd могут быть разделены запятыми в `/boot/syslinux/syslinux.cfg`:

```
LABEL arch
    MENU LABEL Arch Linux
    LINUX ../vmlinuz-linux
    INITRD ../intel-ucode.img,../initramfs-linux.img
    APPEND ...

```

## Проверим, обновился ли microcode при загрузке

Чтобы убедиться, что микрокод обновился, воспользуемся `/usr/bin/dmesg`:

```
$ dmesg | grep microcode

```

На системах Intel вы должны увидеть что-то похожее на это, что говорит о том, что микрокод обновился рано:

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
[    0.507335] microcode: Microcode Update Driver: v2.00 <tigran@aivazian.fsnet.co.uk>, Peter Oruba

```

Вполне возможно, особенно с новым аппаратным обеспечением, что для вашего CPU нет обновления микрокода. В этом случае вы можете увидеть примерно следующее:

```
[    0.292893] microcode: CPU0 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292899] microcode: CPU1 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292906] microcode: CPU2 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292912] microcode: CPU3 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292956] microcode: Microcode Update Driver: v2.00 <tigran@aivazian.fsnet.co.uk>, Peter Oruba

```

На системах AMD микрокод обновляется несколько позже в процессе загрузки, поэтому вывод выглядит примерно так:

```
[    0.807879] microcode: CPU0: patch_level=0x01000098
[    0.807888] microcode: CPU1: patch_level=0x01000098
[    0.807983] microcode: Microcode Update Driver: v2.00 <tigran@aivazian.fsnet.co.uk>, Peter Oruba
[   16.150642] microcode: CPU0: new patch_level=0x010000c7
[   16.150682] microcode: CPU1: new patch_level=0x010000c7

```

**Обратите внимание:** Отображаемая дата отвечает не за версию установленного пакета [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode). Это дата последнего обновления микрокода от Intel для вашего конкретного процессора.

## Каким CPU нужны обновления микрокода

Пользователи могут проконсультироваться как у Intel, так и у AMD насчёт поддержки конкретной модели процессора, перейдя по следующим ссылкам:

*   [AMD's Operating System Research Center](http://www.amd64.org/microcode.html).
*   [Центр загрузки Intel](https://downloadcenter.intel.com/Detail_Desc.aspx?DwnldID=24290&lang=rus).

### Обнаружение доступного обновления микрокода

Вы можете узнать, содержит ли `intel-ucode.img` образ микрокода для вашего процессора с помощью [iucode-tool](https://aur.archlinux.org/packages/iucode-tool/).

*   Установите [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) (для обнаружения обновления не требуется менять initrd)
*   Установите [iucode-tool](https://aur.archlinux.org/packages/iucode-tool/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)")
*   `# modprobe cpuid`
*   `# bsdtar -Oxf /boot/intel-ucode.img | iucode_tool -tb -lS -`

	(Команда извлекает образ микрокода и ищет в нём ваш cpuid)

*   Если обновление доступно, оно должно отобразиться под _selected microcodes_

## Применение ранней загрузки микрокода Intel в кастомных ядрах

Для того, чтобы ранняя загрузка работала в кастомных ядрах, "CPU microcode loading support" должен быть вкомпилирован в ядро, а НЕ скомпилирован как модуль. Это активирует "Early load microcode" промпт, который должен быть установлен в "Y".

```
CONFIG_MICROCODE=y
CONFIG_MICROCODE_INTEL=y
CONFIG_MICROCODE_INTEL_EARLY=y
CONFIG_MICROCODE_EARLY=y

```

## Смотрите также

*   [Updating microcodes](https://flossexperiences.wordpress.com/2013/11/17/updating-microcodes/)
*   [Notes on Intel Microcode updates](http://inertiawar.com/microcode/)
*   [Kernel early microcode](https://www.kernel.org/doc/Documentation/x86/early-microcode.txt)
*   [Erratum found in Haswell/Broadwell](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly)