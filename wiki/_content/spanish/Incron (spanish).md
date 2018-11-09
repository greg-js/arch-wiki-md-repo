**Estado de la traducción**
Este artículo es una traducción de [Incron](/index.php/Incron "Incron"), revisada por última vez el **2018-11-08**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Incron&diff=0&oldid=552688) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[incron](http://inotify.aiken.cz/?section=incron&page=about&lang=en) es un demonio que supervisa los eventos del sistema de archivos y ejecuta los comandos definidos en las tablas del usuario y del sistema.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Activación e inicio automático](#Activaci.C3.B3n_e_inicio_autom.C3.A1tico)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Usar incrontab](#Usar_incrontab)
    *   [3.2 Formato Incrontab](#Formato_Incrontab)
        *   [3.2.1 Tipos de máscara](#Tipos_de_m.C3.A1scara)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [incron](https://www.archlinux.org/packages/?name=incron).

## Activación e inicio automático

Después de la instalación, el demonio no se habilitará por defecto. Se puede habilitar utilizando [systemctl](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)").

## Configuración

Incrontabs nunca debe ser editado directamente; en su lugar, los usuarios deben usar el programa `incrontab` para trabajar con sus incrontabs.

### Usar incrontab

Para ver sus incrontabs, los usuarios deben ejecutar el comando:

```
 $ incrontab -l

```

Para editar sus incrontabs, deben usar:

```
 $ incrontab -e

```

Para eliminar sus incrontabs, pueden usar:

```
 $ incrontab -r

```

Para recargar *incrond*, use:

```
 $ incrontab -d

```

Para editar otro usuario incrontab, ejecute el siguiente comando como root:

```
 $ incrontab -u *usuario*

```

### Formato Incrontab

Cada fila en un archivo incrotab es una tabla que ejecuta el dameon cuando ocurre un evento en un determinado directorio o archivo.

El formato básico para un incrontab es:

```
 *ruta* *máscara* *comando*

```

*   *ruta* es el directorio o archivo donde *incrond* monitoreará los cambios.
*   *máscara* es el tipo de evento de sistema de archivos que incrond monitoreará. Este parámetro puede ser separado por comas.
*   *comando* es el comando que se ejecutará después de que ocurran los eventos del sistema de archivos especificados.

#### Tipos de máscara

Incrontab usa tipos de máscara para especificar qué evento del sistema de archivos monitorear. Para más opciones véase [inotify(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/inotify.7)

Para activar un comando si se accede a un archivo o se lee:

```
**IN_ACCESS**

```

Para activar un comando si los metadatos de un archivo cambian (por ejemplo, *timestamps* , *permissons* ):

```
**IN_ATTRIB**

```

Para activar un comando si se cierra un archivo abierto para escritura:

```
**IN_CLOSE_WRITE**

```

Para activar un comando si se cierra un archivo o directorio no abierto para escritura:

```
**IN_CLOSE_NOWRITE**

```

Para activar un comando si se crea un archivo o directorio en un directorio vigilado:

```
**IN_CREATE**

```

Para activar un comando si un archivo o directorio se elimina de un directorio visto:

```
**IN_DELETE**

```

Para activar un comando si un archivo o directorio visto se elimina (o se mueve a un sistema de archivos diferente):

```
**IN_DELETE_SELF**

```

Para activar un comando si un archivo fue modificado:

```
**IN_MODIFY**

```

Para activar un comando si un archivo o directorio visto se mueve dentro del sistema de archivos:

```
**IN_MOVE_SELF**

```

Para activar un comando si un archivo o directorio se mueve fuera del directorio visto:

```
**IN_MOVED_FROM**

```

Para activar un comando si un archivo o directorio se mueve al directorio visto:

```
**IN_MOVED_TO**

```

Para activar un comando si se abre un archivo o directorio visto:

```
**IN_OPEN**

```