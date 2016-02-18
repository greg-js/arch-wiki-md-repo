Arch Linux es una distribución GNU/Linux independiente, de propósito general, desarrollada para [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)")/[x86-64](https://en.wikipedia.org/wiki/es:x86-64 "wikipedia:es:x86-64") , lo suficientemente versátil como para adaptarse a cualquier función. Su desarrollo se centra en la simplicidad, el minimalismo y la elegancia de código. Arch se instala como un sistema de base mínimo, configurado por el usuario, sobre el que se monta su propio entorno ideal, mediante la instalación de sólo lo que se requiere o se desea para sus propósitos particulares. Las GUI de las utilidades de configuración no son proporcionadas oficialmente y la mayor parte de la configuración del sistema se realiza desde la shell, mediante la simple modificación de archivos de textos. Basado en un modelo rolling-release, Arch se esfuerza por mantenerse al dia y, por lo general, ofrece las últimas versiones estables de la mayoría del software.

## Contents

*   [1 Historia](#Historia)
*   [2 Simplicidad](#Simplicidad)
*   [3 Modernidad](#Modernidad)
*   [4 Empaquetar software](#Empaquetar_software)
*   [5 Integridad del código](#Integridad_del_c.C3.B3digo)
*   [6 Comunidad](#Comunidad)
*   [7 Resumen](#Resumen)

## Historia

	*Artículo principal:* [History of Arch Linux](/index.php/History_of_Arch_Linux "History of Arch Linux").

Arch Linux fue fundada por el programador canadiense Vinet Judd. Su primer lanzamiento formal, Arch Linux 0.1, fue el 11 de marzo de 2002\. Aunque Arch es completamente independiente, se inspira en la simplicidad de otras distribuciones, incluyendo [Slackware](http://slackware.com), [CRUX](http://www.crux.nu) y [BSD](http://en.wikipedia.org/wiki/Berkeley_Software_Distribution). En 2007, Judd Vinet dejó el cargo de Project Lead para dedicarse a otros asuntos y fue reemplazado por el programador estadounidense Aaron Griffin, que continúa dirigiendo el proyecto en la actualidad.

## Simplicidad

Siguiendo la filosofía [The Arch Way](/index.php/The_Arch_Way_(Espa%C3%B1ol) "The Arch Way (Español)"), Arch Linux es ligero, flexible, simple y apunta a ser muy similar a UNIX. Un entorno mínimo (sin GUI), compilado para arquitecturas i686/x86-64, es proporcionado durante la instalación: en lugar de remover paquetes innecesarios y no deseados, al usuario se le ofrece la posibilidad de construir a partir de una base mínima sin ningún modelo previamente seleccionado por defecto. La propia filosofía sobre diseño e implementación hace que Arch sea fácil de extender y moldear a cualquier tipo de sistema que se quiera obtener, desde una máquina de consola minimalista al más grandioso entorno de escritorio disponible de múltiples funciones: es *el usuario* quién decide lo que su sistema Arch será.

## Modernidad

Arch Linux se esfuerza por mantener las últimas versiones estables liberadas de software, siempre y cuando no causen errores del sistema en la medida que pueda evitarse. Se basa en un sistema [rolling-release](https://en.wikipedia.org/wiki/rolling-release "wikipedia:rolling-release"), que permite una instalación de una sola vez con actualizaciones continuas, sin tener que volver a reinstalar y sin tener que elaborar actualizaciones del sistema en el paso de una versión a otra. Mediante la ejecución de un comando, un sistema de Arch se mantiene al día y a la vanguardia.

Arch incorpora muchas de las nuevas tecnologías disponibles para los usuarios de GNU/Linux, incluyendo el sistema de inicio [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"),sistemas de archivos modernos (ext2/3/4, Reiser, XFS, JFS, Btrfs), LVM2/EVMS, software RAID, soporte para udev e initcpio (con [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)")), así como las últimas versiones de kernels disponibles.

## Empaquetar software

Arch está respaldado por [pacman](/index.php/Pacman "Pacman"), un simple [gestor de paquetes](https://en.wikipedia.org/wiki/es:Sistema_de_gesti%C3%B3n_de_paquetes "wikipedia:es:Sistema de gestión de paquetes") binarios que permite actualizar todo el sistema con un solo comando. Pacman está escrito en *C* y diseñado desde cero para ser ligero, simple y muy rápido. Arch también proporciona la [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), un sistema ports-like para que sea fácil de compilar e instalar paquetes desde las fuentes, que también puede ser sincronizado con un solo comando. Incluso se puede recompilar todo el sistema con un solo comando.

Soportando las arquitecturas i686 y x86-64, los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)") proporcionan varios miles de paquetes de alta calidad para satisfacer las distintas demandas de software. Además, Arch estimula el crecimiento de la comunidad y la colaboración al ofrecer la [Arch User Repository](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"), que contiene miles de scripts PKGBUILD mantenidas por el usuario para la compilación y la instalación de paquetes de origen mediante la aplicación *makepkg* . También es posible que los usuarios construyan y gestionen fácilmente sus repositorios personalizados.

## Integridad del código

Arch ofrece software vanilla sin parchear; los paquetes son ofrecidos desde las fuentes [upstream](https://en.wikipedia.org/wiki/es:Upstream_(desarrollo_de_software) originales, como los autores originalmente los destinaron para ser distribuidos. Sólo en raras ocasiones los paquetes vienen parcheados, para evitar errores graves en el caso de desactualizaciones de versiones que pueden producirse dentro de un modelo rolling release.

## Comunidad

La comunidad de Arch es muy confiable, alegre y acogedora: a todos los *Archers* se les anima a participar y contribuir en la distribución, ya sea ayudando con el desarrollo del software principal, mantener paquetes, informar o reparar [bugs](https://bugs.archlinux.org/), mejorar la [documentación ArchWiki](/index.php/Main_page "Main page"), ayudar a otros usuarios a solucionar problemas o a intercambiando opiniones en los [foros](https://bbs.archlinux.org/), [listas de correos](https://mailman.archlinux.org/mailman/listinfo/), [canales IRC](/index.php/IRC_channels "IRC channels"), o compartiendo el conocimiento propio o el desarrollo autónomo de aplicaciones. Arch Linux es el sistema operativo elegido por muchas personas en todo el mundo y existen diversas [Comunidades Internacionales](/index.php/International_communities "International communities") que ofrecen ayuda y documentación en varios idiomas.

Véase [este artículo](/index.php/Getting_Involved_(Espa%C3%B1ol) "Getting Involved (Español)") si tiene intención de convertirse en un miembro activo de la comunidad.

## Resumen

En resumen: Arch Linux es una distribución versátil y sencilla, diseñada para adaptarse a las necesidades del usuario competente de Linux®. Es a la vez potente y fácil de manejar, por lo que es una distribución ideal para servidores y estaciones de trabajo. Tómela en la dirección que le convenga: si se comparte esta visión de lo que debería ser una distribución GNU/Linux, entonces sean bienvenidos y alentados a utilizarla libremente, a participar y a contribuir a la comunidad. ¡Bienvenidos a Arch!