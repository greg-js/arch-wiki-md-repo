## ~/.bash_profile

A login manager-ek helyettesítésére kitűnő alternatíva az, hogy a következőt a `~/.bash_profile` végére fűzöd (ha a `~/.bash_profile` nincs jelen a rendszereden, innen bemásolhatod magadnak: `/etc/skel/.bash_profile`):

 `~/.bash_profile` 
```
if [[ -z "$DISPLAY" ]] && [[ $(tty) = /dev/tty1 ]]; then
  . startx
  logout
fi

```

vagy (ez némi ellenőrzést is futtat):

 `~/.bash_profile` 
```
if [[ -z "$DISPLAY" ]] && [[ ! -a "/tmp/.X11-unix/X0" ]] && [[ "`whoami`" != "root" ]]; then
  . startx
  logout
fi

```

vagy:

 `~/.bash_profile` 
```
if [[ -z "$DISPLAY" ]] && [[ $(tty) = /dev/tty1 ]]; then
  exec xinit -- /usr/bin/X -nolisten tcp
  logout
fi

```

Ezzel a módszerrel, az X automatikusan indul, amikor a parancshéjba lépsz. Továbbá kiléphetsz belőle, ha az X-et a `Ctrl+Alt+Backspace` billentyűkombinációval állítod meg. Ha pedig a [mingetty technique](/index.php/Automatic_login_to_virtual_console#Using_mingetty "Automatic login to virtual console")módszert használod belépésre, vedd ki a fenti beállításokból a "logout" parancsot.

Lásd még: [https://bbs.archlinux.org/viewtopic.php?id=6182](https://bbs.archlinux.org/viewtopic.php?id=6182)