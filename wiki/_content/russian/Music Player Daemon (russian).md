Ссылки по теме

*   [MPD/Tips and Tricks](/index.php/MPD/Tips_and_Tricks "MPD/Tips and Tricks")
*   [MPD/Troubleshooting](/index.php/MPD/Troubleshooting "MPD/Troubleshooting")

**[MPD](http://www.musicpd.org/)** (**m**usic **p**layer **d**aemon) - это музыкальный проигрыватель, имеющий клиент-серверную архитектуру. MPD управляет плейлистами и медиатекой, используя очень мало ресурсов. Для взаимодействия с ним вам нужен отдельный [клиент](#.D0.9A.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D1.8B).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка MPD](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_MPD)
    *   [2.1 Глобальные настройки](#.D0.93.D0.BB.D0.BE.D0.B1.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)
        *   [2.1.1 Директория с музыкой](#.D0.94.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D1.8F_.D1.81_.D0.BC.D1.83.D0.B7.D1.8B.D0.BA.D0.BE.D0.B9)
        *   [2.1.2 Запуск MPD](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_MPD)
            *   [2.1.2.1 Сокет активация](#.D0.A1.D0.BE.D0.BA.D0.B5.D1.82_.D0.B0.D0.BA.D1.82.D0.B8.D0.B2.D0.B0.D1.86.D0.B8.D1.8F)
        *   [2.1.3 Configure audio](#Configure_audio)
        *   [2.1.4 Changing user](#Changing_user)
        *   [2.1.5 Timeline of MPD startup](#Timeline_of_MPD_startup)
    *   [2.2 Local configuration (per user)](#Local_configuration_.28per_user.29)
        *   [2.2.1 Автозапуск при входе на tty](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8_.D0.B2.D1.85.D0.BE.D0.B4.D0.B5_.D0.BD.D0.B0_tty)
        *   [2.2.2 Autostart in X](#Autostart_in_X)
        *   [2.2.3 Autostart with systemd](#Autostart_with_systemd)
        *   [2.2.4 Scripted configuration](#Scripted_configuration)
    *   [2.3 Multi-mpd setup](#Multi-mpd_setup)
*   [3 Клиенты](#.D0.9A.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D1.8B)
    *   [3.1 Консольные](#.D0.9A.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5)
    *   [3.2 Графические](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5)
    *   [3.3 Web](#Web)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Последняя стабильная версия [mpd](https://www.archlinux.org/packages/?name=mpd) доступна в [официальном репозитории](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Если вы хотите установить тестовую версию, [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") предлагает вам несколько вариантов, например [mpd-git](https://aur.archlinux.org/packages/mpd-git/)

**Примечание:** Существует отдельный проект, реализованный на основе mpd с плагинами, называющийся [Mopidy](http://www.mopidy.com). Пакет имеется в репозитории — [mopidy](https://www.archlinux.org/packages/?name=mopidy) и AUR — [mopidy-git](https://aur.archlinux.org/packages/mopidy-git/). Будьте внимательны, т.к. данный проект не является [полноценной заменой](http://docs.mopidy.com/en/latest/ext/mpd/#limitations) MPD.

## Настройка MPD

MPD можно запускать локально (используя конфигурацию пользователя), глобально (настройки применяются для всех пользователей), а также в нескольких экземплярах. Способ запуска (и настройки) зависит от того, как вы хотите использовать MPD (например, для использования на домашней системе более полезен запуск локально).

Чтобы MPD мог воспроизводить аудио, необходимо настроить вывод звука через [ALSA](/index.php/Advanced_Linux_Sound_Architecture_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Advanced Linux Sound Architecture (Русский)") или [OSS](/index.php/OSS "OSS") (возможно использование [PulseAudio](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PulseAudio (Русский)")).

Настройка MPD осуществляется редактированием `mpd.conf`. Расположение этого файла зависит от того, каким образом вы запускали MPD. Далее перечислены наиболее используемые параметры:

*   `pid_file` - Файл, в котором MPD хранит свой pid
*   `db_file` - База данных медиатеки
*   `state_file` - Хранит текущее состояние MPD
*   `playlist_directory` - Директория, в которую сохраняются плейлисты
*   `music_directory` - Директория, сканируемая MPD, при поиске музыки
*   `sticker_file` - Файл с метаданными аудиотреков (sticker database)

**Примечание:** Файлы должны существовать (пути, указанные при настройке) с правильными правами, иначе MPD не запустится.

### Глобальные настройки

**Важно:** Пользователи PulseAudio с глобальными настройками mpd должны использовать [обходной путь](/index.php/Music_Player_Daemon/Tips_and_tricks#Local_.28with_separate_mpd_user.29 "Music Player Daemon/Tips and tricks") для запуска демона!

По умолчанию `/etc/mpd.conf` использует `/var/lib/mpd` и запускается от пользователя *mpd*. Но, т.к. `/var/lib/mpd` по умолчанию принадлежит пользователю *root*, вы должны изменить владельца папки, иначе *mpd* не сможет писать в нее:

```
# chown -R mpd /var/lib/mpd

```

Измените `/etc/mpd.conf` и добавьте в строку `music_directory` путь к вашей папке с музыкой:

```
music_directory /путь/к/музыке

```

#### Директория с музыкой

MPD должен иметь разрешение на выполнение (`+x`) для *всех* директорий музыкальной коллекции, а также доступ на чтение во все директории, содержащие музыкальные файлы. Как правило, это противоречит со стандартной конфигурацией, в которой пользователи хранят свою музыку в своём домашнем каталоге.

Для решения данной проблемы существует несколько способов, которые могут помочь:

*   [запуск MPD от имени текущего пользователя](#Local_configuration_.28per_user.29)
*   добавить пользователя mpd в текущую пользовательскую группу и предоставить разрешения группе к вашему пользовательскому каталогу:

```
 # gpasswd -a mpd <ваша пользовательская группа>
 $ chmod 710 /home/<ваш пользовательский каталог>

```

*   поместить свою музыкальную коллекцию в другой каталог путём

а) полного её перемещения в каталог, доступный mpd;

б) монтированием папки с привязкой к каталогу, в который у mpd есть доступ, например:

```
# mkdir /var/lib/mpd/music
# echo "/путь/к/пользовательской/музыке /var/lib/mpd/music none bind" >> /etc/fstab
# mount -a

```

в) в случае с фс Btrfs — [подразделом Btrfs](/index.php/Btrfs#Subvolumes "Btrfs") (необходимо сделать данные изменения постоянными, путём редактирования файла `/etc/fstab`);

г) созданием символической ссылки на папку с музыкой в `/var/lib/mpd/music`:

```
# mkdir /var/lib/mpd/music
# ln -s /путь/к/пользовательской/музыке /var/lib/mpd/music/

```

В конфигурационном файле mpd может быть указана только одна директория с музыкой. Если музыкальная коллекция содержится в различных директориях, создайте символические ссылки в главную директорию (`/var/lib/mpd`). Не забудьте установить правильные права на эти директории.

#### Запуск MPD

MPD можно контролировать через `mpd.service` [используя systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)"). Первый запуск может занять некоторое время, пока MPD будет сканировать вашу папку с музыкой.

Проверьте все, запустив клиентское приложение ([ncmpc](https://www.archlinux.org/packages/?name=ncmpc) легкий и простой в использовании клиент) и проиграв какие-нибудь треки.

##### Сокет активация

Если `mpd.socket` включен в то время как `mpd.service` (предоставляемый [mpd](https://www.archlinux.org/packages/?name=mpd)) выключен, systemd не станет запускать mpd, но он будет слушать обращения к сокету. Когда mpd клиент попытается обратиться к сокету, systemd запустит `mpd.service` и передаст управление соответствующим портом процессу mpd.

If you prefer to listen on different UNIX sockets or network ports (even multiple sockets of each type), or if you prefer not to listen on network ports at all, you should add/edit/remove the appropriate `"ListenStream="` lines in the `[Socket]` section of `mpd.socket` **and** modify the appropriate lines `/etc/mpd.conf` (see [mpd.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mpd.conf.5) for details).

If you use different (even multiple) network or local sockets, or prefer not to use network sockets at all, simply add, change, or remove lines beginning with `"ListenStream="` in the `[Socket]` section.

 `/etc/systemd/system/mpd.socket` 
```
[Unit]
Description=Music Player Daemon Sockets

[Socket]
ListenStream=/var/run/mpd/socket
ListenStream=6600

[Install]
WantedBy=sockets.target

```

#### Configure audio

To change the volume for mpd independent from other programs, uncomment or add this switch in mpd.conf:

 `/etc/mpd.conf` 
```
mixer_type			"software"

```

Users of [ALSA](/index.php/ALSA "ALSA") will want to have the following device definition, which allows software volume control in the MPD client to control the volume separately from other applications.

 `/etc/mpd.conf` 
```
audio_output {
        type            "alsa"
        name            "My Sound Card"
        mixer_type      "software"      # optional
}
```

Users of [PulseAudio](/index.php/PulseAudio "PulseAudio") will need to make the following modification:

 `/etc/mpd.conf` 
```
audio_output {
        type            "pulse"
        name            "pulse audio"
}
```

PulseAudio supports multiple advanced operations, e.g. transferring the audio to a different machine. For advanced configuration with MPD see [Music Player Daemon Community Wiki](http://mpd.wikia.com/wiki/PulseAudio).

#### Changing user

Changing the group that MPD runs as may result in errors like `output: Failed to open "My ALSA Device"`, `[alsa]: Failed to open ALSA device "default": No such file or directory` or `player_thread: problems opening audio device while playing "Song Name.mp3"`.

This is because the MPD users need to be part of the *audio* group to access sound devices under `/dev/snd/`. To fix it add user make the MPD user part of the *audio* group:

```
# gpasswd -a **mpd** audio

```

#### Timeline of MPD startup

To depict when MPD drops its superuser privileges and assumes those of the user set in the configuration, the timeline of a normal MPD startup is listed here:

1.  Since MPD is started as root by systemd, it first reads the `/etc/mpd.conf` file.
2.  MPD reads the user variable in the `/etc/mpd.conf` file, and changes from root to this user.
3.  MPD then reads the contents of the `/etc/mpd.conf` file and configures itself accordingly.

Notice that MPD changes the running user from root to the one named in the `/etc/mpd.conf` file. This way, uses of `~` in the configuration file point correctly to the home user's directory, and not root's directory. It may be worthwhile to change all uses of `~` to `/home/username` to avoid any confusion over this aspect of MPD's behavior.

### Local configuration (per user)

MPD can be configured per user (rather than the typical method of configuring MPD globally). Running MPD as a normal user has the benefits of:

*   A single directory `~/.config/mpd/` (or any other directory under `$HOME`) that will contain all the MPD configuration files.
*   Easier to avoid unforeseen read/write permission errors.

Good practice is to create a single directory for the required files and playlists. It can be any directory for which you have read and write access, e.g. `~/.config/mpd/` or `~/.mpd/`. This section assumes it is `~/.config/mpd/`, which corresponds to the default value of `$XDG_CONFIG_HOME` (part of [XDG Base Directory Specification](http://standards.freedesktop.org/basedir-spec/basedir-spec-latest.html)).

MPD searches for a config file in `$XDG_CONFIG_HOME/mpd/mpd.conf` and then `~/.mpdconf`. It is also possible to pass other path as command line argument.

Copy the example configuration file to desired location, for example:

```
$ cp /usr/share/doc/mpd/mpdconf.example ~/.config/mpd/mpd.conf

```

Edit `~/.config/mpd/mpd.conf` and specify the required files:

 `~/.config/mpd/mpd.conf` 
```
# Required files
db_file            "~/.config/mpd/database"
log_file           "~/.config/mpd/log"

# Optional
music_directory    "~/Music"
playlist_directory "~/.config/mpd/playlists"
pid_file           "~/.config/mpd/pid"
state_file         "~/.config/mpd/state"
sticker_file       "~/.config/mpd/sticker.sql"

```

Create all the files and directories as configured above:

```
$ mkdir ~/.config/mpd/playlists
$ touch ~/.config/mpd/{database,log,pid,state,sticker.sql}

```

When the paths of required files are configured, MPD can be started. To specify custom location of the configuration file:

```
$ mpd *config_file*

```

#### Автозапуск при входе на tty

Чтобы запустить MPD при входе, добавьте следующее в `~/.profile` (или другой [автозапуск файла](/index.php/Autostarting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9A.D0.BE.D0.BC.D0.BC.D0.B0.D0.BD.D0.B4.D0.BD.D1.8B.D0.B5_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8 "Autostarting (Русский)")):

```
# MPD daemon start (if no other user instance exists)
[ ! -s ~/.config/mpd/pid ] && mpd

```

#### Autostart in X

If you use a [desktop environment](/index.php/Desktop_environment "Desktop environment"), place the following file in `~/.config/autostart/`:

 `~/.config/autostart/mpd.desktop` 
```
[Desktop Entry]
Encoding=UTF-8
Type=Application
Name=Music Player Daemon
Comment=Server for playing audio files
Exec=mpd
StartupNotify=false
Terminal=false
Hidden=false
X-GNOME-Autostart-enabled=false

```

If you do not use a DE, place the line from [#Autostart on tty login](#Autostart_on_tty_login) in your [файле автозапуска](/index.php/Autostarting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9 "Autostarting (Русский)").

#### Autostart with systemd

**Note:** It is assumed that you already have systemd user-session manager running. See the [systemd/User](/index.php/Systemd/User "Systemd/User") page for details.

The package [mpd](https://www.archlinux.org/packages/?name=mpd) provides user service file in `/usr/lib/systemd/user/mpd.service`. The configuration file is expected to exist either in `~/.mpdconf` or `~/.config/mpd/mpd.conf`, see [systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd") if you would like to use different path. The process is not started as root, so you should not use the `user` and `group` variables in the MPD configuration file, the process already has user permissions and therefore it is not necessary to change them further.

All you have to do is enable and start the `mpd` [user service](/index.php/Systemd/User#User_Services "Systemd/User").

**Note:**

*   [mpd](https://www.archlinux.org/packages/?name=mpd) provides also system service file in `/usr/lib/systemd/system/mpd.service`, but as the process is started as root, it does not read the user configuration file and falls back to `/etc/mpd.conf`. [Global configuration](#Global_configuration) is described in other section.
*   Make sure to disable every other method of starting mpd you used before.

#### Scripted configuration

Rasi has written a script that will create the proper directory structure, configuration files and prompt for the location of the user's Music directory; it can be downloaded [here](http://dl.53280.de/mpdsetup.sh).

### Multi-mpd setup

**Useful if running an icecast server.**

For a second MPD (e.g., with icecast output to share music over the network) using the same music and playlist as the one above, simply copy the above configuration file and make a new file (e.g., `/home/username/.mpd/config-icecast`), and only change the log_file, error_file, pid_file, and state_file parameters (e.g., `mpd-icecast.log`, `mpd-icecast.error`, and so on); using the same directory paths for the music and playlist directories would ensure that this second mpd would use the same music collection as the first one e.g., creating and editing a playlist under the first daemon would affect the second daemon as well. Users do not have to create the same playlists all over again for the second daemon. Call this second daemon the same way from `~/.xinitrc` above. (Just be sure to have a different port number, so as to not conflict with the first mpd daemon).

## Клиенты

Для использования mpd необходим отдельный клиент. Список клиентов можно просмотреть по ссылке [mpd wiki](http://mpd.wikia.com/wiki/Clients). Основные приведены здесь:

### Консольные

*   **mpc** — Клиент, использующий для управления mpd-сервером интерпретатор командной строки

	[http://www.musicpd.org/clients/mpc/](http://www.musicpd.org/clients/mpc/) || [mpc](https://www.archlinux.org/packages/?name=mpc)

*   **ncmpc** — Ncurses клиент для *mpd*

	[http://www.musicpd.org/clients/ncmpc/](http://www.musicpd.org/clients/ncmpc/) || [ncmpc](https://www.archlinux.org/packages/?name=ncmpc)

*   **[ncmpcpp](/index.php/Ncmpcpp "Ncmpcpp")** — Копия *ncmpc* с новыми возможностями, написанная на C++ (редактор тегов, поисковый движок)

	[http://ncmpcpp.rybczak.net/](http://ncmpcpp.rybczak.net/) || [ncmpcpp](https://www.archlinux.org/packages/?name=ncmpcpp)

*   **pms** — Гибкий и доступный ncurses клиент

	[http://pms.sourceforge.net/](http://pms.sourceforge.net/) || [pmus](https://aur.archlinux.org/packages/pmus/)

*   **vimpc** — Ncurses mpd-клиент с vi-подобным управлением

	[http://sourceforge.net/projects/vimpc/](http://sourceforge.net/projects/vimpc/) || [vimpc](https://aur.archlinux.org/packages/vimpc/)

### Графические

*   **Ario** — Многофункциональный GTK2 GUI клиент для mpd, вдохновленный Rhythmbox

	[http://ario-player.sourceforge.net/](http://ario-player.sourceforge.net/) || [ario](https://www.archlinux.org/packages/?name=ario)

*   **QmpdClient** — GUI написанный под Qt 4.x

	[http://bitcheese.net/wiki/QMPDClient](http://bitcheese.net/wiki/QMPDClient) || [qmpdclient](https://www.archlinux.org/packages/?name=qmpdclient)

*   **Sonata** — Элегантный Python GTK+ клиент

	[http://sonata.berlios.de/](http://sonata.berlios.de/) || [sonata](https://www.archlinux.org/packages/?name=sonata)

*   **gmpc** — GTK2 интерфейс для Music Player Daemon. Разрабатывался как легковесный клиент, реализующий все возможности, предоставляемые MPD. Предоставляет несколько различных методов обозревания медиатеки. Расширяется плагинами.

	[http://gmpc.wikia.com/wiki/Gnome_Music_Player_Client](http://gmpc.wikia.com/wiki/Gnome_Music_Player_Client) || [gmpc](https://www.archlinux.org/packages/?name=gmpc)

*   **Cantata** — Многофункциональный Qt4, Qt5 или KDE4 клиент для MPD, позволяющий гибко настроить интерфейс

	[https://code.google.com/p/cantata/](https://code.google.com/p/cantata/) || [cantata](https://www.archlinux.org/packages/?name=cantata)

### Web

*   **Patchfork** — Веб клиент для MPD, написанный на PHP и Ajax

	[http://mpd.wikia.com/wiki/Client:Pitchfork](http://mpd.wikia.com/wiki/Client:Pitchfork) || [patchfork-git](https://aur.archlinux.org/packages/patchfork-git/).

## Смотрите также

*   [Форум MPD](http://forum.musicpd.org/)
*   [Руководство пользователя MPD](http://www.musicpd.org/doc/user/)
*   [Статья в Wikipedia](https://en.wikipedia.org/wiki/ru:Music_Player_Daemon "wikipedia:ru:Music Player Daemon")