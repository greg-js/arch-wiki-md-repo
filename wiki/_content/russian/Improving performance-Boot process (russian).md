Ссылки по теме

*   [Увеличение производительности](/index.php/%D0%A3%D0%B2%D0%B5%D0%BB%D0%B8%D1%87%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BF%D1%80%D0%BE%D0%B8%D0%B7%D0%B2%D0%BE%D0%B4%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D0%B8 "Увеличение производительности")
*   [Silent boot](/index.php/Silent_boot "Silent boot")
*   [Демоны](/index.php/%D0%94%D0%B5%D0%BC%D0%BE%D0%BD%D1%8B "Демоны")
*   [e4rat (Русский)](/index.php/E4rat_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "E4rat (Русский)")
*   [Kexec](/index.php/Kexec "Kexec")

## Contents

*   [1 Предисловие](#.D0.9F.D1.80.D0.B5.D0.B4.D0.B8.D1.81.D0.BB.D0.BE.D0.B2.D0.B8.D0.B5)
*   [2 Изменение загрузочных файлов](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BE.D1.87.D0.BD.D1.8B.D1.85_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2)
    *   [2.1 /boot/grub/menu.lst](#.2Fboot.2Fgrub.2Fmenu.lst)
    *   [2.2 /etc/mkinitcpio.conf](#.2Fetc.2Fmkinitcpio.conf)
*   [3 См. также](#.D0.A1.D0.BC._.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Предисловие

Ускорение загрузки системы может быть обеспечено уменьшением время ожидания и изучением того как взаимодействуют некоторые системные файлы и скрипты. В этой статье сделана попытка описать способы уменьшения времени загрузки системы.

## Изменение загрузочных файлов

### /boot/grub/menu.lst

Удалите параметр разрешения <tt>vga=</tt> [framebuffer](https://en.wikipedia.org/wiki/Framebuffer "wikipedia:Framebuffer") и добавьте [fastboot](http://lwn.net/Articles/314808/) и [quiet](http://www.kernel.org/doc/Documentation/kernel-parameters.txt) в параметры загрузки ядра:

```
kernel /vmlinuz26 root=/dev/disk/by-uuid/UUID ro fastboot quiet

```

### /etc/mkinitcpio.conf

Удалите HOOKS, которые вам не нужны и рассмотрите возможность использования только base (иногда udev также необходим), а также необходимые MODULES для вашего корневого раздела (и клавиатуры, вместо USBInput).

Больше информации можно узнать в [этой статье](/index.php/Mkinitcpio "Mkinitcpio").

## См. также

[Systemd](/index.php/Systemd "Systemd")