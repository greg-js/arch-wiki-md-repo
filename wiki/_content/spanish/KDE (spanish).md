KDE es un proyecto de software que comprende actualmente un [desktop environment](/index.php/Desktop_environment "Desktop environment") conocido como Plasma, una colección de bibliotecas y Frameworks (KDE Frameworks) y varias aplicaciones (KDE Applications). KDE upstream tiene un [UserBase wiki](https://userbase.kde.org/) bien mantenido. Allí se puede encontrar información detallada sobre la mayoría de las aplicaciones de KDE.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Plasma Desktop](#Plasma_Desktop)
    *   [1.2 Aplicaciones de KDE y paquetes de idiomas](#Aplicaciones_de_KDE_y_paquetes_de_idiomas)
    *   [1.3 Lanzamientos inestables](#Lanzamientos_inestables)
*   [2 Iniciar Plasma](#Iniciar_Plasma)
    *   [2.1 Gráficamente](#Gr.C3.A1ficamente)
    *   [2.2 Manual](#Manual)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Personalización](#Personalizaci.C3.B3n)
        *   [3.1.1 Escritorio Plasma](#Escritorio_Plasma)
            *   [3.1.1.1 Temas](#Temas)
                *   [3.1.1.1.1 Qt y GTK+ Aplicaciones y Apariencias](#Qt_y_GTK.2B_Aplicaciones_y_Apariencias)
*   [4 EN CONSTRUCCIÓN](#EN_CONSTRUCCI.C3.93N)
    *   [4.1 Widgets](#Widgets)
    *   [4.2 Decoración de ventanas](#Decoraci.C3.B3n_de_ventanas)
    *   [4.3 Integración de KDE 4 con aplicaciones GTK](#Integraci.C3.B3n_de_KDE_4_con_aplicaciones_GTK)
        *   [4.3.1 Procedimiento automático](#Procedimiento_autom.C3.A1tico)
        *   [4.3.2 Procedimiento manual](#Procedimiento_manual)
        *   [4.3.3 Iconos](#Iconos)
    *   [4.4 Temas de iconos](#Temas_de_iconos)
    *   [4.5 Logo de Arch Linux en el menu de Kicker](#Logo_de_Arch_Linux_en_el_menu_de_Kicker)
    *   [4.6 Fuentes](#Fuentes)
    *   [4.7 Eficacia de espacio](#Eficacia_de_espacio)
        *   [4.7.1 Todo tipo de * barras](#Todo_tipo_de_.2A_barras)
        *   [4.7.2 Plasma](#Plasma)
        *   [4.7.3 KWin](#KWin)
    *   [4.8 NetworkManager](#NetworkManager)
    *   [4.9 Impresión](#Impresi.C3.B3n)
    *   [4.10 Soporte Samba/Windows](#Soporte_Samba.2FWindows)
    *   [4.11 Powersaving](#Powersaving)
        *   [4.11.1 Como habilitar Cpufreq](#Como_habilitar_Cpufreq)
    *   [4.12 Registro de cambios en archivos y directorios](#Registro_de_cambios_en_archivos_y_directorios)
    *   [4.13 Administración del sistema](#Administraci.C3.B3n_del_sistema)
        *   [4.13.1 Establecer distribución del teclado](#Establecer_distribuci.C3.B3n_del_teclado)
            *   [4.13.1.1 Terminar servidor Xorg mediante atajo de teclado de KDE](#Terminar_servidor_Xorg_mediante_atajo_de_teclado_de_KDE)
    *   [4.14 Problemas conocidos](#Problemas_conocidos)
    *   [4.15 KDEmod](#KDEmod)
    *   [4.16 Soporte para Java](#Soporte_para_Java)
    *   [4.17 Bajando de versión a kdemod3 o kde3-legacy desde KDE 4.3](#Bajando_de_versi.C3.B3n_a_kdemod3_o_kde3-legacy_desde_KDE_4.3)
    *   [4.18 Archivo Xserver de KDM](#Archivo_Xserver_de_KDM)
    *   [4.19 GPG y SSH](#GPG_y_SSH)
    *   [4.20 Kdebindings](#Kdebindings)
    *   [4.21 Cambiando el DPI para KDM](#Cambiando_el_DPI_para_KDM)
    *   [4.22 Bugs y errores](#Bugs_y_errores)
    *   [4.23 Enlaces externos](#Enlaces_externos)

## Instalación

### Plasma Desktop

Antes de instalar Plasma, asegúrese de tener una instalación funcional de [Xorg](/index.php/Xorg "Xorg") en su sistema.

Instale -[Install](/index.php/Install "Install")- el metapaquete [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) o el grupo [plasma](https://www.archlinux.org/groups/x86_64/plasma/). Para conocer las diferencias entre [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) y el grupo [plasma](https://www.archlinux.org/groups/x86_64/plasma/) refierace a [Creating packages#Meta packages and groups](/index.php/Creating_packages#Meta_packages_and_groups "Creating packages"). Alternativamente, para una instalación de Plasma mínima, instale el paquete [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop).

Para habilitar el soporte para [Wayland](/index.php/Wayland "Wayland") en Plasma, también instale el paquete [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session).

### Aplicaciones de KDE y paquetes de idiomas

Para instalar el conjunto completo de aplicaciones KDE, instale el grupo [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) o el metapaquete [kde-applications-meta](https://www.archlinux.org/packages/?name=kde-applications-meta). Tenga en cuenta que esto sólo instalará aplicaciones, no instalará ninguna versión de Plasma.

La mayoría de los paquetes de KDE contienen sus propias traducciones. La excepción son los paquetes KDE-4 basicos de kde-applications. Si necesita archivos de idioma para estos paquetes, instale `kde-l10n-***yourlanguagehere***` (e.g. [kde-l10n-de](https://www.archlinux.org/packages/?name=kde-l10n-de) para el idioma alemán). Para obtener una lista completa de idiomas disponibles, consulte el paquete dividido de [kde-l10n split package](https://www.archlinux.org/packages/extra/any/kde-l10n/)..

### Lanzamientos inestables

Vea [Official repositories#kde-unstable](/index.php/Official_repositories#kde-unstable "Official repositories")

## Iniciar Plasma

**Nota:** Aunque es posible lanzar Plasma en [Wayland](/index.php/Wayland "Wayland"), hay algunas características que faltan y problemas conocidos con Plasma 5.10\. Vea [Plasma 5.10 Errata](https://community.kde.org/Plasma/5.10_Errata#Wayland) para una lista de problemas y el [Plasma on Wayland workboard](https://phabricator.kde.org/project/board/99/) para el estado actual de desarrollo. Utilice [Xorg](/index.php/Xorg "Xorg") para la experiencia más completa y estable.

Plasma se puede iniciar de forma gráfica, utilizando un [display manager](/index.php/Display_manager "Display manager"), o manualmente desde la consola.

### Gráficamente

**Sugerencia:** Para integrar mejor [SDDM](/index.php/SDDM "SDDM") con Plasma, se recomienda (forzar) seleccionar el tema breeze. La configuración relacionada se encuentra en Configuración del sistema> Inicio y apagado. Ver configuraciones del tema [SDDM#Theme settings](/index.php/SDDM#Theme_settings "SDDM").

Uso de un gestor de visualización [Display manager](/index.php/Display_manager "Display manager"):

*   Seleccione *Plasma* para iniciar una nueva sesión en [Xorg](/index.php/Xorg "Xorg").
*   Instale [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session) y seleccione *Plasma (Wayland)* para lanzar una nueva sesión en [Wayland](/index.php/Wayland "Wayland").

**Nota:** La implementación del controlador propietario de [NVIDIA](/index.php/NVIDIA "NVIDIA") para Wayland requiere EGLStreams. KDE no ha implementado EGLStreams en su implementación Wayland [implementation](https://blog.martin-graesslin.com/blog/2016/09/to-eglstream-or-not).

Las soluciones siguientes están disponibles:

*   Uso del controlador Nouveau.
*   Uso de la sesión (predeterminada) de Xorg.

### Manual

Para iniciar Plasma con [xinit](/index.php/Xinit "Xinit")/*startx*, añada `exec startkde` a su archivo `.xinitrc`. Si desea iniciar Xorg en el inicio de sesión, consulte arrancar X al iniciar sesión [Start X at login](/index.php/Start_X_at_login "Start X at login"). Para iniciar una sesión de Plasma en Wayland desde una consola, ejecute `startplasmacompositor`.

## Configuración

La mayoría de las configuraciones para las aplicaciones de KDE 4 se almacenan en la carpeta oculta `~/.kde4` y otras también en la carpeta oculta, `~/.config` Sin embargo, la configuración de KDE se realiza principalmente a través de la *'aplicación' Configuración del sistema* . Se puede iniciar desde un terminal ejecutando *systemsettings* .

**Nota:** La configuración de KDE se realiza principalmente en ' **Configuración del sistema '**. Hay también algunas otras opciones disponibles para el escritorio en 'Preferencias de escritorio' cuando haces click derecho en el escritorio.

Las aplicaciones de Frameworks 5 (espacio de plasma 5) pueden utilizar la configuración de KDE 4 sin embargo, puede esperar que los archivos de configuración se encuentran en diferentes lugares. Para permitir que las aplicaciones de frameworks 5 se ejecutan en KDE 4, y para compartir las mismas configuraciones, y compatibilidad se hacen enlaces simbólicos, de las nuevas configuraciones a .KDE4\. Por ejemplo:

*   Perfiles de Konsole de `~/.kde4/share/apps/konsole` a `~ /.local/share/Konsole/`
*   Apariencia de la aplicación de `~/.kde4/share/config/kdeglobals` a `~/.config/kdeglobals`

### Personalización

#### Escritorio Plasma

##### Temas

**Nota:** Si en algunos casos el tema del cursor plasma es incorrecta, consulte el siguiente [mensaje del foro](https://bbs.archlinux.org/viewtopic.php?pid=1533071#p1533071) para una solución

En [temas de Plasma](http://kde-look.org/index.php?xcontentmode=76) hay vista de de aspecto de los paneles y plasmoides. Para facilitar la instalación de todo el sistema, algunos de estos temas están disponibles en los repositorios oficiales y en [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmatheme&do_Search=Go).

La forma más fácil de instalar temas es ir a través de preferencias del sistema==Aspecto/temas del espacio de trabajo== Tema de escritorio:

```
 Tema del espacio de trabajo > Tema de escritorio > Obtener nuevos temas

```

Esto presentará un buen principio y fin para [kde-look.org](http://www.kde-look.org/) que permita instalar, des-instalar o actualizar los scripts plasmoides de terceros con literalmente, un sólo clic.

La pantallas de inicio y de bloqueo no están disponibles las manera de personalizar estas pantallas. Por lo que hay que modificar el tema original que se encuentra en `/usr/share/plasma/look-and-feel/`. ver [este hilo](https://www.kubuntuforums.net/showthread.php?67599-Plasma-5-background-images&s=59832dc20e5bfc2948dbb591d8453f61) en los foros de Kubuntu.

Tome nota que [SDDM](/index.php/SDDM "SDDM") gestor de inicio de sesión no es parte de este tema.

###### Qt y GTK+ Aplicaciones y Apariencias

**Tip:** Para que Qt y GTK tengan consistencia con el tema, ver [Uniform look for Qt and GTK applications (Español)](/index.php/Uniform_look_for_Qt_and_GTK_applications_(Espa%C3%B1ol) "Uniform look for Qt and GTK applications (Español)").
, y/o en ingles en caso de estar des-actualizada

	Qt4

Para aplicaciones Qt4 oara que tengan una apariencia consistente, es necesario instalar [breeze-kde4](https://www.archlinux.org/packages/?name=breeze-kde4) y luego recoger Breeze como interfaz gráfica de usuario Style en `qtconfig-qt4`.

# EN CONSTRUCCIÓN

Esta pagina esta en construcción, y por lo pronto no borro lo que estaba en la wiki, por lo que estos artículos siguientes pueden estar des-actualizados

##### Widgets

Los Plasmoides son pequeños script o código de las aplicaciones de KDE que mejoran la funcionalidad de tu escritorio. Existen dos tipos, plasmoides scripts y plasmoides binarios.

Los plasmoides binarios deben ser instalados usando PKGBUILDS desde [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmoid&do_Search=Go&PP=25&SO=d&SB=v). O escribiendo tu propio PKGBUILD.

La forma más fácil de instalar plasmoides scripts es haciendo clic derecho sobre un panel o en el escritorio:

```
Añadir elementos graficos -> Obtener nuevos elementos -> Descargar Widgets

```

Esto presentará una interfaz agradable para [kde-look.org](http://www.kde-look.org/) y te permite (des)instalar o actualizar los plasmoides script de terceros con un solo clic.

La mayoría de plasmoides no se crean de forma oficial por los desarrolladores de KDE. También puedes tratar de instalar widgets de Mac OS X , Microsoft Windows Vista/7, Google, e incluso widgets de SuperKaramba.

#### Decoración de ventanas

La[Decoración de ventanas](http://kde-look.org/index.php?xcontentmode=75) puede cambiarse en:

```
Preferencias del sistema -> Apariencia del espacio de trabajo -> Decoración de ventanas

```

Aquí también se pueden descargar e instalar más temas con un solo clic y podemos encontrar algunos disponibles en [AUR](https://aur.archlinux.org/packages.php?O=0&K=kdestyle&do_Search=Go&PP=25&SO=d&SB=v).

#### Integración de KDE 4 con aplicaciones GTK

Para integrar mejor los temas de GTK y KDE4, puedes usar **QtCurve**

```
 pacman -S qtcurve-gtk2 qtcurve-kde4 gtk-kde4

```

o **oxygen-gtk**

```
 pacman -S oxygen-gtk

```

o puede descargar un tema GTK que coincida con su tema de KDE [aquí](http://kde-look.org/content/show.php?content=103741). Este tema se parece al Oxygen original y se actualiza con frecuencia.

##### Procedimiento automático

Para cambiar el tema GTK a QtCurve o alguna otra cosa están disponible las siguientes aplicaciones:

```
 pacman -S lxappearance
 pacman -S gtk-theme-switch2
 pacman -S gtk-chtheme

```

A continuación, cambie al tema de su elección en la aplicación correspondiente:

```
lxappearance
gtk-theme-switch2
gtk-chtheme

```

##### Procedimiento manual

Para cambiar manualmente el tema GTK al QtCurve, tiene que crear el archivo `~/.gtkrc-2.0-kde4` con el siguiente contenido:

```
include "/usr/share/themes/QtCurve/gtk-2.0/gtkrc"
include "/etc/gtk-2.0/gtkrc"

style "user-font"
{
    font_name="Sans Serif"
}
widget_class "*" style "user-font" 
gtk-theme-name="QtCurve"

```

A continuación, debe crear el vínculo simbólico `~/.gtkrc-2.0`:

```
ln -s .gtkrc-2.0-kde4 .gtkrc-2.0

```

Si desea especificar una fuente, puede añadir (y adaptar) la siguiente línea al archivo:

```
 gtk-font-name="Sans Serif 9"

```

##### Iconos

Si utiliza los iconos oxygen y desea un aspecto coherente en los cuadros de diálogo Abrir y guardar de GTK, puede instalar [oxygenrefit2](https://aur.archlinux.org/packages.php?O=0&K=oxygenrefit2-icon-theme&do_Search=Go) un tema de iconos de AUR y configurarlo como tema de iconos de GTK.Añadiendo el tema en el archivo ~/.gtkrc-2.0 o puede utilizar lxappearance para configurarlo.

```
gtk-icon-theme-name="OxygenRefit2"

```

Hay también un par de temas GTK construidos que pueden hacer esto [gtk-kde42-oxygen-theme Oxygen style](https://aur.archlinux.org/packages.php?ID=24329).

#### Temas de iconos

No existen muchos temas de iconos diponibles para todo sistema en KDE 4\. Puede abrir **configuración del sistema > apariencia de aplicación > iconos** y buscar nuevos o instalarlos manualmente. Muchos de ellos pueden encontrarse en [kde-look.org](http://www.kde-look.org/).

#### Logo de Arch Linux en el menu de Kicker

Haga clic derecho en el botón de menú de Kicker, pulse **Preferencias del lanzador de aplicaciones** y, a continuación, pulse el icono la**derecha**. Ahora puedes elegir el icono de ArchLinux o cualquier otro icono para reemplazar a la opción por defecto. Los iconos oficiales de Arch se encuentran en [archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/) , puedes encontrarlo después de instalar en

```
/usr/share/archlinux/icons

```

#### Fuentes

Por defecto, las fuentes de KDE son pobres, prueba instalando los paquetes [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) y [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation).

Después de la instalación, asegúrete de cerrar y volver a iniciar sesión. No deberías tener que modificar ninguna configuración en la sección "Fuentes" de la configuración del sistema de KDE.

Si ha configurado personalmente cómo procesar sus [fuentes](/index.php/Fuentes "Fuentes"), tenga en cuenta que la configuración del sistema puede alterar su apariencia. Cuando cambias **configuración del sistema > aspecto > fuentes** probablemente se modificará el archivo de configuración de la fuente (`fonts.conf`).

Tenga en cuenta también que las preferencias de fuente de gnome también lo hará si utiliza ambos entornos de escritorio.

#### Eficacia de espacio

KDE es a menudo**criticado**por estar hinchado.

El usuario puede obtener esta percepción de ver ' *muchas barras de herramientas y los iconos con escalados muy grandes en las aplicaciones **. Esta situación se mejoró con el nuevo tema de Kwin que viene con KDE SC 4.4\. * con botones más elegantes que puedes cambiar de tamaño.** Las aplicaciones de KDE permiten ocultar muchas barras de herramientas, barras de menús y barras de estado*.

##### Todo tipo de * barras

La mayoría de las barras de herramientas de un programa se puede quitar de la barra, en el menú de "Configuración'***". Ahí a menudo se pueden ocultar la barra de estado y todas las barras de herramientas. Por último tambien se puede la propia barra de menú a través de**Ctrl + M'*.

Si no desea quitar las barras puede hacerlas más pequeñas o eliminar el texto de esta forma:

```
Configuración del sistema-> apariencia de la aplicación-> estilo-> ajustes-> (texto de barra de herramientas principal / texto secundario de la barra de herramientas)

```

##### Plasma

También hay algunos ajustes y modificaciones que se pueden aplicar a sus plasmoides para hacer perder el menor espacio posible a KDE

Por ejemplo, el "Reloj Digital" desperdicia más espacio que el "reloj analógico". El pequeño icono de plasma ("Cashew") que se puede ver en el panel se puede ocultar mediante el bloqueo de los widgets haciendo click derecho en el panel.

Si tienes muchas tareas en el administrador de tareas puedes utilizar *Smooth-tasks* para ganar espacio.

Este administrador de tareas alternativo permite mostrar los iconos de una tarea usando menos espacio pero manteniendo la capacidad del usuario para distinguir las diferentes tareas.

Instalación [smooth-tasks](https://aur.archlinux.org/packages.php?ID=29410) desde[AUR](/index.php/AUR "AUR").

Después de instalarlo y sustituir el administrador de tareas original debes fijarte en las opciones de configuración que ahora son mucho más amplias.

Para netbooks hay un espacio de trabajo especial, llamado Plasma Netbook, que hace un mejor uso de la pantalla:

```
Configuración del sistema-> comportamiento de espacio de trabajo-> espacio de trabajo-> tipo de espacio de trabajo

```

##### KWin

El decorador de ventanas puede redimensionar los botones de las ventanas y cambiar el borde de las mismas, para hacer los cambios mirar:

```
Configuración del sistema-> apariencia-> decoraciones de ventana -> configurar decoración...-> tamaño de botón

```

También puede quitar el borde de la ventana:

```
Configuración del sistema-> área de apariencia-> ventana decoraciones-> configurar decoración...-> tamaño del borde

```

### NetworkManager

Se ha agregado soporte NetworkManager en KDE SC. Para obtener más información, consulte[NetworkManager](/index.php/NetworkManager#KDE4 "NetworkManager").

También puedes usar [wicd-client-kde](https://aur.archlinux.org/packages.php?ID=40666/).

### Impresión

**Tip:** Usa la interfaz web de [CUPS](/index.php/CUPS "CUPS") para configurar rápidamente.

Las impresoras configuradas en este modo puede encontrarse en las aplicaciones de KDE.

También puede elegir la configuración de la impresora a través de **configuración del sistema -> configuración de impresora** . Para utilizar este método, primero debe instalar los paquetes:

```
# pacman -S kdeadmin-system-config-printer-kde cups

```

### Soporte Samba/Windows

Si desea tener acceso a los servicios de Windows:

```
pacman -S samba

```

A continuación, puede configurar sus acciones de Samba a través de:

```
 Configuración del sistema-> compartir-> Samba

```

### Powersaving

KDE ha integrado el servicio de Ahorro de energía llamado " *'Powerdevil* '" que puede ajustar el perfil de energía del sistema o / y el brillo de la pantalla (si es compatible).

#### Como habilitar Cpufreq

Desde KDE 4.5, [PowerDevil no maneja combinaciones de energía de la CPU a través de Cpufreq](http://lists.kde.org/?l=kde-devel&m=126800277431817&w=2).

**Nota:** En Arch el gobernador por defecto es "**performance**" y no "**ondemand**", por lo que el usuario tiene que instalar el paquete cpufrequtils y añadir el modulo "**cpufreq_ondemand**" en su rc.conf.

Puede utilizar fácilmente los gobernadores deseados mediante los comandos de cpufreq.

Para ello, sige estos pasos:

1\. Instala cpufrequtils

```
pacman -S cpufrequtils

```

y asegúrese de que tiene módulo cpufreq de su CPU cargado. Para más información sobre esto, visita [este articulo](/index.php/Cpufreq "Cpufreq").

2\. Entonces, en **configuración del sistema > administración de energía** , vaya al menú "Perfiles de energía".

Ahora puede crear un perfil nuevo o editar los anteriores.

Si desea que cpufrequtils sea el software que administrará el comportamiento del ahorro de energia del CPU , escriba el siguiente comando en el cuadro de texto "Script":

```
cpufreq-set -g ondemand

```

3\. Ahora seleccione el perfil de "Performance" y escriba este comando en el cuadro de texto "Script":

```
 cpufreq-set -g performance

```

No tienes que habilitar la casilla "Habilitar el ahorro de energía del sistema" para este perfil.

**Nota:** KDE 4.6 introdujo un nuevo marco de gestión de energía y "solid-powermanagement", que podía ser utilizado previamente, **ya no es un comando válido**.Si está satisfecho con el uso del gobernador ondemand todo el tiempo, puede tener este comando ejecutado al inicio colocándolo en "/ etc/rc.local".

### Registro de cambios en archivos y directorios

KDE utiliza **inotify** directamente desde el núcleo utilizando **kdirwatch** (incluido en kdelibs), por lo tanto no son necesarios Gamin o FAM. Puede que desee instalar este paquete ([kdirwatch](https://aur.archlinux.org/packages/kdirwatch/)de AUR) que es un entorno GUI para kdirwatch.

## Administración del sistema

### Establecer distribución del teclado

Para ello, vaya a

```
   Configuración del sistema > dispositivos de entrada > teclado

```

Elige tu modelo de teclado al principio. Por ejemplo: Generic | pc genérico 101 teclas

En la pestaña "**Distribución**", puedes elegir el idioma que quieres usar pulsando "Añadir Distribución" y después elegir la variante favorita.

En la pestaña "**Advanzado**", puedes elegir combinaciones de teclas especiales.

#### Terminar servidor Xorg mediante atajo de teclado de KDE

Dirige hacia:

```
   Ajustes del sistema -> Dispositivos de entrada -> Teclado -> Avanzado (pestaña)> "Secuencia de teclas para matar el servidor X" submenú

```

y marque la casilla de verificación.

## Problemas conocidos

*   Si deseas tener vistas previas de los vídeos en konqueror y dolphin, necesitarás instalar el paquete kdemultimedia-ffmpegthumbs o kdemultimedia-mplayerthumbs.

*   Si arrancas KDM con inittab, asegúrate de cambiar la ruta de /opt/kde a /usr

*   El primer arranque de KDE tarda un poco; no te preocupes. Está creando nuevos archivos de configuración y demás.

*   Si tienes una tarjeta gráfica nvidia y usas los controladores 173.14.x deberías mirar [nvidia/nvnews linux forum](http://www.nvnews.net/vbulletin/forumdisplay.php?f=14) para los nuevos controladores y ayuda (rápida). (Los controladores 180.22-1 de nvidia, en el repositorio extra, arreglan todo esto).

*   Si tienes problemas al actualizar de versión de KDE (de 4.6 a 4.7,por ejemplo) borra la carpeta .kde la ruta /home/tuusario/.kde

**Nota:** Ten en cuenta que eso borrara toda tu configuración en KDE (fondos,iconos,...), pero no afecta a la estabilidad del sistema

## KDEmod

KDEmod es un proyecto del equipo de Chakra para KDE 4.X, ya no esta activo y ha dejado de ser compatible con los paquetes y repositorios de Archlinux. Sí tienes instalado KDEmod, por favor borralo de tu sistema e instala KDE de los repositorios oficiales de Arch.

## Soporte para Java

Sólo tienes que instalar el paquete jre7-openjdk:

```
pacman -S jre7-openjdk

```

Quizá quieras echarle un ojo a la página en el wiki sobre [Java](/index.php/Java "Java") (en inglés), en ella se incluyen otras opciones para instalar java, así como configuración para algunos sistemas.

**Nota:** A partir de aquí no esta actualizada, se recomienda ir a la wiki en ingles para completar la información.

## Bajando de versión a kdemod3 o kde3-legacy desde KDE 4.3

Para la gente que decida que KDE 4.3 aún no está "listo" para su gusto, existe una página con recetas sobre cómo bajar a la rama 3.5 de KDE, llamada kdemod3:

*   [kdemod3](http://kdemod.ath.cx/download-kdemod3.html) (en inglés)

Para la gente que no quiera saber nada de KDE 4.3 ni TAMPOCO de kdemod3, tenemos una página en el foro que puede ayudarte a bajar de versión, o a mantener, KDE 3.5:

*   [kde-legacy 3.5.10 repository](https://bbs.archlinux.org/viewtopic.php?id=54118&p=1) (en inglés).

## Archivo Xserver de KDM

Se puede encontrar una configuración de ejemplo, para KDM, en /usr/share/config/kdm/kdmrc. Si necesitas ver todas las opciones, echa un vistazo en /usr/share/doc/HTML/en/kdm/kdmrc-ref.docbook.

## GPG y SSH

Para desactivar el agente gpg y/o el agente ssh en las sesiones de KDE, edita los archivos /usr/env/agent-startup.sh y /usr/shutdown/agent-shutdown.sh.

## Kdebindings

Kdebindings se ha construido sin el soporte para Java ni GTK. Si necesitas utilizar estas funciones, instala los paquetes adecuados con pacman:

```
pacman -S gtk jdk

```

## Cambiando el DPI para KDM

Edita, como root, el archivo /usr/share/config/kdm/kdmrc, y añade lo siguiente a la sección [X-:*-Core]:

```
ServerArgsLocal=-dpi 96

```

(Sustituye "96" por la cantidad DPI que busques). Sal de KDE y reinicia las X con Ctrl+Alt+Retroceso.

**Note:** Esto sólo es aplicable si estás usando KDM como administrador de acceso. Si no es así, entonces el archivo que tienes que editar es /usr/X11/bin/startx. En el verás una línea para <tt>defaultserverargs</tt>. Añade "-dpi 96" (o la cantidad de DPI que busques) y reinicia las X.

## Bugs y errores

Si crees que has encontrado un bug, por favor, comprueba si ese bug también aparece creando un nuevo usuario, con una instalación límpia. Algunos bugs aparecen por fallos de escritura en los archivos de configuración. Si el nuevo usuario no tiene el bug, prueba a mover los archivos de configuración a tu usuario habitual.

Los archivos de configuración de KDE 4 se encuentran, habitualmente, en /home/$user/.kde4/share/config y, específicos para las aplicaciones en /home/$user/.kde4/share/apps.

## Enlaces externos

*   [KDE Homepage](http://www.kde.org)
*   [KDE Bug Tracker](http://bugs.kde.org)
*   [Arch Linux Bug Tracker](https://bugs.archlinux.org)
*   [KDE WebSVN](http://websvn.kde.org)
*   [Control X Font DPI in X](http://process-of-elimination.net/index.php?title=Control_Font_DPI_in_X)