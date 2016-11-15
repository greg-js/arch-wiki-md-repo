**Состояние перевода:** На этой странице представлен перевод статьи [systemd/User](/index.php/Systemd/User "Systemd/User"). Дата последней синхронизации: 24 марта 2016‎. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Systemd/User&diff=0&oldid=427531).

[systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") предоставляет пользователям возможность управления и контроля службами с отдельным экземпляром Systemd для каждого пользователя, что позволяет пользователю запускать, останавливать, включать и отключать свои собственные службы. Это удобно применять для демонов и других служб, которые обычно выполняются для одного пользователя, например, [mpd](/index.php/Music_Player_Daemon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Music Player Daemon (Русский)") или для выполнения автоматизированных задач, таких как выборка почты. С некоторыми предостережениями можно даже запустить Xorg и весь оконный менеджер из пользовательских служб.

## Contents

*   [1 Как это работает](#.D0.9A.D0.B0.D0.BA_.D1.8D.D1.82.D0.BE_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82)
*   [2 Основные настройки](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D1.8B.D0.B5_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)
    *   [2.1 D-Bus](#D-Bus)
    *   [2.2 Переменные окружения](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
        *   [2.2.1 Пример службы](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.D1.81.D0.BB.D1.83.D0.B6.D0.B1.D1.8B)
        *   [2.2.2 DISPLAY и XAUTHORITY](#DISPLAY_.D0.B8_XAUTHORITY)
        *   [2.2.3 PATH](#PATH)
    *   [2.3 Автоматический запуск пользовательского экземпляра systemd](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D1.8D.D0.BA.D0.B7.D0.B5.D0.BC.D0.BF.D0.BB.D1.8F.D1.80.D0.B0_systemd)
*   [3 Xorg и systemd](#Xorg_.D0.B8_systemd)
    *   [3.1 Автоматический логин в Xorg без экранного менеджера](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.BB.D0.BE.D0.B3.D0.B8.D0.BD_.D0.B2_Xorg_.D0.B1.D0.B5.D0.B7_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0)
    *   [3.2 Xorg как служба systemd пользователь](#Xorg_.D0.BA.D0.B0.D0.BA_.D1.81.D0.BB.D1.83.D0.B6.D0.B1.D0.B0_systemd_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C)
*   [4 Написание пользовательских юнитов](#.D0.9D.D0.B0.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D0.BA.D0.B8.D1.85_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2)
    *   [4.1 Пример](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80)
    *   [4.2 Пример с переменными](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.D1.81_.D0.BF.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.BC.D0.B8)
    *   [4.3 Примечание о приложениях X](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.87.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BE_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F.D1.85_X)
*   [5 Некоторые случаи использования](#.D0.9D.D0.B5.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D0.B5_.D1.81.D0.BB.D1.83.D1.87.D0.B0.D0.B8_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [5.1 Постоянный терминальный мультиплексор](#.D0.9F.D0.BE.D1.81.D1.82.D0.BE.D1.8F.D0.BD.D0.BD.D1.8B.D0.B9_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D0.BC.D1.83.D0.BB.D1.8C.D1.82.D0.B8.D0.BF.D0.BB.D0.B5.D0.BA.D1.81.D0.BE.D1.80)
    *   [5.2 Оконный менеджер](#.D0.9E.D0.BA.D0.BE.D0.BD.D0.BD.D1.8B.D0.B9_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Как это работает

В соответствии с конфигурацией по умолчанию в `/etc/pam.d/system-login`, модуль `pam_systemd` автоматически запускает `systemd --user` в случае, когда пользователь в первый раз входит в систему . Этот процесс будет работать до тех пор, пока есть некоторая сессия для этого пользователя, и будет убит, как только последний сеанс для пользователя будет закрыт. Когда включен [#Автоматический запуск пользовательского экземпляра systemd](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D1.8D.D0.BA.D0.B7.D0.B5.D0.BC.D0.BF.D0.BB.D1.8F.D1.80.D0.B0_systemd), то экземпляр запускается при загрузке и убит не будет. Пользовательский экземпляр systemd отвечает за управление службами пользователей, которые могут быть использованы для запуска демонов или автоматизированных задач, со всеми преимуществами systemd, таких как активация сокета, таймеры, системы зависимостей или строгий контроль процесса через контрольные группы.

Аналогично системным службам, пользовательские службы расположены в следующих каталогах (отсортированы по возрастанию приоритета):

*   `/usr/lib/systemd/user/` где находятся службы, относящиеся к установленным пакетам.
*   `~/.local/share/systemd/user/` где находятся службы, относящиеся к пакетам, установленным в домашний каталог.
*   `/etc/systemd/user/` где находятся общесистемные пользовательские службы, созданные системным администратором.
*   `~/.config/systemd/user/` где пользователь размещает свои собственные службы.

При запуске пользовательского экземпляра systemd, у Вас откроется целевой `default.target`. Другие службы могут управляться вручную с помощью команды `systemctl --user`.

**Примечание:**

*   Имейте в виду, что начиная с версии 206, `systemd --user` представляет собой процесс для каждого пользователя, а не для сессии. Смысл заключается в том, что большая часть ресурсов, обрабатываемых пользовательскими службами, такие как сокеты или файлы состояния будут создаваться отдельно для каждого пользователя (в домашнем каталоге пользователя), и не за один сеанс. Это означает, что все пользовательские службы работают вне сеанса. Как следствие, программы, которые должны быть запущены внутри сессии, вероятно, прервут выполнение пользовательских служб. Способом Systemd обрабатываются пользовательские сеансы довольно много данных. См [[1]](https://mail.gnome.org/archives/desktop-devel-list/2014-January/msg00079.html) и [[2]](http://lists.freedesktop.org/archives/systemd-devel/2014-March/017552.html) для получения подсказок о том, как идут дела.
*   `systemd --user` выполняется как отдельный процесс от родительского `systemd --system` процесса. Службы пользователей не могут ссылаться на или зависеть от системных устройств.

## Основные настройки

All the user services will be placed in `~/.config/systemd/user/`. If you want to run services on first login, execute `systemctl --user enable *service*` for any service you want to be autostarted.

### D-Bus

Some programs will need a [D-Bus](/index.php/D-Bus "D-Bus") user message bus. Traditionally it had been started when launching a desktop environment via `dbus-launch`, but since version 226, systemd has become the manager of the user message bus.[[3]](https://www.archlinux.org/news/d-bus-now-launches-user-buses/) The *dbus-daemon* is started once per user for all sessions with the provided `dbus.socket` and `dbus.service` user units.

**Примечание:** If you had previously created these units manually under `/etc/systemd/user/` or `~/.config/systemd/user/`, they can be removed.

### Переменные окружения

The user instance of systemd does not inherit any of the [environment variables](/index.php/Environment_variables "Environment variables") set in places like `.bashrc` etc. There are several ways to set environment variables for the systemd user instance:

1.  For users with a `$HOME` directory, use the `DefaultEnvironment` option in `~/.config/systemd/user.conf`. Affects only that user's user unit.
2.  Use the `DefaultEnvironment` option in `/etc/systemd/user.conf` file. Affects all user units.
3.  Add a drop-in config file in `/etc/systemd/system/user@.service.d/`. Affects all user units; see [#Service example](#Service_example)
4.  At any time, use `systemctl --user set-environment` or `systemctl --user import-environment`. Affects all user units started after setting the environment variables, but not the units that were already running.
5.  Using the `dbus-update-activation-environment --systemd --all` command provided by [dbus](/index.php/Dbus "Dbus"). Has the same effect as `systemctl --user import-environment`, but also affects the D-Bus session. You can add this to the end of your shell initialization file.

One variable you may want to set is `PATH`.

#### Пример службы

Create the [drop-in](/index.php/Systemd#Drop-in_snippets "Systemd") directory `/etc/systemd/system/user@.service.d/` and inside create a file that has the extension `.conf` (e.g. `local.conf`):

 `/etc/systemd/system/user@.service.d/local.conf` 
```
[Service]
Environment="PATH=/usr/lib/ccache/bin/:$PATH"
Environment="EDITOR=nano -c"
Environment="BROWSER=firefox"
Environment="NO_AT_BRIDGE=1"
```

#### DISPLAY и XAUTHORITY

`DISPLAY` is used by any X application to know which display to use and `XAUTHORITY` to provide a path to the user's `.Xauthority` file and thus the cookie needed to access the X server. If you plan on launching X applications from systemd units, these variables need to be set. Since [version 219](https://github.com/systemd/systemd/blob/v219/NEWS#L194), systemd provides a script in `/etc/X11/xinit/xinitrc.d/50-systemd-user.sh` to import those variables into the systemd user session on X launch. So unless you start X in a nonstandard way, user services should be aware of the `DISPLAY` and `XAUTHORITY`.

#### PATH

As any other environment variable you set in `.bashrc` or `.bash_profile`, the `PATH` variable is not available to systemd. If you customize your `PATH` and plan on launching applications that make use of it from systemd units, you should make sure the modified `PATH` is set on the systemd environment. Assuming you set your `PATH` in `.bash_profile`, the best way to make systemd aware of your modified `PATH` is by adding the following to `.bash_profile` after the `PATH` variable is set:

 `~/.bash_profile` 
```
systemctl --user import-environment PATH

```

### Автоматический запуск пользовательского экземпляра systemd

The systemd user instance is started after the first login of a user and killed after the last session of the user is closed. Sometimes it may be useful to start it right after boot, and keep the systemd user instance running after the last session closes, for instance to have some user process running without any open session. Lingering is used to that effect. Use the following command to enable lingering for specific user:

```
# loginctl enable-linger *username*

```

**Важно:** systemd services are **not** sessions, they run outside of *logind*. Do not use lingering to enable automatic login as it will [break the session](/index.php/General_troubleshooting#Session_permissions "General troubleshooting").

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

Since version 1.16 [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) provides better integration with systemd in two ways:

*   Can be run unprivileged, delegating device management to logind (see Hans de Goede commits around [this commit](http://cgit.freedesktop.org/xorg/xserver/commit/?id=82863656ec449644cd34a86388ba40f36cea11e9)).
*   Can be made into a socket activated service (see [this commit](http://cgit.freedesktop.org/xorg/xserver/commit/?id=b3d3ffd19937827bcbdb833a628f9b1814a6e189)). This removes the need for [systemd-xorg-launch-helper-git](https://aur.archlinux.org/packages/systemd-xorg-launch-helper-git/).

Unfortunately, to be able to run xorg in unprivileged mode, it needs to run inside a session. So, right now the handicap of running xorg as user service is that it must be run with root privileges (like before 1.16), and can't take advantage of the unprivileged mode introduced in 1.16.

**Примечание:** This is not a fundamental restriction imposed by logind, but the reason seems to be that xorg needs to know which session to take over, and right now it gets this information calling [logind](http://www.freedesktop.org/wiki/Software/systemd/logind)'s `GetSessionByPID` using its own pid as argument. See [this thread](http://lists.x.org/archives/xorg-devel/2014-February/040476.html) and [xorg sources](http://cgit.freedesktop.org/xorg/xserver/tree/hw/xfree86/os-support/linux/systemd-logind.c). It seems likely that xorg could be modified to get the session from the tty it is attaching to, and then it could run unprivileged from a user service outside a session.

**Важно:** On xorg 1.18 socket activation seems to be broken. The client triggering the activation deadlocks. See the upstream bug report [[4]](https://bugs.freedesktop.org/show_bug.cgi?id=93072). As a temporary workaround you can start the xorg server without socket activation, making sure the clients connect after a delay, so the server is fully started. There seems to be no nice mechanism te get startup notification for the X server.

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

3\. Make sure to configure the `DISPLAY` environment variable as explained [above](#DISPLAY).

4\. Then, to enable socket activation for xorg on display 0 and tty 2 one would do:

```
$ systemctl --user set-environment XDG_VTNR=2     # So that xorg@.service knows which vt use
$ systemctl --user start xorg@0.socket            # Start listening on the socket for display 0

```

Now running any X application will launch xorg on virtual terminal 2 automatically.

The environment variable `XDG_VTNR` can be set in the systemd environment from `.bash_profile`, and then one could start any X application, including a window manager, as a systemd unit that depends on `xorg@0.socket`.

**Важно:** Currently running a window manager as a user service means it runs outside of a session with the problems this may bring: [break the session](/index.php/General_troubleshooting#Session_permissions "General troubleshooting"). However, it seems that systemd developers intend to make something like this possible. See [[5]](https://mail.gnome.org/archives/desktop-devel-list/2014-January/msg00079.html) and [[6]](http://lists.freedesktop.org/archives/systemd-devel/2014-March/017552.html)

## Написание пользовательских юнитов

### Пример

The following is an example of a user version of the mpd service.

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

The following is an example of a user version of `sickbeard.service`, which takes into account variable home directories where SickBeard can find certain files:

 `~/.config/systemd/user/sickbeard.service` 
```
[Unit]
Description=SickBeard Daemon

[Service]
ExecStart=/usr/bin/env python2 /opt/sickbeard/SickBeard.py --config %h/.sickbeard/config.ini --datadir %h/.sickbeard

[Install]
WantedBy=default.target

```

As detailed in `man systemd.unit`, the `%h` variable is replaced by the home directory of the user running the service. There are other variables that can be taken into account in the [systemd](/index.php/Systemd "Systemd") manpages.

### Примечание о приложениях X

Most X apps need a `DISPLAY` variable to run. See [#DISPLAY и XAUTHORITY](#DISPLAY_.D0.B8_XAUTHORITY) for how to this variable is set for the entire systemd user instance.

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

## Смотрите также

*   [KaiSforza's Bitbucket wiki](https://bitbucket.org/KaiSforza/systemd-user-units/wiki/Home)
*   [Zoqaeski's units on GitHub](https://github.com/zoqaeski/systemd-user-units)
*   [Arch forum thread about changes in systemd 206 user instances](https://bbs.archlinux.org/viewtopic.php?id=167115)