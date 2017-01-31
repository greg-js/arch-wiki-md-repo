## Contents

*   [1 Описание](#.D0.9E.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Включение отображения обложки, текста песен и гитарных табулатур](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BE.D0.B1.D0.BB.D0.BE.D0.B6.D0.BA.D0.B8.2C_.D1.82.D0.B5.D0.BA.D1.81.D1.82.D0.B0_.D0.BF.D0.B5.D1.81.D0.B5.D0.BD_.D0.B8_.D0.B3.D0.B8.D1.82.D0.B0.D1.80.D0.BD.D1.8B.D1.85_.D1.82.D0.B0.D0.B1.D1.83.D0.BB.D0.B0.D1.82.D1.83.D1.80)
*   [4 Проигрывание аудио-CD](#.D0.9F.D1.80.D0.BE.D0.B8.D0.B3.D1.80.D1.8B.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B0.D1.83.D0.B4.D0.B8.D0.BE-CD)
*   [5 Включение мультимедийных клавиш независимо от DE/WM](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D1.83.D0.BB.D1.8C.D1.82.D0.B8.D0.BC.D0.B5.D0.B4.D0.B8.D0.B9.D0.BD.D1.8B.D1.85_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88_.D0.BD.D0.B5.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B8.D0.BC.D0.BE_.D0.BE.D1.82_DE.2FWM)
*   [6 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [6.1 Индикатор прогресса застревает на 0:00](#.D0.98.D0.BD.D0.B4.D0.B8.D0.BA.D0.B0.D1.82.D0.BE.D1.80_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B5.D1.81.D1.81.D0.B0_.D0.B7.D0.B0.D1.81.D1.82.D1.80.D0.B5.D0.B2.D0.B0.D0.B5.D1.82_.D0.BD.D0.B0_0:00)
    *   [6.2 "Playback error encountered! Configured audiosink bin0 is not working"](#.22Playback_error_encountered.21_Configured_audiosink_bin0_is_not_working.22)
    *   [6.3 Проигрывание с SMB share](#.D0.9F.D1.80.D0.BE.D0.B8.D0.B3.D1.80.D1.8B.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81_SMB_share)

# Описание

[Exaile](http://www.exaile.org/) - музыкальный плеер, написанный на Python с использованием графической библиотеки GTK+. Exaile опубликован под лицензией [GPL](http://www.gnu.org/copyleft/gpl.html). Основные особенности плеера:

*   Поиск обложек, информации об артисте\альбоме, а также гитарных табулатур
*   Табовый интерфейс списка воспроизведения
*   Поддержка iPod
*   Поддержка Last.fm
*   Просмотр директорий SHOUTcast
*   Черный список треков

# Установка

[Exaile](https://aur.archlinux.org/packages/Exaile/) доступен в [AUR](/index.php/AUR "AUR").

Если вы используете [ALSA](/index.php/ALSA "ALSA") и хотите использовать alsasink, установите пакет [gstreamer0.10-base-plugins](https://aur.archlinux.org/packages/gstreamer0.10-base-plugins/), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"):

```
pacman -S gstreamer0.10-base-plugins

```

Это может решить проблему отсутствия звука сразу после установки или же при попытке воспроизвести несколько источников одновременно.

# Включение отображения обложки, текста песен и гитарных табулатур

Для включения отображения обложки, текста песен и гитарных табулатур необходимы пакеты [gnome-python-extras](https://www.archlinux.org/packages/search/?q=gnome-python-extras) и [libgtkhtml](https://www.archlinux.org/packages/search/?q=libgtkhtml), которые могут быть найдены [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"):

```
pacman -S gnome-python-extras libgtkhtml

```

# Проигрывание аудио-CD

Для проигрывания аудио-CD необходим пакет [pycddb](https://www.archlinux.org/packages/?name=pycddb):

```
pacman -S pycddb

```

# Включение мультимедийных клавиш независимо от DE/WM

Первым делом, запустите `xev` и получите коды для клавиш Previous, Next, Play, Stop, Mute. Затем, создайте текстовый файл и добавте в него строки для каждой клавиши, следуя формату `keycode 173 = XF86AudioPrev`, где 173 соответствует коду клавиши, а 'Prev' - действию, которое может принимать значения 'Next', 'Play', 'Stop', и 'Mute'.

Затем, отредактируйте файл `~/.xinitrc`, добавив в него строку `xmodmap <file name>`перед секцией запуска DE/WM (начинается с 'exec'), где <file name> - имя созданного вами файла.

Напоследок, в Exaile, откройте меню настроек плагинов (Edit → Preferences → Plugins), и включите XKeys plugin. После перезапуска мультимедийные клавиши должны работать.

# Решение проблем

### Индикатор прогресса застревает на 0:00

Сперва убедитесь, что это не проблема вашей звуковой подсистемы ([ALSA](/index.php/ALSA "ALSA"), [OSS](/index.php/OSS "OSS"), etc.) и ваш *playback sink* в Exaile имеет корректное значение. Попробуйте установить его в automatic.

Если проблема наблюдается только с файлами формата MP3, следует установить пакет gstreamer-ugly:

```
pacman -S gstreamer0.10-ugly gstreamer0.10-ugly-plugins

```

### "Playback error encountered! Configured audiosink bin0 is not working"

Если вы видите это сообщение или "Configured audiosink bin1 is not working" (после 'bin' может быть любой другой номер), это может означать, что Flash блокирует использование ALSA. Решить данную проблему можно, выполнив:

```
killall npviewer.bin

```

В некоторых случаях Flash может блокировать ALSA даже тогда, когда процесс npviewer.bin не запущен. Обновление в браузере страниц, которые используют Flash, должно помочь.

### Проигрывание с SMB share

К сожалению, Exaile не поддерживает протокол smb.