Related articles

*   [Display manager](/index.php/Display_manager "Display manager")
*   [Xorg](/index.php/Xorg "Xorg")
*   [xprofile](/index.php/Xprofile "Xprofile")
*   [Xresources](/index.php/Xresources "Xresources")

From [Wikipedia](https://en.wikipedia.org/wiki/xinit "wikipedia:xinit"):

	The **xinit** program allows a user to manually start an [Xorg](/index.php/Xorg "Xorg") display server. The [startx(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/startx.1) script is a front-end for [xinit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xinit.1).

*xinit* is typically used to start [window managers](/index.php/Window_manager "Window manager") or [desktop environments](/index.php/Desktop_environment "Desktop environment"). While you can also use *xinit* to run GUI applications without a window manager, many graphical applications expect an [EWMH](https://en.wikipedia.org/wiki/Extended_Window_Manager_Hints "wikipedia:Extended Window Manager Hints") compliant window manager. [Display managers](/index.php/Display_manager "Display manager") start [Xorg](/index.php/Xorg "Xorg") for you and generally source [xprofile](/index.php/Xprofile "Xprofile").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 xinitrc](#xinitrc)
    *   [2.2 xserverrc](#xserverrc)
*   [3 Usage](#Usage)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Override xinitrc](#Override_xinitrc)
    *   [4.2 Autostart X at login](#Autostart_X_at_login)
    *   [4.3 Switching between desktop environments/window managers](#Switching_between_desktop_environments/window_managers)
    *   [4.4 Starting applications without a window manager](#Starting_applications_without_a_window_manager)
    *   [4.5 Output redirection using startx](#Output_redirection_using_startx)

## Installation

[Install](/index.php/Install "Install") the [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit) package.

## Configuration

*xinit* and *startx* take an optional client program argument, see [#Override xinitrc](#Override_xinitrc). If you do not provide one they will look for `~/.xinitrc` to run as a shell script to start up client programs.

### xinitrc

`~/.xinitrc` is handy to run programs depending on X and set environment variables on X server startup. If it is present in a user's home directory, *startx* and *xinit* execute it. Otherwise *startx* will run the default `/etc/X11/xinit/xinitrc`.

**Note:** *Xinit* has its own default behaviour instead of executing the file. See [xinit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xinit.1) for details.

This default xinitrc will start a basic environment with [Twm](/index.php/Twm "Twm"), [xorg-xclock](https://www.archlinux.org/packages/?name=xorg-xclock) and [Xterm](/index.php/Xterm "Xterm") (assuming that the necessary packages are installed). Therefore, to start a different window manager or desktop environment, first create a copy of the default `xinitrc` in your home directory:

```
$ cp /etc/X11/xinit/xinitrc ~/.xinitrc

```

Then [edit](/index.php/Help:Reading#Append,_add,_create,_edit "Help:Reading") the file and replace the default programs with desired commands. Remember that lines following a command using `exec` would be ignored. For example, to start `xscreensaver` in the background and then start [openbox](/index.php/Openbox#Standalone "Openbox"), use the following:

 `~/.xinitrc` 
```
...
xscreensaver &
exec openbox-session
```

**Note:** At the very least, ensure that the last if block in `/etc/X11/xinit/xinitrc` is present in your `~/.xinitrc` file to ensure that the scripts in `/etc/X11/xinit/xinitrc.d` are sourced.

Long-running programs started before the window manager, such as a screensaver and wallpaper application, must either fork themselves or be run in the background by appending an `&` sign. Otherwise, the script would halt and wait for each program to exit before executing the window manager or desktop environment. Note that some programs should instead not be forked, to avoid race bugs, as is the case of [xrdb](/index.php/Xrdb "Xrdb"). Prepending `exec` will replace the script process with the window manager process, so that X does not exit even if this process forks to the background.

### xserverrc

The `xserverrc` file is a shell script responsible for starting up the X server. Both *startx* and *xinit* execute `~/.xserverrc` if it exists, *startx* will use `/etc/X11/xinit/xserverrc` otherwise.

In order to maintain an [authenticated session](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") with `logind` and to prevent bypassing the screen locker by switching terminals, [Xorg](/index.php/Xorg "Xorg") has to be started on the same virtual terminal where the login occurred [[1]](http://blog.falconindy.com/articles/back-to-basics-with-x-and-systemd.html). Therefore it is recommended to specify `vt$XDG_VTNR` in the `~/.xserverrc` file:

 `~/.xserverrc` 
```
#!/bin/sh

exec /usr/bin/Xorg -nolisten tcp "$@" vt$XDG_VTNR

```

See [Xserver(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xserver.1) for a list of all command line options.

**Tip:** `-nolisten local` can be added after `-nolisten tcp` to disable abstract sockets of X11 to help with isolation. There is a [quick background](https://tstarling.com/blog/2016/06/x11-security-isolation/) on how this potentially affects X11 security.

Alternatively, if you wish to have the X display on a separate console from the one where the server is invoked, you can do so by using the X server wrapper provided by `/usr/lib/systemd/systemd-multi-seat-x`. For convenience, *xinit* and *startx* can be set up to use this wrapper by modifying your `~/.xserverrc`.

**Note:** To re-enable redirection of the output from X session into the Xorg log file, add the `-keeptty` option. See [Xorg#Broken redirection](/index.php/Xorg#Broken_redirection "Xorg") for details.

## Usage

To run Xorg as a regular user, issue:

```
$ startx

```

Or if [#xserverrc](#xserverrc) is configured:

```
$ xinit -- :1

```

**Note:** *xinit* does not handle multiple displays when another X server is already started. For that you must specify the display by appending `-- :*display_number*`, where `*display_number*` is `1` or more.

Your window manager (or desktop environment) of choice should now start correctly.

To quit X, run your window manager's exit function (assuming it has one). If it lacks such functionality, run:

```
$ pkill -15 Xorg

```

**Note:** *pkill* will kill all running X instances. To specifically kill the window manager on the current virtual terminal, run:
```
$ pkill -15 -t tty"$XDG_VTNR" Xorg

```

See also [signal(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/signal.7).

## Tips and tricks

### Override xinitrc

If you have a working `~/.xinitrc` but just want to try other window manager or desktop environment, you can run it by issuing *startx* followed by the path to the window manager, for example:

```
$ startx /usr/bin/i3

```

If the binary takes arguments, they need to be quoted to be recognized as part of the first parameter of *startx*:

```
$ startx "/usr/bin/*application* --*key value*"

```

Note that the full path is **required**. You can also specify custom options for the [#xserverrc](#xserverrc) script by appending them after the double dash `--` sign:

```
$ startx /usr/bin/enlightenment -- -br +bs -dpi 96

```

See also [startx(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/startx.1).

**Note:** Display needs to be specified (as loading `/etc/X11/xinit/xinitrc.d/` is skipped) for some operations to work (e.g. notification daemons). [[2]](https://bbs.archlinux.org/viewtopic.php?id=202812)

**Tip:** This can be used to start regular GUI programs but without any of the basic window manager features. See also [#Starting applications without a window manager](#Starting_applications_without_a_window_manager) and [Running program in separate X display](/index.php/Running_program_in_separate_X_display "Running program in separate X display").

### Autostart X at login

Make sure that *startx* is properly [configured](#Configuration).

For [Bash](/index.php/Bash "Bash"), add the following to the bottom of `~/.bash_profile`. If the file does not exist, copy a skeleton version from `/etc/skel/.bash_profile`. For [Zsh](/index.php/Zsh "Zsh"), add it to `~/.zprofile`.

```
if [[ ! $DISPLAY && $XDG_VTNR -eq 1 ]]; then
  exec startx
fi

```

You can replace the `-eq` comparison with one like `-le 3` (for vt1 to vt3) if you want to use graphical logins on more than one virtual terminal.

Alternative conditions to detect the virtual terminal include `"$(tty)" = "/dev/tty1"`, which does not allow comparison with `-le`, and `"$(fgconsole 2>/dev/null || echo -1)" -eq 1`, which does not work in [serial consoles](/index.php/Serial_console "Serial console").

If you would like to remain logged in when the X session ends, remove `exec`.

See also [Fish#Start X at login](/index.php/Fish#Start_X_at_login "Fish") and [Systemd/User#Automatic login into Xorg without display manager](/index.php/Systemd/User#Automatic_login_into_Xorg_without_display_manager "Systemd/User").

**Tip:** This method can be combined with [automatic login to virtual console](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console").

### Switching between desktop environments/window managers

If you are frequently switching between different desktop environments or window managers, it is convenient to either use a [display manager](/index.php/Display_manager "Display manager") or expand `~/.xinitrc` to make the switching possible.

The following example shows how to start a particular desktop environment or window manager with an argument:

 `~/.xinitrc` 
```
...

# Here Xfce is kept as default
session=${1:-xfce}

case $session in
    i3|i3wm           ) exec i3;;
    kde               ) exec startkde;;
    xfce|xfce4        ) exec startxfce4;;
    # No known session, try to run it as command
    *                 ) exec $1;;
esac

```

To pass the argument *session*:

```
$ xinit *session*

```

or

```
$ startx ~/.xinitrc *session*

```

### Starting applications without a window manager

It is possible to start only specific applications without a window manager, although most likely this is only useful with a single application shown in full-screen mode. For example:

 `~/.xinitrc` 
```
...

exec chromium

```

Alternatively the binary can be called directly from the command prompt as described in [#Override xinitrc](#Override_xinitrc).

With this method you need to set each application's window geometry through its own configuration files (if possible at all).

**Tip:** This can be useful to launch graphical games, where excluding the overhead of a compositor can help improve the game's performance.

See also [Display manager#Starting applications without a window manager](/index.php/Display_manager#Starting_applications_without_a_window_manager "Display manager").

### Output redirection using startx

See [Xorg#Broken redirection](/index.php/Xorg#Broken_redirection "Xorg") for details.