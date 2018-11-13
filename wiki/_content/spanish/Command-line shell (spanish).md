**Estado de la traducción**
Este artículo es una traducción de [Command-line shell](/index.php/Command-line_shell "Command-line shell"), revisada por última vez el **2018-10-29**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Command-line_shell&diff=0&oldid=551892) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [dotfiles](/index.php/Dotfiles "Dotfiles")
*   [Utilidades principales](/index.php/Core_utilities_(Espa%C3%B1ol) "Core utilities (Español)")

De [Wikipedia](https://en.wikipedia.org/wiki/es:Shell_de_Unix "wikipedia:es:Shell de Unix"):

	Un intérprete de línea de órdenes de Unix proporciona una interfaz de usuario tradicional para el sistema operativo Unix y para sistemas similares a Unix. Los usuarios dirigen el funcionamiento de la computadora introduciendo órdenes como texto para que un intérprete de línea de órdenes ejecute o creando scripts de texto de uno o más órdenes de este tipo.

## Contents

*   [1 Listado de intérpretes de línea de órdenes](#Listado_de_intérpretes_de_línea_de_órdenes)
    *   [1.1 Compatibles POSIX](#Compatibles_POSIX)
    *   [1.2 Intérpretes de línea de órdenes alternativos](#Intérpretes_de_línea_de_órdenes_alternativos)
*   [2 Cambiar su intérprete de línea de órdenes predeterminado](#Cambiar_su_intérprete_de_línea_de_órdenes_predeterminado)
*   [3 Archivos de configuración](#Archivos_de_configuración)
    *   [3.1 /etc/profile](#/etc/profile)
*   [4 Entrada y salida](#Entrada_y_salida)
*   [5 Véase también](#Véase_también)

## Listado de intérpretes de línea de órdenes

Los intérpretes de línea de órdenes que son más o menos [compatibles con POSIX](http://pubs.opengroup.org/onlinepubs/009695399/utilities/xcu_chap02.html) se listan bajo [#Compatibles POSIX](#Compatibles_POSIX), mientras que los intérpretes de línea de órdenes que tienen una sintaxis diferente están bajo [#Intérpretes de línea de órdenes alternativos](#Intérpretes_de_línea_de_órdenes_alternativos).

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

Después de instalar uno de los intérpretes de línea de órdenes anteriores, puede ejecutar ese intérprete de línea de órdenes dentro de su intérprete de línea de órdenes actual, simplemente ejecutándolo. Sin embargo, si quiere que le sirvan ese intérprete de línea de órdenes cuando inicie sesión, deberá cambiar su intérprete de línea de órdenes predeterminado.

Para listar todos los intérpretes de línea de órdenes instalados, ejecute:

```
$ chsh -l

```

Y para configurar uno como predeterminado para su usuario haga:

```
$ chsh -s *ruta-completa-al-intérprete-de-línea-de-órdenes*

```

donde *ruta-completa-al-intérprete-de-línea-de-órdenes* es la ruta completa dada por `chsh -l`.

Si ahora se desconecta y vuelve a iniciar sesión, será recibido por el otro intérprete de línea de órdenes.

## Archivos de configuración

Para iniciar automáticamente los programas en la consola o al iniciar sesión, puede usar los archivos/directorios de inicio del intérprete de línea de órdenes. Lea la documentación de su intérprete de línea de órdenes o su artículo de ArchWiki, por ejemplo [Bash (Español)#Archivos de configuración](/index.php/Bash_(Espa%C3%B1ol)#Archivos_de_configuración "Bash (Español)") o [Zsh#Startup/Shutdown files](/index.php/Zsh#Startup/Shutdown_files "Zsh").

Véase también [Wikipedia:es:Shell de Unix#Archivos de configuración para shells](https://en.wikipedia.org/wiki/es:Shell_de_Unix#Archivos_de_configuraci.C3.B3n_para_shells "wikipedia:es:Shell de Unix").

### /etc/profile

Al iniciar sesión, todas las cargas *(sources)* en `/etc/profile` compatibles con el intérprete de línea de órdenes Bourne, que a su vez cargan los archivos `*.sh` legible en `/etc/profile.d/`: estos scripts no requieren una directiva de intérprete, ni necesitan ser ejecutables. Se utilizan para configurar un entorno y definir configuraciones específicas de la aplicación.

## Entrada y salida

Véase también [GregsWiki](https://mywiki.wooledge.org/BashGuide/InputAndOutput "gregswiki:BashGuide/InputAndOutput") y [Redirección E/S](http://www.tldp.org/LDP/abs/html/io-redirection.html).

*   Las redirecciones truncan los archivos antes de ejecutar las órdenes: `*orden* *archivo* > *archivo*` por lo tanto no funcionará como se esperaba. Mientras que algunas órdenes ([sed](/index.php/Sed_(Espa%C3%B1ol) "Sed (Español)"), por ejemplo) proporcionan una opción para editar archivos al momento, muchos no lo hacen. En esos casos puede utilizar la orden [sponge(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sponge.1) del paquete [moreutils](https://www.archlinux.org/packages/?name=moreutils).
*   Debido a que *cat* no está integrado en el intérprete de línea de órdenes, en muchas ocasiones puede resultarle más conveniente utilizar una [redirección](https://en.wikipedia.org/wiki/Redirection_(computing) "wikipedia:Redirection (computing)"), por ejemplo en scripts, o si le importa mucho el rendimiento. De hecho, `< *archivo*` hace lo mismo que `cat *archivo*`.

*   Los intérpretes de línea de órdenes compatibles con POSIX soportan [Documentos aquí](http://tldp.org/LDP/abs/html/here-docs.html) *(Here Documents)*:

```
$ cat << EOF
uno
dos
tres
EOF

```

*   Las [tuberías](https://en.wikipedia.org/wiki/Pipeline_(Unix) del intérprete de línea de órdenes operan en la salida estándar *(stdout)* por defecto. Para operar en [stderr(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/stderr.3) puede redireccionar *stderr* a *stdout* con `*orden* 2>&1 | *otra-orden*` o, en Bash 4, `*orden* |& *otra-orden*`.
*   Recuerde que muchas [utilidades principales](/index.php/Core_utilities_(Espa%C3%B1ol) "Core utilities (Español)") de GNU aceptan archivos como argumentos, por lo que, por ejemplo `grep *patrón* < *archivo*` se puede reemplazar por `grep *patrón* *archivo*`.

## Véase también

*   [Evolución de los intérpretes de línea de órdenes en Linux](http://www.ibm.com/developerworks/linux/library/l-linux-shells/index.html) en IBM developerWorks
*   [terminal.sexy](https://terminal.sexy/) — Diseñador de esquemas de color de terminal
*   [Hyperpolyglot](http://hyperpolyglot.org/unix-shells) — Comparación lado-a-lado de las sintaxis del intérprete de línea de órdenes
*   [UNIX Power Tools](http://docstore.mik.ua/orelly/unix/upt/index.htm) — Utilización general de la herramienta de línea de comandos
*   [commandlinefu.com](https://www.commandlinefu.com/commands/browse) — Compartir fragmentos de línea de órdenes
*   [List of applications#Terminal emulators](/index.php/List_of_applications#Terminal_emulators "List of applications")