Ссылки по теме

*   [GTK+ (Русский)](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK+ (Русский)")
*   [GDM](/index.php/GDM "GDM")
*   [GNOME/Tips and tricks](/index.php/GNOME/Tips_and_tricks "GNOME/Tips and tricks")
*   [GNOME/Troubleshooting](/index.php/GNOME/Troubleshooting "GNOME/Troubleshooting")
*   [GNOME/Files](/index.php/GNOME/Files "GNOME/Files")
*   [GNOME/Gedit](/index.php/GNOME/Gedit "GNOME/Gedit")
*   [GNOME/Web](/index.php/GNOME/Web "GNOME/Web")
*   [GNOME/Evolution](/index.php/GNOME/Evolution "GNOME/Evolution")
*   [GNOME/Flashback](/index.php/GNOME/Flashback "GNOME/Flashback")
*   [GNOME/Keyring](/index.php/GNOME/Keyring "GNOME/Keyring")
*   [GNOME/Document viewer](/index.php/GNOME/Document_viewer "GNOME/Document viewer")
*   [Официальные репозитории#gnome-unstable](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B8#gnome-unstable "Официальные репозитории")

**Состояние перевода:** На этой странице представлен перевод статьи [GNOME](/index.php/GNOME "GNOME"). Дата последней синхронизации: 28 марта 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=GNOME&diff=0&oldid=569299).

[GNOME](https://en.wikipedia.org/wiki/ru:GNOME "wikipedia:ru:GNOME") (произностися как /(ɡ)noʊm/) - это [окружение рабочего стола](/index.php/%D0%9E%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Окружение рабочего стола"), которое стремится быть простым и легким в использовании. Оно разработано в рамках [Проекта GNOME](https://en.wikipedia.org/wiki/ru:%D0%9F%D1%80%D0%BE%D0%B5%D0%BA%D1%82_GNOME "wikipedia:ru:Проект GNOME") и состоит полностью из свободного и открытого программного обеспечения. Является частью [Проекта GNU](https://en.wikipedia.org/wiki/ru:%D0%9F%D1%80%D0%BE%D0%B5%D0%BA%D1%82_GNU "wikipedia:ru:Проект GNU"). По умолчанию использует [Wayland](/index.php/Wayland_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wayland (Русский)"), а не [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Сессии GNOME](#Сессии_GNOME)
*   [3 Запуск GNOME](#Запуск_GNOME)
    *   [3.1 Графически](#Графически)
    *   [3.2 Вручную](#Вручную)
        *   [3.2.1 Сессия Xorg](#Сессия_Xorg)
        *   [3.2.2 Сессия Wayland](#Сессия_Wayland)
    *   [3.3 Приложения GNOME в Wayland](#Приложения_GNOME_в_Wayland)
*   [4 Навигация](#Навигация)
*   [5 Устаревшие названия](#Устаревшие_названия)
*   [6 Конфигурация](#Конфигурация)
    *   [6.1 Настройки системы](#Настройки_системы)
        *   [6.1.1 Цвет](#Цвет)
        *   [6.1.2 Night Light](#Night_Light)
        *   [6.1.3 Дата & время](#Дата_&_время)
        *   [6.1.4 Приложения по умолчанию](#Приложения_по_умолчанию)
        *   [6.1.5 Мышь и сенсорная панель](#Мышь_и_сенсорная_панель)
        *   [6.1.6 Сеть](#Сеть)
        *   [6.1.7 Сетевые учетные записи](#Сетевые_учетные_записи)
        *   [6.1.8 Поиск](#Поиск)
    *   [6.2 Расширенная конфигурация](#Расширенная_конфигурация)
        *   [6.2.1 Внешний вид](#Внешний_вид)
            *   [6.2.1.1 Темы](#Темы)
            *   [6.2.1.2 Высота заголовка](#Высота_заголовка)
            *   [6.2.1.3 Порядок кнопок в заголовке](#Порядок_кнопок_в_заголовке)
            *   [6.2.1.4 Скрыть заголовок, когда окно во весь экран](#Скрыть_заголовок,_когда_окно_во_весь_экран)
            *   [6.2.1.5 Темы GNOME Shell](#Темы_GNOME_Shell)
            *   [6.2.1.6 Иконки в меню](#Иконки_в_меню)
        *   [6.2.2 Каталоги в меню приложений](#Каталоги_в_меню_приложений)
        *   [6.2.3 Автозапуск приложений при входе в систему](#Автозапуск_приложений_при_входе_в_систему)
        *   [6.2.4 Рабочий стол](#Рабочий_стол)
            *   [6.2.4.1 Иконки на рабочем столе](#Иконки_на_рабочем_столе)
            *   [6.2.4.2 Фон экрана блокировки и рабочего стола](#Фон_экрана_блокировки_и_рабочего_стола)
            *   [6.2.4.3 Отключение перехода в режим навигации при перемещении мыши в левый верхний угол](#Отключение_перехода_в_режим_навигации_при_перемещении_мыши_в_левый_верхний_угол)
        *   [6.2.5 Расширения](#Расширения)
        *   [6.2.6 Шрифты](#Шрифты)
        *   [6.2.7 Методы ввода](#Методы_ввода)
        *   [6.2.8 Электропитание](#Электропитание)
            *   [6.2.8.1 Отключение входа в спящий режим при закрытии крышки ноутбука](#Отключение_входа_в_спящий_режим_при_закрытии_крышки_ноутбука)
            *   [6.2.8.2 Изменить поведение при критическом уровне заряда батареи](#Изменить_поведение_при_критическом_уровне_заряда_батареи)
    *   [6.3 Использование стороннего оконного менеджера](#Использование_стороннего_оконного_менеджера)
*   [7 Смотрите также](#Смотрите_также)

## Установка

Доступны две группы:

*   [gnome](https://www.archlinux.org/groups/x86_64/gnome/) содержит основное рабочее окружение и набор хорошо интегрированных [приложений](https://wiki.gnome.org/Apps);
*   [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/) включает в себя дополнительные приложения GNOME, такие как архиватор, диспетчер дисков, [текстовый редактор](/index.php/Gedit "Gedit") и набор игр. Обратите внимание, что эта группа опирается на [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

Базовый рабочий стол состоит из GNOME Shell, плагина для оконного менеджера [Mutter](https://en.wikipedia.org/wiki/ru:Mutter_(%D0%BE%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80) "wikipedia:ru:Mutter (оконный менеджер)"). Он может быть установлен отдельным пакетом - [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell)

**Примечание:** *mutter* выступает в роли композитного менеджера, который использует аппаратное ускорение для предоставления эффектов. Менеджер сеансов GNOME автоматически определяет, может ли ваша система работать с GNOME Shell, и, если нет, возвращается к использованию рендеринга с использованием *llvmpipe*.

## Сессии GNOME

Доступно три сессии.

*   **GNOME** - сеанс по умолчанию; запускает GNOME Shell, используя протокол Wayland, а также привычные приложения X посредством Xwayland
*   **GNOME Classic** - традиционный рабочий стол, похожий на пользовательский интерфейс GNOME 2, но использующий технологии GNOME 3\. Это достигается за счет использования предустановленных расширений и настроек (смотрите [здесь](http://worldofgnome.org/welcome-to-gnome-3-8-flintstones-mode/), чтобы увидеть список). Следовательно, это более "настроенный", чем первый, режим GNOME Shell
*   **GNOME on Xorg** - запускает GNOME Shell, используя Xorg

## Запуск GNOME

GNOME может быть запущен как графически, используя [экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер"), так и вручную из консоли. При запуске из консоли некоторые возможности могут быть ограничены.

**Примечание:** Поддержка механизмов блокировки экрана в GNOME обеспечивается GDM. Если запускать GNOME не при помощи GDM, то вам придется использовать другой блокировщик экрана. Смотрите [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security").

### Графически

В меню экранного менеджера выберите сессию *GNOME*, *GNOME Classic* или *GNOME on Xorg*.

### Вручную

#### Сессия Xorg

*   Для запуска сессии GNOME on Xorg добавьте следующее в файл `~/.xinitrc` (смотрите [здесь](https://gitlab.gnome.org/GNOME/gtk/issues/1390#note_344758) для подробностей):
    ```
    export GDK_BACKEND=x11
    exec gnome-session
    ```
    .
*   Для запуска сессии GNOME Classic добавьте следующее в файл `~/.xinitrc`:
    ```
    export XDG_CURRENT_DESKTOP=GNOME-Classic:GNOME
    export GNOME_SHELL_SESSION_MODE=classic
    exec gnome-session --session=gnome-classic
    ```

После редактирования файла `~/.xinitrc` можно запустить GNOME при помощи команды `startx` (для получения информации о других возможностях, например сохранении сессии logind, смотрите статью [xinitrc](/index.php/Xinitrc "Xinitrc")). После настройки `~/.xinitrc` можете использовать инструкции из статьи [Запуск Х при входе в систему](/index.php/Start_X_at_login_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Start X at login (Русский)").

#### Сессия Wayland

**Примечание:**

*   Пакет [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) все еще нужен даже для запуска тех приложений, которые не портированы на [Wayland](/index.php/Wayland_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wayland (Русский)").
*   Wayland с проприетарным драйвером [NVIDIA](/index.php/NVIDIA "NVIDIA") на данный момент имеет плохую производительность: [FS#53284](https://bugs.archlinux.org/task/53284).

Вручную можно запустить следующей командой: `QT_QPA_PLATFORM=wayland XDG_SESSION_TYPE=wayland dbus-run-session gnome-session`. QT_QPA_PLATFORM заставляет приложения, написанные на [Qt (Русский)](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)"), например, [VLC](/index.php/VLC "VLC"), calibre и SMPlayer, использовать Wayland.

Чтобы запускать сессию GNOME при входе в систему, добавьте следующее в `.bash_profile`:

```
if [[ -z $DISPLAY ]] && [[ $(tty) = /dev/tty1 ]] && [[ -z $XDG_SESSION_TYPE ]]; then
  QT_QPA_PLATFORM=wayland XDG_SESSION_TYPE=wayland exec dbus-run-session gnome-session
fi

```

Если это не работает, попробуйте изменить `[[ -z $XDG_SESSION_TYPE ]]` на `[[ $XDG_SESSION_TYPE = tty ]]`.

### Приложения GNOME в Wayland

Когда используется сессия *GNOME*, соответствующие приложения будут запущены, используя Wayland. Для отладки смотрите [руководство GTK+](https://developer.gnome.org/gtk3/stable/gtk-running.html), в нем перечислены параметры и переменные окружения.

## Навигация

Чтобы понять, как использовать GNOME эффективно, прочитайте [шпаргалку GNOME Shell](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet); в ней освещаются особенности, включающие в себя переключение между задачами, использование клавиатуры, управление окнами, панель, режим обзора, GNOME shell и горячие клавиши. Вот некоторые из них:

*   `Super` + `m`: показать трей с сообщениями
*   `Super` + `a`: показать меню приложений
*   `Alt` + `Tab`: переключение между активными приложениями
*   `Alt` + ``` (клавиша выше `Tab` на раскладке клавиатуры США): переключение между окнами активного приложения
*   `Alt` + `F2`, затем введите `r` или `restart`: перезапуск оболочки ввиду графических проблем (только для режима X/legacy. Не доступно для Wayland).

## Устаревшие названия

**Примечание:** Имя некоторых приложений GNOME в документации, диалоговых окнах изменилось, но исполняемый файл остался тот же. Несколько таких приложений перечислено в таблице ниже.

**Совет:** Поиск по старому названию успешно найдет требуемое приложение. Например, если искать *nautilus*, то выдаст *Files*.

| Текущее | Старое |
| [Files](/index.php/GNOME/Files "GNOME/Files") | Nautilus |
| [Web](/index.php/GNOME/Web "GNOME/Web") | Epiphany |
| Videos | Totem |
| Main Menu | Alacarte |
| [Document Viewer](/index.php/GNOME/Document_viewer "GNOME/Document viewer") | Evince |
| Disk Usage Analyzer | Baobab |
| Image Viewer | EoG (Eye of GNOME) |
| [Passwords and Keys](/index.php/GNOME/Keyring "GNOME/Keyring") | Seahorse |
| GNOME Translation Editor | Gtranslator |

## Конфигурация

Панель управления GNOME (gnome-control-center) и приложения GNOME используют низкоуровневую систему конфигурации [dconf](https://en.wikipedia.org/wiki/Dconf "wikipedia:Dconf") для хранения своих настроек.

С помощью утилит `gsettings` и `dconf` вы можете напрямую получить доступ к базе данных dconf. Этот метод также позволяет настраивать параметры не предоставляемые графическим интерфейсом.

До версии GNOME 3.24 все настройки применялись с помощью сервиса GNOME settings, который может быть запущен вне сессии GNOME следующим образом:

```
$ nohup /usr/lib/gnome-settings-daemon/gnome-settings-daemon > /dev/null &

```

Однако в GNOME 3.24 сервис GNOME settings был заменён несколькими отдельными плагинами настроек: `/usr/lib/gnome-settings-daemon/gsd-*`. Эти плагины теперь контролируются через `.desktop` файлы, которые находятся в каталоге `/etc/xdg/autostart` (org.gnome.SettingsDaemon.*.desktop). Для того, чтобы запустить эти плагины вне сессии GNOME вам необходимо скопировать соответствующие [ярлыки приложений](/index.php/Desktop_entries_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop entries (Русский)") в каталог `~/.config/autostart`.

Конфигурация обычно производится отдельно для каждого пользователя и остальная часть этого раздела не приводит примеры того, как создать конфигурацию для нескольких пользователей одновременно.

### Настройки системы

#### Цвет

Демон (служба) `colord` считывает данные EDID дисплея и извлекает соответствующий цветовой профиль. Большинство цветовых профилей являются правильными и не требуют настройки; однако для тех, которые не являются правильными или для старых дисплеев, цветовые профили могут быть помещены в `~/.local/share/icc/` и направлены туда же.

#### Night Light

GNOME поставляется со встроенным световым фильтром, который похож на [Redshift](/index.php/Redshift "Redshift"). Его можно включить в меню настроек в разделе Дисплеи. Более того вы можете изменить температуру кельвина посредством [dconf](https://www.archlinux.org/packages/?name=dconf). В следующем примере выбрано значение 5000:

```
$ gsettings set org.gnome.settings-daemon.plugins.color night-light-temperature 5000

```

**Совет:** Для того, чтобы изменить температуру фильтра в [Wayland](/index.php/Wayland_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wayland (Русский)") установите [это расширение](https://extensions.gnome.org/extension/1276/night-light-slider/).

#### Дата & время

Если в системе настроен [Network Time Protocol daemon](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon"), то он будет эффективно работать также и с GNOME. Синхронизация может быть переключена на ручной контроль из меню.

Чтобы показывать дату в верхней панели:

```
$ gsettings set org.gnome.desktop.interface clock-show-date true

```

Кроме того, чтобы показывать номера недель в календаре, открытом в верхней панели:

```
$ gsettings set org.gnome.desktop.calendar show-weekdate true

```

#### Приложения по умолчанию

После установки GNOME в первый раз вы можете обнаружить, что не те приложения обрабатывают определенные протоколы. Например, *totem* открывает видео вместо ранее использованного [VLC](/index.php/VLC "VLC"). Некоторые ассоциации могут быть установлены с помощью системных настроек: *Все параметры* > *Подробности* > *Приложения по умолчанию*.

Для других протоколов и методов их конфигурации смотрите [приложения по умолчанию](/index.php/Default_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Default applications (Русский)").

#### Мышь и сенсорная панель

Многие настройки сенсорной панели могут быть установлены с помощью системных настроек: *Параметры* > *Устройства* > *Мышь и сенсорная панель*.

В зависимости от вашего устройства другие параметры, которые нельзя настроить через интерфейс, могут быть доступны. Например, другой `click-method` тачпада:

 `$ gsettings range org.gnome.desktop.peripherals.touchpad click-method` 
```

enum
'default'
'none'
'areas'
'fingers'
```

Вручную:

```
$ gsettings set org.gnome.desktop.peripherals.touchpad click-method 'fingers'

```

или через [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).

**Примечание:** Драйвер [synaptics](/index.php/Synaptics "Synaptics") не поддерживается GNOME. Вместо него вы должны использовать [libinput](/index.php/Libinput "Libinput"). Смотрите [этот отчет об ошибке](https://bugzilla.gnome.org/show_bug.cgi?id=764257#c12).

#### Сеть

[NetworkManager](/index.php/NetworkManager "NetworkManager") - собственный инструмент проекта GNOME для управления настройками сети. [Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) и [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") `NetworkManager.service`.

В отличие от других [менеджеров сети](/index.php/List_of_applications/Internet#Network_managers "List of applications/Internet"), которые могут быть также использованы, NetworkManager обеспечивает полную интеграцию через настройки сети оболочки и предоставляет апплет индикатора статуса [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) (не требуется для GNOME).

**Note:** Скрытые беспроводные сети, созданные с помощью *nmtui* (консольный интерфейс для [networkmanager](https://www.archlinux.org/packages/?name=networkmanager)) не подключаются автоматически. Вы должны создать новый профиль в настройках GNOME для того, чтобы восстановить возможность автоподключения к этой сети.

#### Сетевые учетные записи

Бекенды для приложения обмена сообщениями GNOME [empathy](https://www.archlinux.org/packages/?name=empathy) и для Сетевых учетных записей GNOME, которые располагаются в Параметрах системы, находятся в отдельной группе: [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). Смотрите [не удается добавить аккаунты в Empathy и Сетевые учетные записи GNOME](/index.php/GNOME/Troubleshooting#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts "GNOME/Troubleshooting"). Некоторые сетевые учетные записи, такие как [ownCloud](/index.php/OwnCloud "OwnCloud"), требуют установки [gvfs-goa](https://www.archlinux.org/packages/?name=gvfs-goa) для полной работоспособности в приложениях GNOME, таких как [GNOME Files](/index.php/GNOME_Files "GNOME Files") и GNOME Documents [[1]](https://wiki.gnome.org/ThreePointSeven/Features/Owncloud).

#### Поиск

Чтобы воспользоваться поиском GNOME нужно нажать клавишу `Super` и просто начать печатать. Пакет [tracker](https://www.archlinux.org/packages/?name=tracker) устанавливается по умолчанию, как часть группы [gnome](https://www.archlinux.org/groups/x86_64/gnome/), и индексирует приложения и базы метаданных. Настраивается при помощи *Поиск и индексация*. Мониторинг состояния производится посредством *tracker-control*. Он автоматически запускается *gnome-session* при входе в систему. Можно запустить вручную: `tracker-control -s`. Параметры поиска также могут быть настроены из панели *Все параметры*.

Отправлять запросы базе данных Tracker можно при помощи *tracker-sparql*. Смотрите страницу справочного руководства [tracker-sparql(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tracker-sparql.1).

### Расширенная конфигурация

Как вы могли заметить выше, многие параметры, такие как изменение темы [GTK+](/index.php/GTK%2B "GTK+") или [оконного менеджера](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер"), недоступны в панели управления GNOME (*gnome-control-center*). Пользователи, желающие настроить эти параметры, возможно, захотят использовать GNOME Tweaks ([gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) - удобная графическая утилита, которая предоставляет доступ к множеству параметров.

Параметры GNOME (которые сохраняются в базе данных DConf) также могут быть настроены, используя [*dconf-editor*](https://developer.gnome.org/dconf/unstable/dconf-editor.html) (графический инструмент для настройки DConf) или [*gsettings*](https://developer.gnome.org/gio/stable/GSettings.html) - консольный утилита для настройки. В GNOME Tweak Tool нет скрытых настроек, все они предоставлены в графическом интерфейсе; заметим, однако, что вы не найдете все описываемые ниже параметры в этой утилите.

#### Внешний вид

##### Темы

GNOME использует Adwaita по умолчанию. Для того, чтобы применить тему Adwaita dark только для GTK+2 приложений, используйте следующую символическую ссылку:

```
 $ ln -s /usr/share/themes/Adwaita-dark ~/.themes/Adwaita

```

Для того, чтобы установить новые темы, переместите их в соответствующий каталог и используйте GNOME Tweaks или следующие команды GSettings:

Для темы GTK+:

```
$ gsettings set org.gnome.desktop.interface gtk-theme *имя-темы*

```

Для темы иконок:

```
$ gsettings set org.gnome.desktop.interface icon-theme *имя-темы*

```

**Примечание:** Тема оконного менеджера использует тему GTK+. Использование `org.gnome.desktop.wm.preferences theme` не поддерживается и игнорируется.

Смотрите [GTK+#Темы](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Темы "GTK+ (Русский)") и [Icons#Manually](/index.php/Icons#Manually "Icons").

##### Высота заголовка

**Примечание:** Эта конфигурация сжимает заголовок GNOME-terminal и Chromium, но не влияет на высоту заголовка Nautilus.
 `~/.config/gtk-3.0/gtk.css` 
```
headerbar.default-decoration {
 padding-top: 0px;
 padding-bottom: 0px;
 min-height: 0px;
 font-size: 0.6em;
}

headerbar.default-decoration button.titlebutton {
 padding: 0px;
 min-height: 0px;
}

```

Смотрите [[2]](https://ask.fedoraproject.org/en/question/10035/shrink-title-bar/?answer=86149#post-id-86149) для дополнительной информации.

##### Порядок кнопок в заголовке

Выполните, чтобы задать порядок кнопок (Mutter, Metacity):

```
$ gsettings set org.gnome.desktop.wm.preferences button-layout ':minimize,maximize,close'

```

**Совет:** Двоеточие указывает, с какой стороны заголовка окна будут располагаться кнопки.

##### Скрыть заголовок, когда окно во весь экран

*   [Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [gnome-shell-extension-no-title-bar-git](https://aur.archlinux.org/packages/gnome-shell-extension-no-title-bar-git/) или [gnome-shell-extension-no-title-bar](https://aur.archlinux.org/packages/gnome-shell-extension-no-title-bar/). Заголовок окон в полноэкранном режиме будет перемещен в панель в верхней части экрана.

*   [Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [mutter-hide-legacy-decorations](https://aur.archlinux.org/packages/mutter-hide-legacy-decorations/). Это изменит стандартные настройки оконного менеджера таким образом, что заголовки старых приложений (без функциональных кнопок в заголовке), будут автоматически скрываться в полноэкранном режиме или при максимальной высоте.

*   [Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [gnome-shell-extension-pixel-saver-git](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver-git/) или [gnome-shell-extension-pixel-saver](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver/). Заголовок окон будет перемещен в панель в верхней части экрана, экономя драгоценные пиксели.

##### Темы GNOME Shell

Тему Gnome Shell можно настроить. Убедитесь, что установлен пакет [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions). Затем включите расширение *User Themes* при помощи GNOME Tweaks или через сайт [GNOME Shell Extensions](https://extensions.gnome.org). Темы Shell могут быть загружены и выбраны, используя GNOME Tweaks.

Некоторые темы GNOME Shell доступны [в AUR](https://aur.archlinux.org/packages.php?O=0&K=gnome-shell-theme&do_Search=Go&PP=50&SB=v&SO=d).

Также темы можно скачать с [gnome-look.org](http://gnome-look.org/).

##### Иконки в меню

По умолчанию никакие иконки в меню не отображаются. Чтобы включить отображение иконок в меню, выполните следующую команду.

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

```

#### Каталоги в меню приложений

**Совет:** Скрипт [gnome-catgen](https://github.com/prurigro/gnome-catgen) ([gnome-catgen-git](https://aur.archlinux.org/packages/gnome-catgen-git/)) позволяет вам управлять папками путем создания файлов в `~/.local/share/applications-categories`, называющихся в соответствии с категорией, содержащей список desktop-файлов, принадлежащих приложениям, которые вы хотели бы видеть внутри. При желании вы можете распределить все приложения без категории в соответствующие папки при помощи цикличного обхода, который не завершится пока вы не нажмете ctrl-c или не закончатся неотсортированные приложения.

В **dconf-editor** перейдите в `org.gnome.desktop.app-folders` и установите значение `folder-children` на массив имен папок, разделенных запятыми:

```
['Utilities', 'Sundry']

```

Добавьте приложения, используя `gsettings`:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ apps "['alacarte.desktop', 'dconf-editor.desktop']"

```

Действия выше добавят приложения `alacarte.desktop` и `dconf-editor.desktop` в папку Sundry. Это также создаст каталог `org.gnome.desktop.app-folders.folders.Sundry`.

Чтобы переименовать папку (если у нее нет имени, которое отображается в верхней части приложений):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ name "Sundry"

```

Приложения аналогично могут быть отсортированы по их категории (указанной в *.desktop* файле):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ categories "['Office']"

```

Если нужные приложения, соответствующие категории, не хотят добавляться в требуемую папку:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ excluded-apps "['libreoffice-draw.desktop']"

```

Для получения более подробной информации смотрите [[3]](https://gitlab.gnome.org/GNOME/gsettings-desktop-schemas/blob/master/schemas/org.gnome.desktop.app-folders.gschema.xml.in) и [[4]](https://wiki.gentoo.org/wiki/Gnome_Applications_Folders).

#### Автозапуск приложений при входе в систему

GNOME реализует [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart").

Утилита [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) позволяет управлять тем, какие приложения будут запущены при входе.

**Совет:** Если кнопка с иконкой "**+**" в GNOME Tweaks недоступна, попробуйте запустить GNOME Tweaks из терминала следующей командой: `gnome-tweaks`. Смотрите [страницу форума](https://bbs.archlinux.org/viewtopic.php?pid=1413631#p1413631).

**Примечание:** Устаревший диалог *gnome-session-properties* может быть добавлен путем [установки](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакета [gnome-session-properties](https://aur.archlinux.org/packages/gnome-session-properties/).

#### Рабочий стол

##### Иконки на рабочем столе

До GNOME 3.28 иконки на рабочем столе предоставлялись [Files](/index.php/GNOME/Files "GNOME/Files"). В GNOME 3.28 такая функциональность была удалена. Чтобы вернуть эту функциональность, можно использовать [Nemo](/index.php/Nemo "Nemo") (форк Files, у которого есть данная функция) или установить расширение [gnome-shell-extension-desktop-icons](https://aur.archlinux.org/packages/gnome-shell-extension-desktop-icons/), которое воспроизводит такие иконки на рабочем столе, какие были в GNOME 3.26 и ниже, но с некоторыми отличиями. Для большей информации смотрите тему форума - [Arch forum thread](https://bbs.archlinux.org/viewtopic.php?id=235633)

##### Фон экрана блокировки и рабочего стола

При настройке фона рабочего стола и экрана блокировки, важно отметить, что вкладка Изображения будет отображать картинки, расположенные только в папке `/home/*имяпользователя*/Изображения`. Если вы хотите использовать картинку, не находящуюся в этой папке, используйте команды ниже.

Для рабочего стола:

```
$ gsettings set org.gnome.desktop.background picture-uri 'file:///путь/к/моей/картинке.jpg'

```

Для экрана блокировки:

```
$ gsettings set org.gnome.desktop.screensaver picture-uri 'file:///путь/к/моей/картинке.jpg'

```

##### Отключение перехода в режим навигации при перемещении мыши в левый верхний угол

Вы можете отключить это поведение, установив пакет [gnome-shell-extension-no-topleft-hot-corner](https://aur.archlinux.org/packages/gnome-shell-extension-no-topleft-hot-corner/).

#### Расширения

Расширения можно найти на [extensions.gnome.org](https://extensions.gnome.org). Они могут быть установлены и активированы в браузере путем установки переключателя в верхнем правом углу экрана на **ON** и последующего нажатия **Install** в диалоге (если расширение не установлено). После установки оно покажется во вкладке [extensions.gnome.org/local/](https://extensions.gnome.org/local/), которая также может быть использована для проверки обновлений. Установленные дополнения могут быть включены или, наоборот, выключены посредством [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).

**Примечание:** Расширения по адресу [extensions.gnome.org](https://extensions.gnome.org) могут сразу же быть установлены с [GNOME/Web](/index.php/GNOME/Web "GNOME/Web"). Для других браузеров необходимо [установить](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C "Установить") [chrome-gnome-shell](https://www.archlinux.org/packages/?name=chrome-gnome-shell) и соответствующее вашему браузеру расширение.

GNOME Shell может быть настроен при помощи расширений как для отдельного пользователя, так и для всех сразу. Расширение, [установленные](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C "Установить") с помощью [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)"), доступны для всех пользователей системы, заодно и автоматизируется процесс их дальнейшего обновления. Пакет [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) предоставляет набор расширений, поддерживаемый как часть проекта GNOME (большинство включенных в него расширений используются в классической сессии GNOME). Пользователи, которые хотят панель задач, но не желают использовать сессию GNOME Classic, возможно, захотят установить расширение *Window list* (предоставляемое пакетом [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions)).

Для просмотра активных на данный момент расширений выполните:

```
$ gsettings get org.gnome.shell enabled-extensions

```

Для получения дополнительной информации о расширениях GNOME, смотрите [[5]](https://extensions.gnome.org/about/).

#### Шрифты

**Совет:** Если вы установите *Коэффициент масштабирования* на число, большее 1.00, Универсальное меню будет автоматически включено.

Можно настроить шрифты для заголовков окон, интерфейса (приложений), документов и изменить моноширинный шрифт. Смотрите вкладку "Шрифты" в GNOME Tweaks.

Для хинтинга, скорее всего, потребуется RGBA, так как он подходит для мониторов большинства типов, и если шрифты кажутся слишком загороженными, то измените хинтинг на *Slight* или *None*.

#### Методы ввода

GNOME имеет встроенную поддержку методов ввода через [IBus](/index.php/IBus "IBus"), нужно установить только [ibus](https://www.archlinux.org/packages/?name=ibus) и соответствующий движок (например, [ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin) для Intelligent Pinyin); после установки можно добавить соответствующий движок, как раскладку клавиатуры, в настройках GNOME Язык и регион.

#### Электропитание

Если вы используете ноутбук, то вы возможно захотите изменить следующие настройки:

```
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-timeout 3600
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type hibernate
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-timeout 1800
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-type hibernate
$ gsettings set org.gnome.settings-daemon.plugins.power power-button-action suspend
$ gsettings set org.gnome.desktop.lockdown disable-lock-screen true

```

Оставить монитор включенным при закрытии крышки:

```
$ gsettings set org.gnome.settings-daemon.plugins.xrandr default-monitors-setup do-nothing

```

Следующие настройки считаются устаревшими после версии GNOME 3.24:

```
org.gnome.settings-daemon.plugins.power button-hibernate
org.gnome.settings-daemon.plugins.power button-power
org.gnome.settings-daemon.plugins.power button-sleep
org.gnome.settings-daemon.plugins.power button-suspend
org.gnome.settings-daemon.plugins.power critical-battery-action

```

##### Отключение входа в спящий режим при закрытии крышки ноутбука

Панель настроек GNOME не предоставляет пользователю возможности выбрать выполняемое действие при закрытии крышки ноутбука. Однако [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) может переопределить настройки, применённые [systemd](https://www.archlinux.org/packages/?name=systemd). На вкладке *Основное* отключите опцию *Режим ожидания при закрытии ноутбука*. Теперь система не будет уходить в [спящий режим](/index.php/Power_management/Suspend_and_hibernate_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Power management/Suspend and hibernate (Русский)") (Suspend to RAM) при закрытии крышки ноутбука.

Для того, чтобы изменить выполняемое действие при закрытии крышки для всех пользователей, убедитесь, что опция *Режим ожидания при закрытии ноутбука* **не отключена** и отредактируйте настройки systemd в `/etc/systemd/logind.conf`. Для отключения входа в спящий режим при закрытии крышки установите опцию `HandleLidSwitch=ignore`, как описано в [Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management").

##### Изменить поведение при критическом уровне заряда батареи

Панель настроек не предоставляет соответствующую опцию для изменения действия, которое будет выполняться при критическом уровне заряда батареи. Также эти настройки были удалены из dconf. В настоящий момент они управляются upower. Отредактируйте файл настроек upower - `/etc/UPower/UPower.conf`. Найдите следующие параметры и настройте под свои нужны.

 `/etc/UPower/UPower.conf` 
```
PercentageLow=10
PercentageCritical=3
PercentageAction=2
CriticalPowerAction=HybridSleep
```

### Использование стороннего оконного менеджера

Оболочка GNOME не поддерживает использование стороннего [оконного менеджера](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)"), однако [GNOME/Flashback](/index.php/GNOME/Flashback "GNOME/Flashback") предоставляет сессии для Metacity и [Compiz](/index.php/Compiz_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Compiz (Русский)"). Более того, можно определять собственные сессии GNOME с использованием альтернативных компонентов.

## Смотрите также

*   [Официальный веб-сайт GNOME](https://www.gnome.org/)
*   [Статья на Wikipedia](https://en.wikipedia.org/wiki/GNOME "wikipedia:GNOME")
*   [Расширения для оболочки GNOME](https://extensions.gnome.org/)
*   [Список горячих клавиш для оболочки GNOME](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet)
*   Кастомизация (темы, иконки...):
    *   [Персонализация GNOME](https://wiki.gnome.org/Personalization)
    *   [GNOME Look](https://www.gnome-look.org/)
*   Приложения GNOME:
    *   [GNOME Apps Index](https://wiki.gnome.org/Apps)
    *   [Wikipedia:GNOME Core Applications](https://en.wikipedia.org/wiki/GNOME_Core_Applications "wikipedia:GNOME Core Applications")
*   Исходный код/Зеркала GNOME:
    *   [Git-репозиторий GNOME](https://gitlab.gnome.org/)
    *   [Зеркало GNOME на GitHub](https://github.com/GNOME)