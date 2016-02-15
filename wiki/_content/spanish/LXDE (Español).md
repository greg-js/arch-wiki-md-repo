## Contents

*   [1 ¿Qué es LXDE?](#.C2.BFQu.C3.A9_es_LXDE.3F)
*   [2 ¿Por qué utilizar LXDE?](#.C2.BFPor_qu.C3.A9_utilizar_LXDE.3F)
*   [3 ¿Qué componentes contiene?](#.C2.BFQu.C3.A9_componentes_contiene.3F)
*   [4 ¿Cómo instalar LXDE?](#.C2.BFC.C3.B3mo_instalar_LXDE.3F)
    *   [4.1 Extras de LXDE en el AUR](#Extras_de_LXDE_en_el_AUR)
*   [5 Ejecutando LXDE](#Ejecutando_LXDE)
*   [6 Consejos](#Consejos)
    *   [6.1 Automontaje](#Automontaje)
    *   [6.2 PCManFM](#PCManFM)
    *   [6.3 Reemplace el gestor de ventanas](#Reemplace_el_gestor_de_ventanas)
    *   [6.4 Apagar y reiniciar desde lxde](#Apagar_y_reiniciar_desde_lxde)
    *   [6.5 Sustitución de gestores de ventanas](#Sustituci.C3.B3n_de_gestores_de_ventanas)
*   [7 Recursos externos](#Recursos_externos)

## ¿Qué es LXDE?

LXDE es el acrónimo en inglés de "Lightweight X11 Desktop Environment" (entorno de escritorio ligero para X11), y además LX puede referirse a LinuX. Lo encontrará diferente con respecto a otros entornos de escritorio, debido a las escasas dependencias de sus componentes, los cuales pueden usarse individualmente porque son independientes.

El proyecto LXDE intenta ofrecer un nuevo entorno de escritorio que sea suficientemente útil, manteniendo a la vez un uso reducido de recursos. la usabilidad, la rapidez, y la utilización de memoria son las prioridades de los desarrolladores.

## ¿Por qué utilizar LXDE?

Nosotros usamos LXDE por sus excelentes cualidades tales como:

*   **Ligero**, utiliza una razonable cantidad de memoria (una vez arrancados X11 y LXDE, el consumo total de memoria es de unos 45 MB en máquinas i386.)
*   **Rápido**, corre bien incluso en máquinas tan antiguas como las producidas en 1999 (los requerimientos de hardware de LXDE son similares a los de Windows 98)
*   **Bonito**, interfaz de usuario gtk+ 2 internacionalizada
*   **Fácil de usar**, la interfaz es sencilla, pero tiene todo lo imprescindible
*   **No depende de ningún escritorio** (¡sorpresa! todos los componentes pueden ser utilizados independiéntemente del propio LXDE)
*   **Ajustado a los estándares**, sigue las especificaciones de freedesktop.org
*   **Apropiado para máquinas antiguas** (Aunque LXDE por sí mismo no requira un mejor hardware, puede que otras aplicaciones bajo X sí lo necesiten. Por ejemplo, Firefox y OpenOffice.org 2 consumen bastante memoria. Se recomienda por tanto que se tenga al menos 128 MB de RAM.)

## ¿Qué componentes contiene?

*   **[PCManFM](http://pcmanfm.sourceforge.net/)**: Gestor de ficheros, proporciona además los iconos del escritorio
*   **[LXPanel](http://www.gnomefiles.org/app.php/LXPanel)**: Panel de escritorio rico en características
*   **[LXSession](http://www.gnomefiles.org/app.php/LXSession)**: Gestor de sesiones ajustado a los estándares con funciones de apagado, reiniciado, y suspensión vía HAL y gdm

	(Persisten algunos errores en lxsession relacionados con la gestión de sesiones.

```
_**lxsession-lite**_ es una versión de lxsession que carece de la capacidad de gestionar las sesiones. La estabilidad de lxsession-lite es mejor que la de lxsession, aunque claro está no puede grabar y recuperar sessions. Se recomienda utlizar, por tanto, _**lxsession-lite**_ hasta que se solucionen los problemas de lxsession.)

```

*   **[LXAppearance](http://www.gnomefiles.org/app.php/LXAppearance)**: LXAppearance es un seleccionador de temas GTK+ muy completo, capaz de cambiar temas GTK+ themes, temas de iconos, e incluso las fuentes tipográficas usadas por las aplicaciones
*   **[Openbox](http://icculus.org/openbox/index.php/Main_Page)**: Openbox es un gestor de ventanas ligero, conforme a los estándares y altamente configurable. (No no es desarrollado por el proyecto LXDE, pero se le utiliza como gestor de ventanas por defecto). Puede ser reemplazado por cualquier otro gestor de ventanas como icewm, fluxbox, metacity, etc.
*   **[GPicView](http://lxde.sourceforge.net/gpicview/)**: Un visualizador de imágenes sencillo, rápido y ligero que arranca al instante.
*   **[Leafpad](http://tarot.freeshell.org/leafpad/)**: Editor de texto ligero y sencillo (No está desarrollado por nosotros, pero le sugerimos que lo use como editor por defecto).
*   **[XArchiver](http://xarchiver.xfce.org/)**: Programa archivador ligero, rápido, basado en gtk+ e independiente del escritorio. (No es desarrollado por el proyecto LXDE, pero le sugerimos que lo use).
*   **[LXNM](http://lxde.sourceforge.net/about.html)** (en desarrollo aún): Gestor de red ligero para LXDE con capacidad de conexión sin hilos (sólo para Linux)

## ¿Cómo instalar LXDE?

LXDE es modular. Puede used escoger cualquiera de los paquetes anteriormente listados, todos ellos instalables mediante Pacman. Tiene que habilitar los repositorios [extra] y [community]. Para instalar algunos paquetes tales como LXAppearance o LXNM, deberá habilitar el repositorio del [AUR].

Sin embargo, los paquetes imprescindibles y que tiene siempre que instalar para poder ejecutar LXDE son Lxde-common, Lxsession, y Openbox. Como se dijo antes, el paquete Openbox puede ser reemplazado por otro gestor de ventanas de su preferencia.

LXDE tiene también un grupo de paquetes para Arch. Por ejemplo, puede instalar LXDE así:

```
# pacman -S lxde

```

### Extras de LXDE en el AUR

*   [lxterminal](https://www.archlinux.org/packages/?name=lxterminal)
*   [lxtask](https://www.archlinux.org/packages/?name=lxtask)

## Ejecutando LXDE

1.  Si está utilizando algún gestor de visualización tal como GDM o KDM, debería ser capaz de seleccionar directamente LXDE a través de ellos.
2.  Si no tiene un gestor de visualizacion, y quiere arrancar lxde desde la consola, añada esta línea al final del fichero ~/.xinitrc:

```
exec startlxde

```

## Consejos

### Automontaje

Si quiere que [PCManFM](http://pcmanfm.sourceforge.net/) monte automáticamnte sus dispositivos usb de almacenamiento, tiene que instalar [HAL](/index.php/HAL "HAL"). Y, si su dispositivo tiene un sistema de fichero NTFS, deberá instalar también [NTFS-3G](/index.php/NTFS_Write_Support "NTFS Write Support").

Por lo general, PCManFM funciona correctamente con [HAL](/index.php/HAL "HAL"), excepto cuando en un sistema de ficheros NTFS tenga ficheros o carpetas cuyos nombres contengan caracteres no latinos (p.ej.; caractere chinos). Este tipo de ficheros o carpetas pueden desaparecer cuando abra (o monte automáticamente) el volumen NTFS. Esto sucede porque la utilidad mounthelper de lxsession (o de lxsession-lite) no analiza correctamente las normas o la opción de localización. Hay una forma de solucionar esto:

1) Elimine el enlace simbólico "/sbin/mount.ntfs-3g".

```
rm /sbin/mount.ntfs-3g

```

2) Cree un nuevo "/sbin/mount.ntfs-3g", que será un guión bash conteniéndo:

```
#!/bin/bash
/bin/ntfs-3g $1 $2 -o utf8

```

3) Hágalo ejecutable:

```
chmod +x /sbin/mount.ntfs-3g 

```

4) Añada "NoUpgrade=sbin/sbin/mount.ntfs-3g" ao pacman.conf en la sección "[options]"

### PCManFM

Si desea tener acceso a la Papelera, montar volúmenes, y la carpeta / archivo de seguimiento que querrá apoyo gvfs:

```
pacman -S polkit-gnome gvfs

```

polkit-gnome proporciona una autenticación y será necesario que se inicie automáticamente:

```
mkdir -p ~/.config/autostart
cp /etc/xdg/autostart/polkit-gnome-authentication-agent-1.desktop ~/.config/autostart

```

Si tiene problemas para que inicio automáticamente elimine la linea:

```
OnlyShowIn=GNOME;XFCE;

```

[PCManFM @ LXDE wiki](http://wiki.lxde.org/en/PCManFM_build_and_setup_guide#Setup_Runtime_Environment_Correctly)

### Reemplace el gestor de ventanas

El gestor de ventanas de LXDE puede ser reemplazado fácilmente por cualquiera otro que usted prefiera, tal como fvwm, icewm, dwm, awesome, etc.

El gestor de ventanas que quiera utilizar está especificado en este archivo:

	/etc/xdg/lxsession/LXDE/default

Por ejemplo su /etc/xdg/lxsession/LXDE/default podría parecerse a esto:

```
smproxy
openbox
lxpanel

```

smproxy es un programa incluido en xorg. Proporciona capacidad de gestionar la sesión para aquellos programas que no trabajan bien con el protocolo de gestión de sesión de X11 R6. Por tanto, se recomienda encarecidamente que incluya esta línea en su escritorio.

openbox es el gestor de ventanas actual, reemplácelo por el que prefiera usted.

### Apagar y reiniciar desde lxde

Para ser capaz de apagar, reiniciar, suspender, etc. desde lxde asegúrese de que tanto DBus como HAL se estén ejecutando. Añada entonces su usuario al grupo power.

```
# gpasswd -a USER power

```

### Sustitución de gestores de ventanas

Openbox, el gestor de ventanas por defecto de LXDE, pueden ser reemplazados fácilmente por otros gestores de ventanas como fvwm, icewm, DWM, metacity, compiz ... etc

LXDE intentará usar gestor de ventanas desde el archivo de configuración de usuario lxsession /.config/lxsession/LXDE/desktop.conf. Si no existe, entonces se intenta utilizar el archivo de configuración global /etc/xdg/lxsession/LXDE/desktop.conf.

Reemplace el comando openbox-lxde con el gestor de ventanas de su elección:

 `~/.config/lxsession/LXDE/desktop.conf` 

```
[Session]
window_manager=openbox-lxde
```

Por metacity:

 `~/.config/lxsession/LXDE/desktop.conf` 

```
[Session]
window_manager=metacity
```

Por compiz:

 `~/.config/lxsession/LXDE/desktop.conf` 

```
[Session]
window_manager=compiz ccp --indirect-rendering
```

## Recursos externos

*   [Proyecto LXDE](http://lxde.sourceforge.net)
*   [Los paquetes más recientes de LX...](https://sourceforge.net/project/showfiles.php?group_id=180858)
*   [Gestor de ficheros PCMan](https://sourceforge.net/project/showfiles.php?group_id=156956)