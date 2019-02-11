Ссылки по теме

*   [Среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола")
*   [Оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер")
*   [Запуск X при входе](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D0%BA_X_%D0%BF%D1%80%D0%B8_%D0%B2%D1%85%D0%BE%D0%B4%D0%B5 "Запуск X при входе")

[Экранный менеджер](https://en.wikipedia.org/wiki/X_display_manager_(program_type) или менеджер входа — графический экран, который отображается в конце процесса загрузки вместо стандартного приглашения командной строки. Экранный менеджер представляет собой экран ввода имени пользователя и пароля для входа в систему. Существует множество экранных менеджеров, как и окружений рабочего стола. Практически все экранные менеджеры можно настраивать, изменяя их стиль и поведение.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Список экранных менеджеров](#Список_экранных_менеджеров)
    *   [1.1 Консольные](#Консольные)
    *   [1.2 Графические](#Графические)
*   [2 Запуск экранного менеджера](#Запуск_экранного_менеджера)
*   [3 Использование systemd-logind](#Использование_systemd-logind)
*   [4 Настройка сеанса](#Настройка_сеанса)
*   [5 Использование ~/.xinitrc как сеанс](#Использование_~/.xinitrc_как_сеанс)
*   [6 Запуск приложений без оконного менеджера](#Запуск_приложений_без_оконного_менеджера)
*   [7 Автозапуск](#Автозапуск)
*   [8 Установка языка](#Установка_языка)

## Список экранных менеджеров

### Консольные

*   **[CDM](/index.php/CDM "CDM")** — ультра-минималистичный, но полностью функциональный менеджер входа, написанный на Bash.

	[https://github.com/ghost1227/cdm](https://github.com/ghost1227/cdm) || [cdm-git](https://aur.archlinux.org/packages/cdm-git/)

*   **[Console TDM](/index.php/Console_TDM "Console TDM")** — расширение для xinit, также написанное на Bash.

	[https://github.com/dopsi/console-tdm](https://github.com/dopsi/console-tdm) || [console-tdm](https://aur.archlinux.org/packages/console-tdm/)

*   **[Nodm](/index.php/Nodm "Nodm")** — минималистичный экранный менеджер для автоматического входа.

	[https://github.com/spanezz/nodm](https://github.com/spanezz/nodm) || [nodm](https://www.archlinux.org/packages/?name=nodm)

*   **[Ly](/index.php/Ly "Ly")** — экспериментальный менеджер входа.

	[https://github.com/cylgom/ly](https://github.com/cylgom/ly) || [ly-git](https://aur.archlinux.org/packages/ly-git/)

### Графические

*   **[GDM](/index.php/GDM "GDM")** — экранный менеджер [GNOME](/index.php/GNOME "GNOME").

	[https://wiki.gnome.org/Projects/GDM](https://wiki.gnome.org/Projects/GDM) || [gdm](https://www.archlinux.org/packages/?name=gdm)

*   **[LightDM](/index.php/LightDM "LightDM")** — независимый от среды рабочего стола экранный менеджер, основанный на WebKit.

	[https://www.freedesktop.org/wiki/Software/LightDM/](https://www.freedesktop.org/wiki/Software/LightDM/) || [lightdm](https://www.archlinux.org/packages/?name=lightdm)

*   **[LXDM](/index.php/LXDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LXDM (Русский)")** — экранный менеджер [LXDE](/index.php/LXDE "LXDE"). Может быть использован отдельно от среды рабочего стола LXDE.

	[https://sourceforge.net/projects/lxdm/](https://sourceforge.net/projects/lxdm/) || [lxdm](https://www.archlinux.org/packages/?name=lxdm)

*   **[SDDM](/index.php/SDDM "SDDM")** — экранный менеджер, основанный на QML. Продолжение KDE4 kdm, рекомендуется для [Plasma 5](/index.php/KDE "KDE") и [LXQt](/index.php/LXQt "LXQt").

	[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm](https://www.archlinux.org/packages/?name=sddm)

*   **[XDM](/index.php/XDM "XDM")** — экранный менеджер с поддержкой XDMCP.

	[xdm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdm.8) || [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)

## Запуск экранного менеджера

Чтобы включить экран входа, [запустите](/index.php/Enable "Enable") соответствующую службу. Например для [SDDM](/index.php/SDDM "SDDM") включите `sddm.service`. Это должно работать без дополнительных настроек. Если нет, возможно, вам придется удалить символическую ссылку `default.target`, чтобы указать на `graphical.target` файл по умолчанию. После включения [SDDM](/index.php/SDDM "SDDM") в `/etc/systemd/system/` должен быть установлен symlink `display-manager.service`. Возможно, вам придется использовать `--force` для переопределения старых символических ссылок.

 `$ file /etc/systemd/system/display-manager.service` 
```
/etc/systemd/system/display-manager.service: symbolic link to /usr/lib/systemd/system/sddm.service

```

## Использование systemd-logind

Чтобы иметь возможность проверить статус вашей сессии, вы можете использовать loginctl. Все действия [polkit](/index.php/Polkit "Polkit"), такие, как перевод системы в ждущий режим или монтирование внешних устройств будут работать "из коробки".

```
$ loginctl show-session $XDG_SESSION_ID

```

## Настройка сеанса

Большинство экранных менеджеров получают список доступных сеансов из каталога `/usr/share/xsessions/`. Он содержит стандартные [файлы *.desktop*](http://standards.freedesktop.org/desktop-entry-spec/latest/) для каждого экранного/оконного менеджера. Чтобы добавить/удалить записи в список сеансов вашего экранного менеджера, создайте/удалите соответствующий файл .desktop в `/usr/share/xsessions/`. Типичный файл .desktop выглядит примерно так:

```
[Desktop Entry]
Name=Openbox
Comment=Log in using the Openbox window manager (without a session manager)
Exec=/usr/bin/openbox-session
TryExec=/usr/bin/openbox-session
Icon=openbox.png
Type=Application

```

## Использование ~/.xinitrc как сеанс

Установите [xinit-xsession](https://aur.archlinux.org/packages/xinit-xsession/) для запуска [xinitrc](/index.php/Xinitrc "Xinitrc") в качестве сеанса. Просто установите `xinitrc` в качестве сеанса в настройках вашего экранного менеджера и убедитесь, что файл `~/.xinitrc` является исполняемым.

## Запуск приложений без оконного менеджера

Вы также можете запускать приложения без какого-либо оформления. Например, для запуска [google-chrome](https://aur.archlinux.org/packages/google-chrome/) создайте файл `web-browser.desktop` в `/usr/share/xsessions/` :

```
[Desktop Entry]
Name=Web Browser
Comment=Use a web browser as your session
Exec=/usr/bin/google-chrome --auto-launch-at-startup
TryExec=/usr/bin/google-chrome --auto-launch-at-startup
Icon=google-chrome
Type=Application

```

При этом, сразу после входа будет запущено приложение, указанное в опции `Exec`. Когда вы закроете приложение, вы будете возвращены к экранному менеджеру (точно так же, как если бы вы вышли из среды рабочего стола/оконного менеджера).

Важно помнить, что большинство графических приложений не рассчитаны на запуск в таком режиме и вы можете столкнуться с определенными ограничениями в их работе (например, диалоговые окна будут отображены без рамки и вы не сможете их перемещать по экрану; вы не сможете управлять никаким окном обычным способом — для установки размеров и положения вам, вероятно, придется вносить изменения в файлы настроек приложения).

Смотрите также [xinitrc (Русский)#Запуск приложений без оконного менеджера](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Запуск_приложений_без_оконного_менеджера "Xinitrc (Русский)").

## Автозапуск

Большинство экранных менеджеров используют `/etc/xprofile`, `~/.xprofile` и `/etc/X11/xinit/xinitrc.d/` при входе. Для получения подробной информации, см. [xprofile](/index.php/Xprofile_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xprofile (Русский)").

## Установка языка

Для экранных менеджеров, которые используют [AccountsService](http://freedesktop.org/wiki/Software/AccountsService/), [язык](/index.php/Locale_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Locale (Русский)") для пользовательского сеанса может быть установлен путем редактирования:

 `/var/lib/AccountsService/users/$USER` 
```
[User]
Language=*your_locale*
```

Выйдите из системы, а затем снова войдите, чтобы изменения вступили в силу.