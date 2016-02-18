**Состояние перевода:** На этой странице представлен перевод статьи [GnuPG](/index.php/GnuPG "GnuPG"). Дата последней синхронизации: 12 декабря 2015‎‎. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=GnuPG&diff=0&oldid=411159).

**[Video Acceleration API](http://www.freedesktop.org/wiki/Software/vaapi)** — спецификация и открытая библиотека, созданная с целью предоставить возможность аппаратного кодирования и декодирования видео.

## Contents

*   [1 Поддерживаемые видеокарты](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE.D0.BA.D0.B0.D1.80.D1.82.D1.8B)
    *   [1.1 Поддерживаемые форматы](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.82.D1.8B)
    *   [1.2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [1.3 Проверка](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0)
*   [2 Поддерживаемое программное обеспечение](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D0.BE.D0.B5_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D0.BD.D0.BE.D0.B5_.D0.BE.D0.B1.D0.B5.D1.81.D0.BF.D0.B5.D1.87.D0.B5.D0.BD.D0.B8.D0.B5)

## Поддерживаемые видеокарты

**Свободные драйверы:**

*   [AMD](/index.php/ATI "ATI") Radeon 9500 и новее поддерживаются пакетами [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) и [mesa](https://www.archlinux.org/packages/?name=mesa).
*   [Intel](/index.php/Intel_graphics "Intel graphics") GMA 4500 серии и новее поддерживаются пакетами [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) и [mesa](https://www.archlinux.org/packages/?name=mesa).
*   [NVIDIA](/index.php/Nouveau "Nouveau") GeForce 8 серии и новее поддерживаются пакетами [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) и [mesa](https://www.archlinux.org/packages/?name=mesa),. Он использует пакет [nouveau-fw](https://aur.archlinux.org/packages/nouveau-fw/), содержащий в себе необходимые прошивки для работы, взятые из закрытого драйвера NVIDIA.

**Проприетарные драйверы:**

*   [AMD](/index.php/AMD_Catalyst "AMD Catalyst") Radeon HD 4000 серии и новее поддерживаются пакетами [libva-xvba-driver](https://aur.archlinux.org/packages/libva-xvba-driver/),. Он использует драйвера [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) для Radeon HD 5000 серии и новее, и [catalyst-total-hd234k](https://aur.archlinux.org/packages/catalyst-total-hd234k/) для Radeon HD 4000 серии.
*   [NVIDIA](/index.php/NVIDIA "NVIDIA") GeForce 8 серии и новее поддерживаются пакетами [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) и [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils).

### Поддерживаемые форматы

 Open source | Proprietary |
 AMD | Intel | Nvidia | AMD | Nvidia |
| Декодирование MPEG2 | AMD Radeon 9500 и новее | Intel GMA 4500 и новее | Nvidia GeForce 8 и новее | AMD Radeon HD 4000 и новее | Nvidia GeForce 8 и новее |
| MPEG4 decoding | AMD Radeon HD 6000 и новее | 

<center>—</center>

 | Nvidia GeForce 200 и новее | AMD Radeon HD 6000 и новее | Nvidia GeForce 200 и новее |
| Декодирование H264 | AMD Radeon HD 4000 и новее | Intel GMA 4500, Ironlake Graphics и новее | Nvidia GeForce 8 и новее | AMD Radeon HD 4000 и новее | Nvidia GeForce 8 и новее |
| Декодирование VC1 | AMD Radeon HD 4000 и новее | Intel Sandy Bridge Graphics и новее | Nvidia GeForce 8200, 8300, 8400, 9300, 200 и новее | AMD Radeon HD 4000 и новее | Nvidia GeForce 8 и новее |
| Кодирование в MPEG2 | 

<center>—</center>

 | Intel Ivy Bridge Graphics и новее | 

<center>—</center>

 | 

<center>—</center>

 | 

<center>—</center>

 |
| Кодирование в H264 | 

<center>—</center>

 | Intel Sandy Bridge Graphics и новее | 

<center>—</center>

 | 

<center>—</center>

 | 

<center>—</center>

 |

Поддерживается пакетом [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/). Инструкция и важная информация доступна на странице [Intel graphics#H.264 decoding on GMA 4500](/index.php/Intel_graphics#H.264_decoding_on_GMA_4500 "Intel graphics").

Чтобы проверить, какие профили (возможности) поддерживаются вашей видеокартой, обратитесь к секции [#Проверка](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0)

### Настройка

**Note:** Можно не экспортировать `LIBVA_DRIVER`, так как большинство (современные) приложений и сред умеют находить VAAPI библиотеку [автоматически](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0).

[libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) необходимо включить вручную, используя [переменную окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") [глобально](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D0.BE.D0.BC_.D1.83.D1.80.D0.BE.D0.B2.D0.BD.D0.B5 "Environment variables (Русский)") или [для отдельного пользователя](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0_.D1.83.D1.80.D0.BE.D0.B2.D0.BD.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F "Environment variables (Русский)"):

```
export LIBVA_DRIVER_NAME=vdpau

```

### Проверка

Проверрьте настройки VAAPI выполнив `vainfo`, которое предоставляет пакет [libva](https://www.archlinux.org/packages/?name=libva):

 `$ vainfo` 
```
libva info: VA-API version 0.38.0
libva info: va_getDriverName() returns 0
libva info: User requested driver 'vdpau'
libva info: Trying to open /usr/lib/dri/vdpau_drv_video.so
libva info: Found init function __vaDriverInit_0_35
libva info: va_openDriver() returns 0
vainfo: VA-API version: 0.38 (libva 1.6.1)
vainfo: Driver version: Splitted-Desktop Systems VDPAU backend for VA-API - 0.7.4
vainfo: Supported profile and entrypoints
      VAProfileMPEG2Simple            : VAEntrypointVLD
      VAProfileMPEG2Main              : VAEntrypointVLD
      VAProfileMPEG4Simple            : VAEntrypointVLD
      VAProfileMPEG4AdvancedSimple    : VAEntrypointVLD
      VAProfileH264Baseline           : VAEntrypointVLD
      VAProfileH264Main               : VAEntrypointVLD
      VAProfileH264High               : VAEntrypointVLD
      VAProfileVC1Simple              : VAEntrypointVLD
      VAProfileVC1Main                : VAEntrypointVLD
      VAProfileVC1Advanced            : VAEntrypointVLD
```

Строка *VAEntrypointVLD* означает, что ваша видеокарта поддерживает декодирование данного формата, а *VAEntrypointEncSlice* — что доступно кодирование в этот формат.

## Поддерживаемое программное обеспечение

*   Плееры, основанные на [GStreamer](/index.php/GStreamer "GStreamer"): VA-API используется автоматически, если найден поддерживаемый формат.

	Больше информации доступно по ссылке: [http://docs.gstreamer.com/display/GstSDK/Playback+tutorial+8%3A+Hardware-accelerated+video+decoding](http://docs.gstreamer.com/display/GstSDK/Playback+tutorial+8%3A+Hardware-accelerated+video+decoding).

*   VLC: [VLC media player#Hardware acceleration support](/index.php/VLC_media_player#Hardware_acceleration_support "VLC media player").
*   Mpv: [Mpv (Русский)#Аппаратное декодирование](/index.php/Mpv_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.90.D0.BF.D0.BF.D0.B0.D1.80.D0.B0.D1.82.D0.BD.D0.BE.D0.B5_.D0.B4.D0.B5.D0.BA.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5 "Mpv (Русский)").
*   MPlayer: [MPlayer#Enabling VA-API](/index.php/MPlayer#Enabling_VA-API "MPlayer").