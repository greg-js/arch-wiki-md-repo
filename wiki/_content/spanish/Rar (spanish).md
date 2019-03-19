**Estado de la traducción**
Este artículo es una traducción de [rar](/index.php/Rar "Rar"), revisada por última vez el **2019-03-18**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Rar&diff=0&oldid=569055) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

RAR (y UNRAR) es el puerto de Linux de la versión de línea de órdenes de [WinRAR](http://www.rarlab.com/download.htm) disponible en las plataformas i686 y x86-64.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Características clave](#Características_clave)
*   [2 Instalación](#Instalación)
    *   [2.1 RAR](#RAR)
    *   [2.2 UNRAR](#UNRAR)
*   [3 Archivo de configuración](#Archivo_de_configuración)
*   [4 Ejemplos de compresión RAR](#Ejemplos_de_compresión_RAR)
    *   [4.1 Sintaxis General](#Sintaxis_General)
    *   [4.2 Compresión recursiva de una estructura directorios completa](#Compresión_recursiva_de_una_estructura_directorios_completa)
    *   [4.3 Archivos en Modo Mixto](#Archivos_en_Modo_Mixto)
    *   [4.4 Compresión recursiva de muchas estructuras de directorio usando una lista](#Compresión_recursiva_de_muchas_estructuras_de_directorio_usando_una_lista)
*   [5 Ejemplos UNRAR](#Ejemplos_UNRAR)
    *   [5.1 Sintaxis General](#Sintaxis_General_2)

## Características clave

*   Cantidades variables de redundancia ("registro de recuperación" o "volúmenes de recuperación" que se muestran a continuación) pueden ser añadidas a un archivo, haciéndolo mas resistente a la corrupción. Incluso si algunas partes de un archivo están dañadas, es un posible recuperar completamente los datos almacenados si existe un registro de recuperación suficientemente grande. Por si mismo, [TAR](/index.php?title=TAR&action=edit&redlink=1 "TAR (page does not exist)") no tiene esta capacidad.
*   RAR es capaz de manejar eficientemente volúmenes divididos. El soporte integrado para archivos multi-volumen permite al programa de desmpaquetado que simplemente solicite al usuario por el siguiente archivo .parteXXX del archivo RAR, sin la necesidad de copiar manualmente y volver a unir las partes, o para extraer un archivo único sin necesitar todas las partes. RAR no soporta cintas, ya que utiliza operaciones de búsqueda y renombrado en sus archivos.
*   Los archivos RAR pueden ser un formato sólido, en donde todos los archivos comprimidos son tratados como un bloque de datos único. Los formatos de compresión mas utilizados actualmente (con excepción del viejo ZIP) permiten un estructuración sólida.
*   Fuertes capacidades de cifrado. Las versiones anteriores del formato de archivo usaban un algoritmo propietario; las versiones recientes usan el algoritmo de cifrado AES, un cifrado de bloque adoptado como estándar de cifrado por el gobierno de Estados Unidos. Las únicas formas conocidas para recuperar un archivo cifrado son a través de diccionario o ataques de fuerza bruta. En versiones recientes, la protección con contraseña también puede proteger opcionalmente los nombres de archivo, de modo que los nombres de archivos contenidos en el archivo no se mostrarán sin la contraseña correcta.

## Instalación

### RAR

Obtenga [rar](https://aur.archlinux.org/packages/rar/) (paquete completo sin UNRAR) disponible en [AUR (Español)](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

### UNRAR

[unrar](https://www.archlinux.org/packages/?name=unrar) es provisto por separado y reside en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Instálelo vía [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") como siempre.

## Archivo de configuración

RAR para Linux lee la información de configuración desde el archivo `~/.rarrc` (es decir, en el directorio de inicio del usuario) o si desea definir un conjunto de opciones globales para todos los usuarios en el directorio /etc.

La sintaxis del archivo es simplemente la siguiente cadena:

```
switches=any RAR switches, separated by spaces

```

Por ejemplo:

```
switches=-m5 -rr5 -ol -msjpg;mp3;avi;zip;rar;tar;gz;jpg

```

Para una listado completo y explicaciones de los modificadores de rar, consulte la [página del manual](https://ss64.com/bash/rar.html).

## Ejemplos de compresión RAR

### Sintaxis General

```
$ rar *command* -*switch 1* -*switch N* *archive* *files.rar* *@listfiles...*

```

Para un listado completo de órdenes y modificadores, consulte la última seccción de éste artículo o simplemente ejecute `rar`.

### Compresión recursiva de una estructura directorios completa

*   Tarea: respaldar `/home/darkhorse` en `/media/data/darkhorse-backup.rar` usando registros de recuperación del 10 %:

```
$ rar a -r -rr10 /media/data/darkhorse-backup.rar /home/darkhorse

```

*   Explicado:

| Modificador | Acción |
| a | **a**grega archivos a los archivos comprimidos. |
| -r | **r**ecursión de subdirectorios (incluye a todos los directorios/archivos bajo el directorio principal). |
| -rr10 | agrega **r**egistros de **r**ecuperación al archivo. Ésto eleva a un 10% que el archivo comprimido llegue a ser corrupto o inutilizable, y que llegue a ser capaz de recuperar los datos por paridad. |

### Archivos en Modo Mixto

Puede usar también archivos en modo mixto de lo cual significa que los tipos de archivo que especifique no sean comprimidos - simplemente se almacenan.

*   Tarea: respaldar `/home/darkhorse` en `/media/data/darkhorse-backup.rar`:

```
$ rar a -r -rr10 -s -m5 -msjpg;mp3;tar /media/data/darkhorse-backup.rar /home/darkhorse

```

*   Explicación:

| Modificador | Acción |
| a | **a**grega archivos al archivo comprimido. |
| -r | **r**ecursión de subdirectorios (incluye a todos los directorios/archivos bajo el directorio principal). |
| -rr10 | agrega **r**egistros de **r**ecuperación al archivo. Ésto eleva a un 10% que el archivo comprimido llegue a ser corrupto o inutilizable, y que llegue a ser capaz de recuperar los datos por paridad. |
| -m5 | Usa el nivel mas alto de compresión (m0 = almacena ... m3 = default ... m5 = máximo nivel de compresión. |
| -msjpg;mp3;tar | ignora la opción de compresión y almacena todos los archivos .jpg y .mp3 y .tar. |

### Compresión recursiva de muchas estructuras de directorio usando una lista

*   Tarea: comprimir `/home/darkhorse` y `/home/palomino` y `/home/seabiscuit` en `/media/data/homes-backup.rar`.

Primero cree una lista (un simpe archivo de texto) que contenga los distintos objetivos. En este ejemplo, la lista será de tres largas líneas. La nombré 'home-list' en éste ejemplo pero puede llamarlo como quiera.

```
/home/darkhorse
/home/palomino
/home/seabiscuit

```

```
$ rar a -r -rr10 -s /media/data/homes-backup.rar @/path/to/home-list

```

## Ejemplos UNRAR

### Sintaxis General

```
$ unrar *command* -*switch 1* -*switch N* *archive* *files...* *@listfiles...* *path_to_extract\*

```

Para una lista completa de órdenes y modificadores simplemente ejecute:

```
$ unrar h

```

Para extraer en un nueva carpeta:

```
$ unrar x /media/data/homes-backup.rar homes-backup/

```

Para archivos multi-partes, ejecute:

```
$ unrar x homes-backup.part1.rar homes-backup/

```