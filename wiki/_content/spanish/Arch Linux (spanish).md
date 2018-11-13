**Estado de la traducción**
Este artículo es una traducción de [Arch Linux](/index.php/Arch_Linux "Arch Linux"), revisada por última vez el **2018-08-23**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Arch_Linux&diff=0&oldid=536968) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Arch Linux es una distribución [GNU](/index.php/GNU_(Espa%C3%B1ol) "GNU (Español)")/Linux de propósito general, desarrollada independientemente para x86-64, que se esfuerza por proporcionar las últimas versiones estables de la mayoría del software, siguiendo un modelo de lanzamiento continuo (*rolling-release*). La instalación por defecto deja un sistema de base mínima, que el usuario configurará posteriormente agregando lo que necesite.

## Contents

*   [1 Principios](#Principios)
    *   [1.1 Simplicidad](#Simplicidad)
    *   [1.2 Modernidad](#Modernidad)
    *   [1.3 Pragmatismo](#Pragmatismo)
    *   [1.4 Centrado en el usuario](#Centrado_en_el_usuario)
    *   [1.5 Versatilidad](#Versatilidad)
*   [2 Historia](#Historia)
    *   [2.1 Los primeros años](#Los_primeros_años)
    *   [2.2 Los años intermedios](#Los_años_intermedios)
    *   [2.3 El nacimiento de ArchWiki](#El_nacimiento_de_ArchWiki)
    *   [2.4 El amanecer de la era de A. Griffin](#El_amanecer_de_la_era_de_A._Griffin)
    *   [2.5 Scripts de instalación de Arch](#Scripts_de_instalación_de_Arch)
    *   [2.6 La era de systemd](#La_era_de_systemd)
    *   [2.7 Finaliza el soporte de i686](#Finaliza_el_soporte_de_i686)

## Principios

### Simplicidad

Arch Linux define simplicidad como *sin adiciones o modificaciones innecesarias*. El software es lanzado por los desarrolladores originales ([upstream](https://en.wikipedia.org/wiki/Upstream_(software_development) "wikipedia:Upstream (software development)")) con cambios mínimos (downstream) específicos para la distribución en cuestión: se evitan los parches no aceptados por upstream, y los parches downstream de Arch consisten, casi en su totalidad, en correcciones de errores backports que han quedado desfasados por el próximo lanzamiento del proyecto.

De un modo similar, los archivos de configuración de Arch proporcionados por los desarrolladores contienen cambios limitados relativos a cuestiones específicas de la distribución, como el ajuste de las rutas de los archivos del sistema. No añade características de automatización, tales como activar un servicio simplemente porque se ha instalado el paquete. Los paquetes son únicamente divididos cuando existen ventajas convincentes, como por ejemplo para ahorrar espacio en disco, en particular con casos de generar acumulación de residuos. No se proporcionan oficialmente utilidades de configuración gráficas, animando al usuario a realizar la mayor parte de la configuración del sistema desde un terminal y con un editor de texto.

### Modernidad

Arch Linux se esfuerza por mantener las últimas versiones estables liberadas de software, siempre y cuando no causen errores del sistema en la medida que pueda evitarse razonablemente. Se basa en un sistema [lanzamiento continuo](https://en.wikipedia.org/wiki/es:Liberaci%C3%B3n_continua "wikipedia:es:Liberación continua"), que permite una instalación de una sola vez con actualizaciones continuas.

Arch incorpora muchas de las nuevas tecnologías disponibles para los usuarios de GNU/Linux, incluyendo el sistema de inicio [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"), [sistemas de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") modernos, LVM2, software RAID, soporte para udev e initcpio (con [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)")), así como las últimas versiones de kernel disponibles.

### Pragmatismo

Arch es una distribución pragmática antes que idealista. Los principios aquí solo sirven como directrices útiles. En última instancia, las decisiones de diseño se realizan caso por caso a través de un desarrollo consensuado. Las técnicas de análisis se basan en la evidencia y los debates, no en la política o las opiniones públicas.

Se ofrece un gran número de paquetes y script de compilación en los diferentes repositorios de Arch Linux tanto de software libre y de código abierto para aquellos que lo prefieran, así como de software propietario para aquellos que abrazan la funcionalidad sobre la ideología.

### Centrado en el usuario

Mientras que muchas distribuciones de GNU/Linux intentan ser *fáciles de usar*, Arch Linux siempre ha pretendido y pretende permanecer *centrado en el usuario*. La distribución está destinada a cubrir las necesidades de aquellos usuarios que contribuyen a ella, en lugar de tratar de atraer a la mayor cantidad posible de usuarios. Está dirigida a usuarios competentes en GNU/Linux, o a cualquier persona con una actitud «do-it-yourself» que esté dispuesta a leer la documentación y resolver por sí misma los problemas.

Todos los usuarios están invitados a [participar](/index.php/Getting_involved_(Espa%C3%B1ol) "Getting involved (Español)") y contribuir con la distribución. Informar y ayudar a arreglar [errores](https://bugs.archlinux.org/) es altamente valorada y, los parches de mejora de paquetes o los [proyectos](https://projects.archlinux.org/) de core, son muy apreciados: los desarrolladores de Arch, a menudo, comenzaron siendo voluntarios y activos contribuyentes antes de formar parte de ese equipo. Los *Archers* pueden contribuir libremente con paquetes en [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), mejorar la [documentación de ArchWiki](/index.php/Main_page_(Espa%C3%B1ol) "Main page (Español)"), proporcionar asistencia técnica a los demás usuarios o simplemente intercambiar opiniones en los [foros](https://bbs.archlinux.org/), [listas de correos](https://mailman.archlinux.org/mailman/listinfo/) o [Canales IRC](/index.php/IRC_channels_(Espa%C3%B1ol) "IRC channels (Español)"). Arch Linux es el sistema operativo elegido por muchas personas en todo el mundo, y existen varias [comunidades internacionales](/index.php/International_communities_(Espa%C3%B1ol) "International communities (Español)") que ofrecen ayuda y traducen la documentación a muchos idiomas diferentes.

### Versatilidad

Arch Linux es una distribución de propósito general. Tras la instalación, solo se proporciona un entorno de línea de órdenes: en lugar de ir eliminando paquetes innecesarios y no deseados, se ofrece al usuario la posibilidad de crear un sistema personalizado, eligiendo entre miles de paquetes de alta calidad presentes en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"), con soporte para arquitectura [x86-64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64").

Arch está respaldado por [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)"), un gestor de paquetes ligero, sencillo y rápido, que permite actualizar todo el sistema con una orden. Arch también ofrece el [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), un sistema tipo puertos que hace fácil compilar e instalar paquetes desde las fuentes, que también se pueden sincronizar con una orden. Además, el *Arch User Repository* contiene muchos miles más de scripts [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") aportados por la comunidad para la elaboración de paquetes desde las fuentes de carácter inestables usando la aplicación [makepkg](/index.php/Makepkg "Makepkg"). También hace posible que los usuarios construyan y mantengan sus propios repositorios personalizados con facilidad.

## Historia

La comunidad Arch ha crecido y madurado hasta convertirse en una de las distribuciones GNU/Linux más populares e influyentes, también atestiguada por la [atención y crítica](/index.php/Arch_Linux_press_coverage "Arch Linux press coverage") recibidas a lo largo de los años.

Los desarrolladores de Arch son voluntarios no remunerados, a tiempo parcial, y no hay perspectivas de monetizar Arch Linux, por lo que seguirá siendo libre en todos los sentidos de la palabra. Aquellos con curiosidad por leer más detalles sobre el historial de desarrollo de Arch pueden navegar por el [registro de Arch en Internet Archive Wayback Machine](http://web.archive.org/web/*/archlinux.org) y los [archivos de noticias de Arch Linux](https://www.archlinux.org/news/).

### Los primeros años

Judd Vinet, un guitarrista ocasional y programador canadiense, comenzó a desarrollar Arch Linux a principios de 2001\. Su primer lanzamiento oficial, Arch Linux 0.1, fue el 11 de marzo de 2002\. [Motivado](https://distrowatch.com/dwres.php?resource=interview-arch) por la elegante sencillez de Slackware, BSD, PLD Linux y CRUX, y también decepcionado ante la falta de gestión de paquetes en ese momento, Vinet construyó su propia distribución basada en principios similares a aquellas distribuciones. Pero, también escribió un programa de gestión de paquetes llamado [pacman](/index.php/Pacman "Pacman") para manejar, de forma automática, la instalación, eliminación y actualización de paquetes.

### Los años intermedios

La primera comunidad de Arch creció de manera constante, como lo demuestra [este gráfico de publicaciones, usuarios e informes de errores en el foro](/index.php/File:Archstats2002-2011.png "File:Archstats2002-2011.png"). Por otra parte, fue desde sus primeros días conocida como [una comunidad abierta, amigable y colaboradora](http://www.osnews.com/story/4827).

### El nacimiento de ArchWiki

En 2005-07-08 la ArchWiki [comenzó](/index.php/ArchWiki:About_(Espa%C3%B1ol)#Historia "ArchWiki:About (Español)") basada en Mediawiki.

### El amanecer de la era de A. Griffin

A finales de 2007, Judd Vinet se retiró de la participación activa como desarrollador de Arch, y [transfirió sin problemas las riendas al programador estadounidense Aaron Griffin](https://bbs.archlinux.org/viewtopic.php?id=38024), también conocido como Phrakture.

Con los años, la comunidad de Arch continuó creciendo y madurando, y ha recibido recientemente una atención inusual de la [prensa](/index.php/Arch_Linux_Press_Review "Arch Linux Press Review"), teniendo en cuenta el tamaño modesto de esta distribución Linux.

Los desarrolladores de Arch no cobran, dedican a la misma parte de su tiempo y no tienen perspectivas de monetizar Arch Linux, por lo que siguen siendo libres en el sentido más amplio de la palabra. Los curiosos que deseen examinar con más detalle la historia del desarrollo de Arch pueden navegar por la [Arch entry in the Internet Archive Wayback Machine](http://web.archive.org/web/*/archlinux.org) y la [Arch Linux News Archives](https://www.archlinux.org/news/).

### Scripts de instalación de Arch

El lanzamiento en 2012-07-15 del medio de instalación volvió [obsoleto](https://www.archlinux.org/news/install-media-20120715-released/) la estructura de instalación por menús de Arch, en favor de los scripts de instalación de Arch (*Arch Install Scripts*).

### La era de systemd

Entre 2012 y 2013 el sistema de inicio tradicional (system V) fue remplazado por systemd.[[1]](https://www.archlinux.org/news/install-medium-20121006-introduces-systemd/)[[2]](https://www.archlinux.org/news/systemd-is-now-the-default-on-new-installations/)[[3]](https://www.archlinux.org/news/end-of-initscripts-support/)[[4]](https://www.archlinux.org/news/final-sysvinit-deprecation-warning/)

### Finaliza el soporte de i686

En 2017-01-25 se [anunció](https://www.archlinux.org/news/phasing-out-i686-support/) que el soporte para la arquitectura i686 seria finalizado debido a la poca popularidad entre los desarrolladores y la comunidad. Al final de [noviembre de 2017](https://www.archlinux.org/news/the-end-of-i686-support/), todos los paquetes fueron eliminados de los servidores réplica.