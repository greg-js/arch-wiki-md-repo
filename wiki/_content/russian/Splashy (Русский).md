[Splashy](http://splashy.alioth.debian.org) это пользовательская реализация экранной заставки при загрузке Линукс, использующая графическую среду предоставляемую [directfb](http://www.directfb.org).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Конфигурирование](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [2.1 /boot/grub/menu.lst](#.2Fboot.2Fgrub.2Fmenu.lst)
    *   [2.2 /etc/rc.conf](#.2Fetc.2Frc.conf)
    *   [2.3 /etc/mkinitcpio.conf](#.2Fetc.2Fmkinitcpio.conf)
    *   [2.4 Модернизация(апгрейд)](#.D0.9C.D0.BE.D0.B4.D0.B5.D1.80.D0.BD.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F.28.D0.B0.D0.BF.D0.B3.D1.80.D0.B5.D0.B9.D0.B4.29)
*   [3 Известные проблемы](#.D0.98.D0.B7.D0.B2.D0.B5.D1.81.D1.82.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B)
*   [4 Ссылки](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

# Установка

1.  Загрузите [пакет](https://aur.archlinux.org/packages.php?do_Details=1&ID=10211) в AUR, создайте его с помощью makepkg (или любой другой заменой makepkg, которая вам нравится) и установите с помощью Pacman.

**Внимание!** "initscripts-splash" теперь зависят от splashy. Они заменяют "initscripts", поэтому некоторые файлы в /etc будут сохранены как *.pacsave.

# Конфигурирование

#### /boot/grub/menu.lst

Добавьте **quiet vga=791 splash** к командной строке вашего ядра в _/boot/grub/menu.lst_. Т.е.:

```
kernel (hd0,6)/vmlinuz26 root=/dev/sda6 ro quiet vga=791 splash

```

#### /etc/rc.conf

Добавьте SPLASH="splashy" в _/etc/rc.conf_. Т.е.:

```
SPLASH="splashy"

```

#### /etc/mkinitcpio.conf

*   **Не забудьте пересоздать initramfs образ после того, как изменилась конфигурация Splashy.** (например, когда изменили тему Splashy)

1.  Добавьте **splashy** в **конец** строки HOOKS в файле _/etc/mkinitcpio.conf_. Т.е.: `HOOKS="base udev autodetect ide sata filesystems ... splashy"` 
2.  Пересоздайте загрузочный образ ядра `# mkinitcpio -p <имя ядра>` Например: `# mkinitcpio -p linux` 

### Модернизация(апгрейд)

*   Не забудьте пересоздать initramfs образ после апгрейда Splashy.

# Известные проблемы

1.  Splashy не сбрасывается и не переключается автоматически в режим обзора при возникновении ошибки или при отказе инициализационного скрипта.
2.  Возникает неприятная ситуация, когда при запущенном Splashy происходит вынужденная проверка файловой системы. В некоторых неопределенных случаях (на текущий момент) система перезагружается после отрабатывания команды fsck.
3.  Система X-Window может отображать артефакты на экране, если splashy активна при загрузке.

# Ссылки

*   [http://splashy.alioth.debian.org](http://splashy.alioth.debian.org)
*   [http://www.directfb.org](http://www.directfb.org)