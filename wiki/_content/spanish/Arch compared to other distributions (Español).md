Esta página pretende mostrar una comparación entre Arch Linux y otras distribuciones de GNU/Linux y sistemas operativos basados en UNIX. Los resúmenes que siguen son breves descripciones que pueden ayudar a un usario a decidir si Arch Linux se adapta a sus necesidades. Aunque las revisiones y descripciones pueden ser útiles, la propia experiencia es siempre la mejor manera de comparar las distribuciones.

## Contents

*   [1 Basadas en el código fuente](#Basadas_en_el_c.C3.B3digo_fuente)
    *   [1.1 Gentoo Linux](#Gentoo_Linux)
    *   [1.2 Sorcerer/Lunar-Linux/Source Mage](#Sorcerer.2FLunar-Linux.2FSource_Mage)
*   [2 Minimalistas](#Minimalistas)
    *   [2.1 LFS](#LFS)
    *   [2.2 CRUX](#CRUX)
    *   [2.3 Slackware](#Slackware)
*   [3 Generalistas](#Generalistas)
    *   [3.1 Debian GNU/Linux](#Debian_GNU.2FLinux)
    *   [3.2 Fedora](#Fedora)
    *   [3.3 Frugalware](#Frugalware)
*   [4 Amigable para los principiantes](#Amigable_para_los_principiantes)
    *   [4.1 Ubuntu](#Ubuntu)
    *   [4.2 Linux Mint](#Linux_Mint)
    *   [4.3 openSUSE](#openSUSE)
    *   [4.4 Mandriva/Mageia](#Mandriva.2FMageia)
    *   [4.5 PCLinuxOS](#PCLinuxOS)
*   [5 Estilos *BSD](#Estilos_.2ABSD)
    *   [5.1 FreeBSD](#FreeBSD)
    *   [5.2 NetBSD](#NetBSD)
    *   [5.3 OpenBSD](#OpenBSD)
*   [6 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Basadas en el código fuente

Las distribuciones basadas en las fuentes son altamente portables, proporcionando la ventaja de controlar y compilar el sistema operativo completo y las aplicaciones para la particular arquitectura de la máquina y el propósito de su uso, con la desventaja de que consumen mucho tiempo en la compilación del código fuente. La base de Arch y todos los paquetes están compilados para arquitecturas i686 y x86-64, ofreciendo un significativo incremento de prestaciones respecto a distribuciones basadas en paquetes i386/i486/i586 binarios, con la ventaja añadida de instalarse rápidamente.

### Gentoo Linux

*   Tanto Arch Linux como Gentoo Linux son sistemas rolling release, los paquetes compilados están disponibles para la distribución en un periódo de tiempo relativamente corto después de que se liberan por los desarrolladores.
*   Los paquetes de Gentoo y el sistema base se construyen directamente a partir del código fuente de acuerdo con 'USE flags' especificadas por el usuario. Arch proporciona un sistema ports-like para la construcción de paquetes de origen, aunque el sistema base Arch está diseñado para ser instalado como binarios pre-construidos para i686/x86_64\. Esto generalmente hace que Arch sea rápido de compilar y actualizar y, al igual que Gentoo, permiten ser más personalizables sistemáticamente.
*   Arch soporta i686 y x86_64 mientras Gentoo soporta oficialmente arquitecturas x86, PPC, SPARC, Alpha, AMD64, ARM, MIPS, HP/PA, S/390, sh y Itanium.
*   Los paquetes oficiales de Gentoo y las herramientas de administración del sistema tienden a ser bastante más complejos y «potentes» que los proporcionados por Arch, y ciertas características que se encuentran en el corazón de Gentoo *(como [USE flags](http://www.gentoo.org/doc/en/handbook/handbook-x86.xml?part=2&chap=2), [SLOTs](http://www.gentoo.org/doc/en/handbook/handbook-x86.xml?part=2&chap=1#doc_chap5), etc.)* no tienen ningún equivalente directo en Arch Linux. Una explicación de esas diferencias se debe al hecho de que Arch es principalmente una distro binaria, pero las diferencias en la [filosofía de diseño](/index.php/The_Arch_Way_(Espa%C3%B1ol) "The Arch Way (Español)") también juegan un papel importante, ya que Arch toma una postura más en favor de la simplicidad arquitectónica y en contra del exceso de ingeniería.
*   Debido a que tanto las instalaciones de Gentoo como de Arch sólo incluyen un sistema de base, ambas son consideradas como altamente personalizables. Los usuarios de Gentoo, en general, se sentirán muy a gusto con la mayoría de los aspectos de Arch.

### Sorcerer/Lunar-Linux/Source Mage

*   Sorcerer/Lunar-Linux/Source Mage (SLS) son todas ellas distribuciones basadas en el código fuente originalmente relacionadas entre sí.
*   Las distribuciones SLS utilizan un conjunto bastante simple de archivos de script para crear descripciones de los paquetes y utilizan un archivo de configuración global para gestionar el proceso de compilación, de modo muy similar al sistema [Arch Build System](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)"). Las herramientas de SLS garantizan un buen control de las dependencias, incluyendo el manejo de funciones opcionales, seguimiento de paquetes, eliminación y actualización. No hay paquetes binarios para cualquiera de las distribuciones de la familia SLS, aunque todas ellas ofrecen fácilmente la posibilidad de efectuar un rollback a los paquetes anteriormente instalados.
*   El proceso de instalación consiste en configurar un sistema de base simple en el menú de shell y ncurses, para luego, opcionalmente, recompilar el sistema base sucesivamente.
*   Al igual que Arch, no hay por defecto WM/DE/DM y Xorg no está incluido en la instalación base. Varias alternativas de servidor X están disponibles (X.Org 6.8 o 7, XFree86).

## Minimalistas

Las distribuciones minimalistas son bastante comparables a Arch, corpartiendo muchas similitudes. Todas son consideradas «simples» desde un punto de vista técnico.

### LFS

*   LFS, (o Linux From Scratch) existe simplemente como documentación. Un libro de instrucciones para el usuario sobre cómo obtener el código fuente de un paquete básico mínimo fijado para un sistema GNU/Linux funcional, y cómo compilarlo manualmente, parchearlo y configurarlo desde cero. LFS es tan mínimo como se puede ser y ofrece un excelente proceso educativo, y de construcción y personalización de un sistema básico.
*   LFS no ofrece repositorios en línea, las fuentes se obtienen manualmente, compilándolas e instalándolas con `make`. (Existen varios métodos manuales de gestión de paquetes y son mencionadas en LFS Hints).
*   Arch ofrece estos mismos paquetes, además de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"), algunas herramientas adicionales y el poderoso [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") como gestor de paquetes de su sistema base, ya compilados para i686/x86-64\. A parte del sistema de base mínima inicial de Arch, la comunidad Arch y los desarrolladores proporcionan y mantienen miles de paquetes binarios instalables a través de pacman, así como scripts [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") de compilación para su uso con [Arch Build System](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)"). Arch también incluye la herramienta [makepkg](/index.php/Makepkg "Makepkg") para compilar o manipular eficazmente paquetes `.pkg.tar.xz` que pueden ser fácilmente instalables mediante pacman.
*   Judd Vinet creó Arch desde cero y luego escribió pacman en C. Históricamente, a veces con humor, Arch fue descrito como simplemente «Linux, con un agradable gestor de paquetes».

### CRUX

*   Antes de crear Arch, Judd Vinet admiraba y utilizaba CRUX, una distribución minimalista creada por Per Lidén. Originalmente inspirado por las ideas en común de CRUX y BSD, Arch fue construido desde cero y [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") se codificó luego en C.
*   Arch y CRUX comparten algunos principios rectores: por ejemplo, ambos están optimizadas para arquitecturas determinadas, minimalistas y orientados por el principio KISS.
*   Ambos vienen con sistemas ports-like y utilizan sistemas de inicio de estilo *.BSD, ambos proporcionan un entorno de base mínimo para compilar posteriormente.
*   Pacman, como característica de Arch, se ocupa de la gestión de paquetes binarios del sistema y funciona a la perfección con el sistema [Arch Build System](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)"). CRUX utiliza un sistema de contribución comunitario llamado prt-get, que, en combinación con su propio sistema de puertos, se ocupa de la resolución de dependencias, pero construye todos los paquetes de origen (aunque la instalación base de CRUX es binaria).
*   Arch soporta oficialmente x86-64 y i686, mientras que CRUX soporta oficialmente i686 solamente, aunque la comunidad proporciona soporte para x86-64, PPC y 64-bit PPC.
*   Arch utiliza un sistema rolling-release y cuenta con una gran variedad de repositorios de paquetes binarios, así como el [Arch User Repository](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"). CRUX proporciona apoyo oficial a través de un sistema limitado de puertos además de un repositorio de la comunidad relativamente modesto.

### Slackware

*   Slackware y Arch son bastante similares dado que ambos son simples distribuciones enfocadas a la elegancia y minimalismo.

*   Slackware es famoso por su falta de marca y paquetes completamente vanilla, desde el kernel hacia arriba. Arch normalmente aplica sólo parches para evitar la ruptura grave o para asegurar que los paquetes se compilan limpiamente.

*   Slackware utiliza scripts de inicio de estilo BSD, Arch usa [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)").

*   Arch suministra un sistema de gestión de paquetes con [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)"), que, a diferencia de las herramientas estándar de Slackware, ofrece resolución automática de dependencias y permite actualizaciones del sistema más automatizado. Los usuarios de Slackware generalmente prefieren el método de resolución manual de dependencias, permaneciendo fieles al nivel de control que les otorga el sistema, aprovechando la excelente oferta de Slackware de bibliotecas y dependencias pre-instaladas.

*   Arch es un sistema rolling-release. Slackware es más conservador en su ciclo de lanzamiento, prefiriendo paquetes de probada estabilidad. Arch es más 'vanguardista' a este respecto.

*   Arch Linux proporciona miles de paquetes binarios en sus repositorios oficiales mientras que los repositorios oficiales de Slackware son más modestos.

*   Arch ofrece [Arch Build System](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)"), un verdadero sistema ports-like y también [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"), una colección considerable de PKGBUILDs aportados por los usuarios. Slackware ofrece un repositorio similar, aunque con un sistema más limitado en [slackbuilds.org](http://www.slackbuilds.org), que es un repositorio semi-oficial de Slackbuilds, análogos a los PKGBUILDs de Arch. Los usuarios de Slackware estarán generalmente bastante cómodos con la mayoría de los aspectos de Arch.

## Generalistas

Estas distribuciones ofrecen una amplia gama de ventajas y fortalezas y pueden satisfacer la mayoría de las necesidades que se pueden esperar de un sistema operativo.

### Debian GNU/Linux

*   Debian es un proyecto mucho más grande y cuenta con una versión comunitaria, estable, de prueba y las ramas inestables, que ofrece más de 20.000 paquetes binarios. El número disponible de paquetes binarios de Arch es más modesto. Sin embargo, al incluir los de AUR, las cantidades son muy comparables.

*   Debian tiene una postura más defensiva con respecto al software libre. Arch es más flexible y, por lo tanto, permisivo, en relación con el software «no libre» según la definición GNU, dejando de ese modo la elección de los usuarios.

*   Debian enfoca el diseño centrado más en la estabilidad y la rigurosidad de las pruebas. Arch se centra más en la filosofía de la simplicidad, el minimalismo y ofrecer el software más vanguardista. Los paquetes de Arch son más actuales que los de Debian Stable y Testing, siendo más comparable a la rama inestable de Debian.

*   Tanto Debian como Arch ofrecen sistemas de gestión de paquetes bien considerados.

*   Arch es rolling release, mientras que Debian Stable se libera con paquetes *«frozen»*. Debian unstable es rolling.

*   Debian está disponible para muchas arquitecturas, incluyendo alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390 y sparc, mientras que Arch está oficialmente disponible para i686 y x86_64, con las rama de la comunidad para arm (para Raspberry Pi por ejemplo) solamente.

*   Arch ofrece un apoyo más eficaz para compilaciones personalizadas, paquetes instalables desde fuentes externas, con un sistema de paquetes compilados ports-like. Debian no ofrece un sistema de puertos, sino que confía en sus grandes repositorios binarios.

*   El sistema de instalación de Arch sólo ofrece una mínima base expuesta transparentemente al usuario durante la configuración del sistema, mientras que Debian ofrece un enfoque de métodos más configurados automáticamente, así como varios métodos alternativos para la instalación.

*   Debian utiliza SysVinit, aunque systemd y upstart están disponibles para poder ser configurados por los usuarios, mientras que Arch usa [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") por defecto para un mejor rendimiento general.

*   Generalmente los paquetes de Arch incorporan tanto las bibliotecas de software como los archivos de cabeceras, en tanto que los archivos de cabecera de Debian tienen que ser descargados por separado.

*   Arch proporciona parches mínimamente, evitando así los problemas que los desarrolladores no son capaces de revisar, mientras que los parches de Debian a los paquetes son más normales.

*   [Algunas diferencias entre el empaquetado de Arch y Debian.](https://bbs.archlinux.org/viewtopic.php?id=179481)

### Fedora

*   Fedora es una desarrollada comunidad, aunque todavía corporativamente respaldada por Red Hat, lo que a menudo se presenta como un sistema *testbed release*; los paquetes y proyectos de Fedora migran a RHEL y algunos llegan a ser finalmente adoptados por otras distribuciones. Arch también se considera generalmente vanguardista, aunque es rolling-release y no sirve como una rama de pruebas para otra distribución.

*   Los paquetes de Fedora están en formato RPM, usando el gestor de paquetes YUM y están también disponibles oficialmente herramientas gráficas de paquetes. Arch usa [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") para administrar paquetes tar.xz y no soporta oficialmente una interfaz gráfica.

*   Fedora se niega a incluir apoyo a los medios MP3 y otros softwares no libres en los repositorios oficiales debido a su dedicación al software libre, aunque repositorios de terceros están disponibles para este tipo de paquetes. Arch es más flexible en su disposición hacia el software MP3 y non-free, dejando la decisión al usuario.

*   Fedora ofrece muchas opciones de instalación incluyendo un instalador gráfico, con unas opciones mínimas. Fedora «spins» también ofrece un surtido de entornos de escritorios alternativos para elegir, cada uno con un modesto conjunto de paquetes por defecto. Arch, por otra parte, sólo ofrece unos cuantos scripts destinados a facilitar el proceso de instalación de un sistema base mínimo.

*   Fedora tiene un ciclo de lanzamiento predefinido, pero oficialmente soporta actualizaciones discretas de las versiones con la herramienta PreUpgrade. Arch es un sistema rolling-release.

*   **The Arch Way** se centra en la simplicidad, la elegancia ligera y la capacidad del usuario, mientras que **Fedora Core Values** se enfoca hacia el software libre, el desarrollo comunitario y la última innovación sistemática.

*   Arch cuenta con un sistema de puertos, mientras que Fedora no.

*   **Tanto Arch Linux como Fedora están dirigidas a usuarios experimentados y a desarrolladores.** Ambos se apoyan decididamente en los usuarios para contribuir al desarrollo del proyecto.

*   Fedora se ha ganado el reconocimiento de la comunidad tanto por la integración de SELinux, como por los paquetes compilados de GCJ (para eliminar la necesidad de JRE de Sun) y la contribución prolífica de los desarrolladores; Red Hat y, por tanto, los desarrolladores de Fedora por extensión, contribuyen en un alto porcentaje al código del kernel Linux, en comparación con cualquier otro proyecto.

*   Arch Linux ofrece lo que es ampliamente considerado como la más completa e integral wiki de una distribución. El wiki de Fedora se utiliza en el sentido original de la palabra «wiki», o una forma de intercambiar información entre los desarrolladores, probadores y usuarios rápidamente. No pretende ser una base de conocimiento del usuario final como en Arch. La Wiki de Fedora se asemeja a un gestor de incidencias o una wiki corporativa.

### Frugalware

*   Arch está orientado a la línea de órdenes.

*   Frugalware no es compatible con el sistema de archivos JFS por defecto.

*   Tanto Arch como Frugalware se promueven optimizado para i686.

*   Tanto Arch y Frugalware podrían instalarse primero como un entorno mínimo y más tarde ampliarlo con pacman de acuerdo a las opciones y necesidades del usuario.

*   Frugalware se instala desde un DVD, con opciones predeterminadas de software y un entorno de escritorio elegido por el usuario previamente.

*   Frugalware tiene un ciclo de liberación programada. Una vez más, Arch está más enfocado en la simplicidad, el minimalismo, la corrección del código y la vanguardia de paquetes dentro de un modelo rolling-release.

## Amigable para los principiantes

A veces llamadas *«newbie distros»*, las distribuciones amigables para principiantes comparten muchas similitudes, aunque Arch es muy diferente de ellas. Arch puede ser una mejor opción si quiere aprender sobre GNU/Linux mediante la creación de una base muy mínima, dado que una instalación de Arch instala muy pocos paquetes en comparación. Las diferencias específicas entre las distribuciones se describen a continuación.

### Ubuntu

*   Ubuntu es una muy popular distribución basada en Debian, comercialmente patrocinada por Canonical Ltd., mientras que Arch es un sistema desarrollado de manera independiente a partir de cero.

*   Ambos proyectos tienen objetivos muy diferentes y se dirigen a una base de usuarios diferentes. Arch está diseñado para usuarios que desean acercarse a una filosofía de «hacer por sí mismos», mientras que Ubuntu proporciona un sistema configurado automáticamente que está destinado a ser más fácil de usar. Arch se presenta como un diseño mucho más minimalista a partir de un montaje de base, apoyándose en gran medida en el usuario para adaptarla a sus propias necesidades específicas. En general, los desarrolladores y expertos probablemente van a preferir Arch mejor que Ubuntu, aunque muchos usuarios de Arch han comenzado en Ubuntu y acabaron migrando a Arch.

*   El desarrollo actual de Ubuntu y su promoción parecen estar fuertemente apostando por el mercado de los dispositivos con pantalla táctil, mientras que el desarrollo Arch está más orientado, por lo general, a un modelo centrado en el usuario que permite a su comunidad crear soluciones personalizadas que se desarrollarán colaborativamente.
    *   Por otra parte, la naturaleza comercial de Canonical les ha llevado a algunas decisiones polémicas, como la inclusión de anuncios en el menú *Dash* de Unity y la recogida de datos del usuario. Arch es un proyecto independiente, impulsado por la comunidad sin una agenda comercial y sin ningún [bloatware](https://en.wikipedia.org/wiki/es:Software_inflado "wikipedia:es:Software inflado") en su distribución.

*   Ubuntu se mueve entre versiones discretas cada 6 meses, mientras que Arch es un sistema rolling-release con una nueva instantánea emitida cada mes.

*   Arch ofrece un sistema ports-like de paquetes compilados, mientras que Ubuntu no lo hace.

*   Las dos comunidades difieren en algunos aspectos también. La comunidad de Arch es mucho más pequeña y está fuertemente alentada a contribuir con la distribución. Por el contrario, la comunidad de Ubuntu es relativamente grande, por lo que puede tolerar un porcentaje mucho mayor de usuarios que no contribuyen activamente al desarrollo, empaquetado o mantenimiento de repositorios.

### Linux Mint

*   [Linux Mint](http://www.linuxmint.com/) nació como una derivación de [Ubuntu](#Ubuntu), y, más tarde, añadió LMDE (Linux Mint Debian Edition) que se basa en [Debian](#Debian_GNU.2FLinux). En este sentido, Arch se diferencia en que es una distribución independiente que tiene su propio [sistema de empaquetado](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") y sus propios [repositorios](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").
*   Al igual que Ubuntu, Mint tiene como objetivo ser «un sistema operativo moderno, elegante y amigable, que sea a la vez potente y fácil de usar», siendo sus destinatarios, el tratamiento de los paquetes y los objetivos de la distribución claramente opuestos al [minimalismo](/index.php/The_Arch_Way_(Espa%C3%B1ol) "The Arch Way (Español)") de Arch.
*   Mint incluye diversas herramientas gráficas para facilitar el mantenimiento, llamadas *MintTools*. Arch solo ofrece sencillas herramientas en línea de órdenes como [pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") y deja la gestión del sistema en manos del usuario.
*   Los buques insignias de Mint son [Cinnamon](/index.php/Cinnamon "Cinnamon") o [MATE](/index.php/MATE "MATE") como sus GUI, y, alternativamente, [KDE](/index.php/KDE "KDE") o [Xfce4](/index.php/Xfce4 "Xfce4"), acompañándoles códecs, flash, reproductores de DVD y soporte para MP3, alguno de los cuales son software proprietario; también incluye una gran variedad de software conocido, como [Firefox](/index.php/Firefox "Firefox"), [GIMP](/index.php/GIMP "GIMP"), [Libreoffice](/index.php/Libreoffice "Libreoffice"), [pidgin](/index.php/Pidgin "Pidgin") y otros. La instalación de la base de Arch, en cambio, ni siquiera incluye [Xorg (Español)](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") y, mucho menos, cualquier gestor de ventanas o entorno de escritorio, que, si es necesario, podrá ser instalado después como un paso posterior. Además, no hay software propietario incluido por defecto en la distribución de Arch.
*   Las nuevas versiones de Mint se liberan cada seis meses, un mes después de Ubuntu, con un ciclo de apoyo ligeramente diferente; las versiones LTS son apoyados por cinco años, y las tres liberaciones entre ellas solo están apoyadas por seis meses, hasta su sucesión. La versión LMDE sigue el ciclo de liberación de Debian Testing, que se describe en su página web como «semi-rolling» que utiliza «Update Packs» que, a su vez, se basa en instantáneas probadas de Debian Testing para proporcionar un sistema más estable. También es posible cambiar las fuentes para seguir a «Testing», o, incluso, a «Unstable» para obtener actualizaciones más frecuentes. Arch en cambio, es una distribución completamente rolling-release.
*   Mint utiliza APT como su gestor de paquetes: Arch utiliza [pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)").

### openSUSE

openSUSE se centra en el formato de paquetes RPM y su bien considerado YaST2, interfaz gráfica de usuario como herramienta de configuración, que es una ventanilla única para satisfacer las necesidades de la mayoría de los usuarios sobre la configuración del sistema, incluida la gestión de paquetes. Arch no ofrece este tipo de instalaciones, ya que va en contra de [The Arch Way](/index.php/The_Arch_Way_(Espa%C3%B1ol) "The Arch Way (Español)"). openSUSE, por lo tanto, es ampliamente considerada como más adecuada para los usuarios menos experimentados, o aquellos que quieren un entorno con más interfáces gráficas de usuario, las auto-configuraciones y las funcionalidades que se espera del ordenador.

### Mandriva/Mageia

Mandriva Linux (antes Mandrake Linux) fue creada en 1998 con el objetivo de hacer de GNU/Linux fácil de usar para todos. Está basada en RPM y utiliza el gestor de paquetes urpmi. Mageia es un fork de Mandriva creado por exempleados de Mandriva que se oponen a la posición comercial de su distribución original, al ser un proyecto impulsado por la comunidad y sin fines de lucro. Una vez más, Arch toma un enfoque más simple, estando basada en texto y apoyándose más en la configuración manual y dirigida a usuarios tanto intermedios como avanzados.

### PCLinuxOS

*   PCLinuxOS es una popular distribución basada en Mandriva que proporciona un completo DE, diseñado para la facilidad de uso y se autodescribe como «simple», aunque su definición de simple es muy diferente a la definición de Arch. Arch está diseñado como un sistema de base simple para personalizar desde la base y se dirige más hacia los usuarios avanzados.

*   PCLOS utiliza el gestor de paquetes apt como wrapper de paquetes RPM. Arch utiliza su propio gestor de paquetes desarrollado de forma independiente [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") para los paquetes `.pkg.tar.xz`.

*   PCLOS está apoyada en GUI, proporciona herramientas gráficas de configuración del hardware y el front-end Synaptic para la gestión de paquetes, y dice tener poca o ninguna confianza en la shell. Arch está orientada a la línea de órdenes y enfocada para el diseño simple en la configuración del sistema, la gestión y el mantenimiento.

*   PCLOS recomienda 256 MB de RAM como parte de sus requisitos mínimos del sistema. Al ser más ligero, Arch se puede ejecutar en sistemas con mucho menos memoria del sistema ya que requiere sólo 64 MB de RAM para la instalación de una sistema base en i686, y se ejecutará sin problemas en los sistemas más modernos.

## Estilos *BSD

Los sistemas operativos al estilo *BSD comparten un origen común y descienden directamente de los trabajos realizados en la Universidad de Berkeley para producir una redistribución libre, sin costo alguno, de un sistema *UNIX*. No son distribuciones GNU/Linux, sino más bien, sistemas operativos basados en *UNIX*. Por lo tanto, aunque Arch y los estilos *BSD comparten el concepto en una base fuertemente integrada y sistema de puertos, no son absolutamente igualables desde un punto de vista de código, excepto quizás con *vi*, ya que el *vi* de Arch es originariamente el *vi* de BSD (la mayoría de los descendientes de *BSD no utilizan más el original *vi* de BSD). Los estilos *BSD se derivaron del original código AT&T de *UNIX* y han heredado un verdadero patrimonio *UNIX*. Para obtener más información acerca de las variantes de *BSD, visite el sitio del proveedor.

### FreeBSD

*   Tanto Arch como [FreeBSD](http://www.freebsd.org/about.html) ofrecen software que se puede obtener utilizando binarios o compilar usando un sistema de 'ports'.

*   Al igual que otros *BSD, la base de FreeBSD es desarrollada fundamentalmente como un sistema diseñado en su conjunto, con cada aplicación «portada» a FreeBSD y asegurándose de que el proceso funcione. Por el contrario, las distribuciones GNU/Linux como Arch son como amalgamas combinadas de muchas fuentes diferentes.

*   La licencia FreeBSD es generalmente más protectora del *coder*, en contraste con la GPL, lo que favorece la protección del *código* mismo. Arch es liberado bajo la licencia GPL.

*   En FreeBSD, como Arch, las decisiones son delegadas a usted, el usuario avanzado. Esta puede ser la comparación más interesante, que Arch va a la cabeza en modernidad de paquete y tiene algo más importante, una inteligente, activa y sensata comunidad.

*   Ambos sistemas comparten muchas similitudes y los usuarios de FreeBSD en general se sentirá muy a gusto con la mayoría de los aspectos de Arch.

### NetBSD

*   NetBSD es un sistema operativo basado en `UNIX` libre, seguro y altamente portable disponible para más de 50 plataformas, desde equipos de 64 bits Opteron hasta sistemas de escritorio para dispositivos portátiles e integrados. Sus características de diseño limpio y avanzado hace que sea excelente tanto en entornos de producción como de investigación, y proporciona al usuario el código fuente completo. Muchas aplicaciones son fácilmente disponibles a través de pkgsrc, la Colección de Paquetes de NetBSD.

*   Arch no puede operar en el gran número de dispositivos en que funciona NetBSD, pero para un sistema i686 puede ofrecer más aplicaciones.

*   pkgsrc para NetBSD proporciona un método de instalación basado en las fuentes similar al ABS de Arch; los paquetes binarios, sin embargo, también están disponibles con pkg_tools.

*   Arch comparte similitudes con NetBSD: ambos requieren la configuración manual, son minimalistas y ligeros, ambos ofrecen paquetes binarios a través de un sistema de puertos y ambos tienen activos y sensatos desarrolladores y comunidades.

### OpenBSD

El proyecto OpenBSD proporciona un sistema operativo basado en `UNIX` libre y multiplataforma basada en 4.4BSD.

*   OpenBSD se centra en la portabilidad, la estandarización, la corrección de código, la seguridad proactiva y la criptografía integrada. Por su parte, Arch se centra más en la sencillez, la elegancia, el minimalismo y el software de vanguardia. OpenBSD se autodescribe como *«quizás el SO número 1 en seguridad»*.

*   Tanto Arch como OpenBSD ofrencen una pequeña instalación elegante de base.

*   Ambos ofrecen un sistema de puertos y empaquetado para permitir una fácil instalación y gestión de los programas que no son parte del sistema operativo base.

*   A diferencia de un sistema GNU /Linux como Arch, pero en común con la mayoría de otros sistemas operativos basados ​​en BSD, el kernel de OpenBSD y programas del espacio de usuario, como las herramientas de shell y comunes (como `ls`, `cp`, `cat` y `ps`), se desarrollan conjuntamente en un repositorio de fuentes único.

## Véase también

*   [DistroWatch.com](http://distrowatch.com/)