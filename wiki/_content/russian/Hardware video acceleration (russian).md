**Состояние перевода:** На этой странице представлен перевод статьи [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration"). Дата последней синхронизации: 8 февраля 2020\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Hardware_video_acceleration&diff=0&oldid=596900).

[Аппаратное ускорение видео](https://en.wikipedia.org/wiki/Graphics_processing_unit#GPU_accelerated_video_decoding "wikipedia:Graphics processing unit") (англ.) позволяет выполнять операции кодирования и декодирования видео на стороне видеокарты, разгружая CPU и экономя энергию.

Существуют несколько реализаций этой технологии на Linux:

*   [Video Acceleration API](https://www.freedesktop.org/wiki/Software/vaapi/) (VA-API) — разработанная Intel спецификация и свободная библиотека, предоставляющая аппаратное ускорение кодирования и декодирования видео.
*   [Video Decode and Presentation API for Unix](https://www.freedesktop.org/wiki/Software/VDPAU/) (VDPAU) — разработанная NVIDIA свободная библиотека и API для переноса части процесса декодирования видео и его постобработки на сторону GPU.
*   [NVDECODE/NVENCODE](https://developer.nvidia.com/nvidia-video-codec-sdk) — проприетарные API аппаратного ускорения, используемые в таких поколениях GPU от NVIDIA, как Fermi, Kepler, Maxwell и Pascal.

Для получения информации о видеокартах, выпущенных до 2007 года, см. [XvMC](/index.php/XvMC "XvMC"). Также всесторонний обзор поддержки данных технологий со стороны драйверов и приложений доступен в разделе [#Сравнительные таблицы](#Сравнительные_таблицы).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
    *   [1.1 Intel](#Intel)
    *   [1.2 NVIDIA](#NVIDIA)
    *   [1.3 ATI/AMD](#ATI/AMD)
    *   [1.4 Слои преобразований](#Слои_преобразований)
*   [2 Проверка](#Проверка)
    *   [2.1 Проверка VA-API](#Проверка_VA-API)
    *   [2.2 Проверка VDPAU](#Проверка_VDPAU)
*   [3 Настройка](#Настройка)
    *   [3.1 Настройка VA-API](#Настройка_VA-API)
    *   [3.2 Настройка VDPAU](#Настройка_VDPAU)
*   [4 Решение проблем](#Решение_проблем)
    *   [4.1 Ошибка "Failed to open VDPAU backend"](#Ошибка_"Failed_to_open_VDPAU_backend")
    *   [4.2 Ошибка "init failed" с VAAPI](#Ошибка_"init_failed"_с_VAAPI)
*   [5 Сравнительные таблицы](#Сравнительные_таблицы)
    *   [5.1 Драйверы VA-API](#Драйверы_VA-API)
    *   [5.2 Драйверы VDPAU](#Драйверы_VDPAU)
    *   [5.3 Драйвер NVIDIA](#Драйвер_NVIDIA)
    *   [5.4 Поддержка приложениями](#Поддержка_приложениями)

## Установка

### Intel

Свободные драйверы [Intel graphics](/index.php/Intel_graphics_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Intel graphics (Русский)") поддерживают VA-API:

*   Серия HD Graphics, начиная с [Broadwell](https://github.com/intel/media-driver/#supported-platforms) [(~2015)](https://en.wikipedia.org/wiki/Template:Intel_processor_roadmap "wikipedia:Template:Intel processor roadmap") и новее, поддерживается [intel-media-driver](https://www.archlinux.org/packages/?name=intel-media-driver).
*   GMA 4500 [series](https://01.org/linuxmedia/vaapi) и более новые GPU до [Coffee Lake](https://en.wikipedia.org/wiki/ru:Coffee_Lake "wikipedia:ru:Coffee Lake") поддерживаются [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver).
*   Декодирование H.264 на GMA 4500 поддерживается [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/), см. [Intel graphics (Русский)#Декодирование H.264 на GMA 4500](/index.php/Intel_graphics_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Декодирование_H.264_на_GMA_4500 "Intel graphics (Русский)").
*   Гибридное декодирование VP9 на процессорах от Broadwell до Skylake, а также гибридное декодирование VP8 на процессорах от Haswell до Skylake, поддерживается [intel-hybrid-codec-driver](https://aur.archlinux.org/packages/intel-hybrid-codec-driver/). См. также отчёт об ошибке "[Сбои декодирования VP9 на Haswell](https://github.com/intel/intel-hybrid-driver/issues/21)" (англ.).

### NVIDIA

Свободный драйвер [Nouveau](/index.php/Nouveau_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nouveau (Русский)") поддерживает как VA-API, так и VDPAU:

*   GeForce 8 series и новее (до GeForce GTX 750) поддерживаются [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver) и [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau).
*   [Необходим](https://nouveau.freedesktop.org/wiki/VideoAcceleration/#firmware) [nouveau-fw](https://aur.archlinux.org/packages/nouveau-fw/) — пакет с микропрограммой, которая на сегодняшний день извлекается из бинарного драйвера NVIDIA.

Проприетарный драйвер [NVIDIA](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)") поддерживает следующие технологии с помощью пакета [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils):

*   VDPAU на серии [GeForce 8](https://en.wikipedia.org/wiki/ru:GeForce_8 "wikipedia:ru:GeForce 8") и новее;
*   NVDECODE на [Fermi](https://en.wikipedia.org/wiki/Fermi_(microarchitecture) и новее [[1]](https://developer.download.nvidia.com/assets/cuda/files/NVIDIA_Video_Decoder.pdf);
*   NVENCODE на [Kepler](https://en.wikipedia.org/wiki/ru:Kepler_(%D0%BC%D0%B8%D0%BA%D1%80%D0%BE%D0%B0%D1%80%D1%85%D0%B8%D1%82%D0%B5%D0%BA%D1%82%D1%83%D1%80%D0%B0) и новее.

### ATI/AMD

Свободные драйверы [ATI](/index.php/ATI_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ATI (Русский)") и [AMDGPU](/index.php/AMDGPU_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AMDGPU (Русский)") поддерживают как VA-API, так и VDPAU:

*   VA-API на Radeon HD 2000 и новее поддерживается [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver).
*   VDPAU на Radeon R300 и новее поддерживается [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau).

Проприетарный драйвер [AMDGPU PRO](/index.php/AMDGPU_PRO "AMDGPU PRO") основывается на драйвере AMDGPU и поддерживает как VA-API, так и VDPAU.

### Слои преобразований

Активация поддержки VA-API при её отсутствии в драйвере:

*   [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) – бекенд VDPAU для VA-API.
*   [libva-vdpau-driver-chromium](https://aur.archlinux.org/packages/libva-vdpau-driver-chromium/) – бекенд VDPAU для VA-API с патчем, позволяющим взаимодействовать с [Chromium](/index.php/Chromium "Chromium").
*   [libva-vdpau-driver-vp9-git](https://aur.archlinux.org/packages/libva-vdpau-driver-vp9-git/) – экспериментальная поддержка VP9.

Активация поддержки VDPAU при её отсутствии в драйвере:

*   [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) – бекенд VA-API для VDPAU, [поддерживается только H.264](https://github.com/i-rinat/libvdpau-va-gl/issues/67#issuecomment-318470175) (англ.).

## Проверка

Аппаратное ускорение, скорее всего, хорошо заработает по умолчанию. Проверить это можно описанными ниже способами.

**Совет:** [mpv](/index.php/Mpv#Hardware_video_acceleration "Mpv") отлично подходит для проверки аппаратного ускорения на практике.

### Проверка VA-API

Проверьте настройки VA-API, выполнив `vainfo` (предоставляется пакетом [libva-utils](https://www.archlinux.org/packages/?name=libva-utils)):

 `$ vainfo` 
```
libva info: VA-API version 0.39.4
libva info: va_getDriverName() returns 0
libva info: Trying to open /usr/lib/dri/i965_drv_video.so
libva info: Found init function __vaDriverInit_0_39
libva info: va_openDriver() returns 0
vainfo: VA-API version: 0.39 (libva 1.7.3)
vainfo: Driver version: Intel i965 driver for Intel(R) Skylake - 1.7.3
vainfo: Supported profile and entrypoints
      VAProfileMPEG2Simple            :	VAEntrypointVLD
      VAProfileMPEG2Simple            :	VAEntrypointEncSlice
      VAProfileMPEG2Main              :	VAEntrypointVLD
      VAProfileMPEG2Main              :	VAEntrypointEncSlice
      VAProfileH264ConstrainedBaseline:	VAEntrypointVLD
      VAProfileH264ConstrainedBaseline:	VAEntrypointEncSlice
      VAProfileH264ConstrainedBaseline:	VAEntrypointEncSliceLP
      VAProfileH264Main               :	VAEntrypointVLD
      VAProfileH264Main               :	VAEntrypointEncSlice
      VAProfileH264Main               :	VAEntrypointEncSliceLP
      VAProfileH264High               :	VAEntrypointVLD
      VAProfileH264High               :	VAEntrypointEncSlice
      VAProfileH264High               :	VAEntrypointEncSliceLP
      VAProfileH264MultiviewHigh      :	VAEntrypointVLD
      VAProfileH264MultiviewHigh      :	VAEntrypointEncSlice
      VAProfileH264StereoHigh         :	VAEntrypointVLD
      VAProfileH264StereoHigh         :	VAEntrypointEncSlice
      VAProfileVC1Simple              :	VAEntrypointVLD
      VAProfileVC1Main                :	VAEntrypointVLD
      VAProfileVC1Advanced            :	VAEntrypointVLD
      VAProfileNone                   :	VAEntrypointVideoProc
      VAProfileJPEGBaseline           :	VAEntrypointVLD
      VAProfileJPEGBaseline           :	VAEntrypointEncPicture
      VAProfileVP8Version0_3          :	VAEntrypointVLD
      VAProfileVP8Version0_3          :	VAEntrypointEncSlice
      VAProfileHEVCMain               :	VAEntrypointVLD
      VAProfileHEVCMain               :	VAEntrypointEncSlice

```

`VAEntrypointVLD` означает, что видеокарта способна декодировать данный формат, а `VAEntrypointEncSlice` означает, что данный формат можно кодировать.

В данном примере используется драйвер `i965`:

```
libva info: Trying to open /usr/lib/dri/**i965**_drv_video.so

```

Если при выполнении `vainfo` отображается следующая ошибка:

```
libva info: va_openDriver() returns -1
vaInitialize failed with error code -1 (unknown libva error),exit

```

Необходимо задать корректный драйвер, см. [#Настройка VA-API](#Настройка_VA-API).

### Проверка VDPAU

Установите пакет [vdpauinfo](https://www.archlinux.org/packages/?name=vdpauinfo), чтобы получить полный отчёт о конфигурации драйвера VDPAU и убедиться, что он загружен корректно:

 `$ vdpauinfo` 
```
display: :0   screen: 0
API version: 1
Information string: G3DVL VDPAU Driver Shared Library version 1.0

Video surface:

name   width height types

* * *

420    16384 16384  NV12 YV12 
422    16384 16384  UYVY YUYV 
444    16384 16384  Y8U8V8A8 V8U8Y8A8 

Decoder capabilities:

name                        level macbs width height

* * *

MPEG1                          --- not supported ---
MPEG2_SIMPLE                    3  9216  2048  1152
MPEG2_MAIN                      3  9216  2048  1152
H264_BASELINE                  41  9216  2048  1152
H264_MAIN                      41  9216  2048  1152
H264_HIGH                      41  9216  2048  1152
VC1_SIMPLE                      1  9216  2048  1152
VC1_MAIN                        2  9216  2048  1152
VC1_ADVANCED                    4  9216  2048  1152

..

```

## Настройка

Несмотря на то, что видеодрайвер должен автоматически активировать поддержку аппаратного ускорения видео с помощью VA-API и VDPAU, в некоторых случаях может потребоваться настроить VA-API/VDPAU вручную. Перед тем как продолжать чтение данного раздела, просмотрите раздел [#Проверка](#Проверка).

Названия драйверов по умолчанию угадываются системой, если остутствуют какие-либо другие настройки. Однако они часто не совпадают и не работают. Предполагаемые значения можно просмотреть, выполнив следующую команду:

 `$ grep -iE 'vdpau | dri driver' /var/log/Xorg.0.log` 
```
(II) RADEON(0): [DRI2] DRI driver: radeonsi
(II) RADEON(0): [DRI2] VDPAU driver: radeonsi

```

В данном случае по умолчанию используется `radeonsi` для VA-API и VDPAU.

**Примечание:** Если используется [GDM](/index.php/GDM "GDM"), выполните вместо этого следующую команду: `journalctl -b | grep -iE 'vdpau | dri driver'`.

### Настройка VA-API

[Драйвер](https://www.freedesktop.org/wiki/Software/vaapi/#driversback-endsthatimplementva-api) VA-API можно переопределить с помощью [переменной окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `LIBVA_DRIVER_NAME`:

*   [Intel graphics](/index.php/Intel_graphics_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Intel graphics (Русский)"):
    *   Укажите `i965`, если используется [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver).
    *   Укажите `iHD`, если используется [intel-media-driver](https://www.archlinux.org/packages/?name=intel-media-driver).
*   NVIDIA:
    *   Укажите `nouveau`, если используется [Nouveau](/index.php/Nouveau_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nouveau (Русский)").
    *   Укажите `vdpau`, если используется [NVIDIA](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)").
*   ATI/AMD:
    *   Укажите `radeonsi`, если используется [AMDGPU](/index.php/AMDGPU "AMDGPU").
    *   Укажите `fglrx`, если используется [AMD Catalyst](/index.php/AMD_Catalyst_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AMD Catalyst (Русский)").

**Примечание:**

*   Установленные драйверы находятся в `/usr/lib/dri/` и используются как `/usr/lib/dri/**${LIBVA_DRIVER_NAME}**_drv_video.so`.
*   Некоторые драйверы устанавливаются несколько раз под разными именами в целях совместимости. Их список можно увидеть, выполнив команду `sha1sum /usr/lib/dri/*`.
*   `LIBVA_DRIVERS_PATH` может использоваться для переопределения расположения драйверов VA-API.
*   Начиная с версии 12.0.1, [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver) предоставляет `radeonsi` вместо `gallium`.

### Настройка VDPAU

Драйвер VDPAU можно переопределить с помощью [переменной окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `VDPAU_DRIVER`.

Корректное название драйвера зависит от конфигурации:

*   Если используется Intel Graphics или AMD Catalyst, [необходимо](#Ошибка_"Failed_to_open_VDPAU_backend") задать `va_gl`.
*   Если используется свободный драйвер AMD/ATI, задайте соответствующую версию драйвера, в зависимости от видеокарты. См. [#Проверка](#Проверка).
*   Если используется свободный драйвер Nouveau, задайте `nouveau`.
*   Если используется проприетарный драйвер NVIDIA, задайте `nvidia`.

**Примечание:**

*   Установленные драйверы находятся в `/usr/lib/vdpau/` и используются как `/usr/lib/vdpau/libvdpau_**${VDPAU_DRIVER}**.so`.
*   Некоторые драйверы устанавливаются несколько раз под разными именами в целях совместимости. Их список можно увидеть, выполнив команду `sha1sum /usr/lib/vdpau/*`.
*   В случае с конфигурацией с гибридной графикой (как с NVIDIA, так и с AMD), может потребоваться [задать](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") переменную окружения `DRI_PRIME=1`. См. статью [PRIME](/index.php/PRIME "PRIME") для получения более подробной информации.

## Решение проблем

### Ошибка "Failed to open VDPAU backend"

Необходимо задать переменную `VDPAU_DRIVER`, указывающую на корректный драйвер. См. [#Настройка VDPAU](#Настройка_VDPAU).

### Ошибка "init failed" с VAAPI

Данная ошибка (например, `libva: /usr/lib/dri/i965_drv_video.so init failed`) может происходить из-за неправильного определения Wayland. Одно из решений — сбросить переменную `$DISPLAY`, таким образом, mpv, MPlayer, VLC и т.д. не будут исходить из того, что используется X11\. Также можно добавить аргумент `--gpu-context=wayland`, если используется mpv.

## Сравнительные таблицы

### Драйверы VA-API

| Кодек | [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) [[2]](https://github.com/01org/intel-vaapi-driver/blob/master/README) | [intel-media-driver](https://www.archlinux.org/packages/?name=intel-media-driver) [[3]](https://github.com/intel/media-driver/blob/master/README.md) | [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver) [[4]](https://www.x.org/wiki/RadeonFeature/) [[5]](https://nouveau.freedesktop.org/wiki/VideoAcceleration/) | [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver)
(адаптер VDPAU) |
| Декодирование |
| MPEG-2 | GMA 4500 и новее | Broadwell и новее | Radeon HD 6000 и новее
GeForce 8 и новее | См. [#Драйверы VDPAU](#Драйверы_VDPAU) |
| MPEG-4 | Нет | Нет | Radeon HD 6000 и новее |
| VC-1 | Sandy Bridge и новее | Broadwell и новее | Radeon HD 2000 и новее
GeForce 9300 и новее |
| H.264/MPEG-4 AVC | GMA 4500, Ironlake и новее | Radeon HD 2000 и новее
GeForce 8 и новее |
| H.265/HEVC 8bit | Cherryview/Braswell и новее | Skylake и новее | Radeon R9 Fury и новее |
| H.265/HEVC 10bit | Broxton и новее | Broxton/Apollo Lake и новее | Radeon 400 и новее |
| VP8 | Broadwell и новее | Broadwell и новее | Нет | Нет |
| VP9 8bit | Broxton и новее
Гибридное: Broadwell to Skylake | Broxton/Apollo Lake и новее | Raven Ridge и новее | См. [#Драйверы VDPAU](#Драйверы_VDPAU) |
| VP9 10bit | Kaby Lake и новее | Kaby Lake и новее | Нет |
| Кодирование |
| MPEG-2 | Ivy Bridge и новее | Broadwell и новее
кроме Broxton/Apollo Lake | Нет | – |
| H.264/MPEG-4 AVC | Sandy Bridge и новее | Broadwell и новее | Radeon HD 7000 и новее |
| H.265/HEVC 8bit | Skylake и новее | Skylake и новее | Radeon 400 и новее |
| H.265/HEVC 10bit | Kaby Lake и новее | Kaby Lake и новее | Raven Ridge и новее |
| VP8 | Cherryview/Braswell и новее
Гибридное: от Haswell до Skylake | Нет |
| VP9 8bit | Kaby Lake и новее | Icelake и новее |
| VP9 10bit | Нет |

*   До GeForce GTX 750.
*   Поддерживается [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/).
*   Гибридный кодировщик VP8 и декодировщик VP9 поддерживается [intel-hybrid-codec-driver](https://aur.archlinux.org/packages/intel-hybrid-codec-driver/). См. также "[Сбои декодирования VP9 на Haswell](https://github.com/intel/intel-hybrid-driver/issues/21)" (англ.).
*   MPEG-4 отключён по умолчанию из-за ограничений VAAPI. Задайте [переменную окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `VAAPI_MPEG4_ENABLED=true`, если вы всё-таки хотите протестировать данную функцию.
*   Экспериментальная поддержка VP9 доступна в [libva-vdpau-driver-vp9-git](https://aur.archlinux.org/packages/libva-vdpau-driver-vp9-git/).

### Драйверы VDPAU

| Кодек | [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) [[6]](https://www.x.org/wiki/RadeonFeature/) [[7]](https://nouveau.freedesktop.org/wiki/VideoAcceleration/) | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) | [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl)
(адаптер VA-API) |
| Декодирование |
| MPEG-2 | Radeon R300 и новее
GeForce 8 и новее | GeForce 8 и новее | Нет |
| MPEG-4 | Radeon HD 6000 и новее
GeForce 200 и новее | GeForce 200 и новее |
| VC-1 | Radeon HD 2000 и новее
GeForce 9300 и новее | GeForce 8 и новее |
| H.264/MPEG-4 AVC | Radeon HD 2000 и новее
GeForce 8 и новее | GeForce 8 и новее | См. [#Драйверы VA-API](#Драйверы_VA-API) |
| H.265/HEVC 8bit | Radeon R9 Fury и новее | GeForce 900 и новее | Нет |
| H.265/HEVC 10bit | Radeon 400 и новее | Нет |
| VP9 8bit | Нет | GeForce 900 и новее |
| VP9 10bit | Нет | Нет |

*   До GeForce GTX 750.
*   [Кроме](https://en.wikipedia.org/wiki/ru:PureVideo "wikipedia:ru:PureVideo") GeForce 8800 Ultra, 8800 GTX, 8800 GTS (320/640 MB).
*   Кроме GeForce GTX 970 и GTX 980.
*   Реализация NVIDIA ограничена 8-битными потоками [[8]](https://devtalk.nvidia.com/default/topic/940228/vdpau-expose-hevc-main10-support-where-available-on-die/) [[9]](https://us.download.nvidia.com/XFree86/Linux-x86_64/410.57/README/vdpausupport.html#vdpau-implementation-limits).

### Драйвер NVIDIA

| Кодек | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) [[10]](https://developer.nvidia.com/nvidia-video-codec-sdk) |
| NVDECODE | NVENCODE |
| MPEG-2 | Fermi и новее | Нет |
| VC-1 |
| H.264/MPEG-4 AVC | Kepler и новее |
| H.265/HEVC 8bit | Maxwell (GM206) и новее | Maxwell (2nd Gen) и новее |
| H.265/HEVC 10bit | Pascal и новее |
| VP8 | Maxwell (2nd Gen) и новее | Нет |
| VP9 8bit | Maxwell (GM206) и новее |
| VP9 10bit | Pascal и новее |

*   Кроме GM108 (не поддерживается)
*   Кроме GM108 и GP108 (не поддерживаются)

### Поддержка приложениями

**Совет:** Каждый новый [кодек](/index.php/Codecs_and_containers_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Codecs and containers (Русский)") имеет тенденцию к использованию всё большего количества времени CPU ([x264](https://en.wikipedia.org/wiki/ru:x264 "wikipedia:ru:x264") < [VP9](https://en.wikipedia.org/wiki/ru:VP9 "wikipedia:ru:VP9") < [AV1](https://en.wikipedia.org/wiki/ru:AV1 "wikipedia:ru:AV1")), что приводит к большему тепловыделению и энергопотреблению, если аппаратное ускорение недоступно. В связи с этим иногда выгоднее использовать более старый кодек (например, x264), чтобы уменьшить нагрузку на CPU ценой пропускной способности сети. Например, можно использовать расширение *h264ify* для YouTube ([Firefox](https://addons.mozilla.org/ru/firefox/addon/h264ify/), [Chromium](https://chrome.google.com/webstore/detail/h264ify/aleakchihdccplidncghkekgioiakgal)) или *enhanced-h264ify* ([Firefox](https://addons.mozilla.org/ru/firefox/addon/enhanced-h264ify/), [Chromium](https://chrome.google.com/webstore/detail/enhanced-h264ify/omkfmpieigblcllmkgbflkikinpkodlk)).

| Приложение | Декодирование | Кодирование | Документация |
| VA-API | VDPAU | NVDECODE | VA-API | NVENCODE |
| [FFmpeg](/index.php/FFmpeg "FFmpeg") | Да | Да | Да | Да | Да | [FFmpeg#Hardware video acceleration](/index.php/FFmpeg#Hardware_video_acceleration "FFmpeg") |
| [GStreamer](/index.php/GStreamer "GStreamer") | Да | Да | Да | Да | Да | [GStreamer#Hardware video acceleration](/index.php/GStreamer#Hardware_video_acceleration "GStreamer") |
| [Kodi](/index.php/Kodi "Kodi") | Да | Да | Да | – | – | [Kodi#Hardware video acceleration](/index.php/Kodi#Hardware_video_acceleration "Kodi") |
| [mpv](/index.php/Mpv_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mpv (Русский)") | Да | Да | Да | – | – | [Mpv (Русский)#Аппаратное декодирование](/index.php/Mpv_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Аппаратное_декодирование "Mpv (Русский)") |
| [VLC media player](/index.php/VLC_media_player "VLC media player") | Да | Да | Нет | – | – | [VLC media player#Hardware video acceleration](/index.php/VLC_media_player#Hardware_video_acceleration "VLC media player") |
| [MPlayer](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MPlayer (Русский)") | Да | Да | Нет | – | – | [MPlayer#Hardware video acceleration](/index.php/MPlayer#Hardware_video_acceleration "MPlayer") |
| [Flash](/index.php/Flash "Flash") | Нет | Да | Нет | – | – | [Browser plugins#Adobe Flash Player](/index.php/Browser_plugins#Adobe_Flash_Player "Browser plugins") |
| [Chromium](/index.php/Chromium_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Chromium (Русский)") | Да | Нет | Нет | – | – | [Chromium#Hardware video acceleration](/index.php/Chromium#Hardware_video_acceleration "Chromium") |
| [Firefox](/index.php/Firefox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Firefox (Русский)") | Нет | Нет | Нет | – | – | [Отчёт об ошибке](https://bugzilla.mozilla.org/show_bug.cgi?id=1210726), [Отчёт об ошибке (Wayland)](https://bugzilla.mozilla.org/show_bug.cgi?id=1610199) |

*   GStreamer [использует белый список](https://blogs.igalia.com/vjaquez/2018/03/28/gstreamer-va-api-troubleshooting/) драйверов VA-API. Чтобы использовать другие драйверы (например, [intel-media-driver](https://www.archlinux.org/packages/?name=intel-media-driver)), задайте [переменную окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `GST_VAAPI_ALL_DRIVERS=1`.
*   NVDECODE/NVENCODE [отключён в пакете Arch](https://git.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/gst-plugins-bad#n45).
*   Не поддерживается официально, но доступны альтернативные пакеты.
*   VDPAU поддерживается только NPAPI-плагином. Доступен экспериментальный адаптер в виде PPAPI-плагина для NPAPI-браузеров, который частично поддерживает ускорение VA-API и VDPAU.