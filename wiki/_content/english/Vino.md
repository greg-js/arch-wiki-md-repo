[Vino](https://wiki.gnome.org/Projects/Vino) is a VNC (Virtual Network Computing) server allowing remote connection to your actual desktop. It is a default component of the [GNOME](/index.php/GNOME "GNOME") desktop environment.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 GNOME](#GNOME)
    *   [1.2 Alternative Desktop Environments](#Alternative_Desktop_Environments)
*   [2 Configuration](#Configuration)
*   [3 Running on a headless server](#Running_on_a_headless_server)
*   [4 See also](#See_also)

## Installation

### GNOME

[Install](/index.php/Install "Install") the [vino](https://www.archlinux.org/packages/?name=vino) package.

You need to restart GNOME so that `vino-server` is started automatically when enabling the remote desktop feature. The remote desktop feature can usually be enabled in Settings > Sharing, however this only seems to be functional when [NetworkManager](/index.php/NetworkManager "NetworkManager") is installed and functional.

### Alternative Desktop Environments

As of version 3.9.2, Vino no longer includes a standalone preferences dialog (see [bug 700070](https://bugzilla.gnome.org/show_bug.cgi?id=700070)), thus making configuration difficult without the GNOME Control Center.

The easiest solution is to install the package [vino38](https://aur.archlinux.org/packages/vino38/), which provides the latest version with the preferences dialog, accessible via the `vino-preferences` command.

## Configuration

You can configure vino via gnome-control-center.

Now you can connect remotely to your desktop via a VNC viewer like TightVNC or Remmina. Remember to forward port 5900 if you are behind a NAT device and to allow the connection through iptables.

If you are having problems regarding security and encryption you could try:

```
$ gsettings set org.gnome.Vino require-encryption false

```

If you use a standalone [window manager](/index.php/Window_manager "Window manager") like [Openbox](/index.php/Openbox "Openbox") and it does not work, you can start `vino-server` manually or add the command to the window manager's autostart script

```
# /usr/lib/vino/vino-server &

```

## Running on a headless server

Vino can be used to manage a headless server with a graphical desktop via VNC. For this, a graphics driver like [xf86-video-dummy](https://www.archlinux.org/packages/?name=xf86-video-dummy) must be installed and [configured](/index.php/Xorg#Configuration "Xorg"). [xpra’s sample xorg.conf](http://xpra.org/xorg.conf) for the Xdummy driver can be used as a base. Then, the server can be configured to [start X at boot](/index.php/Start_X_at_boot "Start X at boot") for the user account that should be usable remotely. Vino must be made to [autostart with the desktop environment](/index.php/Autostarting#On_desktop_environment_startup "Autostarting") by creating a desktop entry in the user’s home directory such as this one:

 `~/.config/autostart/vino-server.desktop` 
```
[Desktop Entry]
Type=Application
Name=Vino VNC server
Exec=/usr/lib/vino/vino-server
NoDisplay=true
```

Next, make Vino accept VNC connections without asking for confirmation by running the following command as the graphical desktop user:

```
$ dbus-launch gsettings set org.gnome.Vino prompt-enabled false

```

You may wish to revoke suspend and hibernate permissions using [Polkit](/index.php/Polkit "Polkit").

For the [GNOME](/index.php/GNOME "GNOME") desktop environment, the following are some further options you may want for GNOME:

```
$ dbus-launch gsettings set org.gnome.desktop.lockdown disable-user-switching true
$ dbus-launch gsettings set org.gnome.desktop.lockdown disable-log-out true
$ dbus-launch gsettings set org.gnome.desktop.interface enable-animations false

```

Remember to configure your [firewall](/index.php/Firewall "Firewall") to not block the `rfb` port used for VNC. For secure authentication – which should be used when giving access to privileged users on the open internet –, you should tunnel the VNC protocol through e.g. [SSH](/index.php/SSH "SSH") or [stunnel](https://www.archlinux.org/packages/?name=stunnel) instead of unblocking the `rfb` port. When using stunnel, you should require a [password](/index.php/Security#Passwords "Security"):

```
$ dbus-launch gsettings set org.gnome.Vino authentication-methods "['vnc']"
$ dbus-launch gsettings set org.gnome.Vino vnc-password $(echo -n "mypassword"|base64)

```

You can now log in to your server with a VNC client such as [vinagre](https://www.archlinux.org/packages/?name=vinagre).

The above setup can also be used with multiple remote users logging in automatically, e.g. by using multiple copies of [xlogin-git](https://aur.archlinux.org/packages/xlogin-git/)’s service files in `/etc/systemd/system/`, each modified to log in a different user on a different X11 display and virtual terminal. With Vino, each user’s VNC server can be configured to listen on a different port as well:

```
$ dbus-launch gsettings set org.gnome.Vino alternative-port 5910
$ dbus-launch gsettings set org.gnome.Vino use-alternative-port true

```

## See also

*   [Vino design document](http://people.gnome.org/~markmc/remote-desktop.html)