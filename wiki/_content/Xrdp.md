# Xrdp

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**xrdp** is a daemon that supports Microsoft's [Remote Desktop Protocol](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol "wikipedia:Remote Desktop Protocol") (RDP). It uses Xvnc or X11rdp as a backend.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Fixing Problems in xrdp<sup>AUR</sup>](#Fixing_Problems_in_xrdpAUR)
    *   [1.2 Autoboot at Startup](#Autoboot_at_Startup)
    *   [1.3 Running with Vino (Gnome VNC-Server for root session)](#Running_with_Vino_.28Gnome_VNC-Server_for_root_session.29)
*   [2 Usage](#Usage)
*   [3 See also](#See_also)

## Installation

Users can find install xrdp from the AUR : [xrdp](https://aur.archlinux.org/packages/xrdp/)<sup><small>AUR</small></sup>.

### Fixing Problems in [xrdp](https://aur.archlinux.org/packages/xrdp/)<sup><small>AUR</small></sup>

You won't have these problems when you use [xrdp-git](https://aur.archlinux.org/packages/xrdp-git/)<sup><small>AUR</small></sup> so you can skip this section when you chose the git version.

If Xvnc (tightvnc) fails with

```
Fatal server error:
could not open default font 'fixed'
```

you must create a symlink at `/usr/X11R6/lib/X11/fonts` pointing to `/usr/share/fonts`.

_xrdp_ will just fail without giving you that error. You can only see the error message when you try to start Xvnc manually for a test.

To fix the message `Couldn't open RGB_DB '/usr/X11R6/lib/X11/rgb'` copy `/usr/share/X11/rgb.txt` to `/usr/X11R6/lib/X11/rgb.txt` or create a symlink. If this file is missing, standard X11 colors are wrong (pink or blue instead of black) and Xterm is broken.

### Autoboot at Startup

The aur xrdp package contains service files for systemd. Enable xrdp.service :

```
# systemctl enable xrdp.service

```

Enable xrdp-sesman.service :

```
# systemctl enable xrdp-sesman.service

```

### Running with Vino (Gnome VNC-Server for root session)

Enable the server to be seen via vino-preferences. Since vino defaults to port : 5900 for connections, we will edit the xrdp configuration file to understand this. Append the the vino session to xrdp's configuration file (/etc/xrdp/xrdp.ini) with the following code :

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

After starting xrdp you can point any RDP client to localhost (on standard RDP port 3389) _xrdp_ will give a small message window.

When you choose _sessman-Xvnc_ you can give a username and password for any account on your host and _xrdp_ will start another _Xvnc_ instance for you. Opening a window manager out of a _SESSION_ list provided in `/etc/xrdp/startwm.sh`.

When you just close the session window and RDP connection, you can access the same session again next time you connect with RDP. When you exit the window manager or desktop environment from the session window, the session will close and a new session will be opened the next time.

_xrdp_ checks only if a session with the same geometry is already opened. It will start a new session if the geometry/resolution doesn't match.

## See also

*   [TigerVNC](/index.php/TigerVNC "TigerVNC") - VNC, an alternative to RDP, also used as backend here

Retrieved from "[https://wiki.archlinux.org/index.php?title=Xrdp&oldid=399611](https://wiki.archlinux.org/index.php?title=Xrdp&oldid=399611)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Remote desktop](/index.php/Category:Remote_desktop "Category:Remote desktop")