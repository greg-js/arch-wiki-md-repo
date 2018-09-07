**Estado de la traducción:** este artículo es una versión traducida de [Arch compared to other distributions](/index.php/Arch_compared_to_other_distributions "Arch compared to other distributions"). Fecha de la última traducción/revisión: **2018-08-23**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Arch_compared_to_other_distributions&diff=0&oldid=537006).

Artículos relacionados

*   [Arch Linux](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)")
*   [Distribuciones basadas en Arch](/index.php/Arch-based_distributions_(Espa%C3%B1ol) "Arch-based distributions (Español)")
*   [Pacman/Rosetta](/index.php/Pacman/Rosetta_(Espa%C3%B1ol) "Pacman/Rosetta (Español)")

Esta página pretende mostrar una comparación entre Arch Linux y otras distribuciones de GNU/Linux y sistemas operativos basados en UNIX. Los resúmenes que siguen son breves descripciones que pueden ayudar a un usario a decidir si Arch Linux se adapta a sus necesidades. Aunque las revisiones y descripciones pueden ser útiles, la propia experiencia es siempre la mejor manera de comparar las distribuciones.

Para una comparación más completa, consulte esta [comparación de sistemas operativos](https://en.wikipedia.org/wiki/Comparison_of_operating_systems "w:Comparison of operating systems") y esta [comparación de distribuciones Linux](https://en.wikipedia.org/wiki/Comparison_of_Linux_distributions "w:Comparison of Linux distributions").

En adelante, solo se compara Arch Linux con otras distribuciones. Las adaptaciones de la comunidad que admiten arquitecturas que no sean x86_64 se pueden encontrar listados entre las [distribuciones basadas en Arch](/index.php/Arch-based_distributions_(Espa%C3%B1ol) "Arch-based distributions (Español)").

## Contents

*   [1 Basadas en las fuentes](#Basadas_en_las_fuentes)
    *   [1.1 CRUX](#CRUX)
    *   [1.2 LFS](#LFS)
    *   [1.3 Gentoo Linux](#Gentoo_Linux)
*   [2 Generalistas](#Generalistas)
    *   [2.1 Debian](#Debian)
    *   [2.2 Fedora](#Fedora)
    *   [2.3 Slackware](#Slackware)
*   [3 Adecuadas para principiantes](#Adecuadas_para_principiantes)
    *   [3.1 Ubuntu](#Ubuntu)
    *   [3.2 Linux Mint](#Linux_Mint)
    *   [3.3 openSUSE](#openSUSE)
    *   [3.4 Mandriva/Mageia](#Mandriva.2FMageia)
*   [4 Los *BSD](#Los_.2ABSD)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Basadas en las fuentes

Las distribuciones basadas en las fuentes son altamente portables, proporcionando la ventaja de controlar y compilar todo el sistema operativo y las aplicaciones para una arquitectura de máquina y un esquema de uso particulares, con la desventaja de la lentitud en la compilación de fuentes. La base de Arch y todos los paquetes solo se compilan para la arquitectura x86_64.

### CRUX

*   [CRUX](https://crux.nu/) es una distribución liviana que se enfoca en el principio [KISS](/index.php/Arch_terminology#KISS "Arch terminology"). CRUX inspiró a Judd Vinet para crear Arch.
*   CRUX utiliza scripts de inicio de estilo BSD, mientras que Arch usa systemd.
*   Mientras Arch usa un sistema de lanzamiento continuo, CRUX tiene lanzamientos más o menos anuales.
*   Ambos vienen con sistemas porst-like y, como *BSD, proporcionan un entorno base sobre el que construir.
*   Arch presenta a pacman, que maneja la administración de paquetes binarios del sistema y funciona a la perfección con el sistema [Arch Build System](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)"). CRUX usa un sistema de contribución comunitario llamado prt-get, que, en combinación con su propio sistema de ports, se ocupa de la resolución de dependencias, pero construye todos los paquetes desde la fuente (aunque la instalación base de CRUX es binaria).
*   Tanto Arch como CRUX solo admiten oficialmente la arquitectura x86_64.
*   Arch presenta una gran variedad de repositorios de paquetes binarios, así como el [Arch User Repository](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"). CRUX proporciona un sistema oficialmente respaldado de ports más reducido, además de un repositorio comunitario más modesto comparativamente.

### LFS

*   [LFS](http://www.linuxfromscratch.org/lfs/), (o Linux From Scratch) existe simplemente como documentación. El libro instruye al usuario sobre la obtención del código fuente para un paquete base mínimo establecido para un sistema funcional GNU/Linux, y cómo compilarlo, parchearlo y configurarlo desde cero. LFS es tan mínimo como sea posible y ofrece un excelente y educativo proceso de construcción y personalización de un sistema base.
*   LFS no ofrece repositorios en línea, las fuentes se obtienen manualmente, compilando e instalándolas con *make*. (Existen varios métodos manuales de gestión de paquetes y son mencionados en LFS Hints).
*   Arch ofrece estos mismos paquetes, además de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"), algunas herramientas adicionales y el potente administrador de paquetes [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") como su sistema base, ya compilado para x86_64\. Junto con el sistema base mínimo de Arch, la comunidad y los desarrolladores de Arch proporcionan y mantienen miles de paquetes binarios instalables a través de pacman, así como los scripts de compilación [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") para usar con [Arch Build System](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)"). Arch también incluye la herramienta [makepkg](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)") para construir o personalizar convenientemente paquetes *.pkg.tar.xz*, instalados fácilmente por pacman.
*   Judd Vinet creó Arch desde cero, y luego escribió pacman en C. Históricamente, Arch a veces se describía con humor simplemente como «Linux, con un buen administrador de paquetes».

### Gentoo Linux

*   Tanto Arch Linux como [Gentoo Linux](https://gentoo.org/) son sistemas de lanzamiento continuo, lo que hace que los paquetes estén disponibles para la distribución poco después de que se liberen.
*   Los paquetes y el sistema base de Gentoo se construyen directamente desde el código fuente de acuerdo con los *ajustes USE* especificados por el usuario. Arch proporciona una especie de sistema de ports para construir paquetes desde la fuente, aunque el sistema base Arch está diseñado para instalarse como binarios x86_64 pre-construidos. Esto generalmente hace que Arch sea más rápido de construir y actualizar, y permite a Gentoo ser sistemáticamente más personalizable.
*   Arch solo soporta x86_64, mientras que Gentoo admite oficialmente arquitecturas x86 (i486/i686), x86_64, PPC/PPC64, SPARC, Alpha, ARM, MIPS, HPPA, S/390 e Itanium.
*   Los paquetes oficiales de Gentoo y las herramientas de administración del sistema tienden a ser bastante más complejos y «potentes» que los provistos por Arch, y ciertas características que están en el corazón de Gentoo *([ajustes USE](https://wiki.gentoo.org/wiki/Handbook:X86/Working/USE/es), [SLOTs](https://wiki.gentoo.org/wiki/Handbook:X86/Working/Portage/es#Terminolog.C3.ADa), etc.)* no tienen ningún equivalente directo en Arch Linux. Parte de esto se debe al hecho de que Arch es principalmente una distribución binaria, pero las diferencias en la [filosofía de diseño](/index.php/Arch_Linux_(Espa%C3%B1ol)#Principios "Arch Linux (Español)") también juegan un papel importante, ya que Arch adopta una postura más en favor de la simplicidad arquitectónica, evitando el exceso de ingeniería.
*   Debido a que tanto las instalaciones de Gentoo como las de Arch solo incluyen un sistema base, ambas se consideran altamente personalizables. Si como usuario de Gentoo se siente cómodo con [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"), también se sentirá cómodo con la mayoría de los aspectos de Arch.

## Generalistas

Estas distribuciones ofrecen una amplia gama de ventajas y fortalezas y pueden satisfacer la mayoría de usos de un sistema operativo.

### Debian

*   [Debian](https://www.debian.org/) es la distribución de Linux más amplia con una comunidad más grande y cuenta con ramas estables, de prueba e inestables, ofreciendo más de 43,000 [paquetes](https://packages.debian.org/unstable/). El número disponible de paquetes binarios en Arch es más modesto. Sin embargo, al incluir los de AUR, las cantidades son comparables.

*   Debian tiene una postura más vehemente en el software libre, pero aún incluye software no libre en sus repositorios no libres. Arch es más indulgente, y por lo tanto incluyente, con respecto a los *paquetes no libres* según lo define GNU.

*   Debian se centra en las pruebas rigurosas de la rama estable, que está «congelada» y da soporte hasta [cinco años](https://wiki.debian.org/LTS "debian:LTS"). Los paquetes de Arch son más actuales que los de la rama estable de Debian, siendo más comparables con las ramas de prueba e inestables de Debian, y no tienen un calendario de lanzamiento fijo.

*   Debian está disponible para muchas arquitecturas, incluidas alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390, y sparc, mientras que Arch está solo para x86_64.

*   Arch ofrece un soporte más conveniente para crear e instalar paquetes personalizables desde fuentes externas, con una especie de sistema de compilación de ports. Debian no ofrece un sistema de ports, confiando en cambio en sus grandes repositorios binarios.

*   El sistema de instalación de Arch solo ofrece una base mínima, expuesta de forma transparente durante la configuración del sistema, mientras que los métodos de Debian, como el uso de *tareas* apt para instalar grupos de paquetes preseleccionados, ofrecen un enfoque de configuración más automático así como varios métodos alternativos de instalación.

*   Arch generalmente empaqueta las bibliotecas de software junto con sus archivos de cabecera, mientras que en Debian los archivos de cabecera deben descargarse por separado.

*   Arch mantiene los parches al mínimo, evitando así los problemas que los desarrolladores no pueden revisar, mientras que Debian parchea sus paquetes de forma más liberal para un público más amplio.

### Fedora

*   [Fedora](https://getfedora.org/) está desarrollado por la comunidad, pero respaldada corporativamente por Red Hat; a menudo se presenta como un sistema de lanzamiento de prueba (o *testbed release system*). Los paquetes y proyectos de Fedora migran a RHEL y algunos finalmente son adoptados por otras distribuciones. Arch no tiene lanzamientos fijos, y no sirve como una rama de prueba para otra distribución.

*   Los paquetes de Fedora usan el formato RPM con el administrador de paquetes DNF. Arch usa [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") para administrar paquetes tar.xz.

*   Fedora rehúsa a incluir software no libre en repositorios oficiales debido a su dedicación al software libre, aunque existen repositorios de terceros disponibles para dichos paquetes. Arch es más indulgente en su disposición hacia el software no libre, dejando la decisión al usuario.

*   Fedora ofrece muchas opciones de instalación que incluyen un instalador gráfico y una opción mínima. Los «spins» de Fedora también ofrecen un surtido de entornos de escritorio alternativos donde elegir, cada uno con una variedad modesta de paquetes predeterminados. Arch, por otro lado, solo proporciona algunos scripts para facilitar el proceso de instalación de un sistema base mínimo.

*   Fedora tiene un ciclo de lanzamiento programado, pero oficialmente admite actualizaciones discretas de versiones con la herramienta FedUp. Arch es un sistema de lanzamiento continuo.

*   Arch presenta un sistema de ports, mientras que Fedora no.

*   Tanto Arch como Fedora están dirigidos a usuarios y desarrolladores experimentados. Ambos alientan fuertemente a sus usuarios a contribuir al desarrollo del proyecto.

*   Fedora ha ganado mucho reconocimiento de la comunidad por la integración de SELinux, los paquetes compilados de GCJ (para eliminar la necesidad de JRE de Oracle) y la contribución prolífica de los desarrolladores; de Red Hat y, por extensión, los de Fedora, contribuyen con el porcentaje más alto de código del kernel de Linux en comparación con cualquier otro proyecto.

*   Arch Linux proporciona lo que ampliamente se considera como la wiki de una distribución más exhaustiva e integral. La wiki de Fedora se usa en el sentido original de la palabra «wiki», o una forma rápida de intercambiar información entre desarrolladores, probadores y usuarios. No pretende ser una base de conocimiento para el usuario final como en Arch. El wiki de Fedora se asemeja a un rastreador de incidencias o una wiki corporativa.

### Slackware

*   [Slackware](http://www.slackware.com/) utiliza scripts de inicio estilo BSD, mientras que Arch usa [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)").

*   Arch suministra un sistema de gestión de paquetes mediante [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") que, a diferencia de las herramientas estándar de Slackware, ofrece una resolución de dependencia automática y permite actualizaciones del sistema más automatizadas. Los usuarios de Slackware generalmente prefieren su método manual de resolución de dependencias, citando el nivel de control del sistema que les concede, aprovechando el excelente suministro de bibliotecas y dependencias pre-instaladas de Slackware.

*   Arch es un sistema de lanzamiento continuo. Slackware es visto como más conservador en su ciclo de lanzamiento, prefiriendo paquetes de probada estabilidad. Arch es más *innovadora* en este sentido.

*   Arch Linux proporciona miles de paquetes binarios en sus repositorios oficiales, mientras que los repositorios oficiales de Slackware son más modestos.

*   Arch ofrece el [Arch Build System](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)"), similar a un sistema de ports y también el [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"), una gran colección de PKGBUILD aportados por los usuarios. Slackware ofrece un sistema similar aunque más limitado en [slackbuilds.org](http://www.slackbuilds.org) que es un repositorio semi-oficial de Slackbuilds, análogos a los PKGBUILDs de Arch. Los usuarios de Slackware estarán generalmente bastante cómodos con la mayoría de los aspectos de Arch.

## Adecuadas para principiantes

A veces llamadas «distribuciones para novatos», las distribuciones adecuadas para principiantes comparten muchas similitudes, aunque Arch es bastante diferente de ellas. Arch puede ser una mejor opción si desea aprender sobre GNU/Linux construyendo desde una base pequeña, ya que una instalación de Arch instala pocos paquetes en comparación. Las diferencias específicas entre las distribuciones se describen a continuación.

### Ubuntu

*   [Ubuntu](https://www.ubuntu.com/) es una distribución popular basada en Debian patrocinada comercialmente por Canonical Ltd., mientras que Arch es un sistema desarrollado de forma independiente desde cero.

*   Ambos proyectos tienen objetivos muy diferentes y están dirigidos a una base de usuarios diferente. Arch está diseñado para usuarios que desean un enfoque de «hazlo tú mismo», mientras que Ubuntu proporciona un sistema pre-configurado. Arch presenta un diseño más simple desde la instalación base en adelante, confiando en que el usuario lo personalice según sus necesidades específicas. Muchos usuarios de Arch han comenzado en Ubuntu y finalmente migraron a Arch.

*   El desarrollo de Arch no está enfocado hacia una interfaz de usuario en particular más allá de la que su comunidad proporciona soporte. Además, la naturaleza comercial de Canonical les ha llevado a tomar decisiones controvertidas, como la inclusión de anuncios en el menú *Dash* de Unity y la recopilación de datos de los usuarios. Arch es un proyecto independiente, impulsado por la comunidad sin agenda comercial.

*   Ubuntu se mueve entre lanzamientos discretos cada 6 meses, mientras que Arch es un sistema de lanzamiento continuo.

*   Arch ofrece un sistema de compilación de paquetes similar a ports y el [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"), donde los usuarios pueden compartir paquetes fuente para el administrador de paquetes [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)"). Ubuntu usa la más compleja [apt](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool "wikipedia:Advanced Packaging Tool"), y permite la redistribución de paquetes binarios a través de [Personal Package Archives](https://launchpad.net/ubuntu/+ppas).

*   Las dos comunidades también difieren en algunos aspectos. La comunidad de Arch es mucho más pequeña y está fuertemente alentada a contribuir con la distribución. Por el contrario, la comunidad de Ubuntu es relativamente grande y, por lo tanto, puede tolerar un porcentaje mucho mayor de usuarios que no contribuyen activamente al desarrollo, el empaquetado o el mantenimiento de repositorios.

### Linux Mint

*   [Linux Mint](https://www.linuxmint.com/) nació como un derivado [Ubuntu](#Ubuntu), y más tarde añadió LMDE (Linux Mint Debian Edition) que está basado en [#Debian](#Debian). Por otro lado, Arch es una distribución independiente que se basa en su propio [sistema de compilación](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") y [repositorios](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").
*   Mint incluye varias herramientas gráficas para un mantenimiento más sencillo, llamadas *MintTools*. Arch solo proporciona herramientas simples de línea de comandos como [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") y deja la administración del sistema en manos del usuario.
*   Mint se publica con [Cinnamon](/index.php/Cinnamon "Cinnamon") o [MATE](/index.php/MATE_(Espa%C3%B1ol) "MATE (Español)") como sus GUI princiaples, y alternativamente [KDE](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)") o [Xfce4](/index.php/Xfce_(Espa%C3%B1ol) "Xfce (Español)").
*   Las nuevas versiones de Mint se liberan cada seis meses, aproximadamente un mes después de Ubuntu. Cada versión se basa en el Ubuntu LTS más reciente y recibe soporte durante cinco años. Linux Mint Debian Edition (LMDE) se basa en Debian estable y solo recibe actualizaciones en los paquetes Mint y las actualizaciones de seguridad. Arch en cambio, es una distribución de lanzamiento continuo.

### openSUSE

[openSUSE](https://www.opensuse.org/) se centra en el formato de paquetes RPM y su reconocida herramienta YaST2, de configuración guiada por GUI. Arch no ofrece esa facilidad. openSUSE, por lo tanto, puede ser más apropiada para los usuarios que desean un entorno más guiado por la GUI, la configuración automática o la funcionalidad que se espera, permitiendo una profunda personalización.

### Mandriva/Mageia

Mandriva Linux (anteriormente conocida como Mandrake Linux) se creó en 1998 con el objetivo de hacer que GNU/Linux sea fácil de usar para todos; está basada en RPM y usa el administrador de paquetes urpmi. Mageia es una bifurcación de Mandriva creada por antiguos empleados de Mandriva que se opone a la posición comercial de su distribución principal, ya que es un proyecto sin fines de lucro y dirigido por la comunidad. Arch toma un enfoque más simple que Mandriva o Mageia, ya que está basada en texto y se apoya en una configuración más manual, estando dirigida a usuarios de nivel tanto intermedios como avanzados.

## Los *BSD

*   Los *BSD comparten un origen común y descienden directamente del trabajo realizado en UC Berkeley para proporcionar un sistema UNIX de redistribución libre. No son distribuciones GNU/Linux, más bien son sistemas operativos de tipo UNIX, derivadas del código UNIX original de AT&T.

*   Arch y los *BSD comparten el concepto de una base y un sistema de ports estrechamente integrados. Sin embargo, a diferencia de las distribuciones GNU/Linux como Arch, el kernel de los *BSD y los programas del espacio de usuario (tanto la shell y las utilidades más comunes como *ls*, *cp*, *cat* y *ps*) se desarrollan conjuntamente en un único repositorio fuente.

*   La licencia BSD es generalmente más protectora del *programador*, en contraste con la GPL, que favorece la protección del *código* en sí mismo. Arch está publicada bajo la licencia GPL.

*   Para obtener más información sobre las variantes de los *BSD, consulte esta [comparación de los sistemas operativos BSD](https://en.wikipedia.org/wiki/Comparison_of_BSD_operating_systems "wikipedia:Comparison of BSD operating systems").

## Véase también

*   [DistroWatch.com](http://distrowatch.com/) - Novedades y reseñas sobre distribuciones de Linux
*   [The Live CD List](https://www.livecdlist.com) - Listado de imágenes en vivo de sistemas operativos