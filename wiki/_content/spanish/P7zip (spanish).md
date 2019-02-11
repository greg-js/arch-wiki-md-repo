**Estado de la traducción**
Este artículo es una traducción de [p7zip](/index.php/P7zip "P7zip"), revisada por última vez el **2019-02-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=P7zip&diff=0&oldid=557880) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[p7zip](http://p7zip.sourceforge.net/) es un port de línea de comandos de [7-Zip](https://en.wikipedia.org/wiki/es:7-Zip "wikipedia:es:7-Zip") para sistemas [POSIX](https://en.wikipedia.org/wiki/es:POSIX "wikipedia:es:POSIX"), incluido Linux.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Ejemplos](#Ejemplos)
*   [3 Diferencias entre los binarios de 7z, 7za y 7zr](#Diferencias_entre_los_binarios_de_7z,_7za_y_7zr)
*   [4 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [p7zip](https://www.archlinux.org/packages/?name=p7zip).

El comando para ejecutar el programa es el siguiente:

```
$ 7z

```

## Ejemplos

*   Listar el contenido de un archivo:

```
$ 7z l <nombre del archivo>

```

*   Extraer todos los archivos de un archivo al directorio actual sin usar nombres de directorio:

```
$ 7z e <nombre del archivo>

```

*   Extraer con rutas completas:

```
$ 7z x <nombre del archivo>

```

*   Extraer a un nuevo directorio:

```
$ 7z x -o<nombre de la carpeta> <nombre del archivo>

```

## Diferencias entre los binarios de 7z, 7za y 7zr

El paquete incluye tres binarios, `/usr/bin/7z`, `/usr/bin/7za`, y `/usr/bin/7zr`. Sus páginas del manual explican las diferencias:

*   [7z(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/7z.1) utiliza plugins para manejar archivos.
*   [7za(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/7za.1) es un ejecutable stand-alone que maneja menos formatos de archivo que 7z.
*   [7zr(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/7zr.1) es un ejecutable stand-alone. Es una "versión ligera" de 7za que solo maneja archivos 7z. A diferencia de 7za, no puede manejar archivos encriptados.

## Véase también

*   [Página web de 7zip](http://7zip-es.updatestar.com/download.html)
*   [Cómo usar 7zip en la línea de comandos de Linux](https://www.ibm.com/developerworks/community/blogs/6e6f6d1b-95c3-46df-8a26-b7efd8ee4b57/entry/how_to_use_7zip_on_linux_command_line144?lang=en)