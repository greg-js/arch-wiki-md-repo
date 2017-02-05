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
*   [6 Вирішення проблем](#.D0.92.D0.B8.D1.80.D1.96.D1.88.D0.B5.D0.BD.D0.BD.D1.8F_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [6.1 Не відтворюється відео чи інші проблеми після оновлення](#.D0.9D.D0.B5_.D0.B2.D1.96.D0.B4.D1.82.D0.B2.D0.BE.D1.80.D1.8E.D1.94.D1.82.D1.8C.D1.81.D1.8F_.D0.B2.D1.96.D0.B4.D0.B5.D0.BE_.D1.87.D0.B8_.D1.96.D0.BD.D1.88.D1.96_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B8_.D0.BF.D1.96.D1.81.D0.BB.D1.8F_.D0.BE.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F)
    *   [6.2 Збій сегментації](#.D0.97.D0.B1.D1.96.D0.B9_.D1.81.D0.B5.D0.B3.D0.BC.D0.B5.D0.BD.D1.82.D0.B0.D1.86.D1.96.D1.97)
    *   [6.3 Немає іконок у випадаючому меню](#.D0.9D.D0.B5.D0.BC.D0.B0.D1.94_.D1.96.D0.BA.D0.BE.D0.BD.D0.BE.D0.BA_.D1.83_.D0.B2.D0.B8.D0.BF.D0.B0.D0.B4.D0.B0.D1.8E.D1.87.D0.BE.D0.BC.D1.83_.D0.BC.D0.B5.D0.BD.D1.8E)
    *   [6.4 Помилка при відкритті VDPAU](#.D0.9F.D0.BE.D0.BC.D0.B8.D0.BB.D0.BA.D0.B0_.D0.BF.D1.80.D0.B8_.D0.B2.D1.96.D0.B4.D0.BA.D1.80.D0.B8.D1.82.D1.82.D1.96_VDPAU)
    *   [6.5 ВІдео перекриває робочий стіл, коректно не масштабується і не знаходиться в правильному положенні](#.D0.92.D0.86.D0.B4.D0.B5.D0.BE_.D0.BF.D0.B5.D1.80.D0.B5.D0.BA.D1.80.D0.B8.D0.B2.D0.B0.D1.94_.D1.80.D0.BE.D0.B1.D0.BE.D1.87.D0.B8.D0.B9_.D1.81.D1.82.D1.96.D0.BB.2C_.D0.BA.D0.BE.D1.80.D0.B5.D0.BA.D1.82.D0.BD.D0.BE_.D0.BD.D0.B5_.D0.BC.D0.B0.D1.81.D1.88.D1.82.D0.B0.D0.B1.D1.83.D1.94.D1.82.D1.8C.D1.81.D1.8F_.D1.96_.D0.BD.D0.B5_.D0.B7.D0.BD.D0.B0.D1.85.D0.BE.D0.B4.D0.B8.D1.82.D1.8C.D1.81.D1.8F_.D0.B2_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE.D0.BC.D1.83_.D0.BF.D0.BE.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.BD.D1.96)
    *   [6.6 Не програються через SFTP медіа-файли, що мають в імені пробіли](#.D0.9D.D0.B5_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D1.8E.D1.82.D1.8C.D1.81.D1.8F_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_SFTP_.D0.BC.D0.B5.D0.B4.D1.96.D0.B0-.D1.84.D0.B0.D0.B9.D0.BB.D0.B8.2C_.D1.89.D0.BE_.D0.BC.D0.B0.D1.8E.D1.82.D1.8C_.D0.B2_.D1.96.D0.BC.D0.B5.D0.BD.D1.96_.D0.BF.D1.80.D0.BE.D0.B1.D1.96.D0.BB.D0.B8)
*   [7 Дивіться також](#.D0.94.D0.B8.D0.B2.D1.96.D1.82.D1.8C.D1.81.D1.8F_.D1.82.D0.B0.D0.BA.D0.BE.D0.B6)

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

## Вирішення проблем

### Не відтворюється відео чи інші проблеми після оновлення

VLC має і буде мати проблем з налаштуванням навіть в незначних релізах. Перед тим, як писати про баґ, видаліть чи змініть ваші конфігурації `~/.config/vlc` і переконайтесь, проблема залишилась.

Якщо ви використовуєте ffmpeg-варіант з AUR, впевніться, що ви так само і оновились. Pacman не оновить пакунок, коли це необхідно, і конфлікт порушить роботу VLC.

### Збій сегментації

При запуску VLC, ви можете отримати збій сегментації. Виключивши загальні фактори такі, як [Microcode](/index.php/Microcode "Microcode"), можливим вирішенням є наступне:

```
 # /usr/lib/vlc/vlc-cache-gen -f /usr/lib/vlc/plugins

```

Потім перевстановіть VLC.

Іншим обхідним рішенням може бути перевстановлення VLC в `LD_PRELOAD` середовищі:

```
# LD_PRELOAD=/usr/lib/libgobject-2.0.so.0 pacman -S vlc

```

### Немає іконок у випадаючому меню

Таке може трапитись у XFCE. Відсутніми виявляться такі іконки, як PCI card, наприклад.

Виконайте ці команди, щоб реактивувати іконки:

```
$ gconftool-2 --type boolean --set /desktop/gnome/interface/buttons_have_icons true
$ gconftool-2 --type boolean --set /desktop/gnome/interface/menus_have_icons true
```

### Помилка при відкритті VDPAU

Дивіться [Hardware video acceleration#Failed to open VDPAU backend](/index.php/Hardware_video_acceleration#Failed_to_open_VDPAU_backend "Hardware video acceleration").

Якщо ваша система можливо не підтримує VDPAU, ви повинні вказати VLC, щоб використовував VA-API замість того. Дивіться [#Hardware acceleration support](#Hardware_acceleration_support).

### ВІдео перекриває робочий стіл, коректно не масштабується і не знаходиться в правильному положенні

Це трапляється як мінімум на картах Intel. Вирішенням проблеми є коригування виводу в налаштуваннях відео на *OpenGL GLX (XCB)* та *Input/Codecs* - встановити декодування на *VA-API* (вибрати будь-який з них).

### Не програються через SFTP медіа-файли, що мають в імені пробіли

Якщо VLC не програє будь-які відео- чи аудіо-файли через SFTP, спочатку ви повинні впевнитись, що sshfs встановлено.

Якщо він відмовляється програвати будь-які медіа-файли, що містять відступи, через SFTP і постійно запитує підтвердження аутентифікації, то змініть рядок

```
Exec=/usr/bin/vlc --started-from-file %U

```

на

```
Exec=/usr/bin/vlc --started-from-file %F

```

у файлі vlc.desktop [[1]](https://bugs.launchpad.net/ubuntu/+source/vlc/+bug/239431/comments/11)

## Дивіться також

*   [List of applications (Українська)#Multimedia](/index.php/List_of_applications_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0)#Multimedia "List of applications (Українська)")
*   [Домашня сторінка VLC](http://www.videolan.org/vlc/)
*   [playerctl](https://github.com/acrisci/playerctl): Командна утиліта та бібліотека для контролювання медіа-плеєрів
*   [Контролювання VLC в браузері](http://wiki.videolan.org/Control_VLC_via_a_browser)