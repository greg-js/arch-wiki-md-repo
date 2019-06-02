Related articles

*   [PRIME](/index.php/PRIME "PRIME")
*   [Nvidia-xrun (Русский)](/index.php/Nvidia-xrun_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nvidia-xrun (Русский)")
*   [NVIDIA Optimus (Русский)](/index.php/NVIDIA_Optimus_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA Optimus (Русский)")
*   [Nouveau (Русский)](/index.php/Nouveau_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nouveau (Русский)")
*   [NVIDIA (Русский)](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)")
*   [Intel graphics (Русский)](/index.php/Intel_graphics_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Intel graphics (Русский)")

Из [FAQ](https://github.com/Bumblebee-Project/Bumblebee/wiki/FAQ) Bumblebee:

*Bumblebee — решение, позволяющее задействовать NVIDIA Optimus в ноутбуках с GNU/Linux, что включает в себя два графических адаптера с двумя разными профилями энергопотребления, использующих общий фреймбуфер.*

**Примечание:** Рассмотрите [nvidia-xrun (Русский)](/index.php/Nvidia-xrun_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nvidia-xrun (Русский)") или [PRIME](/index.php/PRIME "PRIME") в качестве альтернативы, так как у Bumblebee присутствуют значительные проблемы с производительностью[[1]](https://github.com/Witko/nvidia-xrun/issues/4#issuecomment-153386837)[[2]](https://bbs.archlinux.org/viewtopic.php?pid=1822926) и не планируется поддержка [Vulkan](/index.php/Vulkan "Vulkan")[[3]](https://github.com/Bumblebee-Project/Bumblebee/issues/769#issuecomment-218016574).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Bumblebee: Optimus для Linux](#Bumblebee:_Optimus_для_Linux)
*   [2 Установка](#Установка)
*   [3 Использование](#Использование)
    *   [3.1 Тестирование](#Тестирование)
    *   [3.2 Запуск программ](#Запуск_программ)
*   [4 Настройка](#Настройка)
    *   [4.1 Оптимизация скорости](#Оптимизация_скорости)
        *   [4.1.1 Использование VirtualGL в качестве 'моста'](#Использование_VirtualGL_в_качестве_'моста')
        *   [4.1.2 Использование Primus](#Использование_Primus)
    *   [4.2 Энергосбережение](#Энергосбережение)
        *   [4.2.1 Некорректная инициализация запуска видеокарты NVIDIA](#Некорректная_инициализация_запуска_видеокарты_NVIDIA)
*   [5 Решение проблем](#Решение_проблем)
    *   [5.1 [VGL] ERROR: Could not open display :8](#[VGL]_ERROR:_Could_not_open_display_:8)
    *   [5.2 Xlib: extension "GLX" missing on display ":0.0"](#Xlib:_extension_"GLX"_missing_on_display_":0.0")
    *   [5.3 [ERROR]Cannot access secondary GPU: No devices detected](#[ERROR]Cannot_access_secondary_GPU:_No_devices_detected)
        *   [5.3.1 NVIDIA(0): Failed to assign any connected display devices to X screen 0](#NVIDIA(0):_Failed_to_assign_any_connected_display_devices_to_X_screen_0)
        *   [5.3.2 Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)](#Failed_to_initialize_the_NVIDIA_GPU_at_PCI:1:0:0_(GPU_fallen_off_the_bus_/_RmInitAdapter_failed!))
        *   [5.3.3 Could not load GPU driver](#Could_not_load_GPU_driver)
        *   [5.3.4 NOUVEAU(0): [drm] failed to set drm interface version](#NOUVEAU(0):_[drm]_failed_to_set_drm_interface_version)
    *   [5.4 /dev/dri/card0: failed to set DRM interface version 1.4: Permission denied](#/dev/dri/card0:_failed_to_set_DRM_interface_version_1.4:_Permission_denied)
    *   [5.5 ERROR: ld.so: object 'libdlfaker.so' from LD_PRELOAD cannot be preloaded: ignored](#ERROR:_ld.so:_object_'libdlfaker.so'_from_LD_PRELOAD_cannot_be_preloaded:_ignored)
    *   [5.6 Fatal IO error 11 (Resource temporarily unavailable) on X server](#Fatal_IO_error_11_(Resource_temporarily_unavailable)_on_X_server)

## Bumblebee: Optimus для Linux

[Optimus](https://www.nvidia.com/object/optimus_technology.html) реализует [технологию гибридной графики](https://hybrid-graphics-linux.tuxfamily.org/index.php?title=Hybrid_graphics) без аппаратного коммутатора. Интегрированная видеокарта выводит на экран,в то время,как дискретная видеокарта занимается рендерингом, который требует более высокой вычислительной мощности графического процессора. Технология NVIDIA Optimus дает большую производительность, сберегая при этом заряд батареи, подключая дискретный графический процессор, когда это требуется.

Bumblebee — программное решение, базирующееся на VirtualGL и драйверах ядра, позволяющее использовать дискретный GPU, не имеющий физического подключения к экрану.

Bumblebee реализует технологию Optimus в два шага:

*   Дискретная видеокарта производит рендеринг на виртуальном дисплее, в то время как выводом на экран занимается интегрированная видеокарта.
*   Дискретная видеокарта отключается от питания, когда ее вычислительная способность не требуется.

## Установка

Перед установкой Bumblebee убедитесь, что поддержка NVIDIA Optimus включена в настройках BIOS, а дисплей подключён к интегрированной видеокарте.

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите"):

*   [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) — Основной пакет, содержащий демон и клиентское ПО.
*   [mesa](https://www.archlinux.org/packages/?name=mesa) — Свободную реализацию спецификации **OpenGL**.
*   Соответствующую версию драйвера NVIDIA, см. [NVIDIA#Installation](/index.php/NVIDIA#Installation "NVIDIA").
*   Опционально установите [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) — драйвер [Xorg (Русский)](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)") для Intel.

Также включите репозиторий [multilib](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)") для поддержки 32-битных приложений и установите:

*   [lib32-virtualgl](https://www.archlinux.org/packages/?name=lib32-virtualgl) — виртуальный дисплей для рендеринга в 32-битных приложениях.
*   [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) или [lib32-nvidia-340xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-utils) (должен соответствовать версии обычного драйвера NVIDIA).

Чтобы использовать Bumblebee, необходимо добавить обычного *пользователя* в группу `bumblebee`:

```
# gpasswd -a *user* bumblebee

```

Также [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") службу `bumblebeed.service`, перезагрузите систему и см. раздел [#Использование](#Использование).

## Использование

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

### Запуск программ

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

[Primus](https://www.github.com/amonakov/primus) позволяет увеличить производительность и энергосбережение за счет неиспользования VirtualGL. Преимущества [Primus](https://www.github.com/amonakov/primus) перед стандартным `Optirun`:

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

## Решение проблем

**Примечание:** Пожалуйста, сообщайте об ошибках на GitHub-странице [Bumblebee-Project](https://github.com/Bumblebee-Project/Bumblebee) в соответствии с его [вики-разделом](https://github.com/Bumblebee-Project/Bumblebee/wiki/Reporting-Issues).

### [VGL] ERROR: Could not open display :8

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

3\. Переустановите корректный видеодрайвер: [#Использование драйвера Nvidia](#Использование_драйвера_Nvidia)

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