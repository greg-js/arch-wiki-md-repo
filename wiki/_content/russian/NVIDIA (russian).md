**Состояние перевода:** На этой странице представлен перевод статьи [NVIDIA](/index.php/NVIDIA "NVIDIA"). Дата последней синхронизации: 22 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=NVIDIA&diff=0&oldid=427168).

Данная статья описывает процесс установки и настройки проприетарного драйвера графических карт [NVIDIA](http://www.nvidia.com). Для получения информации о драйверах с открытым исходным кодом обратитесь к статье [Nouveau (Русский)](/index.php/Nouveau_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nouveau (Русский)"). Также есть отдельная статья для обладателей ноутбуков с технологиями на базе [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus").

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Не поддерживаемые драйвера](#.D0.9D.D0.B5_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0)
    *   [1.2 Альтернативная установка: собственное ядро](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0:_.D1.81.D0.BE.D0.B1.D1.81.D1.82.D0.B2.D0.B5.D0.BD.D0.BD.D0.BE.D0.B5_.D1.8F.D0.B4.D1.80.D0.BE)
        *   [1.2.1 Автоматическая пересборка модуля NVIDIA при обновлении ядра](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B0.D1.8F_.D0.BF.D0.B5.D1.80.D0.B5.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B0_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D1.8F_NVIDIA_.D0.BF.D1.80.D0.B8_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B8_.D1.8F.D0.B4.D1.80.D0.B0)
    *   [1.3 Pure Video HD (VDPAU/VAAPI)](#Pure_Video_HD_.28VDPAU.2FVAAPI.29)
    *   [1.4 Аппаратное ускорение декодирования видео с помощью XvMC](#.D0.90.D0.BF.D0.BF.D0.B0.D1.80.D0.B0.D1.82.D0.BD.D0.BE.D0.B5_.D1.83.D1.81.D0.BA.D0.BE.D1.80.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B4.D0.B5.D0.BA.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_XvMC)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Минимальная настройка](#.D0.9C.D0.B8.D0.BD.D0.B8.D0.BC.D0.B0.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.2 Автоматическая настройка](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.3 NVIDIA Settings](#NVIDIA_Settings)
    *   [2.4 Несколько мониторов](#.D0.9D.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.BE.D0.B2)
        *   [2.4.1 Использование NVIDIA Settings](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_NVIDIA_Settings)
        *   [2.4.2 ConnectedMonitor](#ConnectedMonitor)
        *   [2.4.3 TwinView](#TwinView)
            *   [2.4.3.1 Ручная конфигурация из командной строки с использованием xrandr](#.D0.A0.D1.83.D1.87.D0.BD.D0.B0.D1.8F_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D0.B8.D0.B7_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.BD.D0.BE.D0.B9_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B8_.D1.81_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC_xrandr)
            *   [2.4.3.2 Vertical sync using TwinView](#Vertical_sync_using_TwinView)
            *   [2.4.3.3 Gaming using TwinView](#Gaming_using_TwinView)
        *   [2.4.4 Режим Mosaic](#.D0.A0.D0.B5.D0.B6.D0.B8.D0.BC_Mosaic)
            *   [2.4.4.1 Base Mosaic](#Base_Mosaic)
            *   [2.4.4.2 SLI Mosaic](#SLI_Mosaic)
    *   [2.5 Драйвер Persistence](#.D0.94.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80_Persistence)
*   [3 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

**Важно:** Избегайте установки пакета драйвера с сайта NVIDIA. Установка через [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)"), позволяет обновлять драйвер вместе с остальной системой.

Данная инструкция предназначена для предоставляемых в дистрибутиве пакетов ядра [linux](https://www.archlinux.org/packages/?name=linux) или [linux-lts](https://www.archlinux.org/packages/?name=linux-lts). Для пользователей ядра, собранного самостоятельно, следует обратится к [следующему](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0:_.D1.81.D0.BE.D0.B1.D1.81.D1.82.D0.B2.D0.B5.D0.BD.D0.BD.D0.BE.D0.B5_.D1.8F.D0.B4.D1.80.D0.BE) подразделу.

1\. Если вы не знаете модель графической карты, установленной у вас, для поиска используйте данный запрос:

	 `$ lspci -k | grep -A 2 -E "(VGA|3D)"` 

2\. Есть несколько вариантов определения необходимой для вас версии драйвера:

*   поиск по кодовому имени (например, NV50, NVC0 и т.д.) на [странице с кодовыми именами nouveau](http://nouveau.freedesktop.org/wiki/CodeNames)
*   просмотр модели в [списке устаревших графических карт](http://www.nvidia.com/object/IO_32667.html) NVIDIA: если вашей карты нет в списке, используйте драйвер для нового оборудования
*   также можно посетить [страницу загрузки драйвера с сайта](http://www.nvidia.com/Download/index.aspx) NVIDIA

3\. Установите подходящий драйвер для своей карты:

*   Для карт GeForce 400 series и более новых [NVCx и новее], [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [nvidia](https://www.archlinux.org/packages/?name=nvidia) или [nvidia-lts](https://www.archlinux.org/packages/?name=nvidia-lts) вместе с [nvidia-libgl](https://www.archlinux.org/packages/?name=nvidia-libgl). (Для самых новых моделей графических ускорителей может потребоваться [установка](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакета [nvidia-beta](https://aur.archlinux.org/packages/nvidia-beta/), т.к. стабильная версия драйвера может не поддерживать новые функции, добавленные в эти карты.

*   Для карт GeForce 8000/9000 и 100-300 series [NV5x, NV8x, NV9x и NVAx] года производства 2006-2010, [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [nvidia-340xx](https://www.archlinux.org/packages/?name=nvidia-340xx) или [nvidia-340xx-lts](https://www.archlinux.org/packages/?name=nvidia-340xx-lts) вместе с [nvidia-340xx-libgl](https://www.archlinux.org/packages/?name=nvidia-340xx-libgl).
*   Для карт GeForce 6000/7000 series [NV4x и NV6x] года производства 2004-2006, [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) или [nvidia-304xx-lts](https://www.archlinux.org/packages/?name=nvidia-304xx-lts) вместе с [nvidia-304xx-libgl](https://www.archlinux.org/packages/?name=nvidia-304xx-libgl).

*   Для более старых моделей, обратитесь к подразделу [#Не поддерживаемые драйвера](#.D0.9D.D0.B5_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0).

4\. Если у вас разрядность ОС 64-бит и вам необходима поддержка OpenGL 32-бит,то необходимо установить соответствующие пакеты *lib32* с репозитория [multilib](/index.php/Multilib "Multilib") (например, [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl), [lib32-nvidia-340xx-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-libgl) или [lib32-nvidia-304xx-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-libgl)).

5\. Перезагрузите систему. Пакет [nvidia](https://www.archlinux.org/packages/?name=nvidia) содержит файл с чёрным списком для модуля *nouveau*, поэтому перезагрузка необходима.

После того, как драйвер будет установлен, можно перейти к разделу [#Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0).

### Не поддерживаемые драйвера

Если вы имеете карту GeForce 5 FX series или старее, Nvidia не поддерживает больше драйвера для вашей карты. Это означает, что эти драйвера [не поддерживают текущую версию Xorg](http://nvidia.custhelp.com/app/answers/detail/a_id/3142/). В вашем случае, проще использовать драйвер [nouveau](/index.php/Nouveau_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nouveau (Русский)"), который поддерживает старые карты в текущей версии Xorg.

Однако, старые драйвера Nvidia пока ещё доступны и могут предоставлять лучшую 3D производительность/стабильность если вы откатите версию Xorg:

*   Для карт GeForce 5 FX series [NV30-NV36], установите пакет [nvidia-173xx-dkms](https://aur.archlinux.org/packages/nvidia-173xx-dkms/). Последняя поддерживаемая версия Xorg 1.15.
*   Для карт GeForce 2/3/4 MX/Ti series [NV11, NV17-NV28], установите пакет [nvidia-96xx-dkms](https://aur.archlinux.org/packages/nvidia-96xx-dkms/). Последняя поддерживаемая версия Xorg 1.12.

**Совет:** Устаревшие драйвера nvidia-96xx-dkms и nvidia-173xx-dkms также можно установить с неофициального [репозитория [city]](http://pkgbuild.com/~bgyorgy/city.html). (Настоятельно рекомендуется использовать данный способ, который поможет избежать любых проблем с зависимостями после установки.)

### Альтернативная установка: собственное ядро

Прежде всего, очень хорошо понимать, как работает система ABS, путём прочтения некоторых статей об этом:

*   Основная статья о [ABS](/index.php/Arch_Build_System_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Build System (Русский)")
*   Статья о [makepkg](/index.php/Makepkg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Makepkg (Русский)")
*   Статья о [Creating packages](/index.php/Creating_packages_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Creating packages (Русский)")

Следующее небольшое руководство описывает процесс создания собственного пакета драйвера NVIDIA, используя [ABS](/index.php/ABS "ABS"):

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [abs](https://www.archlinux.org/packages/?name=abs) и сгенерируйте дерево:

```
# abs

```

Как обычный пользователь, сделайте временный каталог для создания нового пакета:

```
$ mkdir -p ~/abs

```

Сделайте копию каталога пакета `nvidia`:

```
$ cp -r /var/abs/extra/nvidia/ ~/abs/

```

Зайдите в временный каталог сборки `nvidia`:

```
$ cd ~/abs/nvidia

```

Теперь необходимо отредактировать файлы `nvidia.install` и `PKGBUILD`, они должны содержать правильные переменные версии ядра.

Когда запущено собственное ядро, узнайте версию и имя ядра:

```
$ uname -r

```

1.  В nvidia.install, замените переменную `EXTRAMODULES='extramodules-3.4-ARCH'` собственной версией ядра, например `EXTRAMODULES='extramodules-3.4.4'` или `EXTRAMODULES='extramodules-3.4.4-custom'` в зависимости от названия и версии вашего ядра. Сделайте эти изменения для всех найденых совпадений в этом файле.
2.  В PKGBUILD, измените переменную `_extramodules=extramodules-3.4-ARCH` на совпадающую с вашей версией ядра, как описано выше.
3.  Если вы установили параллельно несколько ядер (например собственное ядро и ядро -ARCH, предоставляемое по умолчанию), измените название в PKGBUILD `pkgname=nvidia` на уникальное, такое как nvidia-344 или nvidia-custom. Это позволяет ядрам использовать разные модули nvidia, собственный модуль nvidia будет иметь другое название пакета и не будет переписан оригинальным. Вам также понадобится закоментировать строку в `package()`, которая добавляет в чёрный список модуль nouveau в `/usr/lib/modprobe.d/nvidia.conf` (нет необходимости делать это снова).

Теперь выполните:

```
$ makepkg -ci

```

Ключ `-c` говорит makepkg очистить оставшиеся файлы после сборки пакета, ключ `-i` указывает makepkg автоматически выполнить запуск pacman для установки собранного пакета.

#### Автоматическая пересборка модуля NVIDIA при обновлении ядра

Это возможно благодаря пакету [nvidia-hook](https://aur.archlinux.org/packages/nvidia-hook/) с [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"). Вам необходимо установить пакет с исходным кодом модуля: [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms). В *nvidia-hook*, автоматическая пересборка выполняется хуком `nvidia` в [mkinitcpio](/index.php/Mkinitcpio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mkinitcpio (Русский)") принудительно, при обновлении пакета [linux-headers](https://www.archlinux.org/packages/?name=linux-headers). Вам необходимо добавить `nvidia` в раздел HOOKS файла `/etc/mkinitcpio.conf`.

Хук будет вызывать команду *dkms* для обновления модуля NVIDIA при обновлении версии вашего ядра.

**Примечание:**

*   Если вы используете данную функциональность **необходимо** наблюдать процесс установки пакета [linux](https://www.archlinux.org/packages/?name=linux) (или другого ядра). Хук nvidia будет сообщать вам, если что-то пойдет не так.
*   Если вы хотите это делать вручную, обратитесь к статье [Dynamic Kernel Module Support (Русский)#Использование](/index.php/Dynamic_Kernel_Module_Support_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5 "Dynamic Kernel Module Support (Русский)").

### Pure Video HD (VDPAU/VAAPI)

Видеокартам со второго поколения [PureVideo HD](https://en.wikipedia.org/wiki/ru:Nvidia_PureVideo#.D0.A2.D0.B0.D0.B1.D0.BB.D0.B8.D1.86.D0.B0._.D0.92.D0.B8.D0.B4.D0.B5.D0.BE.D0.BA.D0.B0.D1.80.D1.82.D1.8B_.D1.81_.D0.B1.D0.BB.D0.BE.D0.BA.D0.BE.D0.BC_PureVideo и [VA-API](/index.php/VA-API_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "VA-API (Русский)").

### Аппаратное ускорение декодирования видео с помощью XvMC

Ускоренное декодирование видео MPEG-1 и MPEG-2 с помощью [XvMC](/index.php/XvMC "XvMC") поддерживается на серии видеокарт GeForce4, GeForce 5 FX, GeForce 6 и GeForce 7\. Смотрите [XvMC](/index.php/XvMC "XvMC").

## Настройка

Вполне возможно, что после установки драйвера, вам будет не нужно создавать конфигурационные файлы для сервера Xorg. Вы можете запустить [тест](/index.php/Xorg#Running "Xorg") для проверки корректной работы сервера Xorg без файла конфигурации. Однако, может потребоваться создание конфигурационного файла (предпочтительно `/etc/X11/xorg.conf.d/20-nvidia.conf` поверх `/etc/X11/xorg.conf`) для дополнительной настройки. Это конфигурация может быть сгенерирована инструментом конфигурации NVIDIA Xorg или можно создать её вручную. Если создается вручную, это может быть минимальной конфигурацией (в том смысле, что она будет содержать базовые настройки сервера [Xorg](/index.php/Xorg "Xorg")), либо она может включать в себя ряд настроек, которые могут обоходить автоматически обнаруженные настройки Xorg или предварительно заданные настройки.

**Примечание:** Начиная с версии 1.8.x, Xorg использует разделение конфигурационных файлов в `/etc/X11/xorg.conf.d/` - проверьте раздел [advanced configuration](#Advanced:_20-nvidia.conf).

### Минимальная настройка

Базовый блок конфигурации в `20-nvidia.conf` (или устаревший блок в `xorg.conf`) должен выглядеть так:

 `/etc/X11/xorg.conf.d/20-nvidia.conf` 
```
Section "Device"
        Identifier "Nvidia Card"
        Driver "nvidia"
        VendorName "NVIDIA Corporation"
        Option "NoLogo" "true"
        #Option "UseEDID" "false"
        #Option "ConnectedMonitor" "DFP"
        # ...
EndSection

```

**Совет:** Если вы перешли с драйвера nouveau, удостоверьтесь, в том что вы удалили "`nouveau`" из `/etc/mkinitcpio.conf`. Дополнительно смотрите [Switching between NVIDIA and nouveau drivers](#Switching_between_NVIDIA_and_nouveau_drivers), если вы часто переключаетесь между открытым и закрытым драйвером.

### Автоматическая настройка

Пакет NVIDIA, включает в себя автоматический инструмент для создания файла конфигурации сервера Xorg (`xorg.conf`) и может быть запущен путем выполнения:

```
# nvidia-xconfig

```

Данная команда автоматически обнаруживает и создает (или изменяет, если было уже создано) конфигурацию `/etc/X11/xorg.conf`, в соответствии с текущим аппаратным обеспечением.

Если есть строка с указанием загрузки DRI, убедитесь, что она закомментирована:

```
#    Load        "dri"

```

Проверьте ещё раз `/etc/X11/xorg.conf`, убедитесь, что глубина по умолчанию, горизонтальная синхронизация, частота кадров и разрешение допустимы.

**Важно:** Это может не работать корректно с сервером Xorg версии 1.8

### NVIDIA Settings

The [nvidia-settings](https://www.archlinux.org/packages/?name=nvidia-settings) tool lets you configure many options using a GUI. Run `nvidia-settings` as root, configure as you wish, and then save the configuration to `/etc/X11/xorg.conf.d/` as usual.

Alternatively, you can run the GUI as a normal user and save the settings to `~/.nvidia-settings-rc`. Then you can load the settings using `$ nvidia-settings --load-config-only` (for example in your [xinitrc](/index.php/Xinitrc "Xinitrc")).

**Tip:** If your X server is crashing on startup, it may be because the GUI-generated settings are corrupt. Try deleting the generated file and starting from scratch.

### Несколько мониторов

	*Смотрите [Multihead](/index.php/Multihead "Multihead") для получения основной информации*

#### Использование NVIDIA Settings

The [nvidia-settings](#NVIDIA_Settings) tool can configure multiple monitors.

#### ConnectedMonitor

Если драйвер не определил второй монитор, вы можете принудительно указать его с помощью опции ConnectedMonitor

 `/etc/X11/xorg.conf` 
```

Section "Monitor"
    Identifier     "Monitor1"
    VendorName     "Panasonic"
    ModelName      "Panasonic MICRON 2100Ex"
    HorizSync       30.0 - 121.0 # this monitor has incorrect EDID, hence Option "UseEDIDFreqs" "false"
    VertRefresh     50.0 - 160.0
    Option         "DPMS"
EndSection

Section "Monitor"
    Identifier     "Monitor2"
    VendorName     "Gateway"
    ModelName      "GatewayVX1120"
    HorizSync       30.0 - 121.0
    VertRefresh     50.0 - 160.0
    Option         "DPMS"
EndSection

Section "Device"
    Identifier     "Device1"
    Driver         "nvidia"
    Option         "NoLogo"
    Option         "UseEDIDFreqs" "false"
    Option         "ConnectedMonitor" "CRT,CRT"
    VendorName     "NVIDIA Corporation"
    BoardName      "GeForce 6200 LE"
    BusID          "PCI:3:0:0"
    Screen          0
EndSection

Section "Device"
    Identifier     "Device2"
    Driver         "nvidia"
    Option         "NoLogo"
    Option         "UseEDIDFreqs" "false"
    Option         "ConnectedMonitor" "CRT,CRT"
    VendorName     "NVIDIA Corporation"
    BoardName      "GeForce 6200 LE"
    BusID          "PCI:3:0:0"
    Screen          1
EndSection

```

Дублирование устройств с опцией `Screen` описывает использование сервером Xorg двух мониторов на одной карте без технологии `TwinView`. Учтите, что `nvidia-settings` будет вырезать любое упоминание опции `ConnectedMonitor`.

#### TwinView

Вы хотите только один большой экран вместо двух. Установите значение опции `TwinView` в `1`. Эта опция должна использоваться если вы хотите композитинга. Технология TwinView работает только на базе одной карты, когда все мониторы подключены к одной карте.

```
Option "TwinView" "1"

```

Пример конфигурцаии:

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "ServerLayout"
    Identifier     "TwinLayout"
    Screen         0 "metaScreen" 0 0
EndSection

Section "Monitor"
    Identifier     "Monitor0"
    Option         "Enable" "true"
EndSection

Section "Monitor"
    Identifier     "Monitor1"
    Option         "Enable" "true"
EndSection

Section "Device"
    Identifier     "Card0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"

    #refer to the link below for more information on each of the following options.
    Option         "HorizSync"          "DFP-0: 28-33; DFP-1 28-33"
    Option         "VertRefresh"        "DFP-0: 43-73; DFP-1 43-73"
    Option         "MetaModes"          "1920x1080, 1920x1080"
    Option         "ConnectedMonitor"   "DFP-0, DFP-1"
    Option         "MetaModeOrientation" "DFP-1 LeftOf DFP-0"
EndSection

Section "Screen"
    Identifier     "metaScreen"
    Device         "Card0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option         "TwinView" "True"
    SubSection "Display"
        Modes          "1920x1080"
    EndSubSection
EndSection

```

[Дополнительная информация о технологии TwinView (англ.)](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/configtwinview.html).

Если вы имеете несколько карт, которые совместимы с технологией SLI, вы можете использовать несколько мониторов присоединённых к разным картам (пример: две карты в режиме SLI с подключением монитора на каждой карте). Опция "MetaModes" совместно с режимом SLI Mosaic позволяет это. Ниже указана конфигурация, которая работает для вышеупомянутого примера и безупречно запускает [GNOME](/index.php/GNOME "GNOME").

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "Device"
        Identifier      "Card A"
        Driver          "nvidia"
        BusID           "PCI:1:00:0"
EndSection

Section "Device"
        Identifier      "Card B"
        Driver          "nvidia"
        BusID           "PCI:2:00:0"
EndSection

Section "Monitor"
        Identifier      "Right Monitor"
EndSection

Section "Monitor"
        Identifier      "Left Monitor"
EndSection

Section "Screen"
        Identifier      "Right Screen"
        Device          "Card A"
        Monitor         "Right Monitor"
        DefaultDepth    24
        Option          "SLI" "Mosaic"
        Option          "Stereo" "0"
        Option          "BaseMosaic" "True"
        Option          "MetaModes" "GPU-0.DFP-0: 1920x1200+4480+0, GPU-1.DFP-0:1920x1200+0+0"
        SubSection      "Display"
                        Depth           24
        EndSubSection
EndSection

Section "Screen"
        Identifier      "Left Screen"
        Device          "Card B"
        Monitor         "Left Monitor"
        DefaultDepth    24
        Option          "SLI" "Mosaic"
        Option          "Stereo" "0"
        Option          "BaseMosaic" "True"
        Option          "MetaModes" "GPU-0.DFP-0: 1920x1200+4480+0, GPU-1.DFP-0:1920x1200+0+0"
        SubSection      "Display"
                        Depth           24
        EndSubSection
EndSection

Section "ServerLayout"
        Identifier      "Default"
        Screen 0        "Right Screen" 0 0
        Option          "Xinerama" "0"
EndSection
```

##### Ручная конфигурация из командной строки с использованием xrandr

Если вышеуказанные решения не сработали, вы можете использовать *автозапуск* вашего менеджера окон совместно с пакетом [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr).

Некоторые примеры работы с командой `xrandr`:

```
xrandr --output DVI-I-0 --auto --primary --left-of DVI-I-1

```

или:

```
xrandr --output DVI-I-1 --pos 1440x0 --mode 1440x900 --rate 75.0

```

Где:

*   `--output` используется для указания "монитора", к которому применяются опции.
*   `DVI-I-1` имя второго монитора.
*   `--pos` позиция второго монитора относительно первого.
*   `--mode` разрешение второго монитора.
*   `--rate` частота обновления (в Гц).

##### Vertical sync using TwinView

If you are using TwinView and vertical sync (the "Sync to VBlank" option in **nvidia-settings**), you will notice that only one screen is being properly synced, unless you have two identical monitors. Although **nvidia-settings** does offer an option to change which screen is being synced (the "Sync to this display device" option), this does not always work. A solution is to add the following environment variables at startup, for example append in `/etc/profile`:

```
export __GL_SYNC_TO_VBLANK=1
export __GL_SYNC_DISPLAY_DEVICE=DFP-0
export __VDPAU_NVIDIA_SYNC_DISPLAY_DEVICE=DFP-0

```

You can change `DFP-0` with your preferred screen (`DFP-0` is the DVI port and `CRT-0` is the VGA port). You can find the identifier for your display from **nvidia-settings** in the "X Server XVideoSettings" section.

##### Gaming using TwinView

In case you want to play fullscreen games when using TwinView, you will notice that games recognize the two screens as being one big screen. While this is technically correct (the virtual X screen really is the size of your screens combined), you probably do not want to play on both screens at the same time.

To correct this behavior for SDL, try:

```
export SDL_VIDEO_FULLSCREEN_HEAD=1

```

For OpenGL, add the appropriate Metamodes to your xorg.conf in section `Device` and restart X:

```
Option "Metamodes" "1680x1050,1680x1050; 1280x1024,1280x1024; 1680x1050,NULL; 1280x1024,NULL;"

```

Another method that may either work alone or in conjunction with those mentioned above is [starting games in a separate X server](/index.php/Gaming#Starting_games_in_a_separate_X_server "Gaming").

#### Режим Mosaic

Режим Mosaic единственный способ использовать более чем два монитора через несколько видеокарт с использованием композитинга. Ваш оконный менджер может распознать, а может и не распознать различия между мониторами.

##### Base Mosaic

Режим Base Mosaic работает с картами Geforce 8000 series или выше. Его нельзя включить через графический интерфейс nvidia-setting. Вы должны использовать команду `nvidia-xconfig`, либо отредактировать `xorg.conf` самостоятельно. Опция Metamodes должна быть указана. Следующий пример для четырёх DFP мониторов в конфигурации 2х2, каждый запущен в разрешении 1920x1024, по два подключенных DFP монитора на две карты:

```
$ nvidia-xconfig --base-mosaic --metamodes="GPU-0.DFP-0: 1920x1024+0+0, GPU-0.DFP-1: 1920x1024+1920+0, GPU-1.DFP-0: 1920x1024+0+1024, GPU-1.DFP-1: 1920x1024+1920+1024"

```

**Примечание:** Хотя в документации и указано конфигурация мониторов 2х2, Nvidia уменьшила данную возможность до трех мониторов в режиме Base Mosaic в 304 версии драйвера. Большее количество мониторов доступно в картах серии Quadro, а в обычных картах ограничение в три монитора. Как объяснение данного уменьшения озвучивается как "Паритетное свойство драйвера Windows". С сентября 2014, Windows не имеет ограничение на количество мониторов с той же самой версией драйвера. Это не ошибка, так задумано по дизайну архитектуры.

##### SLI Mosaic

Если вы имеете конфигурацию SLI и все графические ускорители серии Quadro FX 5800, Quadro Fermi или новее, тогда вы можете использовать режим SLI Mosaic. он можеть быть включен из графического интерфейса nvidia-settings или из командной строки:

```
$ nvidia-xconfig --sli=Mosaic --metamodes="GPU-0.DFP-0: 1920x1024+0+0, GPU-0.DFP-1: 1920x1024+1920+0, GPU-1.DFP-0: 1920x1024+0+1024, GPU-1.DFP-1: 1920x1024+1920+1024"

```

### Драйвер Persistence

Начиная с версии 319, Nvidia изменила порядок работы драйвера persistence, теперь он запускается как демон при загрузке. Смотрите раздел [драйвер Persistence (англ.)](http://docs.nvidia.com/deploy/driver-persistence/index.html) документации Nvidia, для получения детальной информации.

Для запуска демона persistence [разрешите](/index.php/Enable "Enable") `nvidia-persistenced.service`. Для использования вручную смотрите [документацию разработчика](http://docs.nvidia.com/deploy/driver-persistence/index.html#usage).

## Смотрите также

*   [NVIDIA User forums](https://forums.geforce.com/)
*   [Official README for NVIDIA drivers, all on one text page. Most Recent Driver Version as of September 7, 2015: 355.11.](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/README.txt)
*   [README Appendix B. X Config Options, 355.11 (direct link)](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/xconfigoptions.html)