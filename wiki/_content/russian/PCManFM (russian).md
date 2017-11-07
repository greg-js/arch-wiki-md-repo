Related articles

*   [SpaceFM (Русский)](/index.php/SpaceFM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SpaceFM (Русский)")

**PCManFM** (PCMan File Manager) — стандартный файловый менеджер среды [LXDE](/index.php/LXDE "LXDE") с открытым исходным кодом, представляющей собой набор приложений незваисимых друг от друга, но объединенных принципом экономии ресурсов. Продукт разрабатывается китайским программистом Hong Jen Yee (кит. 洪任諭), разработчиком графической среды [LXDE](/index.php/LXDE "LXDE").(Источник: [[1]](https://ru.wikipedia.org/wiki/PCManFM))

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Работа с томами](#.D0.A0.D0.B0.D0.B1.D0.BE.D1.82.D0.B0_.D1.81_.D1.82.D0.BE.D0.BC.D0.B0.D0.BC.D0.B8)
    *   [2.1 Монтирование с помощью udisks](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_udisks)
    *   [2.2 Монтирование с помощью gvfs](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_gvfs)
    *   [2.3 Монтирование от обычного пользователя](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BE.D1.82_.D0.BE.D0.B1.D1.8B.D1.87.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F)
*   [3 Советы & Решение проблем](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.26_.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [3.1 Отсутствует пункт "Приложения"?](#.D0.9E.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D0.B5.D1.82_.D0.BF.D1.83.D0.BD.D0.BA.D1.82_.22.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F.22.3F)
    *   [3.2 Отсутствует корзина?](#.D0.9E.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D0.B5.D1.82_.D0.BA.D0.BE.D1.80.D0.B7.D0.B8.D0.BD.D0.B0.3F)
    *   [3.3 Отсутствуют иконки?](#.D0.9E.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.82_.D0.B8.D0.BA.D0.BE.D0.BD.D0.BA.D0.B8.3F)
    *   [3.4 Поддержка чтения/записи на NTFS](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_.D1.87.D1.82.D0.B5.D0.BD.D0.B8.D1.8F.2F.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D0.B8_.D0.BD.D0.B0_NTFS)
    *   [3.5 gnome-open открывает диалог "Поиск" вместо дирректории](#gnome-open_.D0.BE.D1.82.D0.BA.D1.80.D1.8B.D0.B2.D0.B0.D0.B5.D1.82_.D0.B4.D0.B8.D0.B0.D0.BB.D0.BE.D0.B3_.22.D0.9F.D0.BE.D0.B8.D1.81.D0.BA.22_.D0.B2.D0.BC.D0.B5.D1.81.D1.82.D0.BE_.D0.B4.D0.B8.D1.80.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B8)
    *   [3.6 Для кнопок мыши отсутствует функция "Предыдущая/Следующая папка"](#.D0.94.D0.BB.D1.8F_.D0.BA.D0.BD.D0.BE.D0.BF.D0.BE.D0.BA_.D0.BC.D1.8B.D1.88.D0.B8_.D0.BE.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D0.B5.D1.82_.D1.84.D1.83.D0.BD.D0.BA.D1.86.D0.B8.D1.8F_.22.D0.9F.D1.80.D0.B5.D0.B4.D1.8B.D0.B4.D1.83.D1.89.D0.B0.D1.8F.2F.D0.A1.D0.BB.D0.B5.D0.B4.D1.83.D1.8E.D1.89.D0.B0.D1.8F_.D0.BF.D0.B0.D0.BF.D0.BA.D0.B0.22)
    *   [3.7 параметр --desktop не работает / вызывает сбой X-сервера](#.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80_--desktop_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.2F_.D0.B2.D1.8B.D0.B7.D1.8B.D0.B2.D0.B0.D0.B5.D1.82_.D1.81.D0.B1.D0.BE.D0.B9_X-.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0)
    *   [3.8 В расширенных настройках не сохраняется команда вызова эмулятора терминала](#.D0.92_.D1.80.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0.D1.85_.D0.BD.D0.B5_.D1.81.D0.BE.D1.85.D1.80.D0.B0.D0.BD.D1.8F.D0.B5.D1.82.D1.81.D1.8F_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.B0_.D0.B2.D1.8B.D0.B7.D0.BE.D0.B2.D0.B0_.D1.8D.D0.BC.D1.83.D0.BB.D1.8F.D1.82.D0.BE.D1.80.D0.B0_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B0)
    *   [3.9 PCManFM не запоминает настройки из меню Сортировать файлы](#PCManFM_.D0.BD.D0.B5_.D0.B7.D0.B0.D0.BF.D0.BE.D0.BC.D0.B8.D0.BD.D0.B0.D0.B5.D1.82_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D0.B8.D0.B7_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.A1.D0.BE.D1.80.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D1.82.D1.8C_.D1.84.D0.B0.D0.B9.D0.BB.D1.8B)
*   [4 Доступные версии](#.D0.94.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.BD.D1.8B.D0.B5_.D0.B2.D0.B5.D1.80.D1.81.D0.B8.D0.B8)
    *   [4.1 PCManFM2](#PCManFM2)
    *   [4.2 PCManFM 0.5.2](#PCManFM_0.5.2)
    *   [4.3 PCManFM-Mod](#PCManFM-Mod)
    *   [4.4 PCManFM_with_Search](#PCManFM_with_Search)

## Установка

Для установки Pcmanfm выполните:

```
# pacman -S pcmanfm

```

Также, для отслеживания изменений файлов и дирректорий, неоходимо будет установить [gamin](/index.php/Gamin "Gamin") (являющийся заменой устаревшего [FAM](/index.php/FAM "FAM")). Для установки выполните:

```
# pacman -S gamin

```

## Работа с томами

**PCManFM** может монтировать и размонтировать устройства как вручную, так и автоматически. Эта возможность предоставляется в качестве альтернативы таким инструментам **CLI** - как **pmount**. PCManFM поддерживает несколько вариантов управления томами (см. ниже).

**Примечание:** У вас должна существовать директория `/media`.

### Монтирование с помощью udisks

Последний официальный выпуск PCManFM имеет поддержку udisks. Если вы хотите использовать эту функцию - убедитесь в том, что демон D-Bus установлен и запущен. Для получения дополнительной информации обратитесь к странице [D-Bus](/index.php/D-Bus "D-Bus"). Обратите внимание, что вам, скорее всего, прийдется запускать либо из вашего [.xinitrc](/index.php/Xinitrc "Xinitrc"), либо с помощью скрипта автозапуска вашего оконного менеджера. Инструкции по запуску можно найти или на страничке [D-Bus](/index.php/D-Bus "D-Bus"), или на страничке посвященной вашему [оконному менеджеру](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)").

### Монтирование с помощью gvfs

Для поддержки Gnome Virtual FileSystem, помимо действий перечисленных выше, вам придется установить дополнительные пакеты:

*   [gvfs](https://www.archlinux.org/packages/?name=gvfs) (и зависимости);
*   (опционально) [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb), [gvfs-obexftp](https://www.archlinux.org/packages/?name=gvfs-obexftp), [gvfs-afc](https://www.archlinux.org/packages/?name=gvfs-afc), и т.д. для получения нужной функциональности.

### Монтирование от обычного пользователя

Для монтирования устройств, таких как съемные жесткие USB-диски, флэшки или DVD-диски от простого пользователя необходимо соответствующим образом настроить инструментры [PolicyKit](/index.php/PolicyKit "PolicyKit"). Нужные конфигурационные файлы можно найти в подкаталогах `/etc/polkit-1`. Далее будет рассказано как с помощью PolicyKit разрешить пользователям, входящим в группу "storage", монтировать и размонтировать временные устройства.

**Примечание:** На данное время PolicyKit по умолчанию сконфигурирован так, чтобы разрешать монтировать/размонтировать всем пользователям входящим в группу *storage*. Таким образом этот шаг можно пропустить.

От root создайте файл`/etc/polkit-1/localauthority/50-local.d/55-myconf.pkla` (файл может иметь любое имя, но оканчиваться должен на .pkla.) следующего содержания:

```
 [Storage Permissions]
 Identity=unix-group:storage
 Action=org.freedesktop.udisks.filesystem-mount;org.freedesktop.udisks.drive-eject;org.freedesktop.udisks.drive-detach;org.freedesktop.udisks.luks-unlock;org.freedesktop.udisks.inhibit-polling;org.freedesktop.udisks.drive-set-spindown
 ResultAny=yes
 ResultActive=yes
 ResultInactive=no

```

Для вступления в силу изменений настроек PolicyKit не требуется вашего дополнительного вмешательства. Напоследок, нужно всех пользователей, которым можно будет выполнять операции монтирования/размонтирования, добавить в группу storage:

```
# usermod -a -G storage USERNAME

```

Если вам нужно настроить монтирование другим способом (без добавления пользователей в группу storage) или вы хотите лучше понять написаное выше, - обратитесь к manpage:

```
$ man pklocalauthority

```

## Советы & Решение проблем

### Отсутствует пункт "Приложения"?

```
# pacman -S gnome-menus

```

Если в пункте "приложения" не отображаются меню с приложениями то, создайте файл *~/.config/menus/applications.menu* и добавте в него следующие строки:

```
 <Menu>
  <Name>Applications</Name>
  <MergeFile type="parent">/etc/xdg/menus/lxde-applications.menu</MergeFile>
 </Menu>

```

### Отсутствует корзина?

```
# pacman -S gvfs

```

### Отсутствуют иконки?

Если вы используете [оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер") без DE ([Среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола")) и при этом отсутствуют иконки файлов и папок, просто установите следующую тему иконок:

```
# pacman -S tangerine-icon-theme

```

Отредактируйте файл `~/.gtkrc-2.0` **или** `/etc/gtk-2.0/gtkrc` и добавьте в конец строку:

```
gtk-icon-theme-name = "Tangerine"

```

### Поддержка чтения/записи на NTFS

Установите ntfs-3g (Подробнее [NTFS-3G](/index.php/NTFS-3G "NTFS-3G")):

```
# pacman -S ntfs-3g

```

### gnome-open открывает диалог "Поиск" вместо дирректории

Удалите или переименуйте файл `/usr/share/applications/pcmanfm-find.desktop`. При использовании pcmanfm-mod из AUR, следует удалить или переименовать файл `/usr/share/applications/pcmanfm-mod-find.desktop`.

### Для кнопок мыши отсутствует функция "Предыдущая/Следующая папка"

Решение этой проблемы с помощью [Xbindkeys](/index.php/Xbindkeys "Xbindkeys"):

Установите xbindkeys:

```
# pacman -S xbindkeys

```

Отредактируйте ~/.xbindkeysrc добавив в него следующее:

```
# Пример .xbindkeysrc для мыши G9x.
"/usr/bin/xvkbd -text '\[Alt_L]\[Left]'"
 b:8
"/usr/bin/xvkbd -text '\[Alt_L]\[Right]'"
 b:9

```

Свои коды кнопок можно узнать при помощи [xev](https://www.archlinux.org/packages/?name=xev).

Добавьте

```
xbindkeys &

```

В свой файл `~/.xinitrc`, при этом xbindkeys будет запущен при логине.

### параметр --desktop не работает / вызывает сбой X-сервера

Убедитесь что вы являетесь владельцем и имеете право на запись в `~/.config/pcmanfm`

Установка обоев с помощью параметра --desktop-pref или путем отредактирования `~/.config/pcmanfm/default/pcmanfm.config` решает проблему.

### В расширенных настройках не сохраняется команда вызова эмулятора терминала

Убедитесь в наличии прав доступа к конфигурационному файлу libfm:

```
# chmod -R 755 ~/.config/libfm
# chmod 777 ~/.config/libfm/libfm.conf

```

### PCManFM не запоминает настройки из меню Сортировать файлы

Настроить порядок отображения файлов в PCManFM можно с помощью меню **Вид | Сортировать файлы**, но эти настройки будут сбрасываться при следующем запуске PCManFM. Для сохранения настроек перейдите в **Правка | Параметры** и нажмите кнопку **Закрыть**. После этого текущие значения переменных *sort_type* и *sort_by* будут занесены в файл `~/.config/pcmanfm/LXDE/pcmanfm.conf`.

## Доступные версии

В настоящее время доступны несколько версий PCManFM:

### PCManFM2

Этот пакет называется [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm) доступен в репозитории community. Последнюю тестовую версию [pcmanfm-git](https://aur.archlinux.org/packages/pcmanfm-git/) можно найти в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"). Для получения дополнительной информации читайте [LXDE Forum](http://forum.lxde.org/viewforum.php?f=22).

### PCManFM 0.5.2

Предыдущий PCManFM (версия 0.5.2, в настоящее время находящийся в репозиротии [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") и называющийся *pcmanfm-legacy*) больше не разрабатывается и не поддерживается автором. Эта версия для монтирования использует [HAL](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)"). Дополнительную информация можно найти на [странице проекта](http://pcmanfm.sourceforge.net/intro.html).

### PCManFM-Mod

В PCManFM-Mod добавлены пользовательские команды и другие функции, а также исправлены ошибки версии v0.5.2\. Эта версия собирается и устанавливается как *pcmanfm-mod* и работает независимо от других версий PCManFM, которые установлены в вашей системе. Эта версия считается более стабильной, чем 0.9.x, имеет меньше зависимостей [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") и использует [HAL](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") вместо *gnome-vfs*. PCManFM-Mod доступен в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") как [pcmanfm-mod](https://aur.archlinux.org/packages/pcmanfm-mod%5D/)] и как [pcmanfm-mod-prov](https://aur.archlinux.org/packages/pcmanfm-mod-prov/) (последняя разработка *pcmanfm*). Для получения дополнительной информации посетите [блог IgnorantGuru's](http://igurublog.wordpress.com/downloads/mod-pcmanfm/).

### PCManFM_with_Search

В [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") можно найти последнюю весию PCmanFM с диалогом поиска, пакет называется [pcmanfm_with_search](https://aur.archlinux.org/packages/pcmanfm_with_search/).