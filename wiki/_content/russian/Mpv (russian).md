Ссылки по теме

*   [MPlayer (Русский)](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MPlayer (Русский)")

[mpv](http://mpv.io/) — мультимедийный плеер, основанный на [mplayer](http://www.mplayerhq.hu/design7/news.html) и mplayer2\. Плеер поддерживает обширный набор видеоформатов, аудио- и видеокодеков и форматов субтитров. Всеобъемлющий (однако не исчерпывающий) список различий между *mpv* и вышеупомянутыми плеерами доступен [тут](https://github.com/mpv-player/mpv/blob/master/DOCS/man/changes.rst).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Графические оболочки](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Пример файла input.conf](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_input.conf)
    *   [2.2 mpv и управление PulseAudio/ALSA mixer'ом с версии 0.18.1](#mpv_.D0.B8_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_PulseAudio.2FALSA_mixer.27.D0.BE.D0.BC_.D1.81_.D0.B2.D0.B5.D1.80.D1.81.D0.B8.D0.B8_0.18.1)
*   [3 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.1 Аппаратное декодирование](#.D0.90.D0.BF.D0.BF.D0.B0.D1.80.D0.B0.D1.82.D0.BD.D0.BE.D0.B5_.D0.B4.D0.B5.D0.BA.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [3.2 Высокое качество воспроизведения](#.D0.92.D1.8B.D1.81.D0.BE.D0.BA.D0.BE.D0.B5_.D0.BA.D0.B0.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.BE_.D0.B2.D0.BE.D1.81.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [3.3 Воспроизведение с предыдущего места](#.D0.92.D0.BE.D1.81.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81_.D0.BF.D1.80.D0.B5.D0.B4.D1.8B.D0.B4.D1.83.D1.89.D0.B5.D0.B3.D0.BE_.D0.BC.D0.B5.D1.81.D1.82.D0.B0)
    *   [3.4 Звук слишком тихий](#.D0.97.D0.B2.D1.83.D0.BA_.D1.81.D0.BB.D0.B8.D1.88.D0.BA.D0.BE.D0.BC_.D1.82.D0.B8.D1.85.D0.B8.D0.B9)
    *   [3.5 Быстрое переключение между соотношениями сторон](#.D0.91.D1.8B.D1.81.D1.82.D1.80.D0.BE.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.B5.D0.B6.D0.B4.D1.83_.D1.81.D0.BE.D0.BE.D1.82.D0.BD.D0.BE.D1.88.D0.B5.D0.BD.D0.B8.D1.8F.D0.BC.D0.B8_.D1.81.D1.82.D0.BE.D1.80.D0.BE.D0.BD)
    *   [3.6 Отрисовка на корневом окне](#.D0.9E.D1.82.D1.80.D0.B8.D1.81.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BD.D0.B0_.D0.BA.D0.BE.D1.80.D0.BD.D0.B5.D0.B2.D0.BE.D0.BC_.D0.BE.D0.BA.D0.BD.D0.B5)
    *   [3.7 Использование как плагин браузера](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BA.D0.B0.D0.BA_.D0.BF.D0.BB.D0.B0.D0.B3.D0.B8.D0.BD_.D0.B1.D1.80.D0.B0.D1.83.D0.B7.D0.B5.D1.80.D0.B0)
    *   [3.8 Использование mpv для проигрывания музыки](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_mpv_.D0.B4.D0.BB.D1.8F_.D0.BF.D1.80.D0.BE.D0.B8.D0.B3.D1.80.D1.8B.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.BC.D1.83.D0.B7.D1.8B.D0.BA.D0.B8)
    *   [3.9 Просмотр стримов](#.D0.9F.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_.D1.81.D1.82.D1.80.D0.B8.D0.BC.D0.BE.D0.B2)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [mpv](https://www.archlinux.org/packages/?name=mpv) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") или [mpv-git](https://aur.archlinux.org/packages/mpv-git/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

### Графические оболочки

*mpv* предоставляет элегантный интерфейс OSC, появляющийся при движении курсора. Однако, существуют также графические интерфейсы, рассчитанные на более обширную аудиторию:

*   **Baka MPlayer** — Мультимедийный плеер, основанный на libmpv. Qt 5.

	[https://github.com/u8sand/Baka-MPlayer/](https://github.com/u8sand/Baka-MPlayer/) || [baka-mplayer-git](https://aur.archlinux.org/packages/baka-mplayer-git/)

*   **bomi** — Мощный и легкий универсальный мультимедиа проигрыватель. (Qt 5).bomi был ранее известен как CMPlayer.

	[https://bomi-player.github.io/](https://bomi-player.github.io/) || [bomi](https://aur.archlinux.org/packages/bomi/), [bomi-git](https://aur.archlinux.org/packages/bomi-git/)

*   **GNOME MPV** — Простой интерфейс для *mpv* (GTK+ 3).

	[https://github.com/gnome-mpv/gnome-mpv/](https://github.com/gnome-mpv/gnome-mpv/) || [gnome-mpv-git](https://aur.archlinux.org/packages/gnome-mpv-git/), [gnome-mpv](https://aur.archlinux.org/packages/gnome-mpv/)

*   **[SMPlayer](https://en.wikipedia.org/wiki/SMPlayer "wikipedia:SMPlayer")** — Мультимедийный плеер с дополнительным функционалом (CSS темы, интеграция с YouTube и другое) (Qt 5).

	[http://smplayer.sourceforge.net/](http://smplayer.sourceforge.net/) || [smplayer](https://www.archlinux.org/packages/?name=smplayer)

*   **xt7-player-mpv** — Qt/Gambas графическая оболочка для MPV с богатым набором настраиваемых опций, включая фильтры и драйвера, поддержка плагинов LADSPA, а также библиотека / плейлист менеджер, YouTube, интернет-радио, подкасты, DVB-T и многое другое.

	[https://github.com/kokoko3k/xt7-player-mpv](https://github.com/kokoko3k/xt7-player-mpv) || [xt7-player-mpv-git](https://aur.archlinux.org/packages/xt7-player-mpv-git/)

**Примечание:** Пакеты SMPlayer/bomi включают в себя также и сам *mpv*

## Настройка

Настройки *mpv* находятся в файлах `mpv.conf` (общие), `input.conf` (сочетания клавиш) и `lua-settings/osc.conf` (наэкранное меню). Полный список параметров доступен в [mpv(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mpv.1) или [GitHub docs](https://github.com/mpv-player/mpv/tree/master/DOCS/man). Если не установлена [переменная окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `XDG_CONFIG_HOME`, будут использоваться файлы настроек пользователя, расположенные в каталоге `~/.config/mpv`. Системные файлы настроек располагаются в `/etc/mpv`.

### Пример файла input.conf

Скопировав следующее в `~/.config/mpv/input.conf`, можно добавить ряд полезных сочетаний клавиш в mpv, таких как поворот видео на 90 градусов, масштабирование и панорамирование.

```
Alt+RIGHT add video-rotate 90
Alt+LEFT add video-rotate -90
Alt+- add video-zoom -0.25
Alt+= add video-zoom 0.25
Alt+j add video-pan-x -0.05
Alt+l add video-pan-x 0.05
Alt+i add video-pan-y 0.05
Alt+k add video-pan-y -0.05

```

### mpv и управление PulseAudio/ALSA mixer'ом с версии 0.18.1

Данная опция применима только если вы используете pulseaudio с mpv (`-ao=pulse` или `ao=pulse` в `mpv.conf`) или если вы хотите управлять громкостью ALSA mixer с помощью mpv.

Добавьте следующее в `~/.config/mpv/input.conf`, чтобы изменять громкость приложения в PulseAudio / ALSA посредством клавиш в mpv (и наоборот):

```
/ add ao-volume -2
SHIFT+* add ao-volume 2

```

Опционально измените клавиши громкости выше на любые другие.

## Советы и рекомендации

### Аппаратное декодирование

В отличие от *mplayer* и *mplayer2*, *mpv* имеет встроенную поддержку [VA-API](/index.php/VA-API_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "VA-API (Русский)") и [VDPAU](/index.php/VDPAU_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "VDPAU (Русский)"). Чтобы указать способ декодирования, запустите *mpv* с опцией `--hwdec='метод'`. Полный список всех доступных методов вы найдете в [man-странице](/index.php/Man_page_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Man page (Русский)") [mpv(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mpv.1), поискав описание опции `--hwdec=<api>`. Чтобы не указывать метод при каждом запуске mpv, добавьте опцию `hwdec='метод'` в ваш файл настроек.

Когда используется аппаратное декодирование, видеовывод (параметр `--vo='драйвер'`) должен быть равен `opengl` или `opengl-hq` (или `vdpau`, если указан `hwdec=vdpau`).

Если аппаратное декодирование недоступно, *mpv* автоматически переключится на программное декодирование.

Аппаратное декодирование включено по умолчанию для кодеков h264, vc1, wmv3, hevc, mpeg2video and vp9\. Однако, можно указать кодеки вручную (например, `--hwdec-codecs=h264,mpeg2video`) или включить аппаратное декодирование для всех кодеков (`--hwdec-codecs=all`).

**Совет:**

*   `hwdec=vaapi` должен использоваться с `profile=opengl` [[1]](https://github.com/mpv-player/mpv/blob/master/DOCS/man/vo.rst), если возможно (`opengl-hq` иногда приводит к сильным скачкам загрузки процессора при воспроизведении видео).
*   Использование `vo=vaapi` с недавних пор не рекомендуется [[2]](https://github.com/mpv-player/mpv/blob/master/DOCS/man/vo.rst).

Подробную информацию вы можете найти на страницах [options.rst](https://github.com/mpv-player/mpv/blob/master/DOCS/man/options.rst) и [vo.rst](https://github.com/mpv-player/mpv/blob/master/DOCS/man/vo.rst).

### Высокое качество воспроизведения

Профиль `opengl-hq` это набор настроек, обеспечивающий высокое качество видео. Он использует видеодрайвер OpenGL и включает различные опции, избранные разработчиками *mpv*. Чтобы использовать его, укажите его в файле конфигурации.

 `~/.config/mpv/mpv.conf`  `profile=opengl-hq` 

Этот профиль включает фильтр `deband`, который значительно уменьшает количество видимых артефактов, но незначительно размывает некоторые мелкие детали. На практике это чаще всего повышает качество - единственной причиной его отключения может быть производительность.

Если он приводит к низкой производительности, вы можете легко его отключить.

 `~/.config/mpv/mpv.conf` 
```
profile=opengl-hq
deband=no
```

Профиль `opengl-hq` по умолчанию использует фильтр масштабирования `spline36`, обеспечивая быстродействие и среднее качество видео. Для наилучшего качества стоит использовать `ewa_lanczossharp`, если ваше оборудование достаточно мощное.

 `~/.config/mpv/mpv.conf` 
```
profile=opengl-hq
scale=ewa_lanczossharp
cscale=ewa_lanczossharp
```

### Воспроизведение с предыдущего места

Стандартной комбинацией клавиш для выхода из *mpv* с сохранением текущей позиции является `Shift+q`. Это можно изменить, добавив строку `quit_watch_later` в файл настроек сочетаний клавиш.

Чтобы всегда сохранять текущую позицию при выходе, запустите *mpv* с опцией `--save-position-on-quit` или добавьте `save-position-on-quit` в файл конфигурации.

### Звук слишком тихий

Установите параметр `softvol-max=*значение*` в вашем файле настроек на желаемый уровень, например `softvol-max=600`. Дополнительно (или вместо этого), вы можете воспользоваться [компрессором аудиосигнала](https://en.wikipedia.org/wiki/ru:%D0%9A%D0%BE%D0%BC%D0%BF%D1%80%D0%B5%D1%81%D1%81%D0%BE%D1%80_%D0%B0%D1%83%D0%B4%D0%B8%D0%BE%D1%81%D0%B8%D0%B3%D0%BD%D0%B0%D0%BB%D0%B0 "wikipedia:ru:Компрессор аудиосигнала") с `af=acompressor`.

### Быстрое переключение между соотношениями сторон

Начиная с версии 0.8.0, вы можете переключаться между соотношениями сторон, используя `Shift+a`.

Альтернативно, добавьте следующую строку в ваш файл `input.conf`:

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