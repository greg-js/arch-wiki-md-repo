**Estado de la traducción**
Este artículo es una traducción de [Command-line shell](/index.php/Command-line_shell "Command-line shell"), revisada por última vez el **2018-10-27**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Command-line_shell&diff=0&oldid=551650) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [dotfiles](/index.php/Dotfiles "Dotfiles")
*   [Utilidades principales](/index.php/Core_utilities_(Espa%C3%B1ol) "Core utilities (Español)")

De [Wikipedia](https://en.wikipedia.org/wiki/es:Shell_de_Unix "wikipedia:es:Shell de Unix"):

	Un intérprete de línea de órdenes de Unix proporciona una interfaz de usuario tradicional para el sistema operativo Unix y para sistemas similares a Unix. Los usuarios dirigen el funcionamiento de la computadora introduciendo órdenes como texto para que un intérprete de línea de órdenes ejecute o creando scripts de texto de uno o más órdenes de este tipo.

## Contents

*   [1 Listado de intérpretes de línea de órdenes](#Listado_de_int.C3.A9rpretes_de_l.C3.ADnea_de_.C3.B3rdenes)
    *   [1.1 Compatibles POSIX](#Compatibles_POSIX)
    *   [1.2 Intérpretes de línea de órdenes alternativos](#Int.C3.A9rpretes_de_l.C3.ADnea_de_.C3.B3rdenes_alternativos)
*   [2 Cambiar su intérprete de línea de órdenes predeterminado](#Cambiar_su_int.C3.A9rprete_de_l.C3.ADnea_de_.C3.B3rdenes_predeterminado)
*   [3 Archivos de configuración](#Archivos_de_configuraci.C3.B3n)
    *   [3.1 /etc/profile](#.2Fetc.2Fprofile)
*   [4 Entrada y salida](#Entrada_y_salida)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Listado de intérpretes de línea de órdenes

Los intérpretes de línea de órdenes que son más o menos [compatibles con POSIX](http://pubs.opengroup.org/onlinepubs/009695399/utilities/xcu_chap02.html) se listan bajo [#Compatibles POSIX](#Compatibles_POSIX), mientras que los intérpretes de línea de órdenes que tienen una sintaxis diferente están bajo [#Intérpretes de línea de órdenes alternativos](#Int.C3.A9rpretes_de_l.C3.ADnea_de_.C3.B3rdenes_alternativos).

### Compatibles POSIX

Todos estos intérpretes de línea de órdenes se pueden enlazar desde `/usr/bin/sh`. Cuando [Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)"), [mksh](https://www.archlinux.org/packages/?name=mksh) y [zsh](/index.php/Zsh_(Espa%C3%B1ol) "Zsh (Español)") se invocan con el nombre `sh`, automáticamente se vuelven más compatibles con POSIX.

*   **[Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)")** — Bash extiende el intérprete de línea de órdenes Bourne con el historial y el completado de la línea de órdenes, matrices indexadas y asociativas, aritmética de enteros, sustitución de procesos, cadenas de caracteres, coincidencia de expresiones regulares y expansión de llaves.

	[https://www.gnu.org/software/bash/](https://www.gnu.org/software/bash/) || [bash](https://www.archlinux.org/packages/?name=bash)

*   **[DASH](/index.php/Dash "Dash")** — Descendiente de la versión NetBSD del intérprete de línea de órdenes Almquist (ash). Un intérprete de línea de órdenes rápido y compatible con POSIX que pretende ser lo más pequeño posible.

	[http://gondor.apana.org.au/~herbert/dash/](http://gondor.apana.org.au/~herbert/dash/) || [dash](https://www.archlinux.org/packages/?name=dash)

*   **[KornShell](/index.php/KornShell "KornShell") (ksh)** — El lenguaje KornShell es un lenguaje de programación completo, potente y de alto nivel para escribir aplicaciones, a menudo más fácil y rápidamente que con otros lenguajes de alto nivel. Esto lo hace especialmente adecuado para la creación de prototipos. ksh tiene las mejores características del intérprete de línea de órdenes Bourne y el intérprete de línea de órdenes C, además de muchas características nuevas y propias. Por lo tanto, ksh puede hacer mucho para mejorar su productividad y la calidad de su trabajo, tanto en la interacción con el sistema como en la programación. Los programas ksh son más fáciles de escribir, y son más concisos y legibles que los programas escritos en un lenguaje de nivel inferior como C.

	[http://www.kornshell.com](http://www.kornshell.com) || See the [article](/index.php/Ksh#Installation "Ksh").

*   **[Zsh](/index.php/Zsh_(Espa%C3%B1ol) "Zsh (Español)")** — Intérprete de línea de órdenes diseñado para uso interactivo, aunque también es un poderoso lenguaje de scripting. Muchas de las características útiles de Bash, ksh y tcsh se incorporaron a Zsh; se añadieron también muchas características originales. El [documento introductorio](http://zsh.sourceforge.net/Intro/intro_toc.html) detalla algunas de las características únicas de Zsh.

	[https://www.zsh.org/](https://www.zsh.org/) || [zsh](https://www.archlinux.org/packages/?name=zsh)

**Sugerencia:** Los scripts POSIX y Bash se pueden enlazar mediante [shellcheck](https://www.archlinux.org/packages/?name=shellcheck).

### Intérpretes de línea de órdenes alternativos

*   **[C shell](https://en.wikipedia.org/wiki/es:C_shell "wikipedia:es:C shell") (tcsh)** — El intérprete de lenguaje de órdenes se puede utilizar como intérprete de línea de órdenes de inicio de sesión interactivo y como procesador de órdenes de script de intérprete de línea de órdenes. Incluye un editor de línea de órdenes, completado programable de palabras, corrección ortográfica, un mecanismo de historial, control de trabajos y una sintaxis tipo C.

	[http://www.tcsh.org](http://www.tcsh.org) || [tcsh](https://www.archlinux.org/packages/?name=tcsh)

*   **Elvish** — Elvish es un intérprete de línea de órdenes moderno y expresivo, que puede llevar valores estructurados internos a través de tuberías *(pipelines)*. Esta característica hace posible evitar una gran cantidad de código de procesamiento de texto complejo. Cuenta con un lenguaje de programación expresivo, con características como excepciones, espacios de nombres y funciones anónimas. También tiene una potente línea de lectura que comprueba la sintaxis mientras se escribe y resaltado de sintaxis de forma predeterminada.

	[https://elvish.io](https://elvish.io) || [elvish](https://aur.archlinux.org/packages/elvish/)

*   **[fish](/index.php/Fish "Fish")** — Intérprete de línea de órdenes inteligente y amigable. Fish realiza el resaltado de sintaxis de la línea de órdenes a todo color, así como el resaltado y el completado de las órdenes y sus argumentos, la existencia del archivo y el historial. Soporta el completado-mientras-escribes del historial y las órdenes. Fish puede analizar las páginas del manual de las órdenes del sistema para determinar los argumentos para las órdenes, lo que le permite resaltar y completar las órdenes. Se puede hacer una fácil revisión de la última orden mediante `Alt+Arriba`. El demonio fish (fishd) facilita el historial sincronizado en todas las instancias de fish, así como las variables de entorno persistentes y universales..

	[http://fishshell.com/](http://fishshell.com/) || [fish](https://www.archlinux.org/packages/?name=fish)

*   **[Nash](/index.php/Nash "Nash")** — Nash es un intérprete de línea de órdenes del sistema, inspirado en plan9 rc, que facilita la creación de scripts confiables y seguros aprovechando los espacios de nombres de los sistemas operativos (en linux y plan9) de forma idiomática..

	[https://github.com/NeowayLabs/nash](https://github.com/NeowayLabs/nash) || [nash-git](https://aur.archlinux.org/packages/nash-git/)

*   **Oh** — Intérprete de línea de órdenes Unix escrito en Go. Es similar en espíritu pero diferente en detalle de otros intérpretes de línea de órdenes de Unix. Oh extiende las funciones del lenguaje de programación del intérprete de línea de órdenes sin sacrificar las funciones interactivas del intérprete de línea de órdenes.

	[https://github.com/michaelmacinnis/oh](https://github.com/michaelmacinnis/oh) || [oh-git](https://aur.archlinux.org/packages/oh-git/)

*   **[Powershell](https://en.wikipedia.org/wiki/es:Windows_PowerShell "wikipedia:es:Windows PowerShell")** — PowerShell es un lenguaje de programación orientado a objetos y un intérprete de línea de órdenes interactivo, originalmente escrito y exclusivo para Windows. Más tarde, fue de código abierto y portado a Mac OS X y Linux.

	[https://github.com/PowerShell/PowerShell](https://github.com/PowerShell/PowerShell) || [powershell](https://aur.archlinux.org/packages/powershell/)

*   **[rc](https://en.wikipedia.org/wiki/es:rc_(shell) "wikipedia:es:rc (shell)")** — Intérprete de órdenes para Plan 9 que proporciona servicios similares al intérprete de línea de órdenes Bourne de UNIX, con algunas pequeñas adiciones y menos sintaxis idiosincrásica.

	[http://doc.cat-v.org/plan_9/4th_edition/papers/rc](http://doc.cat-v.org/plan_9/4th_edition/papers/rc) || [9base](https://www.archlinux.org/packages/?name=9base)

*   **xonsh** — Un intérprete de línea de órdenes retrocompatible basado en el intérprete python.

	[http://xon.sh/](http://xon.sh/) || [xonsh](https://www.archlinux.org/packages/?name=xonsh)

## Cambiar su intérprete de línea de órdenes predeterminado

After installing one the above shells, you can execute that shell inside of your current shell, by just running its executable. If you want to be served that shell when you login however, you will need to change your default shell.

To list all installed shells, run:

```
$ chsh -l

```

And to set one as default for your user do:

```
$ chsh -s *full-path-to-shell*

```

where *full-path-to-shell* is the full path as given by `chsh -l`.

If you now log out and log in again, you will be greeted by the other shell.

## Archivos de configuración

To autostart programs in console or upon login, you can use shell startup files/directories. Read the documentation for your shell, or its ArchWiki article, e.g. [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash") or [Zsh#Startup/Shutdown files](/index.php/Zsh#Startup.2FShutdown_files "Zsh").

See also [Wikipedia:Unix shell#Configuration files](https://en.wikipedia.org/wiki/Unix_shell#Configuration_files "wikipedia:Unix shell").

### /etc/profile

Upon login, all Bourne-compatible shells source `/etc/profile`, which in turn sources any readable `*.sh` files in `/etc/profile.d/`: these scripts do not require an interpreter directive, nor do they need to be executable. They are used to set up an environment and define application-specific settings.

## Entrada y salida

See also [GregsWiki](https://mywiki.wooledge.org/BashGuide/InputAndOutput "gregswiki:BashGuide/InputAndOutput") and [I/O Redirection](http://www.tldp.org/LDP/abs/html/io-redirection.html).

*   Redirections truncate files before commands are executed: `*command* *file* > *file*` will therefore not work as expected. While some commands ([sed](/index.php/Sed "Sed") for example) provide an option to edit files in-place, many do not. In such cases you can use the [sponge(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sponge.1) command from the [moreutils](https://www.archlinux.org/packages/?name=moreutils) package.
*   Because *cat* is not built into the shell, on many occasions you may find it more convenient to use a [redirection](https://en.wikipedia.org/wiki/Redirection_(computing) "wikipedia:Redirection (computing)"), for example in scripts, or if you care a lot about performance. In fact `< *file*` does the same as `cat *file*`.
*   POSIX-compliant shells support [Here Documents](http://tldp.org/LDP/abs/html/here-docs.html):

```
$ cat << EOF
one
two
three
EOF

```

*   Shell [pipelines](https://en.wikipedia.org/wiki/Pipeline_(Unix) operate on stdout by default. To operate on [stderr(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/stderr.3) you can redirect *stderr* to *stdout* with `*command* 2>&1 | *othercommand*` or, for Bash 4, `*command* |& *othercommand*`.
*   Remember that many GNU [core utilities](/index.php/Core_utilities "Core utilities") accept files as arguments, so for example `grep *pattern* < *file*` is replaceable with `grep *pattern* *file*`.

## Véase también

*   [Evolution of shells in Linux](http://www.ibm.com/developerworks/linux/library/l-linux-shells/index.html) on the IBM developerWorks
*   [terminal.sexy](https://terminal.sexy/) — Terminal Color Scheme Designer
*   [Hyperpolyglot](http://hyperpolyglot.org/unix-shells) — Side-by-side comparison of shell syntaxes
*   [UNIX Power Tools](http://docstore.mik.ua/orelly/unix/upt/index.htm) — General command-line tool usage
*   [commandlinefu.com](https://www.commandlinefu.com/commands/browse) — Command-line snippets sharing
*   [List of applications#Terminal emulators](/index.php/List_of_applications#Terminal_emulators "List of applications")