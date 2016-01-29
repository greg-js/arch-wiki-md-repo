# systemd/User

Related articles

*   [systemd](/index.php/Systemd "Systemd")
*   [Automatic login to virtual console](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console")
*   [Start X at login](/index.php/Start_X_at_login "Start X at login")

[systemd](/index.php/Systemd "Systemd") offers users the ability to manage services under the user's control with a per-user systemd instance, enabling users to start, stop, enable, and disable their own units. This is convenient for daemons and other services that are commonly run for a single user, such as [mpd](/index.php/Mpd "Mpd"), or to perform automated tasks like fetching mail. With some caveats it is even possible to run xorg and the entire window manager from user services.

## Contents

*   [1 How it works](#How_it_works)
*   [2 Basic setup](#Basic_setup)
    *   [2.1 D-Bus](#D-Bus)
    *   [2.2 Environment variables](#Environment_variables)
        *   [2.2.1 DISPLAY and XAUTHORITY](#DISPLAY_and_XAUTHORITY)
        *   [2.2.2 PATH](#PATH)
    *   [2.3 Automatic start-up of systemd user instances](#Automatic_start-up_of_systemd_user_instances)
*   [3 Xorg and systemd](#Xorg_and_systemd)
    *   [3.1 Automatic login into Xorg without display manager](#Automatic_login_into_Xorg_without_display_manager)
    *   [3.2 Xorg as a systemd user service](#Xorg_as_a_systemd_user_service)
*   [4 Writing user units](#Writing_user_units)
    *   [4.1 Example](#Example)
    *   [4.2 Example with variables](#Example_with_variables)
    *   [4.3 Note about X applications](#Note_about_X_applications)
*   [5 Some use cases](#Some_use_cases)
    *   [5.1 Persistent terminal multiplexer](#Persistent_terminal_multiplexer)
    *   [5.2 Window manager](#Window_manager)
*   [6 See also](#See_also)

## How it works

As per default configuration in `/etc/pam.d/system-login`, the `pam_systemd` module automatically launches a `systemd --user` instance when the user logs in for the first time. This process will survive as long as there is some session for that user, and will be killed as soon as the last session for the user is closed. When [#Automatic start-up of systemd user instances](#Automatic_start-up_of_systemd_user_instances) is enabled, the instance is started on boot and will not be killed. The systemd user instance is responsible for managing user services, which can be used to run daemons or automated tasks, with all the benefits of systemd, such as socket activation, timers, dependency system or strict process control via cgroups.

Similarly to system units, user units are located in the following directories (ordered by ascending precedence):

*   `/usr/lib/systemd/user/` where units provided by installed packages belong.
*   `~/.local/share/systemd/user/` where units of packages that have been installed in the home directory belong.
*   `/etc/systemd/user/` where system-wide user units are placed by the system administrator.
*   `~/.config/systemd/user/` where the user puts its own units.

When systemd user instance starts, it brings up the target `default.target`. Other units can be controlled manually with `systemctl --user`.

**Note:**

*   Be aware that since version 206, the `systemd --user` instance is a per-user process, and not per-session. The rationale is that most resources handled by user services, like sockets or state files will be per-user (live on the user's home dir) and not per session. This means that all user services run outside of a session. As a consequence, programs that need to be run inside a session will probably break in user services. The way systemd handles user sessions is pretty much in flux. See [[1]](https://mail.gnome.org/archives/desktop-devel-list/2014-January/msg00079.html) and [[2]](http://lists.freedesktop.org/archives/systemd-devel/2014-March/017552.html) for some hints on where things are going.
*   `systemd --user` runs as a separate process from the `systemd --system` process. User units can not reference or depend on system units.

## Basic setup

All the user services will be placed in `~/.config/systemd/user/`. If you want to run services on first login, execute `systemctl --user enable _service_` for any service you want to be autostarted.

### D-Bus

Some programs will need a [D-Bus](/index.php/D-Bus "D-Bus") user message bus. Traditionally it had been started when launching a desktop environment via `dbus-launch`, but since version 226, systemd has become the manager of the user message bus.[[3]](https://www.archlinux.org/news/d-bus-now-launches-user-buses/) The _dbus-daemon_ is started once per user for all sessions with the provided `dbus.socket` and `dbus.service` user units.

**Note:** If you had previously created these units manually under `/etc/systemd/user/` or `~/.config/systemd/user/`, they can be removed.

### Environment variables

The user instance of systemd does not inherit any of the [environment variables](/index.php/Environment_variables "Environment variables") set in places like `.bashrc` etc. There are several ways to set environment variables for the systemd user instance:

1.  For users with a `$HOME` directory, use the `DefaultEnvironment` option in `~/.config/systemd/user.conf`. Affects only that user's user unit.
2.  Use the `DefaultEnvironment` option in `/etc/systemd/user.conf` file. Affects all user units.
3.  Add a drop-in config file in `/etc/systemd/system/user@.service.d/`. Affects all user units.
4.  At any time, use `systemctl --user set-environment` or `systemctl --user import-environment`. Affects all user units started after setting the environment variables, but not the units that were already running.
5.  Using the `dbus-update-activation-environment --systemd --all` command provided by [dbus](/index.php/Dbus "Dbus"). Has the same effect as `systemctl --user import-environment`, but also affects the D-Bus session. You can add this to the end of your shell initialization file.

One variable you may want to set is `PATH`.

#### DISPLAY and XAUTHORITY

`DISPLAY` is used by any X application to know which display to use and `XAUTHORITY` to provide a path to the user's `.Xauthority` file and thus the cookie needed to access the X server. If you plan on launching X applications from systemd units, these variables need to be set. Since [version 219](http://cgit.freedesktop.org/systemd/systemd/tree/NEWS?id=v219#n194), systemd provides a script in `/etc/X11/xinit/xinitrc.d/50-systemd-user.sh` to import those variables into the systemd user session on X launch. So unless you start X in a nonstandard way, user services should be aware of the `DISPLAY` and `XAUTHORITY`.

#### PATH

As any other environment variable you set in `.bashrc` or `.bash_profile`, the `PATH` variable is not available to systemd. If you customize your `PATH` and plan on launching applications that make use of it from systemd units, you should make sure the modified `PATH` is set on the systemd environment. Assuming you set your `PATH` in `.bash_profile`, the best way to make systemd aware of your modified `PATH` is by adding the following to `.bash_profile` after the `PATH` variable is set:

 `~/.bash_profile` 

```
systemctl --user import-environment PATH

```

### Automatic start-up of systemd user instances

The systemd user instance is started after the first login of a user and killed after the last session of the user is closed. Sometimes it may be useful to start it right after boot, and keep the systemd user instance running after the last session closes, for instance to have some user process running without any open session. Lingering is used to that effect. Use the following command to enable lingering for specific user:

```
# loginctl enable-linger _username_

```

**Warning:** systemd services are **not** sessions, they run outside of _logind_. Do not use lingering to enable automatic login as it will [break the session](/index.php/General_troubleshooting#Session_permissions "General troubleshooting").

## Xorg and systemd

There are several ways to run xorg within systemd units. Below there are two options, either by starting a new user session with an xorg process, or by launching xorg from a systemd user service.

### Automatic login into Xorg without display manager

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** This setup ends up with two user D-Bus buses, one for the desktop, and an other for systemd. Why can't we use the systemd one alone? (Discuss in [Talk:Systemd/User#](https://wiki.archlinux.org/index.php/Talk:Systemd/User))

This option will launch a system unit that will start a user session with an xorg server and then run the usual `~/.xinitrc` to launch the window manager, etc.

You need to have [#D-Bus](#D-Bus) correctly set up and [xlogin-git](https://aur.archlinux.org/packages/xlogin-git/)<sup><small>AUR</small></sup> installed.

Set up your [xinitrc](/index.php/Xinitrc "Xinitrc") from the skeleton, so that it will source the files in `/etc/X11/xinit/xinitrc.d/`. Running your `~/.xinitrc` should not return, so either have `wait` as the last command, or add `exec` to the last command that will be called and which should not return (your window manager, for instance).

The session will use its own dbus daemon, but various systemd utilities will automatically connect to the `dbus.service` instance.

Finally, enable (**as root**) the _xlogin_ service for automatic login at boot:

```
# systemctl enable xlogin@_username_

```

The user session lives entirely inside a systemd scope and everything in the user session should work just fine.

### Xorg as a systemd user service

Alternatively, [xorg](/index.php/Xorg "Xorg") can be run from within a systemd user service. This is nice since other X-related units can be made to depend on xorg, etc, but on the other hand, it has some drawbacks explained below.

Since version 1.16 [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) provides better integration with systemd in two ways:

*   Can be run unprivileged, delegating device management to logind (see Hans de Goede commits around [this commit](http://cgit.freedesktop.org/xorg/xserver/commit/?id=82863656ec449644cd34a86388ba40f36cea11e9)).
*   Can be made into a socket activated service (see [this commit](http://cgit.freedesktop.org/xorg/xserver/commit/?id=b3d3ffd19937827bcbdb833a628f9b1814a6e189)). This removes the need for [systemd-xorg-launch-helper-git](https://aur.archlinux.org/packages/systemd-xorg-launch-helper-git/)<sup><small>AUR</small></sup>.

Unfortunately, to be able to run xorg in unprivileged mode, it needs to run inside a session. So, right now the handicap of running xorg as user service is that it must be run with root privileges (like before 1.16), and can't take advantage of the unprivileged mode introduced in 1.16.

**Note:** This is not a fundamental restriction imposed by logind, but the reason seems to be that xorg needs to know which session to take over, and right now it gets this information calling [logind](http://www.freedesktop.org/wiki/Software/systemd/logind)'s `GetSessionByPID` using its own pid as argument. See [this thread](http://lists.x.org/archives/xorg-devel/2014-February/040476.html) and [xorg sources](http://cgit.freedesktop.org/xorg/xserver/tree/hw/xfree86/os-support/linux/systemd-logind.c). It seems likely that xorg could be modified to get the session from the tty it is attaching to, and then it could run unprivileged from a user service outside a session.

**Warning:** On xorg 1.18 socket activation seems to be broken. The client triggering the activation deadlocks. See the upstream bug report [[4]](https://bugs.freedesktop.org/show_bug.cgi?id=93072). As a temporary workaround you can start the xorg server without socket activation, making sure the clients connect after a delay, so the server is fully started. There seems to be no nice mechanism te get startup notification for the X server.

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

**Warning:** Currently running a window manager as a user service means it runs outside of a session with the problems this may bring: [break the session](/index.php/General_troubleshooting#Session_permissions "General troubleshooting"). However, it seems that systemd developers intend to make something like this possible. See [[5]](https://mail.gnome.org/archives/desktop-devel-list/2014-January/msg00079.html) and [[6]](http://lists.freedesktop.org/archives/systemd-devel/2014-March/017552.html)

## Writing user units

### Example

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

### Example with variables

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

### Note about X applications

Most X apps need a `DISPLAY` variable to run. See [#DISPLAY and XAUTHORITY](#DISPLAY_and_XAUTHORITY) for how to this variable is set for the entire systemd user instance.

## Some use cases

### Persistent terminal multiplexer

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** References `user-session@.service` instead of `user@.service`; the latter does not contain `Conflicts=getty@tty1.service`. (Discuss in [Talk:Systemd/User#](https://wiki.archlinux.org/index.php/Talk:Systemd/User))

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

### Window manager

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

**Note:** The `[Install]` section includes a `WantedBy` part. When using `systemctl --user enable` it will link this as `~/.config/systemd/user/wm.target.wants/_window_manager_.service`, allowing it to be started at login. Is recommended to enable this service, not to link it manually.

## See also

*   [KaiSforza's Bitbucket wiki](https://bitbucket.org/KaiSforza/systemd-user-units/wiki/Home)
*   [Zoqaeski's units on GitHub](https://github.com/zoqaeski/systemd-user-units)
*   [Collection of useful systemd user units](https://github.com/grawity/systemd-user-units)
*   [Arch forum thread about changes in systemd 206 user instances](https://bbs.archlinux.org/viewtopic.php?id=167115)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Systemd/User&oldid=416204](https://wiki.archlinux.org/index.php?title=Systemd/User&oldid=416204)"