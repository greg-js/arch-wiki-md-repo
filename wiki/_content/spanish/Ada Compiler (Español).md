## Contents

*   [1 Construir con éxito un compilador de Ada en Arch](#Construir_con_.C3.A9xito_un_compilador_de_Ada_en_Arch)
    *   [1.1 Introducción](#Introducci.C3.B3n)
    *   [1.2 Obteniendp un compilador binario](#Obteniendp_un_compilador_binario)
    *   [1.3 Actualizando la base de datos abs](#Actualizando_la_base_de_datos_abs)
    *   [1.4 Editando el PKGBUILD](#Editando_el_PKGBUILD)
    *   [1.5 Construyendo el paquete](#Construyendo_el_paquete)
    *   [1.6 Notas adicionales](#Notas_adicionales)
    *   [1.7 Enlaces](#Enlaces)

# Construir con éxito un compilador de Ada en Arch

## Introducción

Lo que fue más molesto para mí en Arch Linux es que debido a mis estudios tenía la absoluta necesidad de tener un compilador operativo en mi computadora, y el descubrimiento de que mi distribución favorita de Linux no me lo proporcionaba.

Desgraciadamente, se necesita un compilador de Ada para construir un compilador de Ada. En est documento, cómo instalar adecuadamente las capacidades Ada en el paquete gcc.

## Obteniendp un compilador binario

Como dije antes, se necesita un compilador de Ada para compilar un compilador de Ada. Por tanto tendrá usted que conseguir uno de una distribución binaria. Le sugiero (y encarecidamente le recomiendo) que use uno de [http://gnuada.sourceforge.net/](http://gnuada.sourceforge.net/). Estos son los únicos que pude lograr que compilaran gcc-ada.

Así que, escoja un RPM para su arquitectura:

Por ejemplo, yo usaré éste: gnat-gcc-4.1.1-r6.FC6.i386.rpm.

Ahora, cree un directorio temporal para la construcción:

```
$ mkdir ~/ADA_BUILD

```

Y extraiga el contenido del RPM a algún directorio (esto requiere rpmextract desde extra):

```
$ cd ~/ADA_BUILD
$ mkdir RPM
$ cd RPM
$ rpmextract.sh /<path to>/gnat-gcc-4.1.1-r6.FC6.i386.rpm

```

Ahora tiene una instalación completa de gcc en ~/ADA_BUILD/RPM.

## Actualizando la base de datos abs

Ejecute, como root:

```
$ mkdir -p /var/abs #no necesita esto si ya lo ejecuto antes
$ abs

```

y copie el PKGBUILD de gcc y los archivos a su directorio temporal:

```
$ cd ~/ADA_BUILD
$ cp -rv /var/abs/core/devel/gcc .

```

## Editando el PKGBUILD

```
$ cd ~/ADA_BUILD/gcc

```

Ahora tendrá que modificar el PKGBUILD para añadir el lenguaje Ada a su compilación. Editelo de esta manera:

*   En el array sources, reemplace:

```
[ftp://gcc.gnu.org/pub/gcc/releases/gcc-${pkgver}/gcc-{core,g++,objc}-${pkgver}.tar.bz2](ftp://gcc.gnu.org/pub/gcc/releases/gcc-${pkgver}/gcc-{core,g++,objc}-${pkgver}.tar.bz2)

```

con

```
[ftp://gcc.gnu.org/pub/gcc/releases/gcc-${pkgver}/gcc-{core,g++,objc](ftp://gcc.gnu.org/pub/gcc/releases/gcc-${pkgver}/gcc-{core,g++,objc),**ada**}-${pkgver}.tar.bz2

```

*   Elimine todo desde "md5sums=(" hasta el próximo paréntesis derecho.

*   Ahora encuentre la línea de ./configure

y añada ada a --enable-languages=...

```
../gcc-${pkgver}/configure --prefix=/usr --enable-shared \
--enable-languages=c,c++,objc,**ada** --enable-threads=posix \

```

## Construyendo el paquete

```
$ cd ~/ADA_BUILD/gcc

```

Limpie completamente el directorio si es necesario.

```
$ rm -r pkg/ src/ *.pkg.tar.gz

```

Tiene que configurar su entorno de manera que se utilice la cadena de herramientas de Ada en vez de la que ya está instalada en sus sistema.

```
$ export PATH="~/ADA_BUILD/RPM/usr/bin:$PATH"

```

Compruebe que su sistema utiliza ahora el compilador gcc correcto.

```
$ which gcc

```

Esto debería de apuntar al gcc que desempaquetó del RPM. Si esto es correcto, entonces está listo para comenzar.

```
$ makepkg

```

Esto llevará un tiempo. Cuando esté construido, actualicelo como root:

```
$ pacman -U gcc-*.pkg.tar.gz

```

Ahora puede probar su compilador Ada con la orden gnatmake:

```
$ gnatmake helloworld.adb

```

## Notas adicionales

Una vez tenga su compilador Ada cargado y corriendo, no necesitará hacer esto una y otra vez. Cuando un nuevo gcc sea publicado, NO actualice o sobreescribirá el anterior. En vez de eso, consiga el PKGBUILD más reciente de abs, haga las modificaciones oportunas, y recompile.

## Enlaces

[http://gnuada.sourceforge.net](http://gnuada.sourceforge.net)