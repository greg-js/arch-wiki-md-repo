**Estado de la traducción**
Este artículo es una traducción de [Clang](/index.php/Clang "Clang"), revisada por última vez el **2018-10-27**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Clang&diff=0&oldid=551753) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Clang](http://clang.llvm.org/) es un compilador de [C](/index.php/C_(Espa%C3%B1ol) "C (Español)")/C ++/Objective C/[CUDA](/index.php/CUDA "CUDA") basado en [LLVM](/index.php/LLVM "LLVM"). Se distribuye bajo la Licencia BSD.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Construir paquetes con Clang](#Construir_paquetes_con_Clang)
*   [3 Usar el Analizador Estático](#Usar_el_Analizador_Est.C3.A1tico)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [clang](https://www.archlinux.org/packages/?name=clang).

## Construir paquetes con Clang

Agregue `export CC=clang` y (para C ++) `export CXX=clang++` a su `/etc/makepkg.conf`. Si está compilando con `debug`, elimine también `-fvar-tracking-assignments` de `DEBUG_CFLAGS` y `DEBUG_CXXFLAGS` ya que clang no lo admite.

Nota: Para los paquetes que especifican opciones de compilación específicas de GCC, puede haber errores de compilación que requieran editar el paquete fuente, el pkgbuild o descomentar las líneas de clang en makepkg.conf.

## Usar el Analizador Estático

Para analizar un proyecto, simplemente coloque la palabra `scan-build` delante de su comando de compilación. Por ejemplo:

```
$ scan-build make

```

**Tip:** Si su proyecto ya está compilado, `scan-build` no se reconstruirá y tampoco lo analizará. Para forzar la recompilación y el análisis, use el interruptor `-B`: `$ scan-build make -B` 

También es posible analizar archivos específicos:

```
$ scan-build gcc -c t1.c t2.c

```

## Véase también

*   [Wikipedia: Clang](https://es.wikipedia.org/wiki/Clang)
*   [scan-build: ejecutar el analizador desde la línea de comandos](http://clang-analyzer.llvm.org/scan-build.html)
*   [Compilar CUDA con clang](http://llvm.org/docs/CompileCudaWithLLVM.html)