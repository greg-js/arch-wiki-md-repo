**Estado de la traducción**
Este artículo es una traducción de [Arch terminology](/index.php/Arch_terminology "Arch terminology"), revisada por última vez el **2020-02-12**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Arch_terminology&diff=0&oldid=593756) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Esta página está destinada a desmitificar los términos comunes utilizados en la comunidad Arch Linux. Siéntase libre de agregar o modificar cualquier término, pero utilice la opción de edición de esa sección en particular. Si decide agregar uno, póngalo en orden alfabético.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 ABS](#ABS)
*   [2 Arch Linux](#Arch_Linux)
*   [3 Arch Linux Archive](#Arch_Linux_Archive)
*   [4 AUR](#AUR)
*   [5 bbs](#bbs)
*   [6 communitiy/[community]](#communitiy/[community])
*   [7 core/[core]](#core/[core])
*   [8 custom/user repository](#custom/user_repository)
*   [9 developer](#developer)
*   [10 extra/[extra]](#extra/[extra])
*   [11 initramfs](#initramfs)
*   [12 initrd](#initrd)
*   [13 KISS](#KISS)
*   [14 makepkg](#makepkg)
*   [15 namcap](#namcap)
*   [16 package](#package)
*   [17 Package maintainer](#Package_maintainer)
*   [18 pacman](#pacman)
*   [19 PKGBUILD](#PKGBUILD)
*   [20 repository/repo](#repository/repo)
*   [21 RTFM](#RTFM)
*   [22 testing/[testing]](#testing/[testing])
*   [23 The Arch Way](#The_Arch_Way)
*   [24 TU, Trusted User](#TU,_Trusted_User)
*   [25 udev](#udev)
*   [26 wiki](#wiki)

## ABS

ABS significa [Arch Build System](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") y puede usarse para:

*   La creación de nuevos paquetes para software que aún no dispone de ellos.
*   Personalizar/modificar paquetes existentes para satisfacer sus necesidades:
*   Habilitar/deshabilitar opciones de tiempo de compilación.
*   Aplicar cambios de código fuente a través de parches.
*   Reconstruir todo su sistema usando marcadores, "a la Gentoo"
*   Hacer que los módulos del núcleo funcionen con su núcleo personalizado.

ABS no es necesario para usar Arch Linux, pero es útil.

## Arch Linux

Esto puede referirse a:

*   **Arch Linux**
*   **Arch** (Linux implícito)
*   **archlinux** (nombre UNIX)

Archlinux, ArchLinux, archLinux, aRcHlInUx, etc. son todas ellas raras y más extrañas mutaciones.

Oficialmente, el 'Arch' en "Arch Linux" se pronuncia /ˈɑrtʃ/ como en "archienemigo" o "archivo". No "Ark".

## Arch Linux Archive

El [Arch Linux Archive](/index.php/Arch_Linux_Archive_(Espa%C3%B1ol) "Arch Linux Archive (Español)") (ALA), formalmente conocido como *Arch Linux Rollback Machine* (ARM), almacena instantáneas de repositorios oficiales, imágenes ISO y archivos de arranque a lo largo del tiempo.

## AUR

El [Arch User Repository](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)") (repositorio de usuarios de Arch), es un repositorio manejado por la comunidad de usuarios de Arch. Contiene descripciones de paquetes ([PKGBUILDs](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)")) que le permiten compilar un paquete a partir de código fuente con [makepkg](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)") y luego instalarlo vía [pacman](/index.php/Pacman#Additional_commands_(Español) "Pacman"). El AUR fue creado para organizar y compartir nuevos paquetes de la comunidad y para ayudar a acelerar la inclusión de paquetes populares en el repositorio [community](/index.php/Community_repository_(Espa%C3%B1ol) "Community repository (Español)").

Una buena cantidad de paquetes nuevos que ingresan a los repositorios oficiales nacen en el AUR. En la AUR, los usuarios pueden contribuir con sus propias compilaciones de paquetes (PKGBUILD y archivos relacionados). La comunidad AUR tiene la capacidad de votar a favor o en contra de los paquetes en AUR. Si un paquete se vuelve lo suficientemente popular — siempre que tenga una licencia compatible y una buena técnica de empaque — puede incluírse en el repositorio *community* (accesible directamente a través de [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") o [abs](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)")).

Puede acceder [aquí](https://aur.archlinux.org) al repositorio comunitario de usuarios de ArchLinux.

## bbs

**B**ulletin **b**oard **b**ystem (sistema de tablón de anuncios), aunque en el caso de Arch es solo el foro de soporte ubicado en [https://bbs.archlinux.org](https://bbs.archlinux.org).

## communitiy/[community]

El repositorio [community](/index.php/Official_repositories_(Espa%C3%B1ol)#community "Official repositories (Español)") es donde los paquetes prefabricados se encuentran disponibles gracias a los [**usuarios de confianza**](/index.php/Trusted_Users_(Espa%C3%B1ol) "Trusted Users (Español)") (UC). Una gran mayoría de los paquetes de *community*, provienen del [AUR](/index.php/AUR "AUR").

**Nota:** (del traductor) Para acceder a este repositorio desde tu sistema, descoméntalo en el archivo `/etc/pacman.conf`.

## core/[core]

El repositorio [core](/index.php/Official_repositories_(Espa%C3%B1ol)#core "Official repositories (Español)") contiene los pocos paquetes necesarios para un sistema Arch. Tiene todo lo necesario para disponer de un sistema de línea de comandos funcional.

## custom/user repository

Cualquiera puede crear un repositorio y dejarlo *online* a disposición de otros usuarios. Para crearlo, se necesitan una serie de paquetes y un archivo de base de datos compatible con [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") para los mismos. Hospede sus archivos en algún servidor y cualquier persona podrá utilizarlo como un repositorio más.

Véase [repositorio local personalizado](/index.php/Pacman_(Espa%C3%B1ol)/Tips_and_tricks_(Espa%C3%B1ol)#Repositorio_local_personalizado "Pacman (Español)/Tips and tricks (Español)").

## developer

Desarrollador, semidiós trabajando para la mejora de Arch sin afán de lucro. Los [Desarroladores](https://www.archlinux.org/people/developers/) sólo son superados por Judd Vinet y Aaron Griffin, quienes a su vez son superados por los [tacos](https://es.wikipedia.org/wiki/Taco).

## extra/[extra]

El conjunto de paquetes oficiales de Arch está bastante simplificado, sin embargo lo complementamos con un repositorio [«extra»](/index.php/Official_repositories_(Espa%C3%B1ol)#extra "Official repositories (Español)") más grande y completo que contiene mucho del material que nunca llegó a nuestro grupo de paquetes esenciales. Este repositorio está en constante crecimiento con la ayuda de paquetes enviados por nuestra sólida comunidad. Aquí es donde se encuentran entornos de escritorio, gestores de ventanas y programas comunes.

## initramfs

Véase [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)")

## initrd

Obsoleto. Hoy en día se usa frecuentemente como sinónimo de *initramfs*.

## KISS

Acrónimo de *Keep It Simple, Stupid* (mantenlo simple, idiota). La simplicidad es un principio fundamental que Arch Linux procura mantener.

## makepkg

[Makepg](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)") creará paquetes para usted y leerá los metadatos requeridos por un archivo [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)").
Todo lo que necesita es una plataforma Linux con capacidad de compilación, [curl](https://www.archlinux.org/packages/?name=curl) y algunos scripts. La ventaja de una compilación basada en script es que realmente solo haces el trabajo una vez. En cuanto está disponible el script de compilación para un paquete, solo se necesita ejecutar *makepkg* y este hará el resto: descargar y validar los archivos fuente, verificar las dependencias, configurar los ajustes de tiempo de compilación, compilar el paquete, instalarlo en una raíz temporal, hacer personalizaciones, generar metainformación y empaquetar todo para que [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") lo use.

## namcap

[Namcap](/index.php?title=Namcap_(Espa%C3%B1ol)&action=edit&redlink=1 "Namcap (Español) (page does not exist)") es una utilidad de análisis de paquetes que busca problemas con los paquetes de Arch Linux o sus archivos [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)"). Puede aplicar reglas a la lista de archivos, a los propios archivos o a archivos PKGBUILD individuales.

Las reglas devuelven listas de mensajes. Cada mensaje puede ser uno de estos tres tipos: error, advertencia o información (piense en ellos como notas o comentarios). Los errores (designados por 'E:') son avisos que namcap está muy seguro de que están mal y deben corregirse. Las advertencias (designadas por 'W:') son cosas que namcap cree que deberían cambiarse, pero si sabe lo que está haciendo, puede dejarlas. La información (denominada 'I:') solo se muestra cuando se utiliza el argumento de información. Los mensajes informativos brindan información que podría ser útil pero que no es algo que deba cambiarse.

## package

Un paquete es un archivo que contiene:

*   Todos los archivos (compilados) de una aplicación.
*   Metadatos acerca de la aplicación, como su nombre, versión, dependencias, ...
*   Archivos de instalación y directivas de [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")
*   Opcionalmente archivos extra para hacer su vida más fácil, tal como un script de inico/parada.

El administrador de paquetes de Arch *pacman* puede instalar, actualizar y eliminar esos paquetes. El uso de paquetes en lugar de compilar e instalar programas tiene varios beneficios:

*   Fácilmente actualizable: pacman actualizará paquetes existentes tan pronto como haya actualizaciones disponibles.
*   Comprobación de dependencias: pacman maneja las dependencias por usted, sólo necesita especificar el programa y pacman lo instala junto a cualquier otro programa que necesite.
*   Eliminación limpia: pacman conserva una lista de todos los archivos de un paquete. De ese modo, nunca quedan archvos olvidados o a la deriva cuando decidimos suprimir un paquete.

**Note:** Las diferentes distribuciones GNU/Linux usan distintos paquetes y otros gestores para estos, entendiéndose que no podemos utilizar pacman para instalar, por ejemplo, un paquete Debian en Arch.

## Package maintainer

Véase [Mantenedor de paquetes](/index.php/Roles_(Espa%C3%B1ol) "Roles (Español)").

## pacman

[Pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [gestor de paquetes](https://en.wikipedia.org/wiki/es:Sistema_de_gesti%C3%B3n_de_paquetes fácil de usar. El objetivo de *pacman* es hacer posible administrar fácilmente los paquetes, ya sean de los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") o de las propias compilaciones del usuario.

Pacman mantiene el sistema actualizado al sincronizar las listas de paquetes con el servidor maestro. Este modelo de servidor/cliente también permite al usuario descargar/instalar paquetes con un comando simple, completo con todas las dependencias requeridas.

N.B.: Pacman fue escrito por Judd Vinet, el creador de Arch Linux. También se usa como una herramienta de administración de paquetes por otras distribuciones, como FrugalWare, Rubix, UfficioZero (en Italia, basado en Ubuntu) y, por supuesto, [distribuciones basadas en Arch](/index.php/Arch-based_distributions_(Espa%C3%B1ol) "Arch-based distributions (Español)") como Archie y AEGIS.

## PKGBUILD

Los [PKGBUILDSs](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") son pequeños scripts que se usan para compilar paquetes de Arch Linux. Ver [Creating packages_(Español)](/index.php/Creating_packages_(Espa%C3%B1ol) "Creating packages (Español)") para más detalles.

## repository/repo

El repositorio posee los paquetes pre-compilados de (normalmente) uno o más [PKGBUILDs](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)"). Los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") están divididos en diferentes secciones para facilitar su mantenimiento. Pacman usa estos repositorios para buscar paquetes e instalarlos. Un repositorio puede ser local (por ejemplo en su propio PC) o remoto (los paquetes se descargan desde un servidor externo antes de ser instalados).

## RTFM

[RTFM](https://en.wikipedia.org/wiki/RTFM "wikipedia:RTFM"), «**R**ead **T**he **F**ine **M**anual» (Lee el buen manual). Con este simple mensaje se responde a muchos usuarios novatos de Linux/Arch quienes preguntan sobre alguna funcionalidad de un programa cuando está claramente definida en su propio manual.

**Nota:** (del traductor) Hasta hace poco tiempo, constaba en esta página la expresión primigenia «**R**ead **T**he **F**ucking **M**anual», literalmente: *Lee el puto/jodido/maldito manual*. Al parecer, debido a imposiciones de corrección política, se está intentando suavizar estas y algunas otras expresiones que podrían resultar duras u ofensivas. Sin embargo también debemos considerar que por razones de memoria histórica y rigor informativo, no debe omitirse en ningún caso el origen expresivo de este o cualquier otro acrónimo.

A menudo se usa cuando un usuario no intenta encontrar una solución al problema por sí mismo. Si alguien le dice esto, no está tratando de ofenderle; simplemente está frustrado debido a su falta de esfuerzo.

Lo mejor que puede hacer si le dicen que haga esto es leer la página del manual.

*   Para leer la página del manual del programa para un programa en particular llamado PROGRAM-NAME, escriba esto en la línea de comando: `man PROGRAM-NAME`.

Si no encuentra la respuesta a su pregunta en el manual del programa, hay más formas de encontrarla. Usted puede:

*   buscar en [wiki](/index.php/Special:Search "Special:Search")
*   buscar en [wiki](/index.php/Special:Search "Special:Search")
*   buscar en [forum](https://bbs.archlinux.org)
*   buscar en [mailing lists](https://www.google.com/#hl=en&q=arch+site:archlinux.org%2Fpipermail%2F)
*   buscar en [web](https://www.google.com)

## testing/[testing]

Este es el repositorio donde se almacena la mayoría de paquetes/actualizaciones antes de su publicación en los repositorios principales, de modo que allí pueden ser probados en busca de errores o cualquier problema que se encuentre. Por defecto se encuentra deshabilitado pero se puede activar en `/etc/pacman.conf`

## The Arch Way

El término no oficial usado tradicionalmente para referirse a los [principios de ArchLinux](/index.php/Arch_Linux#Principles_(Español) "Arch Linux") fundamentales.

## TU, Trusted User

Un [usuario de confianza](/index.php/Trusted_Users_(Espa%C3%B1ol) "Trusted Users (Español)") (UC) es alguien que mantiene el AUR y el repositorio *community*.

Los usuarios de confianza pueden mover un paquete al repositorio community si ha sido votado como popular.

Los UC son elegidos por mayoría de votos entre los UC existentes.

Los usuarios de confianza velan por las [AUR Trusted User Guidelines](/index.php/AUR_Trusted_User_Guidelines_(Espa%C3%B1ol) "AUR Trusted User Guidelines (Español)") y las [TU by-laws](https://aur.archlinux.org/trusted-user/TUbylaws.html)

## udev

[udev](/index.php/Udev "Udev") proporciona un directorio dinámico de dispositivos que contiene sólo los archivos para dispositivos realmente presentes. Crea o elimina archivos de nodo de dispositivo en el directorio `/dev`, o renombra las interfaces de red.

Por lo general, udev se ejecuta como udevd(8) y recibe *uevents* directamente del kernel si se agrega/elimina un dispositivo al/del sistema.

Si udev recibe un evento de dispositivo, hace coincidir sus reglas configuradas con los atributos de dispositivo disponibles proporcionados en [sysfs](https://en.wikipedia.org/wiki/sysfs "wikipedia:sysfs") para identificar el dispositivo. Las reglas que coinciden pueden proporcionar información adicional del dispositivo o especificar un nombre de nodo del dispositivo y múltiples nombres de enlaces simbólicos e indicar a udev que ejecute programas adicionales como parte del manejo de eventos del dispositivo.

## [wiki](https://en.wikipedia.org/wiki/Wiki "wikipedia:Wiki")

[Esto!](/index.php/Main_page_(Espa%C3%B1ol) "Main page (Español)") Un lugar donde encontrar documentación sobre Arch Linux. Cualquiera puede añadir y modificar la documentación.