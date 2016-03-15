El Proyecto Arch Hurd es, como cabía esperar, un proyecto para conseguir un sistema Arch corriendo bajo GNU/Hurd. Esta página, en algún momento, te dirá cómo podrás obtener un sistema Arch Hurd.

Por ahora no hay casi nada hecho, sino una idea, algunas personas lo suficientemente locas a las que le gusta esta idea, y la promesa de algunos PKGBUILDs y un compilador cruzado. Pedimos disculpas por ello :).

## Contents

*   [1 Etapa 1 - Compilador cruzado](#Etapa_1_-_Compilador_cruzado)
*   [2 Etapa 2 - Compilar un sistema de arranque](#Etapa_2_-_Compilar_un_sistema_de_arranque)
*   [3 Etapa 3 - Crear paquetes de forma nativa](#Etapa_3_-_Crear_paquetes_de_forma_nativa)
*   [4 Ideas](#Ideas)
*   [5 Repositorios](#Repositorios)
*   [6 Enlaces](#Enlaces)

## Etapa 1 - Compilador cruzado

Siendo consecuente con Arch, la arquitectura para la que será construído será i686-pc-gnu. Las fuentes de los componentes Hurd se pueden obtener de su repositorio [git](http://git.savannah.gnu.org/cgit/hurd/).

Orden de construcción (desde [aquí](http://nic-nac-project.de/~schwinge/tmp/cross-gnu)):

*   binutils
*   gcc (pasada 1)
*   mach
*   mig
*   hurd
*   glibc (pasada 1)
*   libpthread
*   gcc (pasada 2)
*   glibc (pasada 2)

Un script para generar un entorno de compilación cruzada está disponible [aquí](http://allanmcrae.com/scripts/crosshurd.sh). Actualmente el script usa binutils-2.19.1, gcc-4.1.2, glibc-2.7 y está construído para i586-pc-gnu.

Nuevos y actualizados scripts están disponibles [aquí](http://allanmcrae.com/hurd/).

## Etapa 2 - Compilar un sistema de arranque

Un sistema de arranque mínimo GNU requiere (al menos) los siguientes paquetes construídos en este orden...

*   gnumach-headers (construído anteriormente)
*   hurd-headers (construído anteriormente)
*   libpthreads (construído anteriormente)
*   glibc (construído anteriormente)
*   gnumach
*   hurd
*   coreutils
*   bash
*   (grub)

## Etapa 3 - Crear paquetes de forma nativa

*   conseguir que makepkg/pacman trabajen
*   construír paquetes
*   hacer instalación desde un CD
*   fiesta!

## Ideas

¿Qué hace que sea algo parecido a Arch? Añade ideas a esta lista.

*   pacman/makepkg para mantenimiento de paquetes
*   Algo similar al árbol ABS (en git/svn/cvs/cualquier-cosa tal vez para permitir fáciles restauraciones)
*   Algo como el archivo /etc/rc.conf (¿Alguien sabe algo sobre el proceso de arranque de Hurd?)
*   optimización - construír para i686.
*   mkinitcpio

## Repositorios

Yo (Barrucadu) tengo una tonelada de espacio libre/ancho de banda en mi cuenta Dreamhost, así que cuando esto vaya avanzando, si las personas quieren contrubuír voluntariamente a mantener los paquetes que usen, los repositorios pueden alojarse ahí.

Si puedo configurar un repositorio git para el árbol ABS, una lista de correo, y repositorios (core/extra se deben hacer al principio, imagino), podría dar acceso a los voluntarios para que pudiéramos avanzar.

## Enlaces

[Web oficial del proyecto Arch Hurd](http://www.archhurd.org/)

[Hilo en el foro](https://bbs.archlinux.org/viewtopic.php?pid=682472)

[Página principal del proyecto Hurd, contiene informació útil y enlaces](http://www.gnu.org/software/hurd/)

[Debian GNU/Hurd](http://www.debian.org/ports/hurd/)

[Cross Linux From Scratch](http://trac.cross-lfs.org/)

[Hurd From Scratch - Non-English](http://fondriest.frederic.free.fr/hurd/GNU_HURD%20from%20scratch.html)