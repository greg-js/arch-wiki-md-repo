**Estado de la traducción**
Este artículo es una traducción de [Pacman/Restore local database](/index.php/Pacman/Restore_local_database "Pacman/Restore local database"), revisada por última vez el **2018-11-24**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Pacman/Restore_local_database&diff=0&oldid=557130) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Señales de que pacman necesita una restauración de la base de datos local:

*   `pacman -Q` no da absolutamente ninguna salida, y `pacman -Syu` informa erróneamente que el sistema está actualizado.
*   Al intentar instalar un paquete utilizando `pacman -S paquete`, se genera una lista de dependencias ya satisfechas.

Lo más probable es que esto se deba a que la base de datos de software instalado por pacman, `/var/lib/pacman/local`, se haya corrompido o eliminado. Si bien este es un problema grave, puede restaurarse siguiendo las instrucciones siguientes.

En primer lugar, asegúrese de que el archivo de registro de pacman esté presente:

```
$ ls /var/log/pacman.log

```

Si no existe, *no* será posible continuar con este método. Puede usar el [script de detección de paquetes de Xyne](https://bbs.archlinux.org/viewtopic.php?pid=670876) para recrear la base de datos. Si no es así, entonces la solución más factible será reinstalar todo el sistema.

## Generar la lista de recuperación de paquetes

**Advertencia:** si por algún motivo la memoria caché de [pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") de destino de paquetes de [makepkg (Español)](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)") contiene paquetes para otras arquitecturas, elimínelos antes de continuar.

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [pacutils](https://www.archlinux.org/packages/?name=pacutils) para obtener *paclog*.

Cree un script de filtro de registro y hágalo ejecutable:

 `pacrecover` 
```
#!/bin/bash -e

. /etc/makepkg.conf

PKGCACHE=$((grep -m 1 '^CacheDir' /etc/pacman.conf || echo 'CacheDir = /var/cache/pacman/pkg') | sed 's/CacheDir = //')

pkgdirs=("$@" "$PKGDEST" "$PKGCACHE")

while read -r -a parampart; do
  pkgname="${parampart[0]}-${parampart[1]}-*.pkg.tar.xz"
  for pkgdir in ${pkgdirs[@]}; do
    pkgpath="$pkgdir"/$pkgname
    [ -f $pkgpath ] && { echo $pkgpath; break; };
  done || echo ${parampart[0]} 1>&2
done

```

Ejecute el script (opcionalmente, pasando directorios adicionales con paquetes como parámetros):

```
$ paclog --pkglist /var/log/pacman.log | ./pacrecover >files.list 2>pkglist.orig

```

De esta manera, se crearán dos archivos: `files.list` con los archivos de paquetes que todavía están presentes en el equipo, y `pkglist.orig`, paquetes que se deben descargar. La operación posterior puede dar lugar a discrepancia entres los archivos de versiones anteriores aún presentes en el equipo, y los archivos que se encuentran con una nueva versión. Dichos desajustes deberán ser arreglados manualmente.

He aquí una forma de restringir automáticamente la segunda lista a los paquetes disponibles en un repositorio:

```
$ { cat pkglist.orig; pacman -Slq; } | sort | uniq -d > pkglist

```

**Nota:** si esto falla mostrando `failed to initialise alpm library`, verifique si `/var/lib/pacman/local/ALPM_DB_VERSION` existe. En caso contrario, ejecute `pacman-db-upgrade` como root, seguido de `pacman -Sy` y luego **repita la orden anterior**.

Compruebe si falta algún paquete *base* importante y agréguelo a la lista:

```
$ comm -23 <(pacman -Sgq base | sort) pkglist.orig >> pkglist

```

Continúe una vez que el contenido de ambas listas sea satisfactorio, ya que se utilizarán para restaurar la base de datos de paquetes instalada por pacman (`/var/lib/pacman/local/`).

## Realizar la recuperación

Defina una función de bash para fines de recuperación:

```
 recovery-pacman() {
    sudo pacman "$@"  \
    --log /dev/null   \
    --noscriptlet     \
    --dbonly          \
    --force           \
    --nodeps          \
    --needed
}

```

`--log /dev/null` permite evitar la saturación innecesaria del registro de pacman, `--needed` ahorrará tiempo al omitir instalar paquetes ya presentes en la base de datos, `--nodeps` permitirá la instalación de paquetes almacenados en caché, incluso si los paquetes que se instalan dependen de versiones más nuevas. El resto de opciones permitirá que **pacman** funcione sin leer/escribir el sistema de archivos.

Refresque la base de datos:

```
# pacman -Sy

```

Inicie la generación de la base de datos instalando archivos de paquetes disponibles localmente desde `files.list`:

```
# recovery-pacman -U $(< files.list)

```

Instale el resto desde `pkglist`:

```
# recovery-pacman -S $(< pkglist)

```

Actualice la base de datos local para que los paquetes que no son requeridos por cualquier otro paquete se marquen como instalados explícitamente y el resto como dependencias. Necesitará tener más cuidado en el futuro al eliminar paquetes, pero con la base de datos original perdida es lo mejor que podemos hacer.

```
# pacman -D --asdeps $(pacman -Qq)
# pacman -D --asexplicit $(pacman -Qtq)

```

Opcionalmente, compruebe todos los paquetes instalados con daños:

```
# pacman -Qk

```

Opcionalmente [Pacman/Tips and tricks (Español)#Identificar archivos que no pertenecen a ningún paquete](/index.php/Pacman/Tips_and_tricks_(Espa%C3%B1ol)#Identificar_archivos_que_no_pertenecen_a_ningún_paquete "Pacman/Tips and tricks (Español)").

Actualice todos los paquetes:

```
# pacman -Su

```