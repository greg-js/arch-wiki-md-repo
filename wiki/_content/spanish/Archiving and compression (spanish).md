**Estado de la traducción**
Este artículo es una traducción de [Archiving and compression](/index.php/Archiving_and_compression "Archiving and compression"), revisada por última vez el **2018-11-18**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Archiving_and_compression&diff=0&oldid=555712) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Las herramientas tradicionales de archivado y compresión de Unix se separan de acuerdo con la [filosofía de Unix](https://en.wikipedia.org/wiki/Unix_philosophy "wikipedia:Unix philosophy"):

*   Un [archivador](https://en.wikipedia.org/wiki/es:Archivador_de_ficheros "wikipedia:es:Archivador de ficheros") combina varios archivos en uno solo, por ejemplo *tar*.
*   Una herramienta de [compresión](https://en.wikipedia.org/wiki/es:Compresi%C3%B3n_de_datos "wikipedia:es:Compresión de datos") comprime y descomprime datos, por ejemplo *gzip*.

Estas herramientas a menudo se utilizan en secuencia creando primero un archivo de almacenamiento y luego comprimiéndolo.

Por supuesto, también hay [herramientas que hacen ambas cosas](#Archivado_y_compresión), que tienden a ofrecer adicionalmente cifrado, detección de errores y recuperación.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Solo archivado](#Solo_archivado)
*   [2 Herramientas de compresión](#Herramientas_de_compresión)
    *   [2.1 Solo compresión](#Solo_compresión)
    *   [2.2 Archivado y compresión](#Archivado_y_compresión)
    *   [2.3 Tablas de características](#Tablas_de_características)
        *   [2.3.1 Descompresión](#Descompresión)
*   [3 Comparación de utilización](#Comparación_de_utilización)
    *   [3.1 Utilización para solo archivado](#Utilización_para_solo_archivado)
    *   [3.2 Utilización para solo compresión](#Utilización_para_solo_compresión)
    *   [3.3 Utilización para archivado y compresión](#Utilización_para_archivado_y_compresión)
*   [4 Herramientas convenientes](#Herramientas_convenientes)
*   [5 Determinar el formato de archivo](#Determinar_el_formato_de_archivo)
*   [6 Herramientas esotéricas, raras u obsoletas](#Herramientas_esotéricas,_raras_u_obsoletas)
*   [7 Bibliotecas de compresión](#Bibliotecas_de_compresión)
*   [8 Véase también](#Véase_también)

## Solo archivado

| Nombre | Paquete | Manuales | Descripción |
| GNU [tar](https://en.wikipedia.org/wiki/es:tar para manipular los archivos de tar ubicuos (tarballs), que son utilizados por [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") y [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)"). |
| [libarchive](http://libarchive.org/) | [libarchive](https://www.archlinux.org/packages/?name=libarchive) | [bsdtar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bsdtar.1)
[bsdcpio(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bsdcpio.1) | Implementación de *tar* y *cpio* que también ofrece una biblioteca. Utilizado por [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") y [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"). |
| [ar](https://en.wikipedia.org/wiki/es:ar_(Unix) | [binutils](https://www.archlinux.org/packages/?name=binutils) | [ar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ar.1) | Archivador de Unix heredado anterior a *tar*. Hoy solo se utiliza para crear archivos de [biblioteca estáticos](https://en.wikipedia.org/wiki/Static_library "wikipedia:Static library"). |
| [cpio](https://en.wikipedia.org/wiki/es:cpio "wikipedia:es:cpio") | [cpio](https://www.archlinux.org/packages/?name=cpio) | [cpio(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cpio.1) | Archivador a través de stdin/stdout, soporta los formatos cpio y tar. |
| [DAR](http://dar.linux.free.fr/) | [dar](https://aur.archlinux.org/packages/dar/) | [dar(1)](http://dar.linux.free.fr/doc/man/dar.html) | Archivador para hacer copias de seguridad de grandes sistemas de archivos en vivo, se encarga de los enlaces duros, [atributos extendidos](/index.php/Extended_attributes "Extended attributes"), archivos dispersos y tipos de inodo. |

**Sugerencia:** Tanto tar de GNU como de BSD hacen automáticamente la delegación de descompresión para los archivos comprimidos con bzip2, compress, gzip, lzip, lzma y xz. Al crear archivos, ambos admiten la opción `-a` para filtrar automáticamente el archivo creado a través del programa de compresión adecuado en función de la extensión del archivo. Mientras que tar de BSD reconoce los formatos de compresión basados ​​en el formato, tar de GNU lo adivina según la extensión del archivo.

Véase también [#Utilización para solo archivado](#Utilización_para_solo_archivado).

## Herramientas de compresión

### Solo compresión

Estos programas de compresión implementan su propio formato de archivo de almacenamiento.

| Nombre | Paquete | Manual | Ext | Ext tar | Descripción | Implementación multihilo |
| [bzip2](https://en.wikipedia.org/wiki/bzip2 "wikipedia:bzip2") | [bzip2](https://www.archlinux.org/packages/?name=bzip2) | [bzip2(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bzip2.1) | .bz2, .bz | .tbz2, .tbz | Utiliza el [algoritmo Burrows–Wheeler](https://en.wikipedia.org/wiki/es:Compresi%C3%B3n_de_Burrows-Wheeler "wikipedia:es:Compresión de Burrows-Wheeler"). | [lbzip2](https://www.archlinux.org/packages/?name=lbzip2), [pbzip2](https://www.archlinux.org/packages/?name=pbzip2) |
| [gzip](https://en.wikipedia.org/wiki/gzip "wikipedia:gzip") | [gzip](https://www.archlinux.org/packages/?name=gzip) | [gzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gzip.1) | .gz, .z | .tgz, .taz | GNU zip, basado en el algoritmo [DEFLATE](https://en.wikipedia.org/wiki/es:Deflaci%C3%B3n_(algoritmo) "wikipedia:es:Deflación (algoritmo)"). | [pigz](https://www.archlinux.org/packages/?name=pigz) |
| [lrzip](/index.php/Lrzip "Lrzip") | [lrzip](https://www.archlinux.org/packages/?name=lrzip) | [lrzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lrzip.1) | .lrz | Versión mejorada de [rzip](https://en.wikipedia.org/wiki/rzip "wikipedia:rzip"), utiliza varios algoritmos. | es multihilo |
| [LZ4](https://en.wikipedia.org/wiki/LZ4_(compression_algorithm) | [lz4](https://www.archlinux.org/packages/?name=lz4) | [lz4(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lz4.1) | .lz4 | Escrito en C, orientado a la velocidad de compresión y descompresión. | es multihilo |
| [lzip](https://en.wikipedia.org/wiki/es:lzip "wikipedia:es:lzip") | [lzip](https://www.archlinux.org/packages/?name=lzip) | [lzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lzip.1) | .lz | Utiliza [LZMA](https://en.wikipedia.org/wiki/es:LZMA "wikipedia:es:LZMA"). | [plzip](https://aur.archlinux.org/packages/plzip/) |
| [lzop](https://en.wikipedia.org/wiki/lzop "wikipedia:lzop") | [lzop](https://www.archlinux.org/packages/?name=lzop) | [lzop(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lzop.1) | .lzop | .tzo | Utiliza la biblioteca [LZO](https://en.wikipedia.org/wiki/Lempel%E2%80%93Ziv%E2%80%93Oberhumer "wikipedia:Lempel–Ziv–Oberhumer") ([lzo](https://www.archlinux.org/packages/?name=lzo)). |
| [xz](https://en.wikipedia.org/wiki/xz "wikipedia:xz") | [xz](https://www.archlinux.org/packages/?name=xz) | [xz(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xz.1) | .xz, .lzma | .txz, .tlz | Utiliza [LZMA](https://en.wikipedia.org/wiki/es:LZMA "wikipedia:es:LZMA"), predeterminado para GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) y el archivo del kernel. | [pixz](https://www.archlinux.org/packages/?name=pixz), [pxz](https://aur.archlinux.org/packages/pxz/) |

*   Las implementaciones multihilo ofrecen velocidades mejoradas mediante el uso de múltiples núcleos de CPU.
*   Las extensiones de tar se refieren a archivos comprimidos donde se utiliza `tar` y la herramienta de compresión, por ejemplo. `.tzo` es `.tar.lzo`.
*   Véase también [#Utilización para solo compresión](#Utilización_para_solo_compresión).

### Archivado y compresión

| Nombre | Paquete(s) | Manuale(s) | Ext | Descripción |
| [7z](https://en.wikipedia.org/wiki/es:7z "wikipedia:es:7z") | [p7zip](https://www.archlinux.org/packages/?name=p7zip) | [7z(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/7z.1) | .7z | Port POSIX de la línea de órdenes 7-zip. Véase [p7zip](/index.php/P7zip "P7zip"). |
| [RAR](https://en.wikipedia.org/wiki/es:RAR "wikipedia:es:RAR") | [rar](https://aur.archlinux.org/packages/rar/), [unrar](https://www.archlinux.org/packages/?name=unrar) | rar(1) | .rar | Tanto el formato como la utilidad [rar](/index.php/Rar "Rar") son ​​propietarios. |
| [ZIP](https://en.wikipedia.org/wiki/es:Formato_de_compresi%C3%B3n_ZIP "wikipedia:es:Formato de compresión ZIP") | [zip](https://www.archlinux.org/packages/?name=zip), [unzip](https://www.archlinux.org/packages/?name=unzip) | [zip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zip.1), [unzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unzip.1) | .zip | Ampliamente utilizado fuera del mundo Linux. |
| [Unarchiver](https://theunarchiver.com/) | [unarchiver](https://www.archlinux.org/packages/?name=unarchiver) | [unar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unar.1), [lsar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsar.1) | *many* | Herramienta de línea de órdenes de una aplicación Mac, soporta más de 40 formatos de archivo de almacenamiento. |
| [ZPAQ](https://en.wikipedia.org/wiki/ZPAQ "wikipedia:ZPAQ") | [zpaq](https://aur.archlinux.org/packages/zpaq/) | [zpaq(1)](http://mattmahoney.net/dc/zpaqdoc.html) | .zpaq | Un archivador de alta tasa de compresión escrito en C++, utiliza varios algoritmos. |

Véase también [#Utilización para archivado y compresión](#Utilización_para_archivado_y_compresión).

### Tablas de características

#### Descompresión

| Nombre | gzip | bzip2 | ZIP | compress | pack | CAB | ARJ |
| [gzip](https://www.archlinux.org/packages/?name=gzip) | Sí | No | Sí | Sí | Sí | No | No |
| [p7zip](https://www.archlinux.org/packages/?name=p7zip) | Sí | Sí | Sí | No | Sí | Sí | Sí |
| [unarchiver](https://www.archlinux.org/packages/?name=unarchiver) | Sí | Sí | Sí | Sí | No | Sí | parcial |

## Comparación de utilización

### Utilización para solo archivado

| Nombre | Crear archivo | Extraer archivo | Listar contenido |
| [tar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tar.1) | `tar cfv archivo_almacenamiento.tar archivo1 archivo2` | `tar xfv archivo_almacenamiento.tar` | `tar -tvf archivo_almacenamiento.tar` |
| [cpio(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cpio.1) | `ls archivo1 archivo2 | cpio -o > archivo_almacenamiento.cpio` | `cpio -i -vd < archivo_almacenamiento.cpio` | `cpio -t < archivo_almacenamiento.cpio` |

### Utilización para solo compresión

| Nombre | Comprimir | Descomprimir | Descomprimir a la salida estándar |
| [bzip2(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bzip2.1) | `bzip2 archivo` | `bzip2 -d archivo.bz2` | `bzcat archivo.bz2` |
| [gzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gzip.1) | `gzip archivo` | `gzip -d archivo.gz` | `zcat archivo.gz` |
| [lrzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lrzip.1) | `lrzip archivo`
`lrztar carpeta` | `lrzip -d archivo.lrz`
`lrztar -d carpeta.tar.lrz` | `lrzcat archivo.lrz` |
| [xz(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xz.1) | `xz archivo` | `xz -d archivo.xz` | `xzcat archivo.xz` |

### Utilización para archivado y compresión

| Nombre | Comprimir | Descomprimir | Descomprimir a la salida estándar | Listar contenido |
| [7z(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/7z.1) | `7z a archivo_almacenamiento.7z archivo1 archivo2` | `7z x archivo_almacenamiento.7z` | `7z e -so archivo_almacenamiento.7z archivo1` | `7z l archivo_almacenamiento.7z` |
| rar(1) y unrar | `rar a archivo_almacenamiento.rar archivo1 archivo2` | `rar x archivo_almacenamiento.rar` | `rar p -inul archivo_almacenamiento.rar archivo1` | `rar l archivo_almacenamiento.rar` |
| [zip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zip.1), [unzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unzip.1) | `zip archivo_almacenamiento.zip archivo1 archivo2` | `unzip archivo_almacenamiento.zip` | `unzip -p archivo_almacenamiento.zip archivo1` | `unzip -l archivo_almacenamiento.zip` |

## Herramientas convenientes

*   **atool** — Script para gestionar archivos de almacenamiento de varios tipos.

	[https://www.nongnu.org/atool/](https://www.nongnu.org/atool/) || [atool](https://www.archlinux.org/packages/?name=atool)

*   **dtrx** — Una herramienta inteligente de extracción de archivos.

	[https://brettcsmith.org/2007/dtrx/](https://brettcsmith.org/2007/dtrx/) || [dtrx](https://aur.archlinux.org/packages/dtrx/)

*   **unp** — Herramienta de línea de órdenes que puede descomprimir archivos fácilmente.

	[https://github.com/mitsuhiko/unp](https://github.com/mitsuhiko/unp) || [python-unp](https://aur.archlinux.org/packages/python-unp/)

*   **unpack** — Script Wrapper para manejar múltiples formatos de archivo.

	[https://github.com/githaff/unpack](https://github.com/githaff/unpack) || [unpack-git](https://aur.archlinux.org/packages/unpack-git/)

*   [Bash/Functions (Español)#Extraer](/index.php/Bash/Functions_(Espa%C3%B1ol)#Extraer "Bash/Functions (Español)")

## Determinar el formato de archivo

Para extraer un archivo, se debe determinar su formato. Si el archivo tiene el nombre correcto, puede deducir su formato a partir de su extensión.

De lo contrario, puede utilizar la herramienta [file](https://www.archlinux.org/packages/?name=file), véase [file(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/file.1).

## Herramientas esotéricas, raras u obsoletas

| Nombre | Paquete(s) | Ext | Descripción |
| [ARC](https://en.wikipedia.org/wiki/ARC_(file_format) | [arc](https://aur.archlinux.org/packages/arc/) | .arc, .ark | Fue muy popular durante los inicios de las BBS. Reemplazado por ZIP. |
| [ARJ](https://en.wikipedia.org/wiki/es:ARJ "wikipedia:es:ARJ") | [arj](https://www.archlinux.org/packages/?name=arj) | .arj | Un archivador utilizado en DOS/Windows a mediados de la década de 1990\. Este es una copia de código abierto. |
| [compress](https://en.wikipedia.org/wiki/es:compress "wikipedia:es:compress") | [ncompress](https://aur.archlinux.org/packages/ncompress/) | .Z | La utilidad clásica de compresión de Unix que puede manejar el antiguo archivo .Z. |
| [LHA](https://en.wikipedia.org/wiki/es:LHA "wikipedia:es:LHA") | [lha](https://aur.archlinux.org/packages/lha/) | .lzh, .lha | Formato popular en Japón, archivador para crear archivos en formato LH-7\. Solo 32 bits (requiere [multilib](/index.php/Multilib_(Espa%C3%B1ol) "Multilib (Español)")). |
| [PAR2](https://en.wikipedia.org/wiki/Parchive "wikipedia:Parchive") | [par2cmdline](https://www.archlinux.org/packages/?name=par2cmdline) | .par2 | Archivador con paridad para una mayor integridad de los datos. Véase también [Parchive](/index.php/Parchive "Parchive"). |
| [shar](https://en.wikipedia.org/wiki/es:shar "wikipedia:es:shar") | [sharutils](https://www.archlinux.org/packages/?name=sharutils) | .shar | Crea archivos autoextraíbles que son scripts de shell válidos. |
| [Zoo](https://en.wikipedia.org/wiki/Zoo_(file_format) | [zoo](https://aur.archlinux.org/packages/zoo/) | .zoo | Era sobre todo popular en el sistema operativo [OpenVMS](https://en.wikipedia.org/wiki/es:OpenVMS "wikipedia:es:OpenVMS") antes de que PKZIP se hiciera popular. |

## Bibliotecas de compresión

*   **[Brotli](https://en.wikipedia.org/wiki/Brotli "wikipedia:Brotli")** — Algoritmo de compresión para flujos de datos utilizando el algoritmo LZ77, la codificación de Huffman y el modelado de contexto de segundo orden.

	[https://github.com/google/brotli](https://github.com/google/brotli) || [brotli](https://www.archlinux.org/packages/?name=brotli)

*   **[zlib](https://en.wikipedia.org/wiki/zlib "wikipedia:zlib")** — Biblioteca de compresión que implementa el método de compresión deflate que se encuentra en gzip y PKZIP.

	[https://www.zlib.net/](https://www.zlib.net/) || [zlib](https://www.archlinux.org/packages/?name=zlib)

*   **[Zopfli](https://en.wikipedia.org/wiki/Zopfli "wikipedia:Zopfli")** — Compresor de archivos de alta tasa de compresión de Google, utilizando un algoritmo compatible con deflate llamado zopfli.

	[https://github.com/google/zopfli](https://github.com/google/zopfli) || [zopfli-git](https://aur.archlinux.org/packages/zopfli-git/)

## Véase también

*   [List of applications/Utilities#Archive managers](/index.php/List_of_applications/Utilities#Archive_managers "List of applications/Utilities")
*   [List of applications/Multimedia#Image compression](/index.php/List_of_applications/Multimedia#Image_compression "List of applications/Multimedia")
*   [Wikipedia:Comparison of file archivers](https://en.wikipedia.org/wiki/Comparison_of_file_archivers "wikipedia:Comparison of file archivers")
*   [Wikipedia:es:Anexo:Formatos de archivo](https://en.wikipedia.org/wiki/es:Anexo:Formatos_de_archivo "wikipedia:es:Anexo:Formatos de archivo")
*   [Wikipedia:Comparison of archive formats](https://en.wikipedia.org/wiki/Comparison_of_archive_formats "wikipedia:Comparison of archive formats")