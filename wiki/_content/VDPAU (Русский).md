# VDPAU (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Ссылки по теме

*   [VA-API (Русский)](/index.php/VA-API_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "VA-API (Русский)")
*   [XvMC](/index.php/XvMC "XvMC")

**Состояние перевода:** На этой странице представлен перевод статьи [VDPAU](/index.php/VDPAU "VDPAU"). Дата последней синхронизации: 12 декабря 2015‎‎. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=VDPAU&diff=0&oldid=411185).

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

**[Video Decode and Presentation API for Unix](http://http.download.nvidia.com/XFree86/vdpau/doxygen/html/)** — открытая библиотека и API для выполнения задач декодирования и постобработки видео на аппаратных ускорителях.

## Contents

*   [1 Поддерживаемые видеокарты](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE.D0.BA.D0.B0.D1.80.D1.82.D1.8B)
    *   [1.1 Поддерживаемые форматы](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.82.D1.8B)
    *   [1.2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
        *   [1.2.1 Гибридная графика](#.D0.93.D0.B8.D0.B1.D1.80.D0.B8.D0.B4.D0.BD.D0.B0.D1.8F_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D0.BA.D0.B0)
*   [2 Поддерживаемое программное обеспечение](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D0.BE.D0.B5_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D0.BD.D0.BE.D0.B5_.D0.BE.D0.B1.D0.B5.D1.81.D0.BF.D0.B5.D1.87.D0.B5.D0.BD.D0.B8.D0.B5)

## Поддерживаемые видеокарты

**Свободные драйверы:**

*   [AMD](/index.php/ATI "ATI") Radeon 9500 и новее поддерживаются пакетом [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau).
*   [Intel](/index.php/Intel_graphics "Intel graphics") GMA 4500 серии и новее поддерживаются пакетом [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) вместе с [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver).
*   [NVIDIA](/index.php/Nouveau "Nouveau") GeForce 8 серии и новее поддерживаются пакетом [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau). Он [требует](http://nouveau.freedesktop.org/wiki/VideoAcceleration/#firmware) пакет [nouveau-fw](https://aur.archlinux.org/packages/nouveau-fw/)<sup><small>AUR</small></sup>, который содержит в себе необходимые прошивки для работы, взятые из закрытого драйвера NVIDIA.

**Проприетарные драйверы:**

*   [AMD](/index.php/AMD_Catalyst "AMD Catalyst") Radeon HD 4000 серии и новее поддерживаются пакетом [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl), вместе с пакетом [libva-xvba-driver](https://aur.archlinux.org/packages/libva-xvba-driver/)<sup><small>AUR</small></sup>. Он использует драйвер [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/)<sup><small>AUR</small></sup> для Radeon HD 5000 серии и новее, и [catalyst-total-hd234k](https://aur.archlinux.org/packages/catalyst-total-hd234k/)<sup><small>AUR</small></sup> для Radeon HD 4000 серии.

*   [NVIDIA](/index.php/NVIDIA "NVIDIA") GeForce 400 серии и новее поддерживаются пакетом [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils).
    *   GeForce 8/9 и GeForce 100-300 серии и новее поддерживаются пакетом [nvidia-340xx-utils](https://www.archlinux.org/packages/?name=nvidia-340xx-utils).

### Поддерживаемые форматы

<table class="wikitable" style="width: 100%">

<tbody>

<tr>

<th colspan="3">Открытые</th>

<th colspan="2">Проприетарные</th>

</tr>

<tr>

<th>AMD</th>

<th>Intel</th>

<th>Nvidia</th>

<th>AMD</th>

<th>Nvidia</th>

</tr>

<tr>

<td>Декодирование MPEG2</td>

<td>Radeon 9500 и новее</td>

<td>

<center>— <sup>2</sup></center>

</td>

<td>GeForce 8 и новее</td>

<td>

<center>— <sup>2</sup></center>

</td>

<td>GeForce 8 и новее</td>

</tr>

<tr>

<td>Декодирование MPEG4</td>

<td>Radeon HD 6000 и новее</td>

<td>

<center>—</center>

</td>

<td>GeForce 200 и новее</td>

<td>

<center>— <sup>2</sup></center>

</td>

<td>GeForce 200 и новее</td>

</tr>

<tr>

<td>Декодирование H.264</td>

<td>Radeon HD 4000 и новее</td>

<td>GMA 4500<sup>1</sup>, Ironlake Graphics и новее</td>

<td>GeForce 8 и новее</td>

<td>Radeon HD 4000 и новее</td>

<td>GeForce 8 и новее</td>

</tr>

<tr>

<td>H.265 decoding</td>

<td>

<center>—</center>

</td>

<td>

<center>—</center>

</td>

<td>

<center>—</center>

</td>

<td>

<center>—</center>

</td>

<td>[upcoming:](http://www.phoronix.com/scan.php?page=news_item&px=VDPAU-H.265-HEVC-Decode) GeForce 900<sup>4</sup> и новее</td>

</tr>

<tr>

<td>Декодирование VC1</td>

<td>Radeon HD 4000 и новее</td>

<td>

<center>— <sup>2</sup></center>

</td>

<td>GeForce 8<sup>3</sup> и новее</td>

<td>

<center>— <sup>2</sup></center>

</td>

<td>GeForce 8<sup>3</sup> и новее</td>

</tr>

</tbody>

</table>

*   <sup>1</sup> Поддерживается пакетом [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/)<sup><small>AUR</small></sup>. Инструкция и важная информация доступна на странице [Intel graphics#H.264 decoding on GMA 4500](/index.php/Intel_graphics#H.264_decoding_on_GMA_4500 "Intel graphics").
*   <sup>2</sup> Драйвер VA GL не поддерживает другие аппаратные декодеры помимо H.264 (на состояние 21 июня 2014 года, ветка master, версия 0.3.x).
*   <sup>3</sup> [За исключением](https://en.wikipedia.org/wiki/Nvidia_PureVideo "wikipedia:Nvidia PureVideo") GeForce 8800 Ultra, 8800 GTX, 8800 GTS (320/640 MB).
*   <sup>4</sup> Except GeForce GTX 970 and GTX 980.

Чтобы проверить, какие возможности поддерживаются вашей видеокартой, воспользуйтесь следующей командой, предоставляемой пакетом [vdpauinfo](https://www.archlinux.org/packages/?name=vdpauinfo):

```
$ vdpauinfo

```

### Настройка

**Note:** Можно не экспортировать переменную `VDPAU_DRIVER`, так как большинство (современных) приложений и сред умеют находить библиотеку VDPAU [автоматически](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0)

В переменной окружения `VDPAU_DRIVER` должен быть указан файл драйвера. Вы можете установить [переменную окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") [глобально](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D0.BE.D0.BC_.D1.83.D1.80.D0.BE.D0.B2.D0.BD.D0.B5 "Environment variables (Русский)") или [для отдельного пользователя](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0_.D1.83.D0.BE.D0.B2.D0.BD.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F "Environment variables (Русский)").

Корректное название драйвера зависит от вашей конфигурации:

*   Для Intel Graphics или AMD Catalyst: `va_gl`.
*   Для свободного драйвера AMD/ATI, необходимо выставить название, включающее в себя корректную версию драйвера, которая зависит от вашей видеокарты.
*   Для проприетарного драйвера Nvidia: `nvidia`

Чтобы определить правильное название драйвера, воспользуйтесь командой

 `$ grep -i vdpau /var/log/Xorg.0.log` 

```
(II) RADEON(0): [DRI2] VDPAU driver: r300

```

В данном примере необходимо установить значение `VDPAU_DRIVER=r300`.

#### Гибридная графика

Для конфигураций с гибридной графикой (NVIDIA и AMD), возможно понадобится установить следующую переменную окружения:

```
$ export DRI_PRIME=1

```

Больше информации доступно на странице [PRIME](/index.php/PRIME "PRIME").

## Поддерживаемое программное обеспечение

*   **Adobe Flash Player** — смотрите раздел [Плагины для браузеров#Adobe Flash Player](/index.php/%D0%9F%D0%BB%D0%B0%D0%B3%D0%B8%D0%BD%D1%8B_%D0%B4%D0%BB%D1%8F_%D0%B1%D1%80%D0%B0%D1%83%D0%B7%D0%B5%D1%80%D0%BE%D0%B2#Adobe_Flash_Player "Плагины для браузеров")

|| [flashplugin](https://www.archlinux.org/packages/?name=flashplugin)

*   **bomi** — аппаратное ускорение можно включить в: _Preferences > Video > Hardware acceleration_

[https://bomi-player.github.io](https://bomi-player.github.io) || [bomi](https://aur.archlinux.org/packages/bomi/)<sup><small>AUR</small></sup> [bomi-git](https://aur.archlinux.org/packages/bomi-git/)<sup><small>AUR</small></sup>

*   **gnome-mplayer** — чтобы включить аппаратное ускорение зайдите в _Edit > Preferences > Player_ и установите параметр `vdpau` в положение _Video Output_

|| [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer)

*   **[MPlayer](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MPlayer (Русский)") или [mplayer2](http://www.mplayer2.org/)** — смотрите раздел [MPlayer (Русский)#Использование vdpau (только для новых видеокарт nVidia)](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_vdpau_.28.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.B4.D0.BB.D1.8F_.D0.BD.D0.BE.D0.B2.D1.8B.D1.85_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE.D0.BA.D0.B0.D1.80.D1.82_nVidia.29 "MPlayer (Русский)")

|| [mplayer](https://www.archlinux.org/packages/?name=mplayer) [mplayer2](https://aur.archlinux.org/packages/mplayer2/)<sup><small>AUR</small></sup>

*   **[mpv](/index.php/Mpv_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mpv (Русский)")** — смотрите раздел [Mpv (Русский)#Аппаратное декодирование](/index.php/Mpv_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.90.D0.BF.D0.BF.D0.B0.D1.80.D0.B0.D1.82.D0.BD.D0.BE.D0.B5_.D0.B4.D0.B5.D0.BA.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5 "Mpv (Русский)")

|| [mpv](https://www.archlinux.org/packages/?name=mpv)

*   **[SMplayer](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC "MPlayer (Русский)")** — чтобы включить аппаратное ускорение зайдите в _Options > Preferences > General > Video_ и установите параметр `vdpau` в положение _Output driver_

|| [smplayer](https://www.archlinux.org/packages/?name=smplayer)

*   **[VLC media player](/index.php/VLC_media_player "VLC media player")** — смотрите раздел [VLC media player#Hardware acceleration support](/index.php/VLC_media_player#Hardware_acceleration_support "VLC media player")

|| [vlc](https://www.archlinux.org/packages/?name=vlc)

Retrieved from "[https://wiki.archlinux.org/index.php?title=VDPAU_(Русский)&oldid=412719](https://wiki.archlinux.org/index.php?title=VDPAU_(Русский)&oldid=412719)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Graphics (Русский)](/index.php/Category:Graphics_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Graphics (Русский)")
*   [X server (Русский)](/index.php/Category:X_server_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:X server (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")