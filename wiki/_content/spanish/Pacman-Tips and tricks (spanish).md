Para métodos generales para mejorar la flexibilidad de las sugerencias proporcionadas o del propio pacman, consulte [Core utilities](/index.php/Core_utilities "Core utilities") y [Bash](/index.php/Bash "Bash").

## Contents

*   [1 Mantenimiento](#Mantenimiento)
    *   [1.1 Listando paquetes](#Listando_paquetes)
        *   [1.1.1 Con el tamaño](#Con_el_tama.C3.B1o)
        *   [1.1.2 Por fecha](#Por_fecha)
*   [2 Optimización](#Optimizaci.C3.B3n)
    *   [2.1 Velocidades de acceso a la base de datos](#Velocidades_de_acceso_a_la_base_de_datos)
    *   [2.2 Velocidades de descarga](#Velocidades_de_descarga)
    *   [2.3 Powerpill](#Powerpill)
    *   [2.4 Wget](#Wget)
    *   [2.5 Aria2](#Aria2)

## Mantenimiento

### Listando paquetes

Es posible que desee obtener la lista de paquetes instalados con su versión, lo cual es útil cuando se reportan errores o se discuten los paquetes instalados.

*   Enumere todos los paquetes explícitamente instalados: pacman -Qe .
*   todos los paquetes nativos instalados explícitamente (es decir, presentes en la base de datos de sincronización) que no sean dependencias directas o opcionales: pacman -Qent .
*   Lista de todos los paquetes extranjeros (normalmente descargados e instalados manualmente): pacman -Qm .
*   Haga una lista de todos los paquetes nativos (instalados desde la (s) base de datos de sincronización): pacman -Qn .
*   Listar paquetes por regex: pacman -Qs regex .
*   Lista de paquetes por regex con formato de salida personalizado: expac -s "%-30n %v" regex (necesita expac ).

#### Con el tamaño

Para obtener una lista de paquetes instalados ordenados por tamaño, lo que puede ser útil al liberar espacio en el disco duro:

*   Instalar expac y ejecutar expac -HM '%m\t%n' | sort -h expac -HM '%m\t%n' | sort -h .
*   Ejecute pacgraph con la opción -c .

Para enumerar el tamaño de descarga de varios paquetes (deje packages en blanco para listar todos los paquetes):

```
 $ Expac -S -HM '% k \ t% n' paquetes

```

Para listar los paquetes explícitamente instalados que no están en base ni en base-devel con tamaño y descripción:

```
 $ Expac -HM "% 011m \ t% -20n \ t% 10d" $ (comm -23 <(pacman -Qqen | sort) <(pacman -Qqg base-devel | sort)) |  Ordenar -n

```

#### Por fecha

Para enumerar los 20 últimos paquetes instalados con expac , ejecute:

```
 $ Expac --timefmt = '% Y-% m-% d% T' '% l \ t% n' |  Ordenar |  Cola-n 20

```

O, con segundos desde la época (1970-01-01 UTC):

```
 $ Expac --timefmt =% s '% l \ t% n' |  Sort -n |  Cola-n 20

```

Lista los paquetes explícitamente instalados que no están en los grupos de base o base-devel :

```
 $ Comm -23 <(pacman -Qeq | sort) <(pacman -Qgq base base-devel | sort)

```

Enumere todos los paquetes instalados no requeridos por otros paquetes y que no estén en los grupos de base o de base :

```
 $ Comm -23 <(pacman -Qqt | sort) <(pacman -Sqg base base-devel | sort)

```

Como arriba, pero con descripciones:

```
 $ Expac -HM '% -20n \ t% 10d' $ (comm -23 <(pacman -Qqt | sort) <(pacman -Qqg base -devel | sort)

```

Lista todos los paquetes instalados que no están en el repositorio especificado repo_name

```
 $ Comm -23 <(pacman -Qtq | sort) <(pacman -Slq repo_name | sort)

```

Liste todos los paquetes instalados que están en el repositorio repo_name :

```
 $ Comm -12 <(pacman -Qtq | sort) <(pacman -Slq repo_name | sort)

```

## Optimización

### Velocidades de acceso a la base de datos

Pacman almacena toda la información del paquete en una colección de archivos pequeños, uno para cada paquete. La mejora de las velocidades de acceso a la base de datos reduce el tiempo empleado en las tareas relacionadas con la base de datos, por ejemplo, buscar paquetes y resolver las dependencias del paquete. El método más seguro y fácil es ejecutarlo como root:

```
 # Pacman-optimize

```

Esto intentará poner todos los archivos pequeños juntos en una ubicación (física) en el disco duro para que la cabeza del disco duro no tenga que moverse tanto al acceder a todos los datos. Este método es seguro, pero no es infalible: depende del sistema de archivos, el uso del disco y la fragmentación del espacio vacío. Otra opción más agresiva sería eliminar primero los paquetes desinstalados del caché y eliminar los repositorios no utilizados antes de la optimización de la base de datos:

```
 # Pacman -Sc && pacman-optimize

```

### Velocidades de descarga

Nota: Si las velocidades de descarga se han reducido a un rastreo, asegúrese de que está utilizando uno de los muchos espejos y no ftp.archlinux.org, que se estrangula desde marzo de 2007 . Al descargar paquetes pacman usa los espejos en el orden en que están en /etc/pacman.d/mirrorlist . El espejo que está en la parte superior de la lista por defecto, sin embargo, puede no ser el más rápido para usted. Para seleccionar un espejo más rápido, consulte Espejos . La velocidad de Pacman en la descarga de paquetes también puede ser mejorada mediante el uso de una aplicación diferente para descargar paquetes, en lugar del descargador de archivos integrado de Pacman. En todos los casos, asegúrese de tener la última Pacman antes de hacer cualquier modificación.

```
 # Pacman -Syu

```

### Powerpill

Powerpill es un envoltorio de Pacman que utiliza la descarga paralela y segmentada para tratar de acelerar las descargas de Pacman.

### Wget

Esto también es muy útil si necesita configuraciones proxy más potentes que las capacidades incorporadas de pacman.

Para usar wget , primero instale el paquete wget y luego modifique /etc/pacman.conf descomentando la siguiente línea en la sección [options] :

```
 XferCommand = / usr / bin / wget -c -q --show-progress --passive-ftp -O% o% u

```

En lugar de descomentar los parámetros de wget en /etc/pacman.conf , también puede modificar el archivo de configuración de wget directamente (el archivo de todo el sistema es /etc/wgetrc , por usuario los archivos son $HOME/.wgetrc .

### Aria2

Aria2 es una utilidad de descarga de peso ligero con soporte para HTTP / HTTPS y transferencias directas continuas y segmentadas. Aria2 permite múltiples y simultáneas conexiones HTTP / HTTPS y FTP a un espejo de Arch, lo que debería resultar en un aumento en las velocidades de descarga para la recuperación de archivos y paquetes.

Nota: El uso de aria2c en XferCommand de Pacman no dará lugar a descargas paralelas de varios paquetes. Pacman invoca el XferCommand con un solo paquete a la vez y espera a que se complete antes de invocar el siguiente. Para descargar varios paquetes en paralelo, consulte Powerpill.

Instale aria2 y luego edite /etc/pacman.conf agregando la siguiente línea a la sección [options] :

```
 XferCommand = / usr / bin / aria2c --allow-overwrite = true --continue = true --file-allocation = ninguno --log-level = error --max-tries = 2 --max-connection-per-server = 2 --max-file-not-found = 5 --min-split-size = 5M --no-conf --remote-time = true --summary-interval = 60 --timeout = 5 --dir = / --out% o% u

```

Sugerencia: Esta configuración alternativa para usar pacman con aria2 intenta simplificar la configuración y añade más opciones de configuración.

Vea OPCIONES en man aria2c para las opciones de aria2c usadas.

*   -d, --dir : El directorio para almacenar los archivos descargados según lo especificado por pacman .
*   -o, --out : El nombre de archivo de salida del archivo (s) descargado (s).
*   %o : Variable que representa el nombre de archivo local especificado por pacman.
*   %u : Variable que representa la URL de descarga especificada por pacman.