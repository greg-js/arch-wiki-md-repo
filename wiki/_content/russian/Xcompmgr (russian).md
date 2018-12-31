Ссылки по теме

*   [Compiz (Русский)](/index.php/Compiz_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Compiz (Русский)")
*   [Compton (Русский)](/index.php/Compton_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Compton (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [Xcompmgr](/index.php/Xcompmgr "Xcompmgr"). Дата последней синхронизации: 9 февраля 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Xcompmgr&diff=0&oldid=527757).

[Xcompmgr](http://cgit.freedesktop.org/xorg/app/xcompmgr/) - это простой [композитный менеджер окон](https://en.wikipedia.org/wiki/ru:%D0%9A%D0%BE%D0%BC%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80_%D0%BE%D0%BA%D0%BE%D0%BD "wikipedia:ru:Композитный менеджер окон"), умеющий рендерить тени, создавать примитивную прозрачность окон посредством **transset**. Разработан исключительно как доказательство концепции, Xcompmgr - легковесная альтернатива Compiz и ему подобных композитных менеджеров.

Так как Xcompmgr не заменяет любой существующий оконный менеджер, он является идеальным решением для пользователей, использующих легковесные [оконные менеджеры](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)") и желающих создать более элегантный рабочий стол.

## Contents

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 Прозрачность окон](#Прозрачность_окон)
*   [3 Советы и рекомендации](#Советы_и_рекомендации)
    *   [3.1 Запуск/остановка Xcompmgr по требованию](#Запуск/остановка_Xcompmgr_по_требованию)
    *   [3.2 Переключатель Xcompmgr](#Переключатель_Xcompmgr)
*   [4 Решение проблем](#Решение_проблем)
    *   [4.1 Mozilla Firefox падает при заходе на сайт с Flash](#Mozilla_Firefox_падает_при_заходе_на_сайт_с_Flash)
    *   [4.2 Фон становится светло-серым после входа в систему (например, в Openbox)](#Фон_становится_светло-серым_после_входа_в_систему_(например,_в_Openbox))
    *   [4.3 BadPicture request в awesome](#BadPicture_request_в_awesome)
    *   [4.4 Не обновляется экран в awesome после изменения разрешения](#Не_обновляется_экран_в_awesome_после_изменения_разрешения)

## Установка

Перед установкой Xcompmgr убедитесь в том, что [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)") [установлен](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BB%D0%B5%D0%BD "Установлен") и правильно настроен. Чтобы убедиться в том, что расширение [Composite](/index.php/Composite "Composite") для X Server включено, выполните:

 `$ xdpyinfo | grep Composite`  `Composite` 

Если вывод отсутствует, добавьте `Composite` в раздел `Extensions` в xorg.conf:

 `/etc/X11/xorg.conf` 
```
Section "Extensions"
        Option  "Composite" "true"
EndSection
```

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr). Для прозрачности [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [transset-df](https://www.archlinux.org/packages/?name=transset-df). Для примера смотрите [Xterm#Automatic transparency](/index.php/Xterm#Automatic_transparency "Xterm").

## Настройка

Запуск `xcompmgr`:

```
$ xcompmgr -c

```

Чтобы запускать `xcompmgr` при старте сессии, добавьте в [xprofile](/index.php/Xprofile_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xprofile (Русский)"):

```
xcompmgr -c &

```

Вы можете экспериментировать с параметрами, чтобы изменить отбрасывание теней или даже включить затухание. Например:

```
xcompmgr -c -t-5 -l-5 -r4.2 -o.55 &

```

Получение полного списка опций:

```
$ xcompmgr --help

```

### Прозрачность окон

Практическое применение ограничено из-за низкой производительности, но можно использовать `transset-df` для установки прозрачности отдельных окон.

Чтобы установить прозрачность окна программы, убедитесь в том, что она запущена, затем выполните:

```
$ transset-df *прозрачность*

```

где *прозрачность* - это число от 0 до 1, где 0 - абсолютная прозрачность, 1 - непрозрачность.

Курсор превратится в крест, наведите его на требуемую программу. Например, `transset-df 0.25` установит непрозрачность на уровне 25% (75% прозрачности).

## Советы и рекомендации

### Запуск/остановка Xcompmgr по требованию

Этот скрипт позволяет легко запустить, перезапустить и остановить композитный менеджер.

 `~/.bin/comp` 
```
#!/bin/bash
#
# Start a composition manager.
# (xcompmgr in this case)

comphelp() {
    echo "Composition Manager:"
    echo "   (re)start: COMP"
    echo "   stop:      COMP -s"
    echo "   query:     COMP -q"
    echo "              returns 0 if composition manager is running, else 1"
    exit
}

checkcomp() {
    pgrep xcompmgr &>/dev/null
}

stopcomp() {
    checkcomp && killall xcompmgr
}

startcomp() {
    stopcomp
    # Example settings only. Replace with your own.
    xcompmgr -CcfF -I-.015 -O-.03 -D6 -t-1 -l-3 -r4.2 -o.5 &
    exit
}

case "$1" in
    "")   startcomp ;;
    "-q") checkcomp ;;
    "-s") stopcomp; exit ;;
    *)    comphelp ;;
esac

```

Для удобства использования можно назначить скрипт на горячую клавишу, используя, например, [Xbindkeys](/index.php/Xbindkeys_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xbindkeys (Русский)"). Это позволит перезапускать или временно приостанавливать Xcompmgr в случае необходимости, не прерывая работу.

### Переключатель Xcompmgr

Назначьте следующий скрипт на любую горячую клавишу:

```
#!/bin/bash

if pgrep xcompmgr &>/dev/null; then
    echo "Turning xcompmgr ON"
    xcompmgr -c -C -t-5 -l-5 -r4.2 -o.55 &
else
    echo "Turning xcompmgr OFF"
    pkill xcompmgr &
fi

exit 0

```

## Решение проблем

### Mozilla Firefox падает при заходе на сайт с Flash

Вы можете исправить это путем создания файла `/etc/profile.d/flash.sh`, который должен содержать следующее:

```
export XLIB_SKIP_ARGB_VISUALS=1

```

**Важно:** Это отключит композитные эффекты.

### Фон становится светло-серым после входа в систему (например, в Openbox)

Эта ошибка исправляется [установкой](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [hsetroot](https://www.archlinux.org/packages/?name=hsetroot) и настройки цвета фона посредством `hsetroot -solid "#000000"` (просто введите код цвета, который вы хотите вместо *#000000*) перед `xcompmgr`. Если `xcompmgr` запускается до `exec` в `~/.xinitrc`, то вы можете заменить `xcompmgr &` на `(sleep 1 && xcompmgr) &`; это позволит `xcompmgr` запускаться после старта оконного менеджера.

### BadPicture request в awesome

Если вы получаете следующую ошибку в [awesome](/index.php/Awesome_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Awesome (Русский)"):

```
 error 163: BadPicture request 149 minor 8 serial 34943
 error 163: BadPicture request 149 minor 8 serial 34988
 error 163: BadPicture request 149 minor 8 serial 35033

```

просто установите [feh](/index.php/Feh_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Feh (Русский)") и перезапустите [awesome](/index.php/Awesome_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Awesome (Русский)").

### Не обновляется экран в awesome после изменения разрешения

При использовании внешнего монитора могут возникнуть проблемы при автоматическом изменении разрешения экрана: часть экрана становится "застывшей" и больше не обновляется. Эта проблема возникает из-за первоначального изменения разрешения (которое происходит перед стартом Xcompmgr), а также при установке фона в [awesome](/index.php/Awesome_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Awesome (Русский)") посредством [feh](/index.php/Feh_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Feh (Русский)").

Чтобы исправить это, вам нужно [установить](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [hsetroot](https://www.archlinux.org/packages/?name=hsetroot) и добавить следующую строчку в `.xinitrc` перед `xcompmgr`:

```
hsetroot -solid "#000066"

```

(можно заменить *#000066* на любой другой цвет).