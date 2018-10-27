**Estado de la traducción**
Este artículo es una traducción de [Core utilities](/index.php/Core_utilities "Core utilities"), revisada por última vez el **2018-10-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Core_utilities&diff=0&oldid=549217) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Command-line shell](/index.php/Command-line_shell "Command-line shell")
*   [Usuarios y grupos](/index.php/Users_and_groups_(Espa%C3%B1ol) "Users and groups (Español)")
*   [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)")
*   [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")
*   [Recomendaciones generales](/index.php/General_recommendations_(Espa%C3%B1ol) "General recommendations (Español)")

Las *utilidades principales* son las herramientas básicas y fundamentales de un sistema [GNU](/index.php/GNU_(Espa%C3%B1ol) "GNU (Español)")/[Linux](/index.php/Linux_(Espa%C3%B1ol) "Linux (Español)"). En Arch Linux se encuentran en el [grupo base](/index.php/Base_group "Base group"). Este artículo proporciona una visión general e incompleta de ellos, vincula su documentación y describe alternativas útiles. El alcance de este artículo incluye, pero no se limita, a [GNU coreutils](https://www.gnu.org/software/coreutils/coreutils.html). La mayoría de los servicios básicos son herramientas tradicionales [Unix](https://en.wikipedia.org/wiki/es:Unix "wikipedia:es:Unix") (véase [Heirloom](/index.php/Heirloom "Heirloom")) y muchos fueron estandarizados por [POSIX](https://en.wikipedia.org/wiki/es:POSIX "wikipedia:es:POSIX") pero se han seguido desarrollado para proporcionar más funciones.

La mayoría de las interfaces de línea de comandos están documentadas en las [páginas del manual](/index.php/Man_page_(Espa%C3%B1ol) "Man page (Español)"), las utilidades del [Proyecto GNU](/index.php/GNU_Project_(Espa%C3%B1ol) "GNU Project (Español)") están documentadas en los [manuales de información](/index.php/Info_manual_(Espa%C3%B1ol) "Info manual (Español)"), algunos [intérpretes de comandos](/index.php/Shell "Shell") proporcionan un comando `help` para los comandos incorporados de la [línea de comandos](/index.php/Shell "Shell"). Además, la mayoría de los comandos imprimen su uso cuando se ejecutan con el indicador `--help`.

## Contents

*   [1 Esenciales](#Esenciales)
    *   [1.1 Previniendo la pérdida de datos](#Previniendo_la_p.C3.A9rdida_de_datos)
*   [2 No esenciales](#No_esenciales)
*   [3 Alternativas](#Alternativas)
    *   [3.1 Alternativas a find](#Alternativas_a_find)
    *   [3.2 Alternativas a diff](#Alternativas_a_diff)
    *   [3.3 Alternativas a grep](#Alternativas_a_grep)
        *   [3.3.1 Buscadores de código](#Buscadores_de_c.C3.B3digo)
        *   [3.3.2 Filtros interactivos](#Filtros_interactivos)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Esenciales

La siguiente tabla enumera algunos comandos importantes con los que los usuarios de Arch Linux deben estar familiarizados. Véase también [intro(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/intro.1).

| Paquete | Comando | Descripción | Documentación | Alternativas |
| incluído en la línea de comandos | cd | cambia de directorio | [cd(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cd.1p) |
| GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) | ls | lista el directorio | [ls(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ls.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/ls-invocation.html) | [exa](https://www.archlinux.org/packages/?name=exa), [tree](https://www.archlinux.org/packages/?name=tree) |
| cat | concatena archivos a la salida estándar | [cat(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cat.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/cat-invocation.html) | [tac(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tac.1) |
| mkdir | crea un directorio | [mkdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkdir.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/mkdir-invocation.html) |
| rmdir | elimina un directorio vacío | [rmdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rmdir.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/rmdir-invocation.html) |
| rm | elimina archivos o directorios | [rm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rm.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/rm-invocation.html) | [shred](/index.php/Shred "Shred") |
| cp | copia archivos o directorios | [cp(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cp.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/cp-invocation.html) |
| mv | mueve archivos o directorios | [mv(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mv.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/mv-invocation.html) |
| ln | crea enlaces duros o simbólicos | [ln(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ln.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/ln-invocation.html) |
| [chown](/index.php/Chown "Chown") | cambia el usuario y grupo del archivo | [chown(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chown.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/chown-invocation.html) | [chgrp(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chgrp.1) |
| [chmod](/index.php/Chmod "Chmod") | cambia los permisos del archivo | [chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/chmod-invocation.html) |
| [dd](/index.php/Dd "Dd") | convierte y copia un archivo | [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/dd-invocation.html) |
| df | informa del espacio disponible en disco del sistema de archivo | [df(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/df.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/df-invocation.html) |
| GNU [tar](https://www.archlinux.org/packages/?name=tar) | [tar](/index.php/Tar_(Espa%C3%B1ol) "Tar (Español)") | archivador tar | [tar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tar.1), [info](https://www.gnu.org/software/tar/manual/html_chapter/index.html) | [archivadores](/index.php/Archiver_(Espa%C3%B1ol) "Archiver (Español)") |
| GNU [less](https://www.archlinux.org/packages/?name=less) | less | paginador de terminal | [less(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/less.1) | [terminal pagers](/index.php/Terminal_pager "Terminal pager") |
| GNU [findutils](https://www.archlinux.org/packages/?name=findutils) | find | busca archivos o directorios | [find(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/find.1), [info](https://www.gnu.org/software/findutils/manual/html_node/find_html/index.html), [GregsWiki](https://mywiki.wooledge.org/UsingFind "gregswiki:UsingFind") | [#Alternativas a find](#Alternativas_a_find) |
| GNU [diffutils](https://www.archlinux.org/packages/?name=diffutils) | diff | compara archivos línea por línea | [diff(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/diff.1), [info](https://www.gnu.org/software/diffutils/manual/html_node/Invoking-diff.html) | [#Alternativas a diff](#Alternativas_a_diff) |
| GNU [grep](https://www.archlinux.org/packages/?name=grep) | grep | imprime las línea que coinciden con un patrón | [grep(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/grep.1), [info](https://www.gnu.org/software/grep/manual/html_node/index.html) | [#Alternativas a grep](#Alternativas_a_grep) |
| GNU [sed](https://www.archlinux.org/packages/?name=sed) | sed | editor de secuencias (stream editor) | [sed(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sed.1), [info](https://www.gnu.org/software/sed/manual/html_node/index.html), [one-liners](http://sed.sourceforge.net/sed1line.txt) |
| GNU [gawk](https://www.archlinux.org/packages/?name=gawk) | awk | lenguaje de escaneo y procesamiento de patrones | [gawk(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gawk.1), [info](https://www.gnu.org/software/gawk/manual/html_node/index.html) | [nawk](https://www.archlinux.org/packages/?name=nawk), [mawk](https://aur.archlinux.org/packages/mawk/) |
| [util-linux](https://www.archlinux.org/packages/?name=util-linux) | [dmesg](https://en.wikipedia.org/wiki/dmesg |
| [lsblk](/index.php/Lsblk "Lsblk") | lista los dispositivos de bloques | [lsblk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsblk.8) |
| [mount](/index.php/Mount "Mount") | monta un sistema de archivos | [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) |
| [umount](/index.php/Umount "Umount") | desmonta un sistema de archivos | [umount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/umount.8) |
| [su](/index.php/Su_(Espa%C3%B1ol) "Su (Español)") | substitute user | [su(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/su.1) | [sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)") |
| kill | finaliza un proceso | [kill(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/kill.1) | [pkill(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pkill.1), [killall(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/killall.1) |
| [procps-ng](https://www.archlinux.org/packages/?name=procps-ng) | pgrep | buscar procesos por nombre o atributos | [pgrep(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pgrep.1) | [pidof(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pidof.1) |
| ps | muestra información sobre los procesos | [ps(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ps.1) | [top(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/top.1), [htop](https://www.archlinux.org/packages/?name=htop) |
| free | muestra la cantidad de memoria libre y utilizada | [free(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/free.1) |

### Previniendo la pérdida de datos

rm, mv, cp y las redirecciones de la línea de comandos eliminan o sobrescriben archivos sin preguntar. rm, mv y cp son compatibles con el indicador `-i` para avisar al usuario antes de cada eliminación / sobreescritura. A algunos usuarios les gusta habilitar el indicador `-i` de forma predeterminada utilizando [alias](/index.php/Alias_(Espa%C3%B1ol) "Alias (Español)"). Sin embargo, estas configuraciones de la línea de comandos son peligrosas porque te acostumbra a ellas, lo que da como resultado la posible pérdida de datos cuando utiliza otro sistema o usuario que no tiene dicho indicador. La mejor forma de evitar la pérdida de datos es hacer [copias de seguridad](/index.php/Backup "Backup").

## No esenciales

Esta tabla enumera las utilidades principales que a menudo son útiles.

| Paquete | Comando | Descripción | Documentación | Alternativas |
| incluidos en la línea de comandos | alias | define o muestra los alias | [alias(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/alias.1p) |
| type | imprime el tipo de un comando | [type(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/type.1p) | [which(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/which.1) |
| time | temporiza un comando | [time(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/time.1p) |
| GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) | tee | lee de la entrada estándar y escribe en la salida estándar y archivos | [tee(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tee.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/tee-invocation.html) |
| mktemp | crea un archivo o directorio temporal | [mktemp(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mktemp.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/mktemp-invocation.html) |
| cut | imprime partes seleccionadas de líneas | [cut(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cut.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/cut-invocation.html) |
| tr | traduce o elimina caracteres | [tr(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tr.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/tr-invocation.html) |
| od | vuelca archivos en octal y otros formatos | [od(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/od.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/od-invocation.html) | [hexdump(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hexdump.1), [vim](/index.php/Vim "Vim")'s [xxd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xxd.1) |
| sort | ordena lineas | [sort(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sort.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/sort-invocation.html) |
| uniq | informa u omite líneas repetidas | [uniq(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/uniq.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/uniq-invocation.html) |
| comm | compara dos archivos ordenados línea por línea | [comm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/comm.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/comm-invocation.html) |
| head | vuelca la primera parte de los archivos | [head(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/head.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/head-invocation.html) |
| tail | vuelca la última parte de los archivos, o sigue los archivos | [tail(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tail.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/tail-invocation.html) |
| wc | imprime el recuento de líneas nuevas, palabras y bytes | [wc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wc.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/wc-invocation.html) |
| GNU [binutils](https://www.archlinux.org/packages/?name=binutils) | strings | imprime caracteres imprimibles en archivos binarios | [strings(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/strings.1), [info](https://sourceware.org/binutils/docs/binutils/strings.html) |
| GNU [glibc](https://www.archlinux.org/packages/?name=glibc) | iconv | convierte codificaciones de caracteres | [iconv(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iconv.1) | [recode](https://www.archlinux.org/packages/?name=recode) |
| [file](https://www.archlinux.org/packages/?name=file) | file | estima el tipo de archivo | [file(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/file.1) |

El paquete [moreutils](https://www.archlinux.org/packages/?name=moreutils) proporciona herramientas útiles como [sponge(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sponge.1) que no se encuentran en GNU coreutils.

## Alternativas

Las alternativas a las utilidades principales del grupo [base](https://www.archlinux.org/groups/x86_64/base/) son [BusyBox](/index.php/BusyBox "BusyBox"), [Heirloom Toolchest](/index.php/Heirloom "Heirloom"), [9base](https://www.archlinux.org/packages/?name=9base), [sbase-git](https://aur.archlinux.org/packages/sbase-git/) y [ubase-git](https://aur.archlinux.org/packages/ubase-git/).

### Alternativas a find

*   **fd** — Alternativa simple, rápida y sencilla de find. Ignora los archivos ocultos y `.gitignore` por defecto.

	[Https://github.com/sharkdp/fd](Https://github.com/sharkdp/fd) || [fd](https://www.archlinux.org/packages/?name=fd)

*   **fuzzy-find** — Completado difuso para la búsqueda de archivos.

	[Https://github.com/silentbicycle/ff](Https://github.com/silentbicycle/ff) || [ff-git](https://aur.archlinux.org/packages/ff-git/)

*   **[mlocate](/index.php/Mlocate_(Espa%C3%B1ol) "Mlocate (Español)")** — Mezcla las implementaciónes locate/updatedb.

	[Https://pagure.io/mlocate](Https://pagure.io/mlocate) || [mlocate](https://www.archlinux.org/packages/?name=mlocate)

Para buscadores de archivos en modo gráfico, véase [List of applications/Utilities#File searching](/index.php/List_of_applications/Utilities#File_searching "List of applications/Utilities").

### Alternativas a diff

Mientras que [diffutils](https://www.archlinux.org/packages/?name=diffutils) no proporciona una comparación (diff) de palabras, muchos otros programas lo hacen:

*   [git](/index.php/Git_(Espa%C3%B1ol) "Git (Español)") diff puede hacer una comparación de palabras con `--color-words`, utilizando `--no-index` también se puede usar para archivos fuera de la estructura de trabajo de Git.
*   **dwdiff** — Una interfaz de comparación de palabras para el programa diff; admite colores.

	[https://os.ghalkes.nl/dwdiff.html](https://os.ghalkes.nl/dwdiff.html) || [dwdiff](https://www.archlinux.org/packages/?name=dwdiff)

*   **GNU wdiff** — Una implementación para palabras de GNU diff; no admite colores.

	[https://www.gnu.org/software/wdiff/](https://www.gnu.org/software/wdiff/) || [wdiff](https://www.archlinux.org/packages/?name=wdiff)

*   **cwdiff** — Un envoltorio de wdiff de GNU que colorea el resultado.

	[Https://github.com/junghans/cwdiff](Https://github.com/junghans/cwdiff) || [cwdiff](https://aur.archlinux.org/packages/cwdiff/), [cwdiff-git](https://aur.archlinux.org/packages/cwdiff-git/)

Véase también [List of applications/Utilities#Comparison, diff, merge](/index.php/List_of_applications/Utilities#Comparison.2C_diff.2C_merge "List of applications/Utilities").

### Alternativas a grep

*   **mgrep** — Un grep multilínea.

	[Https://sourceforge.net/projects/multiline-grep/](Https://sourceforge.net/projects/multiline-grep/) || [mgrep](https://aur.archlinux.org/packages/mgrep/)

#### Buscadores de código

Las siguientes tres herramientas tienen como objetivo reemplazar grep para la búsqueda de código. Realizan búsquedas recursivas de manera predeterminada, omiten archivos binarios y respetan `.gitignore`.

*   **ack** — Un reemplazo de grep basado en Perl, dirigido a programadores con grandes estructuras de código fuente heterogéneo.

	[Https://beyondgrep.com/](Https://beyondgrep.com/) || [ack](https://www.archlinux.org/packages/?name=ack)

*   **ripgrep (rg)** — Una herramienta de búsqueda que combina las capacidades de ag con la velocidad de grep.

	[Https://github.com/BurntSushi/ripgrep](Https://github.com/BurntSushi/ripgrep) || [ripgrep](https://www.archlinux.org/packages/?name=ripgrep)

*   **La herramienta de búsqueda de código Silver Searcher (ag)** — similar a Ack, pero más rápida.

	[Https://github.com/ggreer/the_silver_searcher](Https://github.com/ggreer/the_silver_searcher) || [the_silver_searcher](https://www.archlinux.org/packages/?name=the_silver_searcher)

#### Filtros interactivos

*   **[fzf](/index.php/Fzf "Fzf")** — Buscador difuso de línea de comandos de propósito general, potenciado por find por defecto.

	[Https://github.com/junegunn/fzf](Https://github.com/junegunn/fzf) || [fzf](https://www.archlinux.org/packages/?name=fzf), [fzf-git](https://aur.archlinux.org/packages/fzf-git/)

*   **fzy** — Un selector de texto difuso simple y rápido con un algoritmo de puntuación avanzado.

	[Https://github.com/jhawthorn/fzy](Https://github.com/jhawthorn/fzy) || [fzy](https://www.archlinux.org/packages/?name=fzy), [fzy-git](https://aur.archlinux.org/packages/fzy-git/)

*   **peco** — Herramienta de filtrado interactivo simplista.

	[Https://github.com/peco/peco](Https://github.com/peco/peco) || [peco](https://aur.archlinux.org/packages/peco/), [peco-git](https://aur.archlinux.org/packages/peco-git/)

*   **percol** — Añade algo del filtrado interactivo al concepto de conducto (pipe) tradicional del intérprete de comandos de UNIX.

	[Https://github.com/mooz/percol](Https://github.com/mooz/percol) || [percol](https://www.archlinux.org/packages/?name=percol), [percol-git](https://aur.archlinux.org/packages/percol-git/)

## Véase también

*   [Documentación de GNU Coreutils](https://www.gnu.org/software/coreutils/manual/coreutils.html)
*   [Utilidades POSIX](http://pubs.opengroup.org/onlinepubs/9699919799/idx/utilities.html)