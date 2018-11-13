**Estado de la traducción**
Este artículo es una traducción de [Bioperl](/index.php/Bioperl "Bioperl"), revisada por última vez el **2018-10-30**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Bioperl&diff=0&oldid=552022) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Bioperl](http://bioperl.org/) es un conjunto de scripts en el lenguaje de programación Perl para ayudar a investigadores en la [Biología Computacional](https://en.wikipedia.org/wiki/es:Biolog%C3%ADa_computacional "wikipedia:es:Biología computacional") y la [Bioinformática](https://en.wikipedia.org/wiki/es:Bioinform%C3%A1tica "wikipedia:es:Bioinformática").

## Contents

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
*   [3 Extras](#Extras)
*   [4 Solución de problemas](#Solución_de_problemas)
*   [5 Véase también](#Véase_también)

## Instalación

Instale [bioperl-live-git](https://aur.archlinux.org/packages/bioperl-live-git/) desde [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

## Configuración

Si instaló desde AUR a la ruta `/usr` (por defecto), la ruta a bioperl debe agregarse a la matriz @INC de perl. Esto se hace fácilmente editando la variable PERL5LIB en su archivo .bashrc, de la siguiente manera:

```
$ nano ~/.bashrc

```

Y luego agregar esta línea al final del archivo:

```
export PERL5LIB=$PERL5LIB:/usr/share/perl5/site_perl/5.10.0

```

Nota: consulte la carpeta `/usr/share/perl5/site_perl/` para ver si la versión es la misma, la carpeta 5.10.0 (o una versión más reciente) debe contener una carpeta llamada BIO. Si no se encuentra ninguna 5.10.0 ni ninguna otra versión, busque la carpeta Bio en `vendor_perl` o cualquier otra carpeta perl5 donde se haya instalado la carpeta Bio, agregue la ruta donde está la carpeta Bio al archivo bash.

Después de guardar el archivo, para actualizar la variable `$PERL5LIB`, bash debe volver a cargarse en el terminal:

```
$ bash

```

Se recomienda instalar módulos adicionales CPAN, para evitar errores de dependencias.

*   Actualizar CPAN

```
# perl -MCPAN -e shell
install Bundle::CPAN
q

```

*   Instale/actualice Module::Compile, y conviértalo en su instalador preferido

```
# cpan
install Module::Build
o conf prefer_installer MB
o conf commit
q

```

## Extras

El paquete Bioperl-run, que proporciona módulos wrapper alrededor de muchas aplicaciones bioinformáticas y herramientas comunes, no se instala de manera predeterminada.

```
# cpan
d /bioperl/

```

Lo que devolvería algo así:

```
Distribution    BIRNEY/bioperl-1.2.2.tar.gz
Distribution    BIRNEY/bioperl-1.2.3.tar.gz
Distribution    BIRNEY/bioperl-1.2.tar.gz
Distribution    BIRNEY/bioperl-1.4.tar.gz
Distribution    BIRNEY/bioperl-db-0.1.tar.gz
Distribution    BIRNEY/bioperl-ext-1.4.tar.gz
Distribution    BIRNEY/bioperl-gui-0.7.tar.gz
Distribution    BIRNEY/bioperl-run-1.4.tar.gz
Distribution    BOZO/Fry-Lib-BioPerl-0.15.tar.gz
Distribution    CJFIELDS/BioPerl-1.6.0.tar.gz
Distribution    CJFIELDS/BioPerl-1.6.1.tar.gz
Distribution    CJFIELDS/BioPerl-db-1.6.0.tar.gz
Distribution    CJFIELDS/BioPerl-network-1.6.0.tar.gz
Distribution    CJFIELDS/BioPerl-run-1.6.1.tar.gz
Distribution    CRAFFI/Bundle-BioPerl-2.1.8.tar.gz
15 items found

```

Entonces simplemente haga (verifique la compatibilidad de la versión):

```
install CJFIELDS/BioPerl-run-1.6.1.tar.gz
q

```

## Solución de problemas

Si tiene problemas al compilar sus scripts perl, con un error como `Can't locate (Nombre del módulo) in @INC`, instale los módulos faltantes como se describe a continuación:

```
# cpan
install Module::Name
q

```

## Véase también

*   [http://bioperl.org/INSTALL.html](http://bioperl.org/INSTALL.html)