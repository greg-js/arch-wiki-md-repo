Las **páginas man** (abreviatura de "páginas del manual") son una extensa documentación que viene preinstalada en casi todos los sistemas operativos derivados de UNIX más importantes incluyendo Arch Linux. El comando para mostrarlas es `man`.

Contrario a su ámbito, las páginas del manual están diseñadas para ser documentos autocontenidos, limitándose consecuentemente a enlazar a otras páginas del manual cuando se discuten temas relacionados. Esto contrasta bastante con los archivos info con conocimiento de hipervínculos, el intento de GNU para remplazar el formato tradicional de las páginas del manual.

## Contents

*   [1 Acceder a las páginas del manual](#Acceder_a_las_p.C3.A1ginas_del_manual)
*   [2 Formato](#Formato)
*   [3 Buscando manuales](#Buscando_manuales)
*   [4 Páginas del manual coloreadas](#P.C3.A1ginas_del_manual_coloreadas)
    *   [4.1 Usando less (Recomendado)](#Usando_less_.28Recomendado.29)
    *   [4.2 Usando most (No recomendado)](#Usando_most_.28No_recomendado.29)
    *   [4.3 Páginas del manual a color en xterm o rxvt-unicode](#P.C3.A1ginas_del_manual_a_color_en_xterm_o_rxvt-unicode)
        *   [4.3.1 xterm](#xterm)
        *   [4.3.2 rxvt-unicode](#rxvt-unicode)
*   [5 Leyendo páginas del manual locales](#Leyendo_p.C3.A1ginas_del_manual_locales)
    *   [5.1 Convertir a HTML legible por el navegador](#Convertir_a_HTML_legible_por_el_navegador)
        *   [5.1.1 mandoc](#mandoc)
        *   [5.1.2 man2html](#man2html)
        *   [5.1.3 man -H](#man_-H)
        *   [5.1.4 roffit](#roffit)
    *   [5.2 Convertir a PDF](#Convertir_a_PDF)
*   [6 Páginas del manual online](#P.C3.A1ginas_del_manual_online)
*   [7 Páginas del manual de especial interés](#P.C3.A1ginas_del_manual_de_especial_inter.C3.A9s)
*   [8 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Acceder a las páginas del manual

Para leer una página de manual, introduzca:

```
$ man *nombre_de_página*

```

Los manuales se ordenan en varias secciones:

1.  Comandos generales
2.  Llamadas al sistema (funciones proveídas por el kernel)
3.  Llamadas a librerías (funciones de la librería de C)
4.  Ficheros especiales (normalmente se encuentran /dev) y controladores
5.  Formatos de archivos y convenciones
6.  Juegos
7.  Miscelánea (incluye convenciones)
8.  Comandos de administración de sistemas (normalmente requiere privilegios de superusuario) y demonios

Generalmente, para indicar las páginas del manual se suelen usar el nombre seguido del número entre paréntesis de la sección a la que pertenece. A menudo , existen múltiples páginas del manual con el mismo nombre, como man(1) y man(7). En este caso, pásele a man como argumentos el número de página seguido del nombre, por ejemplo:

```
$ man 5 passwd

```

para leer la página del manual sobre `/etc/passwd`, en vez de la página sobre el propio comando `passwd`.

Descripciones de una línea de las páginas del manual pueden mostrarse usando el comando `whatis`. Por ejemplo, para una breve descripción de las páginas de secciones del manual sobre `ls`, escriba:

 `$ whatis ls` 
```
ls (1p)              - lista el contenido de directorios
ls (1)               - lista el contenido de directorios
```

## Formato

Todas las páginas del manual siguen un formato prácticamente estándar, lo que ayude a navegar por ellas. Algunas secciones que suelen estar presentes son:

*   NAME - El nombre del comando y una frase de una línea que enuncie su propósito.
*   SYNOPSIS - Una lista de las opciones y argumentos que toman el comando o los parámetros que la función toma y su fichero de cabecera.
*   DESCRIPTION - Una descripción más detallada del propósito y mecanismos del comando o función.
*   EXAMPLES - Ejemplos comunes, generalmente del más simple al más complejo.
*   OPTIONS - Descripciones de cada una de las opciones que toma el comando y que hacen.
*   EXIT STATUS - El significado de los distintos códigos de salida.
*   FILES - Fichero relacionados con el comando o función.
*   BUGS - Problemas que el comando o función que están pendientes de ser subsanados. También conocido como KNOWN BUGS.
*   SEE ALSO - Una lista de comandos o funciones relacionadas.
*   AUTHOR, HISTORY, COPYRIGHT, LICENSE, WARRANTY - Información sobre el programa, su pasado, sus términos de uso, y su creador.

**Nota:** He dejado a propósito los nombres de las secciones en inglés porque no existe un paquete en los repositorios oficiales **actualizado** con la traducción al español. Creo que, de esta manera, será más fácil hacer indicaciones usando los nombres de las distintas secciones.

## Buscando manuales

Aunque el comando `man` permite a los usuarios mostrar las páginas del manual, surge un problema que es cuando uno no se sabe en primera instancia el nombre exacto de la página del manual. Afortunadamente, los parámetros `-k` o `--apropos` pueden usarse para buscar en las descripciones de las páginas del manual por apariciones de una palabra clave dada.

La característica de búsqueda es proporcionada por una caché dedicada. Por defecto puede no tener ninguna cache creada y todas sus búsquedas generarán el resultado *nada apropiado*. Puede generar o actualizar la cache ejecutando

```
# mandb

```

Es recomendable ejecutarlo cada vez que se instala una nueva página del manual.

Ahora puede iniciar su búsqueda. Por ejemplo, para buscar páginas del manual relacionadas con "password":

```
$ man -k password

```

o:

```
$ man --apropos password

```

Esto es equivalente a llamar al comando `apropos`:

```
$ apropos password

```

La palabra clave suministrada es interpretada como una expresión regular por defecto.

Si quiere hacer una búsqueda en profundidad mediante coincidencia de las palabras clave a lo largo de los artículos, puede usar la opción `-K`:

```
$ man -K password

```

## Páginas del manual coloreadas

Las páginas del manual a color permiten una presentación más clara y una lectura del contenido más fácil. Existen dos métodos predominantes para conseguir páginas del manual en color: usando `less`, u optar por `most`.

### Usando less (Recomendado)

	<small>*Fuente: [Colores de less para páginas del manual | Linux Tidbits](http://linuxtidbits.wordpress.com/2009/03/23/less-colors-for-man-pages/)*</small>

Este método tiene la ventaja que `less` tiene un conjunto de características mas grande que `most`, y es el usado por defecto para visualizar las páginas del manual.

Añada lo siguiente a su archivo de configuración del intérprete de órdenes. Para [Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)") sería:

 `~/.bashrc` 
```
man() {
    env LESS_TERMCAP_mb=$'\E[01;31m' \
    LESS_TERMCAP_md=$'\E[01;38;5;74m' \
    LESS_TERMCAP_me=$'\E[0m' \
    LESS_TERMCAP_se=$'\E[0m' \
    LESS_TERMCAP_so=$'\E[38;5;246m' \
    LESS_TERMCAP_ue=$'\E[0m' \
    LESS_TERMCAP_us=$'\E[04;38;5;146m' \
    man "$@"
}

```

Para ver los cambios en las páginas del manual (sin reiniciar bash o linux), puede ejecutar:

```
# source ~/.bashrc

```

Para [Fish](/index.php?title=Fish_(Espa%C3%B1ol)&action=edit&redlink=1 "Fish (Español) (page does not exist)") un fichero de configuración sería:

 `~/.config/fish/config.fish` 
```
set -xU LESS_TERMCAP_mb (printf "\e[01;31m")      # iniciar parpadeo
set -xU LESS_TERMCAP_md (printf "\e[01;31m")      # iniciar negrita
set -xU LESS_TERMCAP_me (printf "\e[0m")          # finalizar modo
set -xU LESS_TERMCAP_se (printf "\e[0m")          # finalizar modo resaltado
set -xU LESS_TERMCAP_so (printf "\e[01;44;33m")   # iniciar modo resaltado - caja de información
set -xU LESS_TERMCAP_ue (printf "\e[0m")          # finalizar subrayado
set -xU LESS_TERMCAP_us (printf "\e[01;32m")      # comenzar subrayado

```

Para ver los cambios en las páginas del manual (sin reiniciar fish o linux), puede ejecutar:

```
# source ~/.config/fish/config.fish

```

Para personalizar los colores, vea [Código escape ANSI](https://en.wikipedia.org/wiki/es:C%C3%B3digo_escape_ANSI "wikipedia:es:Código escape ANSI") para más referencias.

### Usando most (No recomendado)

La función básica de 'most' es similar a `less` y `more`, pero tiene un conjunto de características más pequeño. Configurando most para usar colores es más fácil que usar less, pero es necesario configuraciones adicionales para hacer que most se comporte como less. Instale [most](https://www.archlinux.org/packages/?name=most) usando [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)"):

```
# pacman -S most

```

Edite `/etc/man_db.conf`, descomente la definición del visualizador(pager) y cámbielo a:

```
DEFINE     pager     most -s

```

Pruebe la nueva configuración con:

```
$ man _cualquier\_página\_del\_manual_

```

Modificar los valores de colores requiere editar `~/.mostrc` (crear el fichero si no está presente) o editar `/etc/most.conf` para cambios de todo el sistema. Ejemplo de `~/.mostrc`:

```
% Configuración de colores
color normal lightgray black
color status yellow blue
color underline yellow black
color overstrike brightblue black

```

Otro ejemplo mostrando atajos de teclado similares a `less` (saltar a línea está configurado con 'J'):

```
% atajos de teclado estilo less
unsetkey "^K"
unsetkey "g"
unsetkey "G"
unsetkey ":"

setkey next_file ":n"
setkey find_file ":e"
setkey next_file ":p"
setkey toggle_options ":o"
setkey toggle_case ":c"
setkey delete_file ":d"
setkey exit ":q"

setkey bob "g"
setkey eob "G"
setkey down "e"
setkey down "E"
setkey down "j"
setkey down "^N"
setkey up "y"
setkey up "^Y"
setkey up "k"
setkey up "^P"
setkey up "^K"
setkey page_down "f"
setkey page_down "^F"
setkey page_up "b"
setkey page_up "^B"
setkey other_window "z"
setkey other_window "w"
setkey search_backward "?"
setkey bob "p"
setkey goto_mark "'"
setkey find_file "E"
setkey edit "v"

```

### Páginas del manual a color en xterm o rxvt-unicode

	<small>*Fuente: [Fichero de recursos XFree para el programa XTerm](http://pub.ligatura.org/fs/xfree86/xresources/xterm)*</small>

Una manera rápida de añadir color a páginas del manual en [xterm](https://www.archlinux.org/packages/?name=xterm)/`uxterm` o [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) es modificar el fichero `~/.Xresources`.

#### xterm

```
*VT100.colorBDMode:     true
*VT100.colorBD:         red
*VT100.colorULMode:     true
*VT100.colorUL:         cyan

```

que *reemplaza* las decoraciones con colores. Añada también:

```
*VT100.veryBoldColors: 6

```

Si quiere colores y decoraciones (negrita o subrayado) *al mismo tiempo*. Vea [xterm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xterm.1) para una descripción del recurso `veryBoldColors`.

#### rxvt-unicode

```
URxvt.colorIT:      #87af5f
URxvt.colorBD:      #d7d7d7
URxvt.colorUL:      #87afd7

```

Ejecute:

```
$ xrdb -load ~/.Xresources

```

Lance una nueva instancia de `xterm/uxterm` o `rxvt-unicode` y debería poder ver las páginas del manual a color. Esta combinación pone colores a palabras en **negrita** y <u>subrayadas</u> en `xterm/uxterm` o texto en **negrita**, <u>subrayado</u>, y en *cursiva* en `rxvt-unicode`. Puede jugar con las diferentes variaciones de estos atributos (vea las [fuentes](http://pub.ligatura.org/fs/xfree86/xresources/xterm) de este item).

## Leyendo páginas del manual locales

En vez de usar la interfaz estándar, usar navegadores como [lynx](https://www.archlinux.org/packages/?name=lynx) y [Firefox](/index.php/Firefox_(Espa%C3%B1ol) "Firefox (Español)") para ver las páginas del manual permite a los usuarios sacarle partido al principal beneficio de las páginas info: el texto con hipervínculos.

Los usuarios de [KDE](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)") pueden leer las páginas del manual en Konqueror con:

```
man:<name>

```

Existen dos alternativas en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"):

1\. [xorg-xman](https://www.archlinux.org/packages/?name=xorg-xman) proporciona una vista categorizada de las páginas del manual en [X](/index.php?title=X_(Espa%C3%B1ol)&action=edit&redlink=1 "X (Español) (page does not exist)").

2\. El navegador de ayuda de [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)") [yelp](https://www.archlinux.org/packages/?name=yelp), es una manera más clara pero tiene algunas dependencias.

### Convertir a HTML legible por el navegador

#### mandoc

Instale [mandoc](https://aur.archlinux.org/packages/mandoc/) desde [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)"). Para convertir una página, por ejemplo `free(1)`:

```
$ gunzip -c /usr/share/man/man1/free.1.gz | mandoc -Thtml -Ostyle=style.css 1> free.html

```

Ahora abra el fichero llamado `free.html` en su navegador favorito.

#### man2html

Primero, instale [man2html](https://www.archlinux.org/packages/?name=man2html) desde los repositorios oficiales.

Ahora, convierta de esta forma una página del manual:

```
$ man free | man2html -compress -cgiurl man$section/$title.$section$subsection.html > ~/man/free.html

```

Otro uso para `man2html` es exportar texto a un formato virgen listo para imprimir:

```
$ man free | man2html -bare > ~/free.txt

```

#### man -H

La implementación GNU de man en los repositorios de Arch también tiene la habilidad de hacer esto mismo por si solo:

```
$ man -H free

```

Esto buscará la [variable de entorno](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") `BROWSER` para determinar que navegador usa por defecto. Puede invalidar este comportamiento pasándole el binario a la opción `-H`.

#### roffit

Primero instale [roffit](https://aur.archlinux.org/packages/roffit/) desde [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

Para convertir una página del manual:

```
$ gunzip -c /usr/share/man/man1/free.1.gz | roffit > free.html

```

### Convertir a PDF

Las páginas del manual siempre han sido imprimibles: están escritas en troff, que esencialmente es un lenguaje de composición tipográfica. Si tiene ghostscript instalado, convertir una página de manual a PDF es realmente sencillo: `man -t <manpage> | ps2pdf - <pdf>`. [Esta búsqueda de imágenes en google](https://www.google.com/search?q=manpage+pdf+troff&num=100&hl=en&prmd=imvns&source=lnms&tbm=isch&sa=X&ei=5BZpUI3oH6rI2AXvx4CoAw&ved=0CAoQ_AUoAQ&biw=1321&bih=1100) debería darle una idea de como queda el resultado; Puede no ser a gusto de todos.

Advertencia: Las fuentes están generalmente limitadas a Times a tamaños prefijados. No tiene hipervínculos. Algunas páginas del manual fueron específicamente diseñadas para verlas en terminal, y por ello no se visualizarán correctamente en PS o en PDF.

El siguiente script en perl convierte las páginas del manual a PDFs, cachea los PDFs en el directorio `$HOME/.manpdf/`, y llama a un visor de PDFs, concretamente [mupdf](https://www.archlinux.org/packages/?name=mupdf).

 `Uso: manpdf [<section>] <manpage>` 
```
#!/usr/bin/perl
use File::stat;

$pdfdir = $ENV{"HOME"}."/.manpdf";
-d $pdfdir || mkdir $pdfdir || die "No se pudo crear $pdfdir";
$manpage = $ARGV[0];
chop($manpath = `man -w $manpage`);
die if $?;

$maninfo = stat($manpath) or die;
$manpath =~ s@.*/man./(.*)(\.(gz|bz2))?$@$1@;
$pdfpath = "$pdfdir/$manpath.pdf";
$pdftime = 0;
if (-f $pdfpath) {
    $pdfinfo = stat($pdfpath) or die;
    $pdftime = $pdfinfo->mtime;
}
if (!-f $pdfpath || $maninfo->mtime > $pdftime) {
    system "man -t $manpage | ps2pdf -dPDFSETTINGS=/screen - $pdfpath";
}
die if !-f $pdfpath;
if (!fork) {
    open(STDOUT, "/dev/null");
    open(STDERR, "/dev/null");
    exec "mupdf", "-r", "96", $pdfpath;
    #exec "acroread", $pdfpath;
}

```

## Páginas del manual online

Existen numerosas bases de datos de páginas de manual online, incluyendo:

*   [Man7.org.](http://man7.org/linux/man-pages/index.html) Versión original para Arch Linux's [man-pages](https://www.archlinux.org/packages/?name=man-pages).
*   [*Debian GNU/Linux man pages*](http://manpages.debian.net/)
*   [*DragonFlyBSD manual pages*](http://leaf.dragonflybsd.org/cgi/web-man)
*   [*FreeBSD Hypertext Man Pages*](http://www.freebsd.org/cgi/man.cgi)
*   [*Linux and Solaris 10 Man Pages*](http://www.manpages.spotlynx.com/)
*   [*Linux/FreeBSD Man Pages*](http://manpagehelp.net) with user comments
*   [*Linux man pages at die.net*](http://linux.die.net/man/)
*   [The Linux man-pages project at kernel.org](http://www.kernel.org/doc/man-pages/)
*   [*NetBSD manual pages*](http://netbsd.gw.com/cgi-bin/man-cgi)
*   [*Mac OS X Manual Pages*](http://developer.apple.com/documentation/Darwin/Reference/ManPages/index.html)
*   [*On-line UNIX manual pages*](http://unixhelp.ed.ac.uk/alphabetical/index.html)
*   [*OpenBSD manual pages*](http://www.openbsd.org/cgi-bin/man.cgi)
*   [*Plan 9 Manual — Volume 1*](http://man.cat-v.org/plan_9/)
*   [*Inferno Manual — Volume 1*](http://man.cat-v.org/inferno/)
*   [*Storage Foundation Man Pages*](http://sfdoccentral.symantec.com/sf/5.0MP3/linux/manpages/index.html)
*   [*The UNIX and Linux Forums Man Page Repository*](http://www.unix.com/man-page/OpenSolaris/1/man/)
*   [*Ubuntu Manpage Repository*](http://manpages.ubuntu.com/)

**Advertencia:** Algunas distribuciones proporcionan páginas de manual parcheadas u obsoletas que difieren de aquellas proporcionadas por Arch. Sea cauto al usar páginas de manual online.

## Páginas del manual de especial interés

A continuación se muestra una lista no exhaustiva de páginas de especial interés que podrían ayudarle a comprender muchas cosas en mayor profundidad. Algunas de ellas podrían servir como buena referencia(como la tabla ascii).

*   ascii(7)
*   boot(7)
*   charsets(7)
*   chmod(1)
*   credentials(7)
*   fstab(5)
*   hier(7)
*   systemd(1)
*   locale(1P)(5)(7)
*   printf(3)
*   proc(5)
*   regex(7)
*   signal(7)
*   term(5)(7)
*   termcap(5)
*   terminfo(5)
*   utf-8(7)

De formas más general, eche un vistazo a las páginas de la categoría 7:

```
$ man -s 7 -k ".*" 

```

Páginas específicas de Arch Linux:

*   archlinux(7)
*   mkinitcpio(8)
*   pacman(8)
*   pacman-key(8)
*   pacman.conf(5)

## Véase también

*   [Recomendaciones generales](/index.php/General_recommendations_(Espa%C3%B1ol) "General recommendations (Español)") - Recomendaciones generales de Arch
*   [man page - Artículo de la wiki de Gentoo](http://wiki.gentoo.org/wiki/Man_page)