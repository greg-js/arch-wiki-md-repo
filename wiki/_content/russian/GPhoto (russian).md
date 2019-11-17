**Состояние перевода:** На этой странице представлен перевод статьи [gPhoto](/index.php/GPhoto "GPhoto"). Дата последней синхронизации: 10 ноября 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=GPhoto&diff=0&oldid=588471).

[Libgphoto2](http://www.gphoto.org/proj/libgphoto2/) — основная библиотека, созданная для предоставления доступа к цифровым камерам с помощью внешних программ (фронтендов), например, digiKam и gPhoto2\. Список официально поддерживающихся камер доступен на [официальном сайте](http://www.gphoto.org/proj/libgphoto2/support.php) (другие камеры также могут быть совместимы).

Эта статья описывает настройку `libgphoto2` для получения доступа к цифровым камерам. Также обратите внимание, что некоторые камеры монтируются как обычные [USB-накопители](/index.php/USB-%D0%BD%D0%B0%D0%BA%D0%BE%D0%BF%D0%B8%D1%82%D0%B5%D0%BB%D0%B8 "USB-накопители") и не требуют libgphoto2.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
    *   [1.1 Фронтенды libgphoto2](#Фронтенды_libgphoto2)
*   [2 Использование gPhoto2](#Использование_gPhoto2)
    *   [2.1 Пример использования с GVfs](#Пример_использования_с_GVfs)
*   [3 Проблемы с правами доступа](#Проблемы_с_правами_доступа)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [libgphoto2](https://www.archlinux.org/packages/?name=libgphoto2), а также [gphoto2](https://www.archlinux.org/packages/?name=gphoto2), если необходим интерфейс командной строки.

### Фронтенды libgphoto2

*   **[Darktable](https://en.wikipedia.org/wiki/ru:Darktable "wikipedia:ru:Darktable")** — утилита для организации и работы с RAW-изображениями.

	[https://darktable.org/](https://darktable.org/) || [darktable](https://www.archlinux.org/packages/?name=darktable)

*   **[digiKam](/index.php/Digikam "Digikam")** — организация цифровых фото для [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)").

	[https://www.digikam.org/](https://www.digikam.org/) || [digikam](https://www.archlinux.org/packages/?name=digikam)

*   **Entangle** — предоставляет графический интерфейс для съёмки с подключённым компьютером и полным управлением камеры с него.

	[https://entangle-photo.org/](https://entangle-photo.org/) || [entangle](https://aur.archlinux.org/packages/entangle/)

*   **gphotofs** — [FUSE](/index.php/FUSE "FUSE")-модуль для монтирования камеры в качестве файловой системы.

	[http://www.gphoto.org/proj/gphotofs/](http://www.gphoto.org/proj/gphotofs/) || [gphotofs](https://aur.archlinux.org/packages/gphotofs/)

*   **[gThumb](https://en.wikipedia.org/wiki/GThumb "wikipedia:GThumb")** — просмотрщик изображений для [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)").

	[https://wiki.gnome.org/action/show/Apps/Gthumb](https://wiki.gnome.org/action/show/Apps/Gthumb) || [gthumb](https://www.archlinux.org/packages/?name=gthumb)

*   **GTKam** — фронтенд gPhoto2 на [GTK](/index.php/GTK_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK (Русский)") 2.

	[http://www.gphoto.org/proj/gtkam/](http://www.gphoto.org/proj/gtkam/) || [gtkam](https://aur.archlinux.org/packages/gtkam/)

*   **gvfs-gphoto2** — бекенд gPhoto2 для GVfs, позволяющий монтировать камеру в качестве файловой системы из файловых менеджеров, поддерживающих GVfs. Например, [GNOME Files](/index.php/GNOME_Files "GNOME Files"), [Nemo](/index.php/Nemo "Nemo"), [PCManFM](/index.php/PCManFM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PCManFM (Русский)") и [Thunar](/index.php/Thunar_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Thunar (Русский)").

	[https://wiki.gnome.org/Projects/gvfs](https://wiki.gnome.org/Projects/gvfs) || [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2)

*   **Kamera** — интеграция gPhoto2 в [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)").

	[https://github.com/KDE/kamera](https://github.com/KDE/kamera) || [kamera](https://www.archlinux.org/packages/?name=kamera)

*   **Pantheon Photos** — просмотрщик изображений для Pantheon.

	[https://launchpad.net/pantheon-photos](https://launchpad.net/pantheon-photos) || [pantheon-photos](https://www.archlinux.org/packages/?name=pantheon-photos)

*   **Rapid Photo Downloader** — загрузка фото и видео с камер, карт памяти и переносных запоминающих устройств.

	[https://www.damonlynch.net/rapid/](https://www.damonlynch.net/rapid/) || [rapid-photo-downloader](https://www.archlinux.org/packages/?name=rapid-photo-downloader)

*   **[Rawstudio](https://en.wikipedia.org/wiki/ru:Rawstudio "wikipedia:ru:Rawstudio")** — свободный конвертер RAW-изображений, написанный на GTK. Поддерживает съёмку с подключённым компьютером с помощью gPhoto2.

	[https://rawstudio.org/](https://rawstudio.org/) || [rawstudio](https://aur.archlinux.org/packages/rawstudio/)

*   **[Shotwell](https://en.wikipedia.org/wiki/ru:Shotwell "wikipedia:ru:Shotwell")** — организатор цифровых фото для [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)").

	[https://wiki.gnome.org/Apps/Shotwell](https://wiki.gnome.org/Apps/Shotwell) || [shotwell](https://www.archlinux.org/packages/?name=shotwell)

## Использование gPhoto2

GPhoto2 — клиент командной строки для libgphoto2\. GPhoto2 предоставляет доступ к библиотеке libgphoto2 через терминал или из shell-скрипта для выполнения доступных операций с камерой. Это основной пользовательский интерфейс.

GPhoto2 также предоставляет удобную отладку для разработчиков драйверов камер.

**Быстрые команды**

*   `gphoto2 --list-ports`
*   `gphoto2 --auto-detect`
*   `gphoto2 --summary`
*   `gphoto2 --list-files`
*   `gphoto2 --get-all-files`
*   `gphoto2 --set-config datetime=now` — задаёт камере текущее время

Для получения более подробной информации о работе с файлами, см.

*   `gphoto2 --shell`

### Пример использования с GVfs

Автоматическое обнаружение подключённой камеры и вывод необходимого порта:

```
$ gphoto2 --auto-detect
Model                          Port                                            
----------------------------------------------------------
Canon Digital IXUS 980 IS      usb:006,011 

```

Теперь откройте файловый менеджер и введите адрес с указанным выше портом — "gphoto2://[usb:006,011]" — камера автоматически смонтируется GVfs и станет доступна в файловом менеджере.

## Проблемы с правами доступа

Пользователям с локальной сессией разрешения на доступ к камерам выдаются с помощью [ACL](https://en.wikipedia.org/wiki/ru:ACL "wikipedia:ru:ACL"). См. раздел [Устранение часто встречающихся неполадок#Разрешения сессии](/index.php/%D0%A3%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D1%87%D0%B0%D1%81%D1%82%D0%BE_%D0%B2%D1%81%D1%82%D1%80%D0%B5%D1%87%D0%B0%D1%8E%D1%89%D0%B8%D1%85%D1%81%D1%8F_%D0%BD%D0%B5%D0%BF%D0%BE%D0%BB%D0%B0%D0%B4%D0%BE%D0%BA#Разрешения_сессии "Устранение часто встречающихся неполадок"), если это не работает.