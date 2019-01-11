This page intends to allow remote sessions using "X Display Manager Control Protocol" (XDMCP). See the GDM documention for more information on the parameters: [https://help.gnome.org/admin/gdm/3.6/configuration.html.en#xdmcpsection](https://help.gnome.org/admin/gdm/3.6/configuration.html.en#xdmcpsection).

## Contents

*   [1 Setup Graphical Logins](#Setup_Graphical_Logins)
    *   [1.1 XDM](#XDM)
    *   [1.2 GDM](#GDM)
    *   [1.3 KDM](#KDM)
    *   [1.4 LightDM](#LightDM)
    *   [1.5 SLiM](#SLiM)
*   [2 Accessing X from a remote Machine on your LAN](#Accessing_X_from_a_remote_Machine_on_your_LAN)
*   [3 Thin client setup](#Thin_client_setup)
    *   [3.1 Example GUI-based Clients](#Example_GUI-based_Clients)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Session declined: Maximum Number of Sessions Reached](#Session_declined:_Maximum_Number_of_Sessions_Reached)
    *   [4.2 Login screen and GNOME is somehow flickering](#Login_screen_and_GNOME_is_somehow_flickering)

## Setup Graphical Logins

### XDM

Modify `/etc/X11/xdm/xdm-config` and comment out:

```
DisplayManager.requestPort:    0

```

So it will be:

```
!DisplayManager.requestPort:    0

```

Then modify `/etc/X11/xdm/Xaccess` to allow any host to get a login window. Look for a line that looks like this:

```
*             #any host can get a login window

```

and remove the hash '#' sign at the beginning of the line.

In case you have multiple network interfaces also add a line like this:

```
LISTEN 192.168.0.10

```

Where 192.168.0.10 should be you server IP address.

Then reboot or restart your X server and xdm daemon.

### GDM

Modify `/etc/gdm/custom.conf` to include:

```
[xdmcp]
Enable=true
Port=177

```

Then restart the Gnome Display Manager:

```
systemctl restart gdm

```

Or if using the inittab method, login as root on another tty and

```
telinit 3
telinit 5 && exit 

```

### KDM

Support for this feature seems to be very buggy. Lightdm is probably an easier choice.

Edit kdmrc ( `/opt/kde/share/config/kdm/kdmrc` [KDE 3x] or `/usr/share/config/kdm/kdmrc` (KDE 4x] ) and at the end there should be something like this:

```
[Xdmcp]
Enable=true

```

Then you need to restart your X server so the change you just made takes effect:

```
systemctl restart kdm

```

### LightDM

Modify `/etc/lightdm/lightdm.conf`

Enable the XDMCP Server:

```
[XDMCPServer]
enabled=true
port=177

```

On a headless system, disable the automatic start of one seat so that LightDM can run in the background:

```
[LightDM]
start-default-seat=false

```

Then restart the LightDM:

```
systemctl restart lightdm

```

### SLiM

SLiM doesn't support Xdmcp.

## Accessing X from a remote Machine on your LAN

You can access your login manager on the network computer 192.168.0.10 via the following command. TCP and UDP streams are opened. So it is not possible to access the login manager via an SSH connection.

```
Xnest -query 192.168.0.10 -geometry 1280x1024 :1

```

Or, with Xephyr, if you experience refreshing problems with Xnest:

```
Xephyr -query 192.168.0.10 -screen 1280x1024 -br -reset -terminate :1

```

Or, if you are on runlevel 3

```
X -query your_server_ip

```

Xserver should recognize your monitor and set appropriate resolution.

**Note:** You can enable XDMCP Direct/Query and Broadcast connections from remote hosts without XDM starting a local X server.

After allowing XDMCP access as described above, edit `/etc/X11/xdm/Xservers` and comment out:

```
#:0 local /usr/bin/X :0

```

Then launch XDM as root, e.g. `xdm -config /etc/X11/xdm/archlinux/xdm-config`

## Thin client setup

First of all one should setup dhcp and tftp server. [Dnsmasq](/index.php/Dnsmasq "Dnsmasq") has both of them. For network boot image check [thinstation](http://www.thinstation.org/) project. If your network card does not support PXE, you can try [Etherboot](http://etherboot.org/wiki/)

### Example GUI-based Clients

*   community/remmina
*   Xming for Windows

## Troubleshooting

### Session declined: Maximum Number of Sessions Reached

Edit `/etc/gdm/custom.conf` and add/increase the maximum sessions.

```
[xdmcp]
Enable=true
**MaxSessions=2**

```

### Login screen and GNOME is somehow flickering

If the login screen is created again and again and unresponsive, you are trying to access GNOME Shell on the remote machine. This is apparently caused by network speed, e.g. by accessing via wireless connections. The workaround is to disable/deinstall GNOME Shell.

```
 pacman -R gnome-shell

```