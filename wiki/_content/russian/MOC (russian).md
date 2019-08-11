**M**usic **O**n **C**onsole (Музыка в консоли) — лёгкий музыкальный плеер, который состоит из двух частей: сервера (Moc) и плеера/интерфейса (Mocp). Такая реализация похожа на реализацию [mpd](/index.php/Music_Player_Daemon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Music Player Daemon (Русский)"), но в отличие от *mpd*, Moc поставляется сразу с интерфейсом. Сервер не поддерживает удалённый доступ.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
    *   [1.1 PulseAudio](#PulseAudio)
*   [2 Фронтэнды](#Фронтэнды)
*   [3 Настройка](#Настройка)
*   [4 Использование](#Использование)
*   [5 Скробблинг Last.fm](#Скробблинг_Last.fm)
    *   [5.1 mocp-scrobbler](#mocp-scrobbler)
*   [6 Файл сервиса systemd](#Файл_сервиса_systemd)
*   [7 Решение проблем](#Решение_проблем)
    *   [7.1 MOC не запускается](#MOC_не_запускается)
    *   [7.2 Странные символы](#Странные_символы)
    *   [7.3 FATAL_ERROR: Layout1 is malformed](#FATAL_ERROR:_Layout1_is_malformed)
*   [8 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [moc](https://www.archlinux.org/packages/?name=moc).

### PulseAudio

Установите пакет [moc-pulse](https://aur.archlinux.org/packages/moc-pulse/) или [moc-pulse-svn](https://aur.archlinux.org/packages/moc-pulse-svn/) (содержащий последнюю разрабатываемую версию) для получения поддержки [PulseAudio](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PulseAudio (Русский)"). См. раздел [MOC#Using PulseAudio](/index.php/MOC#Using_PulseAudio "MOC") для получения информации об использовании драйвера pulseaudio.

## Фронтэнды

*   **mocicon** — GTK-апплет панели для управления MOC

	[http://mocicon.sourceforge.net/](http://mocicon.sourceforge.net/) || [mocicon](https://aur.archlinux.org/packages/mocicon/)

*   **eXo** — Qt-фронтэнд для MOC, поддерживающий скробблинг

	[https://bitbucket.org/blaze/exo/](https://bitbucket.org/blaze/exo/) || [exo-player](https://aur.archlinux.org/packages/exo-player/)

## Настройка

Пакет включает в себя пример конфигурационного файла `/usr/share/doc/moc/config.example`. Для настройки *moc* скопируйте этот файл в `~/.moc/config` и отредактируйте его.

Настройка горячих клавиш описана в `/usr/share/doc/moc/keymap.example`.

Если вы хотите использовать Moc с [OSS](/index.php/OSS "OSS") v4.1, обратитесь к разделу [OSS#MOC](/index.php/OSS#MOC "OSS").

## Использование

Запустите *moc*:

```
$ mocp

```

Эта команда запустит сервер и интерфейс. Некоторые полезные горячие клавиши (чувствительны к регистру):

| Начать воспроизведение | `Enter` |
| Пауза | `Space` или `p` |
| Следующий трек | `n` |
| Предыдущий трек | `b` |
| Переключиться с плейлиста к
обзору файлов (и обратно) | `Tab` |
| Добавить один трек в плейлист | `a` |
| Удалить трек из плейлиста | `d` |
| Добавить каталог (рекурсивно) в плейлист | `Shift+a` |
| Очистить плейлист | `Shift+c` |
| Увеличить громкость на 5% | `.` (точка) |
| Уменьшить громкость на 5% | `,` (запятая) |
| Увеличить громкость на 1% | `>` |
| Увеличить громкость на 1% | `<` |
| Изменить громкость на 10% | `meta+1` |
| Изменить громкость на 20% | `meta+2` |
| Закрыть проигрыватель (без завершения работы сервера) | `q` |

**Примечание:** Для завершения работы сервера, используйте `Shift+q` или:
```
$ mocp -x

```

## Скробблинг Last.fm

### mocp-scrobbler

[mocp-scrobbler](https://aur.archlinux.org/packages/mocp-scrobbler/) — скробблер Last.fm/Libre.fm для MOC с поддержкой уведомлений о текущем воспроизведении, "демонизации" и кеширования. Он зависит только от [Python](/index.php/Python_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Python (Русский)") 3.

Скопируйте пример файла в каталог с пользовательскими конфигурационными файлами:

```
mkdir ~/.mocpscrob/
cp /usr/share/doc/mocp-scrobbler/config.example  ~/.mocpscrob/config

```

Отредактируйте `~/.mocpscrob/config`, добавив в него свои имя пользователя и пароль. При первом запуске переменная с паролем будет заменена на переменную `password_md5`, содержащую в себе MD5-хеш. Если необходимо изменить пароль, просто (опять) добавьте переменную с новым паролем, и значение переменной `password_md5` будет обновлено.

Чтобы начать скробблинг, перед запуском *mocp* запустите как демон *mocp-scrobbler*. Также можно использовать [псевдоним](/index.php/Bash_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Псевдонимы "Bash (Русский)"):

```
alias mocp='/usr/bin/mocp-scrobbler.py -d; mocp'

```

## Файл сервиса systemd

 `/etc/systemd/system/moc@.service` 
```
[Unit]
Description=MOC server
ConditionPathExists=/usr/bin/mocp
After=network.target sound.target

[Service]
RemainAfterExit=yes
User=%I
ExecStart=/usr/bin/mocp -S
ExecStop=/usr/bin/mocp -x
WorkingDirectory=/home/%I/

[Install]
WantedBy=multi-user.target

```

[Включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") этот сервис для соответствующего пользователя.

## Решение проблем

### MOC не запускается

Если MOC не запускается, скорее всего, проблема в конфигурационных файлах `~/.moc/`. Можно попробовать отредактировать файлы настройки или просто удалить весь каталог.

### Странные символы

Если вместо нормальных линий (вертикальные линии для разделения пространства и т.д.) вы видите странного вида символы, возможно, у вас установлен шрифт, несовместимый с MOC. Либо смените шрифт, либо установите в `.moc/config` ASCII для рисования линий:

```
ASCIILines = no

```

### FATAL_ERROR: Layout1 is malformed

Если MOC завершается с такой ошибкой, попробуйте добавить одну из этих строк в `.moc/config`:

```
Layout1 = directory(0,0,50%,100%): playlist(50%,0,100%,100%)

```

либо

```
Layout1 = directory(0,0,50%,100%): playlist(50%,0,FILL,100%)

```

Смотрите [отчет об ошибке](http://moc.daper.net/node/262) и [Debian bugs](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=485059).

## Смотрите также

*   [Официальная документация](http://moc.daper.net/documentation)