**Estado de la traducción**
Este artículo es una traducción de [GNU](/index.php/GNU "GNU"), revisada por última vez el **2018-10-25**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GNU&diff=0&oldid=550124) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Arch Linux](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)")
*   [Utilidades principales](/index.php/Core_utilities_(Espa%C3%B1ol) "Core utilities (Español)")

From [Wikipedia](https://en.wikipedia.org/wiki/es:GNU "wikipedia:es:GNU"):

	GNU es un sistema operativo y una extensa colección de programas de computadora. GNU está compuesto en su totalidad de software libre, la mayoría de los cuales está licenciado bajo la Licencia Pública General (GPL) del propio Proyecto GNU. GNU es un acrónimo recursivo de "GNU's Not Unix!" *(¡GNU no es unix!)*.

Debido a que el kernel de GNU, [Hurd](https://www.gnu.org/s/hurd/hurd.html), no está listo para producción [[1]](https://www.gnu.org/software/hurd/hurd/status.html) GNU se utiliza generalmente con el kernel de Linux. [Arch Linux](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)") es una distribución de GNU/Linux de este tipo, que utiliza software de GNU como el intérprete de línea de órdenes [Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)"), *coreutils* de GNU, *toolchain* de GNU y muchas otras utilidades y bibliotecas. Esta página no intenta listar todos los paquetes GNU que son [casi 400](https://www.gnu.org/software/software.html#allgnupkgs) y solo destaca algunos.

## Contents

*   [1 Texinfo](#Texinfo)
*   [2 Sistema Base](#Sistema_Base)
*   [3 Toolchain](#Toolchain)
    *   [3.1 Sistema de construcción](#Sistema_de_construcci.C3.B3n)
*   [4 Otros programas](#Otros_programas)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Texinfo

Los programas de GNU se documentan utilizando la sintaxis de composición tipográfica [Texinfo](https://en.wikipedia.org/wiki/es:Texinfo "wikipedia:es:Texinfo"). Puede ver los documentos de información utilizando el programa `info`, proporcionado por el paquete [texinfo](https://www.archlinux.org/packages/?name=texinfo), que forma parte de [base](https://www.archlinux.org/groups/x86_64/base/).

Si bien la mayoría de los programas de GNU también tienen [páginas de manual](/index.php/Man_page_(Espa%C3%B1ol) "Man page (Español)"), los documentos de información tienden a ser más completos.

## Sistema Base

*   **[GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)")** — GRUB es el gestor de arranque del proyecto GNU.

	[https://www.gnu.org/software/grub/](https://www.gnu.org/software/grub/) || [grub](https://www.archlinux.org/packages/?name=grub)

*   **[Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)")** — Es un intérprete de línea de órdenes compatible con sh que incorpora características útiles del intérprete de línea de órdenes Korn (ksh) y del intérprete de línea de órdenes C (csh).

	[https://www.gnu.org/software/bash/](https://www.gnu.org/software/bash/) || [bash](https://www.archlinux.org/packages/?name=bash)

*   **[Coreutils](/index.php/Coreutils_(Espa%C3%B1ol) "Coreutils (Español)")** — Coreutils proporciona las utilidades básicas de manipulación de archivos, intérprete de línea de órdenes y texto del sistema operativo GNU.

	[https://www.gnu.org/software/coreutils/](https://www.gnu.org/software/coreutils/) || [coreutils](https://www.archlinux.org/packages/?name=coreutils)

*   **[gzip](https://en.wikipedia.org/wiki/es:gzip "wikipedia:es:gzip")** — gzip es tanto un formato de archivo como una aplicación para compresión y descompresión.

	[https://www.gnu.org/software/gzip/](https://www.gnu.org/software/gzip/) || [gzip](https://www.archlinux.org/packages/?name=gzip)

*   **[tar](/index.php/Tar_(Espa%C3%B1ol) "Tar (Español)")** — Proporciona la capacidad de crear o descomprimir archivos tar, así como varios otros tipos de manipulación.

	[https://www.gnu.org/software/tar/](https://www.gnu.org/software/tar/) || [tar](https://www.archlinux.org/packages/?name=tar)

## Toolchain

La mayoría de las herramientas de [toolchain de GNU](https://en.wikipedia.org/wiki/es:GNU_toolchain "wikipedia:es:GNU toolchain") están en el grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), excepto *glibc*, que está en [base](https://www.archlinux.org/groups/x86_64/base/) y GDB, que no está en ningún grupo.

*   **[GNU make](https://en.wikipedia.org/wiki/es:Make "wikipedia:es:Make")** — Utilidad para mantener grupos de programas.

	[http://www.gnu.org/software/make](http://www.gnu.org/software/make) || [make](https://www.archlinux.org/packages/?name=make)

*   **[GCC](/index.php/GCC_(Espa%C3%B1ol) "GCC (Español)")** — La colección de compiladores GNU - frontends de C y C++.

	[https://gcc.gnu.org/](https://gcc.gnu.org/) || [gcc](https://www.archlinux.org/packages/?name=gcc)

*   **[glibc](https://en.wikipedia.org/wiki/es:glibc "wikipedia:es:glibc")** — Implementación de GNU de la biblioteca C.

	[https://www.gnu.org/software/libc/](https://www.gnu.org/software/libc/) || [glibc](https://www.archlinux.org/packages/?name=glibc) (parte de [base](https://www.archlinux.org/groups/x86_64/base/))

*   **[GNU Binutils](https://en.wikipedia.org/wiki/es:GNU_Binutils "wikipedia:es:GNU Binutils")** — Un conjunto de programas para ensamblar y manipular archivos binarios y de objetos. Incluye [ld](https://en.wikipedia.org/wiki/GNU_linker "wikipedia:GNU linker").

	[https://www.gnu.org/software/binutils/](https://www.gnu.org/software/binutils/) || [binutils](https://www.archlinux.org/packages/?name=binutils)

*   **[GNU bison](https://en.wikipedia.org/wiki/es:GNU_bison "wikipedia:es:GNU bison")** — El generador de analizadores *(parser generator)* de propósito general de GNU.

	[https://www.gnu.org/software/bison/bison.html](https://www.gnu.org/software/bison/bison.html) || [bison](https://www.archlinux.org/packages/?name=bison)

*   **[GNU m4](https://en.wikipedia.org/wiki/GNU_m4 "wikipedia:GNU m4")** — El procesador de macros de GNU.

	[https://www.gnu.org/software/m4/](https://www.gnu.org/software/m4/) || [m4](https://www.archlinux.org/packages/?name=m4)

*   **[GDB](https://en.wikipedia.org/wiki/es:GNU_Debugger "wikipedia:es:GNU Debugger")** — El depurador de GNU.

	[https://www.gnu.org/software/gdb/](https://www.gnu.org/software/gdb/) || [gdb](https://www.archlinux.org/packages/?name=gdb)

### Sistema de construcción

De [Wikipedia](https://en.wikipedia.org/wiki/es:GNU_build_system "wikipedia:es:GNU build system"):

	El sistema de construcción de GNU, también conocido como Autotools, es un conjunto de herramientas de programación diseñadas para ayudar a hacer que los paquetes de código fuente sean portables a muchos sistemas similares a Unix.

*   **[GNU Autoconf](https://en.wikipedia.org/wiki/es:Autoconf "wikipedia:es:Autoconf")** — Herramienta para configurar automáticamente el código fuente.

	[http://www.gnu.org/software/autoconf](http://www.gnu.org/software/autoconf) || [autoconf](https://www.archlinux.org/packages/?name=autoconf)

*   **[GNU Automake](https://en.wikipedia.org/wiki/es:GNU_Automake "wikipedia:es:GNU Automake")** — Herramienta para crear Makefiles automáticamente.

	[http://www.gnu.org/software/automake](http://www.gnu.org/software/automake) || [automake](https://www.archlinux.org/packages/?name=automake)

*   **[GNU Libtool](https://en.wikipedia.org/wiki/es:GNU_Libtool "wikipedia:es:GNU Libtool")** — Una biblioteca genérico de soporte para script.

	[http://www.gnu.org/software/libtool](http://www.gnu.org/software/libtool) || [libtool](https://www.archlinux.org/packages/?name=libtool)

## Otros programas

Muchas otras herramientas de GNU opcionales están disponibles en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"):

*   [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"), un entorno de escritorio
*   [GIMP](/index.php/GIMP "GIMP"), un editor de imágenes
*   [GTK+](/index.php/GTK%2B_(Espa%C3%B1ol) "GTK+ (Español)"), un kit de herramientas de widgets
*   [Gnumeric](/index.php/Gnumeric "Gnumeric"), un programa de hoja de cálculo
*   [GNU Parted](/index.php/GNU_Parted "GNU Parted"), un gestor de particiones
*   [GNU Screen](/index.php/GNU_Screen "GNU Screen"), un multiplexor de terminal
*   [GNU nano](/index.php/GNU_nano_(Espa%C3%B1ol) "GNU nano (Español)"), un editor de texto de línea de órdenes
*   [GNU Emacs](/index.php/GNU_Emacs_(Espa%C3%B1ol) "GNU Emacs (Español)"), Un editor de texto extensible, personalizable y autodocumentado
*   [GnuPG](/index.php/GnuPG_(Espa%C3%B1ol) "GnuPG (Español)"), una implementación de OpenPGP
*   [GNU Octave](/index.php/GNU_Octave "GNU Octave"), un lenguaje de programación científica
*   [GNU Readline](/index.php/Readline_(Espa%C3%B1ol) "Readline (Español)"), Una biblioteca de edición para interfaces de línea de órdenes

## Véase también

*   [https://www.gnu.org/](https://www.gnu.org/)
*   [El manifiesto de GNU](https://www.gnu.org/gnu/manifesto)
*   [Wikipedia:es:Anexo:Paquetes GNU](https://en.wikipedia.org/wiki/es:Anexo:Paquetes_GNU "wikipedia:es:Anexo:Paquetes GNU")
*   El [proyecto Arch Hurd](https://archhurd.org/) tiene como objetivo portar Arch Linux al kernel Hurd.