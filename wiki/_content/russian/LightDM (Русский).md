**Состояние перевода:** На этой странице представлен перевод статьи [LightDM](/index.php/LightDM "LightDM"). Дата последней синхронизации: 13 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=LightDM&diff=0&oldid=425490).

[LightDM](http://www.freedesktop.org/wiki/Software/LightDM) это кросс-десктопный [[оконный менеджер]. Главные особенности:

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
        *   [5.1.1 GTK+ greeter](#GTK.2B_greeter)
        *   [5.1.2 Unity greeter](#Unity_greeter)
        *   [5.1.3 KDE greeter](#KDE_greeter)
    *   [5.2 Изменение вашего аватара](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2.D0.B0.D1.88.D0.B5.D0.B3.D0.BE_.D0.B0.D0.B2.D0.B0.D1.82.D0.B0.D1.80.D0.B0)
    *   [5.3 Внедрение Arch-ориентированных 64x64 иконок](#.D0.92.D0.BD.D0.B5.D0.B4.D1.80.D0.B5.D0.BD.D0.B8.D0.B5_Arch-.D0.BE.D1.80.D0.B8.D0.B5.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_64x64_.D0.B8.D0.BA.D0.BE.D0.BD.D0.BE.D0.BA)
    *   [5.4 Включение автовхода](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B0.D0.B2.D1.82.D0.BE.D0.B2.D1.85.D0.BE.D0.B4.D0.B0)
    *   [5.5 Включение интерактивного безпарольного входа в систему](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.B0.D0.BA.D1.82.D0.B8.D0.B2.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B1.D0.B5.D0.B7.D0.BF.D0.B0.D1.80.D0.BE.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
    *   [5.6 Скрытие пользователей служб и системы](#.D0.A1.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.B9_.D1.81.D0.BB.D1.83.D0.B6.D0.B1_.D0.B8_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [5.7 Миграция с SLiM](#.D0.9C.D0.B8.D0.B3.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D1.81_SLiM)
    *   [5.8 NumLock включен по умолчанию](#NumLock_.D0.B2.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [5.9 Переключение пользователя при Xfce4](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F_.D0.BF.D1.80.D0.B8_Xfce4)
    *   [5.10 Сессия по умолчанию](#.D0.A1.D0.B5.D1.81.D1.81.D0.B8.D1.8F_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [5.11 Adjusting the login window's position](#Adjusting_the_login_window.27s_position)
        *   [5.11.1 GTK+ greeter](#GTK.2B_greeter_2)
*   [6 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [6.1 Локаль неправильно отображается](#.D0.9B.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C_.D0.BD.D0.B5.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F)
    *   [6.2 Ресурсы X не корректно распознаны](#.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B_X_.D0.BD.D0.B5_.D0.BA.D0.BE.D1.80.D1.80.D0.B5.D0.BA.D1.82.D0.BD.D0.BE_.D1.80.D0.B0.D1.81.D0.BF.D0.BE.D0.B7.D0.BD.D0.B0.D0.BD.D1.8B)
    *   [6.3 Отсутствующие иконки с GTK greeter](#.D0.9E.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.89.D0.B8.D0.B5_.D0.B8.D0.BA.D0.BE.D0.BD.D0.BA.D0.B8_.D1.81_GTK_greeter)
    *   [6.4 LightDM зависает при попытке входа в систему](#LightDM_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.B5.D1.82_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BF.D1.8B.D1.82.D0.BA.D0.B5_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
    *   [6.5 LightDM отображаетсяв неправильном мониторе](#LightDM_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F.D0.B2_.D0.BD.D0.B5.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE.D0.BC_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.B5)
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

Some greeters have their own configuration files. For example, [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) has:

```
/etc/lightdm/lightdm-gtk-greeter.conf

```

and [lightdm-kde-greeter](https://www.archlinux.org/packages/?name=lightdm-kde-greeter) has:

```
/etc/lightdm/lightdm-kde-greeter.conf

```

as well as a section in KDE's System Settings (recommended).

LightDM can be configured by modifying its configuration script, `/etc/lightdm/lightdm.conf`.

### Изменение фонового изображения/цветов

Users wishing to have a flat color (no image) may simply set the `background` variable to a hex color.

Example:

```
background=#000000

```

If you want to use an image instead, see below.

#### GTK+ greeter

You can use the [lightdm-gtk-greeter-settings](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter-settings) gui.

Users wishing to customize the wallpaper on the greeter screen need to edit `/etc/lightdm/lightdm-gtk-greeter.conf` and define the `background` variable under the `[greeter]` section. For example:

 `/etc/lightdm/lightdm-gtk-greeter.conf` 
```
[greeter]
background=/usr/share/pixmaps/black_and_white_photography-wallpaper-1920x1080.jpg
```

**Note:** It is recommended to place the PNG or JPG file in `/usr/share/pixmaps` since the LightDM user needs read access to the wallpaper file.

#### Unity greeter

Users using the [lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/) must edit the `/usr/share/glib-2.0/schemas/com.canonical.unity-greeter.gschema.xml` file and then execute:

```
# glib-compile-schemas /usr/share/glib-2.0/schemas/

```

According to [this](https://bbs.archlinux.org/viewtopic.php?id=149945) page.

#### KDE greeter

Go to *System Settings > Login Screen (LightDM)* and change the background image for your theme.

Alternatively, you can edit the `Background` variable in `lightdm-kde-greeter.conf` :

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

**Совет:** If you are using KDE, you can change your avatar in KDE System Settings.

First, make sure the [accountsservice](https://www.archlinux.org/packages/?name=accountsservice) package from the [official repositories](/index.php/Official_repositories "Official repositories") is installed, then set it up as follows, replacing `*username*` with the desired user's login name. The *.png* file extension should not be included in the filename.

*   Edit or create the file `/var/lib/AccountsService/users/*username*`, and add the lines

```
[User]
Icon=/var/lib/AccountsService/icons/*username*

```

*   Create the file `/var/lib/AccountsService/icons/*username*` using a 96x96 PNG image file.

**Примечание:** Make sure that both created files have 644 permissions, use [chmod](/index.php/Chmod "Chmod") to correct them.

### Внедрение Arch-ориентированных 64x64 иконок

The [archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/) package from the [AUR](/index.php/AUR "AUR") contains some nice examples that install to `/usr/share/archlinux/icons` and that can be copied to `/usr/share/icons/hicolor/64x64/devices` as follows:

```
# find /usr/share/archlinux/icons -name "*64*" -exec cp {} /usr/share/icons/hicolor/64x64/devices \;

```

After copying, the [archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/) package can be removed.

### Включение автовхода

Edit the LightDM configuration file and ensure these lines are uncommented and correctly configured:

 `/etc/lightdm/lightdm.conf` 
```
[Seat:*]
pam-service=lightdm
pam-autologin-service=lightdm-autologin
autologin-user=*username*
autologin-user-timeout=0
session-wrapper=/etc/lightdm/Xsession
```

LightDM goes through PAM even when `autologin` is enabled. You must be part of the `autologin` group to be able to login automatically without entering your password:

```
# groupadd -r autologin
# gpasswd -a *username* autologin

```

**Примечание:** GNOME users, and by extension any gnome-keyring user will have to set up a blank password to their keyring for it to be unlocked automatically.

### Включение интерактивного безпарольного входа в систему

LightDM goes through PAM so you must configure the lightdm configuration of PAM:

 `/etc/pam.d/lightdm` 
```
#%PAM-1.0
**auth        sufficient  pam_succeed_if.so user ingroup nopasswdlogin**
auth        include     system-login
...
```

You must then also be part of the `nopasswdlogin` group to be able to login interactively without entering your password:

```
# groupadd -r nopasswdlogin
# gpasswd -a *username* nopasswdlogin

```

**Примечание:** GNOME users, and by extension any gnome-keyring user may have to follow the instructions at the end of the previous section on enabling autologin.

To create a new user account that logs in automatically and additionally able to login again without a password the user can be created with supplementary membership of both groups, e.g.:

```
# useradd -mG autologin,nopasswdlogin -s /bin/bash *username*

```

### Скрытие пользователей служб и системы

To prevent system users from showing-up in the login, install the optional dependency [accountsservice](https://www.archlinux.org/packages/?name=accountsservice), or add the user names to `/etc/lightdm/users.conf` under `hidden-users`. The first option has the advantage of not needing to update the list when more users are added or removed.

### Миграция с SLiM

Move the contents of [xinitrc](/index.php/Xinitrc "Xinitrc") to [xprofile](/index.php/Xprofile "Xprofile"), removing the call to start the [window manager](/index.php/Window_manager "Window manager") or [desktop environment](/index.php/Desktop_environment "Desktop environment").

### NumLock включен по умолчанию

Install the [numlockx](https://www.archlinux.org/packages/?name=numlockx) package and the edit `/etc/lightdm/lightdm.conf` adding the following line:

```
greeter-setup-script=/usr/bin/numlockx on

```

### Переключение пользователя при Xfce4

If you use the [Xfce](/index.php/Xfce "Xfce") desktop, the Switch User functionality of the Action Button found in your Application Launcher specifically looks for the *gdmflexiserver* executable in order to enable itself. If you provide it with an executable shell script `/usr/bin/gdmflexiserver` consisting of

```
#!/bin/sh
/usr/bin/dm-tool switch-to-greeter

```

then user switching in Xfce should work with Lightdm.

Alternatively, if you use the Whisker Menu, you can go to Properties -> Commands and change the "Switch Users" command directly to:

```
 dm-tool switch-to-greeter

```

You can also switch users from the [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") lock screen - see [XScreenSaver#LightDM](/index.php/XScreenSaver#LightDM "XScreenSaver").

### Сессия по умолчанию

Lightdm, like other DMs, stores the last-selected xsession in `~/.dmrc`. See [Display manager#Session list](/index.php/Display_manager#Session_list "Display manager") for more info.

### Adjusting the login window's position

#### GTK+ greeter

Users need to edit `/etc/lightdm/lightdm-gtk-greeter.conf` and enter a value for the `position` variable. It accepts `x` and `y` values, either absolute (in pixels) or relative (in percent). Each value can also have an additional anchor location for the window, `start`, `center` and `end` separated from the value by a comma.

Example:

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

In case of your locale not being displayed correctly in Lightdm add your locale to `/etc/environment`

```
 LANG=pt_PT.utf8

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

### Отсутствующие иконки с GTK greeter

If you're using [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) as a greeter and it shows placeholder images as icons, make sure valid icon themes and themes are installed and configured. Check the following file:

 `/etc/lightdm/lightdm-gtk-greeter.conf` 
```
[greeter]
theme-name=mate      # this should be the name of a directory under /usr/share/themes/
icon-theme-name=mate # this should be the name of a fully featured icons set directory under /usr/share/icons/
```

### LightDM зависает при попытке входа в систему

You may find that after entering the correct username and password and attempting to log in, LightDM freezes and you are unable to continue to the desktop. To fix the issue, reinstall the [gdk-pixbuf2](https://www.archlinux.org/packages/?name=gdk-pixbuf2) package. See [this forum thread](https://bbs.archlinux.org/viewtopic.php?id=179031).

### LightDM отображаетсяв неправильном мониторе

If you are using multiple monitors, LightDM may display in the wrong one (e.g. if your primary monitor is on the right). To force the LightDM login screen to display on a specific monitor, edit `/etc/lightdm/lightdm.conf` and change the *display-setup-script* parameter like this:

 `/etc/lightdm/lightdm.conf`  `display-setup-script=xrandr --output *HDMI1* --primary` 

Replace *HDMI1* with your real monitor ID, which you can find from **xrandr** command output.

### LightDM не отображается

It may happen that your system boots so fast that LightDM service is started before your graphics drivers are properly loaded. If this is your case, you'll want to add the following config to your lightdm.conf file:

```
   [LightDM]
   logind-check-graphical=true

```

This setting will tell LightDM to wait until graphics devices are ready before spawning greeters/autostarting sessions on them.

### Pulseaudio не запускается автоматически

Смотрите [PulseAudio (Русский)#Выполнение](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.92.D1.8B.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5 "PulseAudio (Русский)").

## Смотрите также

*   [light-locker](https://www.archlinux.org/packages/?name=light-locker), a screen locker using LightDM.
*   [Ubuntu Wiki article](https://wiki.ubuntu.com/LightDM)
*   [Gentoo Wiki article](http://wiki.gentoo.org/wiki/LightDM)
*   [Launchpad Page](https://launchpad.net/lightdm)
*   [LightDM blog](http://www.mattfischer.com/blog/?tag=lightdm)