Ссылки по теме

*   [Intel GMA3600](/index.php/Intel_GMA3600 "Intel GMA3600")
*   [Xorg](/index.php/Xorg "Xorg")
*   [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting")
*   [Xrandr](/index.php/Xrandr "Xrandr")
*   [Hybrid graphics](/index.php/Hybrid_graphics "Hybrid graphics")

**Состояние перевода:** На этой странице представлен перевод статьи [Intel graphics](/index.php/Intel_graphics "Intel graphics"). Дата последней синхронизации: 7 октября 2015\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Intel_graphics&diff=0&oldid=403749).

С тех пор как Intel предоставляет и поддерживает только свободные драйвера, видеокарты Intel graphics работают "из коробки".

Всеобъемлющий список моделей видеокарт и соответствующих чипсетов и процессоров доступен в [английской Википедии](https://en.wikipedia.org/wiki/Comparison_of_Intel_graphics_processing_units "wikipedia:Comparison of Intel graphics processing units").

**Примечание:** Основанные на PowerVR видеокарты [GMA 3600](/index.php/Intel_GMA3600 "Intel GMA3600") серии) не поддерживаются свободными драйверами.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
*   [3 Kernel Mode Setting](#Kernel_Mode_Setting)
*   [4 Опции модуля для энергосбережения](#.D0.9E.D0.BF.D1.86.D0.B8.D0.B8_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D1.8F_.D0.B4.D0.BB.D1.8F_.D1.8D.D0.BD.D0.B5.D1.80.D0.B3.D0.BE.D1.81.D0.B1.D0.B5.D1.80.D0.B5.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
*   [5 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [5.1 Видео без тиринга (горизонтального разрыва)](#.D0.92.D0.B8.D0.B4.D0.B5.D0.BE_.D0.B1.D0.B5.D0.B7_.D1.82.D0.B8.D1.80.D0.B8.D0.BD.D0.B3.D0.B0_.28.D0.B3.D0.BE.D1.80.D0.B8.D0.B7.D0.BE.D0.BD.D1.82.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D1.80.D0.B0.D0.B7.D1.80.D1.8B.D0.B2.D0.B0.29)
    *   [5.2 Отключение вертикальной синхронизации (VSYNC)](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2.D0.B5.D1.80.D1.82.D0.B8.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B9_.D1.81.D0.B8.D0.BD.D1.85.D1.80.D0.BE.D0.BD.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8_.28VSYNC.29)
    *   [5.3 Настройка режима масштабирования](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B0_.D0.BC.D0.B0.D1.81.D1.88.D1.82.D0.B0.D0.B1.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [5.4 Проблема с KMS: консоль ограничена в небольшую площадь](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D1.81_KMS:_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C_.D0.BE.D0.B3.D1.80.D0.B0.D0.BD.D0.B8.D1.87.D0.B5.D0.BD.D0.B0_.D0.B2_.D0.BD.D0.B5.D0.B1.D0.BE.D0.BB.D1.8C.D1.88.D1.83.D1.8E_.D0.BF.D0.BB.D0.BE.D1.89.D0.B0.D0.B4.D1.8C)
    *   [5.5 Декодирование H.264 на GMA 4500](#.D0.94.D0.B5.D0.BA.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_H.264_.D0.BD.D0.B0_GMA_4500)
    *   [5.6 Управление яркостью и гаммой](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.8F.D1.80.D0.BA.D0.BE.D1.81.D1.82.D1.8C.D1.8E_.D0.B8_.D0.B3.D0.B0.D0.BC.D0.BC.D0.BE.D0.B9)
*   [6 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [6.1 Проблемы SNA](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_SNA)
    *   [6.2 Font and screen corruption in GTK+ applications (missing glyphs after suspend/resume)](#Font_and_screen_corruption_in_GTK.2B_applications_.28missing_glyphs_after_suspend.2Fresume.29)
    *   [6.3 Пустой экран во время загрузки системы на этапе "Loading modules"](#.D0.9F.D1.83.D1.81.D1.82.D0.BE.D0.B9_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD_.D0.B2.D0.BE_.D0.B2.D1.80.D0.B5.D0.BC.D1.8F_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B_.D0.BD.D0.B0_.D1.8D.D1.82.D0.B0.D0.BF.D0.B5_.22Loading_modules.22)
    *   [6.4 X зависает/падает с драйверами intel](#X_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.B5.D1.82.2F.D0.BF.D0.B0.D0.B4.D0.B0.D0.B5.D1.82_.D1.81_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0.D0.BC.D0.B8_intel)
    *   [6.5 Добавление неопределённых разрешений](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D1.91.D0.BD.D0.BD.D1.8B.D1.85_.D1.80.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [6.6 Проблема цвета](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D1.86.D0.B2.D0.B5.D1.82.D0.B0)
    *   [6.7 Подсветка не регулируется](#.D0.9F.D0.BE.D0.B4.D1.81.D0.B2.D0.B5.D1.82.D0.BA.D0.B0_.D0.BD.D0.B5_.D1.80.D0.B5.D0.B3.D1.83.D0.BB.D0.B8.D1.80.D1.83.D0.B5.D1.82.D1.81.D1.8F)
    *   [6.8 Отключение сжатия буфера кадров](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.B6.D0.B0.D1.82.D0.B8.D1.8F_.D0.B1.D1.83.D1.84.D0.B5.D1.80.D0.B0_.D0.BA.D0.B0.D0.B4.D1.80.D0.BE.D0.B2)
    *   [6.9 Искажение/Зависание в Chromium и Firefox](#.D0.98.D1.81.D0.BA.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5.2F.D0.97.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B2_Chromium_.D0.B8_Firefox)
    *   [6.10 Розовые и зелёные артефакты на видео или выводе Веб-камеры](#.D0.A0.D0.BE.D0.B7.D0.BE.D0.B2.D1.8B.D0.B5_.D0.B8_.D0.B7.D0.B5.D0.BB.D1.91.D0.BD.D1.8B.D0.B5_.D0.B0.D1.80.D1.82.D0.B5.D1.84.D0.B0.D0.BA.D1.82.D1.8B_.D0.BD.D0.B0_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE_.D0.B8.D0.BB.D0.B8_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4.D0.B5_.D0.92.D0.B5.D0.B1-.D0.BA.D0.B0.D0.BC.D0.B5.D1.80.D1.8B)
    *   [6.11 Ядро сбоит с ядрами 4.0+ на чипах Broadwell/Core-M](#.D0.AF.D0.B4.D1.80.D0.BE_.D1.81.D0.B1.D0.BE.D0.B8.D1.82_.D1.81_.D1.8F.D0.B4.D1.80.D0.B0.D0.BC.D0.B8_4.0.2B_.D0.BD.D0.B0_.D1.87.D0.B8.D0.BF.D0.B0.D1.85_Broadwell.2FCore-M)
    *   [6.12 Драйвер не работает на чипах Intel Skylake](#.D0.94.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.BD.D0.B0_.D1.87.D0.B8.D0.BF.D0.B0.D1.85_Intel_Skylake)
*   [7 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Необходимое условие: [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)").

[Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") пакет [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Пакет предоставляет драйвер DDX для 2D ускорения и устанавливает пакет [intel-dri](https://www.archlinux.org/packages/?name=intel-dri) как зависимость, который предоставляет драйвер DRI для 3D ускорения.

Для поддержи 32-битного 3D ускорения на x86_64, установите [lib32-intel-dri](https://www.archlinux.org/packages/?name=lib32-intel-dri) из репозитория [multilib](/index.php/Multilib "Multilib").

Установите драйвер [VA-API](/index.php/VA-API_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "VA-API (Русский)") и необходимую библиотеку с помощью пакетов [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) и [libva](https://www.archlinux.org/packages/?name=libva) соответственно. На старых видеокартах, это предоставляет драйвер [XvMC](/index.php/XvMC "XvMC"), который включён в драйвер DDX.

## Конфигурация

Для запуска [X](/index.php/X_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "X (Русский)") конфигурация не требуется.

Полный список опций доступен в документации `$ man intel`.

## Kernel Mode Setting

**Совет:** Если вы наблюдаете проблемы с разрешением экрана, обратитесь к [этой странице](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting").

[Kernel Mode Setting](/index.php/KMS "KMS") (KMS) необходим для запуска X и [среды рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)"). KMS поддерживается чипсетами Intel, которые используют драйвер i915 DRM включенный по умолчанию. Версии драйвера [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) 2.10 и новее больше не поддерживают UMS (за исключением очень старых чипсетов 810 серии), что делает использование KMS обязательным. KMS обычно инициализируется сразу после [стадии initramfs](/index.php/Arch_boot_process#initramfs "Arch boot process"). Однако, есть возможность активировать KSM во время стадии initramfs.

**Примечание:** Users must remove any deprecated references to `vga` or `nomodeset` from boot configuration.

Для этого добавьте модуль `i915` в строку `MODULES` в файле `/etc/mkinitcpio.conf`:

```
MODULES=i915

```

Если вы используете собственный, нестандартный, файл [EDID](https://ru.wikipedia.org/wiki/Extended_display_identification_data)], вам также необходимо вставить его в initramfs:

 `/etc/mkinitcpio.conf`  `FILES="/lib/firmware/edid/your_edid.bin"` 

Теперь перегенерируйте initramfs:

```
# mkinitcpio -p linux

```

Изменения вступят в силу после следующей перезагрузки.

## Опции модуля для энергосбережения

Модуль ядра `i915` можно конфигурировать через [опции модуля](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Setting_module_options "Kernel modules (Русский)"). Часть этих опций модуля влияют на энергосбережение.

Для проверки, какие опции в данный момент включены, воспользуйтесь командой

```
# for i in /sys/module/i915/parameters/*; do echo $i=$(cat $i); done

```

Список всех опций с кратким их описанием и значения по умолчанию можно получить командой:

```
$ modinfo i915 | grep parm

```

Следующий набор опций, как правило, можно включить без негативных последствий:

 `/etc/modprobe.d/i915.conf` 
```
options i915 i915_enable_rc6=1 i915_enable_fbc=1 lvds_downclock=1

```

Вы можете поэкспериментировать со более большими значениями `enable_rc6`, однако ваша видеокарта может их не поддерживать [[2]](https://wiki.archlinux.org/index.php?title=Talk:Intel_Graphics&oldid=327547#Kernel_Module_options).

Сжатие буфера кадров может оказаться ненадёжным на старых поколениях видеокарт Intel (Каких?). В результате чего подобные сообщения выводятся в системный журнал:

```
kernel: drm: not enough stolen space for compressed buffer, disabling.

```

## Советы и рекомендации

### Видео без тиринга (горизонтального разрыва)

**Совет:** Если вы используете окружение рабочего стола [GNOME](/index.php/GNOME "GNOME"), наиболее простой и предпочтительный, с точки зрения производительности, способ можно найти на странице [GNOME#Tear-free_video_with_Intel_HD_Graphics](/index.php/GNOME#Tear-free_video_with_Intel_HD_Graphics "GNOME").

Для некоторых пользователей рывки видео происходят из-за метода ускорения SNA. Чтобы исправить это, включите опцию `"Tearfree"` в драйвере:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "TearFree"    "true"
EndSection
```

См. [отчёт об ошибке](https://bugs.freedesktop.org/show_bug.cgi?id=37686) за подробной информацией.

**Примечание:**

*   Данная опция может не работать если `SwapbuffersWait` выставлена на `false`.
*   Данная опция может создать дополнительные проблемы в некоторых приложениях, например [Super Meat Boy](https://ru.wikipedia.org/wiki/Super_Meat_Boy).
*   Данная опция не работает с методом ускорения UXA, только с SNA.

### Отключение вертикальной синхронизации (VSYNC)

Драйвер intel использует [тройную буферизацию](http://www.intel.com/support/graphics/sb/CS-004527.htm) для вертикальной синхронизации, что позволяет без потерь в производительности избежать разрывы кадров. Чтобы отключить вертикальную синхронизацию (например, для "бенчмаркинга") создайте файл .drirc в вашей домашней директории со следующим содержимым:

 `~/.drirc` 
```
<device screen="0" driver="dri2">
	<application name="Default">
		<option name="vblank_mode" value="0"/>
	</application>
</device>
```

Не используйте [driconf](https://www.archlinux.org/packages/?name=driconf) для создания этого файла, так как он выставит неправильное название драйвера.

### Настройка режима масштабирования

Это может быть полезно для некоторых полноэкранных приложений:

```
$ xrandr --output LVDS1 --set PANEL_FITTING param

```

Где `param` одно из следующих значений:

*   `center`: разрешение экрана не будет меняться, масштабирование отключено,
*   `full`: масштабировать разрешение экрана для использования всего места на экране или
*   `full_aspect`: максимально масштабировать разрешение экрана, но соблюдать соотношение сторон.

Если это не сработало, попробуйте:

```
$ xrandr --output LVDS1 --set "scaling mode" param

```

Где `param` это `"Full"`, `"Center"` или `"Full aspect"`.

### Проблема с KMS: консоль ограничена в небольшую площадь

Один из портов низкого разрешения видео может быть включен во время загрузки системы, в результате чего терминал использует маленькую часть экрана. Чтобы исправить это, отдельно отключите порт с помощью опции модуля i915 `video=SVIDEO-1:d` в параметрах командной строке ядра в загрузчике. Больше информации об этом доступно на странице [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

Если это не сработало, попробуйте выключить TV1 или VGA1 вместо SVIDEO-1.

### Декодирование H.264 на GMA 4500

Пакет [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) предоставляет декодирование MPEG-2 только для GMA 4500 серии видеокарт. Поддержка декодирования H.264 сопровождается в отдельной ветке под названием g45-h264, которой можно воспользоваться установив пакет [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/), доступный в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"). Однако имейте в виду, что данная поддержка экспериментально и в данный не ведётся активная разработка. Использование VA-API с этим драйвером на GMA 4500 серии видеокарт уменьшит нагрузку на центральный процессор, однако не гарантируется плавное воспроизведение в сравнении с программным декодированием. Тестирование с использованием mplayer показало что использование vaapi для воспроизведения закодированного в H.264 1080p видео снизило нагрузку на процессор, однако воспроизведение происходит с рывками, в то время как воспроизведение 720p работало удовлетворительно [[3]](https://bbs.archlinux.org/viewtopic.php?id=150550). Это подтверждает и опыт других пользователей [[4]](http://www.emmolution.org/?p=192&cpage=1#comment-12292).

### Управление яркостью и гаммой

Следующий пример демонстрирует использование [виртуальную файловую систему](https://ru.wikipedia.org/wiki/Виртуальная_файловая_система) `/sys` для выставления уровня яркости на уровне драйвера. Максимальная яркость указана в файле `/sys/class/backlight/intel_backlight/max_brightness`. Имейте в виду, что это значение может отличаться в зависимости от разной конфигурации оборудования.

```
# cd /sys/class/backlight/intel_backlight
# cat max_brightness
4437
# echo 2200 > brightness

```

Яркость также можно выставить используя пакет [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight).

```
$ xbacklight -set 50  # sets brightness to 50% of maximum

```

Вместо абсолютных значений можно использовать инкрементирующие, например:

```
$ xbacklight -inc 10  # increase brightness by 10%
$ xbacklight -dec 10  # decrease brightness by 10%

```

Гамму можно выставить используя пакет [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr), либо [xorg-xgamma](https://www.archlinux.org/packages/?name=xorg-xgamma). Следующие команды делают одно и то же.

```
$ xrandr --output LVDS1 --gamma 1.0:1.0:1.0
$ xgamma -rgamma 1 -ggamma 1 -bgamma 1

```

## Решение проблем

### Проблемы SNA

Согласно [intel(4)](http://jlk.fjfi.cvut.cz/arch/manpages/man/intel.4):

	*Есть несколько движков для ускорения DDX. "UXA" (Архитектура Единого Ускорения) является зрелой базовой, которая была введена для поддержки модели драйвера GEM. Именно в процессе заменены "SNA" (новое ускорение в SandyBridge). Cпособность выбора использовать базовую остается для обратной совместимости.*

*SNA* — стандартный метод ускорения в [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). Если вы наблюдаете проблемы с *SNA*, попробуйте переключить на *UXA*. Для этого нужно создать файл конфигурации [X](/index.php/X_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "X (Русский)") со следующим содержимым:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "AccelMethod"  "uxa"
EndSection

```

Можно также воспользоваться [Glamor](http://www.freedesktop.org/wiki/Software/Glamor/):

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "AccelMethod"  "glamor"
EndSection

```

### Font and screen corruption in GTK+ applications (missing glyphs after suspend/resume)

Should you experience missing font glyphs in GTK+ applications, the following workaround might help. [Edit](/index.php/Textedit "Textedit") `/etc/environment` to add the following line:

 `/etc/environment`  `COGL_ATLAS_DEFAULT_BLIT_MODE=framebuffer` 

See also [FreeDesktop bug 88584](https://bugs.freedesktop.org/show_bug.cgi?id=88584).

### Пустой экран во время загрузки системы на этапе "Loading modules"

Если вы используете "поздний старт" KMS и во время загрузки системы наблюдаете пустой экран. Исправить проблему можно добавив `i915` и `intel_agp` в initramfs. Смотрите раздел [#Kernel Mode Setting](#Kernel_Mode_Setting) выше.

Либо можно добавить следующее в [параметры ядра](/index.php/Kernel_parameters "Kernel parameters"):

```
video=SVIDEO-1:d

```

Если необходим вывод в VGA, попробуйте следующее:

```
video=VGA-1:1280x800

```

### X зависает/падает с драйверами intel

Некоторые проблемы со сбоем X, зависания GPU, или проблемы с зависанием X, могут быть решены путем отключения использования GPU с опцией `NoAccel`:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier "Intel Graphics"
   Driver "intel"
   Option "NoAccel" "True"
EndSection
```

Кроме того, попробуйте отключить 3D-ускорение только с опцией `DRI`:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier "Intel Graphics"
   Driver "intel"
   Option "DRI" "False"
EndSection
```

Если у вас есть сбои при

```
Option "TearFree" "true"
Option "AccelMethod" "sna"

```

в файле настроек, в большинстве случаев это может быть исправлено добавлением

```
i915.semaphores=1

```

к вашим параметрам загрузки.

### Добавление неопределённых разрешений

Этот вопрос рассматривается в [Xrandr page](/index.php/Xrandr#Adding_undetected_resolutions "Xrandr").

### Проблема цвета

**Примечание:** Эта проблема связана с изменениями в ядре 3.9\. Эта проблема до сих пор остается в ядре 3.10

Ядро 3.9 содержит изменения, позволяющие драйверу Intel легко настраивать глубину RGB, что в некоторых случаях может привести к проблемам цвета. Это связано с новым "Автоматическим" режимом на "Broadcast RGB». Можно заставить использовать режим, например, `xrandr --output <HDMI> --set "Broadcast RGB" "Full"` (замените `<HDMI>` на соответствующее устройство вывода, проверьте запустив `xrandr`). Вы можете добавить его в свой `.xprofile` и сделать его исполняемым, чтобы запускать команду, прежде чем он запустит графический режим.

**Примечание:** Некоторые телевизоры могут отображать только цвета из диапазона 16-255, поэтому установка на Full вызовет ограничение цвета в диапазоне 0-15, так что лучше оставить его в автоматическом режиме, который будет автоматически определять необходимость сокращать цветовое пространство для телевизора.

Также есть и другие связанные с ними проблемы, которые могут быть исправлены редактированием регистров GPU. Больше информации можно найти [[5]](http://lists.freedesktop.org/archives/intel-gfx/2012-April/016217.html) и [[6]](http://github.com/OpenELEC/OpenELEC.tv/commit/09109e9259eb051f34f771929b6a02635806404c).

### Подсветка не регулируется

После возобновления из режима ожидания, горячие клавиши для изменения яркости экрана не работают. Использование следующих параметров ядра потенциально может решить проблему.

```
acpi_backlight=vendor

```

Устройствам Samsung с гибридной графикой (таким как 770Z5E) нужно указать acpi_backlight=video в качестве параметра ядра, при использовании ядра >= 3.17

```
acpi_backlight=video

```

Либо в дополнение к вышеуказанному параметру, либо по своей инициативе, добавьте один из следующих двух параметров:

```
acpi_osi=Linux
acpi_osi="!Windows 2012"

```

Другой доступный параметр:

```
video.use_native_backlight=1

```

Если не один из них не решает проблему, отредактируйте или создайте `/etc/X11/xorg.conf.d/20-intel.conf` со следующим содержимым:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
        Identifier  "card0"
        Driver      "intel"
    Option      "Backlight"  "intel_backlight"
        BusID       "PCI:0:2:0"

EndSection
```

При использовании ускорения SNA, как упоминалось выше, создайте файл следующим образом:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
        Identifier  "card0"
        Driver      "intel"
        Option      "AccelMethod"  "sna"
        Option      "Backlight"    "intel_backlight"
        BusID       "PCI:0:2:0"

EndSection
```

### Отключение сжатия буфера кадров

На некоторых картах, таких как Intel Corporation Mobile 4 Series Chipsets, включение сжатия буфера кадров в результате приведёт к потоку ошибок:

```
$ dmesg |tail 
[ 2360.475430] [drm] not enough stolen space for compressed buffer (need 4325376 bytes), disabling
[ 2360.475437] [drm] hint: you may be able to increase stolen memory size in the BIOS to avoid this

```

Решение заключается в отключении сжатия буфера кадров, которое будет немного увеличивать расход энергии. Для того, чтобы отключить его добавьте `i915.enable_fbc=0` в строку параметров ядра. Более подробная информация о результатах отключения сжатия может быть найдена [здесь](http://zinc.canonical.com/~cking/power-benchmarking/background-colour-and-framebuffer-compression/results.txt).

### Искажение/Зависание в Chromium и Firefox

Если у вас проявляются искажения или зависания в Chromium и/или Firefox [поменяйте AccelMethod на "uxa"](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_SNA)

Проблема с искажениями в **Chromium** в **Gnome-shell** на **sna** решается включением настройки "Использовать системные рамки и строку заголовка".

### Розовые и зелёные артефакты на видео или выводе Веб-камеры

На машинах с Broadwell, приложения использующие вывод *xv* или *Intel Textured Video* (в частности Skype и VLC), видеопоток выдаёт розовые и залёные артефакты. Это общая проблема Broadwell, которая была зафиксирована 16.04.2015 [[7]](https://bugs.freedesktop.org/show_bug.cgi?id=89807). Обновите [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) чтобы исправить её.

### Ядро сбоит с ядрами 4.0+ на чипах Broadwell/Core-M

Через несколько секунд после запуска X/Wayland машина зависает и в логе journalctl будет описан крах ядра ссылающийся на графику Intel, как показано ниже:

```
Jun 16 17:54:03 hostname kernel: BUG: unable to handle kernel NULL pointer dereference at           (null)
Jun 16 17:54:03 hostname kernel: IP: [<          (null)>]           (null)
...
Jun 16 17:54:03 hostname kernel: CPU: 0 PID: 733 Comm: gnome-shell Tainted: G     U     O    4.0.5-1-ARCH #1
...
Jun 16 17:54:03 hostname kernel: Call Trace:
Jun 16 17:54:03 hostname kernel:  [<ffffffffa055cc27>] ? i915_gem_object_sync+0xe7/0x190 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa0579634>] intel_execlists_submission+0x294/0x4c0 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa05539fc>] i915_gem_do_execbuffer.isra.12+0xabc/0x1230 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa055d349>] ? i915_gem_object_set_to_cpu_domain+0xa9/0x1f0 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffff811ba2ae>] ? __kmalloc+0x2e/0x2a0
Jun 16 17:54:03 hostname kernel:  [<ffffffffa0555471>] i915_gem_execbuffer2+0x141/0x2b0 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa042fcab>] drm_ioctl+0x1db/0x640 [drm]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa0555330>] ? i915_gem_execbuffer+0x450/0x450 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffff8122339b>] ? eventfd_ctx_read+0x16b/0x200
Jun 16 17:54:03 hostname kernel:  [<ffffffff811ebc36>] do_vfs_ioctl+0x2c6/0x4d0
Jun 16 17:54:03 hostname kernel:  [<ffffffff811f6452>] ? __fget+0x72/0xb0
Jun 16 17:54:03 hostname kernel:  [<ffffffff811ebec1>] SyS_ioctl+0x81/0xa0
Jun 16 17:54:03 hostname kernel:  [<ffffffff8157a589>] system_call_fastpath+0x12/0x17
Jun 16 17:54:03 hostname kernel: Code:  Bad RIP value.
Jun 16 17:54:03 hostname kernel: RIP  [<          (null)>]           (null)

```

Это может быть исправлено путем отключения поддержки *execlist*, которая была изменена по умолчанию на ядре с версии 4.0\. Добавьте следующий параметр ядра:

```
i915.enable_execlists=0

```

Эта поломка с ядрами версии меньше 4.0.5.

### Драйвер не работает на чипах Intel Skylake

Для работы драйвера на новом Intel Skylake (6-е поколение) GPU, строка `i915.preliminary_hw_support=1` должна быть добавлена к параметрам загрузки.

## Смотрите также

*   [https://01.org/linuxgraphics/documentation](https://01.org/linuxgraphics/documentation) (includes a list of supported hardware)
*   Arch Linux forums: [Intel 945GM, Xorg, Kernel - performance](https://bbs.archlinux.org/viewtopic.php?pid=522665#p522665)