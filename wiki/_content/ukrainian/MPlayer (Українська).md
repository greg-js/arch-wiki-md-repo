**MPlayer** є одним з най-най-популярніших програвачів відео для Лінукса. MPlayer підтримує майже всі відео та аудіо формати і є дуже багатофункціональним. Саме тому більшість користувачів використовують його для перегляду відео.

## Contents

*   [1 Інсталяція](#.D0.86.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D1.8F.D1.86.D1.96.D1.8F)
*   [2 Деякі додаткові поради при інсталяції](#.D0.94.D0.B5.D1.8F.D0.BA.D1.96_.D0.B4.D0.BE.D0.B4.D0.B0.D1.82.D0.BA.D0.BE.D0.B2.D1.96_.D0.BF.D0.BE.D1.80.D0.B0.D0.B4.D0.B8_.D0.BF.D1.80.D0.B8_.D1.96.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D1.8F.D1.86.D1.96.D1.97)
    *   [2.1 Більше кодеків](#.D0.91.D1.96.D0.BB.D1.8C.D1.88.D0.B5_.D0.BA.D0.BE.D0.B4.D0.B5.D0.BA.D1.96.D0.B2)
    *   [2.2 Frontends/GUIs](#Frontends.2FGUIs)
    *   [2.3 Інтеграція з Веб-переглядачами](#.D0.86.D0.BD.D1.82.D0.B5.D0.B3.D1.80.D0.B0.D1.86.D1.96.D1.8F_.D0.B7_.D0.92.D0.B5.D0.B1-.D0.BF.D0.B5.D1.80.D0.B5.D0.B3.D0.BB.D1.8F.D0.B4.D0.B0.D1.87.D0.B0.D0.BC.D0.B8)
        *   [2.3.1 Firefox](#Firefox)
        *   [2.3.2 Konqueror](#Konqueror)
*   [3 Використання](#.D0.92.D0.B8.D0.BA.D0.BE.D1.80.D0.B8.D1.81.D1.82.D0.B0.D0.BD.D0.BD.D1.8F)
    *   [3.1 Конфігурація](#.D0.9A.D0.BE.D0.BD.D1.84.D1.96.D0.B3.D1.83.D1.80.D0.B0.D1.86.D1.96.D1.8F)
    *   [3.2 Напівпрозоре відео з radeon і включеними композитними ефектами](#.D0.9D.D0.B0.D0.BF.D1.96.D0.B2.D0.BF.D1.80.D0.BE.D0.B7.D0.BE.D1.80.D0.B5_.D0.B2.D1.96.D0.B4.D0.B5.D0.BE_.D0.B7_radeon_.D1.96_.D0.B2.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.BC.D0.B8_.D0.BA.D0.BE.D0.BC.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BD.D0.B8.D0.BC.D0.B8_.D0.B5.D1.84.D0.B5.D0.BA.D1.82.D0.B0.D0.BC.D0.B8)
    *   [3.3 Перегляд відео-потоків (відео-стрім)](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B3.D0.BB.D1.8F.D0.B4_.D0.B2.D1.96.D0.B4.D0.B5.D0.BE-.D0.BF.D0.BE.D1.82.D0.BE.D0.BA.D1.96.D0.B2_.28.D0.B2.D1.96.D0.B4.D0.B5.D0.BE-.D1.81.D1.82.D1.80.D1.96.D0.BC.29)
    *   [3.4 Передача потоку аудіо з mplayer до jackd](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B4.D0.B0.D1.87.D0.B0_.D0.BF.D0.BE.D1.82.D0.BE.D0.BA.D1.83_.D0.B0.D1.83.D0.B4.D1.96.D0.BE_.D0.B7_mplayer_.D0.B4.D0.BE_jackd)
    *   [3.5 Прив’язка клавіш](#.D0.9F.D1.80.D0.B8.D0.B2.E2.80.99.D1.8F.D0.B7.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B0.D0.B2.D1.96.D1.88)
    *   [3.6 Mplayer не може відкрити файли з пропусками в назві](#Mplayer_.D0.BD.D0.B5_.D0.BC.D0.BE.D0.B6.D0.B5_.D0.B2.D1.96.D0.B4.D0.BA.D1.80.D0.B8.D1.82.D0.B8_.D1.84.D0.B0.D0.B9.D0.BB.D0.B8_.D0.B7_.D0.BF.D1.80.D0.BE.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D0.BC.D0.B8_.D0.B2_.D0.BD.D0.B0.D0.B7.D0.B2.D1.96)
*   [4 Додаткові джерела](#.D0.94.D0.BE.D0.B4.D0.B0.D1.82.D0.BA.D0.BE.D0.B2.D1.96_.D0.B4.D0.B6.D0.B5.D1.80.D0.B5.D0.BB.D0.B0)

## Інсталяція

Запустіть `pacman -S mplayer` в командній стрічці (перед тим залогуйтесь як root).

## Деякі додаткові поради при інсталяції

### Більше кодеків

Щоб отримати більше від MPlayer, спробуйте заінсталювати пакет `codecs`, який додає підтримку для кодеків Віндовса, Real9 і QuickTime (.mov).

Інсталяція запусскається наступним чином `pacman -S codecs`. [Примітка: цей пакет на даний момент видалений з репозиторію; більше дивіться тут: [https://bbs.archlinux.org/viewtopic.php?id=73230](https://bbs.archlinux.org/viewtopic.php?id=73230)].

### Frontends/GUIs

Є кілька графічних накладок (GUI) для MPlayer.

*   Qt: `smplayer` міститься в extra репозиторії. Пакет `smplayer-themes` містить тему для Smplayer.
*   Gtk+: `pymp` і `gnome-mplayer` містяться в AUR і community репозиторіях.
*   gmplayer: це gui більше не входить в пакет mplayer. Існує альтернативний пакет (`mplayer-x`) в AUR, в якому включено опцію gui для mplayer.

### Інтеграція з Веб-переглядачами

Якщо ви бажаєте контролювати відео в Вашому улюбленому веб-переглядачі за допомогою MPlayer, спробуйте наступне:

#### Firefox

`pacman -S mplayer-plugin`

`pacman -S gecko-mediaplayer`

#### Konqueror

`pacman -S kmplayer` (також дає повну графічну накладку для MPlayer.)

## Використання

### Конфігурація

Системну конфігурацію можна знайти в `/etc/mplayer/mplayer.conf`, тоді як конфігурація для користувача зберігається в `~/.mplayer/config`. Почніть з файлу `/etc/mplayer/example.conf`, тут є приклад:

```
#profile for up-mixing two channels audio to six channels
# use -profile 2chto6ch to activate
[2chto6ch]
af-add=pan=6:1:0:.4:0:.6:2:0:1:0:.4:.6:2

#profile to down-mixing six channels audio to two channels
# use -profile 6chto2ch to activate
[6chto2ch]
af-add=pan=2:0.7:0:0:0.7:0.5:0:0:0.5:0.6:0.6:0:0

#default configuration that applies to every file
[default]
#use X11 for video output
vo=x11
#use also for audio output
ao=alsa
#prefere using six channels audio
channels = 6
#scale the subtitles to the 3% of the screen size
subfont-text-scale = 3
#never use font config
nofontconfig = 1
#add black borders so the movies have the same aspect ratio of the monitor
#change if your monitor is not 16/9
vf-add=expand=::::1:16/9:16

```

### Напівпрозоре відео з radeon і включеними композитними ефектами

Щоб отримати напівпрозорий відео вивід в X Ви повинні включити текстуроване відео в mplayer:

```
mplayer -vo xv:adaptor=1 <Файл>

```

Або додати наступну стрічку до ~/.mplayer/config:

```
vo=xv:adaptor=1

```

Ви можете використати `xvinfo` щоб перевірити які відео режими підтримує Ваша відео-карта.

### Перегляд відео-потоків (відео-стрім)

Якщо Ви бажаєте переглядати відео-потоки (наприклад *.asx посилання), скористайтеся `mplayer -playlist посилання_на_потік.asx` для перегляду потоку, оскільки такі посилання містять список програвання інших потоків і без опції -playlist їх неможливо переглянути.

### Передача потоку аудіо з mplayer до jackd

Відредагуйте ~/.mplayer/config додайте:

ao=jack

### Прив’язка клавіш

	*Це є список найбільш вживаних клавіш для MPlayer.*

| Key | Description |
| p | Пауза/програвати. |
| Space | Пауза/програвати. |
| Left | Промотати 10 секунд назад. |
| Right | Промотати 10 секунд вперед. |
| Down | Промотати 1 хвилину назад. |
| Up | Промотати 1 хвилину вперед. |
| < | Іти назад в списку програвання. |
| > | Іти вперед в списку програвання. |
| m | Виключити звук. |
| 0 | Збільшити гучність. |
| 9 | Зменшити гучність. |
| f | Переключитися в режим повного екрану. |
| o | Включити підказки на екрані (OSD). |
| j | Включити перегляд субтитлів. |
| `I` | Показати назву файла. |
| 1, 2 | Налаштувати контраст. |
| 3, 4 | Налаштувати яскравість. |

### Mplayer не може відкрити файли з пропусками в назві

Якщо Ви намагаєтеся відкрити файл з пропусками в назві (Якийсь Фільм) і mplayer не запускається, видаючи помилку, що не може відкрити файл (file:///Якийсь%20Фільм), де всі пропуски відображаються як %20, тоді відкрийте

```
/usr/share/applications/mplayer.desktop

```

і змініть стрічку

```
Exec=mplayer %U

```

на

```
Exec=mplayer %F

```

Якщо Ви маєте накладку на Mplayer (GUI), тоді додайте назву накладки GUI в Exec=назва GUI %F, наприклад Exec=gmplayer %F.

## Додаткові джерела

*   [Офіційна сторінка MPlayer](http://www.mplayerhq.hu/)