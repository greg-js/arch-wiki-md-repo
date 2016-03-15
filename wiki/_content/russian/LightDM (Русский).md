**Состояние перевода:** На этой странице представлен перевод статьи [LightDM](/index.php/LightDM "LightDM"). Дата последней синхронизации: 13 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=LightDM&diff=0&oldid=425490).

[LightDM](http://www.freedesktop.org/wiki/Software/LightDM) это кросс-десктопный [Экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер"). Главные особенности:

*   Кросс-десктопный - поддерживает различные технологии рабочего стола.
*   Поддерживает различные технологии отображения (X, Wayland, Mir, ...).
*   Легковесный - низкое потребление памяти и высокая производительность.
*   Поддержка гостевых сессий.
*   Поддержка удаленного входа (входящий - XDMCP, VNC, исходящие - XDMCP, подключаемые).
*   Комплексный набор тестов.
*   Низкая сложность кода.

Более подробную информацию о проекте LightDM можно найти [здесь](http://www.freedesktop.org/wiki/Software/LightDM/Design).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Greeter (Экран приветствия/входа в систему)](#Greeter_.28.D0.AD.D0.BA.D1.80.D0.B0.D0.BD_.D0.BF.D1.80.D0.B8.D0.B2.D0.B5.D1.82.D1.81.D1.82.D0.B2.D0.B8.D1.8F.2F.D0.B2.D1.85.D0.BE.D0.B4.D0.B0_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83.29)
*   [2 Включение LightDM](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_LightDM)
*   [3 Инструмент командной строки](#.D0.98.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BC.D0.B5.D0.BD.D1.82_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.BD.D0.BE.D0.B9_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B8)
*   [4 Тестирование](#.D0.A2.D0.B5.D1.81.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [5 Дополнительные настройки и твики](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D0.B8_.D1.82.D0.B2.D0.B8.D0.BA.D0.B8)
    *   [5.1 Изменение фонового изображения/цветов](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.84.D0.BE.D0.BD.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D0.B8.D0.B7.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F.2F.D1.86.D0.B2.D0.B5.D1.82.D0.BE.D0.B2)
        *   [5.1.1 Экран преветствия GTK+](#.D0.AD.D0.BA.D1.80.D0.B0.D0.BD_.D0.BF.D1.80.D0.B5.D0.B2.D0.B5.D1.82.D1.81.D1.82.D0.B2.D0.B8.D1.8F_GTK.2B)
        *   [5.1.2 Экран приветствия Unity](#.D0.AD.D0.BA.D1.80.D0.B0.D0.BD_.D0.BF.D1.80.D0.B8.D0.B2.D0.B5.D1.82.D1.81.D1.82.D0.B2.D0.B8.D1.8F_Unity)
        *   [5.1.3 Экран приветствия KDE](#.D0.AD.D0.BA.D1.80.D0.B0.D0.BD_.D0.BF.D1.80.D0.B8.D0.B2.D0.B5.D1.82.D1.81.D1.82.D0.B2.D0.B8.D1.8F_KDE)
    *   [5.2 Изменение вашего аватара](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2.D0.B0.D1.88.D0.B5.D0.B3.D0.BE_.D0.B0.D0.B2.D0.B0.D1.82.D0.B0.D1.80.D0.B0)
    *   [5.3 Внедрение Arch-ориентированных 64x64 иконок](#.D0.92.D0.BD.D0.B5.D0.B4.D1.80.D0.B5.D0.BD.D0.B8.D0.B5_Arch-.D0.BE.D1.80.D0.B8.D0.B5.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_64x64_.D0.B8.D0.BA.D0.BE.D0.BD.D0.BE.D0.BA)
    *   [5.4 Включение автовхода](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B0.D0.B2.D1.82.D0.BE.D0.B2.D1.85.D0.BE.D0.B4.D0.B0)
    *   [5.5 Включение интерактивного без парольного входа в систему](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.B0.D0.BA.D1.82.D0.B8.D0.B2.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B1.D0.B5.D0.B7_.D0.BF.D0.B0.D1.80.D0.BE.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
    *   [5.6 Скрытие пользователей служб и системы](#.D0.A1.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.B9_.D1.81.D0.BB.D1.83.D0.B6.D0.B1_.D0.B8_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [5.7 Миграция с SLiM](#.D0.9C.D0.B8.D0.B3.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D1.81_SLiM)
    *   [5.8 NumLock включен по умолчанию](#NumLock_.D0.B2.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [5.9 Переключение пользователя при Xfce4](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F_.D0.BF.D1.80.D0.B8_Xfce4)
    *   [5.10 Сессия по умолчанию](#.D0.A1.D0.B5.D1.81.D1.81.D0.B8.D1.8F_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [5.11 Adjusting the login window's position](#Adjusting_the_login_window.27s_position)
        *   [5.11.1 Экран приветствия GTK+](#.D0.AD.D0.BA.D1.80.D0.B0.D0.BD_.D0.BF.D1.80.D0.B8.D0.B2.D0.B5.D1.82.D1.81.D1.82.D0.B2.D0.B8.D1.8F_GTK.2B)
*   [6 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [6.1 Локаль неправильно отображается](#.D0.9B.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C_.D0.BD.D0.B5.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F)
    *   [6.2 Ресурсы X не корректно распознаны](#.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B_X_.D0.BD.D0.B5_.D0.BA.D0.BE.D1.80.D1.80.D0.B5.D0.BA.D1.82.D0.BD.D0.BE_.D1.80.D0.B0.D1.81.D0.BF.D0.BE.D0.B7.D0.BD.D0.B0.D0.BD.D1.8B)
    *   [6.3 Отсутствуют иконки в Экране приветствия GTK](#.D0.9E.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.82_.D0.B8.D0.BA.D0.BE.D0.BD.D0.BA.D0.B8_.D0.B2_.D0.AD.D0.BA.D1.80.D0.B0.D0.BD.D0.B5_.D0.BF.D1.80.D0.B8.D0.B2.D0.B5.D1.82.D1.81.D1.82.D0.B2.D0.B8.D1.8F_GTK)
    *   [6.4 LightDM зависает при попытке входа в систему](#LightDM_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.B5.D1.82_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BF.D1.8B.D1.82.D0.BA.D0.B5_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
    *   [6.5 LightDM отображается в неправильном мониторе](#LightDM_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.B2_.D0.BD.D0.B5.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE.D0.BC_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.B5)
    *   [6.6 LightDM не отображается](#LightDM_.D0.BD.D0.B5_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F)
    *   [6.7 Pulseaudio не запускается автоматически](#Pulseaudio_.D0.BD.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.B0.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8)
*   [7 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/Install "Install") [lightdm](https://www.archlinux.org/packages/?name=lightdm). Обратите внимание, что чётные выпуски являются стабильными (1.8, 1.10), а разрабатываемые релизы, - нечётными (1.9, 1.11). Разрабатываемые релизы доступны в [lightdm-devel](https://aur.archlinux.org/packages/lightdm-devel/). Также доступен [lightdm-bzr](https://aur.archlinux.org/packages/lightdm-bzr/).

### Greeter (Экран приветствия/входа в систему)

Возможно вы хотите установить Экран приветствия. Экран приветствия представляет собой графический интерфейс, который предлагает пользователю ввести учетные данные, выбрать сеанс, и так далее. Можно использовать LightDM без Экрана приветствия, но только если он настроен на автоматический вход в систему. Ссылка на Экран приветствия [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter). LightDM пытается использовать этот Экран приветствия при запуске, если он не настроен иначе.

Официальные репозитории содержат следующие альтернативные Экраны приветствия.

*   [lightdm-kde-greeter](https://www.archlinux.org/packages/?name=lightdm-kde-greeter): Гритер использующий KDE4.
*   lightdm-deepin-greeter ([deepin-session-ui](https://www.archlinux.org/packages/?name=deepin-session-ui)): Экран приветствия из проекта [Deepin](/index.php/Deepin_Desktop_Environment "Deepin Desktop Environment").

Другие альтернативные Экраны приветствия доступны в [AUR](/index.php/AUR "AUR").

*   [lightdm-webkit2-greeter](https://aur.archlinux.org/packages/lightdm-webkit2-greeter/): Экран приветствия, который использует Webkit2 для тем. Он заменяет [lightdm-webkit-greeter](https://aur.archlinux.org/packages/lightdm-webkit-greeter/).
*   [lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/): Экран приветствия использующися в Ubuntu [Unity](/index.php/Unity "Unity").
*   [lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/): Экран приветствия из проекта elementary OS.

Вы можете установить Экран приветствия по умолчанию, путём изменения раздела `[Seat:*]` в файле настроек LightDM, например:

 `/etc/lightdm/lightdm.conf` 
```
[Seat:*]
...
greeter-session=lightdm-yourgreeter-greeter
```

Какие Экраны приветствия доступны? Какие значения можно назначить опцией `greeter-session`? Каждый файл `.desktop` в каталоге `/usr/share/xgreeters` обозначает доступный Экран приветствия. В этом примере доступны Экраны приветствия `lightdm-gtk-greeter` и `lightdm-kde-greeter`:

```
$ ls -1 /usr/share/xgreeters/
lightdm-gtk-greeter.desktop
lightdm-kde-greeter.desktop

```

## Включение LightDM

Убедитесь в том что вы [включили](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") `lightdm.service` чтобы LightDM запускался при загрузке. Смотрите также [Экранный менеджер#Запуск экранного менеджера](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0 "Экранный менеджер").

## Инструмент командной строки

LightDM предлагает инструмент командной строки, `dm-tool`, который может быть использован для блокировки текущего места, переключения сеансов и т.д., что полезно в «минималистских» оконных менеджерах и для тестирования. Чтобы увидеть список доступных команд, выполните следующую команду:

```
$ dm-tool --help

```

## Тестирование

Вопервых, [установите](/index.php/Install "Install") [xorg-server-xephyr](https://www.archlinux.org/packages/?name=xorg-server-xephyr) из [официальных репозиториев](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B8 "Официальные репозитории").

Затем запустите LightDM как приложение X:

```
$ lightdm --test-mode --debug

```

## Дополнительные настройки и твики

Некоторые Экраны приветствия имеют свои собственные файлы настроек. Например [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) имеет:

```
/etc/lightdm/lightdm-gtk-greeter.conf

```

и [lightdm-kde-greeter](https://www.archlinux.org/packages/?name=lightdm-kde-greeter) has:

```
/etc/lightdm/lightdm-kde-greeter.conf

```

а также раздел в системных настройках KDE (рекомендуется).

LightDM может быть настроен путём изменения его скрипта настроек, `/etc/lightdm/lightdm.conf`.

### Изменение фонового изображения/цветов

Пользователи, желающие иметь плоский цвет (без изображения) могут установить шестнадцатеричное значение `background` цвета.

Пример:

```
background=#000000

```

Если вы хотите вместо этого использовать изображение, смотрите ниже.

#### Экран преветствия GTK+

Можете воспользоваться программой с графическим интерфейсом [lightdm-gtk-greeter-settings](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter-settings).

Пользователям, желающим настроить обои на экране приветствия необходимо отредактировать `/etc/lightdm/lightdm-gtk-greeter.conf` и определить переменную `background` под секцией `[greeter]`. Например:

 `/etc/lightdm/lightdm-gtk-greeter.conf` 
```
[greeter]
background=/usr/share/pixmaps/black_and_white_photography-wallpaper-1920x1080.jpg
```

**Примечание:** Рекомендуется поместить PNG или JPG-файл в `/usr/share/pixmaps` т.к. пользователю LightDM нужен доступ на чтение файла обоев рабочего стола.

#### Экран приветствия Unity

Пользователи, использующие [lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/) должны отредактировать `/usr/share/glib-2.0/schemas/com.canonical.unity-greeter.gschema.xml` файл, а затем выполнить:

```
# glib-compile-schemas /usr/share/glib-2.0/schemas/

```

В соответствии с [этой](https://bbs.archlinux.org/viewtopic.php?id=149945) страницей.

#### Экран приветствия KDE

Зайдите в *System Settings > Login Screen (LightDM)* и измените фоновое изображение для вашей темы.

Как вариант, можете отредактировать переменную `Background` в `lightdm-kde-greeter.conf` :

 `/etc/lightdm/lightdm-kde-greeter.conf` 
```
[greeter]
theme-name=classic

[greeter-settings]
Background=/usr/share/archlinux/wallpaper/archlinux-underground.jpg
BackgroundKeepAspectRatio=true
GreetMessage=Welcome to %hostname%
```

### Изменение вашего аватара

**Совет:** Если вы используете KDE, вы можете изменить свой аватар в Системных Настройках KDE.

Во-первых, убедитесь, что пакет [accountsservice](https://www.archlinux.org/packages/?name=accountsservice) из [Официальных репозиториев](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B8 "Официальные репозитории") установлен, затем установите его следующим образом, заменив `*username*` на регистрационное именем нужного пользователя. Расширение файла *.png* не должно быть включено в имя файла.

*   Отредактируйте или создайте файл `/var/lib/AccountsService/users/*username*`, и добавьте строки

```
[User]
Icon=/var/lib/AccountsService/icons/*username*

```

*   Создайте файл `/var/lib/AccountsService/icons/*username*` используя файл изображения 96x96 PNG.

**Примечание:** Убедитесь, что оба созданных файлы имеют права 644, используйте [Chmod](/index.php/Chmod "Chmod"), чтобы исправить права, при необходимости.

### Внедрение Arch-ориентированных 64x64 иконок

Пакет [archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/) из [AUR](/index.php/AUR "AUR") содержит некоторые интересные примеры, которые устанавливаются в `/usr/share/archlinux/icons` и которые могут быть скопированы в `/usr/share/icons/hicolor/64x64/devices` следующим образом:

```
# find /usr/share/archlinux/icons -name "*64*" -exec cp {} /usr/share/icons/hicolor/64x64/devices \;

```

После копирования, пакет [archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/) может быть удалён.

### Включение автовхода

Отредактируйте файл настроек LightDM, расскомментируйте эти строки и правильно настройте:

 `/etc/lightdm/lightdm.conf` 
```
[Seat:*]
pam-service=lightdm
pam-autologin-service=lightdm-autologin
autologin-user=*username*
autologin-user-timeout=0
session-wrapper=/etc/lightdm/Xsession
```

LightDM проходит через PAM даже когда включен `autologin`. Вы должны быть в группе `autologin` чтобы входить в систему автоматически без вода пароля:

```
# groupadd -r autologin
# gpasswd -a *username* autologin

```

**Примечание:** GNOME users, and by extension any gnome-keyring user will have to set up a blank password to their keyring for it to be unlocked automatically.

### Включение интерактивного без парольного входа в систему

LightDM проходит через PAM, так что вы должны сконфигурировать lightdm настройки PAM:

 `/etc/pam.d/lightdm` 
```
#%PAM-1.0
**auth        sufficient  pam_succeed_if.so user ingroup nopasswdlogin**
auth        include     system-login
...
```

Вы также должны входить в группу `nopasswdlogin` чтобы получить возможность входа в систему в интерактивном режиме без ввода пароля:

```
# groupadd -r nopasswdlogin
# gpasswd -a *username* nopasswdlogin

```

**Примечание:** Пользователям GNOME, и расширениям любого пользовательского Gnome-брелка, возможно, придётся следовать инструкциям в конце предыдущего раздела о включении автоматического логина.

Для того, чтобы создать новую учетную запись пользователя, которая входит в систему автоматически и дополнительно имеет возможность снова войти в систему без пароля, пользователь может быть создан с помощью дополнительного участия в обеих группах и т.д .:

```
# useradd -mG autologin,nopasswdlogin -s /bin/bash *username*

```

### Скрытие пользователей служб и системы

To prevent system users from showing-up in the login, install the optional dependency [accountsservice](https://www.archlinux.org/packages/?name=accountsservice), or add the user names to `/etc/lightdm/users.conf` under `hidden-users`. The first option has the advantage of not needing to update the list when more users are added or removed.

### Миграция с SLiM

Move the contents of [xinitrc](/index.php/Xinitrc "Xinitrc") to [xprofile](/index.php/Xprofile "Xprofile"), removing the call to start the [window manager](/index.php/Window_manager "Window manager") or [desktop environment](/index.php/Desktop_environment "Desktop environment").

### NumLock включен по умолчанию

Установите пакет [numlockx](https://www.archlinux.org/packages/?name=numlockx) и отредактируйте `/etc/lightdm/lightdm.conf` добавив следующие строки:

```
greeter-setup-script=/usr/bin/numlockx on

```

### Переключение пользователя при Xfce4

If you use the [Xfce](/index.php/Xfce "Xfce") desktop, the Switch User functionality of the Action Button found in your Application Launcher specifically looks for the *gdmflexiserver* executable in order to enable itself. If you provide it with an executable shell script `/usr/bin/gdmflexiserver` consisting of

```
#!/bin/sh
/usr/bin/dm-tool switch-to-greeter

```

то переключение пользователей в Xfce должно работать с LightDM.

В качестве альтернативы, если вы используете меню Whisker, пройдите Properties -> Commands и измените команду "Switch Users" непосредственно на:

```
 dm-tool switch-to-greeter

```

Кроме того, можно переключать пользователей с экрана блокировки [XScreenSaver](/index.php/XScreenSaver "XScreenSaver"), - смотрите [XScreenSaver#LightDM](/index.php/XScreenSaver#LightDM "XScreenSaver").

### Сессия по умолчанию

Lightdm, как и другие Экранные менеджеры, хранит последнюю выбранную xsession в `~/.dmrc`. Для подробностей смотрите [Экранный менеджер#Список сеансов](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D1.81.D0.B5.D0.B0.D0.BD.D1.81.D0.BE.D0.B2 "Экранный менеджер").

### Adjusting the login window's position

#### Экран приветствия GTK+

Пользователям нужно отредактировать `/etc/lightdm/lightdm-gtk-greeter.conf` и ввести значение в переменную `position`. Оно принимает значения `x` и `y`, абсолютные (в пикселях) или относительные (в процентах). Каждое значение может иметь дополнительное местоположение для привязки окна, `start`, `center` и `end`. Значения отделяются запятой.

Пример:

```
position=200,start 50%,center

```

## Решение проблем

If you encounter consistent screen flashing and ultimately no LightDM on boot, ensure that you have defined the greeter correctly in LightDM's config file. And if you have correctly defined the GTK greeter, make sure the `xsessions-directory` (default: `/usr/share/xsessions`) exists and contains at least one .desktop file.

The same error can happen on lightdm startup if the last used session is not available anymore (eg. you last used gnome and then removed the gnome-session package): the easiest workaround is to temporarily restore the removed package. Another solution might be:

```
# dbus-send --system --type=method_call --print-reply --dest=org.freedesktop.Accounts /org/freedesktop/Accounts/User1000 org.freedesktop.Accounts.User.SetXSession string:xfce

```

This example sets the session "xfce" as default for the user 1000.

### Локаль неправильно отображается

Если ваша локаль не отображается правильно LightDM, добавьте свой языковой стандарт в `/etc/environment`

```
 LANG=ru_RU.utf8

```

### Ресурсы X не корректно распознаны

LightDM has an [upstream bug](https://bugs.launchpad.net/lightdm/+bug/1084885) where your [Xresources](/index.php/Xresources "Xresources") file will not be loaded with a pre-processor. In practical terms, this means that variables set with `#define` are not expanded when called later. You may see this reflected as an all-pink screen if using a custom color set with urxvt. To fix it, edit `/etc/lightdm/Xsession` and search for the line:

```
xrdb -nocpp -merge "$file"

```

Change it to read:

```
xrdb -merge "$file"

```

Your Xresources will now be pre-processed so that variables are correctly expanded.

### Отсутствуют иконки в Экране приветствия GTK

Если вы используете [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) как Экран приветствия и видите "заполнитель изображений" в виде иконок, убедитесь что действующая тема значков установлена и задействована. Проверьте следующий файл:

 `/etc/lightdm/lightdm-gtk-greeter.conf` 
```
[greeter]
theme-name=mate      # this should be the name of a directory under /usr/share/themes/
icon-theme-name=mate # this should be the name of a fully featured icons set directory under /usr/share/icons/
```

### LightDM зависает при попытке входа в систему

You may find that after entering the correct username and password and attempting to log in, LightDM freezes and you are unable to continue to the desktop. To fix the issue, reinstall the [gdk-pixbuf2](https://www.archlinux.org/packages/?name=gdk-pixbuf2) package. See [this forum thread](https://bbs.archlinux.org/viewtopic.php?id=179031).

### LightDM отображается в неправильном мониторе

Если вы используете несколько мониторов, LightDM может отображаться в неправильном (например, если ваш основной монитор находится справа). Чтобы заставить экран LightDM отображаться на конкретном мониторе, отредактируйте `/etc/lightdm/lightdm.conf` и измените *display-setup-script* параметр, например:

 `/etc/lightdm/lightdm.conf`  `display-setup-script=xrandr --output *HDMI1* --primary` 

Замените *HDMI1* на ваш настоящий ID монитора, который можно найти с помощью результата вывода команды **xrandr**.

### LightDM не отображается

Может случиться так, что ваша система загружается так быстро, что служба LightDM запускается перед загрузкой вашего графического драйвера. Если это ваш случай, добавьте следующие настройки в ваш файл lightdm.conf:

```
   [LightDM]
   logind-check-graphical=true

```

Этот параметр прикажет LightDM ждать, пока графический драйвер не будет готов перед запуском сессии Экранного приветствия/автозапуска.

### Pulseaudio не запускается автоматически

Смотрите [PulseAudio (Русский)#Выполнение](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.92.D1.8B.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5 "PulseAudio (Русский)").

## Смотрите также

*   [light-locker](https://www.archlinux.org/packages/?name=light-locker), a screen locker using LightDM.
*   [Ubuntu Wiki article](https://wiki.ubuntu.com/LightDM)
*   [Gentoo Wiki article](http://wiki.gentoo.org/wiki/LightDM)
*   [Launchpad Page](https://launchpad.net/lightdm)
*   [LightDM blog](http://www.mattfischer.com/blog/?tag=lightdm)