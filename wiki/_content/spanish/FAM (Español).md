## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Configuración](#Configuraci.C3.B3n)
*   [4 Otros recursos](#Otros_recursos)

## Introducción

File Alteration Monitor (FAM) es un demonio usado por entornos de escritorio como [GNOME](/index.php/GNOME "GNOME") y [Xfce](/index.php/Xfce "Xfce") para monitoreo y reporte de cambios en el sistema de archivos. FAM también es usado por el servidor Samba. KDE ya no utiliza FAM, han migrado al sistema *inotify* del kernel, el cual no requiere ninguna configuración.

[Gamin](/index.php/Gamin "Gamin") es una reimplementación de las FAM. Es mas nuevo y su mantenimiento es mas activo que el de FAM, también es mas facíl de configurar.

## Instalación

Normalmente FAM es instalado como una dependencia de otro paquete. Puede ser directamente instalado con:

```
pacman -S fam

```

## Configuración

Se puede inicial FAM manualmente con:

```
/etc/rc.d/fam start

```

Para iniciar FAM al arrancar, agrega *fam* en la línea DAEMONS en [rc.conf](/index.php/Rc.conf "Rc.conf"). Sí utilizas [NetworkManager](/index.php/NetworkManager "NetworkManager") *fam* debe estar **después** de *networkmanager*

## Otros recursos

[FAM](http://en.wikipedia.org/wiki/File_alteration_monitor)

[FAM, Gamin and inotify](http://www.noah.org/wiki/FAM,_Gamin,_inotify)