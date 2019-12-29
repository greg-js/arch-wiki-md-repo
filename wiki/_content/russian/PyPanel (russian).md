Страница PyPanel: [SourceForge](http://pypanel.sourceforge.net/)

	PyPanel - легковесная панель/панель задач написанная на Python и C для [X11 Window Mangaer](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)"). PyPanel может быть легко настроена под любую тему рабочего стола. PyPanel работает под практически любой [WM](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)") (Openbox, PekWM, FVWM, и т.д.), распространяется PyPanel под лицензией GNU General Public v2.

	функции кастомизации включают в себя:

*   Прозрачность и тонировка
*   Размеры панели, расположение, планировка
*   Стили шрифтов, цвета с [Xft](/index.php/Font_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Font configuration (Русский)") и поддержка теней
*   События и действия кнопок
*   Часы и названия рабочих столов
*   Системный трей (Область оповещений)
*   Автоматически скрывать панель
*   Лаунчер приложений (имеется ввиду иконки приложений)
*   Кастомизируемые иконки для приложений

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 Запуск приложений](#Запуск_приложений)
*   [3 Хитрости, советы и подсказки](#Хитрости,_советы_и_подсказки)
*   [4 Полезные ссылки](#Полезные_ссылки)

## Установка

Установите пакет [pypanel](https://www.archlinux.org/packages/?name=pypanel).

## Настройка

Так как pypanel легковесный, то большинство его возможностей по настройке скрывается в файле `.pypanelrc`, который создаётся автоматически после первого запуска.

Запустить pypanel можно выполнив команду от пользователя:

```
$ pypanel

```

Для автоматического запуска смотрите [xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)") или [автозапуск приложений](/index.php/Autostarting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Autostarting (Русский)").

После первого запуска в домашней директории пользователя появится конфигурационный файл с настройками `~/.pypanelrc`. Конфигурационный файл использует синтаксис Python-скриптов, а также имеет больше количество комментариев и заметок, так что сложности в настройке возникнуть не должно. Здесь несколько предложений и рекомендаций по настройке:

```
BG_COLOR        = "0xfaebd7"    # Panel background and tint (Antique White)
TASK_COLOR      = "0xffffff"    # Цвет панели
DESKTOP_COLOR   = "0xffffff"    # Цвет рабочего стола
CLOCK_COLOR     = "0xffffff"    # Цвет часов на панели

TASK_SHADOW_COLOR      = "0x000000"
FOCUSED_SHADOW_COLOR   = "0x000000"
SHADED_SHADOW_COLOR    = "0x000000"
MINIMIZED_SHADOW_COLOR = "0x000000" 
DESKTOP_SHADOW_COLOR   = "0x000000"
CLOCK_SHADOW_COLOR     = "0x000000"

SHADE           = 64

ABOVE           = 1             # Панель перекрывает приложения
APPICONS        = 1             # Показывает иконки приложений
AUTOHIDE        = 0             # Автоматическое скрывание панели
SHADOWS         = 1             # Показать тень
SHOWLINES       = 0             # Показать разделительные линии
SHOWBORDER      = 1             # Показать границу вокруг панели

```

Множество настроек могут быть изменены. Рекомендации выше показывают графические возможности настройки панели. Нажатие кнопок мыши и множество другого можно настроить в файле конфигурации, попробуйте почитать комментарии к рекомендациям, мануалы и экспериментируйте.

### Запуск приложений

Если вы желаете добавить иконки приложений для запуск в pypanel, то внесите следующие изменения в разделе "Panel Layout section":

```
 # Panel Layout:
 # ...
 DESKTOP    = 1
 TASKS      = 3
 TRAY       = 4
 CLOCK      = 5
 LAUNCHER   = 2

```

Далее добавьте это в `LAUNCH_LIST` секции. Первая часть команды для запуска, вторая для указания иконки.

**Примечание:** Указывайте полный путь к иконкам, это требуется для корректного отображения.

```
 LAUNCH_LIST  = [
            ("firefox", "/usr/lib/firefox-3.0.1/icons/mozicon16.xpm"),
            ("thunar", "/usr/share/icons/oxygen/16x16/apps/system-file-manager.png"),
            ("urxvt -bg black -fg grey", "/usr/share/icons/oxygen/16x16/apps/terminal.png"),
            ]

```

Просмотрите директорию `/usr/share/icons` для поиска иконок приложений.

## Хитрости, советы и подсказки

Если вы желаете сделать нажатия клавиш мыши более традиционными, то проследуй в файл `.pypanelrc`:

```
#-------------------------------------
def taskButtonEvent(pp, button, task):
#-------------------------------------
  """ Button event handler for the panel's tasks """

  if button == 1:
      pp.taskFocus(task)

```

далее, скопируйте последнюю строку ещё раз, это должно выглядеть примерно так:

```
#-------------------------------------
def taskButtonEvent(pp, button, task):
#-------------------------------------
  """ Button event handler for the panel's tasks """

  if button == 1:
      pp.taskFocus(task)
      pp.taskFocus(task)

```

Если pypanel ссылается на отсутствие `.Xauthority`, то создайте его:

```
$ touch ~/.Xauthority

```

## Полезные ссылки

*   [PyPanel SourceForge page](http://pypanel.sourceforge.net)
*   [X Window System](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)")
*   [xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)")