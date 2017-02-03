З [домашньої сторінки](http://www.videolan.org/vlc/) проекту:

	VLC це відкритий і вільний кросплатформенний медіаплеєр, що здатен програвати більшість мультимедійних файлів таких, як DVD, Audio CD, VCD та різні потокові протоколи.

## Contents

*   [1 Встановлення](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F)
*   [2 Мова](#.D0.9C.D0.BE.D0.B2.D0.B0)
*   [3 Вигляд](#.D0.92.D0.B8.D0.B3.D0.BB.D1.8F.D0.B4)
*   [4 Веб-інтерфейс](#.D0.92.D0.B5.D0.B1-.D1.96.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81)
*   [5 Поради та рекомендації](#.D0.9F.D0.BE.D1.80.D0.B0.D0.B4.D0.B8_.D1.82.D0.B0_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D1.96.D1.97)
    *   [5.1 Відкриття аудіо та відео-файлів по замовчуванню в GNOME](#.D0.92.D1.96.D0.B4.D0.BA.D1.80.D0.B8.D1.82.D1.82.D1.8F_.D0.B0.D1.83.D0.B4.D1.96.D0.BE_.D1.82.D0.B0_.D0.B2.D1.96.D0.B4.D0.B5.D0.BE-.D1.84.D0.B0.D0.B9.D0.BB.D1.96.D0.B2_.D0.BF.D0.BE_.D0.B7.D0.B0.D0.BC.D0.BE.D0.B2.D1.87.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8E_.D0.B2_GNOME)
    *   [5.2 Twitch.tv-cтрімінг через VLC](#Twitch.tv-c.D1.82.D1.80.D1.96.D0.BC.D1.96.D0.BD.D0.B3_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_VLC)
    *   [5.3 Програвання потокового контенту з локального DLNA серверу](#.D0.9F.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D0.BF.D0.BE.D1.82.D0.BE.D0.BA.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D0.BA.D0.BE.D0.BD.D1.82.D0.B5.D0.BD.D1.82.D1.83_.D0.B7_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_DLNA_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D1.83)
    *   [5.4 Контроль за допомогою швидкого доступу чи cli](#.D0.9A.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D1.8C_.D0.B7.D0.B0_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BC.D0.BE.D0.B3.D0.BE.D1.8E_.D1.88.D0.B2.D0.B8.D0.B4.D0.BA.D0.BE.D0.B3.D0.BE_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D1.83_.D1.87.D0.B8_cli)
    *   [5.5 Запобігання відкриттю великої кількості вікон](#.D0.97.D0.B0.D0.BF.D0.BE.D0.B1.D1.96.D0.B3.D0.B0.D0.BD.D0.BD.D1.8F_.D0.B2.D1.96.D0.B4.D0.BA.D1.80.D0.B8.D1.82.D1.82.D1.8E_.D0.B2.D0.B5.D0.BB.D0.B8.D0.BA.D0.BE.D1.97_.D0.BA.D1.96.D0.BB.D1.8C.D0.BA.D0.BE.D1.81.D1.82.D1.96_.D0.B2.D1.96.D0.BA.D0.BE.D0.BD)
    *   [5.6 Підтримка прискорення апаратноо засобу](#.D0.9F.D1.96.D0.B4.D1.82.D1.80.D0.B8.D0.BC.D0.BA.D0.B0_.D0.BF.D1.80.D0.B8.D1.81.D0.BA.D0.BE.D1.80.D0.B5.D0.BD.D0.BD.D1.8F_.D0.B0.D0.BF.D0.B0.D1.80.D0.B0.D1.82.D0.BD.D0.BE.D0.BE_.D0.B7.D0.B0.D1.81.D0.BE.D0.B1.D1.83)
    *   [5.7 systemd service](#systemd_service)

## Встановлення

[Встановіть](/index.php/Install "Install") [vlc](https://www.archlinux.org/packages/?name=vlc) з [офіційного репозиторію](/index.php/Official_repositories "Official repositories").

Відомі варіанти:

*   [vlc-git](https://aur.archlinux.org/packages/vlc-git/) - розробницький варіант.
*   [vlc-nox](https://aur.archlinux.org/packages/vlc-nox/) - без підтримки Х.

Необов'язкові залежності:

*   [qt4](https://www.archlinux.org/packages/?name=qt4) - для GUI.
*   [libcdio](https://www.archlinux.org/packages/?name=libcdio) - для підтримки відтворення Audio CD.

## Мова

VLC не має опції для зміни мови в *Preferences*. Однак ви можете використати префікс *LANGUAGE=*. Для прикладу, змініть рядок файлу `/usr/share/applications/vlc.desktop`:

```
Exec=/usr/bin/vlc %U

```

на:

```
Exec=LANGUAGE=fr /usr/bin/vlc %U

```

щоб змінити мову інтерфейсу на Французьку.

## Вигляд

Тему програвача можна змінити на свій смак. Ви можете отримати її [звідси.](http://www.videolan.org/vlc/skins.php)

Встановлення теми просте - просто завантажте ту, яку бажаєте і скопіюйте до:

```
~/.local/share/vlc/skins2

```

Запустіть VLC, потім *Tools > Preferences*. Коли відкрито сторінку параметрів, ви будете на вкладці Interface.

Натисніть кнопку "Use custom skin" і вкажіть шлях до завантаженої теми.

Перезапустіть VLC, щоб зміни почали діяти.

## Веб-інтерфейс

Запустіть VLC з параметром `--extraintf=http`,щоб використовувати спільний з робочим оточенням веб-інтерфейс. Параметр `--http-host` визначає адресу, яка по замовчуванню є `localhost`. Щоб ввести пароль, введіть `--http-password`, інакше VLC не дозволить вам ввійти.

```
# vlc --extraintf=http --http-host 0.0.0.0:8080 --http-password 'вашпароль'

```

Або можете ввімкнути цю опцію в UI по вкладкам *View > Add Interface > Web Interface*.

По замовчуванню VLC визначає порт 8080: [http://127.0.0.1:8080](http://127.0.0.1:8080)

Відредагуйте `/usr/share/vlc/lua/http/.hosts`, щоб дозволити віддалене з'єднання. Вам потрібно буде перезапустити VLC, щоб зміни вступили в силу.

## Поради та рекомендації

### Відкриття аудіо та відео-файлів по замовчуванню в GNOME

Скопіюйте системний файл вашого робочого оточення до теки з місцевим (локальний `.desktop` файл заміниться системним):

```
$ cp /usr/share/applications/vlc.desktop ~/.local/share/applications/

```

Визначіть mime-тип (типи файлів, що програватимуться VLC):

```
sed -i 's|^Mimetype.*$|MimeType=video/dv;video/mpeg;video/x-mpeg;video/msvideo;video/quicktime;video/x-anim;video/x-avi;video/x-ms-asf;video/x-ms-wmv;video/x-msvideo;video/x-nsv;video/x-flc;video/x-fli;application/ogg;application/x-ogg;application/x-matroska;audio/x-mp3;audio/x-mpeg;audio/mpeg;audio/x-wav;audio/x-mpegurl;audio/x-scpls;audio/x-m4a;audio/x-ms-asf;audio/x-ms-asx;audio/x-ms-wax;application/vnd.rn-realmedia;audio/x-real-audio;audio/x-pn-realaudio;application/x-flac;audio/x-flac;application/x-shockwave-flash;misc/ultravox;audio/vnd.rn-realaudio;audio/x-pn-aiff;audio/x-pn-au;audio/x-pn-wav;audio/x-pn-windows-acm;image/vnd.rn-realpix;video/vnd.rn-realvideo;audio/x-pn-realaudio-plugin;application/x-extension-mp4;audio/mp4;video/mp4;video/mp4v-es;x-content/video-vcd;x-content/video-svcd;x-content/video-dvd;x-content/audio-cdda;x-content/audio-player;|' ~/.local/share/applications/vlc.desktop

```

Після цього в *System Settings > Details > Default Applications* та в *Video* , виберіть *Open VLC media player*.

### Twitch.tv-cтрімінг через VLC

Дивись [Livestreamer#Twitch](/index.php/Livestreamer#Twitch "Livestreamer").

### Програвання потокового контенту з локального DLNA серверу

Якщо програвання uPNP/DLNA-контенту (*View > Playlist > Local Network > Universal Plug'n'Play*), неможливе і VLC не бачить локальний DLNA-сервер, то впевніться, що брандмауер не блокує порт 1900 UPD. Для програвання локального uPNP/DLNA-контенту необхідно, щоб цей порт був відкритим.

### Контроль за допомогою швидкого доступу чи cli

Встановіть [openbsd-netcat](https://www.archlinux.org/packages/?name=openbsd-netcat).

Візьміть скрипт з: [http://crunchbang.org/forums/viewtopic.php?pid=112035%23p112035#p112035](http://crunchbang.org/forums/viewtopic.php?pid=112035%23p112035#p112035)

Слідуйте інструкціям в скрипті, щоб встановити пакунок для VLC.

Або запустіть скрипт з терміналу чи створіть гарячі клавіші для скрипта у вашому робочому середовищі.

Також ви можете використати dbus-send [(інструкція-пояснення dbus-send(англ.))](http://theelitist.github.io/control-vlc-media-player-through-d-bus), щоб взаємодіяти з VLC:

```
$ dbus-send --print-reply --session --dest=org.mpris.MediaPlayer2.vlc /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.PlayPause

```

### Запобігання відкриттю великої кількості вікон

По замовчуванню VLC для кожного файлу відкриває нове вікно програми. Це може дратувати, якщо ви використовуєте VLC, наприклад, для програвання музичної колекції. Ви можете вимкнути це в *Tools > Preferences > Interface > Instances > Allow only one instance*. Можна ввімкнути параметр *Enqueue files when in one instance mode*, який додаватиме новий файл в поточний плейлист, якщо вже програється якийсь файл.

### Підтримка прискорення апаратноо засобу

Дивись [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

VLC стандартно намагається використувувати наявне API, однак ви можете змінити це через *Tools > Preferences > Input & Codecs*, вибравши відповідний параметр - *Hardware-accelerated decoding*, наприклад, `Video Acceleration (VA) API` для VA-API чи `Video Decode and Presentation API for Unix (VDPAU)` для VDPAU.

### systemd service

Веб-інтерфейс VLC можна запустити за допомогою systemd. Спершу, потрібно задати користувача по замовчуванню. Ми використаємо UID 75 в цьому прикладі, оскільки він не використовується відповідно до [DeveloperWiki:UID / GID Database](/index.php/DeveloperWiki:UID_/_GID_Database "DeveloperWiki:UID / GID Database").

```
# useradd -c "VLC daemon" -d / -G audio -M -p \! -r -s /bin/false -u 75 -U vlcd

```

Тепер створимо файл systemd service:

 `/etc/systemd/system/vlc.service` 
```
[Unit]
Description=VideoOnLAN Service
After=network.target

[Service]
Type=forking
User=vlcd
ExecStart=/usr/bin/vlc --daemon --syslog -I http --http-port 8090 --http-password *password* 
Restart=on-abort

[Install]
WantedBy=multi-user.target

```

[Запустіть](/index.php/Start "Start") та [ввімкніть](/index.php/Enable "Enable") `vlc.service`. Ввійдіть до http://*yourmachine*:8090/ без імені користувача та з паролем, який ви призначили в файлі systemd service.