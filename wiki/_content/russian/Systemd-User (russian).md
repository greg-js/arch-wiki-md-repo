Ссылки по теме

*   [systemd (Русский)](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)")
*   [Автоматический вход в виртуальную консоль](/index.php/%D0%90%D0%B2%D1%82%D0%BE%D0%BC%D0%B0%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B9_%D0%B2%D1%85%D0%BE%D0%B4_%D0%B2_%D0%B2%D0%B8%D1%80%D1%82%D1%83%D0%B0%D0%BB%D1%8C%D0%BD%D1%83%D1%8E_%D0%BA%D0%BE%D0%BD%D1%81%D0%BE%D0%BB%D1%8C "Автоматический вход в виртуальную консоль")
*   [xinitrc (Русский)#Автозапуск X при входе в систему](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_X_.D0.BF.D1.80.D0.B8_.D0.B2.D1.85.D0.BE.D0.B4.D0.B5_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83 "Xinitrc (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [systemd/User](/index.php/Systemd/User "Systemd/User"). Дата последней синхронизации: 9 Декабря 2016‎. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Systemd/User&diff=0&oldid=458617).

[systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") предоставляет пользователям возможность управления и контроля службами с отдельными процессами systemd для каждого пользователя, что позволяет ему запускать, останавливать, включать и отключать свои собственные службы. Это удобно применять для демонов и других служб, которые обычно выполняются для одного пользователя, например, [mpd](/index.php/Music_Player_Daemon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Music Player Daemon (Русский)") или для выполнения автоматизированных задач, таких как выборка почты. С некоторыми предостережениями можно даже запустить Xorg и весь оконный менеджер с помощью пользовательских служб.

## Contents

*   [1 Как это работает](#.D0.9A.D0.B0.D0.BA_.D1.8D.D1.82.D0.BE_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82)
*   [2 Основные настройки](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D1.8B.D0.B5_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)
    *   [2.1 D-Bus](#D-Bus)
    *   [2.2 Переменные окружения](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
        *   [2.2.1 Пример службы](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.D1.81.D0.BB.D1.83.D0.B6.D0.B1.D1.8B)
        *   [2.2.2 DISPLAY и XAUTHORITY](#DISPLAY_.D0.B8_XAUTHORITY)
        *   [2.2.3 PATH](#PATH)
        *   [2.2.4 pam_environment](#pam_environment)
    *   [2.3 Автоматический запуск systemd от имени пользователя](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_systemd_.D0.BE.D1.82_.D0.B8.D0.BC.D0.B5.D0.BD.D0.B8_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F)
*   [3 Xorg и systemd](#Xorg_.D0.B8_systemd)
    *   [3.1 Автоматический логин в Xorg без экранного менеджера](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.BB.D0.BE.D0.B3.D0.B8.D0.BD_.D0.B2_Xorg_.D0.B1.D0.B5.D0.B7_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0)
    *   [3.2 Xorg как служба systemd пользователь](#Xorg_.D0.BA.D0.B0.D0.BA_.D1.81.D0.BB.D1.83.D0.B6.D0.B1.D0.B0_systemd_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C)
*   [4 Написание пользовательских юнитов](#.D0.9D.D0.B0.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D0.BA.D0.B8.D1.85_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2)
    *   [4.1 Пример](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80)
    *   [4.2 Пример с переменными](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.D1.81_.D0.BF.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.BC.D0.B8)
    *   [4.3 Примечание о приложениях X](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.87.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BE_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F.D1.85_X)
    *   [4.4 Reading the journal](#Reading_the_journal)
*   [5 Некоторые случаи использования](#.D0.9D.D0.B5.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D0.B5_.D1.81.D0.BB.D1.83.D1.87.D0.B0.D0.B8_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [5.1 Постоянный терминальный мультиплексор](#.D0.9F.D0.BE.D1.81.D1.82.D0.BE.D1.8F.D0.BD.D0.BD.D1.8B.D0.B9_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D0.BC.D1.83.D0.BB.D1.8C.D1.82.D0.B8.D0.BF.D0.BB.D0.B5.D0.BA.D1.81.D0.BE.D1.80)
    *   [5.2 Оконный менеджер](#.D0.9E.D0.BA.D0.BE.D0.BD.D0.BD.D1.8B.D0.B9_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80)
*   [6 Kill user processes on logout](#Kill_user_processes_on_logout)
*   [7 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Как это работает

В соответствии с конфигурацией по умолчанию в `/etc/pam.d/system-login`, модуль `pam_systemd` автоматически запускает `systemd --user` в случае, когда пользователь в первый раз входит в систему . Этот процесс будет работать до тех пор, пока существует сессия этого пользователя, и будет убит, как только последний сеанс для пользователя будет закрыт. Когда включен [#Автоматический запуск systemd от имени пользователя](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_systemd_.D0.BE.D1.82_.D0.B8.D0.BC.D0.B5.D0.BD.D0.B8_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F), то процесс запускается при загрузке и убит не будет. Пользовательский процесс systemd отвечает за управление службами пользователей, которые могут быть использованы для запуска демонов или автоматизированных задач, со всеми преимуществами systemd, таких как активация сокета, таймеры, системы зависимостей или строгий контроль процесса через контрольные группы.

Аналогично системным службам, пользовательские службы расположены в следующих каталогах (отсортированы по возрастанию приоритета):

*   `/usr/lib/systemd/user/` где находятся службы, относящиеся к установленным пакетам.
*   `~/.local/share/systemd/user/` где находятся службы, относящиеся к пакетам, установленным в домашний каталог.
*   `/etc/systemd/user/` где находятся общесистемные пользовательские службы, созданные системным администратором.
*   `~/.config/systemd/user/` где пользователь размещает свои собственные службы.

При запуске пользовательского процесса systemd, у Вас откроется целевой `default.target`. Другие службы могут управляться вручную с помощью команды `systemctl --user`.

**Примечание:**

*   Имейте в виду, что `systemd --user` представляет собой процесс для каждого пользователя, а не для сессии. Смысл заключается в том, что большая часть ресурсов, обрабатываемых пользовательскими службами, такие как сокеты или файлы состояния будут создаваться отдельно для каждого пользователя (в его домашнем каталоге), и не за один сеанс. Это означает, что все пользовательские службы работают вне сеанса. Как следствие, программы, которые должны быть запущены внутри сессии, вероятно, прервут выполнение пользовательских служб. С помощью systemd в пользовательском сеансе обрабатывается довольно много данных. См [[1]](https://mail.gnome.org/archives/desktop-devel-list/2014-January/msg00079.html) и [[2]](http://lists.freedesktop.org/archives/systemd-devel/2014-March/017552.html) для получения подсказок о том, как идут дела.
*   `systemd --user` выполняется как отдельный процесс от родительского `systemd --system` процесса. Службы пользователей не могут ссылаться или зависеть от системных устройств.

## Основные настройки

Все пользовательские службы размещаются в `~/.config/systemd/user/`. Если вы хотите запускать службы при первом входе в систему, выполните `systemctl --user enable *service*` для любой службы, которую вы хотите сделать автозагрузочной.

### D-Bus

Некоторые программы нуждаются в [D-Bus](/index.php/D-Bus "D-Bus") пользовательской шине сообщений, и Systemd является менеджером шины сообщений пользователя.[[3]](https://www.archlinux.org/news/d-bus-now-launches-user-buses/) *dbus-daemon* запускается только один раз для каждого пользователя и для всех его сеансов с предусмотренными для этого `dbus.socket` и `dbus.service` службами.

**Примечание:** Если ранее Вы уже создали эти службы вручную в `/etc/systemd/user/` или `~/.config/systemd/user/`, то они могут быть удалены.

### Переменные окружения

Пользовательский процесс systemd не наследует какую-либо из [переменных окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)"), установленных в `.bashrc` или других. Существует несколько способов установить переменные окружения для systemd:

1.  Для переменной `$HOME` пользовательского каталога, используйте опцию `DefaultEnvironment` в `~/.config/systemd/user.conf`. Применяется только к части пользовательских служб.
2.  Используйте опцию `DefaultEnvironment` в `/etc/systemd/user.conf`. Применяется ко всем пользовательским службам.
3.  Добавление конфигурационного файла в `/etc/systemd/system/user@.service.d/`. Применяется ко всем пользовательским процессам; см [#Пример службы](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.D1.81.D0.BB.D1.83.D0.B6.D0.B1.D1.8B)
4.  Для временного изменения используйте `systemctl --user set-environment` или `systemctl --user import-environment`. Применяется ко всем пользовательским службам, созданным после установки переменных окружения, но не к службам, которые уже были запущены.
5.  Используйте `dbus-update-activation-environment --systemd --all` команда обеспечивается [dbus](/index.php/Dbus "Dbus"). Имеет тот же эффект, что и `systemctl --user import-environment`, но так же влияет на сессию D-Bus. Вы можете добавить это в конец вашего файла инициализации оболочки.

Одну переменную Вы можете установить в `PATH`.

#### Пример службы

Создайте [drop-in](/index.php/Systemd#Drop-in_files "Systemd") каталог `/etc/systemd/system/user@.service.d/` и внутри создайте файл с расширением `.conf` (например, `local.conf`):

 `/etc/systemd/system/user@.service.d/local.conf` 
```
[Service]
Environment="PATH=/usr/lib/ccache/bin/:$PATH"
Environment="EDITOR=nano -c"
Environment="BROWSER=firefox"
Environment="NO_AT_BRIDGE=1"
```

#### DISPLAY и XAUTHORITY

Переменная `DISPLAY` используется любым графическим приложением, чтобы знать, какой дисплей использовать, `XAUTHORITY`, чтобы указать путь к пользовательскому файлу `.Xauthority`, а также куки, необходимые для запуска Х-сервера. Если Вы планируете запускать графические приложения из процесса systemd, то эти переменные обязательно должны быть установлены. Systemd предоставляет скрипт в `/etc/X11/xinit/xinitrc.d/50-systemd-user.sh` для импорта этих переменных в пользовательскую сессию systemd на запуск X. [[4]](https://github.com/systemd/systemd/blob/v219/NEWS#L194) Так что если Вы не запускаете Х нестандартным образом, пользовательские службы должны знать переменные `DISPLAY` и `XAUTHORITY`.

#### PATH

Если изменить `PATH` и запланированный запуск приложений, которые используют службу systemd, Вы должны убедиться, что модифицированный `PATH` установлен и в среде systemd. Если предположить, что Вы установили переменную `PATH` в `.bash_profile`, то лучшим способом сделать systemd осведомленным о модификации `PATH` будет добавление в `.bash_profile` после `PATH` заданной переменной:

 `~/.bash_profile` 
```
systemctl --user import-environment PATH

```

#### pam_environment

Environment variables can be made available through use of the `pam_env.so` module. Create the file `~/.pam_environment`, for example:

 `~/.pam_environment` 
```
XDG_CONFIG_HOME DEFAULT=@{HOME}/.local/config
XDG_DATA_HOME   DEFAULT=@{HOME}/.local/data
```

For details about the syntax of the `.pam_environment` file see [Environment variables#Using pam_env](/index.php/Environment_variables#Using_pam_env "Environment variables"). You can verify that the configuration was successful by running the command `systemctl --user show-environment`:

 `$ systemctl --user show-environment` 
```
...
XDG_CONFIG_HOME=/home/*user*/.local/config
XDG_DATA_HOME=/home/*user*/.local/data
...
```

### Автоматический запуск systemd от имени пользователя

Пользовательский процесс systemd запускается сразу после первого входа пользователя в систему, и будет убит после завершения последнего сеанса пользователя. Иногда может быть полезно запустить службу сразу после загрузки, и поддерживать процесс systemd запущенным даже после завершения последнего сеанса пользователя, например, чтобы некоторый пользовательский процесс работал без какой-либо открытой сессии. Для этой цели используются долговременные службы. Используйте следующую команду, чтобы включить долговременную службу для конкретного пользователя:

```
# loginctl enable-linger *username*

```

**Важно:** служба systemd находится **вне** сессии, она запускается за пределами *logind*. Не используйте долговременные службы для включения автоматического входа в систему, иначе будет [перерыв в работе сессии](/index.php/General_troubleshooting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81.D0.B5.D1.81.D1.81.D0.B8.D0.B8 "General troubleshooting (Русский)").

## Xorg и systemd

There are several ways to run xorg within systemd units. Below there are two options, either by starting a new user session with an xorg process, or by launching xorg from a systemd user service.

### Автоматический логин в Xorg без экранного менеджера

This option will launch a system unit that will start a user session with an xorg server and then run the usual `~/.xinitrc` to launch the window manager, etc.

You need to have [#D-Bus](#D-Bus) correctly set up and [xlogin-git](https://aur.archlinux.org/packages/xlogin-git/) installed.

Set up your [xinitrc](/index.php/Xinitrc "Xinitrc") from the skeleton, so that it will source the files in `/etc/X11/xinit/xinitrc.d/`. Running your `~/.xinitrc` should not return, so either have `wait` as the last command, or add `exec` to the last command that will be called and which should not return (your window manager, for instance).

The session will use its own dbus daemon, but various systemd utilities will automatically connect to the `dbus.service` instance.

Finally, enable (**as root**) the *xlogin* service for automatic login at boot:

```
# systemctl enable xlogin@*username*

```

The user session lives entirely inside a systemd scope and everything in the user session should work just fine.

### Xorg как служба systemd пользователь

Alternatively, [xorg](/index.php/Xorg "Xorg") can be run from within a systemd user service. This is nice since other X-related units can be made to depend on xorg, etc, but on the other hand, it has some drawbacks explained below.

[xorg-server](https://www.archlinux.org/packages/?name=xorg-server) provides integration with systemd in two ways:

*   Can be run unprivileged, delegating device management to logind (see Hans de Goede commits around [this commit](http://cgit.freedesktop.org/xorg/xserver/commit/?id=82863656ec449644cd34a86388ba40f36cea11e9)).
*   Can be made into a socket activated service (see [this commit](http://cgit.freedesktop.org/xorg/xserver/commit/?id=b3d3ffd19937827bcbdb833a628f9b1814a6e189)). This removes the need for [systemd-xorg-launch-helper-git](https://aur.archlinux.org/packages/systemd-xorg-launch-helper-git/).

Unfortunately, to be able to run xorg in unprivileged mode, it needs to run inside a session. So, right now the handicap of running xorg as user service is that it must be run with root privileges (like before 1.16), and can't take advantage of the unprivileged mode introduced in 1.16.

**Примечание:** This is not a fundamental restriction imposed by logind, but the reason seems to be that xorg needs to know which session to take over, and right now it gets this information calling [logind](http://www.freedesktop.org/wiki/Software/systemd/logind)'s `GetSessionByPID` using its own pid as argument. See [this thread](http://lists.x.org/archives/xorg-devel/2014-February/040476.html) and [xorg sources](http://cgit.freedesktop.org/xorg/xserver/tree/hw/xfree86/os-support/linux/systemd-logind.c). It seems likely that xorg could be modified to get the session from the tty it is attaching to, and then it could run unprivileged from a user service outside a session.

**Важно:** On xorg 1.18 socket activation seems to be broken. The client triggering the activation deadlocks. See the upstream bug report [[5]](https://bugs.freedesktop.org/show_bug.cgi?id=93072). As a temporary workaround you can start the xorg server without socket activation, making sure the clients connect after a delay, so the server is fully started. There seems to be no nice mechanism te get startup notification for the X server.

This is how to launch xorg from a user service:

1\. Make xorg run with root privileges and for any user, by editing `/etc/X11/Xwrapper.config`

 `/etc/X11/Xwrapper.config` 
```
allowed_users=anybody
needs_root_rights=yes

```

2\. Add the following units to `~/.config/systemd/user`

 `~/.config/systemd/user/xorg@.socket` 
```
[Unit]
Description=Socket for xorg at display %i

[Socket]
ListenStream=/tmp/.X11-unix/X%i

```
 `~/.config/systemd/user/xorg@.service` 
```
[Unit]
Description=Xorg server at display %i

Requires=xorg@%i.socket
After=xorg@%i.socket

[Service]
Type=simple
SuccessExitStatus=0 1

ExecStart=/usr/bin/Xorg :%i -nolisten tcp -noreset -verbose 2 "vt${XDG_VTNR}"

```

where `${XDG_VTNR}` is the virtual terminal where xorg will be launched, either hard-coded in the service unit, or set in the systemd environment with

```
$ systemctl --user set-environment XDG_VTNR=1

```

**Note:** xorg should be launched at the same virtual terminal where the user logged in. Otherwise logind will consider the session inactive.

3\. Make sure to configure the `DISPLAY` environment variable as explained [above](#DISPLAY_.D0.B8_XAUTHORITY).

4\. Then, to enable socket activation for xorg on display 0 and tty 2 one would do:

```
$ systemctl --user set-environment XDG_VTNR=2     # So that xorg@.service knows which vt use
$ systemctl --user start xorg@0.socket            # Start listening on the socket for display 0

```

Now running any X application will launch xorg on virtual terminal 2 automatically.

The environment variable `XDG_VTNR` can be set in the systemd environment from `.bash_profile`, and then one could start any X application, including a window manager, as a systemd unit that depends on `xorg@0.socket`.

**Важно:** Currently running a window manager as a user service means it runs outside of a session with the problems this may bring: [break the session](/index.php/General_troubleshooting#Session_permissions "General troubleshooting"). However, it seems that systemd developers intend to make something like this possible. See [[6]](https://mail.gnome.org/archives/desktop-devel-list/2014-January/msg00079.html) and [[7]](http://lists.freedesktop.org/archives/systemd-devel/2014-March/017552.html)

## Написание пользовательских юнитов

### Пример

Ниже приведен пример варианта пользовательской службы mpd.

 `~/.config/systemd/user/mpd.service` 
```
[Unit]
Description=Music Player Daemon

[Service]
ExecStart=/usr/bin/mpd --no-daemon

[Install]
WantedBy=default.target

```

### Пример с переменными

Ниже приведен пример пользовательской версии `sickbeard.service`, которая учитывает все переменные окружения пользовательских каталогов, где SickBeard может найти некоторые файлы:

 `~/.config/systemd/user/sickbeard.service` 
```
[Unit]
Description=SickBeard Daemon

[Service]
ExecStart=/usr/bin/env python2 /opt/sickbeard/SickBeard.py --config %h/.sickbeard/config.ini --datadir %h/.sickbeard

[Install]
WantedBy=default.target

```

Как указано в [systemd.unit(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5), переменная `%h` заменяется домашней директорией пользователя, запускающего службу. Есть и другие переменные, которые учитываются на странице руководства [systemd](/index.php/Systemd "Systemd").

### Примечание о приложениях X

Most X apps need a `DISPLAY` variable to run. See [#DISPLAY и XAUTHORITY](#DISPLAY_.D0.B8_XAUTHORITY) for how to this variable is set for the entire systemd user instance.

### Reading the journal

The journal for the user can be read using the analogous command:

```
$ journalctl --user

```

To specify a unit, one can use

```
$ journalctl --user -u myunit.service

```

For a user unit, use

```
$ journalctl --user --user-unit myunit.service

```

Note that there seems to be some sort of bug that can sometimes stop output from user services from being properly attributed to their service unit. Therefore, filtering by the `-u` may unwittingly exclude some of the output from the service units.

## Некоторые случаи использования

### Постоянный терминальный мультиплексор

You may wish your user session to default to running a terminal multiplexer, such as [GNU Screen](/index.php/GNU_Screen "GNU Screen") or [Tmux](/index.php/Tmux "Tmux"), in the background rather than logging you into a window manager session. Separating login from X login is most likely only useful for those who boot to a TTY instead of to a display manager (in which case you can simply bundle everything you start in with myStuff.target).

To create this type of user session, procede as above, but instead of creating wm.target, create multiplexer.target:

```
[Unit]
Description=Terminal multiplexer
Documentation=info:screen man:screen(1) man:tmux(1)
After=cruft.target
Wants=cruft.target

[Install]
Alias=default.target
```

`cruft.target`, like `mystuff.target` above, should start anything you think should run before tmux or screen starts (or which you want started at boot regardless of timing), such as a GnuPG daemon session.

You then need to create a service for your multiplexer session. Here is a sample service, using tmux as an example and sourcing a gpg-agent session which wrote its information to `/tmp/gpg-agent-info`. This sample session, when you start X, will also be able to run X programs, since DISPLAY is set.

```
[Unit]
Description=tmux: A terminal multiplixer 
Documentation=man:tmux(1)
After=gpg-agent.service
Wants=gpg-agent.service

[Service]
Type=forking
ExecStart=/usr/bin/tmux start
ExecStop=/usr/bin/tmux kill-server
Environment=DISPLAY=:0
EnvironmentFile=/tmp/gpg-agent-info

[Install]
WantedBy=multiplexer.target
```

Once this is done, `systemctl --user enable` `tmux.service`, `multiplexer.target` and any services you created to be run by `cruft.target` and you should be set to go! Activated `user-session@.service` as described above, but be sure to remove the `Conflicts=getty@tty1.service` from `user-session@.service`, since your user session will not be taking over a TTY. Congratulations! You have a running terminal multiplexer and some other useful programs ready to start at boot!

### Оконный менеджер

To run a window manager as a systemd service, you first need to run [#Xorg as a systemd user service](#Xorg_as_a_systemd_user_service). In the following we will use awesome as an example:

 `~/.config/systemd/user/awesome.service` 
```
[Unit]
Description=Awesome window manager
After=xorg.target
Requires=xorg.target

[Service]
ExecStart=/usr/bin/awesome
Restart=always
RestartSec=10

[Install]
WantedBy=wm.target

```

**Примечание:** The `[Install]` section includes a `WantedBy` part. When using `systemctl --user enable` it will link this as `~/.config/systemd/user/wm.target.wants/*window_manager*.service`, allowing it to be started at login. Is recommended to enable this service, not to link it manually.

## Kill user processes on logout

Arch Linux builds the [systemd](https://www.archlinux.org/packages/?name=systemd) package with `--without-kill-user-processes`, setting `KillUserProcesses` to `no` by default. This setting causes user processes not to be killed when the user completely logs out. To change this behavior in order to have all user processes killed on the user's logout, set `KillUserProcesses=yes` in `/etc/systemd/logind.conf`.

Note that changing this setting breaks terminal multiplexers such as [tmux](/index.php/Tmux "Tmux") and [GNU Screen](/index.php/GNU_Screen "GNU Screen"). If you change this setting, you can still use a terminal multiplexer by using `systemd-run` as follows:

```
$ systemd-run --scope --user *command* *args*

```

For example, to run `screen` you would do:

```
$ systemd-run --scope --user screen -S *foo*

```

## Смотрите также

*   [KaiSforza's Bitbucket wiki](https://bitbucket.org/KaiSforza/systemd-user-units/wiki/Home)
*   [Zoqaeski's units on GitHub](https://github.com/zoqaeski/systemd-user-units)
*   [Arch forum thread about changes in systemd 206 user instances](https://bbs.archlinux.org/viewtopic.php?id=167115)