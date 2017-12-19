Related articles

*   [Display manager](/index.php/Display_manager "Display manager")
*   [Xorg](/index.php/Xorg "Xorg")
*   [xprofile](/index.php/Xprofile "Xprofile")
*   [Xresources](/index.php/Xresources "Xresources")

The `~/.xinitrc` file is a shell script read by *xinit* and by its front-end *startx*. It is mainly used to execute [desktop environments](/index.php/Desktop_environment "Desktop environment"), [window managers](/index.php/Window_manager "Window manager") and other programs when starting the X server (e.g., starting daemons and setting environment variables). The *xinit* program starts the [X Window System](/index.php/X_Window_System "X Window System") server and works as the first client program on systems that are not using a [display manager](/index.php/Display_manager "Display manager").

One of the main functions of `~/.xinitrc` is to dictate which client for the X Window System is invoked with *startx* or *xinit* programs on a per-user basis. There exists numerous additional specifications and commands that may also be added to `~/.xinitrc` as you further customize your system.

Most display managers also source the similar [xprofile](/index.php/Xprofile "Xprofile") before xinit.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 xserverrc](#xserverrc)
    *   [2.2 xinitrc](#xinitrc)
*   [3 Usage](#Usage)
*   [4 Autostart X at login](#Autostart_X_at_login)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Override xinitrc from command line](#Override_xinitrc_from_command_line)
    *   [5.2 Switching between desktop environments/window managers](#Switching_between_desktop_environments.2Fwindow_managers)
    *   [5.3 Starting applications without a window manager](#Starting_applications_without_a_window_manager)
    *   [5.4 Output redirection using startx](#Output_redirection_using_startx)

## Installation

[Install](/index.php/Install "Install") the [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit) package, which provides both *xinit*, *startx*, and a default xinitrc configuration file.

## Configuration

### xserverrc

The `xserverrc` file is a shell script responsible for starting up the X server. Both *startx* and *xinit* execute `~/.xserverrc` if it exists, *startx* will use `/etc/X11/xinit/xserverrc` otherwise.

In order to maintain an [authenticated session](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") with `logind` and to prevent bypassing the screen locker by switching terminals, [Xorg](/index.php/Xorg "Xorg") has to be started on the same virtual terminal where the login occurred.[[1]](http://blog.falconindy.com/articles/back-to-basics-with-x-and-systemd.html) Therefore it is recommended to specify `vt$XDG_VTNR` in the `~/.xserverrc` file:

 `~/.xserverrc` 
```
#!/bin/sh

exec /usr/bin/Xorg -nolisten tcp "$@" vt$XDG_VTNR

```

Alternatively, if you wish to have the X display on a separate console from the one where the server is invoked, you can do so by using the X server wrapper provided by `/usr/lib/systemd/systemd-multi-seat-x`. For convenience, *xinit* and *startx* can be set up to use this wrapper by modifying your `~/.xserverrc`.

**Note:** To re-enable redirection of the output from X session into the Xorg log file, add the `-keeptty` option. See [Xorg#Broken redirection](/index.php/Xorg#Broken_redirection "Xorg") for details.

### xinitrc

If `.xinitrc` is present in a user's home directory, *startx* and *xinit* execute it. Otherwise *startx* will run the default `/etc/X11/xinit/xinitrc`.

**Note:** *Xinit* has its own default behaviour instead of executing the file. See [xinit(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/xinit.1) for details.

This default xinitrc will start a basic environment with [Twm](/index.php/Twm "Twm"), [xorg-xclock](https://www.archlinux.org/packages/?name=xorg-xclock) and [Xterm](/index.php/Xterm "Xterm") (assuming that the necessary packages are installed). Therefore, to start a different window manager or desktop environment, first create a copy of the default `xinitrc` in your home directory:

```
$ cp /etc/X11/xinit/xinitrc ~/.xinitrc

```

Then [edit](/index.php/Help:Reading#Append.2C_add.2C_create.2C_edit "Help:Reading") the file and replace the default programs with desired commands. Remember that lines following a command using `exec` would be ignored. For example, to start `xscreensaver` in the background and then start [openbox](/index.php/Openbox#Standalone "Openbox"), use the following:

 `~/.xinitrc` 
```
xscreensaver &
exec openbox-session
```

**Note:** At the very least, ensure that the last if block in `/etc/X11/xinit/xinitrc` is present in your `.xinitrc` file to ensure that the scripts in `/etc/X11/xinit/xinitrc.d` are sourced.

Long-running programs started before the window manager, such as a screensaver and wallpaper application, must either fork themselves or be run in the background by appending an `&` sign. Otherwise, the script would halt and wait for each program to exit before executing the window manager or desktop environment. Note that some programs should instead not be forked, to avoid race bugs, as is the case of [xrdb](/index.php/Xrdb "Xrdb"). Prepending `exec` will replace the script process with the window manager process, so that X does not exit even if this process forks to the background.

## Usage

To run Xorg as a regular user, issue:

```
$ startx

```

or

```
$ xinit -- :1

```

**Note:** *xinit* does not handle multiple displays when another X server is already started. For that you must specify the display by appending `-- :*display_number*`, where `*display_number*` is 1 or more.

Your window manager (or desktop environment) of choice should now start correctly.

To quit X, run your window manager's exit function (assuming it has one). If it lacks such functionality, run:

```
$ pkill -15 Xorg

```

**Note:** *pkill* will kill all running X instances. To specifically kill the window manager on the current virtual terminal, run:
```
$ pkill -15 -t tty"$XDG_VTNR" Xorg

```

## Autostart X at login

Make sure that *startx* is properly [configured](#Configuration).

For [Bash](/index.php/Bash "Bash"), add the following to the bottom of `~/.bash_profile`. If the file does not exist, copy a skeleton version from `/etc/skel/.bash_profile`. For [Zsh](/index.php/Zsh "Zsh"), add it to `~/.zprofile`.

```
if [ -z "$DISPLAY" ] && [ -n "$XDG_VTNR" ] && [ "$XDG_VTNR" -eq 1 ]; then
  exec startx
fi

```

You can replace the `-eq 1` comparison with one like `-le 3` (for vt1 to vt3) if you want to use graphical logins on more than one virtual terminal.

Alternative conditions to detect the virtual terminal include `"$(tty)" = "/dev/tty1"`, which does not allow comparison with `-le`, and `"$(fgconsole 2>/dev/null || echo -1)" -eq 1`, which does not work in [serial consoles](/index.php/Serial_console "Serial console").

If you would like to remain logged in when the X session ends, remove `exec`.

See also [Fish#Start X at login](/index.php/Fish#Start_X_at_login "Fish") and [Systemd/User#Automatic login into Xorg without display manager](/index.php/Systemd/User#Automatic_login_into_Xorg_without_display_manager "Systemd/User").

**Tip:** This method can be combined with [automatic login to virtual console](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console").

## Tips and tricks

### Override xinitrc from command line

If you have a working `~/.xinitrc`, but just want to try other window manager or desktop environment, you can run it by issuing *startx* followed by the path to the window manager:

```
$ startx /full/path/to/window-manager

```

If the window manager takes arguments, they need to be quoted to be recognized as part of the first parameter of *startx*:

```
$ startx "/full/path/to/window-manager --key value"

```

Note that the full path is **required**. Optionally, you can also specify custom options for [#xserverrc](#xserverrc) script by appending them after `--`, e.g.:

```
$ startx /usr/bin/enlightenment -- -br +bs -dpi 96

```

See also [startx(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/startx.1).

**Tip:** This can be used even to start a regular GUI programs but without any of the window manager features. See also [#Starting applications without a window manager](#Starting_applications_without_a_window_manager) and [Running program in separate X display](/index.php/Running_program_in_separate_X_display "Running program in separate X display").

### Switching between desktop environments/window managers

If you are frequently switching between different desktop environments or window managers, it is convenient to either use a [display manager](/index.php/Display_manager "Display manager") or expand `.xinitrc` to make the switching possible.

The following example `~/.xinitrc` shows how to start a particular desktop environment or window manager with an argument:

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

With this method you need to set each application window's geometry through its own configuration files, if possible at all.

**Tip:** This method can be useful to launch graphical games, especially on systems where excluding the memory or CPU usage of a window manager or desktop environment, and possible accessory applications, can help improve the game's execution performance.

See also [Display manager#Starting applications without a window manager](/index.php/Display_manager#Starting_applications_without_a_window_manager "Display manager").

### Output redirection using startx

See [Xorg#Broken redirection](/index.php/Xorg#Broken_redirection "Xorg") for details.