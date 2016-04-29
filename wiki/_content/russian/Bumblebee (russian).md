**Примечание:** пожалуйста сообщите об ошибках на [Bumblebee-Project](https://github.com/Bumblebee-Project/Bumblebee)'s GitHub как описано в [Wiki](https://github.com/Bumblebee-Project/Bumblebee/wiki/Reporting-Issues).

*Bumblebee это решение, позволяющее задействовать гибридную графику с Nvidia Optimus. Основатель проекта Martin Juhl*

## Contents

*   [1 О Bumblebee](#.D0.9E_Bumblebee)
    *   [1.1 Как это работает](#.D0.9A.D0.B0.D0.BA_.D1.8D.D1.82.D0.BE_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82)
*   [2 Сведения об установке](#.D0.A1.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BE.D0.B1_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B5)
    *   [2.1 Использование драйвера Nvidia](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0_Nvidia)
    *   [2.2 Использование драйвера Nouveau](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0_Nouveau)
*   [3 Запуск и тестирование](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B8_.D1.82.D0.B5.D1.81.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [3.1 Тестирование](#.D0.A2.D0.B5.D1.81.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [3.2 Запуск программ (примеры)](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC_.28.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B.29)
*   [4 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [4.1 Оптимизация скорости](#.D0.9E.D0.BF.D1.82.D0.B8.D0.BC.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D1.81.D0.BA.D0.BE.D1.80.D0.BE.D1.81.D1.82.D0.B8)
        *   [4.1.1 Использование VirtualGL в качестве 'моста'](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_VirtualGL_.D0.B2_.D0.BA.D0.B0.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.B5_.27.D0.BC.D0.BE.D1.81.D1.82.D0.B0.27)
        *   [4.1.2 Использование Primus](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_Primus)
    *   [4.2 Энергосбережение](#.D0.AD.D0.BD.D0.B5.D1.80.D0.B3.D0.BE.D1.81.D0.B1.D0.B5.D1.80.D0.B5.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5)
        *   [4.2.1 Некорректная инициализация запуска видеокарты NVIDIA](#.D0.9D.D0.B5.D0.BA.D0.BE.D1.80.D1.80.D0.B5.D0.BA.D1.82.D0.BD.D0.B0.D1.8F_.D0.B8.D0.BD.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE.D0.BA.D0.B0.D1.80.D1.82.D1.8B_NVIDIA)
*   [5 Основные ошибки и варианты исправления](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D1.8B.D0.B5_.D0.BE.D1.88.D0.B8.D0.B1.D0.BA.D0.B8_.D0.B8_.D0.B2.D0.B0.D1.80.D0.B8.D0.B0.D0.BD.D1.82.D1.8B_.D0.B8.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [5.1 [VGL] ERROR: Could not open display :8](#.5BVGL.5D_ERROR:_Could_not_open_display_:8)
    *   [5.2 Xlib: extension "GLX" missing on display ":0.0"](#Xlib:_extension_.22GLX.22_missing_on_display_.22:0.0.22)
    *   [5.3 [ERROR]Cannot access secondary GPU: No devices detected](#.5BERROR.5DCannot_access_secondary_GPU:_No_devices_detected)
        *   [5.3.1 NVIDIA(0): Failed to assign any connected display devices to X screen 0](#NVIDIA.280.29:_Failed_to_assign_any_connected_display_devices_to_X_screen_0)
        *   [5.3.2 Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)](#Failed_to_initialize_the_NVIDIA_GPU_at_PCI:1:0:0_.28GPU_fallen_off_the_bus_.2F_RmInitAdapter_failed.21.29)
        *   [5.3.3 Could not load GPU driver](#Could_not_load_GPU_driver)
        *   [5.3.4 NOUVEAU(0): [drm] failed to set drm interface version](#NOUVEAU.280.29:_.5Bdrm.5D_failed_to_set_drm_interface_version)
    *   [5.4 /dev/dri/card0: failed to set DRM interface version 1.4: Permission denied](#.2Fdev.2Fdri.2Fcard0:_failed_to_set_DRM_interface_version_1.4:_Permission_denied)
    *   [5.5 ERROR: ld.so: object 'libdlfaker.so' from LD_PRELOAD cannot be preloaded: ignored](#ERROR:_ld.so:_object_.27libdlfaker.so.27_from_LD_PRELOAD_cannot_be_preloaded:_ignored)
    *   [5.6 Fatal IO error 11 (Resource temporarily unavailable) on X server](#Fatal_IO_error_11_.28Resource_temporarily_unavailable.29_on_X_server)

## О Bumblebee

[Optimus](http://www.nvidia.com/object/optimus_technology.html) реализует [технологию гибридной графики](http://hybrid-graphics-linux.tuxfamily.org/index.php?title=Hybrid_graphics) без аппаратного коммутатора. Интегрированная видеокарта выводит на экран,в то время,как дискретная видеокарта занимается рендерингом, который требует более высокой вычислительной мощности графического процессора. Технология NVIDIA Optimus дает большую производительность, сберегая при этом заряд вашей батареи, подключая дискретный графический процессор,когда это требуется.

Bumblebee это программное решение, базирующееся на VirtualGL и драйверах ядра, позволяющее использовать дискретный GPU, не имеющий физического подключения к экрану.

### Как это работает

Bumblebee реализует технологию Optimus в два шага;

*   Дискретная видеокарта производит рендеринг на виртуальном дисплее,в то время,как выводом на экран занимается интегрированная видеокарта
*   Дискретная видеокарта отключается от питания,когда ее вычислительная способность не требуется.

## Сведения об установке

Перед установкой Bumblebee убедитесь,что поддержка технологии NVIDIA Optimus включена в настройках BIOS,а также в том,что интегрированная видеокарта включена занята выводом на экран.

### Использование драйвера Nvidia

Установите с помощью [pacman](/index.php/Pacman "Pacman") :

*   [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) - Основной пакет, содержащий клиентское ПО

**Примечание:** [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) зависит от [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl),который обеспечивает [nvidia-libgl](https://www.archlinux.org/packages/?name=nvidia-libgl), [nvidia-340xx-libgl](https://www.archlinux.org/packages/?name=nvidia-340xx-libgl) и [nvidia-304xx-libgl](https://www.archlinux.org/packages/?name=nvidia-304xx-libgl) и не создает конфликты между разными версиями библиотек

*   [mesa](https://www.archlinux.org/packages/?name=mesa) - Open-source реализация OpenGL
*   [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) - Intel видеодрайвер
*   [nvidia](https://www.archlinux.org/packages/?name=nvidia), [nvidia-340xx](https://www.archlinux.org/packages/?name=nvidia-340xx), [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) - Проприетарные видеодрайвера NVIDIA

Если вы используете систему 64-битную систему,возможно,вам понадобятся библиотеки для запуска 32-битных приложений

*   [lib32-virtualgl](https://www.archlinux.org/packages/?name=lib32-virtualgl) - Обеспечивает виртуальный дисплей для рендеринга 32-битных приложений
*   [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) или [lib32-nvidia-340xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-utils) или [lib32-nvidia-304xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-utils) - Проприетарные утилиты NVIDIA для запуска 32-битных приложений
*   [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) в случае, если [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl) не установлен

После установки нужных пакетов добавьте нужных пользователей в группу `bumblebee`:

```
# gpasswd -a *user* bumblebee

```

А затем добавьте сервис Bumblebeed в автозапуск:

```
# systemctl enable bumblebeed

```

### Использование драйвера Nouveau

Для использования драйвера [Nouveau](/index.php/Nouveau "Nouveau") вы должны установить Bumblebee и некоторые дополнительные пакеты:

*   [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) - Эксперементальный 3D драйвер
*   [mesa](https://www.archlinux.org/packages/?name=mesa) - Пакет с Gallium3D драйвером и классическими 3D библиотеками

**Примечание:** Если при вызове `primusrun` с драйвером nouveau вы видите:
```
primus: fatal: failed to load any of the libraries: /usr/$LIB/nvidia/libGL.so.1 
/usr/$LIB/nvidia/libGL.so.1: Cannot open shared object file: No such file or directory

```

Экспортируйте путь к LibGL-библиотеке в переменную `PRIMUS_libGLa`:

```
export PRIMUS_libGLa='/usr/$LIB/libGL.so.1'

```
Для удобства можно сделать скрипт.

## Запуск и тестирование

### Тестирование

**Примечание:** Для использования `glxgears` и `glxspheres32`, `glxspheres64` требуется установить пакет [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos)

Протестируйте bumblebee:

```
$ optirun glxgears -info

```

Если это не сработало

*   64-битная система:

```
$ optirun glxspheres64

```

*   32-битная система:

```
$ optirun glxspheres32

```

**Примечание:** Если `glxgears` не запустилось,а `glxspheresXX` работает, используйте `glxspheresXX` во всех случаях

### Запуск программ (примеры)

```
$ optirun [options] application [application-options]

```

Для примера, запуск [firefox](https://www.archlinux.org/packages/?name=firefox) с параметром 'www.yandex.ru':

```
$ optirun firefox www.yandex.ru

```

Для просмотра документации и всех опций `optirun` используйте следующую команду:

```
$ man optirun

```

## Настройка

Вы можете настраивать bumblebee под свои нужды, редактируя `/etc/bumblebee/bumblebee.conf`

### Оптимизация скорости

#### Использование VirtualGL в качестве 'моста'

Bumblebee отрисовывает, используя дискретную видеокарту NVIDIA на виртуальном дисплее с помощью VirtualGL,а затем отрисовка происходит на 'реальном' дисплее, когда интегрированная видеокарта передает изображение на `X Server`. Для увеличения скорости передачи `'Виртуальный дисплей'->'X Server'` можно использовать различные методы сжатия,вызывая `optirun` с опцией `-c`

```
$ optirun -c compress-method application [application-options]

```

Методы со сжатием:

*   `jpeg`
*   `rgb`
*   `yuv`

Методы без сжатия

*   `proxy`
*   `xv`

Таблица производительности с [ASUS N550JV](/index.php/ASUS_N550JV "ASUS N550JV") приложение для тестирования: [unigine-heaven](https://aur.archlinux.org/packages/unigine-heaven/):

| Command | FPS | Score | Min FPS | Max FPS |
| optirun unigine-heaven | 25.0 | 630 | 16.4 | 36.1 |
| optirun -c jpeg unigine-heaven | 24.2 | 610 | 9.5 | 36.8 |
| optirun -c rgb unigine-heaven | 25.1 | 632 | 16.6 | 35.5 |
| optirun -c yuv unigine-heaven | 24.9 | 626 | 16.5 | 35.8 |
| optirun -c proxy unigine-heaven | 25.0 | 629 | 16.0 | 36.1 |
| optirun -c xv unigine-heaven | 22.9 | 577 | 15.4 | 32.2 |

Для использования метода сжатия по-умолчанию выставьте переменную `VGLTransport` c параметром `*compress-method*` в `/etc/bumblebee/bumblebee.conf`:

 `/etc/bumblebee/bumblebee.conf` 
```
[...]
[optirun]
VGLTransport=proxy
[...]
```

#### Использование Primus

[Primus](http://www.github.com/amonakov/primus) позволяет увеличить производительность и энергосбережение за счет неиспользования VirtualGL. Преимущества [Primus](http://www.github.com/amonakov/primus) перед стандартным `Optirun`:

*   уменьшенное использование дополнительных ресурсов (увеличена частота кадров) и оптимизированное решение (без сетевых процессов или процессов сжатия)
*   отсутствие бага с преждевременным выключением GPU
*   более стабильный,нежели `Optirun`, а также более прост в отладке
*   дискретная видеокарта используется только для обработки OpenGL,вся остальная информация обрабатывается и хранится в интегрированном графическом процессоре

**Примечание:** Для использования `primus` понадобится пакет [primus](https://www.archlinux.org/packages/?name=primus).

*   Для запуска 32-битных приложений на 64-битной машине понадобится пакет [lib32-primus](https://www.archlinux.org/packages/?name=lib32-primus) (Должен быть подключен [Multilib (Русский)](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)"))

Пример запуска `glxspheres32`:

```
$ primusrun glxspheres32

```

Для запуска приложения с ипользованием VirtualGL используйте:

```
$ optirun -b primus glxspheres32

```

### Энергосбережение

Для регулировки потребления энергии на десктопном ПК используется пакет [bbswitch](https://www.archlinux.org/packages/?name=bbswitch)

**Примечание:** Bumblebee не умеет регулировать потребление энергии на ПК самостоятельно.

Для настройки включения и отключения видеокарты редактируйте опции `load_state` и `unload_state`. Подробнее смотрите [BBSwitch-документация](https://github.com/Bumblebee-Project/bbswitch).

 `/etc/modprobe.d/bbswitch.conf`  `options bbswitch load_state=0 unload_state=1` 

#### Некорректная инициализация запуска видеокарты NVIDIA

Если ваша видеокарта NVidia некорректно запускается после последнего выключения, то следует выставить опцию `TurnCardOffAtExit=false` в `/etc/bumblebee/bumblebee.conf` - видеокарта будет выключаться каждый раз после отключения демона bumblebee. Для того,чтобы видеокарта NVidia постоянно работала,следует включить соответствующий сервис:

```
# systemctl enable nvidia-enable.service

```
 `/etc/systemd/system/nvidia-enable.service` 
```
[Unit]
Description=Enable NVIDIA card
DefaultDependencies=no

[Service]
Type=oneshot
ExecStart=/bin/sh -c 'echo ON > /proc/acpi/bbswitch'

[Install]
WantedBy=shutdown.target
```

Для более подробного разбора всех возможностей Bumblebee посетите английскую ветку wiki: [bumblebee](/index.php/Bumblebee "Bumblebee")

## Основные ошибки и варианты исправления

### [VGL] ERROR: Could not open display :8

Проблема заключается в VirtualGL, в этом случае можно использовать primus

```
$ optirun -b primus wine windows program.exe

```

Если использование драйвера NVIDIA решило проблему,то отредактируйте файл `/etc/bumblebee/xorg.conf.nvidia` и измените опцию `ConnectedMonitor` на `CRT-0`.

### Xlib: extension "GLX" missing on display ":0.0"

Если вы установили видеодрайвер с сайта NVidia, то попробуйте проделать следующее

1\. Удалите драйвер:

```
# ./NVIDIA-Linux-*.run --uninstall

```

2\. Удалите сгенерированный xorg.conf:

```
# rm /etc/X11/xorg.conf

```

3\. Переустановите корректный видеодрайвер: [#Использование драйвера Nvidia](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0_Nvidia)

### [ERROR]Cannot access secondary GPU: No devices detected

В некоторых случаях запуск `optirun` возвращает сообщение об ошибке вида:

```
[ERROR]Cannot access secondary GPU - error: [XORG] (EE) No devices detected.
[ERROR]Aborting because fallback start is disabled.

```

В этом случае вам следует переместить файл `/etc/X11/xorg.conf.d/20-intel.conf` куда-нибудь в другое место,а затем сделать [restart](/index.php/Restart "Restart") the bumblebeed демона и это должно сработать. Если же вам нужны настройки модулей Intel, то соедините файл `/etc/X11/xorg.conf.d/20-intel.conf` c `/etc/X11/xorg.conf`.

Закомментируйте строку `Drive` в `/etc/X11/xorg.conf.d/10-monitor.conf`.

Если вы используете драйвер `nouveau` попробуйте поменять его на `nvidia` драйвер.

Вам требуется обозначить видеокарту (в конфигурационных файлах `/etc/X11/xorg.conf.d`), используя корректный `BusID` получив его выводом команды `lspci`;

```
Section "Device"
    Identifier "nvidiagpu1"
    Driver "nvidia"
    BusID "PCI:0:1:0"
EndSection

```

#### NVIDIA(0): Failed to assign any connected display devices to X screen 0

Если консоль возвращает сообщения об ошибке вида:

```
[ERROR]Cannot access secondary GPU - error: [XORG] (EE) NVIDIA(0): Failed to assign any connected display devices to X screen 0
[ERROR]Aborting because fallback start is disabled.

```

Вы должны поменять эту строку в `/etc/bumblebee/xorg.conf.nvidia`:

```
Option "ConnectedMonitor" "DFP"

```

На:

```
Option "ConnectedMonitor" "CRT"

```

#### Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)

Добавьте `rcutree.rcu_idle_gp_delay=1` в [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") из [bootloader](/index.php/Bootloader "Bootloader") конфигурации (подробнее [BBS post](https://bbs.archlinux.org/viewtopic.php?id=169742) для примера).

#### Could not load GPU driver

Если консоль возвращает сообщения об ошибке вида:

```
[ERROR]Cannot access secondary GPU - error: Could not load GPU driver

```

И вы пробуете загрузить модуль nvidia, но получаете это:

```
modprobe nvidia
modprobe: ERROR: could not insert 'nvidia': Exec format error

```

Это происходит потому,что видеодрайвер не может синхронизироваться с ядром, к примеру,если вы установили последний драйвер nvidia, но не можете обновить ядро. Полное обновление системы поможет исправить эту проблему. Если проблема не ушла,то попробуйте вручную скомпилировать пакеты nvidia для своего ядра. Потребуются: [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) или скомпилированный [nvidia](https://www.archlinux.org/packages/?name=nvidia) из [ABS](/index.php/ABS "ABS").

#### NOUVEAU(0): [drm] failed to set drm interface version

Примите во внимание то,что nouveau драйвер в стадии тестирования. Как написано тут: [here](https://github.com/Bumblebee-Project/Bumblebee/issues/438#issuecomment-22005923), лучшим выходом будет - установка официального драйвера nvidia.

### /dev/dri/card0: failed to set DRM interface version 1.4: Permission denied

Это можно решить, добавив в `/etc/bumblebee/xorg.conf.nvidia` несколько строк. (Подробнее [тут](https://github.com/Bumblebee-Project/Bumblebee/issues/580)):

```
Section "Screen"
    Identifier "Default Screen"
    Device "DiscreteNvidia"
EndSection

```

### ERROR: ld.so: object 'libdlfaker.so' from LD_PRELOAD cannot be preloaded: ignored

Вы пытаетесь запустить 32-битное приложение. Решит проблему запуск приложения через `primus`

### Fatal IO error 11 (Resource temporarily unavailable) on X server

Измените параметр `KeepUnusedXServer` в `/etc/bumblebee/bumblebee.conf` c `false` на `true`. Программа запустится в фоновом режиме и bumblebee не будет 'видеть' её.