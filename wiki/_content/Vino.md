# Vino

**Vino** is a VNC (Virtual Network Computing) server allowing remote connection to your actual desktop. It is a default component of the [GNOME](/index.php/GNOME "GNOME") [Desktop environment](/index.php/Desktop_environment "Desktop environment").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 GNOME](#GNOME)
    *   [1.2 Alternative Desktop Environments](#Alternative_Desktop_Environments)
*   [2 Configuration](#Configuration)

## Installation

### GNOME

[Install](/index.php/Install "Install") the package [vino](https://www.archlinux.org/packages/?name=vino), which is available in the [official repositories](/index.php/Official_repositories "Official repositories").

You need to restart GNOME so that `vino-server` is started automatically when enabling the remote desktop feature. The remote desktop feature can usually be enabled in Settings > Sharing, however this only seems to be functional when [NetworkManager](/index.php/NetworkManager "NetworkManager") is installed and functional.

### Alternative Desktop Environments

As of version 3.9.2, Vino no longer includes a standalone preferences dialog (see [bug 700070](https://bugzilla.gnome.org/show_bug.cgi?id=700070)), thus making configuration difficult without the GNOME Control Center.

The easiest solution is to install [vino38](https://aur.archlinux.org/packages/vino38/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR"), which provides the latest version with the preferences dialog, accessible via the `vino-preferences` command.

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Vino&oldid=412207](https://wiki.archlinux.org/index.php?title=Vino&oldid=412207)"