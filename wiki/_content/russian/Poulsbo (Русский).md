Набор микросхем **US15W**, точнее Intel® System Controller Hub (Intel® SCH) US15W, более известный как **Poulsbo**-чипсет со встроенным графическим адаптером **GMA 500** используется в современных нетбуках. По замыслу производителя, данный графический ускоритель должен прекрасно воспроизводить FullHD видео. Не так давно появился драйвер данного устройства для ОС Linux, в частности для Arch Linux.

Данный драйвер работает корректно только с ядром Linux версии 2.6.31 и X.org сервером 1.6.

## Contents

*   [1 Установка Xorg сервер 1.6](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_Xorg_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80_1.6)
    *   [1.1 Installing the FBDEV Xorg framebuffer driver](#Installing_the_FBDEV_Xorg_framebuffer_driver)
    *   [1.2 Решение проблем X.org 1.6](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC_X.org_1.6)
        *   [1.2.1 Драйвер не может быть найден](#.D0.94.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80_.D0.BD.D0.B5_.D0.BC.D0.BE.D0.B6.D0.B5.D1.82_.D0.B1.D1.8B.D1.82.D1.8C_.D0.BD.D0.B0.D0.B9.D0.B4.D0.B5.D0.BD)
*   [2 Choosing between psb and IEGD driver](#Choosing_between_psb_and_IEGD_driver)

## Установка Xorg сервер 1.6

**Пожалуйста учтите, что Xorg сервер 1.6 официально не поддерживается Arch Linux**

На текущий момент файлы Xorg 1.6 для платформы i686 доступны на следующих сайтах:

*   [Chakra Project's xorg-old repository](http://chakra-project.org/repo/xorg-old/i686/)
*   [A mirror of the repository](http://kdemod.iskrembilen.com/xorg-old/i686/)

Скачайте приведенные нужные файлы с одного из предложенных репозитариев. Для простого обращения с ними, рекомендуется сохранить их в отдельную папку.

*   xorg-server-1.6.3.901-1-i686.pkg.tar.gz
*   xf86-input-evdev-2.2.5-1-i686.pkg.tar.gz
*   xf86-input-keyboard-1.3.2-2-i686.pkg.tar.gz
*   xf86-input-mouse-1.4.0-2-i686.pkg.tar.gz
*   xf86-input-synaptics-1.1.3-1-i686.pkg.tar.gz
*   xf86-video-vesa-2.2.0-1-i686.pkg.tar.gz

Запустите окно терминала и выполните следующие команды:

```
sudo pacman -R xorg-server xf86-input-evdev xf86-input-mouse xf86-input-synaptics xf86-input-keyboard xf86-video-vesa xf86-video-fbdev
sudo pacman -U xf86-input-evdev-2.2.5-1-i686.pkg.tar.gz xorg-server-1.6.3.901-1-i686.pkg.tar.gz \
     xf86-input-keyboard-1.3.2-2-i686.pkg.tar.gz xf86-input-mouse-1.4.0-2-i686.pkg.tar.gz \
     xf86-input-synaptics-1.1.3-1-i686.pkg.tar.gz xf86-video-vesa-2.2.0-1-i686.pkg.tar.gz

```

Вторую команду можно вводить без разделения бэкслешами в одну строку. The second command may be entered as one line, without the backslashes.

Далее текст еще не переведён. Пожалуйста, обратитесь к английскому варианту статьи.

Еще потребуется более An older version of libssl is also needed. This requirement can be fufilled with the openssl-compatibility package from the [Arch User Repository (Русский)](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"). You must have the [prerequisites](/index.php/Arch_User_Repository#Prerequisites "Arch User Repository") installed to build this.

```
mkdir openssl-compatibility
cd openssl-compatibility
wget http://aur.archlinux.org/packages/openssl-compatibility/openssl-compatibility/PKGBUILD
makepkg -s
sudo pacman -U openssl-compatibility*.pkg.tar.xz

```

После этого перезагрузитесь либо закройте все инстансы X.org и введите

```
startx

```

The Xorg 1.6 server should start without issue.

### Installing the FBDEV Xorg framebuffer driver

Использование драйвера FBDEV driver даёт немного лучший performance, чем использование голого драйвера VESA. It is not, however, currently in the Chakra Project's repositories. Fortunately an Arch user found the package in his backups, and has posted it online at [http://drop.io/hh6gtvv](http://drop.io/hh6gtvv). Feel free to download it, but please do not abuse the URL given below (via multiple-threaded download or otherwise) as the traffic limit is currently unknown.

Go to the site with a web browser that supports JavaScript and download the file. Then run

```
sudo pacman -U xf86-video-fbdev-0.4.1-1-i686.pkg.tar.gz

```

to install the FBDEV driver.

### Решение проблем X.org 1.6

#### Драйвер не может быть найден

If it complains that the driver cannot be found, you probably have the FBDEV driver specified in your /etc/X11/xorg.conf file, but didn't install the FBDEV driver as described [above](/index.php/Poulsbo#Installing_the_FBDEV_Xorg_framebuffer_driver "Poulsbo") . Change the

```
Driver "fbdev"

```

line to

```
Driver "vesa"

```

and everything should be fine.

## Choosing between psb and IEGD driver

The Intel Embedded Graphics Driver is the more recent driver, and is updated upstream. Intel does **not** support it on Arch Linux. There are efforts underway by users to adapt the driver and create a PKGBUILD, but these are still incomplete and experimental at this time. At this time, the IEGD driver [is not thread-safe](http://community.edc.intel.com/t5/Software-Tools-Discussions/IEGD-10-3-VA-is-NOT-thread-safe-crashing-on-iegd-drv-video-so/m-p/2366), and does not support suspend-to-RAM.

The older driver, commonly referred to as "the GMA500 driver", "the PSB driver", or "the old Poulsbo driver", was produced by a different part of the Intel corporation. It provides less performance than the IEGD driver, and in Arch only works with kernels <=2.6.31, but is much less of a headache to install.