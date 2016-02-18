[Экранный менеджер](https://en.wikipedia.org/wiki/X_display_manager_(program_type) или менеджер входа — графический экран, который отображается в конце процесса загрузки вместо стандартного приглашения командной строки. Экранный менеджер представляет собой экран ввода имени пользователя и пароля для входа в систему. Существует множество экранных менеджеров, также как и окружений рабочего стола. Практически все экранные менеджеры можно конфигурировать, изменяя их стиль и поведение.

## Contents

*   [1 Список экранных менеджеров](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.BE.D0.B2)
    *   [1.1 Консольные](#.D0.9A.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5)
    *   [1.2 Графические](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5)
*   [2 Запуск экранного менеджера](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0)
    *   [2.1 Использование systemd-logind](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_systemd-logind)
*   [3 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.1 Список сеансов](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D1.81.D0.B5.D0.B0.D0.BD.D1.81.D0.BE.D0.B2)
    *   [3.2 Запуск приложений без оконного менеджера](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.D0.B1.D0.B5.D0.B7_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0)
    *   [3.3 Автозапуск](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [4 Известные проблемы](#.D0.98.D0.B7.D0.B2.D0.B5.D1.81.D1.82.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B)
    *   [4.1 Несовместимость с systemd](#.D0.9D.D0.B5.D1.81.D0.BE.D0.B2.D0.BC.D0.B5.D1.81.D1.82.D0.B8.D0.BC.D0.BE.D1.81.D1.82.D1.8C_.D1.81_systemd)

## Список экранных менеджеров

### Консольные

*   **[CDM](/index.php/CDM "CDM")** — ультра-минималистичный, но полностью функциональный менеджер входа, написанный на Bash.

	[https://github.com/ghost1227/cdm](https://github.com/ghost1227/cdm) || [cdm-git](https://aur.archlinux.org/packages/cdm-git/)

*   **[Console TDM](/index.php/Console_TDM "Console TDM")** — расширение для *xinit*, также написанное на Bash.

	[http://code.google.com/p/t-display-manager/](http://code.google.com/p/t-display-manager/) || [console-tdm](https://aur.archlinux.org/packages/console-tdm/)

### Графические

*   **[Entrance](/index.php/Enlightenment "Enlightenment")** — очень экспериментальная реализация, основанная на EFL.

	[http://enlightenment.org/](http://enlightenment.org/) || [entrance-git](https://aur.archlinux.org/packages/entrance-git/)

*   **[GDM](/index.php/GDM "GDM")** — экранный менеджер [GNOME](/index.php/GNOME "GNOME").

	[http://projects.gnome.org/gdm/](http://projects.gnome.org/gdm/) || [gdm](https://www.archlinux.org/packages/?name=gdm)

*   **[KDM](/index.php/KDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDM (Русский)")** — экранный менеджер [KDE](/index.php/KDE "KDE").

	[http://www.kde.org/](http://www.kde.org/) || [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)

*   **[LightDM](/index.php/LightDM "LightDM")** — независимый от среды рабочего стола экранный менеджер, основанный на WebKit.

	[http://www.freedesktop.org/wiki/Software/LightDM](http://www.freedesktop.org/wiki/Software/LightDM) || [lightdm](https://www.archlinux.org/packages/?name=lightdm)

*   **[LXDM](/index.php/LXDM "LXDM")** — экранный менеджер [LXDE](/index.php/LXDE "LXDE"). Может быть использован отдельно от среды рабочего стола LXDE.

	[http://sourceforge.net/projects/lxdm/](http://sourceforge.net/projects/lxdm/) || [lxdm](https://www.archlinux.org/packages/?name=lxdm)

*   **MDM** — экранный менеджер, используемый в Linux Mint, форк GDM 2.

	[https://github.com/linuxmint/mdm](https://github.com/linuxmint/mdm) || [mdm-display-manager](https://aur.archlinux.org/packages/mdm-display-manager/)

*   **[Qingy](/index.php/Qingy "Qingy")** — очень легкий и гибкий в настройке экран входа, не зависящий от [X](https://en.wikipedia.org/wiki/ru:X_Window_System "wikipedia:ru:X Window System") (использует DirectFB).

	[http://qingy.sourceforge.net/](http://qingy.sourceforge.net/) || [qingy](https://aur.archlinux.org/packages/qingy/)

*   **[SDDM](/index.php/SDDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SDDM (Русский)")** — экранный менеджер, основанный на QML.

	[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm](https://www.archlinux.org/packages/?name=sddm), [sddm-git](https://aur.archlinux.org/packages/sddm-git/)

*   **[SLiM](/index.php/SLiM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SLiM (Русский)")** — легкий и элегантный экран входа.

	[http://sourceforge.net/projects/slim.berlios/](http://sourceforge.net/projects/slim.berlios/) || [slim](https://www.archlinux.org/packages/?name=slim)

*   **[XDM](/index.php/XDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "XDM (Русский)")** — экранный менеджер, входящий в проект [X Window System](https://en.wikipedia.org/wiki/ru:X_Window_System "wikipedia:ru:X Window System"); поддерживает XDMCP и имеет возможность выбора хоста.

	[http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html](http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html) || [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)

## Запуск экранного менеджера

Чтобы включить экран входа, запустите демон вашего экранного менеджера (например, KDM):

```
# systemctl enable kdm

```

Это должно работать без дополнительной настройки, и при перезагрузке вы увидите экран входа. Если это не так, вероятно, ссылка *default.target* была изменена вручную:

 `$ ls -l /etc/systemd/system/default.target`  `[...] /etc/systemd/system/default.target -> /usr/lib/systemd/system/graphical.target` 

Просто удалите символическую ссылку, и *systemd* станет использовать стандартный *default.target* (указывающий на *graphical.target*).

```
# rm /etc/systemd/system/default.target

```

После включения службы KDM символическая ссылка *display-manager.service* должна быть установлена в `/etc/systemd/system/`:

 `$ ls -l /etc/systemd/system/display-manager.service`  `[...] /etc/systemd/system/display-manager.service -> /usr/lib/systemd/system/kdm.service` 

### Использование systemd-logind

Чтобы иметь возможность проверить статус вашей сессии, вы можете использовать `loginctl`. Все действия [polkit](/index.php/Polkit "Polkit"), такие как перевод системы в ждущий режим или монтирование внешних устройств будут работать "из коробки".

```
$ loginctl show-session $XDG_SESSION_ID

```

## Советы и рекомендации

### Список сеансов

Большинство экранных менеджеров получают список доступных сеансов из каталога `/usr/share/xsessions/`. Он содержит стандартные [файлы *.desktop*](http://standards.freedesktop.org/desktop-entry-spec/latest/) для каждого экранного/оконного менеджера.

Чтобы добавить (удалить) записи в список сеансов вашего экранного менеджера, создайте (удалите) соответствующий файл *.desktop* в `/usr/share/xsessions/`. Типичный файл *.desktop* выглядит следующим образом:

```
[Desktop Entry]
Encoding=UTF-8
Name=Openbox
Comment=Log in using the Openbox window manager (without a session manager)
Exec=/usr/bin/openbox-session
TryExec=/usr/bin/openbox-session
Icon=openbox.png
Type=XSession

```

### Запуск приложений без оконного менеджера

Вы можете запускать приложения без всяких оконных декораций и рабочего стола. Например, для запуска [google-chrome](https://aur.archlinux.org/packages/google-chrome/) создайте файл `web-browser.desktop` в `/usr/share/xsessions/`:

```
[Desktop Entry]
Encoding=UTF-8
Name=Веб-браузер
Comment=Запуск веб-браузера в качестве сеансового приложения
Exec=/usr/bin/google-chrome --auto-launch-at-startup
TryExec=/usr/bin/google-chrome --auto-launch-at-startup
Icon=google-chrome

```

При этом, сразу после входа будет запущено приложение, указанное в опции `Exec`. Когда вы закроете приложение, вы будете возвращены к экранному менеджеру (точно так же, как если бы вы вышли из среды рабочего стола/оконного менеджера).

Важно помнить, что большинство графических приложений не рассчитаны на запуск в таком режиме и вы можете столкнуться с определенными ограничениями в их работе (например, диалоговые окна будут отображены без рамки и вы не сможете их перемещать по экрану; вы не сможете управлять никаким окном обычным способом — для установки размеров и положения вам, вероятно, придется вносить изменения в файлы настроек приложения).

Смотрите также [xinitrc (Русский)#Запуск приложений без оконного менеджера](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.D0.B1.D0.B5.D0.B7_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0 "Xinitrc (Русский)").

### Автозапуск

Большинство экранных менеджеров запускают скрипты `/etc/xprofile`, `~/.xprofile` и `/etc/X11/xinit/xinitrc.d/` при входе. Для получения подробной информации, см. [xprofile](/index.php/Xprofile_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xprofile (Русский)").

## Известные проблемы

### Несовместимость с systemd

*Это относится к Entrance и MDM.*

Некоторые менеджеры не полностью совместимы с systemd, потому, что они переиспользуют процесс сеанса PAM. Это вызывает разнообразные проблемы при повторном входе, например:

*   апплет NetworkManager перестает работать,
*   уровень громкости в PulseAudio не может быть отрегулирован,
*   невозможно зайди в GNOME под другим пользователем.