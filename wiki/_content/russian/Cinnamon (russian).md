**Состояние перевода:** На этой странице представлен перевод статьи [Cinnamon](/index.php/Cinnamon "Cinnamon"). Дата последней синхронизации: 31 января 2015‎. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Cinnamon&diff=0&oldid=358916).

Ссылки по теме

*   [Nemo](/index.php/Nemo "Nemo")
*   [GNOME (Русский)](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)")
*   [MATE (Русский)](/index.php/MATE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MATE (Русский)")
*   [Среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола")
*   [Экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер")

Из [Википедии](https://en.wikipedia.org/wiki/ru:Cinnamon "wikipedia:ru:Cinnamon"):

	*"Cinnamon (от англ.* cinnamon *— корица) — свободная [среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола"), являющаяся ответвлением от кодовой базы GNOME Shell. Основное направление разработки — предоставление пользователю более привычной, традиционной среды в стиле GNOME 2."*

Размещение элементов рабочего стола схоже с той, которое предоставляла панель GNOME (GNOME 2), однако, лежащая в основе технология была взята из GNOME Shell (GNOME 3). Начиная с версии 2.0, Cinnamon стал самостоятельной средой рабочего стола, а не просто оболочкой для GNOME, как GNOME Shell и Unity.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Запуск Cinnamon](#Запуск_Cinnamon)
    *   [2.1 Графический вход](#Графический_вход)
    *   [2.2 Запуск Cinnamon вручную](#Запуск_Cinnamon_вручную)
*   [3 Настройка](#Настройка)
    *   [3.1 Cinnamon settings](#Cinnamon_settings)
        *   [3.1.1 Сеть](#Сеть)
        *   [3.1.2 Bluetooth](#Bluetooth)
    *   [3.2 Апплеты и расширения](#Апплеты_и_расширения)
*   [4 Советы и рекомендации](#Советы_и_рекомендации)
    *   [4.1 Создание собственных апплетов и тем](#Создание_собственных_апплетов_и_тем)
    *   [4.2 Стандартный каталог обоев рабочего стола](#Стандартный_каталог_обоев_рабочего_стола)
    *   [4.3 Отобразить стандартные значки рабочего стола](#Отобразить_стандартные_значки_рабочего_стола)
    *   [4.4 Запуск произвольных команд из меню](#Запуск_произвольных_команд_из_меню)
    *   [4.5 Переключение между рабочими столами](#Переключение_между_рабочими_столами)
    *   [4.6 Скрытие значков рабочего стола](#Скрытие_значков_рабочего_стола)
    *   [4.7 Темы и значки GTK](#Темы_и_значки_GTK)
    *   [4.8 Изменение размеров окон мышью](#Изменение_размеров_окон_мышью)
    *   [4.9 Перенос настроек назначений клавиш](#Перенос_настроек_назначений_клавиш)
*   [5 Решение проблем](#Решение_проблем)
    *   [5.1 QGtkStyle не может определить текущую тему](#QGtkStyle_не_может_определить_текущую_тему)
    *   [5.2 Нажатие кнопки включения переводит систему в ждущий режим](#Нажатие_кнопки_включения_переводит_систему_в_ждущий_режим)
    *   [5.3 Уровень громкости не сохраняется](#Уровень_громкости_не_сохраняется)
    *   [5.4 cinnamon-settings: No module named Image](#cinnamon-settings:_No_module_named_Image)
    *   [5.5 Не удается изменить язык в Cinnamon](#Не_удается_изменить_язык_в_Cinnamon)
    *   [5.6 Video tearing](#Video_tearing)

## Установка

Cinnamon можно [установить](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_отдельных_пакетов "Pacman (Русский)") с пакетом [cinnamon](https://www.archlinux.org/packages/?name=cinnamon), доступном в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Чтобы установить дополнительные темы, апплеты и расширения, вы можете добавить [неофициальный репозиторий Cinnamon](/index.php/Unofficial_user_repositories#cinnamon "Unofficial user repositories") в ваш `pacman.conf`.

## Запуск Cinnamon

### Графический вход

Выберите *Cinnamon* либо *Cinnamon (Software Rendering)* из меню вашего [экранного менеджера](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)"). Первый вариант использует ускорение графического адаптера, и его следует использовать если не возникает проблем. Если вы испытываете проблемы с драйвером видео (появляются артефакты или прочие сбои), попробуйте запустить сеанс *Cinnamon (Software Rendering)*, в котором отрисовка осуществляется программно.

### Запуск Cinnamon вручную

Если вы предпочитаете входить в среду рабочего стола из консоли, добавьте следующую строку в ваш [Xinitrc](/index.php/Xinitrc "Xinitrc") (для Cinnamon 1.9 и выше):

 `~/.xinitrc` 
```
 exec cinnamon-session

```

Будет запущена версия среды, использующая аппаратное ускорение. Если требуется программная отрисовка, используйте `cinnamon-session-cinnamon2d` вместо `cinnamon-session`.

## Настройка

Cinnamon достаточно прост в настройке. Большую часть настройки можно осуществить используя графические панели. Рабочий стол можно дополнить разнообразными [апплетами](http://cinnamon-spices.linuxmint.com/applets) и [расширениями](http://cinnamon-spices.linuxmint.com/extensions), а также [темами](http://cinnamon-spices.linuxmint.com/themes).

### Cinnamon settings

*cinnamon-settings* запускает указанную панель настройки из командной строки. Без аргументов запускается панель *System Settings* (Настройки Системы). Например, для запуска настроек панели, наберите:

```
$ cinnamon-settings panel

```

Отобразить список всех доступных модулей вы можете командой

```
$ pacman -Ql cinnamon | grep -o "cs_.*\.py" | awk -F'[_.]' '{ print $2 }'

```

#### Сеть

Чтобы добавить поддержку сетевого модуля, включите [Network Manager](/index.php/NetworkManager#Configuration "NetworkManager"). Чтобы NetworkManager мог хранить пароли к беспроводным сетям, установите также [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring").

#### Bluetooth

**Важно:** [cinnamon-bluetooth](https://aur.archlinux.org/packages/cinnamon-bluetooth/) несовместим с [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") 3.10 и выше. Альтернативные варианты вы можете найти на странице [Bluetooth](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bluetooth (Русский)")

Компоненты графического интерфейса для работы с bluetooth доступны в [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") с пакетом [cinnamon-bluetooth](https://aur.archlinux.org/packages/cinnamon-bluetooth/). Однако, с 18 ноября 2014 г. ни один из пакетов *cinnamon-bluetooth* не работает нормально.

### Апплеты и расширения

Апплеты представляют собой дополнительные компоненты для панели Cinnamon. В свою очередь, расширение может внести значительные изменения в среду рабочего стола. Они могут быть установлены как из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") ([поиск пакетов](https://aur.archlinux.org/packages.php?O=0&K=cinnamon-&do_Search=Go)), так и с помощью панели *Get more online* в самом Cinnamon, которую можно запустить командами:

```
$ cinnamon-settings applets
$ cinnamon-settings extensions

```

Также вы можете скачать и установить их вручную со страницы [Cinnamon spices](http://cinnamon-spices.linuxmint.com/).

**Примечание:** Если установленные апплеты не появляются, перезапустите Cinnamon, введя `r` в диалоговое окно по нажатию `Alt+F2`.

## Советы и рекомендации

### Создание собственных апплетов и тем

Официальное руководство по созданию апплетов Cinnamon доступно [здесь](http://cinnamon.linuxmint.com/?p=156). Руководство по созданию собственных также доступно [здесь](http://cinnamon.linuxmint.com/?p=144).

### Стандартный каталог обоев рабочего стола

Когда вы добавляете изображение в качестве обоев по указанному пути в Cinnamon Settings, файл изображения копируется в `~/.cinnamon/backgrounds`. Таким образом, с каждым изменением изображения обоев, вам придется добавлять новое изображение снова через панель настроек или копировать его вручную (либо создавать символическую ссылку) в `~/.cinnamon/backgrounds`.

### Отобразить стандартные значки рабочего стола

По умолчанию, Cinnamon запускается без значков на рабочем столе. Чтобы добавить стандартные значки для домашнего каталога, файловой системы и корзины, а также смонтированные диски и сетевые службы, откройте настройки рабочего стола в *Settings* и установите флажки для тех значков, которые вы хотите отобразить.

### Запуск произвольных команд из меню

Апплет *Menu* позволяет запускать указанную команду при выборе. Для того, чтобы добавить новый пункт меню, нажмите правой кнопкой мыши по апплету, выберите *Configure...*, *Open the menu editor*. Выберите нужное подменю (или создайте новое) и выберите *New Item*. Укажите имя в поле *Name* и команду в поле *Command*. Вы можете оставить подсказку к пункту меню в поле *Comment*. Если при запуске команды нужно отображать окно терминала, установите флажок *launch in terminal*. После нажатия *OK* в меню появится новый пункт.

### Переключение между рабочими столами

Для переключения между рабочими столами вы можете добавить переключатель на панель. Нажмите по панели правой кнопкой мыши, выберите *Add applets to the panel*. Добавьте апплет *Workspace switch* на панель. Чтобы переместить апплет, нажмите правой кнопкой мыши по панели, и установите переключатель 'Panel edit mode' во включенное положение. Перетащите мышью апплет на выбранное место, после чего выключите *Panel edit mode*.

По умолчанию предусмотрено два рабочих стола. Вы можете добавить еще, нажав `Control+Alt+Up` и кликнув на кнопку `+` справа.

Также вы можете указать точное количество в командной строке, выполнив:

```
$ gsettings set org.cinnamon number-workspaces 4

```

В данном случае, будет установлено 4 рабочих стола. Чтобы изменения вступили в силу, вам необходимо перезагрузить Cinnamon (для чего нажмите `Alt-F2` и введите `r` в поле ввода команды).

### Скрытие значков рабочего стола

За отображение значков на рабочем столе отвечает [Nemo](/index.php/Nemo "Nemo"). Чтобы выключить отображение значков, выполните команду

```
$ gsettings set org.nemo.desktop show-desktop-icons false

```

### Темы и значки GTK

Темы и значки, стилизованные под цвета Linux Mint доступны в [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") с пакетами [mint-themes](https://aur.archlinux.org/packages/mint-themes/) и [mint-x-icons](https://aur.archlinux.org/packages/mint-x-icons/). Настройки темы вы можете найти в `Settings → Themes → Other settings`

### Изменение размеров окон мышью

Чтобы изменять размеры окон нажатием `Alt + Right click`, выполните

```
gsettings set org.cinnamon.desktop.wm.preferences resize-with-right-button true

```

### Перенос настроек назначений клавиш

Вы можете выполнить экспорт ваших назначений клавиш командой

```
dconf dump /org/cinnamon/muffin/keybindings/ >keybindings-backup.dconf

```

Чтобы впоследствии импортировать их, выполните

```
dconf load /org/cinnamon/muffin/keybindings/ <keybindings-backup.dconf

```

## Решение проблем

### QGtkStyle не может определить текущую тему

Установка [libgnome-data](https://aur.archlinux.org/packages/libgnome-data/) частично решает проблему, и QGtkStyle начинает определять текущую тему GTK+. Однако, чтобы использовался правильный набор значков и курсоры мыши, необходимо задать их явно.

Тема значков для приложений Qt может быть установлена следующей командой:

```
$ gconftool-2 --set --type string /desktop/gnome/interface/icon_theme Faenza-Dark

```

Команда установит тему значков *Faenza-Dark*, которая находится, соответственно, в `/usr/share/icons/Faenza-Dark`.

Тема курсоров мыши для приложений Qt может быть установлена созданием символической ссылки `~/.icons/default`:

```
$ mkdir ~/.icons
$ ln -s /usr/share/icons/Adwaita ~/.icons/default

```

Команда установит тему курсоров *Adwaita*, которая находится в `/usr/share/icons/Adwaita`.

### Нажатие кнопки включения переводит систему в ждущий режим

Это является стандартным поведением. Чтобы изменить настройки управления электропитанием, откройте панель *Settings* и выберите *Power Management*. Выберите желаемое действие для события *When the power button is pressed*.

### Уровень громкости не сохраняется

Уровень громкости не сохраняется после перезагрузки. Звук при запуске системы не приглушен, но уровень установлен в 0\. В таком случае, решить проблему поможет установка [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils).

### cinnamon-settings: No module named Image

Если панель `cinnamon-settings` не запускается, отображая сообщение о том, что не найден какой-либо модуль, например `Image`, это значит, что он использует устаревшие файлы, которые ссылаются на несуществующие пути. В этом случае, удалите все файлы *.pyc* в каталоге `/usr/lib/cinnamon-settings` и его подкаталогах.

### Не удается изменить язык в Cinnamon

Языковой модуль был удален из панели управления Cinnamon с версии 2.2\. Чтобы добавить или удалить языки, смотрите [Locale (Русский)](/index.php/Locale_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Locale (Русский)"). Чтобы выбрать другой язык, установите пакет [mintlocale](https://aur.archlinux.org/packages/mintlocale/).

### Video tearing

Video tearing представляет собой неисправность, при которой вы видите на экране не перерисованный полностью кадр, что выражается в появлении видимых мерцающих горизонтальных полос.

Если вы наблюдаете подобные эффекты при просмотре видео или в играх, добавьте следующие строки в конец файла `/etc/environment`:

```
CLUTTER_PAINT=disable-clipped-redraws:disable-culling
CLUTTER_VBLANK=True

```

После перезагрузки проблема должна решиться.