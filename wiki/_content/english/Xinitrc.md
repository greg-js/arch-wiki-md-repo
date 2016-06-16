The `~/.xinitrc` file is a shell script read by *xinit* and by its front-end *startx*. It is mainly used to execute [desktop environments](/index.php/Desktop_environment "Desktop environment"), [window managers](/index.php/Window_manager "Window manager") and other programs when starting the X server (e.g., starting daemons and setting environment variables). The *xinit* program starts the [X Window System](/index.php/X_Window_System "X Window System") server and works as first client program on systems that are not using a [display manager](/index.php/Display_manager "Display manager").

One of the main functions of `~/.xinitrc` is to dictate which client for the X Window System is invoked with *startx* or *xinit* programs on a per-user basis. There exists numerous additional specifications and commands that may also be added to `~/.xinitrc` as you further customize your system.

Most DMs also source the similar [xprofile](/index.php/Xprofile "Xprofile") before xinit.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 xserverrc](#xserverrc)
    *   [2.2 xinitrc](#xinitrc)
*   [3 Running](#Running)
*   [4 Autostart X at login](#Autostart_X_at_login)
    *   [4.1 Automatic login to the virtual console](#Automatic_login_to_the_virtual_console)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Override xinitrc from command line](#Override_xinitrc_from_command_line)
    *   [5.2 Making a DE/WM choice](#Making_a_DE.2FWM_choice)
    *   [5.3 Starting applications without a window manager](#Starting_applications_without_a_window_manager)

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

### xinitrc

If `.xinitrc` is present in a user's home directory, *startx* and *xinit* execute it. Otherwise *startx* will run the default `/etc/X11/xinit/xinitrc`.

**Note:** *Xinit* has its own default behaviour instead of executing the file. See `man 1 xinit` for details.

This default xinitrc will start a basic environment with [Twm](/index.php/Twm "Twm"), [xorg-xclock](https://www.archlinux.org/packages/?name=xorg-xclock) and [Xterm](/index.php/Xterm "Xterm") (assuming that the necessary packages are installed). Therefore, to start a different window manager or desktop environment, first create a copy of the default `xinitrc` in home directory:

```
$ cp /etc/X11/xinit/xinitrc ~/.xinitrc

```

The reason of doing this (instead of creating one from scratch) is to preserve some desired default behaviour in the original file, such as sourcing shell scripts from `/etc/X11/xinit/xinitrc.d`. Scripts in this directory without `.sh` extension are not sourced.

Append desired commands and *remove/comment the conflicting lines*. Remember, lines following `exec` would be ignored. For example, to start [openbox](/index.php/Openbox#Standalone "Openbox"):

 `~/.xinitrc` 
```
...

if [ -d /etc/X11/xinit/xinitrc.d ] ; then
    for f in /etc/X11/xinit/xinitrc.d/**?*.sh** ; do
        [ -x "$f" ] && . "$f"
    done
    unset f
fi

# twm &
# xclock -geometry 50x50-1+1 &
# xterm -geometry 80x50+494+51 &
# xterm -geometry 80x20+494-0 &
# exec xterm -geometry 80x66+0+0 -name login

## some applications that should be run in the background
xscreensaver **&**
xsetroot -cursor_name left_ptr **&**

**exec** openbox-session

```

**Note:** At the very least, ensure that the *if block* in the example above is present in your `.xinitrc` file to ensure that the scripts in `/etc/X11/xinit/xinitrc.d` are sourced.

Long-running programs started before the window manager, such as a screensaver and wallpaper application, must either fork themselves or be run in the background by appending an `&` sign. Otherwise, the script would halt and wait for each program to exit before executing the window manager or desktop environment. Note that some programs should instead not be forked, to avoid race bugs, as is the case of [xrdb](/index.php/Xrdb "Xrdb"). Prepending `exec` will replace the script process with the window manager process, so that X does not exit even if this process forks to the background.

## Running

To now run Xorg as a regular user, issue:

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

**Note:** *pkill* will kill all running X instances. To specifically kill the window manager on the current virtual terminal, use:
```
WM_PID=$(xprop -id $(xprop -root _NET_SUPPORTING_WM_CHECK \
| awk -F'#' '{ print $2 }') _NET_WM_PID \
| awk -F' = ' '{ print $2 }')

kill -15 $WM_PID
```

The program `xprop` is provided by the package [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) in the [official repositories](/index.php/Official_repositories "Official repositories").

## Autostart X at login

Make sure that *startx* is properly [configured](#Configuration).

For [Bash](/index.php/Bash "Bash"), add the following to the bottom of `~/.bash_profile`. If the file does not exist, copy a skeleton version from `/etc/skel/.bash_profile`. For [Zsh](/index.php/Zsh "Zsh"), add it to `~/.zprofile`.

```
[[ -z $DISPLAY && $XDG_VTNR -eq 1 ]] && exec startx

```

**Note:**

*   You can replace the `-eq 1` comparison with one like `-le 3` (for vt1 to vt3) if you want to use graphical logins on more than one virtual terminal.
*   If you would like to remain logged in when the X session ends, remove `exec`.

See also [Fish#Start X at login](/index.php/Fish#Start_X_at_login "Fish") and [Systemd/User#Automatic login into Xorg without display manager](/index.php/Systemd/User#Automatic_login_into_Xorg_without_display_manager "Systemd/User").

### Automatic login to the virtual console

This method can be combined with [automatic login to virtual console](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console").

## Tips and tricks

### Override xinitrc from command line

If you have a working `~/.xinitrc`, but just want to try other WM/DE, you can run it by issuing *startx* followed by the path to the window manager:

```
$ startx /full/path/to/window-manager

```

If the window manager takes arguments, they need to be enquoted to be recognized as part of the first parameter of *startx*:

```
$ startx "/full/path/to/window-manager --key value"

```

Note that the full path is **required**. Optionally, you can also specify custom options for [#xserverrc](#xserverrc) script by appending them after `--`, e.g.:

```
$ startx /usr/bin/enlightenment -- -br +bs -dpi 96

```

See also `man startx`.

**Tip:** This can be used even to start a regular GUI programs but without any of the window manager features. See also [#Starting applications without a window manager](#Starting_applications_without_a_window_manager) and [Running program in separate X display](/index.php/Running_program_in_separate_X_display "Running program in separate X display").

### Making a DE/WM choice

If you are frequently switching between different DEs/WMs, it is recommended to either use a [Display manager](/index.php/Display_manager "Display manager") or add code to `.xinitrc`. The code described next consists of a simple few lines, which will take the argument and load the desired desktop environment or window manager.

The following example `~/.xinitrc` shows how to start a particular DE/WM with an argument:

 `~/.xinitrc` 
```
...

# Here Xfce is kept as default
session=${1:-xfce}

case $session in
    awesome           ) exec awesome;;
    bspwm             ) exec bspwm;;
    catwm             ) exec catwm;;
    cinnamon          ) exec cinnamon-session;;
    dwm               ) exec dwm;;
    enlightenment     ) exec enlightenment_start;;
    ede               ) exec startede;;
    fluxbox           ) exec startfluxbox;;
    gnome             ) exec gnome-session;;
    gnome-classic     ) exec gnome-session --session=gnome-classic;;
    i3|i3wm           ) exec i3;;
    icewm             ) exec icewm-session;;
    jwm               ) exec jwm;;
    kde               ) exec startkde;;
    mate              ) exec mate-session;;
    monster|monsterwm ) exec monsterwm;;
    notion            ) exec notion;;
    openbox           ) exec openbox-session;;
    unity             ) exec unity;;
    xfce|xfce4        ) exec startxfce4;;
    xmonad            ) exec xmonad;;
    # No known session, try to run it as command
    *) exec $1;;
esac

```

After that, you can easily start a particular DE/WM by passing an argument, e.g.:

```
$ xinit
$ xinit gnome
$ xinit kde
$ xinit wmaker

```

or

```
$ startx
$ startx ~/.xinitrc gnome
$ startx ~/.xinitrc kde
$ startx ~/.xinitrc wmaker

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