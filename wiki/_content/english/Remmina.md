Related articles

*   [Rdesktop](/index.php/Rdesktop "Rdesktop")
*   [xrdp](/index.php/Xrdp "Xrdp")

[Remmina](https://remmina.org/) is a remote desktop client written in GTK from the [FreeRDP](http://www.freerdp.com/) project. It supports the following protocols: SSH, VNC, RDP, NX and XDMCP.

## Installation

[Install](/index.php/Install "Install") the [remmina](https://www.archlinux.org/packages/?name=remmina) package.

For VNC support install the [libvncserver](https://www.archlinux.org/packages/?name=libvncserver) package.

If you need RDP support, also install the optional [freerdp](https://www.archlinux.org/packages/?name=freerdp) or [remmina-plugin-rdesktop](https://aur.archlinux.org/packages/remmina-plugin-rdesktop/). For these note:

*   If the RDP option is not available in the Remmina dropdown menu after installing [freerdp](https://www.archlinux.org/packages/?name=freerdp), make sure to completely quit Remmina first: run `killall remmina`. When you restart Remmina, RDP should be available.
*   As of Remmina 1.2.0, some users report RDP connections using freerdp suffer from frequent unrequested disconnections, but [rdesktop](/index.php/Rdesktop "Rdesktop") RDP connections being more reliable.
*   Password saving depends on [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring").

## Usage

To open previously saved connection profile you can do:

```
$ remmina -c ~/.remmina/file-name.remmina

```

Here is the script, which renames connection profile files basing on `name=` property to make it human readable:

```
#!/bin/bash
cd ~/.remmina
ls -1 *.remmina | while read a; do
       N=`grep '^name=' "$a" | cut -f2 -d=`;
       [ "$a" == "$N.remmina" ] || mv "$a" "$N".remmina;
done

```

To minimize to tray on startup, use `-i` option.

## See also

*   [Remmina GitLab Repository](https://gitlab.com/Remmina/Remmina)
*   [FreeRDP Wiki](https://github.com/FreeRDP/FreeRDP/wiki)