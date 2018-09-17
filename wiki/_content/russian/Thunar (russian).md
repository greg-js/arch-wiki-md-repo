**Состояние перевода:** На этой странице представлен перевод статьи [Thunar](/index.php/Thunar "Thunar"). Дата последней синхронизации: 4 мая 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Thunar&diff=0&oldid=520240).

Related articles

*   [Xfce (Русский)](/index.php/Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xfce (Русский)")
*   [Функциональность файлового менеджера](/index.php/%D0%A4%D1%83%D0%BD%D0%BA%D1%86%D0%B8%D0%BE%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D1%8C_%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D0%BE%D0%B3%D0%BE_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80%D0%B0 "Функциональность файлового менеджера")
*   [GNOME Files](/index.php/GNOME_Files "GNOME Files")
*   [PCManFM (Русский)](/index.php/PCManFM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PCManFM (Русский)")
*   [Nemo](/index.php/Nemo "Nemo")

С [домашней страницы](https://docs.xfce.org/xfce/thunar/start) проекта:

	Thunar - это современный файловый менеджер, разработанный для окружения рабочего стола Xfce. Он был спроектирован с нуля, чтобы быть быстрым и простым в использовании. Его пользовательский интерфейс чист и интуитивен, и по умолчанию он не содержит какие-либо запутывающие или бесполезные параметры. Thunar - быстрый и отзывчивый файловый менеджер с хорошей скоростью запуска и открывания каталогов.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Плагины и дополнения](#.D0.9F.D0.BB.D0.B0.D0.B3.D0.B8.D0.BD.D1.8B_.D0.B8_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F)
*   [2 Thunar Volume Manager](#Thunar_Volume_Manager)
    *   [2.1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_2)
    *   [2.2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [3 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.1 Автомонтирование больших внешних накопителей](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B1.D0.BE.D0.BB.D1.8C.D1.88.D0.B8.D1.85_.D0.B2.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D1.85_.D0.BD.D0.B0.D0.BA.D0.BE.D0.BF.D0.B8.D1.82.D0.B5.D0.BB.D0.B5.D0.B9)
    *   [3.2 Использование Thunar для просмотра удаленных мест](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_Thunar_.D0.B4.D0.BB.D1.8F_.D0.BF.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80.D0.B0_.D1.83.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BC.D0.B5.D1.81.D1.82)
    *   [3.3 Запуск в режиме демона](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B2_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5_.D0.B4.D0.B5.D0.BC.D0.BE.D0.BD.D0.B0)
    *   [3.4 Исправление отображения русских букв](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D1.80.D1.83.D1.81.D1.81.D0.BA.D0.B8.D1.85_.D0.B1.D1.83.D0.BA.D0.B2)
    *   [3.5 Решение проблемы с медленным первым запуском](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.BC.D0.B5.D0.B4.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D0.BC_.D0.BF.D0.B5.D1.80.D0.B2.D1.8B.D0.BC_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.BE.D0.BC)
    *   [3.6 Скрытие закладок в боковой панели](#.D0.A1.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D0.B7.D0.B0.D0.BA.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA_.D0.B2_.D0.B1.D0.BE.D0.BA.D0.BE.D0.B2.D0.BE.D0.B9_.D0.BF.D0.B0.D0.BD.D0.B5.D0.BB.D0.B8)
    *   [3.7 Создание горячих клавиш в Thunar](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B3.D0.BE.D1.80.D1.8F.D1.87.D0.B8.D1.85_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88_.D0.B2_Thunar)
    *   [3.8 Отображение разделов, определенных в fstab](#.D0.9E.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2.2C_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.B2_fstab)
*   [4 Особые действия](#.D0.9E.D1.81.D0.BE.D0.B1.D1.8B.D0.B5_.D0.B4.D0.B5.D0.B9.D1.81.D1.82.D0.B2.D0.B8.D1.8F)
    *   [4.1 Поиск файлов и папок](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D0.B8_.D0.BF.D0.B0.D0.BF.D0.BE.D0.BA)
    *   [4.2 Поиск вирусов](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA_.D0.B2.D0.B8.D1.80.D1.83.D1.81.D0.BE.D0.B2)
    *   [4.3 Ссылка на Dropbox](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B0_.D0.BD.D0.B0_Dropbox)
*   [5 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.1 Tumblerd зависает, сильно нагружает ЦП](#Tumblerd_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.B5.D1.82.2C_.D1.81.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE_.D0.BD.D0.B0.D0.B3.D1.80.D1.83.D0.B6.D0.B0.D0.B5.D1.82_.D0.A6.D0.9F)
    *   [5.2 Исчезают иконки корзины/сети](#.D0.98.D1.81.D1.87.D0.B5.D0.B7.D0.B0.D1.8E.D1.82_.D0.B8.D0.BA.D0.BE.D0.BD.D0.BA.D0.B8_.D0.BA.D0.BE.D1.80.D0.B7.D0.B8.D0.BD.D1.8B.2F.D1.81.D0.B5.D1.82.D0.B8)
    *   [5.3 Не авторизирован для монтирования файловых систем](#.D0.9D.D0.B5_.D0.B0.D0.B2.D1.82.D0.BE.D1.80.D0.B8.D0.B7.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD_.D0.B4.D0.BB.D1.8F_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D1.8B.D1.85_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [thunar](https://www.archlinux.org/packages/?name=thunar). Он является частью группы [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/), поэтому если вы используете [Xfce](/index.php/Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xfce (Русский)"), то скорее всего Thunar у вас уже есть.

### Плагины и дополнения

*   **Gnome Virtual File System** — Для поддержки корзины, монтирования съемных носителей и удаленных файловых систем (`mtp`/`smb`). Для получения дополнительной информации смотрите [Функциональность файлового менеджера#Монтирование](/index.php/%D0%A4%D1%83%D0%BD%D0%BA%D1%86%D0%B8%D0%BE%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D1%8C_%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D0%BE%D0%B3%D0%BE_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80%D0%B0#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5 "Функциональность файлового менеджера").

	[https://wiki.gnome.org/Projects/gvfs](https://wiki.gnome.org/Projects/gvfs) || [gvfs](https://www.archlinux.org/packages/?name=gvfs)

*   **Thunar Archive Plugin** — Плагин, который позволяет создавать и распаковывать архивы через контекстное меню. Он не создает и не распаковывает напрямую архивы, вместо этого он действует как интерфейс для других программ, таких как File Roller ([file-roller](https://www.archlinux.org/packages/?name=file-roller)), Ark ([ark](https://www.archlinux.org/packages/?name=ark)) или Xarchiver ([xarchiver](https://www.archlinux.org/packages/?name=xarchiver)). Является частью группы [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/).

	[https://goodies.xfce.org/projects/thunar-plugins/thunar-archive-plugin](https://goodies.xfce.org/projects/thunar-plugins/thunar-archive-plugin) || [thunar-archive-plugin](https://www.archlinux.org/packages/?name=thunar-archive-plugin)

*   **Thunar Media Tags Plugin** — Плагин, который позволяет просматривать подробную информацию о медиафайлах. Кроме того, в него включена функция массового переименования файлов и редактирования тегов мультимедиа. Поддерживает тэги ID3 (система формата MP3-файла) и Ogg/Vorbis. Является частью группы [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/).

	[https://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin](https://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin) || [thunar-media-tags-plugin](https://www.archlinux.org/packages/?name=thunar-media-tags-plugin)

*   **Thunar Shares Plugin** — Плагин, который позволяет быстро открыть общий доступ к папке из Thunar, используя Samba. Не требует права суперпользователя. Также смотрите [как настроить направления](/index.php/Samba#Enable_usershares "Samba").

	[https://goodies.xfce.org/projects/thunar-plugins/thunar-shares-plugin](https://goodies.xfce.org/projects/thunar-plugins/thunar-shares-plugin) || [thunar-shares-plugin](https://aur.archlinux.org/packages/thunar-shares-plugin/)

*   **[Thunar Volume Manager](#Thunar_Volume_Manager)** — Автоматическое управление съемными устройствами в Thunar. Является частью группы [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/).

	[https://goodies.xfce.org/projects/thunar-plugins/thunar-volman](https://goodies.xfce.org/projects/thunar-plugins/thunar-volman) || [thunar-volman](https://www.archlinux.org/packages/?name=thunar-volman)

*   **Tumbler** — Дополнительная программа для создания эскизов. Также установите [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer), чтобы включить поддержку эскизов для видеофайлов.

	[https://git.xfce.org/xfce/tumbler/tree/README](https://git.xfce.org/xfce/tumbler/tree/README) || [tumbler](https://www.archlinux.org/packages/?name=tumbler)

*   **RAW Thumbnailer** — Легкий и быстрый просмотрщик изображений raw, который необходим для отображения эскизов raw.

	[https://code.google.com/p/raw-thumbnailer/](https://code.google.com/p/raw-thumbnailer/) || [raw-thumbnailer](https://www.archlinux.org/packages/?name=raw-thumbnailer)

*   **libgsf** — GNOME Structured File Library - это библиотека для чтения и записи структурированных форматов файлов. Установите, если вам нужна поддержка эскизов odf

	[https://directory.fsf.org/wiki/Libgsf](https://directory.fsf.org/wiki/Libgsf) || [libgsf](https://www.archlinux.org/packages/?name=libgsf)

## Thunar Volume Manager

Хотя Thunar и поддерживает автоматическое монтирование и размонтирование съемных носителей (требуется пакет [gvfs](https://www.archlinux.org/packages/?name=gvfs)), Thunar Volume Manager обеспечивает дополнительные возможности, такие как автозапуск команд или открытие окна Thunar для подмонтированного устройства.

### Установка

Thunar Volume Manager можно установить из официальных репозиториев пакетом [thunar-volman](https://www.archlinux.org/packages/?name=thunar-volman).

**Совет:** Чтобы Thunar мог автоматически монтировать вставленные устройства, нужно запустить его в режиме демона. [#Запуск в режиме демона](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B2_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5_.D0.B4.D0.B5.D0.BC.D0.BE.D0.BD.D0.B0)

### Настройка

Thunar Volume Manager можно настроить на выполнение определённых действий, например когда подключена фотокамера или аудиоплеер. После установки плагина выполните:

1.  Запустите Thunar и перейдите к *Правка > Параметры*
2.  Во вкладке 'Дополнительно', отметьте флажком 'Включить управление томами'
3.  Щёлкните 'Настроить' и проверьте следующие пункты:
    *   Подключать обнаруженные съемные устройства
    *   Подключать вставленные съемные носители
4.  Также сделайте необходимые изменения (смотрите пример ниже)

Вот пример настройки - запуска Amarok для проигрывания аудио с вставленного диска.

```
 Мультимедиа - Аудиодиски: `amarok --cdplay %d`

```

## Советы и рекомендации

### Автомонтирование больших внешних накопителей

Если Thunar отказывается монтировать большие съемные носители (размером > 1 ТБ), хотя были установлены thunar-volman и gvfs, попробуйте установить другую программу, например, [udevil](https://www.archlinux.org/packages/?name=udevil) или [udiskie](https://www.archlinux.org/packages/?name=udiskie). Рекомендуется использовать последнее, поскольку оно использует udisks2 и, следовательно, совместимо с gvfs. Чтобы запустить udiskie с поддержкой udisks2, добавьте следующую строку в файл автозапуска:

```
udiskie -2 &

```

### Использование Thunar для просмотра удаленных мест

Начиная с Xfce 4.8 (Thunar 1.2), вы можете просматривать удаленные местоположения (например, FTP-серверы или общие папки Samba) непосредственно в Thunar. Чтобы включить эту функциональность, убедитесь, что установлены пакеты [gvfs](https://www.archlinux.org/packages/?name=gvfs), [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) и [sshfs](https://www.archlinux.org/packages/?name=sshfs). В боковой панели Thunar видна закладка 'Сеть', и удаленные местоположения можно открыть там, используя следующие схемы URI в панели для отображения текущего файлового пути (выбранной с помощью `Ctrl+l`): smb://, ftp://, ssh://, sftp://, davs:// и за которыми следует имя хоста сервера или IP-адрес.

Для общего доступа через [NFS](/index.php/NFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NFS (Русский)") нет схемы URI, но Thunar может выдать команду `mount`, если вы правильно настроили [fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)").

 `/etc/fstab` 
```
# nas1 server
nas1:/c/home		/media/nas1/home	nfs	noauto,user,_netdev,bg  0 0
```

Здесь важны параметры: `noauto`, который запрещает монтировать до тех пор, пока вы не нажмете на нее, `user`, который позволяет любому пользователю монтировать (и отключать) общий доступ, `_netdev`, который устанавливает подключение к сети необходимым условием, и, наконец, `bg`, который устанавливает операцию монтирования в фоне, поэтому, если вашему серверу требуется некоторое время отклика, вам не придется иметь дело с сообщениями тайм-аута и повторно нажимать, пока это не сработает.

**Совет:** Если вы хотите постоянно хранить пароли от удаленных файловых систем, вам необходимо установить [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring").

### Запуск в режиме демона

Thunar может запускаться в режиме демона. Это даёт несколько преимуществ, включая более быстрый запуск Thunar и его выполнение в фоне. При работе в фоне Thunar может автоматически монтировать съемные носители и при их подсоединение вызывать необходимые действия (например, при подсоединение флешки откроется Thunar с ее содержимым).

Убедитесь, что команда `thunar --daemon` запускается при входе в систему. Для получения дополнительной информации смотрите [Xfce](/index.php/Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xfce (Русский)") и [Автозапуск](/index.php/%D0%90%D0%B2%D1%82%D0%BE%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA "Автозапуск").

### Исправление отображения русских букв

В общесистемном `/etc/xdg/xfce4/mount.rc` или в пользовательском файле `~/.config/xfce4/mount.rc` добавьте *utf8=true* в секции файловых систем, с которыми имеет место проблема. Например:

```
[vfat]
uid=<auto>
shortname=winnt
utf8=true
# FreeBSD specific option
longnames=true

```

В этом файле определены правила для нескольких файловых систем:

*   **vfat** - FAT, флешки
*   **iso9660** - CDFS, компакт-диски CD
*   **udf** - UDF, обычно DVD
*   **ntfs** - собственно, NTFS
*   **ntfs-3g** - свободная реализация NTFS

### Решение проблемы с медленным первым запуском

У некоторых людей по-прежнему возникают проблемы с тем, что Thunar долго запускается в первый раз. Это связано с тем, что gvfs проверяет сеть, предотвращая запуск Thunar до завершения этой проверки. Чтобы изменить это поведение, отредактируйте `/usr/share/gvfs/mounts/network.mount` и замените **AutoMount=true** на **AutoMount=false**.

### Скрытие закладок в боковой панели

Существует меню для скрытия закладок в боковой панели.

Щелкните правой кнопкой мыши в боковой панели, где нет закладок, например, по надписи Устройства. Затем вы увидете появляющее меню, в котором вы можете снять флажки с элементов, которые вы не хотите отображать.

### Создание горячих клавиш в Thunar

Для получения дополнительной информации смотрите [GTK+ (Русский)#Горячие клавиши](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.93.D0.BE.D1.80.D1.8F.D1.87.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8 "GTK+ (Русский)"),

### Отображение разделов, определенных в fstab

По умолчанию Thunar не будет показывать в устройствах какие-либо разделы, определенные в `/etc/fstab`, кроме корневого раздела.

Мы можем изменить это, добавив параметр **x-gvfs-show** в fstab для раздела, который мы хотим видеть.

## Особые действия

В этом разделе рассматриваются полезные особые действия, которые можно настроить через `Правка -> Особые действия`. Их настройки хранятся в `~/.config/Thunar/uca.xml`. Дополнительные примеры перечислены в [вики thunar](https://docs.xfce.org/xfce/thunar/custom-actions). Кроме того, на этих сайтах [[1]](https://duncanlock.net/blog/2013/06/28/useful-thunar-custom-actions/)[[2]](https://xubuntu-ru.net/how-to/699-osobyie-deystviya-v-thunar.html)[[3]](http://pingvinus.ru/forum/discussion/338/stop-thunar.-osobye-deystviya./p1) представлены неплохие подборки особых действий.

### Поиск файлов и папок

Для использования этого действия необходим установленный [catfish](https://www.archlinux.org/packages/?name=catfish). Необходимо также установить необязательную зависимость [mlocate](https://www.archlinux.org/packages/?name=mlocate) для него.

| Имя | Команда | Шаблон имени файла | Появляться, если выделение содержит |
| Поиск | `catfish --path=%f` | * | Каталоги |

### Поиск вирусов

Для использования этого действия необходимы установленные пакеты [clamav](https://www.archlinux.org/packages/?name=clamav) и [clamtk](https://www.archlinux.org/packages/?name=clamtk).

| Имя | Команда | Шаблон имени файла | Появляться, если выделение содержит |
| Поиск вирусов | `clamtk %F` | * | Выберите все |

### Ссылка на Dropbox

| Имя | Команда | Шаблон имени файла | Появляться, если выделение содержит |
| Ссылка на Dropbox | `ln -s %f /путь/до/папки_Dropbox` | * | Каталоги, другие файлы |

Обратите внимание, что при использовании большого количества особых действий для создания ссылок на файлы и папки в определенные места может быть удобнее поместить их в контекстного меню `Отправить на`, чтобы избежать раздувания главного меню. Это довольно легко сделать - для каждого действия требуется файл .desktop в каталоге `~/.local/share/Thunar/sendto`. Предположим, что мы хотим поместить вышеуказанное действие создания ссылки на Dropbox в Отправить на, мы создаем `dropbox_folder.desktop` со следующим содержимым. Новое действие будет включено после перезапуска Thunar.

```
[Desktop Entry]
Type=Application
Version=1.0
Encoding=UTF-8
Exec=ln -s %f /путь/до/папки_Dropbox
Icon=/usr/share/icons/dropbox.png
Name=Dropbox

```

## Решение проблем

### Tumblerd зависает, сильно нагружает ЦП

Tumblerd - служба, следящая за файловой системой и уведомляющая систему, когда нужно сделать эскиз. Она может застрять в цикле, нагружая при этом на 100% ЦП системы, для получения дополнительной информации смотрите [сообщение об ошибке](https://bugzilla.xfce.org/show_bug.cgi?id=7384). Следующий скрипт является временным обходным решением, чтобы этого не происходило. Скопируйте и вставьте его в файл *.sh*, сохраните его где-нибудь в своем домашнем каталоге, отметьте файл как исполняемый, а затем включите его в автозапуск.

```
#!/bin/bash
period=20
tumblerpath="/usr/lib/*/tumbler-1/tumblerd" # * здесь используется для правильного выбора, будь то 32 и 64-битный
cpu_threshold=50
mem_threshold=20
max_strikes=2                               # максимальное количество вышеперечисленных cpu/mem-threshold в строке
log="/tmp/tumblerd-watcher.log"

if [[ -n "${log}" ]]; then
    cat /dev/null > "${log}"
    exec >"${log}" 2>&1
fi

strikes=0
while sleep "${period}"; do
    while read pid; do
	cpu_usage=$(ps --no-headers -o pcpu -f "${pid}"|cut -f1 -d.)
	mem_usage=$(ps --no-headers -o pmem -f "${pid}"|cut -f1 -d.)

	if [[ $cpu_usage -gt $cpu_threshold ]] || [[ $mem_usage -gt $mem_threshold ]]; then
	    echo "$(date +"%F %T") PID: $pid CPU: $cpu_usage/$cpu_threshold %cpu MEM: $mem_usage/$mem_threshold STRIKES: ${strikes} NPROCS: $(pgrep -c -f ${tumblerpath})"
	    (( strikes++ ))
	    if [[ ${strikes} -ge ${max_strikes} ]]; then
		kill "${pid}"
		echo "$(date +"%F %T") PID: $pid KILLED; NPROCS: $(pgrep -c -f ${tumblerpath})"
		strikes=0
	    fi
	else
	    strikes=0
	fi
    done < <(pgrep -f ${tumblerpath})
done

```

### Исчезают иконки корзины/сети

Убедитесь что, все экземпляры Thunar запускаются **после** *gvfs*. [[4]](https://bugs.launchpad.net/ubuntu/+source/thunar/+bug/1057610) Для `thunar --daemon` вы можете создать скрипт, который ждет, пока включится GVFS:

**Примечание:** Путь `/usr/local/bin` должен предшествовать `/usr/bin` в переменной `$PATH`.
 `/usr/local/bin/Thunar` 
```
#!/bin/bash
if [[ $1 == --daemon ]]; then
  until pgrep gvfs >/dev/null; do
    sleep 1
  done
  exec /usr/bin/Thunar "$@"
else
  exec /usr/bin/Thunar "$@"
fi

```

### Не авторизирован для монтирования файловых систем

Для получения дополнительной информации смотрите [Функциональность файлового менеджера#Решение проблем](/index.php/%D0%A4%D1%83%D0%BD%D0%BA%D1%86%D0%B8%D0%BE%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D1%8C_%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D0%BE%D0%B3%D0%BE_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80%D0%B0#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC "Функциональность файлового менеджера").

## Смотрите также

*   Страницу проекта [Thunar](https://docs.xfce.org/xfce/thunar/start)
*   Страницу проекта [Thunar Volume Manager](https://goodies.xfce.org/projects/thunar-plugins/thunar-volman)
*   Этот [список](https://goodies.xfce.org/projects/thunar-plugins/start) плагинов