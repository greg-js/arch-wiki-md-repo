**Estado de la traducción**
Este artículo es una traducción de [xprofile](/index.php/Xprofile "Xprofile"), revisada por última vez el **2018-11-11**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Xprofile&diff=0&oldid=540305) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)")

Un archivo xprofile, `~/.xprofile` y `/etc/xprofile`, le permite ejecutar comandos al inicio de la sesión de X user - antes de que se inicie el [gestor de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") .

El archivo xprofile es similar en estilo a [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)").

## Compatibilidad

Los archivos xprofile son cargados de manera nativa por los siguientes gestores de pantalla:

*   [GDM](/index.php/GDM_(Espa%C3%B1ol) "GDM (Español)") - `/etc/gdm/Xsession`
*   [LightDM](/index.php/LightDM_(Espa%C3%B1ol) "LightDM (Español)") - `/etc/lightdm/Xsession`
*   [LXDM](/index.php/LXDM "LXDM") - `/etc/lxdm/Xsession`
*   [SDDM](/index.php/SDDM "SDDM") - `/usr/share/sddm/scripts/Xsession`

### Cargar xprofile desde una sesión iniciada con xinit

Es posible cargar xprofile desde una sesión iniciada con uno de los siguientes programas:

*   `startx`
*   `xinit`
*   [XDM](/index.php/XDM "XDM")
*   Cualquier otro [gesto de pantalla](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)") que utilize `~/.xsession` o `~/.xinitrc`

Todos estos ejecutan, directa o indirectamente, `~/.xinitrc` o `/etc/X11/xinit/xinitrc` si no existe. Es por eso que xprofile tiene que ser cargado desde estos archivos.

 `~/.xinitrc and /etc/X11/xinit/xinitrc` 
```
#!/bin/sh

# Asegúrese de que esto se encuentra antes del comando 'exec' o no se cargará.
[ -f /etc/xprofile ] && . /etc/xprofile
[ -f ~/.xprofile ] && . ~/.xprofile

...

```

## Configuración

En primer lugar, cree el archivo `~/.xprofile` si aún no existe. Luego, simplemente agregue los comandos para los programas que desea que se inicien con la sesión. Véase abajo:

 `~/.xprofile` 
```
tint2 &
nm-applet &

```