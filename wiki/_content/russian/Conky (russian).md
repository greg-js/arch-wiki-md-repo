*Conky* является системным монитором для оконной системы X. Он доступен для Linux и FreeBSD. Это свободное программное обеспечение выпущенное на условиях лицензии GPLv3\. *Conky* может производить мониторинг большинства системных параметров, включая частоту и загрузку CPU, RAM, подкачки, дискового пространства, температуру, может отображать системные сообщения, и др. Он довольно легко настраивается, однако, процесс настройки может быть слегка сложным для понимания. *Conky* - это ответвление от проекта *torsmo*.

## Contents

*   [1 Установка и настройка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [2 Версии из AUR](#.D0.92.D0.B5.D1.80.D1.81.D0.B8.D0.B8_.D0.B8.D0.B7_AUR)
*   [3 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.1 Включить реальную прозрачность в KDE4 и Xfce4](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B8.D1.82.D1.8C_.D1.80.D0.B5.D0.B0.D0.BB.D1.8C.D0.BD.D1.83.D1.8E_.D0.BF.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D0.BE.D1.81.D1.82.D1.8C_.D0.B2_KDE4_.D0.B8_Xfce4)
    *   [3.2 Автозапуск в Xfce4](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B2_Xfce4)
    *   [3.3 Как предотвратить мерцание](#.D0.9A.D0.B0.D0.BA_.D0.BF.D1.80.D0.B5.D0.B4.D0.BE.D1.82.D0.B2.D1.80.D0.B0.D1.82.D0.B8.D1.82.D1.8C_.D0.BC.D0.B5.D1.80.D1.86.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [3.4 Настройка цвета](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.86.D0.B2.D0.B5.D1.82.D0.B0)
    *   [3.5 С двумя экранами](#.D0.A1_.D0.B4.D0.B2.D1.83.D0.BC.D1.8F_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0.D0.BC.D0.B8)
    *   [3.6 Не сворачивать при сворачивании всех окон](#.D0.9D.D0.B5_.D1.81.D0.B2.D0.BE.D1.80.D0.B0.D1.87.D0.B8.D0.B2.D0.B0.D1.82.D1.8C_.D0.BF.D1.80.D0.B8_.D1.81.D0.B2.D0.BE.D1.80.D0.B0.D1.87.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8_.D0.B2.D1.81.D0.B5.D1.85_.D0.BE.D0.BA.D0.BE.D0.BD)
    *   [3.7 Интеграция с Gnome 3](#.D0.98.D0.BD.D1.82.D0.B5.D0.B3.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D1.81_Gnome_3)
    *   [3.8 Интеграция с KDE](#.D0.98.D0.BD.D1.82.D0.B5.D0.B3.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D1.81_KDE)
    *   [3.9 Интеграция с Razor-qt](#.D0.98.D0.BD.D1.82.D0.B5.D0.B3.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D1.81_Razor-qt)
    *   [3.10 Показывать информацию об обновлениях пакетов](#.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D1.8B.D0.B2.D0.B0.D1.82.D1.8C_.D0.B8.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D1.8E_.D0.BE.D0.B1_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
    *   [3.11 Показывать прогноз погоды](#.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D1.8B.D0.B2.D0.B0.D1.82.D1.8C_.D0.BF.D1.80.D0.BE.D0.B3.D0.BD.D0.BE.D0.B7_.D0.BF.D0.BE.D0.B3.D0.BE.D0.B4.D1.8B)
    *   [3.12 Показывать RSS ленты](#.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D1.8B.D0.B2.D0.B0.D1.82.D1.8C_RSS_.D0.BB.D0.B5.D0.BD.D1.82.D1.8B)
    *   [3.13 Показывать рейтинг Arch Linux на Distrowatch](#.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D1.8B.D0.B2.D0.B0.D1.82.D1.8C_.D1.80.D0.B5.D0.B9.D1.82.D0.B8.D0.BD.D0.B3_Arch_Linux_.D0.BD.D0.B0_Distrowatch)
    *   [3.14 Показывать состояние rTorrent](#.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D1.8B.D0.B2.D0.B0.D1.82.D1.8C_.D1.81.D0.BE.D1.81.D1.82.D0.BE.D1.8F.D0.BD.D0.B8.D0.B5_rTorrent)
    *   [3.15 Показывать состояние вашего WordPress блога](#.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D1.8B.D0.B2.D0.B0.D1.82.D1.8C_.D1.81.D0.BE.D1.81.D1.82.D0.BE.D1.8F.D0.BD.D0.B8.D0.B5_.D0.B2.D0.B0.D1.88.D0.B5.D0.B3.D0.BE_WordPress_.D0.B1.D0.BB.D0.BE.D0.B3.D0.B0)
    *   [3.16 Показывать количество новых писем из Gmail](#.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D1.8B.D0.B2.D0.B0.D1.82.D1.8C_.D0.BA.D0.BE.D0.BB.D0.B8.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.BE_.D0.BD.D0.BE.D0.B2.D1.8B.D1.85_.D0.BF.D0.B8.D1.81.D0.B5.D0.BC_.D0.B8.D0.B7_Gmail)
        *   [3.16.1 Аналогичные способы](#.D0.90.D0.BD.D0.B0.D0.BB.D0.BE.D0.B3.D0.B8.D1.87.D0.BD.D1.8B.D0.B5_.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1.D1.8B)
    *   [3.17 Показывать новые письма (IMAP + SSL)](#.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D1.8B.D0.B2.D0.B0.D1.82.D1.8C_.D0.BD.D0.BE.D0.B2.D1.8B.D0.B5_.D0.BF.D0.B8.D1.81.D1.8C.D0.BC.D0.B0_.28IMAP_.2B_SSL.29)
    *   [3.18 Исправление прокручивания для кодировки UTF-8](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.87.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.B4.D0.BB.D1.8F_.D0.BA.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B8_UTF-8)
*   [4 Примеры конфигурации от пользователей](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8_.D0.BE.D1.82_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.B9)
    *   [4.1 Graysky](#Graysky)
    *   [4.2 Пример скрипта с поддержкой nvidia](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.D1.81.D0.BA.D1.80.D0.B8.D0.BF.D1.82.D0.B0_.D1.81_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.BE.D0.B9_nvidia)
*   [5 Замечание о шрифтах](#.D0.97.D0.B0.D0.BC.D0.B5.D1.87.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BE_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.B0.D1.85)
*   [6 Шрифты отображаются мельче, чем они должны быть](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D1.8E.D1.82.D1.81.D1.8F_.D0.BC.D0.B5.D0.BB.D1.8C.D1.87.D0.B5.2C_.D1.87.D0.B5.D0.BC_.D0.BE.D0.BD.D0.B8_.D0.B4.D0.BE.D0.BB.D0.B6.D0.BD.D1.8B_.D0.B1.D1.8B.D1.82.D1.8C)
*   [7 Универсальный способ включения настоящей прозрачности](#.D0.A3.D0.BD.D0.B8.D0.B2.D0.B5.D1.80.D1.81.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_.D0.B2.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D0.BE.D1.8F.D1.89.D0.B5.D0.B9_.D0.BF.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D0.BE.D1.81.D1.82.D0.B8)
*   [8 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка и настройка

*   [Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [conky](https://www.archlinux.org/packages/?name=conky) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").
*   Отредактируйте конфигурационный файл `~/.conkyrc`, используя пример конфигурации с [homeproject-screenshot](http://conky.sourceforge.net/screenshots.html)

Редактируя конфигурационный файл, вы сразу же сможете видеть результат внесённых изменений, как только сохраните его. Вам не нужно завершать/начинать ваш X сеанс. Поэтому лучше всего тестировать все опции по порядку, сохраняя конфигурационный файл и наблюдаяя за окном conky, и исправлять их, если они вам не понравились.

*   Либо используйте файл стандартной конфигурации `/etc/conky/conky.conf`:

```
$ cp /etc/conky/conky.conf ~/.conkyrc

```

Лучше использовать локальный `~/.conkyrc` конфигурационный файл. Как и многие приложения, *conky* сначала проверит, есть ли локальный файл `.conkyrc`. В случае его отсутствия *conky* прочитает файл по умолчанию из `/etc/conky`.

В случае, если вы храните вашу конфигурацию локально, например, в домашней директории, вы не сможете читать файлы логов, пока не внесете некоторые изменения. Одной из полезных функций *conky* является вывод на рабочий стол некоторых файлов из `/var/log/`, чтобы наблюдать за журнальными сообщениями. Большинство этих файлов может читать только `root`, вам придётся запускать *conky* через `sudo`. Однако, запуск *conky* с привилегиями `root` не рекомендуется, поэтому выполните следующие действия:

```
$ usermod -aG log *имя_пользователя*

```

Вы добавили пользователя `*имя_пользователя*` в группу `log`. Теперь `*имя_пользователя*` может читать файлы логов, и *conky* сможет отображать журнальные записи на рабочем столе.

*   В случае, если conky не принимает изменения, например, `minimum_size`, которые вы делаете в `~/.conkyrc`, убедитесь, что вы очистили `/etc/conky/conky.conf` или закомментировали соответствующюю секцию. Лучше всего удалить файлы из `/etc/conky/`, так как *conky* будет пытаться их читать и из-за этого выдавать вам некоторые сообщения об ошибках Xorg.

## Версии из AUR

В дополнение к обычному пакету *conky* есть ещё нескеолько [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") пакетов с разными опциями компиляции:

*   **conky-cli** — *Conky* без X11 зависимостей

	|| [conky-cli](https://aur.archlinux.org/packages/conky-cli/)

*   **conky-lua** — *Conky* с поддержкой Lua

	|| [conky-lua](https://aur.archlinux.org/packages/conky-lua/)

*   **conky-lua-nv** — *Conky* с поддержкой Lua и Nvidia

	|| [conky-lua-nv](https://aur.archlinux.org/packages/conky-lua-nv/)

*   **conky-nvidia** — *Conky* с поддержкой Nvidia

	|| [conky-nvidia](https://aur.archlinux.org/packages/conky-nvidia/)

## Советы и рекомендации

### Включить реальную прозрачность в KDE4 и Xfce4

Начиная с версии 1.8.0 *conky* поддерживает реальную прозрачность. Чтобы её включить, добавьте следующую строку в `~/.conkyrc`:

```
own_window_transparent yes

```

Предыдущая опция не совместима с опцией `OWN_WINDOW_ARGB_VISUAL yes`. Она заменяет [feh](https://www.archlinux.org/packages/?name=feh) метод, описанный ниже.

### Автозапуск в Xfce4

В файле `.conkyrc`:

```
background yes

```

Эта переменная запустит *conky* в фоновом режиме. Если вы хотите сделать окно всегда видимым на вашем рабочем столе, на всех рабочих местах и чтобы оно не отображалось на панели задач, добавьте следующие аргументы:

```
own_window yes
own_window_type override

```

Опция `override` делает ваше окно неконтролируемым из вашего оконного менеджера.

Напишите в `~/.config/autostart/conky.desktop`:

```
[Desktop Entry]
Encoding=UTF-8
Version=0.9.4
Type=Application
Name=conky
Comment=
Exec=conky -d
StartupNotify=false
Terminal=false
Hidden=false

```

### Как предотвратить мерцание

Чтобы предотвратить мерцание, *conky* требует поддержку Double Buffer Extension (DBE) со стороны X-сервера, потому что он не может достаточно быстро обновлять окно без этого. Поддержка DBE может быть включена в `/etc/X11/xorg.conf` добавлением строки `Load "dbe"` в разделе `"Module"`. Файл `xorg.conf` заменён (начиная с патча 1.8.x и выше) на `/etc/X11/xorg.conf.d`, который содержит отдельные конфигурационные файлы. *DBE* загружен автоматически.

Для включения double-buffer проверте наличие в `~/.conkyrc` строки:

```
# Place below the other options, not below TEXT or XY
double_buffer yes

```

### Настройка цвета

Помимо стандартных предопределённых цветов (white, black, yellow...), вы можете задать свой собственный цвет, используя название для кода цвета. Чтобы определить код нужного вам цвета, воспользуйтесь приложением для выбора цвета. Базовый пакет [gcolor2](https://www.archlinux.org/packages/?name=gcolor2) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") подскажет вам название цвета. Он состоит из шести шестнадцатеричных цифр (0-9, A-F). Добавьте такую строку в конфигурационный файл, чтобы задать собственные цвета:

```
color1     Имя_цвета_1
color2     Имя_цвета_2

```

Затем, при редактировании раздела `TEXT`, используйте собственный номер цвета, определённый ранее.

### С двумя экранами

При работе с двумя экранами, вам придётся поиграться с двумя опциями, чтобы разместить ваше окно *conky*. Предположим, у вас разрешение 1680X1050 и вы хотите, чтобы окно было на левом мониторе сверху по центру. Сделайте так:

```
alignment top_left
gap_X 840

```

Опция `alignment` отвечает за выравнивание, а опция `gap_X` определяет расстояние в пикселях от левой границы вашего экрана.

### Не сворачивать при сворачивании всех окон

**Используя Compiz:** Если кнопка 'Показать рабочий стол' или комбинация клавиш сворачивает *conky* вместе со всеми остальными окнами, запустите Compiz configuration settings manager, перейдите в "General Options" и снимите галочку с опции "Hide Skip Taskbar Windows".

Если вы не используете Compiz, попробуйте отредактировать `~/.conkyrc`, добавив/изменив следующую строку:

```
own_window_type override

```

или

```
own_window_type desktop

```

Обратитесь к странице справочного руководства (man) по *conky*, чтобы выяснить, чем они отличаются. Последний вариант позволяет изменять границы окна с помощью растягивания или сочетаний клавиш, например, в Openbox, а с первым вариантом так не получится.

### Интеграция с Gnome 3

У некоторых возникают проблемы с отображением *conky* в Gnome 3.

*   Добавьте эти строки в `~/.conkyrc`:

```
own_window yes
own_window_type conky
own_window_transparent yes
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

Если у вас всё ещё остались проблемы с прозрачностью, можете добавить следующие строки:

```
own_window_argb_visual yes
own_window_argb_value 255

```

### Интеграция с KDE

*Conky* с конфигурацией из примеров на странице со скриншотами создаёт проблему с отображением иконок. Итак, выполните следующее:

*   Добавьте эти строки в `~/.conkyrc`:

```
own_window yes
own_window_type normal
own_window_transparent yes
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

*   Если данная строка есть, закомментируйте или удалите её:

```
minimum_size

```

*   Для автозапуска *conky* создайте следующую символьную ссылку:

*   *   KDE4:

```
$ ln -s /usr/bin/conky ~/.kde4/Autostart/conkylink

```

*   *   KDE3:

```
$ ln -s /usr/bin/conky ~/.kde/share/autostart/conkylink

```

*   Установите пакет [feh](https://www.archlinux.org/packages/?name=feh) из официальных репозиториев.
*   Создайте скрипт для разрешения прозрачности с рабочим столом

Для пользователей KDE4 `~/.kde4/Autostart/fehconky`:

```
#!/bin/bash
feh --bg-scale "$(sed -n 's/wallpaper=//p' ~/.kde4/share/config/plasma-desktop-appletsrc)"

```

Для пользователей KDE3 `~/.kde/share/autostart/fehconky`:

```
#!/bin/bash
feh --bg-scale $(dcop kdesktop KBackgroundIface currentWallpaper 1)

```

используйте `--bg-center`, чтобы расположить фоновый рисунок по ценру.

*   Сделайте его исполняемым:
    *   KDE4:

```
$ chmod +x ~/.kde4/Autostart/fehconky

```

*   *   KDE3:

```
$ chmod +x ~/.kde/share/autostart/fehconky

```

*   По желанию, вместо использования скрипта, вы можете добавить подобную строку в самый низ файла `~/.conkyrc`
    *   Для KDE4

```
${exec feh --bg-scale "$(sed -n 's/wallpaper=//p' ~/.kde4/share/config/plasma-desktop-appletsrc)"}

```

*   *   Для KDE3

```
${exec feh --bg-scale $(dcop kdesktop KBackgroundIface currentWallpaper 1)}

```

### Интеграция с Razor-qt

С конфигурацией по умолчанию окно *conky* может исчезнуть с рабочего стола, если вы кликнете на букву. Добавьте эти строки в:

 `~/.conkyrc` 
```
own_window yes
own_window_class Conky
own_window_type normal
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager
own_window_transparent yes

```

### Показывать информацию об обновлениях пакетов

*   [Pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") предоставляет свой собственный скрипт, называемый `checkupdates`, который отображает обновления пакетов из официальных репозиториев. Используйте `${execpi 3600 checkupdates | wc -l}`, чтобы показать общее количество пакетов
*   [Paconky](https://bbs.archlinux.org/viewtopic.php?id=68104) - показывает информацию об обновлении пакета в формате, определённом пользователем. Вывод этой программы может быть включён в Conky с помощью команды `${execpi}`
*   [Прокручиваемые уведомления](https://bbs.archlinux.org/viewtopic.php?id=53761) - печатает прокручиваемые уведомления об обновлениях. От создателя *paconky*
*   [Perl Script](https://bbs.archlinux.org/viewtopic.php?id=57291) - более простой и древний скрипт от автора *paconky*. Печатает только количество пакетов, нуждающихся в обновлении
*   [Python Script](https://bbs.archlinux.org/viewtopic.php?id=37284) - хорошо настраиваемая программа для уведомления пользователя о наличии обновлений, написанная на [python](/index.php/Python_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Python (Русский)")
*   [Bash Script](https://bbs.archlinux.org/viewtopic.php?pid=483742#p483742) - [bash](/index.php/Bash "Bash")-скрипт для пользователей, которые включили ShowSize

### Показывать прогноз погоды

Смотрите [это обсуждение](https://bbs.archlinux.org/viewtopic.php?id=37381).

### Показывать RSS ленты

*Conky* имеет возможность отображать RSS-ленты самостоятельно, без необходимости применения внешних скриптов. Например, чтобы отображать заголовки десяти последних обновлений Planet Arch и обновлять ленту каждую минуту вы должны поместить это в ваш `~/.conkyrc` в раздел `TEXT`:

```
${rss [https://planet.archlinux.org/rss20.xml](https://planet.archlinux.org/rss20.xml) 1 item_titles 10 }

```

Если вы хотите отображать rss ленту форума Arch, добавьте следующую строку:

```
${rss [https://bbs.archlinux.org/extern.php?action=feed&type=rss](https://bbs.archlinux.org/extern.php?action=feed&type=rss) 1 item_titles 4}

```

где 1 - это интервал обновлений в минутах (15 мин по умолчанию), 4 - количество объектов, которые вы хотите отображать.

Ленты русскоязычного форума:

*   Последние сообщения: [http://archlinux.org.ru/forum/feeds/posts/](http://archlinux.org.ru/forum/feeds/posts/)
*   Последние темы: [http://archlinux.org.ru/forum/feeds/topics/](http://archlinux.org.ru/forum/feeds/topics/)

### Показывать рейтинг Arch Linux на Distrowatch

Смотрите [это обсуждение](https://bbs.archlinux.org/viewtopic.php?id=88779).

### Показывать состояние rTorrent

Смотрите [это обсуждение](https://bbs.archlinux.org/viewtopic.php?id=67304).

### Показывать состояние вашего WordPress блога

Вы можете это сделать, используя расширение, написанное на python [ConkyPress](http://evilshit.wordpress.com/2013/04/20/conkypress-a-wordpress-stats-visualization-tool-for-your-desktop/).

### Показывать количество новых писем из Gmail

Создайте файл `gmail.py` в удобнов месте (в данном примере в `~/.scripts/`) со следующем [python](/index.php/Python_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Python (Русский)")-кодом:

 `gmail.py` 
```
#!/usr/bin/env python

from urllib.request import FancyURLopener

email = 'ваш email' # @gmail.com can be left out
password  = 'ваш пароль'

url = 'https://%s:%s@mail.google.com/mail/feed/atom' % (email, password)

opener = FancyURLopener()
page = opener.open(url)

contents = page.read().decode('utf-8')

ifrom = contents.index('<fullcount>') + 11
ito   = contents.index('</fullcount>')

fullcount = contents[ifrom:ito]

print(fullcount + ' new')

```

Вы также можете использовать Python urllib, как описано ниже:

 `gmail.py` 
```
#! /usr/bin/env python

import urllib.request
from xml.etree import ElementTree as etree

# Enter your username and password below within quotes below, in place of ****.
# Set up authentication for gmail
auth_handler = urllib.request.HTTPBasicAuthHandler()
auth_handler.add_password(realm='New mail feed',
                          uri='https://mail.google.com/',
                          user= '****',
                          passwd= '****')
opener = urllib.request.build_opener(auth_handler)
# ...and install it globally so it can be used with urlopen.
urllib.request.install_opener(opener)

gmail = 'https://mail.google.com/gmail/feed/atom'
NS = '{http://purl.org/atom/ns#}'
with urllib.request.urlopen(gmail) as source:
    tree = etree.parse(source)
fullcount = tree.find(NS + 'fullcount').text

print(fullcount + ' new')

```

Добавьте следующую строку в ваш `~/.conkyrc`, чтобы проверять свой Gmail на предмет новых писем каждые пять минут (300 секунд) и показать их:

```
${execpi 300 python ~/.scripts/gmail.py}

```

#### Аналогичные способы

Всё то же самое, но используя `curl`, `grep` и `sed`:

```
$ curl -s -u '''email''':'''пароль''' https://mail.google.com/mail/feed/atom | grep fullcount | sed 's/<[^0-9]*>//g'

```

замените *email* и *пароль* на свои данные.

Также вы можете воспользоваться [stunnel](http://www.stunnel.org/), предоставленном в пакете [stunnel](https://www.archlinux.org/packages/?name=stunnel).

Следующая конфигурация взята из [FAQ по conky](http://conky.sourceforge.net/faq.html)

Измените `/etc/stunnel/stunnel.conf` как показано ниже, а затем запустите [демон](/index.php/Daemon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Daemon (Русский)") `stunnel`:

```
# Service-level configuration for TLS server
[imap]
client = yes
accept  = 143
connect = imap.gmail.com:143
protocol = imap
sslVersion = TLSv1
# Service-level configuration for SSL server
[imaps]
client = yes
accept  = 993
connect = imap.gmail.com:993

```

Теперь осталось только отредактировать `~/.conkyrc`:

```
imap localhost username * -i 120 -p 993
TEXT
Inbox: ${imap_unseen}/${imap_messages}

```

Здесь использована `*` вместо пароля для того, чтобы *сonky* его спрашивал, но вы **не** обязаны так делать.

### Показывать новые письма (IMAP + SSL)

*Conky* имеет встроенную поддержку IMAP аккаунтов, но не поддерживает SSL. Его может обеспечить следующий скрипт, взятый с [этого форума](http://www.unix.com/shell-programming-scripting/115322-perl-conky-gmail-imap-unread-message-count.html). Для этого требуются Perl/CPAN модули Mail::IMAPClient и IO::Socket::SSL, которые находятся в пакетах [perl-mail-imapclient](https://aur.archlinux.org/packages/perl-mail-imapclient/) и [perl-io-socket-ssl](https://www.archlinux.org/packages/?name=perl-io-socket-ssl).

Создайте файл `imap.pl` в месте, где его сможет прочитать *conky*. Добавьте следующее содержимое в этот файл, внеся соответствующие изменения:

```
#!/usr/bin/perl

# gimap.pl by gxmsgx
# description: get the count of unread messages on imap

use strict;
use Mail::IMAPClient;
use IO::Socket::SSL;

my $username = 'имя_пользователя'; 
my $password = 'пароль123'; 

my $socket = IO::Socket::SSL->new(
  PeerAddr => 'imap.server',
  PeerPort => 993
 )
 or die "socket(): $@";

my $client = Mail::IMAPClient->new(
  Socket   => $socket,
  User     => $username,
  Password => $password,
 )
 or die "new(): $@";

if ($client->IsAuthenticated()) {
   my $msgct;

   $client->select("INBOX");
   $msgct = $client->unseen_count||'0';
   print "$msgct
";
}

$client->logout();

```

Добавьте в `~/.conkyrc`:

```
${execpi 300 ~/.conky/imap.pl} 

```

или другое расположение, куда вы сохранили файл.

Если вы пользуетесь Gmail, вам может понадобиться [сгенерировать](http://www.google.com/accounts/IssuedAuthSubTokens?hide_authsub=1) пароль для конкретного приложения.

Также вы можете использовать stunnel, как описано выше: [#Показывать количество новых писем из Gmail](#.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D1.8B.D0.B2.D0.B0.D1.82.D1.8C_.D0.BA.D0.BE.D0.BB.D0.B8.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.BE_.D0.BD.D0.BE.D0.B2.D1.8B.D1.85_.D0.BF.D0.B8.D1.81.D0.B5.D0.BC_.D0.B8.D0.B7_Gmail)

### Исправление прокручивания для кодировки UTF-8

В текущей версии *conky* (1.9.0) замечена ошибка ([http://sourceforge.net/p/conky/bugs/341/](http://sourceforge.net/p/conky/bugs/341/)), из-за которой прокрутка текста производится по байтам, а не по символам, из-за чего в тексте, содержащем мультибайтные символы происходит их исчезновение и появление при прокрутке. Пакет, с исправлением данного бага можно установить из AUR: [conky-utfscroll](https://aur.archlinux.org/packages/conky-utfscroll/)

## Примеры конфигурации от пользователей

### Graysky

[Вот](https://raw.github.com/graysky2/configs/5fbe513918dfe8066f87e670108318464902afae/dotfiles/.conkyrc) оно - изменяйте под вашу систему. Оптимизировано для четырёх ядерного процессора с несколькими hdd (хотя один из них не подсоединён на скриншоте) и видеокарты nvidia. Вы легко можете изменить этот пример под двух- или однопроцессорную машину с одним или любым другим количеством hdd.

### Пример скрипта с поддержкой nvidia

```
# -- Conky settings -- #
background no
update_interval 1

cpu_avg_samples 2
net_avg_samples 2

override_utf8_locale yes

double_buffer yes
no_buffers yes

text_buffer_size 2048
imlib_cache_size 0

# -- Window specifications -- #

own_window yes
own_window_type normal
own_window_transparent yes
own_window_hints undecorate,sticky,skip_taskbar,skip_pager,below

border_inner_margin 0
border_outer_margin 0

minimum_size 320 800
maximum_width 320

alignment bottom_right
gap_x 0
gap_y 0

# -- Graphics settings -- #
draw_shades no
draw_outline no
draw_borders no
draw_graph_borders yes

# -- Text settings -- #
use_xft yes
xftfont MaiandraGD:size=24
xftalpha 0.4

uppercase no

default_color 888888

# -- Lua Load -- #
lua_load ~/conky/lua/lua.lua
lua_draw_hook_pre ring_stats

TEXT
${alignr}${voffset 53}${goto 90}${font MaiandraGD:size=11}${time %A, %d %B %Y}

${voffset 5}${goto 164}${font MaiandraGD:size=16}${time %H:%M}

${voffset -40}${goto 100}${font MaiandraGD:size=9}Kernel:${offset 70}Uptime:
${goto 90}${font MaiandraGD:size=9}$kernel${offset 40}$uptime
${voffset 57}${goto 117}${font snap:size=8}${cpu cpu0}%
${goto 117}${cpu cpu1}%
${goto 117}CPU
${voffset 19}${goto 145}${memperc}%
${goto 145}$swapperc%
${goto 145}MEM
${voffset 25}${goto 170}${nvidia gpufreq}
${goto 170}${nvidia memfreq}
${goto 170}GPU
${voffset 27}${goto 198}${totaldown ppp0}
${goto 198}${totalup ppp0}
${goto 205}NET
${voffset 21}
${goto 222}${fs_used /home}
${goto 230}DISK
```

И приложеный lua.lua скрипт:

```
--[[
 Ring Meters by londonali1010 (2009)

 This script draws percentage meters as rings. It is fully customisable; all options are described in the script.

 IMPORTANT: if you are using the 'cpu' function, it will cause a segmentation fault if it tries to draw a ring straight away. The if statement on line 145 uses a delay to make sure that this does not happen. It calculates the length of the delay by the number of updates since Conky started. Generally, a value of 5s is long enough, so if you update Conky every 1s, use update_num > 5 in that if statement (the default). If you only update Conky every 2s, you should change it to update_num > 3; conversely if you update Conky every 0.5s, you should use update_num > 10\. ALSO, if you change your Conky, is it best to use "killall conky; conky" to update it, otherwise the update_num will not be reset and you will get an error.

 To call this script in Conky, use the following (assuming that you save this script to ~/scripts/rings.lua):
         lua_load ~/scripts/rings-v1.2.1.lua
         lua_draw_hook_pre ring_stats

 Changelog:
 + v1.2.1 -- Fixed minor bug that caused script to crash if conky_parse() returns a nil value (20.10.2009)
 + v1.2 -- Added option for the ending angle of the rings (07.10.2009)
 + v1.1 -- Added options for the starting angle of the rings, and added the "max" variable, to allow for variables that output a numerical value rather than a percentage (29.09.2009)
 + v1.0 -- Original release (28.09.2009)
 ]]

 settings_table = {
         {
                 -- Edit this table to customise your rings.
                 -- You can create more rings simply by adding more elements to settings_table.
                 -- "name" is the type of stat to display; you can choose from 'cpu', 'memperc', 'fs_used_perc', 'battery_used_perc'.
                 name='time',
                 -- "arg" is the argument to the stat type, e.g. if in Conky you would write ${cpu cpu0}, 'cpu0' would be the argument. If you would not use an argument in the Conky variable, use ''.
                 arg='%I.%M',
                 -- "max" is the maximum value of the ring. If the Conky variable outputs a percentage, use 100.
                 max=12,
                 -- "bg_colour" is the colour of the base ring.
                 bg_colour=0x888888,
                 -- "bg_alpha" is the alpha value of the base ring.
                 bg_alpha=0.3,
                 -- "fg_colour" is the colour of the indicator part of the ring.
                 fg_colour=0x888888,
                 -- "fg_alpha" is the alpha value of the indicator part of the ring.
                 fg_alpha=0.5,
                 -- "x" and "y" are the x and y coordinates of the centre of the ring, relative to the top left corner of the Conky window.
                 x=191, y=145,
                 -- "radius" is the radius of the ring.
                 radius=32,
                 -- "thickness" is the thickness of the ring, centred around the radius.
                 thickness=4,
                 -- "start_angle" is the starting angle of the ring, in degrees, clockwise from top. Value can be either positive or negative.
                 start_angle=0,
                 -- "end_angle" is the ending angle of the ring, in degrees, clockwise from top. Value can be either positive or negative, but must be larger (e.g. more clockwise) than start_angle.
                 end_angle=360
         },
         {
                 name='time',
                 arg='%M.%S',
                 max=60,
                 bg_colour=0x888888,
                 bg_alpha=0.3,
                 fg_colour=0x888888,
                 fg_alpha=0.5,
                 x=191, y=145,
                 radius=37,
                 thickness=4,
                 start_angle=0,
                 end_angle=360
         },
         {
                 name='time',
                 arg='%S',
                 max=60,
                 bg_colour=0x888888,
                 bg_alpha=0.3,
                 fg_colour=0x888888,
                 fg_alpha=0.5,
                 x=191, y=145,
                 radius=42,
                 thickness=4,
                 start_angle=0,
                 end_angle=360
         },
         {
                 name='cpu',
                 arg='cpu0',
                 max=100,
                 bg_colour=0x888888,
                 bg_alpha=0.3,
                 fg_colour=0x888888,
                 fg_alpha=0.5,
                 x=140, y=300,
                 radius=26,
                 thickness=5,
                 start_angle=-90,
                 end_angle=180
         },
         {
                 name='cpu',
                 arg='cpu1',
                 max=100,
                 bg_colour=0x888888,
                 bg_alpha=0.3,
                 fg_colour=0x888888,
                 fg_alpha=0.5,
                 x=140, y=300,
                 radius=20,
                 thickness=5,
                 start_angle=-90,
                 end_angle=180
         },
         {
                 name='memperc',
                 arg='',
                 max=100,
                 bg_colour=0x888888,
                 bg_alpha=0.3,
                 fg_colour=0x888888,
                 fg_alpha=0.5,
                 x=170, y=350,
                 radius=26,
                 thickness=5,
                 start_angle=-90,
                 end_angle=180
         },
         {
                 name='swapperc',
                 arg='',
                 max=100,
                 bg_colour=0x888888,
                 bg_alpha=0.3,
                 fg_colour=0x888888,
                 fg_alpha=0.5,
                 x=170, y=350,
                 radius=20,
                 thickness=5,
                 start_angle=-90,
                 end_angle=180
         },
         {
                 name='time',
                 arg='%d',
                 max=31,
                 bg_colour=0x888888,
                 bg_alpha=0.3,
                 fg_colour=0x888888,
                 fg_alpha=0.5,
                 x=191, y=145,
                 radius=50,
                 thickness=5,
                 start_angle=-140,
                 end_angle=-30
         },
         {
                 name='time',
                 arg='%m',
                 max=12,
                 bg_colour=0x888888,
                 bg_alpha=0.3,
                 fg_colour=0x888888,
                 fg_alpha=0.5,
                 x=191, y=145,
                 radius=50,
                 thickness=5,
                 start_angle=30,
                 end_angle=140
         },
 --      {
 --              name='fs_used_perc',
 --              arg='/',
 --              max=100,
 --              bg_colour=0x888888,
 --              bg_alpha=0.3,
 --              fg_colour=0x888888,
 --              fg_alpha=0.5,
 --              x=260, y=503,
 --              radius=26,
 --              thickness=5,
 --              start_angle=-90,
 --              end_angle=180
 --      },
         {
                 name='fs_used_perc',
                 arg='/home',
                 max=100,
                 bg_colour=0x888888,
                 bg_alpha=0.3,
                 fg_colour=0x888888,
                 fg_alpha=0.5,
                 x=260, y=503,
                 radius=20,
                 thickness=5,
                 start_angle=-90,
                 end_angle=180
         },
         {
                 name='totalup',
                 arg='ppp0',
                 max=2,
                 bg_colour=0x888888,
                 bg_alpha=0.3,
                 fg_colour=0x888888,
                 fg_alpha=0.5,
                 x=230, y=452,
                 radius=20,
                 thickness=5,
                 start_angle=-90,
                 end_angle=180
         },
         {
                 name='totaldown',
                 arg='ppp0',
                 max=2,
                 bg_colour=0x888888,
                 bg_alpha=0.3,
                 fg_colour=0x888888,
                 fg_alpha=0.5,
                 x=230, y=452,
                 radius=26,
                 thickness=5,
                 start_angle=-90,
                 end_angle=180
         },
         {
                 name='nvidia',
                 arg='gpufreq',
                 max=475,
                 bg_colour=0x888888,
                 bg_alpha=0.3,
                 fg_colour=0x888888,
                 fg_alpha=0.5,
                 x=200, y=401,
                 radius=26,
                 thickness=5,
                 start_angle=-90,
                 end_angle=180
         },
 {
                 name='nvidia',
                 arg='memfreq',
                 max=700,
                 bg_colour=0x888888,
                 bg_alpha=0.3,
                 fg_colour=0x888888,
                 fg_alpha=0.5,
                 x=200, y=401,
                 radius=20,
                 thickness=5,
                 start_angle=-90,
                 end_angle=180
         },
 }

 require 'cairo'

 function rgb_to_r_g_b(colour,alpha)
         return ((colour / 0x10000) % 0x100) / 255., ((colour / 0x100) % 0x100) / 255., (colour % 0x100) / 255., alpha
 end

 function draw_ring(cr,t,pt)
         local w,h=conky_window.width,conky_window.height

         local xc,yc,ring_r,ring_w,sa,ea=pt['x'],pt['y'],pt['radius'],pt['thickness'],pt['start_angle'],pt['end_angle']
         local bgc, bga, fgc, fga=pt['bg_colour'], pt['bg_alpha'], pt['fg_colour'], pt['fg_alpha']

         local angle_0=sa*(2*math.pi/360)-math.pi/2
         local angle_f=ea*(2*math.pi/360)-math.pi/2
         local t_arc=t*(angle_f-angle_0)

         -- Draw background ring

         cairo_arc(cr,xc,yc,ring_r,angle_0,angle_f)
         cairo_set_source_rgba(cr,rgb_to_r_g_b(bgc,bga))
         cairo_set_line_width(cr,ring_w)
         cairo_stroke(cr)

         -- Draw indicator ring

         cairo_arc(cr,xc,yc,ring_r,angle_0,angle_0+t_arc)
         cairo_set_source_rgba(cr,rgb_to_r_g_b(fgc,fga))
         cairo_stroke(cr)
 end

 function conky_ring_stats()
         local function setup_rings(cr,pt)
                 local str=''
                 local value=0

                 str=string.format('${%s %s}',pt['name'],pt['arg'])
                 str=conky_parse(str)

                 value=tonumber(str)
                 if value == nil then value = 0 end
                 pct=value/pt['max']

                 draw_ring(cr,pct,pt)
         end

         if conky_window==nil then return end
         local cs=cairo_xlib_surface_create(conky_window.display,conky_window.drawable,conky_window.visual, conky_window.width,conky_window.height)

         local cr=cairo_create(cs)

         local updates=conky_parse('${updates}')
         update_num=tonumber(updates)

         if update_num>5 then
                 for i in pairs(settings_table) do
                         setup_rings(cr,settings_table[i])
                 end
         end
 end            

```

## Замечание о шрифтах

Большинство из наиболее красивых конфигураций `.conkyrc` используют шрифты PizzaDude Bullets и Pie Charts for Maps. Они доступны в AUR в пакетах [ttf-pizzadude-bullets](https://aur.archlinux.org/packages/ttf-pizzadude-bullets/) и [ttf-piechartsformaps](https://aur.archlinux.org/packages/ttf-piechartsformaps/) соответственно, или же вы можете найти и скачать их из интернета и установить вручную, как описано в статье [Шрифты](/index.php/%D0%A8%D1%80%D0%B8%D1%84%D1%82%D1%8B "Шрифты").

## Шрифты отображаются мельче, чем они должны быть

Если вы заметите, что шрифты в *conky* мельче, чем должны быть, или они неправильно выровнены, это может происходить из-за настройки по умолчанию в infinality freetype2 patch. Из-за этой настройки в некоторых программах шрифт отображается в 72 DPI, вместо 96, даже если в вашей системе установлено 96\. Если вы заметили проблему, откройте `/etc/fonts/infinality/infinality.conf`, найдите раздел о DPI и смените 72 на 96.

## Универсальный способ включения настоящей прозрачности

Прозрачность в *conky* ведёт себя упрямо, но есть универсальный способ включения настоящей прозрачности с любым окружением или оконным менеджером - использование *xcompmgr* и *transset-df*. [Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакеты [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr) и [transset-df](https://www.archlinux.org/packages/?name=transset-df) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Оба эти пакета имеют одинаковые зависимости, поэтому это самый легкий способ для компоновки, для тех кто использует отдельные оконные менеджеры для достижения минимальной установки (или по какой-либо другой причине :D)

**Примечание:** Это может привести к конфликту с другими композитными менеджерами, которые вы уже используете

Проверьте документацию *xcompmgr*, чтобы разобраться, какие композитные опции вы хотите применить. Вот стандартная команда:

```
$ xcompmgr -c -t-5 -l-5 -r4.2 -o.55 &

```

Убедитесь, что *conky* запущен с `conky &`. Используйте *transset-df*, чтобы включить прозрачность для окна *conky*. Установите '.5' в любое значение из диапазона 0 - 1:

```
$ transset-df .5 -n Conky

```

Это сделает окно *conky* по-настоящему прозрачным. Если у вас возникает ошибка типа:

 `$ transset-df .5 -n Conky`  `No Window matching Conky exists!` 

Проверьте, что *conky* запущен и, используя *xprop*, нажмите на окно *conky*, чтобы узнать название, которое вы должны вписать в `transset-df`:

 `$ xprop | grep WM_NAME`  `WM_NAME(STRING) = "Conky (ArchitectLinux)"` 

В данном случае подошло *conky*, но у вас оно может отличаться, поэтому убедитесь, что вы использовали своё значение. Если в `~/.conkyrc` написано `own_window_type panel`, тогда этот вызов xprop может сейчас выводить. Попробуйте использовать какую-нибудь из следующих опций: `own_window_type {dock,normal,override,desktop}`.

Напишите в `~/.xinitrc` следующие строки, чтобы *conky* был прозрачным при запуске `startx`:

```
xcompmgr -c -t-5 -l-5 -r4.2 -o.55 &
conky -d; sleep 1 && transset-df .5 -n Conky

```

## Смотрите также

*   [Конфигурация сonky на официальном сайте](http://conky.sourceforge.net/config_settings.html)
*   [Конфигурация сonky на Arch форумах](https://bbs.archlinux.org/viewtopic.php?id=39906)
*   [Официальный сайт](http://conky.sourceforge.net/)
*   [Conky](http://freshmeat.net/projects/conky/) на [Freshmeat](https://en.wikipedia.org/wiki/Freshmeat "wikipedia:Freshmeat")
*   [Conky](http://sourceforge.net/projects/conky/) на [SourceForge](https://en.wikipedia.org/wiki/sourceforge.net "wikipedia:sourceforge.net")
*   [#conky](irc://chat.freenode.org/conky) IRC чат канал на [freenode](https://en.wikipedia.org/wiki/Freenode "wikipedia:Freenode")
*   [FAQ](http://novel.evilcoder.org/wiki/index.php?title=ConkyFAQ&oldid=12463)