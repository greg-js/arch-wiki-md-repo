[Emacs](https://en.wikipedia.org/wiki/Emacs "wikipedia:Emacs") es un editor de texto en tiempo real extensible, configurable y auto-documentado. En el corazón de Emacs yace un intérprete de [Emacs Lisp](https://en.wikipedia.org/wiki/Emacs_Lisp "wikipedia:Emacs Lisp"), el lenguaje de programación en que el mayoría de la funcionalidad y extensiones de Emacs están implementadas. GTK es el conjunto de herramientas de X usado en GNU Emacs 22, aunque funciona igualmente bien en una interfaz de línea de comandos (CLI). Las capacidades de edición de texto de Emacs son a menudo comparadas con aquellas de [vim](/index.php/Vim_(Espa%C3%B1ol) "Vim (Español)").

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Ejecutando Emacs](#Ejecutando_Emacs)
    *   [2.1 Modo normal](#Modo_normal)
    *   [2.2 Sin colores](#Sin_colores)

## Instalación

Existen varias variantes de Emacs (a menudo llamadas *emacsen*). La más común de ellas es [GNU Emacs](http://www.gnu.org/software/emacs/).

Se puede [instalar](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [emacs](https://www.archlinux.org/packages/?name=emacs) a través de los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Si usted suele trabajar en una terminal, puede que prefiera la variante [emacs-nox](https://www.archlinux.org/packages/?name=emacs-nox) sin GTK+ (desprovista de sonido y otras características). Téngase en cuenta que ésta versión tiene algunos inconvenientes: soporta menos colores y menos características para el manejo de fuentes (cambio de tamaño en vivo, varios tamaños en un mismo documento, etc.). Además, *emacs-nox* tiene algunas limitaciones con características avanzadas como la Speedbar o el entorno de depuración (GUD), y es un tanto lento al manejar *faces* complejas (una "*face*" es la apariencia visual de un texto en Emacs).

Si desea disfrutar de todas las características extendidas de Emacs sin la necesidad de instalar una abrumadora cantidad de dependencias, puede usar el PKGBUILD para personalizar sus necesidades. Usando tan solo `gtk3` puede usted deshacerse de gconf. El soporte para imagen y sonido también puede ser desactivado. Ejecute `./configure --help` en la carpeta del código fuente de Emacs para obtener una lista de todas las opciones disponibles.

 `PKGBUILD` 
```
# ...
  ./configure --prefix=/usr --sysconfdir=/etc --libexecdir=/usr/lib \
    --localstatedir=/var --with-x-toolkit=gtk2 --with-xft \
    --without-gconf --without-sound
# ...

```

Otra variante común es [xemacs](https://www.archlinux.org/packages/?name=xemacs).

## Ejecutando Emacs

Antes de abrir Emacs ha de saber como cerrarlo (especialmente si se está ejecutando desde una terminal): Para cerrar Emacs use la secuencia `Ctrl+x``Ctrl+c`.

### Modo normal

Para iniciar Emacs ejecute:

```
$ emacs

```

o si desea usarlo desde la consola:

```
$ emacs -nw

```

o para una carga rápida (sin utilizar al archivo de inicialización *.emacs* ni cargar la pantalla ni la página de presentacion) y editar usando la línea de comandos:

```
$ emacs -Q -nw

```

Si ha instalado la versón nox, entonces 'emacs' y 'emacs -nw' son lo mismo.

Se puede proporcionar un nombre de archivo para abrir dicho archivo inmediatamente:

```
$ emacs archivo.txt

```

### Sin colores

Por defecto, Emacs se inicia con un tema de color mostrando hipervínculos en azul oscuro. Para iniciar Emacs sin ningún tema de color ejecute:

```
$ emacs -nw --color=no

```

Esto hará que los textos aparezcan únicamente en color blanco.