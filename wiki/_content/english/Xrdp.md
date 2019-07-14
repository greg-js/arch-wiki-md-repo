**xrdp** is a daemon that supports Microsoft's [Remote Desktop Protocol](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol "wikipedia:Remote Desktop Protocol") (RDP). It uses Xvnc, X11rdp or xorgxrdp as a backend.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Autoboot at startup](#Autoboot_at_startup)
    *   [1.2 Running as Terminal Server (Xorg)](#Running_as_Terminal_Server_(Xorg))
        *   [1.2.1 Troubleshooting](#Troubleshooting)
    *   [1.3 Running with Vino (Gnome VNC-Server for root session)](#Running_with_Vino_(Gnome_VNC-Server_for_root_session))
*   [2 Usage](#Usage)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [xrdp](https://aur.archlinux.org/packages/xrdp/) package (or alternatively [xrdp-git](https://aur.archlinux.org/packages/xrdp-git/) for the development version).

### Autoboot at startup

The [xrdp](https://aur.archlinux.org/packages/xrdp/) package contains service files for systemd. [Enable](/index.php/Enable "Enable") `xrdp.service` and `xrdp-sesman.service`.

### Running as Terminal Server (Xorg)

[Install](/index.php/Install "Install") the [xorgxrdp-git](https://aur.archlinux.org/packages/xorgxrdp-git/) package.

Add `allowed_users=anybody` to `/etc/X11/Xwrapper.config` to allow anybody to start X

Edit `~/.xinitrc` or `/etc/X11/xinit/xinitrc` to launch your DE.

#### Troubleshooting

If you encounter black box around mouse pointer create `~/.Xresources-xrdp` with line `Xcursor.core:1` and load it in `~/.xinitrc` like

```
xrdb ~/.Xresources-xrdp
exec startlxde

```

You may need to install [xorg-xrdb](https://www.archlinux.org/packages/?name=xorg-xrdb).

### Running with Vino (Gnome VNC-Server for root session)

Enable the server to be seen via vino-preferences. Since vino defaults to port : 5900 for connections, we will edit the xrdp configuration file to understand this. Append the vino session to xrdp's configuration file (/etc/xrdp/xrdp.ini) with the following code :

```
# echo "
[xrdp8]
name=Vino-Session
lib=libvnc.so
username=ask
password=ask
ip=127.0.0.1
port=5900
" >> "/etc/xrdp/xrdp.ini"

```

Remember to restart the xrdp server, and one should be able to connect to the vino session (tested using xfreerdp).

## Usage

After starting xrdp you can point any RDP client to localhost (on standard RDP port 3389) *xrdp* will give a small message window.

When you choose *sessman-Xvnc* you can give a username and password for any account on your host and *xrdp* will start another *Xvnc* instance for you. Opening a window manager out of a *SESSION* list provided in `/etc/xrdp/startwm.sh`.

When you just close the session window and RDP connection, you can access the same session again next time you connect with RDP. When you exit the window manager or desktop environment from the session window, the session will close and a new session will be opened the next time.

*xrdp* checks only if a session with the same geometry is already opened. It will start a new session if the geometry/resolution doesn't match.

## See also

*   [TigerVNC](/index.php/TigerVNC "TigerVNC") - VNC, an alternative to RDP, also used as backend here
*   [freerdp](https://www.archlinux.org/packages/?name=freerdp) a rdesktop fork that supports RDP 7.1 features including network level authentication (NLA). See also [[1]](http://askubuntu.com/a/97932/217269).