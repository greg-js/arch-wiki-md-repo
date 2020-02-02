Этот документ пояснит вам как установить, настроить, и использовать Fbsplash.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Установка и Настройка](#Установка_и_Настройка)
    *   [2.1 /boot/grub/grub.cfg](#/boot/grub/grub.cfg)
    *   [2.2 /etc/mkinitcpio.conf](#/etc/mkinitcpio.conf)
    *   [2.3 Декорация консоли](#Декорация_консоли)
*   [3 Обновление](#Обновление)
*   [4 Используйте :D](#Используйте_:D)

### Установка

Возьмите [fbsplash](https://aur.archlinux.org/packages.php?do_Details=1&ID=10211), [fbsplash-theme-arch-black](https://aur.archlinux.org/packages/fbsplash-theme-arch-black/), из AUR и соберите пакеты с помощью makepkg (или любой другой оболочкой для makepkg, которая вам по вкусу) и установите с помощью pacman-а.

### Установка и Настройка

#### /boot/grub/grub.cfg

Добавьте **ro logo.nologo quiet nomodeset vga=792 console=tty1 splash=silent,fadein,fadeout,theme:arch-black** в файл */boot/grub/grub.cfg*. напр.:

```
kernel (hd0,6)/vmlinuz26 root=/dev/sda6 ro logo.nologo quiet nomodeset vga=792 console=tty1 splash=silent,fadein,fadeout,theme:arch-black

```

logo.nologo - не показывать стандартное лого

nomodeset vga=792 - используя framebuffer выставить в консоли разрешение 1024х768

console=tty1 - перенаправит сообщения ядра и initscripts на tty1

splash=silent - режим загрузки при котором вся загрузка спрятана под картинкой, splash=verbose - показывает полный вывод загруки

fadein - красивый эффект, загрузочная картинка появляется из темноты ( в начале загрузки)

fadeout - красивый эффект, загрузочная картинка уходит в темноту ( в конце загрузки)

theme:arch-black - тема загруки

Все настройки хранятся в файле /etc/conf.d/splash. Прописываем нашу тему

```
SPLASH_THEMES="
   arch-black
   arch-black/1024x768.cfg 
"

```

#### /etc/mkinitcpio.conf

*   **Не забудьте пересобрать initramfs image после изменения конфигурации fbsplash.** (например, тема fbsplash изменилась)

1.  Добавьте **fbsplash** в **конец** HOOKS в */etc/mkinitcpio.conf*. напр.: `HOOKS="base udev autodetect ide sata filesystems ... fbsplash"` 
2.  Пересоберите образ ядра `# mkinitcpio -p <kernel name>` e.g. `# mkinitcpio -p linux` 

#### Декорация консоли

Для поддержки фона в консоли нужно установить патченное ядро. Просто [найдите fbcondecor в AUR](https://aur.archlinux.org/packages.php?O=0&K=fbcondecor&do_Search=Go). Соберите и установите. Затем добавьте *fbcondecor* в список Ваших демонов в rc.conf:

```
DAEMONS=(... fbcondecor ...)

```

Файл конфигурации находиться в /etc/conf.d/fbcondecor.

### Обновление

*   Не забудьте пересобрать образ initramfs после апгрейда fbsplash.

### Используйте :D

*   Shutdown
*   Boot up
*   Reboot