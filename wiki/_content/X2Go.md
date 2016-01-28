# X2Go

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[X2Go](http://wiki.x2go.org) enables you to access a graphical desktop of a computer over the network. The transmission is done using the [Secure Shell](/index.php/Secure_Shell "Secure Shell") protocol, so it is encrypted.

**Note:** X2Go isn't compatible with all desktop environments. You can check [X2Go desktop environment compatibility](http://wiki.x2go.org/doku.php/doc:de-compat) first, especially if you want to shadow your current desktop.

## Contents

*   [1 Installation](#Installation)
*   [2 Server configuration](#Server_configuration)
    *   [2.1 Configure Secure Shell daemon](#Configure_Secure_Shell_daemon)
    *   [2.2 Load fuse kernel module](#Load_fuse_kernel_module)
    *   [2.3 Setup SQLite database](#Setup_SQLite_database)
    *   [2.4 Start X2Go server daemon](#Start_X2Go_server_daemon)
*   [3 Desktop Shadowing](#Desktop_Shadowing)
*   [4 Client configuration](#Client_configuration)
*   [5 Various](#Various)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Authentication error](#Authentication_error)
    *   [6.2 No selection screen in x2goclient](#No_selection_screen_in_x2goclient)
*   [7 Links](#Links)

## Installation

Two parts are available in [official repositories](/index.php/Official_repositories "Official repositories"). They can be [installed](/index.php/Pacman "Pacman") with the following packages:

*   [x2goserver](https://www.archlinux.org/packages/?name=x2goserver) - X2Go server
*   [x2goclient](https://www.archlinux.org/packages/?name=x2goclient) - X2Go client based on Qt4

## Server configuration

### Configure Secure Shell daemon

X2Go uses [Secure Shell](/index.php/Secure_Shell "Secure Shell") in order to work, so you need to configure sshd daemon to allow X11 forwarding and then start it first. Follow the instructions at [Secure Shell#X11 forwarding](/index.php/Secure_Shell#X11_forwarding "Secure Shell") and [Secure Shell#Managing the sshd daemon](/index.php/Secure_Shell#Managing_the_sshd_daemon "Secure Shell").

If you are using other than POSIX (C) locale, you may want to add the following line to [configuration file](/index.php/Secure_Shell#Daemon "Secure Shell")

```
# Allow client to pass locale environment variables
AcceptEnv LANG LC_*

```

### Load fuse kernel module

In order for the server to be able to access files on the client computer you should load a `fuse` [kernel module](/index.php/Kernel_module "Kernel module").

### Setup SQLite database

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** What is it used for? Why do we need it? (Discuss in [Talk:X2Go#](https://wiki.archlinux.org/index.php/Talk:X2Go))

Run the following command to initialize SQLite database

```
# x2godbadmin --createdb

```

### Start X2Go server daemon

Now all you need to do is [start](/index.php/Start "Start") `x2goserver.service`.

## Desktop Shadowing

To gain access to the "local desktop" (as opposed to a unique session/desktop environment) you need to install [x2godesktopsharing](https://aur.archlinux.org/packages/x2godesktopsharing/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR"). Then, launch `x2godesktopsharing`.

Note, you do not need x2godesktopsharing to access "local desktop" of user "foo" by user "foo". x2godesktopsharing is for accessing "foo"'s desktop by "foo2" user. Just choose "Connection to local desktop" in "session type" in x2goclient.

## Client configuration

Make sure you can open a ssh-session from the client to the server

```
ssh username@host

```

Then run X2Go client itself

```
x2goclient

```

You can now create several sessions, which then appear on the right side and can be selected by a mouse click. Each entry consists of your username, hostname, IP, and port for SSH-connection. Furthermore you can define several speed profiles (coming from modem up to LAN) and the desktop environment you want to start remotely.

**Common mistakes:** Do not simply choose the defaults of KDE or Gnome, since the executables startkde or startgnome are usually not in the PATH when logging in using ssh. Use full paths to startkde or startgnome. You can also start openbox or another window manager.

You should be asked for your password for your user at the server now and after login you will see the X2Go logo for a short time, and -- voila -- the desktop.

**Exchange data between client and server(desktop)** On the x2goclient (e.g. laptop) local directories could be shared. The server will use fuse and sshfs to access this directory and mount it to a subdirectory media of your home directory on the server. This enables you to have access to laptop data on your server or to exchange files. It is also possible to mount these shares automatically at each session start.

**To leave a session temporarily** Another special feature of X2Go is the possibility of suspending a session. This means you can leave a session on one client and reopen it even from another client at the same point. This can be used to to start a session in the LAN and to reopen it later on a laptop. The session data are stored and administered in a postgres database on the server in the meanwhile. The state of the sessions is protocolled by a process named x2gocleansessions.

## Various

**Workaround for failing compositing window manager for remote session**

This is useful for situations, when the computer running x2goserver is used also for local sessions with e.g. compiz as the window manager. For remote connections with x2goclient, compiz fails to load and metacity should be used instead. The following is for GNOME, but could be modified for other desktop environments. (Getting compiz ready is not part of this how-to.)

Create /usr/local/share/applications/gnome-wm-test.desktop:

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=gnome-wm-test
Exec=/usr/local/bin/gnome-wm-test.sh
NoDisplay=true

```

Create script /usr/local/bin/gnome-wm-test.sh:

```
#!/bin/sh
# Script for choosing compiz when possible, otherwise metacity
# Proper way to use this script is to set the key to mk-gnome-wm
# /desktop/gnome/session/required_components/windowmanager
xdpyinfo 2> /dev/null | grep -q "^ *Composite$" 2> /dev/null
IS_X_COMPOSITED=$?
if [ $IS_X_COMPOSITED -eq 0 ] ; then
    gtk-window-decorator &
    WM="compiz ccp --indirect-rendering --sm-client-id $DESKTOP_AUTOSTART_ID"
else
    WM="metacity --sm-client-id=$DESKTOP_AUTOSTART_ID"
fi
exec bash -c "$WM"

```

Modify the following gconf key to start the session with gnome-wm-test window manager:

```
$ gconftool-2 --type string --set /desktop/gnome/session/required_components/windowmanager "gnome-wm-test"

```

## Troubleshooting

### Authentication error

If the following error appears:

```
Authentification Failed:
The host key for this server was not found but an othertype of key exists.
An Attacker might change the default server key to confuse  
your client into thinking the key does not exist

```

Delete the servers entry from `~/.ssh/known_hosts` file and retry to authenticate.

### No selection screen in x2goclient

A regression in [iproute2](https://www.archlinux.org/packages/?name=iproute2) causes _ss_ to show no result when specifying the `-u` flag, as done in `/usr/bin/x2golistdesktops`. [[1]](https://marc.info/?l=linux-netdev&m=143018447007958&w=2)

See [[2]](http://bugs.x2go.org/cgi-bin/bugreport.cgi?bug=799), [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1541035) for more information.

## Links

*   [Screenshot KDE-Session](http://wiki.archlinux.de/?title=Bild:X2go-1.png)
*   [Screenshot configuration dialog](http://wiki.archlinux.de/?title=Bild:X2go-2.png)
*   [Project page](http://x2go.org)

Retrieved from "[https://wiki.archlinux.org/index.php?title=X2Go&oldid=391799](https://wiki.archlinux.org/index.php?title=X2Go&oldid=391799)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Remote desktop](/index.php/Category:Remote_desktop "Category:Remote desktop")

Hidden category:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")