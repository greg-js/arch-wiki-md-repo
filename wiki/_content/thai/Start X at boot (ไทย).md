This article explains how to have the [X server](/index.php/X_server "X server") start automatically right after logging in at a virtual terminal. This is achieved by running the _startx_ command, whose behaviour can be customized as described in the [xinitrc](/index.php/Xinitrc "Xinitrc") article, for example for choosing what [window manager](/index.php/Window_manager "Window manager") to launch. Alternatively, a [display manager](/index.php/Display_manager "Display manager") can be used to start X automatically and provide a graphical login screen.

## Shell profile files

**Note:** These solutions run X on the same tty used to login, which is required in order to maintain the login session.

For [Bash](/index.php/Bash "Bash"), add the following to the bottom of `~/.bash_profile`. If the file does not exist, copy a skeleton version from `/etc/skel/.bash_profile`. For [Zsh](/index.php/Zsh "Zsh"), add it to `~/.zlogin` (or `~/.zprofile`) instead.

```
[[ -z $DISPLAY && $XDG_VTNR -eq 1 ]] && exec startx

```

**Note:**

*   You can replace the `-eq 1` comparison with one like `-le 3` (for vt1 to vt3) if you want to use graphical logins on more than one VT.
*   X must always be run on the same tty where the login occurred, to preserve the logind session. This is handled by the default `/etc/X11/xinit/xserverrc`.
*   `xinit` may be faster than `startx`, but needs additional parameter such as `-nolisten tcp`.

For [Fish](/index.php/Fish "Fish"), add the following to the bottom of your `~/.config/fish/config.fish`.

```
# start X at login
if status --is-login
    if test -z "$DISPLAY" -a $XDG_VTNR = 1
        exec startx
    end
end

```

## Tips and tricks

*   This method can be combined with [automatic login to virtual console](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console"). When doing this you have to set correct dependencies for the autologin systemd service to ensure that dbus is started before `~/.xinitrc` is read and hence pulseaudio started (see: [BBS#155416](https://bbs.archlinux.org/viewtopic.php?id=155416))
*   If you would like to remain logged in when the X session ends, remove `exec`.
*   To redirect the output of the X session to a file, create an [alias](/index.php/Alias "Alias"):

	 `alias startx='startx &> ~/.xlog'` 

**Note:** Redirecting stderr (`startx &>`) breaks rootless startup, see [Xorg#Rootless Xorg (v1.16)](/index.php/Xorg#Rootless_Xorg_.28v1.16.29 "Xorg").

## See also

[Start X after automatic login](http://unix.stackexchange.com/questions/62722/start-x-after-automatic-login)