**Состояние перевода:** На этой странице представлен перевод статьи [LXQt](/index.php/LXQt "LXQt"). Дата последней синхронизации: 12 августа 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=LXQt&diff=0&oldid=484396).

В начале 2013 года Hong Jen Yee "PCMan" приступил к портированию компонентов [LXDE](/index.php/LXDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LXDE (Русский)") на [Qt](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)"). Первую [превью-версию LXDE-Qt](http://blog.lxde.org/?p=1013) показали 3 июля 2013 года, а 21 июля было анонсировано слияние Razor-qt (схожего с LXDE по внешнему виду) и LXDE.

В результате [LXQt](http://lxqt.org) основан на Qt и частично использует компоненты Razor-qt и LXDE. Хотя разработка и сосредоточена на LXQt, работа над GTK-версией LXDE будет продолжаться.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Запуск окружения](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [2.1 С использованием xinit](#.D0.A1_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC_xinit)
    *   [2.2 Графический вход](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B2.D1.85.D0.BE.D0.B4)
*   [3 Настройки](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)
    *   [3.1 Замена Openbox](#.D0.97.D0.B0.D0.BC.D0.B5.D0.BD.D0.B0_Openbox)
    *   [3.2 Автозапуск приложений](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [3.3 Настройка переменных окружения](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BF.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [3.4 Редактирование меню приложений](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
*   [4 Устранение проблем](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Иконки рабочего стола группируются](#.D0.98.D0.BA.D0.BE.D0.BD.D0.BA.D0.B8_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0_.D0.B3.D1.80.D1.83.D0.BF.D0.BF.D0.B8.D1.80.D1.83.D1.8E.D1.82.D1.81.D1.8F)
*   [5 Советы и хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.85.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [5.1 Настройка меню "Выйти"](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BC.D0.B5.D0.BD.D1.8E_.22.D0.92.D1.8B.D0.B9.D1.82.D0.B8.22)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") группу пакетов [lxqt](https://www.archlinux.org/groups/x86_64/lxqt/) и тему иконок (например, [breeze-icons](https://www.archlinux.org/packages/?name=breeze-icons) или [oxygen-icons](https://www.archlinux.org/packages/?name=oxygen-icons)).

Для дополнительных функций, возможно, пригодится установить:

*   **LXQt Connman applet** — LXQt-апплет для [ConnMan](/index.php/ConnMan "ConnMan").

	[https://github.com/surlykke/lxqt-connman-applet](https://github.com/surlykke/lxqt-connman-applet) || [lxqt-connman-applet-git](https://aur.archlinux.org/packages/lxqt-connman-applet-git/)

*   **[SDDM](/index.php/SDDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SDDM (Русский)")** — Рекомендуемый дисплейный менеджер для LXQt.

	[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm](https://www.archlinux.org/packages/?name=sddm)

*   Блокировщик экрана, при необходимости. К примеру, [slock](/index.php/Slock "Slock") или [XScreenSaver](/index.php/XScreenSaver "XScreenSaver"). Оба они поддерживают LXQt, остальные, возможно, тоже. Отключение блокировки экрана в ждущем или спящем режиме можно найти в "настройках LXQt/Настройках сеанса/Основной сеанс/Завершение сеанса".

**Совет:** LXQt использует *xdg-screensaver* из [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) для блокировки экрана, который работает только с XScreenSaver и [xautolock](https://www.archlinux.org/packages/?name=xautolock). Вы можете использовать их или любой другой совместимый блокировщик. К примеру, в случае с *slock* воспользуйтесь инструкцией [Slock#Lock on suspend](/index.php/Slock#Lock_on_suspend "Slock") или пропатченным пакетом [xdg-utils-slock](https://aur.archlinux.org/packages/xdg-utils-slock/) для совместимости с LXQt

*   Некоторые плагины панели LXQt для работы требуют дополнительные пакеты. Обратитесь к [дополнительным зависимостям](/index.php/PKGBUILD#optdepends "PKGBUILD") пакета [lxqt-panel](https://www.archlinux.org/packages/?name=lxqt-panel).

## Запуск окружения

### С использованием xinit

Добавьте к [Xinitrc](/index.php/Xinitrc "Xinitrc") строчку:

```
exec startlxqt

```

### Графический вход

Выберите *LXQt Desktop* из меню вашего [менеджера входа](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)").

## Настройки

Для управления собственными настройками LXQt стремится предоставить графический интерфейс. Файлы конфигурации располагаются в `~/.config/lxqt`, папка создается автоматически. Конфигурация по умолчанию для новых пользователей находится в `/etc/xdg/lxqt`.

### Замена Openbox

Хотя [Openbox](/index.php/Openbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Openbox (Русский)") установлен [оконным менеджером](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)") для LXQt по умолчанию, вы можете использовать и другой. Для этого в меню "Настройки LXQt/Настройки сеанса" (`lxqt-config-session`) выберите нужный или же отредактируйте в файле `~/.config/lxqt/session.conf` строчку:

```
window_manager=openbox

```

для установки вашего [оконного менеджера](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)"):

```
window_manager=*your_window_manager*

```

### Автозапуск приложений

Для управления автозапуском графических приложений выберите в меню "Настройки LXQt" -> Настройки сессии -> Автозапуск . Также меню может быть вызвано при помощи:

```
lxqt-config-session

```

Здесь можно добавить приложения для глобального автозапуска (во всех сессиях, "Общий автозапуск" в настройках) или для вашего личного автозапуска ("Автозапуск только для LXQt") (Обратите внимание на [связанную с этим проблему 746](https://github.com/lxde/lxqt/issues/746)).

Для каждого добавленного элемента `lxqt-config-session` создается .desktop-файл в папке `~/.config/autostart`. Предустановленные приложения, автоматически запускаемые при входе, можно найти в `/etc/xdg/autostart`. Управлять автозапуском можно через редактирование файлов в этих папках. Кроме того, попадание в категорию "Общий автозапуск" и "Автозапуск только для LXQt" не зависит от расположения .desktop-файла, а используется опция `OnlyShowIn`. Если установлено `OnlyShowIn=true`, пункт относится к "Автозапуск только для LXQt". Если же значение установлено `X-LXQt-Module=true`, пункт вообще не отображается в `lxqt-config-session`.

### Настройка переменных окружения

[Переменные окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") для LXQt также устанавливаются в "Настройках сессии", на вкладке "Окружение".

### Редактирование меню приложений

Редактировать меню приложений можно при помощи изменения файлов *.desktop*, расположенных в `/usr/share/applications/lxqt-*.desktop`. Подробности - [ярлыки приложений](/index.php/Desktop_entries_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop entries (Русский)").

## Устранение проблем

### Иконки рабочего стола группируются

При перемещении иконок на рабочем столе их можно расположить настолько близко, что они соединятся друг с другом. Если разделить их не получается, остановите "Рабочий стол" в настройках сессии LXQt, удалите `.config/pcmanfm-qt/lxqt/desktop-items-0.conf` и снова запустите "Рабочий стол".

## Советы и хитрости

### Настройка меню "Выйти"

Настроить меню "Выйти" можно простым копированием соответствующего файла .desktop в `~/.local/share/applications` и изменением параметра на *NoDisplay=true*. Подробнее: [#876](https://github.com/lxde/lxqt/issues/876).

Полный список файлов, которые можно скрыть:

```
lxqt-hibernate.desktop
lxqt-leave.desktop
lxqt-lockscreen.desktop
lxqt-logout.desktop
lxqt-reboot.desktop
lxqt-shutdown.desktop
lxqt-suspend.desktop

```

Пример: удаление спящего режима.

```
$ mkdir -p ~/.local/share/applications
$ sed '/OnlyShowIn/aNoDisplay=true' </usr/share/applications/lxqt-hibernate.desktop >~/.local/share/applications/lxqt-hibernate.desktop

```

## Смотрите также

*   [LXQt homepage](http://lxqt.org)
*   [LXQt development](https://github.com/lxde/lxqt)
*   [LXQt on deviantART](http://lxqt-de.deviantart.com/)
*   [LXQt wiki on GitHub](https://github.com/lxde/lxqt/wiki)