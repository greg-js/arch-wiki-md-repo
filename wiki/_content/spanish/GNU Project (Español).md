Tomado de [http://www.gnu.org/](http://www.gnu.org/)

	*GNU es un sistema operativo similar a Unix que es software libre y respeta su libertad.*

	*El Proyecto GNU se inició en 1984 para desarrollar el sistema GNU. El nombre «GNU» (que significa «ñu» en inglés) es un acrónimo recursivo de «GNU's Not Unix» (¡GNU No es Unix!) y en español se pronuncia fonéticamente, como una sílaba sin vocal entre la g y la n.*

	*Los sistemas operativos parecidos a Unix se construyen a partir de un conjunto de aplicaciones, bibliotecas y herramientas de programación, además de un programa para alojar recursos e interactuar con el hardware, denominado núcleo.*

Dado de que Arch Linux es una distribución basada en GNU/Linux, muchas de sus herramientas básicas pertenecen al proyecto GNU. Este artículo le dará una descripción de los componentes principales, así como también de otras útiles aplicaciones.

## Contents

*   [1 El Sistema Base](#El_Sistema_Base)
    *   [1.1 Núcleo](#N.C3.BAcleo)
    *   [1.2 Colección de Software](#Colecci.C3.B3n_de_Software)
*   [2 Herramientas de Desarrollo](#Herramientas_de_Desarrollo)
*   [3 Otras Herramientas](#Otras_Herramientas)
*   [4 Enlaces](#Enlaces)

## El Sistema Base

Al final del proceso de instalación, un sistema Arch no es nada más que un núcleo Linux, las herramientas principales GNU y unas pocas herramientas de línea de comandos. La instalación mínima normalmente contiene [el grupo base](https://www.archlinux.org/groups/i686/base/).

### Núcleo

Mientras que [Hurd](http://www.gnu.org/s/hurd/hurd.html), el núcleo GNU, está bajo activo desarrollo, no existe aún una versión oficial. Por esta razón Arch y la mayoría de otros sistemas basados en GNU, usan el núcleo Linux. El [Proyecto Arch Hurd](/index.php/Arch_Hurd_Project "Arch Hurd Project") tiene como objetivo portar Arch Linux al núcleo Hurd.

### Colección de Software

**cargador de arranque (bootloader):** [GRUB](/index.php/GRUB "GRUB") es el cargador de arranque estándar para Arch Linux, el cual es ahora mantenido por [GNU](http://www.gnu.org/software/grub/).

**librería de C:** [glibc](https://www.archlinux.org/packages/?name=glibc) es *"la librería la cual define las 'llamadas al sistema' y otras funciones básicas como open, malloc, printf, exit... "*[[1]](http://www.gnu.org/software/libc/)

**utilidades binarias:** [binutils](https://www.archlinux.org/packages/?name=binutils) provee una *"colección de herramientas de programación para la manipulación de código objeto en varios formatos de archivo"*[[2]](http://en.wikipedia.org/wiki/GNU_Binutils).

**shell:** [Bash](/index.php/Bash "Bash"), otra aplicación basada en GNU [[3]](http://www.gnu.org/software/bash/), es el shell por defecto.

**utilidades esenciales:** El paquete [coreutils](https://www.archlinux.org/packages/?name=coreutils) contiene *"las utilidades básicas para manejo de archivos, shell y manipulación de texto"*[[4]](http://www.gnu.org/software/coreutils/).

**compresión:** [gzip](https://www.archlinux.org/packages/?name=gzip) y [Tar](/index.php/Tar "Tar") manejan muchos paquetes para sistemas GNU/Linux. Por ejemplo, los paquetes del [Repositorio de Usuarios de Arch](/index.php/Arch_User_Repository "Arch User Repository") vienen en formato [Gzip](http://www.gnu.org/software/gzip/) [tarballs](http://www.gnu.org/software/tar/).

## Herramientas de Desarrollo

Aunque no es necesario, los usuarios tiene la opción de instalar el grupo [base-devel](https://www.archlinux.org/groups/i686/base-devel/) en el cual se encuentran algunas herramientas de desarrollo. Este grupo es un requerimiento para construir paquetes del [Repositorio de usuarios de Arch](/index.php/Arch_User_Repository "Arch User Repository").

Dentro del grupo **base-devel** hay muchos miembros de [GNU toolchain](https://en.wikipedia.org/wiki/GNU_toolchain "wikipedia:GNU toolchain"), los cuales son un *"una serie de proyectos que contienen las herramientas de programación producidas por el proyecto GNU. Estos proyectos forman un sistema integrado que es usado para programar tanto aplicaciones como sistemas operativos."*. Proyectos que son incluidos en el GNU toolchain:

**compilación y construcción:** [make](https://www.archlinux.org/packages/?name=make)

**colección de compiladores:** [gcc](https://www.archlinux.org/packages/?name=gcc)

**enlazador, ensamblador y otras herramientas:** [binutils](https://www.archlinux.org/packages/?name=binutils)

**generador de analizadores sintácticos:** [bison](https://www.archlinux.org/packages/?name=bison)

**procesador de macros:** [m4](https://www.archlinux.org/packages/?name=m4)

[GNU Build System](https://en.wikipedia.org/wiki/GNU_build_system "wikipedia:GNU build system") (también conocido como autotools):

	**configuración automática del código fuente:** [autoconf](https://www.archlinux.org/packages/?name=autoconf)

	**creación automática de archivos Makefile:** [automake](https://www.archlinux.org/packages/?name=automake)

	**librería de scripts de soporte:** [libtool](https://www.archlinux.org/packages/?name=libtool)

## Otras Herramientas

Muchas otras herramientas opcionales GNU se encuentran disponibles en los [repositorios oficiales](/index.php/Official_repositories "Official repositories"):

**widget toolkit:** [GTK+](/index.php/GTK%2B "GTK+")

**ambiente de escritorio:** [GNOME](/index.php/GNOME "GNOME")

**reproductor flash:** [gnash](https://aur.archlinux.org/packages/gnash/)

**hoja de cálculo:** [Gnumeric](/index.php/Gnumeric "Gnumeric")

**editor de imágenes:** [GIMP](/index.php/Multimedia#GIMP "Multimedia")

**administrador de ventanas a pantalla completa:** [GNU Screen](/index.php/GNU_Screen "GNU Screen")

## Enlaces

Para una lista de todos los proyectos actuales GNU, mire [todos los paquetes de GNU](http://www.gnu.org/software/software.html#allgnupkgs)