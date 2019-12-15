**Estado de la traducción**
Este artículo es una traducción de [Mirrors](/index.php/Mirrors "Mirrors"), revisada por última vez el **2019-11-13**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Mirrors&diff=0&oldid=587446) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Unofficial mirrors (Español)](/index.php/Unofficial_mirrors_(Espa%C3%B1ol) "Unofficial mirrors (Español)")
*   [pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")

Esta página es una guía para seleccionar y configurar los servidores de réplicas, y obtener un listado de los servidores de réplicas disponibles actuales.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Servidores de réplicas oficiales](#Servidores_de_réplicas_oficiales)
    *   [1.1 Servidores de réplicas preparados para IPv6](#Servidores_de_réplicas_preparados_para_IPv6)
*   [2 Activar un servidor de réplica específico](#Activar_un_servidor_de_réplica_específico)
    *   [2.1 Forzar a pacman a actualizar las listas de paquetes](#Forzar_a_pacman_a_actualizar_las_listas_de_paquetes)
*   [3 Ordenar los servidores de réplicas](#Ordenar_los_servidores_de_réplicas)
    *   [3.1 Lista por velocidad](#Lista_por_velocidad)
        *   [3.1.1 Clasificación de una lista servidores de réplicas existente](#Clasificación_de_una_lista_servidores_de_réplicas_existente)
        *   [3.1.2 Obtener y ordenar una lista de servidores de réplicas funcionales](#Obtener_y_ordenar_una_lista_de_servidores_de_réplicas_funcionales)
    *   [3.2 Clasificación del lado del servidor](#Clasificación_del_lado_del_servidor)
*   [4 Solución de problemas](#Solución_de_problemas)
*   [5 Véase también](#Véase_también)

## Servidores de réplicas oficiales

La lista servidores de réplicas oficial de Arch Linux está disponible en el paquete [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist). Para obtener una lista aún más actualizada de servidores de réplicas, utilice la página [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) en el sitio principal.

Verifique el estado de los servidores de réplicas de Arch visitando la página [Mirror Status](https://www.archlinux.org/mirrors/status/). Se recomienda usar solo servidores de réplicas que estén actualizados, es decir, que estén sincronizados.

Si desea que su servidor de réplica se añada a la lista oficial, consulte [DeveloperWiki:NewMirrors](/index.php/DeveloperWiki:NewMirrors "DeveloperWiki:NewMirrors"). Mientras tanto, agréguelo al artículo [Unofficial mirrors](/index.php/Unofficial_mirrors "Unofficial mirrors").

### Servidores de réplicas preparados para IPv6

El [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/?ip_version=6) también se puede utilizar para encontrar una lista de los servidores de réplicas IPv6 actuales.

## Activar un servidor de réplica específico

Para activar los servidores de réplicas, edite `/etc/pacman.d/mirrorlist` y localice su región geográfica. Descomente los servidores de réplicas que le gustaría usar.

Ejemplo:

```
# Any
# Server = http://mirrors.kernel.org/archlinux/$repo/os/$arch
**Server = https://mirrors.kernel.org/archlinux/$repo/os/$arch**

```

Consulte [#Ordenar los servidores de réplicas](#Ordenar_los_servidores_de_réplicas) para conocer herramientas que ayudan a elegir servidores de réplicas.

**Sugerencia:**

*   Descomente 5 servidores de réplicas favoritos y colóquelos en la parte superior del archivo mirrorlist. De esa manera, es fácil encontrarlos y moverlos si el primer servidor de réplica de la lista tiene problemas. También facilita la fusión de las actualizaciones de mirrorlist.
*   Los servidores de réplicas HTTP son más rápidos que los FTP debido a [persistent HTTP connection](https://en.wikipedia.org/wiki/HTTP_persistent_connection "wikipedia:HTTP persistent connection"): con FTP, se debe establecer una nueva conexión al servidor cada vez que *pacman* solicita que se descargue un paquete, lo que resulta en una breve pausa.

También es posible especificar servidores de réplicas en `/etc/pacman.conf`. Para el repositorio *[core]*, la configuración predeterminada sería:

```
[core]
Include = /etc/pacman.d/mirrorlist

```

Para usar el servidor de réplica *HostEurope* como servidor predeterminado, agréguelo antes de la línea `Include`:

```
[core]
**Server = http://ftp.hosteurope.de/mirror/ftp.archlinux.org/core/os/$arch**
Include = /etc/pacman.d/mirrorlist

```

pacman ahora intentará conectarse a este servidor de réplica primero. Proceda a hacer lo mismo para *[testing]*, *[extra]* y *[community]*, si procede.

**Nota:** si los servidores de réplicas se han establecido directamente en `pacman.conf`, recuerde usar el mismo servidor de réplica para todos los repositorios. De lo contrario, se pueden instalar paquetes que sean incompatibles entre sí, como Linux de *[core]* y un módulo del kernel antiguo de *[extra]*.

### Forzar a pacman a actualizar las listas de paquetes

Los servidores de réplicas pueden no estar sincronizados y la lista de paquetes del servidor antiguo puede no corresponder con la lista de paquetes del servidor nuevo, aunque las fechas de las listas puedan sugerir que sí lo están.

Después de crear/editar `/etc/pacman.d/mirrorlist`, emita la siguiente orden:

```
# pacman -Syyu

```

Pasar dos indicadores `--refresh`/`-y` obliga a pacman a actualizar todas las listas de paquetes, incluso si se consideran actualizadas. Emitir `pacman -Syyu` es un desperdicio innecesario de ancho de banda en la mayoría de los casos, pero a veces puede solucionar problemas al cambiar de un servidor de réplica roto a otro que funcione. Vea también [Is -Syy safe?](https://bbs.archlinux.org/viewtopic.php?id=163124).

**Advertencia:** en la mayoría de los casos, si fuerza la actualización de la base de datos de pacman, querrá forzar la degradación de los paquetes potencialmente demasiado nuevos para que correspondan a las versiones ofrecidas por el nuevo servidor de réplica. Esto evita problemas en los que los paquetes se actualizan de forma inconsistente, lo que lleva a una actualización parcial.
```
# pacman -Syyuu

```

Esto no es necesario cuando se usan marcas de tiempo para garantizar que los servidores de réplicas solo se actualicen.

## Ordenar los servidores de réplicas

Al descargar paquetes, pacman usa los servidores de réplicas en el orden en que se enumeran en `/etc/pacman.d/mirrorlist`. El orden de los servidores que aparecen en la lista establece su prioridad.

No es óptimo clasificar los servidores de réplicas basándose solo en la velocidad, ya que los servidores más rápidos pueden estar desincronizados. En su lugar, haga una lista de servidores de réplicas ordenados por su [velocidad](#Lista_por_velocidad), y luego elimine aquellos de la lista que no estén sincronizados de acuerdo con su [estado](https://www.archlinux.org/mirrors/status/).

Se recomienda repetir este proceso antes de cada actualización del sistema para mantener actualizada la lista de servidores de réplicas.

### Lista por velocidad

#### Clasificación de una lista servidores de réplicas existente

El paquete [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib) proporciona un script de Bash, `/usr/bin/rankmirrors`, que se puede utilizar para clasificar los servidores de réplicas según su conexión y velocidades de apertura para aprovechar el uso del servidor de réplica local más rápido.

Haga una copia de seguridad del archivo `/etc/pacman.d/mirrorlist` existente:

```
# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup

```

Para preparar `mirrorlist.backup` para clasificarlo con *rankmirrors*, se pueden realizar las siguientes acciones:

*   Edite `mirrorlist.backup` y descomente los servidores que se probarán.

*   Si los servidores en el archivo están agrupados por país, se pueden extraer todos los servidores de un país específico utilizando: `$ awk '/^## *Nombre del país*$/{f=1; next}f==0{next}/^$/{exit}{print substr($0, 1); f=0}' /etc/pacman.d/mirrorlist.backup` 

*   Para descomentar cada servidor de réplica, ejecute la siguiente línea con `sed`: `# sed -i 's/^#Server/Server/' /etc/pacman.d/mirrorlist.backup` 

Por último, clasifique los servidores de réplicas, aquí con el operando `-n 6` para generar solo los 6 servidores de réplicas más rápidos:

```
# rankmirrors -n 6 /etc/pacman.d/mirrorlist.backup > /etc/pacman.d/mirrorlist

```

#### Obtener y ordenar una lista de servidores de réplicas funcionales

Para comenzar con una lista reducida de servidores de réplicas actualizados basados en algunos países y que sirvan de fuente a *rankmirrors*, se puede obtener la lista de *Pacman Mirrorlist Generator*. La siguiente orden muestra los servidores de réplicas actualizados de *Francia* o *Reino Unido* que admiten el protocolo *https*, los descomenta en la lista y luego los clasifica y genera el 5 más rápido:

```
$ curl -s "[https://www.archlinux.org/mirrorlist/?country=FR&country=GB&protocol=https&use_mirror_status=on](https://www.archlinux.org/mirrorlist/?country=FR&country=GB&protocol=https&use_mirror_status=on)" | sed -e 's/^#Server/Server/' -e '/^#/d' | rankmirrors -n 5 -

```

**Sugerencia:** este procedimiento se puede hacer interactivamente navegando a `[https://www.archlinux.org/mirrorlist](https://www.archlinux.org/mirrorlist)` con cualquier navegador basado en texto, por ejemplo [elinks(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/elinks.1).

### Clasificación del lado del servidor

El [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) oficial proporciona una manera fácil de obtener una lista clasificada de servidores de réplicas. Debido a que toda la clasificación se realiza en un único servidor que tiene en cuenta múltiples factores, la cantidad de carga en los servidores de réplicas y los clientes es significativamente menor en comparación con la clasificación en cada cliente individual.

Otra alternativa popular es la siguiente herramienta:

**[Reflector](/index.php/Reflector "Reflector")** — Recupera la última lista servidores de réplicas de la página [MirrorStatus](https://www.archlinux.org/mirrors/status/), los filtra y los ordena por velocidad, y sobrescribe el archivo `/etc/pacman.d/mirrorlist`

	[https://xyne.archlinux.ca/projects/reflector/](https://xyne.archlinux.ca/projects/reflector/) || [reflector](https://www.archlinux.org/packages/?name=reflector)

## Solución de problemas

En caso de que encuentre el siguiente error:

```
error: config file /etc/pacman.d/mirrorlist could not be read: No such file or directory

```

Obtenga la lista servidores de réplicas directamente desde el sitio web:

```
# curl -o /etc/pacman.d/mirrorlist https://www.archlinux.org/mirrorlist/all/

```

Asegúrese de descomentar un servidor de réplica preferido como se describió anteriormente, así:

```
# pacman -Syu pacman-mirrorlist

```

## Véase también

*   [GitHub archweb mirrorlist.py](https://github.com/archlinux/archweb/blob/master/mirrors/views/mirrorlist.py) — código fuente del generador demirrorlist de archweb