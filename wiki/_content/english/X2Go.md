[X2Go](http://wiki.x2go.org) enables to access a graphical desktop of a computer over the network. The protocol is tunneled through the [Secure Shell](/index.php/Secure_Shell "Secure Shell") protocol, so it is encrypted.

**Note:** X2Go is not compatible with all desktop environments. You can check [X2Go desktop environment compatibility](http://wiki.x2go.org/doku.php/doc:de-compat) first, especially if you want to shadow your current desktop.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Server side](#Server_side)
    *   [2.1 Configure Secure Shell daemon](#Configure_Secure_Shell_daemon)
    *   [2.2 Check fuse kernel module is loaded](#Check_fuse_kernel_module_is_loaded)
    *   [2.3 Setup SQLite database](#Setup_SQLite_database)
    *   [2.4 Control published applications](#Control_published_applications)
    *   [2.5 Start X2Go server daemon](#Start_X2Go_server_daemon)
*   [3 Client side](#Client_side)
    *   [3.1 Access the local desktop](#Access_the_local_desktop)
    *   [3.2 Exchange data between client and server (desktop)](#Exchange_data_between_client_and_server_(desktop))
    *   [3.3 Leave a session temporarily](#Leave_a_session_temporarily)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 The desktop environment does not start](#The_desktop_environment_does_not_start)
        *   [4.1.1 Local session prevents X2Go new session](#Local_session_prevents_X2Go_new_session)
        *   [4.1.2 Path issue](#Path_issue)
    *   [4.2 No selection screen in x2goclient](#No_selection_screen_in_x2goclient)
    *   [4.3 Sessions do not logoff correctly](#Sessions_do_not_logoff_correctly)
    *   [4.4 Notification area disappeared](#Notification_area_disappeared)
    *   [4.5 Shared folders do not mount (Windows Clients)](#Shared_folders_do_not_mount_(Windows_Clients))
    *   [4.6 Workaround for failing compositing window manager for remote session](#Workaround_for_failing_compositing_window_manager_for_remote_session)
    *   [4.7 /bin/bash: No such file or directory when connect (or what ever shell you use)](#/bin/bash:_No_such_file_or_directory_when_connect_(or_what_ever_shell_you_use))
*   [5 See also](#See_also)

## Installation

Two parts are available in [official repositories](/index.php/Official_repositories "Official repositories"). They can be [installed](/index.php/Pacman "Pacman") with the following packages:

*   [x2goserver](https://www.archlinux.org/packages/?name=x2goserver) - X2Go server
*   [x2goclient](https://www.archlinux.org/packages/?name=x2goclient) - X2Go client based on Qt5

## Server side

### Configure Secure Shell daemon

X2Go uses [Secure Shell](/index.php/Secure_Shell "Secure Shell") in order to work, so you need to configure sshd daemon to allow X11 forwarding. Follow the instructions at [OpenSSH#X11 forwarding](/index.php/OpenSSH#X11_forwarding "OpenSSH") and [OpenSSH#Daemon management](/index.php/OpenSSH#Daemon_management "OpenSSH").

### Check fuse kernel module is loaded

In order for the server to be able to access files on the client computer, the fuse module is needed. One can check that `lsmod | grep fuse` returns a match, otherwise load the `fuse` [kernel module](/index.php/Kernel_module "Kernel module").

### Setup SQLite database

Run the following command on the server to initialize the SQLite database (which is required in order for the x2go server to work):

```
# x2godbadmin --createdb

```

### Control published applications

X2Go can publish the installed applications in a menu to the client. This is controlled by the files in `/etc/x2go/applications/`. This location however is not created by default and can be created by creating a symlink to `/usr/share/applications/`. Alternatively instead of creating a symlink one could also create a folder and link only the desired applications instead.

See [[1]](https://wiki.x2go.org/doku.php/wiki:advanced:published-applications) for more information.

### Start X2Go server daemon

Now all you need to do is [start](/index.php/Start "Start") the system `x2goserver.service`.

## Client side

Run *X2Go Client* on the client computer, the one that wants to access the server:

```
$ x2goclient

```

For the list of available options, see [x2goclient(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/x2goclient.1).

**Note:** Make sure the client computer can open a SSH session to the server by checking from the client that `ssh *username@host*` is successful.

You can now create several sessions, which then appear on the right side and can be selected by a mouse click. Each entry consists of your username, hostname, IP, and port for SSH connection. Furthermore you can define several speed profiles (coming from modem up to LAN) and the desktop environment you want to start remotely.

### Access the local desktop

To access the local desktop, the one currently running on the server rather than a new one, one can choose the option "Connection to local desktop" in "session type" in the *X2Go Client* as long as the users match, if it is user *foo* accessing the session of user *foo*.

However to access the local desktop of a different user, one needs to install [x2godesktopsharing](https://aur.archlinux.org/packages/x2godesktopsharing/) and launch `x2godesktopsharing`.

### Exchange data between client and server (desktop)

On the X2Go client (e.g. laptop) local directories could be shared. The server will use [fuse](/index.php/Fuse "Fuse") and [SSHFS](/index.php/SSHFS "SSHFS") to access this directory and mount it to a subdirectory media of your home directory on the server. This enables you to have access to laptop data on your server or to exchange files. It is also possible to mount these shares automatically at each session start.

### Leave a session temporarily

Another special feature of X2Go is the possibility of suspending a session. This means you can leave a session on one client and reopen it even from another client at the same point. This can be used to to start a session in the LAN and to reopen it later on a laptop. The session data are stored and administered in a [SQLite](/index.php/SQLite "SQLite") database on the server in the meanwhile. The state of the sessions is protocolled by a process named *x2gocleansessions*.

## Troubleshooting

### The desktop environment does not start

#### Local session prevents X2Go new session

It happens that when a desktop session already runs locally and X2Go tries to start a new one, it fails. This is typically an issue related to *D-Bus*, see [[2]](https://bugzilla.redhat.com/show_bug.cgi?id=1350004) for details.

If *D-Bus* fails to start, try using a *Custom desktop* command instead of the default session type. For the command, use the desktop starter as an option of `dbus-launch`, for example `dbus-launch startxfce4`. This is a way to launch a session bus instance, set the appropriate environment variables so that the new session can find the bus.

#### Path issue

It may be that the desktop environment's executable, *startkde*, *startgnome* or *startxfce4* is not in the `$PATH` when logging in using SSH. In this case, do not simply choose the defaults of KDE, Gnome or XFCE but use the full paths to the executable, for example `/usr/bin/startxfce4`. You can also start [openbox](/index.php/Openbox "Openbox") or another window manager. You should be asked for your server's password and user name, now and after login you will see the X2Go logo for a short time, and the desktop.

### No selection screen in x2goclient

A regression in [iproute2](https://www.archlinux.org/packages/?name=iproute2) causes *ss* to show no result when specifying the `-u` flag, as done in `/usr/bin/x2golistdesktops`. [[3]](https://marc.info/?l=linux-netdev&m=143018447007958&w=2)

See [[4]](http://bugs.x2go.org/cgi-bin/bugreport.cgi?bug=799), [[5]](https://bbs.archlinux.org/viewtopic.php?pid=1541035) for more information.

### Sessions do not logoff correctly

Due to [this bug](http://bugs.x2go.org/cgi-bin/bugreport.cgi?bug=914) the X2Go sessions might not logoff correctly. The script that initiates the session spits out many log lines that might confuse X2go. A simple workarround is to create a custom session script and redirect the log output either to a file or to `/dev/null` and then point your X2Go-client to this custom script.

Here is a sample script for an XFCE session:

```
 #!/bin/sh
 #
 #xfce4-session spits out quite a bit of text during logout, which I guess
 #confuses x2go so we would get a black screen and session hang.
 #adding redirect to a logfile like "~/logfile" or "/dev/null" nicely solved it
 # see [http://bugs.x2go.org/cgi-bin/bugreport.cgi?bug=914](http://bugs.x2go.org/cgi-bin/bugreport.cgi?bug=914)
 /usr/bin/xfce4-session > /dev/null

```

### Notification area disappeared

If you log in, but the notification area is missing, you can use exactly the same fix as for [#Local session prevents X2Go new session](#Local_session_prevents_X2Go_new_session).

### Shared folders do not mount (Windows Clients)

The ssh-daemon used by the X2go windows client uses depreceated ssh-dss keys by default and because Arch does not accept them your shared folders will not mount. Check out this [bug report](http://bugs.x2go.org/cgi-bin/bugreport.cgi?bug=1009) for more information.

This can be solved on the windows side by generating different type of key:

```
 C:\Program Files (x86)\x2goclient\ssh-keygen -b 2048 -t rsa

```

And simply replace `c:\Users\User\.x2go\etc\ssh_host_dsa_key` and `c:\Users\User\.x2go\etc\ssh_host_dsa_key.pub` with the newly generated key files.

Other workarrounds from [[6]](http://bugs.x2go.org/cgi-bin/bugreport.cgi?bug=1009) might help, too.

### Workaround for failing compositing window manager for remote session

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

### /bin/bash: No such file or directory when connect (or what ever shell you use)

In you ssh configuration, if you chroot a user, this user need to have his own /bin directory inside his chrooted directory. If not, you will not be able to connect.

## See also

*   [Screenshot KDE-Session](http://wiki.archlinux.de/?title=Bild:X2go-1.png)
*   [Screenshot configuration dialog](http://wiki.archlinux.de/?title=Bild:X2go-2.png)