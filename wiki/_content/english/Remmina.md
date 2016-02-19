Remmina is a remote desktop client written in GTK+. It supports the following protocols:

*   SSH
*   VNC
*   RDP
*   NX
*   SFTP
*   XDMCP

## Installation

Install the [remmina](https://www.archlinux.org/packages/?name=remmina) package. If you want RDP support, also install [freerdp](https://www.archlinux.org/packages/?name=freerdp).

**Note:** If the RDP option is not available in the Remmina dropdown menu after installing [freerdp](https://www.archlinux.org/packages/?name=freerdp), make sure to completely quit Remmina first: run `killall remmina`. When you restart Remmina, RDP should be available.

## Using from command line

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