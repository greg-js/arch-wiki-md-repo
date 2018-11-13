**Состояние перевода:** На этой странице представлен перевод статьи [MATE](/index.php/MATE "MATE"). Дата последней синхронизации: 21 января 2015\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=MATE&diff=0&oldid=357540).

Related articles

*   [GNOME (Русский)](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)")
*   [Cinnamon (Русский)](/index.php/Cinnamon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Cinnamon (Русский)")
*   [Среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола")
*   [Экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер")
*   [Uniform Look for Qt and GTK Applications (Русский)](/index.php/Uniform_Look_for_Qt_and_GTK_Applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Uniform Look for Qt and GTK Applications (Русский)")

С [официального сайта MATE](http://mate-desktop.org/):

	*MATE Desktop Environment является продолжением GNOME 2\. Он предоставляет интуитивное и привлекательное окружение рабочего стола, используя традиционные методы для Linux и других Unix-подобных систем. MATE [активно разрабатывается](https://github.com/mate-desktop) для обеспечения поддержки новых технологий, сохраняя традиционный стиль рабочего стола.*

## Contents

*   [1 Приложения](#Приложения)
*   [2 Установка](#Установка)
    *   [2.1 Дополнительные пакеты MATE](#Дополнительные_пакеты_MATE)
*   [3 Запуск MATE](#Запуск_MATE)
    *   [3.1 Графический вход](#Графический_вход)
    *   [3.2 Ручной запуск](#Ручной_запуск)
*   [4 Специальные возможности](#Специальные_возможности)
*   [5 Bluetooth](#Bluetooth)
*   [6 PulseAudio и GStreamer](#PulseAudio_и_GStreamer)
*   [7 Подсказки](#Подсказки)
    *   [7.1 Композитный менеджер](#Композитный_менеджер)
    *   [7.2 Новые окна по центру](#Новые_окна_по_центру)
    *   [7.3 Включить привязку окон](#Включить_привязку_окон)
    *   [7.4 Скрытие или показ иконок рабочего стола](#Скрытие_или_показ_иконок_рабочего_стола)
        *   [7.4.1 Скрыть все иконки на рабочем столе](#Скрыть_все_иконки_на_рабочем_столе)
        *   [7.4.2 Скрыть определённые иконки на рабочем столе](#Скрыть_определённые_иконки_на_рабочем_столе)
    *   [7.5 Поменять оконный менеджер](#Поменять_оконный_менеджер)
    *   [7.6 Изменить порядок кнопок у окон](#Изменить_порядок_кнопок_у_окон)
    *   [7.7 Авто-открытие файлового менеджера при мотнировании устройств](#Авто-открытие_файлового_менеджера_при_мотнировании_устройств)
    *   [7.8 Заставка](#Заставка)
    *   [7.9 Экран блокировки и его фоновое изображение](#Экран_блокировки_и_его_фоновое_изображение)
*   [8 Решение проблем](#Решение_проблем)
    *   [8.1 Переключение композиции](#Переключение_композиции)
    *   [8.2 Вертикальная синхронизация в композитных менеджерах](#Вертикальная_синхронизация_в_композитных_менеджерах)
    *   [8.3 Совместимость курсоров](#Совместимость_курсоров)
    *   [8.4 Отбрасывание панелью тени](#Отбрасывание_панелью_тени)
*   [9 Смотрите также](#Смотрите_также)

## Приложения

MATE состоит в основном из приложений и утилит GNOME 2, которые были ответвлены и переименованы для избежания конфликта с их аналогами в GNOME 3\. Ниже располагается список наиболее распростанённых приложений GNOME, которые были переименованы в MATE.

| Приложение | GNOME 2 | MATE |
| Редактор меню | Alacarte | Mozo |
| Файловый менеджер | Nautilus | Caja |
| Оконный менеджер | Metacity | Marco |
| Текстовый редактор | Gedit | Pluma |
| Просмотр изображений | Eye of GNOME | Eye of MATE |
| Просмотр документов | Evince | Atril |
| Менеджер архивов | File Roller | Engrampa |

Остальные приложения и компоненты, имевшие приставку GNOME (например, GNOME Terminal, GNOME Panel, GNOME Menus и т.п.) сменили приставку на MATE (и стали MATE Terminal, MATE Panel, MATE Menus и т.п.)

## Установка

MATE доступен в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") и может быть [установлен](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_пакетов "Pacman (Русский)") одним из следующих способов:

*   Пакет [mate-panel](https://www.archlinux.org/packages/?name=mate-panel) предоставляет минимальное окружение рабочего стола.
*   Группа пакетов [mate](https://www.archlinux.org/groups/x86_64/mate/) содержит основное рабочее окружение и приложения, необходимые для стандартной работы MATE
*   Группа пакетов [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/) содержит различные необязательные инструменты, которые хорошо работают в MATE. Заметьте, что установка только группы пакетов [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/) не вытянет всю группу [mate](https://www.archlinux.org/groups/x86_64/mate/) зависимостями: если вы действительно хотите всё, вы должны установить обе группы

### Дополнительные пакеты MATE

Также существуют пакеты, которые не входят в группы [mate](https://www.archlinux.org/groups/x86_64/mate/) или [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/), т.к. вероятнее всего они будут нужны малому количеству пользователей.

*   [gnome-main-menu](https://aur.archlinux.org/packages/gnome-main-menu/) - Апллет для панели MATE, подобный классическому главному меню, но с небольшими изменениями.
*   [mate-netbook](https://www.archlinux.org/packages/?name=mate-netbook) - Апплет для панели MATE, который может быть полезен владельцем устройств с небольшим экраном, такими как нетбук. Апплет будет автоматически разворачивать все окна, и предоставляет возможность переключения между приложениями.

Кроме того, имеется ряд приложений, которые разрабатываются и поддерживаются сообществом MATE, но которые не включены в группы [mate](https://www.archlinux.org/groups/x86_64/mate/) или [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/).

*   [mate-applet-lockkeys](https://aur.archlinux.org/packages/mate-applet-lockkeys/) - Апплет, показывающий состояние клавиш CapsLock, NumLock и ScrollLock.
*   [mate-applet-streamer](https://www.archlinux.org/packages/?name=mate-applet-streamer) - Апплет, позволяющий включить любимое online-радио одним кликом.
*   [mate-color-manager](https://aur.archlinux.org/packages/mate-color-manager/) - Утилита управления цветом.
*   [mate-accountsdialog](https://www.archlinux.org/packages/?name=mate-accountsdialog) - Приложение для просмотра и редактирования информации об аккаутнах.
*   [mate-disk-utility](https://aur.archlinux.org/packages/mate-disk-utility/) - Утилита управления дисками.
*   [mate-screensaver-hacks](https://aur.archlinux.org/packages/mate-screensaver-hacks/) - Хранители экрана xscreensaver для MATE.
*   [mate-themes-extras](https://www.archlinux.org/packages/?name=mate-themes-extras) - Коллекция GTK2/3 тем для MATE.

*   [variety](https://www.archlinux.org/packages/?name=variety) - Смена обоев на рабочем столе с регулярным интервалом.

Следующие пакеты также доступны в [AUR](/index.php/Arch_User_Repository "Arch User Repository") и работают в MATE, но разрабатываются силами других сообществ:

*   [mintmenu](https://aur.archlinux.org/packages/mintmenu/) - Linux Mint Menu для MATE

## Запуск MATE

MATE может быть запущен при помощи менеджера входа или вручную.

### Графический вход

Выберите *MATE* в [менеджере входа](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)"). Команда MATE рекомендует использовать [LightDM (Русский)](/index.php/LightDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LightDM (Русский)"), который устанавливается пакетом [lightdm-gtk2-greeter](https://aur.archlinux.org/packages/lightdm-gtk2-greeter/).

### Ручной запуск

Если вы предпочитаете запускать MATE самостоятельно из консоли, добавьте следующие строки в файл `~/.xinitrc`:

 `~/.xinitrc` 
```
exec mate-session

```

Затем используйте команду `startx` для запуска MATE.

Смотрите статью [xinitrc](/index.php/Xinitrc "Xinitrc") для подробностей.

## Специальные возможности

MATE хорошо подходит для использования людьми с нарушением зрения или подвижности. [Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_пакетов "Pacman (Русский)") пакеты [orca](https://www.archlinux.org/packages/?name=orca) и [espeak](https://www.archlinux.org/packages/?name=espeak) (Программа чтения с экрана для слабовидящих и слепых людей) и [onboard](https://www.archlinux.org/packages/?name=onboard) (Экранная клавиатура для людей с ограниченной подвижностью)

Теперь запустите указанную ниже команду от имени пользователя, нуждающегося в специальных возможностях:

```
gsettings set org.mate.interface accessibility true

```

После запуска MATE вы сможете настраивать эти приложения при помощи `Система -> Параметры -> Вспомогательные технологии`. Хотя если вам необходима Orca, её нужно запускать при помощи окна `Alt-F2` для начала озвучки текста.

## Bluetooth

Начиная с версии 1.8, поддержка [Bluetooth](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bluetooth (Русский)") в MATE обеспечивается при помощи [Blueman](/index.php/Blueman "Blueman").

## PulseAudio и GStreamer

MATE поддерживает два аудио-бекэнда: [PulseAudio](http://www.pulseaudio.org) и [GStreamer](http://www.gstreamer.net). По умолчанию устанавливается PulseAudio, но если вы хотите использовать GStreamer, [установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_пакетов "Pacman (Русский)") пакеты: [mate-settings-daemon-gstreamer](https://www.archlinux.org/packages/?name=mate-settings-daemon-gstreamer) и [mate-media-gstreamer](https://www.archlinux.org/packages/?name=mate-media-gstreamer)

## Подсказки

### Композитный менеджер

Композиция по умолчанию выключена. Для её использования запустите `Система -> Параметры -> Окна` и выберите опцию **Включить программный композитный оконный менеджер** на вкладке `Общие`. Или можно воспользоваться следующей командой в терминале:

```
$ dconf write /org/mate/marco/general/compositing-manager true

```

### Новые окна по центру

По умолчанию новые окна помещаются в левый верхний угол. Для того, чтобы они появлялись по центру запустите `Система -> Параметры -> Окна` и отметьте опцию **Размещать новые окна по центру** на вкладке `Расположение`. Этого же результата можно добиться при помощи dconf:

```
$ dconf write /org/mate/marco/general/center-new-windows true

```

### Включить привязку окон

По умолчанию привязка окон не используется. Для включения данного функционала запустите `Система -> Параметры -> Окна` и отметьте опцию **Включить тайлинговый режим** на вкладке `Расположение`. Сделать то же самое при помощи dconf:

```
$ dconf write /org/mate/marco/general/side-by-side-tiling true 

```

### Скрытие или показ иконок рабочего стола

По умолчанию в MATE отображаются различные иконки на рабочем столе: содержимое директории рабочего стола, Компьютер, Домашняя и сетевые директории, Корзина и смонтированные устройства. Вы можете настроить их отображение при помощи `dconf`.

#### Скрыть все иконки на рабочем столе

```
$ dconf write /org/mate/desktop/background/show-desktop-icons false

```

#### Скрыть определённые иконки на рабочем столе

Скрыть иконку Компьютера:

```
$ dconf write /org/mate/caja/desktop/computer-icon-visible false

```

Скрыть иконку домашней папки:

```
$ dconf write /org/mate/caja/desktop/home-icon-visible false

```

Скрыть иконку Сети:

```
$ dconf write /org/mate/caja/desktop/network-icon-visible false

```

Скрыть иконку Корзины:

```
$ dconf write /org/mate/caja/desktop/trash-icon-visible false

```

Скрыть иконку смонтированных устройств:

```
$ dconf write /org/mate/caja/desktop/volumes-visible false

```

Чтобы иконки снова появились, поменяйте `false` на `true`.

### Поменять оконный менеджер

По умолчанию MATE использует оконный менеджер *marco* - ответвление [metacity](https://www.archlinux.org/packages/?name=metacity), используемого в GNOME 2\. Вы можете заменить *marco* другим оконным менеджером несколькими способами:

*   Самый лёгкий способ — добавить его в автозапуск используя `mate-session-properties` (указанный вами оконный менеджер заменит стандарнтый при входе в систему). Откройте меню **Система**, перейдите в **Настройки**, нажмите **Запускаемые приложения**. В диалоге нажмите **Добавить**, введите какое-нибудь название, а в поле **Команда** введите *"ваш_оконный_менеджер"* *"--replace"*

Например, для openbox команда будет такой: `openbox --replace`.

Выйдите из MATE и снова зайдите. *marco* будет заменён выбранным вами оконным менеджером. Для возврата *marco* просто удалите созданную запись в **Запускаемых приложениях**.

**Note:** Стоит отметить, что этот способ не очень рекомендуется, так как сначала запустится *marco*, а потом ещё и ваш оконный менеджер, который, в конечном итоге, закроет *macro*

*   Также смену можно произвести при помощи dconf:

```
$ dconf write /org/mate/desktop/session/required-components/windowmanager "'ваш_оконный_менеджер'"

```

### Изменить порядок кнопок у окон

Вы можете изменить порядок кнопок при помощи dconf. Ключ - org.mate.marco.general.button-layout. Используйте графический dconf-editor или следующую команду для терминала:

```
$ dconf write /org/mate/marco/general/button-layout "'close,maximize,minimize:'"

```

Поставьте **menu**, **close**, **minimize** и **maximize** в желаемом порядке, разделяя их запятыми. Двоеточие означает заголовок окна.

### Авто-открытие файлового менеджера при мотнировании устройств

По умолчанию MATE автоматические открывает окно файлового менеджера при монтировании сменных устройств. Для отключения такого поведения скомандуйте в терминал:

```
$ dconf write /org/mate/desktop/media-handling/automount-open false

```

### Заставка

MATE использует [mate-screensaver](https://www.archlinux.org/packages/?name=mate-screensaver) для блокировки вашей сессии. По умолчанию имеется лишь несколько тем для заставки. Установив пакет [mate-screensaver-hacks](https://aur.archlinux.org/packages/mate-screensaver-hacks/) можно получить их гораздо больше. Это позволит вам использовать темы и экраны блокировки [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") для [mate-screensaver](https://www.archlinux.org/packages/?name=mate-screensaver).

### Экран блокировки и его фоновое изображение

Полный список настроек можно найти в `/usr/share/glib-2.0/schemas/org.mate.background.gschema.xml`. Они переопределяются созданием файла `/usr/share/glib-2.0/schemas/mate-background.gschema.override`.

**Note:** Значения справа должны быть заключены в одинарные кавычки (''), иначе произойдёт ошибка во время компиляции.

Пример #1: Сменить фоновое изображение на экране блокировки:

 `/usr/share/glib-2.0/schemas/mate-background.gschema.override` 
```
[org.mate.background]
picture-filename='/путь/к/изображению.jpg'
```

Пример #2: Сменить изображение на экране блокировки, используя градиент:

 `/usr/share/glib-2.0/schemas/mate-background.gschema.override` 
```
[org.mate.background]
color-shading-type='vertical-gradient'
picture-options='scaled'
picture-filename=''
primary-color='#152233'
secondary-color='#000000'
```

Перекомпилируйте схемы:

```
# glib-compile-schemas /usr/share/glib-2.0/schemas/

```

Перезапустите X для получения результата.

## Решение проблем

### Переключение композиции

Некоторое ПО может некорректно рендерить изображение, работая в системе с проприетарным драйвером Nvidia и композитным менеджером окон.

Для быстрого переключения функции композиции сохраните следующий скрипт где-нибудь в домашней директории, например `~/.scripts/compositing.sh`:

```
#!/bin/bash
if $(dconf read /org/mate/marco/general/compositing-manager) == "true"
 then
  dconf write /org/mate/marco/general/compositing-manager false
 else
  dconf write /org/mate/marco/general/compositing-manager true
fi

```

Затем создайте сочетание клавиш клавиатуры, например `Ctrl+Alt+C` для команды `sh ~/.scripts/compositing.sh`.

### Вертикальная синхронизация в композитных менеджерах

Композитный менеджер *marco* не поддерживает вертикальную синхронизацию через *OpenGL*, Что может вызывать тиринг (распадание изображения на полосы) при включенном композитном менеджере. [[1]](https://github.com/mate-desktop/marco/issues/91) Рекомендуется выбрать другой композитный менеджер [composite manager](/index.php/Xorg#Composite "Xorg") с поддержкой OpenGL, например [compton-git](https://aur.archlinux.org/packages/compton-git/).

### Совместимость курсоров

Вы можете обнаружить, что тема курсора, используемая в MATE непоследовательна. Например, курсор может меняться при перемещении между окнами разных приложений. Чтобы исправить это, установите тему курсора создав файл `index.theme`. Он определяет тему курсора в соответствии с спецификацией XDG. Для подробностей смотри статью [Темы курсора#Спецификация XDG](/index.php/%D0%A2%D0%B5%D0%BC%D1%8B_%D0%BA%D1%83%D1%80%D1%81%D0%BE%D1%80%D0%B0#Спецификация_XDG "Темы курсора").

### Отбрасывание панелью тени

Для того, чтобы панель отбрасывала тень, добавьте задержку при запуске *marco* (см. [обсуждение на github](https://github.com/mate-desktop/mate-panel/issues/193)).

```
$ cp /usr/share/applications/marco.desktop ~/.local/share/applications/marco.desktop

```
 `~/.local/share/applications/marco.desktop` 
```
...
X-MATE-Autostart-Phase=**Applications**
**X-MATE-Autostart-Delay=2**
X-MATE-Provides=windowmanager
X-MATE-Autostart-Notify=true
```

**Note:** Переменная `X-MATE-Autostart-Phase` должна быть установлена в `Applications`.

Если результата не будет - увеличьте время задержки.

## Смотрите также

*   [Официальный сайт MATE](http://mate-desktop.org)
*   [wiki-страница на сайте MATE, посвещённая Arch Linux](http://wiki.mate-desktop.org/archlinux_custom_repo)
*   [*Скриншоты MATE*](http://mate-desktop.org/gallery/1.8/)
*   [*The MATE Desktop Environment*](https://bbs.archlinux.org/viewtopic.php?pid=1018647) - Обсуждение MATE на форме Arch Linux