Ссылки по теме

*   [PCManFM (Русский)](/index.php/PCManFM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PCManFM (Русский)")
*   [SpaceFM (Русский)](/index.php/SpaceFM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SpaceFM (Русский)")
*   [Thunar (Русский)](/index.php/Thunar_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Thunar (Русский)")
*   [Оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер")
*   [Среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола")
*   [Udisks (Русский)](/index.php/Udisks_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udisks (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [File manager functionality](/index.php/File_manager_functionality "File manager functionality"). Дата последней синхронизации: 20 февраля 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=File_manager_functionality&diff=0&oldid=421403).

В этой статье описываются дополнительные программные пакеты, необходимые для расширения возможностей и функций файловых менеджеров, в частности, где используются [оконные менеджеры](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер") такие как [Openbox](/index.php/Openbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Openbox (Русский)"). Если необходимо, также предусмотрена возможность доступа к разделам и съемным носителям информации (например флешкам) без пароля.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Обзор](#Обзор)
*   [2 Дополнительные возможности](#Дополнительные_возможности)
    *   [2.1 Монтирование](#Монтирование)
        *   [2.1.1 Демон файлового менеджера](#Демон_файлового_менеджера)
        *   [2.1.2 Автономный режим](#Автономный_режим)
    *   [2.2 Сети](#Сети)
        *   [2.2.1 Доступ к Windows](#Доступ_к_Windows)
        *   [2.2.2 Доступ к Apple](#Доступ_к_Apple)
    *   [2.3 Превью изображений](#Превью_изображений)
        *   [2.3.1 Другие файловые менеджеры, кроме Dolphin и Konqueror](#Другие_файловые_менеджеры,_кроме_Dolphin_и_Konqueror)
        *   [2.3.2 Dolphin и Konqueror (KDE)](#Dolphin_и_Konqueror_(KDE))
    *   [2.4 Запакованные файлы](#Запакованные_файлы)
    *   [2.5 Поддержка чтения/записи NTFS](#Поддержка_чтения/записи_NTFS)
    *   [2.6 Настольные уведомления](#Настольные_уведомления)
    *   [2.7 Включение функции корзины на разных файловых системах (внешние диски)](#Включение_функции_корзины_на_разных_файловых_системах_(внешние_диски))
*   [3 Решение проблем](#Решение_проблем)
    *   [3.1 При попытке монтирования дисков выдаётся "Not Authorized" (нет авторизации)](#При_попытке_монтирования_дисков_выдаётся_"Not_Authorized"_(нет_авторизации))
    *   [3.2 Для доступа к разделам требуется пароль](#Для_доступа_к_разделам_требуется_пароль)
    *   [3.3 Каталоги не открываются в файловом менеджере](#Каталоги_не_открываются_в_файловом_менеджере)

## Обзор

**Примечание:** При установке, пакеты программного обеспечения перечисленные ниже, автоматически будут поставляться во всех установленных - и поддерживаемых Файловых менеджерах, во всех рабочих средах и/или оконных менеджерах.

Файловый менеджер сам по себе не будет предоставлять возможности и функциональность рабочих сред, таких как [Xfce](/index.php/Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xfce (Русский)") или [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)") к которым привыкли пользователи. Это потому, что дополнительные пакеты программного обеспечения надо будет включить в данный файловый менеджер для:

*   Отображения и доступа к другим разделам
*   Отображения, монтирования, и доступа к съёмным носителям (таким, как USB-флешки, оптические диски, и цифровые камеры)
*   Включения обмена информацией с помощью сети/общих сетей, с другими установленными операционными системами
*   Включения миниатюр для файлов
*   Создания и распаковки файлов из архива
*   Автоматического монтирования сменных носителей

Если файловый менеджер устанавливается как часть полного окружения рабочего стола, эти пакеты, как правило, устанавливаются автоматически. Следовательно, если файловый менеджер был установлен для автономного оконного менеджера, то, как и в случае с самим оконным менеджером - будут предоставляться только основные базовые функции. Затем, пользователь должен определить характер и степень функциональных возможностей которые будут добавлены.

## Дополнительные возможности

В частности, когда вы хотите использовать легковесную среду, следует отметить, что чем больше возможностей и функций у файлового менеджера тем больше он использует памяти. Смотрите также [udisks](/index.php/Udisks_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udisks (Русский)").

### Монтирование

*   [gvfs](https://www.archlinux.org/packages/?name=gvfs): The **G**nome **V**irtual **F**ile **S**ystem (Виртуальная Файловая Система Gnome) предоставляет функции монтирования и корзины. GVFS использует [udisks2](https://www.archlinux.org/packages/?name=udisks2) для функции монтирования, он является рекомендуемым решением для большинства файловых менеджеров.

Каталоги используемые GVFS:

*   `/usr/lib/gvfs/` содержит файлы `gvfsd-*`, где `*` относится к различным поддерживаемым типам файловых систем.
*   `/usr/share/gvfs/mounts/` содержит правила монтирования для GVFS. Для использования собственных правил, создайте `~/.gvfs/mounts`.

Дополнительные пакеты для установки обычно следуют из этого [gvfs-* шаблона](https://www.archlinux.org/packages/?q=gvfs-), например:

*   [gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp): медиа-плееры и мобильные устройства, которые используют [MTP](/index.php/MTP "MTP")
*   [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2): цифровые фотоаппараты и мобильные устройства, которые используют [PTP](https://en.wikipedia.org/wiki/Picture_Transfer_Protocol "wikipedia:Picture Transfer Protocol")
*   [gvfs-afc](https://www.archlinux.org/packages/?name=gvfs-afc): мобильные устройства Apple

#### Демон файлового менеджера

Во-первых, просто добавьте в автозагрузку файловый менеджер или запустите его в режиме [демона](/index.php/%D0%94%D0%B5%D0%BC%D0%BE%D0%BD%D1%8B "Демоны") (т.е. в качестве фонового процесса). Например, при использовании [PCManFM](/index.php/PCManFM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PCManFM (Русский)") в [Openbox](/index.php/Openbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Openbox (Русский)"), следующая команда будет добавлена в файл `~/.config/openbox/autostart`:

```
pcmanfm -d &

```

Также будет необходимо настроить сам файловый менеджер в отношении управления томами (например, то, что он будет делать и какие приложения будут запущены, когда некоторые типы файлов будут обнаружены при монтировании).

**Совет:** Большинство настольных сред, по умолчанию, запускает файловый менеджер в режиме демона, так что в этих случаях ручное вмешательство не требуется.

#### Автономный режим

Другой вариант заключается в установке отдельного [приложения для монтирования разделов](/index.php/List_of_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Разделы_дисков "List of applications (Русский)"). Преимущество такого варианта:

*   Может потребоваться меньше памяти для запуска в качестве фонового процесса/[демона](/index.php/%D0%94%D0%B5%D0%BC%D0%BE%D0%BD%D1%8B "Демоны") по сравнению с файловым менеджером
*   Не специфично для файлового менеджера, что позволяет его свободно добавлять, удалять и менять
*   [gvfs](https://www.archlinux.org/packages/?name=gvfs) не должен быть установлен для монтирования, что уменьшит использование памяти.

### Сети

**Примечание:** Также будет необходимо включить [Bluetooth](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bluetooth (Русский)") и/или связь по сети с [Windows](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Samba (Русский)") для того, чтобы задействовать соответствующую функциональность файлового менеджера.

*   [obexfs](https://aur.archlinux.org/packages/obexfs/): Монтирование устройств Bluetooth и передача файлов (смотрите [Bluetooth](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bluetooth (Русский)"))
*   [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb): Совместное использование принтеров и файлов Windows для **Не-KDE** рабочих сред (смотрите [Samba](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Samba (Русский)"))
*   [kdenetwork-filesharing](https://www.archlinux.org/packages/?name=kdenetwork-filesharing): Совместное использование принтеров и файлов Windows для [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)") (смотрите [Samba#KDE](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#KDE "Samba (Русский)"))
*   [gvfs-afp](https://www.archlinux.org/packages/?name=gvfs-afp): Совместное использование файлов и принтеров Apple
*   [sshfs](https://www.archlinux.org/packages/?name=sshfs): FUSE-клиент на основе протокола передачи файлов SSH

#### Доступ к Windows

При использовании [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb), чтобы получить доступ к общим файлам Windows/CIFS/Samba сначала откройте файловый менеджер, и введите следующую команду в адресной строке, изменяя <sever name> и <share name> в соответствующих случаях:

```
smb://<server name>/<share name>

```

#### Доступ к Apple

Поддержка AFP включена в [gvfs](https://www.archlinux.org/packages/?name=gvfs), для доступа к файлам AFP начала откройте файловый менеджер, и введите следующую команду в адресной строке, изменяя <sever name> и <share name> в соответствующих случаях:

```
afp://<server name>/<share name>

```

### Превью изображений

Некоторые файловые менеджеры не поддерживают миниатюры, даже когда перечисленные пакеты были установлены. Проверьте документацию для соответствующего файлового менеджера.

#### Другие файловые менеджеры, кроме Dolphin и Konqueror

Эти пакеты применяются для большинства файловых менеджеров, таких как [PCManFM](/index.php/PCManFM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PCManFM (Русский)"), [SpaceFM](/index.php/SpaceFM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SpaceFM (Русский)"), [Thunar](/index.php/Thunar_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Thunar (Русский)") и [xfe](https://aur.archlinux.org/packages/xfe/). Исключение составляют Dolphin и Konqueror, использующиеся в среде рабочего стола [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)").

*   [tumbler](https://www.archlinux.org/packages/?name=tumbler): Графические файлы. **<u>Необходимо</u>** поставить чтобы расширить возможности для отображения миниатюр файлов других типов
*   [poppler-glib](https://www.archlinux.org/packages/?name=poppler-glib): Adobe файлы `.pdf`
*   [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer): Видео файлы
*   [freetype2](https://www.archlinux.org/packages/?name=freetype2): Файлы шрифтов
*   [libgsf](https://www.archlinux.org/packages/?name=libgsf): Файлы `.odf`
*   [raw-thumbnailer](https://www.archlinux.org/packages/?name=raw-thumbnailer): `.raw` файлы
*   [totem](https://www.archlinux.org/packages/?name=totem): Видео файлы и тэги аудио файлов (только [GNOME Files](/index.php/GNOME_Files "GNOME Files"), [Nemo](/index.php/Nemo "Nemo") и Caja)
*   [evince](https://www.archlinux.org/packages/?name=evince) или [atril](https://www.archlinux.org/packages/?name=atril): `.pdf` файлы

#### Dolphin и Konqueror (KDE)

Смотрите [Dolphin#File previews](/index.php/Dolphin#File_previews "Dolphin").

### Запакованные файлы

Чтобы извлечь сжатые файлы, такие как "тарболы" (`.tar` и `.tar.gz`) с помощью файлового менеджера, сначала надо установить архиватор с графическим интерфейсом, например [file-roller](https://www.archlinux.org/packages/?name=file-roller). Для получения дополнительной информации смотрите [Список приложений#Инструменты архивации и сжатия](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#Инструменты_архивации_и_сжатия "Список приложений"). Дополнительный пакет, например [unzip](https://www.archlinux.org/packages/?name=unzip) также должен быть установлен, для поддержки распаковки файлов `.zip`. После установки программы-архиватора, можно в контекстном меню (вызываемым правой кнопкой мыши) выбрать упаковывать/распаковывать файлы.

Архивные файлы смонтированы в папке `/run/user/$(id -u)/gvfs/`, автоматически создается точка монтирования, которая содержит полный путь к файлу в его названии, где все `/` заменены на `%252F` и `:` заменены на `%253A` [шестнадцатеричные коды](https://www.owasp.org/index.php/Double_Encoding).

Пример пути к смонтированному архиву `/full/path/to/file/name.zip`

```
/run/user/$(id -u)/gvfs/archive:host=file%253A%252F%252F%252F**full%252Fpath%252Fto%252Ffile%252Fname.zip**

```

### Поддержка чтения/записи NTFS

Смотрите статью [NTFS-3G (Русский)](/index.php/NTFS-3G_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NTFS-3G (Русский)").

### Настольные уведомления

Некоторые файловые менеджеры используют [настольные уведомления](/index.php/Desktop_notifications "Desktop notifications") для подтверждения различных событий и состояний, например: монтирование, размонтирование и отсоединение съемных носителей.

### Включение функции корзины на разных файловых системах (внешние диски)

Создайте [каталог Корзины](http://www.ramendik.ru/docs/trashspec.html) `.Trash-*<uid>*` для всех пользователей на верхнем уровне файловой системы:

Например (точка монтирования: /media/sdc1, uid: 1000, gid: 1000):

```
# mkdir /media/sdc1/.Trash-1000

```

и `chown` (смените владельца):

```
# chown 1000:1000 /media/sdc1/.Trash-1000

```

## Решение проблем

### При попытке монтирования дисков выдаётся "Not Authorized" (нет авторизации)

Файловые менеджеры использующие [Udisks](/index.php/Udisks_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udisks (Русский)") требуют агент аутендификации [polkit](/index.php/Polkit "Polkit"). Смотрите [polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit").

### Для доступа к разделам требуется пароль

Необходимость ввода пароля для доступа к другим разделам или монтирования съемных носителей, вероятно, будет из-за настроек разрешения по умолчанию в [udisks2](https://www.archlinux.org/packages/?name=udisks2). Более конкретно разрешение может быть установлен только в учетной записи администратора, а не учетной записи пользователя. Для подробностей смотрите [Udisks#Настройка](/index.php/Udisks_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Настройка "Udisks (Русский)").

### Каталоги не открываются в файловом менеджере

Вы можете обнаружить, что приложение, которое не является файловым менеджером, например [Audacious](/index.php/Audacious "Audacious") устанавливается в качестве приложения по умолчанию для открытия каталогов — приложение указывает MIME тип `inode/directory` в его desktop записи по умолчанию. Вы можете запросить приложение по умолчанию для открытия каталогов с помощью следующей команды:

```
$ xdg-mime query default inode/directory

```

Для того, чтобы убедиться, что каталоги открываются в файловом менеджере, выполните следующую команду:

```
$ xdg-mime default *my-file-manager.desktop* inode/directory

```

где `*my-file-manager.desktop*` запись desktop является вашим файловым менеджером — например `*org.gnome.Nautilus.desktop*`.

**Совет:** Если вы хотите поменять общесистемные настройки, запустите вышеуказанную команду от имени суперпользователя, или создайте / отредактируйте следующий файл: `/usr/share/applications/mimeapps.list` 
```
[Default Applications]
inode/directory=*my-file-manager.desktop*
```