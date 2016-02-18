[mpv](http://mpv.io/) — мультимедийный плеер, основанный на [mplayer](http://www.mplayerhq.hu/design7/news.html) и mplayer2\. Плеер поддерживает обширный набор видеоформатов, аудио- и видеокодеков и форматов субтитров. Всеобъемлющий (однако не исчерпывающий) список различий между *mpv* и вышеупомянутыми плеерами доступен [тут](https://github.com/mpv-player/mpv/blob/master/DOCS/man/changes.rst).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Графические оболочки](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [3 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.1 Аппаратное декодирование](#.D0.90.D0.BF.D0.BF.D0.B0.D1.80.D0.B0.D1.82.D0.BD.D0.BE.D0.B5_.D0.B4.D0.B5.D0.BA.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [3.2 Воспроизведение с предыдущего места](#.D0.92.D0.BE.D1.81.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81_.D0.BF.D1.80.D0.B5.D0.B4.D1.8B.D0.B4.D1.83.D1.89.D0.B5.D0.B3.D0.BE_.D0.BC.D0.B5.D1.81.D1.82.D0.B0)
    *   [3.3 Звук слишком тихий](#.D0.97.D0.B2.D1.83.D0.BA_.D1.81.D0.BB.D0.B8.D1.88.D0.BA.D0.BE.D0.BC_.D1.82.D0.B8.D1.85.D0.B8.D0.B9)
    *   [3.4 Быстрое переключение между соотношениями сторон](#.D0.91.D1.8B.D1.81.D1.82.D1.80.D0.BE.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.B5.D0.B6.D0.B4.D1.83_.D1.81.D0.BE.D0.BE.D1.82.D0.BD.D0.BE.D1.88.D0.B5.D0.BD.D0.B8.D1.8F.D0.BC.D0.B8_.D1.81.D1.82.D0.BE.D1.80.D0.BE.D0.BD)
    *   [3.5 Отрисовка на корневом окне](#.D0.9E.D1.82.D1.80.D0.B8.D1.81.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BD.D0.B0_.D0.BA.D0.BE.D1.80.D0.BD.D0.B5.D0.B2.D0.BE.D0.BC_.D0.BE.D0.BA.D0.BD.D0.B5)
    *   [3.6 Использование как плагин браузера](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BA.D0.B0.D0.BA_.D0.BF.D0.BB.D0.B0.D0.B3.D0.B8.D0.BD_.D0.B1.D1.80.D0.B0.D1.83.D0.B7.D0.B5.D1.80.D0.B0)
    *   [3.7 Использование mpv для проигрывания музыки](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_mpv_.D0.B4.D0.BB.D1.8F_.D0.BF.D1.80.D0.BE.D0.B8.D0.B3.D1.80.D1.8B.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.BC.D1.83.D0.B7.D1.8B.D0.BA.D0.B8)
    *   [3.8 Просмотр стримов](#.D0.9F.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_.D1.81.D1.82.D1.80.D0.B8.D0.BC.D0.BE.D0.B2)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [mpv](https://www.archlinux.org/packages/?name=mpv) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") или [mpv-git](https://aur.archlinux.org/packages/mpv-git/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

### Графические оболочки

*mpv* предоставляет элегантный интерфейс OSC, появляющийся при движении курсора. Однако, существуют также графические интерфейсы, рассчитанные на более обширную аудиторию:

*   **Baka MPlayer** — Мультимедийный плеер, основанный на libmpv. Qt 5.

	[https://github.com/u8sand/Baka-MPlayer/](https://github.com/u8sand/Baka-MPlayer/) || [baka-mplayer-git](https://aur.archlinux.org/packages/baka-mplayer-git/)

*   **CMPlayer** — Продвинутый и лёгкий мультимедийный плеер. Qt 5.

	[https://cmplayer.github.io/](https://cmplayer.github.io/) || [cmplayer](https://aur.archlinux.org/packages/cmplayer/), [cmplayer-git](https://aur.archlinux.org/packages/cmplayer-git/)

*   **[SMPlayer](https://en.wikipedia.org/wiki/SMPlayer "wikipedia:SMPlayer")** — Мультимедийный плеер с дополнительным функционалом (CSS темы, интеграция с YouTube и другое) (Qt 5).

	[http://smplayer.sourceforge.net/](http://smplayer.sourceforge.net/) || [smplayer](https://www.archlinux.org/packages/?name=smplayer)

**Обратите внимание:** Пакеты CMPlayer включают в себя также и сам *mpv*

## Настройка

Настройки Mpv находятся в файлах `mpv.conf` (общие) и `input.conf` (сочетания клавиш). Если не установлена [переменная окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `XDG_CONFIG_HOME`, будут использоваться файлы настроек пользователя, расположенные в каталоге `~/.config/mpv`. Системные файлы настроек располагаются в `/etc/mpv`.

## Советы и рекомендации

### Аппаратное декодирование

В отличие от *mplayer* и *mplayer2*, *mpv* имеет встроенную поддержку [VA-API](/index.php/VA-API_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "VA-API (Русский)") и [VDPAU](/index.php/VDPAU_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "VDPAU (Русский)"). Указать способ декодирования вы можете, запустив *mpv* с опцией `--hwdec=*метод*`. Полный список всех доступных методов вы найдете в [man-странице](/index.php/Man_page_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Man page (Русский)") `mpv (1)`, поискав описание опции `--hwdec=<api>`. Чтобы не указывать метод при каждом запуске mpv, добавьте опцию `hwdec=*метод*` в ваш файл настроек. Используя аппаратное декодирование, вывод видео должен быть установлен как `opengl`, `opengl-hq` или `vdpau` (если указано `hwdec=vdpau`). Использование `vo=vaapi` с недавних пор не рекомендуется [[1]](https://github.com/mpv-player/mpv/blob/master/DOCS/man/vo.rst). Если аппаратное декодирование недоступно, *mpv* автоматически переключится на программное декодирование. Подробную информацию вы можете найти на страницах [options.rst](https://github.com/mpv-player/mpv/blob/master/DOCS/man/options.rst) и [vo.rst](https://github.com/mpv-player/mpv/blob/master/DOCS/man/vo.rst).

### Воспроизведение с предыдущего места

Стандартной комбинацией клавиш для выхода из *mpv* с сохранением текущей позиции является `Shift+q`. Это можно изменить, добавив строку `quit_watch_later` в файл настроек сочетаний клавиш.

### Звук слишком тихий

Установите параметр `softvol-max=*значение*` в вашем файле настроек на желаемый уровень, например `softvol-max=600`. Дополнительно (или вместо этого), вы можете воспользоваться [компрессором аудиосигнала](https://en.wikipedia.org/wiki/ru:%D0%9A%D0%BE%D0%BC%D0%BF%D1%80%D0%B5%D1%81%D1%81%D0%BE%D1%80_%D0%B0%D1%83%D0%B4%D0%B8%D0%BE%D1%81%D0%B8%D0%B3%D0%BD%D0%B0%D0%BB%D0%B0 "wikipedia:ru:Компрессор аудиосигнала") с `af=drc`.

### Быстрое переключение между соотношениями сторон

Добавьте следующую строку в ваш файл `input.conf`:

```
F2 cycle_values video-aspect "16:9" "16:10" "4:3" "2.35:1" "-1"

```

Теперь вы cможете переключаться между перечисленными соотношениями сторон по нажатию `F2`.

### Отрисовка на корневом окне

Запустите *mpv* с опцией `--wid=0 файл.mp4`. Таким образом *mpv* будет отрисован в фоне экрана (окне с идентификатором 0).

### Использование как плагин браузера

С помощью [mozplugger](https://aur.archlinux.org/packages/mozplugger/) *mpv* можно использовать для воспроизведения видео в поддерживаемых браузерах. Инструкции по настройке смотрите на странице [Browser plugins#MozPlugger](/index.php/Browser_plugins#MozPlugger "Browser plugins"). Плагин в связке с пользовательским скриптом [ViewTube](http://isebaro.com/viewtube/?ln=en) позволяет использовать *mpv* для просмотра видео на различных сайтах, заменяя интегрированный в сайт плеер.

### Использование mpv для проигрывания музыки

Разработка скриптов Lua в *mpv* по состоянию на 30 ноября 2014 не имеет формальной документации, но есть примеры в [TOOLS/lua](https://github.com/mpv-player/mpv/tree/master/TOOLS/lua) из [репозитория mpv](https://github.com/mpv-player/mpv). А [в этой статье](https://bamos.github.io/2014/07/05/mpv-lua-scripting/) представлен скрипт [music.lua](https://github.com/bamos/dotfiles/blob/master/.mpv/lua/music.lua), в котором показано, как при помощи скриптов добавить функциональность в *mpv*, которая делает его удобнее в качестве проигрывателя музыки.

### Просмотр стримов

Смотрите [Livestreamer](/index.php/Livestreamer "Livestreamer").