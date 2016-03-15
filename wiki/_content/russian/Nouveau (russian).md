[[1]](http://nouveau.freedesktop.org/wiki/Nouveau) - это свободный (Open Source) видеодрайвер для карт NVIDIA, разрабатываемый без поддержки самой NVIDIA и в противоположность [проприетарному драйверу](/index.php/NVIDIA "NVIDIA"). В [FAQ проекта](http://nouveau.freedesktop.org/wiki/FAQ) содержится достаточно много ценной информации, поэтому имеет смысл в том числе ознакомиться и с ним.

Прежде чем устанавливать драйвер, изучите [таблицу возможностей](http://nouveau.freedesktop.org/wiki/FeatureMatrix) драйвера Nouveau для вашего графического чипа. Его название можно определить по модели видеокарты с помощью [список кодовых имён](http://nouveau.freedesktop.org/wiki/CodeNames).

Также примите во внимание [список GPU NVIDIA](https://en.wikipedia.org/wiki/Comparison_of_Nvidia_Graphics_Processing_Units "wikipedia:Comparison of Nvidia Graphics Processing Units") в Википедии.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Загрузка](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [4 KMS](#KMS)
    *   [4.1 Отложенный запуск](#.D0.9E.D1.82.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.BD.D1.8B.D0.B9_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
    *   [4.2 Быстрый запуск](#.D0.91.D1.8B.D1.81.D1.82.D1.80.D1.8B.D0.B9_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [5 Альтернативная установка](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [6 3D](#3D)
*   [7 DualHead](#DualHead)
*   [8 Примеры исправления проблем](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_.D0.B8.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [8.1 Виртуальное разрешение консоли не соответствует реальному](#.D0.92.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B5_.D1.80.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D0.B8_.D0.BD.D0.B5_.D1.81.D0.BE.D0.BE.D1.82.D0.B2.D0.B5.D1.82.D1.81.D1.82.D0.B2.D1.83.D0.B5.D1.82_.D1.80.D0.B5.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.BC.D1.83)

## Установка

Перед установкой драйвера Nouveau следует удалить официальный графический драйвер NVIDIA и очистить файл `/etc/X11/xorg.conf`, созданный этим драйвером.

**Tip:** Можно сохранить официальный драйвер NVIDIA, но потребуется [настроить систему](#Keep_NVIDIA_driver_installed) на загрузку драйвера Nouveau вместо официального.

Следующие две команды заменят стек драйверов NVIDIA (модуль ядра, реализацию LibGL и GLX) свободной версией LibGL из проекта Mesa.

```
# pacman -Rdds nvidia nvidia-utils
# pacman -S --asdeps libgl

```

Затем следует установить новый драйвер DDX ([xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau)) и соответствующий драйвер Mesa (для аппаратной поддержки 3D-рендеринга):

```
# pacman -S xf86-video-nouveau nouveau-dri

```

Для Arch x86_64, установите также пакет [lib32-nouveau-dri](https://www.archlinux.org/packages/?name=lib32-nouveau-dri) из репозитория [Multilib](/index.php/Multilib "Multilib").

По состоянию на [2010-02-25](http://cgit.freedesktop.org/nouveau/linux-2.6/commit/?id=d5f3c90d4f3ad6b054f9855b7b69137b97bda131), nouveau автоматически генерирует прошивку для nv50\. Пакет [nouveau-firmware](https://www.archlinux.org/packages/?name=nouveau-firmware) больше не требуется для любых видеокарт с [nouveau-drm](https://www.archlinux.org/packages/?name=nouveau-drm) новее, чем 0.0.15_20100313-1.

## Загрузка

Модуль ядра nouveau должен загрузиться автоматически при старте системы.

Если это не случилось, проверьте следуещее:

*   **Нет** [опций загрузки ядра](/index.php/Kernel_parameters "Kernel parameters") таких, как `nomodeset` или `vga=` .
*   Нет blacklisting-а для nouveau в `/etc/modprobe.d/`.

## Настройка

Add the following to the file `/etc/X11/xorg.conf.d/20-nouveau.conf`, which is required to ensure that Nouveau loads instead of the vesa driver. This also allows you to easily switch back to other drivers.

```
Section "Device"
       Identifier "nvidia"
       Driver "nouveau"
       #Driver "nv"
       #Driver "nvidia"
EndSection

```

## KMS

Kernel Mode-Setting ([KMS](/index.php/KMS "KMS")) поддерживается драйвером nouveau. Upstream рекомендует испльзование и тестирование этого режима, так как в будущем он будет использоваться по умолчанию для всех графических чипсетов. Просмотрите страницу [KernelModeSetting](http://nouveau.freedesktop.org/wiki/KernelModeSetting) для дополнительной информации.

Начиная с [2009-12-11](http://cgit.freedesktop.org/nouveau/linux-2.6/commit/?id=8fb5c3ada2678defb0351e8b155c564471da05a7), KMS включен по умолчанию (nouveau-drm 0.0.15_20091220-1 и выше). Вы можете отключить KMS, указав опцию nouveau.modeset=0 в строке параметров ядра, однако учтите, что начиная с [2010-01-10](http://cgit.freedesktop.org/nouveau/xf86-video-nouveau/commit/?id=17485c234ff191cee3dd19e3dd693a80b024e189) (xf86-video-nouveau 0.0.15_git20100117-1 и выше) в драйвере xorg удалена поддержка работы без KMS.

### Отложенный запуск

В случае позднего старта KMS будет включен на стадии загрузки "Loading modules." Это может привести к пропаданию изображения во время установки видеорежима.

Удалите опции "vga=" и "video=" из строки параметров ядра в файле `/boot/grub/menu.lst`. Использование других драйверов фреймбуфера (таки как uvesafb) вызовет конфликт с KMS.

### Быстрый запуск

**Важно:** Если у вас появляются проблемы с драйвером nouveau или если Вы часто пересобираете пакет nouveau-drm в целях тестирования и отладки, не добавляйте модуль nouveau в initramfs. Легко забыть пересобрать initramfs при обновлении nouveau - это может усложнить тестирование. Используйте *Отложенный запуск*. Также могут возникнуть сложности с initramfs, если Вам понадобится firmware для семейства nv50.

Этото метод запускает KMS рано, насколько это возможно, когда загружается [initramfs](/index.php/Initramfs "Initramfs"). Далее описано как настроить это используя официальные пакеты:

1) Добавьте "nouveau" в массив *MODULES* в файле `/etc/mkinitcpio.conf`:

```
MODULES="**nouveau** ..."

```

2) Добавьте "/etc/modprobe.d/modprobe.conf" в секцию FILES в `/etc/mkinitcpio.conf`:

```
FILES="/etc/modprobe.d/modprobe.conf"

```

3) Пересоберите ваш образ initrd:

```
# mkinitcpio -p <*ваш профиль ядра (kernel26, etc.)*>

```

<small>Вы также можете просмотреть инструкцию для видеокарт [Intel](/index.php/Intel "Intel"): [Intel Graphics:KMS (Kernel Mode Setting)](/index.php/Intel#KMS_.28Kernel_Mode_Setting.29 "Intel")</small>

## Альтернативная установка

If the official Arch Linux packages do not work, you can try a more current video driver from the [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"): [xf86-video-nouveau-git](https://aur.archlinux.org/packages/xf86-video-nouveau-git/). A more up-to-date DRM module can be built by using the [nouveau-drm](https://www.archlinux.org/packages/?name=nouveau-drm) PKGBUILD from [ABS](/index.php/Arch_Build_System_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Build System (Русский)"). Simply update `_snapdate` to the current date, and modify the `sources` array to read:

```
source=(# [ftp://ftp.archlinux.org/other/$pkgname/master-${_snapdate}.tar.gz](ftp://ftp.archlinux.org/other/$pkgname/master-${_snapdate}.tar.gz)
        [http://people.freedesktop.org/~pq/nouveau-drm/master.tar.gz](http://people.freedesktop.org/~pq/nouveau-drm/master.tar.gz)
        # get the Makefile from [http://cgit.freedesktop.org/nouveau/linux-2.6/plain/nouveau/Makefile?h=master-compat](http://cgit.freedesktop.org/nouveau/linux-2.6/plain/nouveau/Makefile?h=master-compat)
        Makefile)

```

You can use [kernel26-nouveau-git](https://aur.archlinux.org/packages/kernel26-nouveau-git/) to compile the nouveau project's kernel tree, which already includes the necessary modules. This is the method recommended by upstream.

## 3D

3D *не поддерживается*.

[Исходя из этого](http://www.linux.org.ru/forum/talks/8671256) и [из этого](http://nouveau.freedesktop.org/wiki/FeatureMatrix/) всё таки **3D** поддерживается **FIXME**

Это значит:

*   Не спрашивайте инструкции чтобы проверить это.
*   Не устанавливайте драйвер 3D в систему.
*   Если Вы хотите проверить 3D ускорение или имеете проблемы с этим, делайте на свой риск, за исключением если Вы хотите сделать вклад с помощью патчев.

Ссылки: [домашняя страница Nouveau](http://nouveau.freedesktop.org/wiki/FrontPage) и [Nouveau ЧаВо](http://nouveau.freedesktop.org/wiki/FAQ#head-ae99a8e6a3f57b76ae2589d4c0d2a5fa7ebf9f5d)

## DualHead

Nouveau поддерживает расширение xrandr для установки режимов и поддержки нескольких мониторов. Смотрите страницу [RandR12](/index.php/RandR12 "RandR12") для примеров.

Пример полного файла `/etc/X11/xorg.conf` для работы с двумя мониторами. Вы можете использовать графические утилиты такие как gnome-display-properties (System -> Preferences -> Display) для настройки.

```
# the right one
Section "Monitor"
          Identifier   "NEC"
          Option "PreferredMode" "1280x1024_60.00"
EndSection

# the left one
Section "Monitor"
          Identifier   "FUS"
          Option "PreferredMode" "1280x1024_60.00"
          Option "LeftOf" "NEC"
EndSection

Section "Device"
    Identifier "nvidia card"
    Driver "nouveau"
    Option  "Monitor-DVI-I-0" "NEC"
    Option  "Monitor-DVI-I-1" "FUS"
    #Option "AccelMethod" "XAA"
EndSection

Section "Screen"
    Identifier "screen1"
    DefaultDepth 24
      SubSection "Display"
       Depth      24
       Virtual 2560 1024
      EndSubSection
    Device "nvidia card"
EndSection

Section "ServerLayout"
    Identifier "layout1"
    Screen "screen1"
    # will be replaced by gallium 3D
    Option "AIGLX" "false"
EndSection

```

## Примеры исправления проблем

### Виртуальное разрешение консоли не соответствует реальному

Используйте [fbset](https://www.archlinux.org/packages/?name=fbset) чтобы отрегулировать разрешение консоли.