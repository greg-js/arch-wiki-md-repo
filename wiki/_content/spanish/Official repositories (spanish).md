Artículos relacionados

*   [Mirrors (Español)](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)")
*   [Arch User Repository (Español)](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)")
*   [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories")
*   [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")
*   [makepkg](/index.php/Makepkg "Makepkg")
*   [pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")
*   [Arch Build System (Español)](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)")

Un [repositorio de software](https://en.wikipedia.org/wiki/es:Repositorio "wikipedia:es:Repositorio") es un lugar donde se almacenan los paquetes de software, los cuales pueden ser recuperados e instalados en un ordenador. Los [mantenedores de paquetes](/index.php/Package_Maintainer "Package Maintainer") de Arch Linux (y los desarrolladores [Trusted Users](/index.php/Trusted_Users "Trusted Users")) mantienen una serie de repositorios oficiales que contienen paquetes de software, desde el más esencial al extra, a los que se puede acceder fácilmente mediante [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)"). En este artículo se describen estos repositorios con apoyo oficial.

## Contents

*   [1 Antecedentes históricos](#Antecedentes_hist.C3.B3ricos)
*   [2 [core]](#.5Bcore.5D)
*   [3 [extra]](#.5Bextra.5D)
*   [4 [community]](#.5Bcommunity.5D)
*   [5 [multilib]](#.5Bmultilib.5D)
*   [6 [testing]](#.5Btesting.5D)
*   [7 [community-testing]](#.5Bcommunity-testing.5D)
*   [8 [multilib-testing]](#.5Bmultilib-testing.5D)

## Antecedentes históricos

La mayoría de los grupos de repositorios existen por razones históricas. Originalmente, cuando Arch Linux era usada por muy pocos usuarios, solo había un depósito conocido como *[official]* (ahora **[core]**). Este repositorio contenía básicamente las aplicaciones preferidas de Judd Vinet. Cada grupo estaba diseñado para contener un programa para cada tipo de aplicación: un entorno de escritorio, un navegador, etc.

En aquel entonces existían algunos usuarios a los que no les gustaba las selecciones de Judd, y dado que el [ABS](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") era fácil de usar, comenzaron a crear sus propios paquetes. Estos paquetes fueron incorporados a un repositorio llamado [unofficial] y fueron mantenidos por algunos desarrolladores de Judd. Con el tiempo estos dos repositorios consiguieron apoyo por parte de todos los desarrolladores. Como los nombres [oficial] y [unoficial] ya no reflejaban su verdadero propósito fueron renombrados a [current] y [extra] en torno a la versión 0.5\.

Poco tiempo después del lanzamiento de la versión 2007.08.01, [current] fue renombrado a [core] para prevenir confusiones sobre lo que contenía. Los repositorios ahora se encuentran atendidos por igual por los desarrolladores y la comunidad, pero [core] tiene algunas diferencias, la principal es que los paquetes para el CD de instalación y las liberaciones de instantáneas (*«snapshots»*) son tomados solo de [core]. Este repositorio aun provee un completo sistema Linux, pero puede no ser el sistema que desee.

En algún momento entre versión 0.5 y la 0.6, se descubrió que existían muchos paquetes que los desarrolladores no querían mantener. Uno de los desarrolladores (Xentac) preparó el «Repositorio de Usuarios de Confianza» (*Trusted User Repositories*) que era básicamente un repositorio no oficial en el cual los usuarios de confianza podían colocar paquetes que ellos hubieran creado. Existió un repositorio [staging], donde los paquetes podían ser derivados a uno de los repositorios oficiales mantenidos por los desarrolladores de Arch Linux, pero a parte de esto, los desarrolladores y usuarios de confianza se han mantenidos más o menos distintos.

Este sistema funciono por un tiempo, pero luego los Usuarios de Confianza comenzaron a descuidar su repositorio, mientras que los usuarios normales deseaban compartir sus paquetes. Esto llevo al desarrollo del repositorio [AUR](https://aur.archlinux.org/). Los Usuarios de Confianza (*«Trusted Users»*) fueron congregados en un grupo más unido y ahora mantienen colectivamente el repositorio **[community]**. Los usuarios de confianza aun son un grupo separado de los desarrolladores de Arch Linux y no existe mucha comunicación entre ambos colectivos. Sin embargo, los paquetes populares aun siguen siendo derivados desde [community] a **[extra]**, en ocasiones. El repositorio [AUR](https://aur.archlinux.org/) también permite a usuarios que no tienen la clasificación de «Trusted Users» enviar PKGBUILDs.

Después de [numerosos problemas](https://www.archlinux.org/news/please-avoid-kernel-261614-1/) causados por un kernel introducido en **[core]** , fue presentada la norma «política del visto bueno del núcleo» (*«core signoff policy»*) . Desde entonces, todas las actualizaciones de los paquetes depositados en [core] tienen que ser presentados primero a través del repositorio **[testing]** , y únicamente después de varios *vistos buenos* («signoffs») de otros desarrolladores se les permite moverse a core. Con el tiempo, se observó que algunos paquetes destinados a [core] tenían poco uso, para este tipo de paquetes el visto bueno de los usuarios o, incluso, la falta de informes de errores, se aceptó oficiosamente como criterio para admitirlos.

A finales 2009, principios de 2010, con la llegada de unos nuevos sistemas de archivos y el deseo de apoyarlos durante la instalación, junto con la conciencia de que [core] nunca se definió claramente (simplemente «paquetes importantes, seleccionados por los desarrolladores»), los repositorios recibieron una descripción más precisa (véase más adelante).

## [core]

Este depósito se encuentra en `.../core/os/` desde su mirror favorito.

Cuenta con unos requisitos de calidad muy estrictos:

*   Los desarrolladores y/o usuarios necesitan dar el visto bueno para las actualizaciones de los paquetes antes de que estos últimos sean aceptados.

*   Para paquetes con poco uso, una exposición razonable (es decir, el informe de los usuarios acerca de la actualización, peticiones de autoriazaciones, período de pruebas de hasta una semana, dependiendo de la severidad del cambio, la falta de informes de fallos pendientes, junto con el visto bueno implícito del mantenedor del paquete) es suficiente.

Contiene paquetes que:

*   Son necesarios para arrancar cualquier tipo de sistema de apoyo de Arch.
*   Pueden ser necesario para conectarse a Internet.
*   Son esenciales para la compilación de paquetes.
*   Pueden gestionar y verificar/reparar sistemas de archivos compatibles.
*   Paquetes necesarios en la primera fase del proceso de instalación aunque sean muy exclusivos dado que la mayoría de los usuarios no los van a necesitar (por ejemplo, [openssh](https://www.archlinux.org/packages/?name=openssh)).
*   Son dependencias (pero no necesariamente makedepends) de los anteriores.

**Nota:** Este depósito era incluido en los soportes de instalación, por lo que podía construirse un sistema de base totalmente funcional sin acceso a Internet. Esto ya no es posible. El acceso a Internet se necesario ahora con el fin de instalar un nuevo sistema. Véase [esto](/index.php/Pacman_tips#Installing_packages_from_a_CD.2FDVD_or_USB_stick "Pacman tips") si desea crear un repositorio local con paquetes desde [core] o desde cualquiera de los otros repositorios.

## [extra]

Este depósito se encuentra en `.../extra/os/` desde su mirror favorito.

Contiene todos los paquetes que no se ajustan a los requisitos para estar en [core]. Por ejemplo: Xorg, gestores de ventanas, navegadores Web, reproductores multimedia, herramientas para trabajar con lenguajes como Python y Ruby, y mucho otros.

## [community]

Este depósito se encuentra en `.../community/os/` con su mirror favorito.

Contiene los paquetes provenientes del repositorio [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") que obtivieron los votos suficientes para ser adoptadas por un [Usuario de Confianza](/index.php/Trusted_Users "Trusted Users").

## [multilib]

Este depósito se encuentra en `.../multilib/os/` desde su mirror favorito.

Contiene el software de 32 bits y las bibliotecas que se pueden utilizar para ejecutar y desarrollar aplicaciones de 32 bits en instalaciones de 64 bits (por ejemplo, [wine](https://www.archlinux.org/packages/?name=wine), [skype](https://aur.archlinux.org/packages/skype/), etc.).

Para obtener más información, véase [Multilib](/index.php/Multilib "Multilib").

## [testing]

**Advertencia:** Tenga cuidado al activar el repositorio [testing]. Su sistema puede volverse inestable después de realizar una actualización. Solo los usuarios experimentados que saben cómo hacer frente a una potencial rotura del sistema deben utilizarlo.

Este depósito se encuentra en `.../testing/os/` desde su mirror favorito.

Es especial porque contiene paquetes que son candidatos para los repositorios [core] o [extra].

Los nuevos paquetes entran en [testing] si:

*   Se sospecha que puedan romper algo con una actualización y necesitan ser probado en primer lugar.

*   Se requieren otros paquetes que ser reconstruido. En este caso, todos los paquetes que se necesitan para la recompilación se ponen en [testing] primero y cuando se completan todas las recompilaciones, se les traslada de nuevo a los otros repositorios.

Este es el único depósito que puede tener colisiones de nombres con cualquiera de los repositorios oficiales. Si está habilitado, tiene que ser el primer repositorio listado en su archivo `/etc/pacman.conf`.

Tenga en cuenta que no se trata de un repositorio que contenga «la más reciente» de las versiones de los paquetes. Parte de su propósito es mantener actualizaciones de paquetes que tienen el potencial de **causar la rotura del sistema**, ya sea por ser parte del conjunto de paquetes contenidos en [core], o por ser crítico de otra manera. Como tal, los usuarios del repositorio [testing] son **fuertemente alentados** a suscribirse a la lista de correo de [arch-dev-public](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public), mirar el [Fórum del Repositorio [testing](https://bbs.archlinux.org/viewforum.php?id=49)], y a [informar](https://bugs.archlinux.org/) de todos los fallos.

Si activa [testing], también debe activar [community-testing].

## [community-testing]

Este repositorio es como el repositorio [testing] pero con los paquetes que son candidatos para el repositorio [community].

Si lo activa, también tiene que activar [testing].

## [multilib-testing]

Este repositorio es como el repositorio [testing] pero con los paquetes que son candidatos para el repositorio [multilib].

Si lo activa, también tiene que activar [testing].