**Estado de la traducción**
Este artículo es una traducción de [General purpose mouse](/index.php/General_purpose_mouse "General purpose mouse"), revisada por última vez el **2019-02-07**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=General_purpose_mouse&diff=0&oldid=565868) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

GPM, abreviatura de General Purpose Mouse, es un daemon que proporciona soporte de ratón para las consolas virtuales Linux.

## Instalación

**Advertencia:** El paquete [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) ya no se actualiza de forma activa. Si es posible, utilize [libinput](/index.php/Libinput_(Espa%C3%B1ol) "Libinput (Español)").

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [gpm](https://www.archlinux.org/packages/?name=gpm). Es posible que también necesite instalar [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) para la compatibilidad con el panel táctil en un ordenador portátil.

## Configuración

El parámetro `-m` precede a la declaración del ratón que se va a utilizar. El parámetro `-t` precede al tipo de ratón. Para obtener una lista de los tipos disponibles para la opción `-t`, ejecute `gpm` con `-t help`.

```
# gpm -m /dev/input/mice -t help

```

El paquete [gpm](https://www.archlinux.org/packages/?name=gpm) debe iniciarse con algunos parámetros. Estos parámetros se pueden registrar [creando](/index.php/Help:Reading_(Espa%C3%B1ol)#Adjuntar,_añadir,_crear,_editar "Help:Reading (Español)") el archivo `/etc/conf.d/gpm`, o ser usados cuando se ejecuta *gpm* directamente. A partir de 2016, el archivo `gpm.service` para [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") incluye los parámetros para un ratón USB.

 `/usr/lib/systemd/system/gpm.service`  `ExecStart=/usr/bin/gpm -m /dev/input/mice -t imps2` 

Obviamente, debe editarse, preferiblemente de [manera amigable con systemd](/index.php/Systemd_(Espa%C3%B1ol)#Modificar_los_archivos_de_unidad_suministrados "Systemd (Español)"), si existe otro tipo de ratón, y si se utiliza el servicio.

*   Para ratones PS/2, los parámetros son:

```
-m /dev/psaux -t ps2

```

*   Y los IBM Trackpoints necesitan:

```
-m /dev/input/mice -t ps2

```

**Nota:** Si el ratón tiene solo 2 botones, pase `-2` a `GPM_ARGS` y el segundo botón realizará la función de pegado.

Una vez que se haya encontrado una configuración adecuada, [inicie](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") y [active](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") `gpm.service`.

Para obtener más información, véase [gpm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpm.8).

## Véase también

*   [Gentoo:GPM](https://wiki.gentoo.org/wiki/GPM "gentoo:GPM")