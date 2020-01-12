The [systemd](https://www.archlinux.org/packages/?name=systemd) package is built not to kill user process on log out by default, see [Systemd/User#Kill user processes on logout](/index.php/Systemd/User#Kill_user_processes_on_logout "Systemd/User").

There are several ways to make a program continue after logoff:

*   use the [nohup(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nohup.1) GNU coreutil
*   use the `disown` [Bash](/index.php/Bash "Bash")/[Zsh](/index.php/Zsh "Zsh") shell builtin
*   use a [terminal multiplexer](/index.php/Terminal_multiplexer "Terminal multiplexer"), also allowing you to reattach to your detached session.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 X applications](#X_applications)
    *   [1.1 Secondary X server](#Secondary_X_server)
    *   [1.2 xpra](#xpra)
    *   [1.3 X2Go](#X2Go)

## X applications

As [xmove](https://en.wikipedia.org/wiki/xmove "wikipedia:xmove") is dead, you probably want to use something else.

### Secondary X server

With your favourite editor make a script with this content, use [chmod](/index.php/Chmod "Chmod") to make it executable (`chmod a+x scriptname.sh`).

```
#!/bin/sh

if [ $# -eq 0 ] ; then # check to see if arguments are given (color depth)
    a=24        # default color depth
else
    a=$1        # use given argument
fi

if [ $a -ne 8 -a $a -ne 16 -a $a -ne 24 ] ; then
    echo "Invalid color depth. Use 8, 16, or 24."
    exit 1
fi

for display in 0 1 2 3 4 5 ; do
    if [ ! -f "/tmp/.X$display-lock" ] ; then
        exec startx -- :$display -depth $a -quiet
        exit 0
    fi
done

echo "No displays available."
exit 1
```

executing this little script will start a new X server. Then you can simply start your application and lock the server with `xlock -mode blank` (you need the [xlockmore](https://www.archlinux.org/packages/?name=xlockmore) package for using [xlock(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xlock.1).)

Do not start your application in the first X server. If it is not already started, start the first and start a second one. Use the second one for your applications.

This is important because some features, like AGP mode, works only on one X server and other users of the computer will be annoyed if those feature will be lacking because you started a X server for your own purposes. So just use the second, the first will be full featured for everyone who need.

### xpra

[Xpra](/index.php/Xpra "Xpra") allows you to start X programs and leave them running after disconnecting to reconnect again at a later time. It is possible to start X programs on a remote machine, connect to the machine over ssh, disconnect and reconnect again while the programs continue running.

### X2Go

[X2Go](/index.php/X2Go "X2Go") supports suspending of sessions and reconnecting even from different client. While designed for remote access, it can be used even on localhost.