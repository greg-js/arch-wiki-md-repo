**Estado de la traducción**
Este artículo es una traducción de [Remmina](/index.php/Remmina "Remmina"), revisada por última vez el **2019-02-15**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Remmina&diff=0&oldid=566597) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Rdesktop](/index.php/Rdesktop "Rdesktop")
*   [xrdp](/index.php/Xrdp "Xrdp")

[Remmina](http://www.remmina.org/wp/) es un cliente de escritorio remoto escrito en GTK+ del proyecto [freerdp](http://www.freerdp.com/). Es compatible con los protocolos SSH, VNC, RDP, NX y XDMCP.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [remmina](https://www.archlinux.org/packages/?name=remmina).

Para tener soporte de VNC instale el paquete [libvncserver](https://www.archlinux.org/packages/?name=libvncserver).

Si necesita soporte RDP, instale también de manera opcional [freerdp](https://www.archlinux.org/packages/?name=freerdp) o [remmina-plugin-rdesktop](https://aur.archlinux.org/packages/remmina-plugin-rdesktop/). Para estos nb'0ote:

*   Si la opción RDP no está disponible en el menú desplegable de Remmina después de instalar [freerdp](https://www.archlinux.org/packages/?name=freerdp), asegúrese de salir de Remmina primero: ejecute `killall remmina`. Cuando reinicie Remmina, RDP debería estar disponible.
*   A partir de Remmina 1.2.0, algunos usuarios han informado que las conexiones RDP que utilizan freerdp sufren frecuentes desconexiones no solicitadas, pero que las conexiones RDP de rdesktop son más estables.
*   El almacenamiento de la contraseña depende de [GNOME Keyring](/index.php/GNOME/Keyring_(Espa%C3%B1ol) "GNOME/Keyring (Español)")

## Utilización

Para abrir el perfil de conexión previamente guardado, puede hacerlo así:

```
$ remmina -c ~/.remmina/file-name.remmina

```

Aquí está el script, que cambia el nombre de los archivos de perfil de conexión basándose en la propiedad `name=` para que sea legible por una persona:

```
#!/bin/bash
cd ~/.remmina
ls -1 *.remmina | while read a; do
       N=`grep '^name=' "$a" | cut -f2 -d=`;
       [ "$a" == "$N.remmina" ] || mv "$a" "$N".remmina;
done

```

Para minimizar la bandeja en el inicio, utilice la opción `-i`.

## Véase también

*   [Bugtracker](https://gitlab.com/Remmina/Remmina/issues) - para la aplicación
*   [Wiki del proyecto](https://github.com/FreeRDP/FreeRDP/wiki) - con amplios recursos