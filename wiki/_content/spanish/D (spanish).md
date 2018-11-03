De [Wikipedia: D (lenguaje de programación)](https://en.wikipedia.org/wiki/es:D_(lenguaje_de_programaci%C3%B3n) "wikipedia:es:D (lenguaje de programación)")

	"D es un lenguaje de programación de propósito general desarrollado por Walter Bright cuya primera versión apareció en 1999\. Se origina como un rediseño de C++, con un enfoque más pragmático, pero no es un lenguaje puramente derivado del anterior. D ha mantenido algunas características de C++ y también está influido por otros conceptos de otros lenguajes como Java, C# y Eiffel. Una versión estable fue lanzada el 2 de enero de 2007.".

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Probando la instalación](#Probando_la_instalaci.C3.B3n)
*   [3 Consideraciones](#Consideraciones)
*   [4 Librerías y enlaces útiles](#Librer.C3.ADas_y_enlaces_.C3.BAtiles)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

Para programar en D necesita dos cosas: un compilador de D y una librería. La forma más sencilla de comenzar rápidamente es instalar el grupo de paquetes [dlang-dmd](https://www.archlinux.org/groups/x86_64/dlang-dmd/). Proporcionará el compilador oficial ([dmd](https://www.archlinux.org/packages/?name=dmd)), la librería estándar [libphobos](https://www.archlinux.org/packages/?name=libphobos) y [dtools](https://www.archlinux.org/packages/?name=dtools), una colección de pequeñas herramientas de desarrollo.

## Probando la instalación

Para asegurarse de que todo está instalado y configurado correctamente, un simple Hello World debería ser suficiente.

```
import std.stdio;

void main() {
   string yourName = "archer";
   writefln("Hello %s!", yourName);
}

```

Pegue el código en un archivo, llámelo "hello.d" (sin comillas) y ejecute

```
$ dmd hello.d

```

en el mismo directorio que el archivo. Entonces debería poder ejecutar el programa con:

```
$ ./hello

```

También puede ejecutar

```
$ dmd -run hello.d

```

que simplemente compilará y ejecutará sin dejar ningún archivo de objeto en el directorio.

## Consideraciones

Sin embargo, hay distintas opciones posibles con respecto al compilador que elija. El estándar (primera referencia) es dmd, pero [gdc](https://www.archlinux.org/packages/?name=gdc) (Compilador GNU D) y [ldc](https://www.archlinux.org/packages/?name=ldc) (Compilador LLVM D) también son populares. Estos también están en [community].

A partir de abril de 2017 [el backend de dmd ahora es FOSS](https://github.com/dlang/dmd/pull/6680) (Boost-licensed). Los 3 compiladores comparten el mismo código de front-end y, por lo tanto, tienen soporte casi idéntico para las características del lenguaje (asumiendo la misma versión de front-end).

## Librerías y enlaces útiles

*   [DDT](https://code.google.com/p/ddt/) - Complemento "Eclipse" para la gestión de proyectos y código en D
*   [Mono-D](http://mono-d.alexanderbothe.com/) - [MonoDevelop](http://monodevelop.com/) complemento para la programación en D
*   [QtD](https://bitbucket.org/qtd/repo) - enlaces Qt para D
*   [GtkD](http://gtkd.org/) - Un wrapper GTK + orientado a objetos para D
*   [Derelict](https://github.com/aldacron/Derelict3) - Enlaces para librerías multimedia, enfocadas hacia el desarrollo de juegos
*   [Deimos](https://github.com/D-Programming-Deimos) - Proyecto que alberga muchos enlaces a diferentes librerías de C

## Véase también

*   [Phobos GitHub repository](https://github.com/D-Programming-Language/phobos/)
*   [The D Programming Language](http://dlang.org/) - Página web oficial de D
*   [Planet D](http://planet.dsource.org/) - Una colección de blogs sobre D