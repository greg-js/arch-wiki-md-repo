# Feh (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Ссылки по теме

*   [Nitrogen (Русский)](/index.php/Nitrogen_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nitrogen (Русский)")
*   [sxiv](/index.php/Sxiv "Sxiv")

**Состояние перевода:** На этой странице представлен перевод статьи [GnuPG](/index.php/GnuPG "GnuPG"). Дата последней синхронизации: 13 декабря 2015‎‎. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=GnuPG&diff=0&oldid=394158).

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

[Feh](https://derf.homelinux.org/~derf/projects/feh/) это лёгкий и мощный просмотрщик изображений, который также может управлять фоном рабочего стола для оконных менеджеров, не умеющих делать это самостоятельно.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [2.1 Как просмотрщик изображений](#.D0.9A.D0.B0.D0.BA_.D0.BF.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80.D1.89.D0.B8.D0.BA_.D0.B8.D0.B7.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
        *   [2.1.1 Более удобный просмотр изображений](#.D0.91.D0.BE.D0.BB.D0.B5.D0.B5_.D1.83.D0.B4.D0.BE.D0.B1.D0.BD.D1.8B.D0.B9_.D0.BF.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_.D0.B8.D0.B7.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [2.2 Как менеджер фона рабочего стола](#.D0.9A.D0.B0.D0.BA_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80_.D1.84.D0.BE.D0.BD.D0.B0_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
*   [3 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.1 Просмотр SVG изображений](#.D0.9F.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_SVG_.D0.B8.D0.B7.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [3.2 Случайный фон рабочего стола](#.D0.A1.D0.BB.D1.83.D1.87.D0.B0.D0.B9.D0.BD.D1.8B.D0.B9_.D1.84.D0.BE.D0.BD_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
        *   [3.2.1 Использование скрипта](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.BA.D1.80.D0.B8.D0.BF.D1.82.D0.B0)
            *   [3.2.1.1 Для двух экранов no-xinerama](#.D0.94.D0.BB.D1.8F_.D0.B4.D0.B2.D1.83.D1.85_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BE.D0.B2_no-xinerama)
        *   [3.2.2 Используя cron](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_cron)
        *   [3.2.3 Используя пользовательсую сессию systemd](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D1.83.D1.8E_.D1.81.D0.B5.D1.81.D1.81.D0.B8.D1.8E_systemd)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [feh](https://www.archlinux.org/packages/?name=feh)

## Использование

Feh имеет множество настроек. Для получения полного списка опций, выполните `feh --help`.

### Как просмотрщик изображений

Чтобы быстро просматривать изображения в определенном каталоге, вы можете запустить feh со следующими параметрами:

```
$ feh -g 640x480 -d -S filename /path/to/directory

```

*   Ключ `-g` используется для просмотра изображений в разрешении 640x480
*   Ключ `-d` отображает имя файла
*   Ключ `-S filename` сортирует изображения по их названию

Это всего лишь один пример; есть много других вариантов для большей гибкости.

#### Более удобный просмотр изображений

Если открывать изображение с помощью feh из файлового менеджера, то, чтобы просмотреть все изображения в каталоге вам прийдется или открывать непосредственно каждый файл по очереди, или выделить все файлы, а затем открыть их. Это очень некомфортно.

Данный скрипт способен обойти эти неудобства.

 `feh_browser.sh` 

```
#!/bin/bash

shopt -s nullglob

if [[ ! -f $1 ]]; then
	echo "$0: first argument is not a file" >&2
	exit 1
fi

file=$(basename -- "$1")
dir=$(dirname -- "$1")
arr=()
shift

cd -- "$dir"

for i in *; do
	[[ -f $i ]] || continue
	arr+=("$i")
	[[ $i == $file ]] && c=$((${#arr[@]} - 1))
done

exec feh "$@" -- "${arr[@]:c}" "${arr[@]:0:c}"

```

Скрипт принимает первый аргумент, как имя файла.

Запустите скрипт с путем до выбранного изображения с любыми дополнительными параметрами. Пример запуска, который вы можете использовать в своем файловом менеджере:

 `$ /path/to/script/feh_browser.sh %f -F -Z` 

`-F` и `-Z` аргументы feh. `-F` открывает изображения в полноэкранном режиме, а `-Z` автоматически масштабирует. Добавление ключа `-q` (quiet) предотвращает спам сообщениями об ошибках, когда feh пытается открыть не изображения из текущего каталога.

Простая, но менее функциональная альтернатива:

 `feh_browser.sh` 

```
#! /bin/sh
feh -. "$(dirname "$1")" --start-at "$1"

```

Этот скрипт не имеет возможности принимать какие-либо дополнительные параметры.

### Как менеджер фона рабочего стола

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**Информация в этой статье или разделе устарела**

**Причина:** GNOME Files больше не управляет рабочим столом (его обрабатыает GNOME Shell) и Files больше не используют GConf. Информация о Gnome требует переработки или удаления. ([Обсудить](https://wiki.archlinux.org/index.php/Talk:Feh_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

Feh может управлять обоями рабочего стола для оконных менеджеров, не имеющих такой функции, таких как [Openbox](/index.php/Openbox "Openbox") и [Fluxbox](/index.php/Fluxbox "Fluxbox").

При использовании [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)"), Вы должны отключить управление рабочим столом в [GNOME Files](/index.php/GNOME_Files "GNOME Files"). Самый быстрый способ сделать это:

```
$ gconftool-2 --set /apps/nautilus/preferences/show_desktop --type boolean false

```

Эта команда является примером для установки фона рабочего стола:

```
$ feh --bg-scale /path/to/image.file

```

Другие варианты опций:

```
--bg-tile FILE
--bg-center FILE
--bg-seamless FILE

```

Для сохранения фона в следующих сессиях, добавьте команду в автозагрузку (например `~/.xinitrc`, `~/.config/openbox/autostart.sh`, и т.д.):

```
sh ~/.fehbg &

```

Чтобы изменить фоновое изображение, измените `~/.fehbg`, который будет создан после выполнения команды `feh --bg-scale /path/to/image.file` упомянутой выше.

## Советы и рекомендации

#### Просмотр SVG изображений

 `$ feh --magick-timeout 1 file.svg` 

Обратите внимание, что вам нужен [imagemagick](https://www.archlinux.org/packages/?name=imagemagick)

### Случайный фон рабочего стола

Вы можете заставить feh ставить случайные обои используя опцию `--randomize` с одной из `--bg-foo` опцией, пример:

 `$ feh --randomize --bg-fill ~/.wallpaper/*` 

Команда выше говорит feh'у перемешать список файлов в каталоге `~/.wallpaper/` и установить фоны для всех доступных рабочих столов. В этом случае берется первое изображение из перемешанного списка (одно уникальное изображение на каждый рабочий стол). Вы также можете сделать это рекурсивно, если ваш каталог с обоями содержит подкаталоги:

 `$ feh --recursive --randomize --bg-fill ~/.wallpaper` 

Чтобы получать для каждой сессии разные случайные обои из `~/.wallpaper`, добавьте следующее в ваш `.xinitrc`:

 `$ feh --bg-max --randomize ~/.wallpaper/* &` 

Другой способ устанавливать случайные обои для каждой x.org сессии - отредактируйте ваш `.fehbg`, как показано ниже:

 `$HOME/.fehbg` 

```
 feh --bg-max --randomize --no-fehbg ~/.wallpaper/* 

```

Для периодической смены обоев используйте скрипт, cron или systemd для выполнения команды с желаемым интервалом.

#### Использование скрипта

Для случайного изменения обоев, создайте скрипт на примере приведённого кода (например `wallpaper.sh`). Сделайте скрипт исполняемым и вызывайте его из `~/.xinitrc`. Вы можете поместить код непосредственно в `~/.xinitrc`, а не отдельным файлом.

Измените каталог `~/.wallpaper` в соответствии с вашими настройками, также можно указать задержку `15m`, по вашему желанию (смотрите `man sleep` для опций).

 `wallpaper.sh` 

```
#!/bin/sh

while true; do
	find ~/.wallpaper -type f \( -name '*.jpg' -o -name '*.png' \) -print0 |
		shuf -n1 -z | xargs -0 feh --bg-max
	sleep 15m
done

```

Замените `find ~/.wallpaper` на `find ~/.wallpaper/`, если код выше не работает.

Эта версия не создает так много форков, но она не работает рекурсивно по каталогам:

 `wallpaper.sh` 

```
#!/bin/bash

shopt -s nullglob
cd ~/.wallpaper

while true; do
	files=()
	for i in *.jpg *.png; do
		[[ -f $i ]] && files+=("$i")
	done
	range=${#files[@]}

	((range)) && feh --bg-scale "${files[RANDOM % range]}"

	sleep 15m
done

```

##### Для двух экранов no-xinerama

Этот скрипт заменяет вызов feh для добавления обоев на системах с двумя экранами nvidia twinview (для например):

 `wallpaper.sh` 

```
#!/bin/sh
exec feh --bg-max --no-xinerama "$@"

```

#### Используя cron

Используя [cron](/index.php/Cron "Cron"), вы получите схожий результат и это не требует все время держать скрипт, который большее время спит.

Выполните `$ crontab -e` и добавьте:

```
* * * * *  DISPLAY=:0.0 feh --bg-max "$(find ~/.wallpaper/|shuf -n1)"

```

#### Используя пользовательсую сессию systemd

**Обратите внимание:** Это пригодно **только** если вы используете _пользовательскую сессию systemd_. Прочитайте [Systemd/User](/index.php/Systemd/User "Systemd/User") для дополнительной информации.

Создайте юнит service:

 `$HOME/.config/systemd/user/feh-wallpaper.service` 

```
[Unit]
Description=Random wallpaper with feh

[Service]
Type=oneshot
EnvironmentFile=%h/.wallpaper
ExecStart=/bin/bash -c '/usr/bin/feh --bg-max "$(find ${WALLPATH}|shuf|head -n 1)"'

[Install]
WantedBy=default.target

```

Теперь создайте юнит таймера. При необходимости измените время. В это примере `15 секунд`:

 `$HOME/.config/systemd/user/feh-wallpaper.timer` 

```
[Unit]
Description=Random wallpaper with feh

[Timer]
OnUnitActiveSec=_15s_
Unit=feh-wallpaper.service

[Install]
WantedBy=default.target

```

В этом примере файл конфигурации является скрым файлом в домашнем каталоге и содержит в себе путь к каталогу с вашими изображениями

 `$HOME/.wallpaper` 

```
WALLPATH=_/home/user/.wallpaper/_

```

Активируйте `feh-wallpaper.timer` и `feh-wallpaper.service`. Читайте [Daemons (Русский)](/index.php/Daemons_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Daemons (Русский)") для дополнительной информации.

## Смотрите также

*   [Пост на форуме с оригинальным скриптом feh_browser (англ.)](https://bbs.archlinux.org/viewtopic.php?pid=884635#p884635)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Feh_(Русский)&oldid=411835](https://wiki.archlinux.org/index.php?title=Feh_(Русский)&oldid=411835)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Graphics and desktop publishing (Русский)](/index.php/Category:Graphics_and_desktop_publishing_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Graphics and desktop publishing (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")