Artículos relacionados

*   [Guía oficial de Instalación](/index.php/Gu%C3%ADa_oficial_de_Instalaci%C3%B3n "Guía oficial de Instalación")
*   [Guía para Principiantes](/index.php/Gu%C3%ADa_para_Principiantes "Guía para Principiantes")

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
                *   [3.1.1.1.1 Apariencia de aplicaciones Qt y GTK +](#Apariencia_de_aplicaciones_Qt_y_GTK_.2B)
            *   [3.1.1.2 Widgets](#Widgets)
            *   [3.1.1.3 Applet de sonido en la bandeja del sistema](#Applet_de_sonido_en_la_bandeja_del_sistema)
            *   [3.1.1.4 Desactivar la sombra del panel](#Desactivar_la_sombra_del_panel)
        *   [3.1.2 Decoraciones para ventanas](#Decoraciones_para_ventanas)
        *   [3.1.3 Temas de iconos](#Temas_de_iconos)
        *   [3.1.4 Fuentes](#Fuentes)
            *   [3.1.4.1 Las fuentes en una sesión de Plasma lucen pobres](#Las_fuentes_en_una_sesi.C3.B3n_de_Plasma_lucen_pobres)
            *   [3.1.4.2 Las fuentes son enormes o parecen desproporcionadas](#Las_fuentes_son_enormes_o_parecen_desproporcionadas)
            *   [3.1.4.3 Eficiencia del espacio](#Eficiencia_del_espacio)
            *   [3.1.4.4 Generación de miniaturas](#Generaci.C3.B3n_de_miniaturas)
    *   [3.2 Impresión](#Impresi.C3.B3n)
    *   [3.3 Soporte de Samba/Windows](#Soporte_de_Samba.2FWindows)
    *   [3.4 Actividades de KDE Desktop](#Actividades_de_KDE_Desktop)
    *   [3.5 Ahorro de energía](#Ahorro_de_energ.C3.ADa)
    *   [3.6 Aplicaciones de autoarranque](#Aplicaciones_de_autoarranque)
    *   [3.7 Phonon](#Phonon)
        *   [3.7.1 ¿Qué backend debo elegir?](#.C2.BFQu.C3.A9_backend_debo_elegir.3F)
*   [4 Aplicaciones](#Aplicaciones)
*   [5 Administración del sistema](#Administraci.C3.B3n_del_sistema)
    *   [5.1 Establecer distribución del teclado](#Establecer_distribuci.C3.B3n_del_teclado)
        *   [5.1.1 Terminar servidor Xorg mediante atajo de teclado de KDE](#Terminar_servidor_Xorg_mediante_atajo_de_teclado_de_KDE)
*   [6 Problemas conocidos](#Problemas_conocidos)
*   [7 KDEmod](#KDEmod)
*   [8 Soporte para Java](#Soporte_para_Java)
*   [9 Bajando de versión a kdemod3 o kde3-legacy desde KDE 4.3](#Bajando_de_versi.C3.B3n_a_kdemod3_o_kde3-legacy_desde_KDE_4.3)
*   [10 Archivo Xserver de KDM](#Archivo_Xserver_de_KDM)
*   [11 GPG y SSH](#GPG_y_SSH)
*   [12 Kdebindings](#Kdebindings)
*   [13 Cambiando el DPI para KDM](#Cambiando_el_DPI_para_KDM)
*   [14 Bugs y errores](#Bugs_y_errores)
*   [15 Enlaces externos](#Enlaces_externos)

## Instalación

### Plasma Desktop

Antes de instalar Plasma, asegúrese de tener una instalación funcional de [Xorg](/index.php/Xorg "Xorg") en su sistema.

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el metapaquete [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) o el grupo [plasma](https://www.archlinux.org/groups/x86_64/plasma/). Para conocer las diferencias entre [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) y el grupo [plasma](https://www.archlinux.org/groups/x86_64/plasma/) refierace a [Creating packages#Meta packages and groups](/index.php/Creating_packages#Meta_packages_and_groups "Creating packages"). Alternativamente, para una instalación de Plasma mínima, instale el paquete [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop).

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

La mayoría de las configuraciones para las aplicaciones de KDE se almacenan en `~/.config`, pero algunas aplicaciones más antiguas pueden usar `~/.kde4`. Sin embargo, la configuración de KDE se realiza principalmente a través de la aplicación **Configuración del sistema**. Se puede iniciar desde un terminal ejecutando `systemsettings5`.

Algunas aplicaciones del Frameworks 5 pueden usar la configuración de KDElibs 4, después de mover los archivos de configuración a la nueva ubicación. Los ejemplos son:

```
* Los perfiles de Konsole de `~/.kde4/share/apps/konsole` a `~/.local/share/konsole/`

```

```
* Apariencia de la aplicación desde `~/.kde4/share/config/kdeglobals` a `~/.config/kdeglobals` 

```

### Personalización

#### Escritorio Plasma

##### Temas

Los [de Plasma](https://store.kde.org/browse/cat/104/%7Ctemas) definen la apariencia de paneles y plasmoides. Para una instalación fácil en todo el sistema, algunos de estos temas están disponibles tanto en los [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmatheme&do_Search=Go).

La forma más fácil de instalar temas es ir a través de la *Configuración del sistema> Tema del espacio de trabajo> Tema de escritorio> Obtener nuevos temas*.

Se mostrará una interfaz agradable de [https://store.kde.org/](https://store.kde.org/) que le permite instalar, desinstalar o actualizar scripts plasmoid de terceros literalmente un solo clic.

Las pantallas Splash y Lock no están disponibles actualmente, por lo que para personalizar estas pantallas debe modificar el tema original que se encuentra en `/usr/share/plasma/look-and-feel/`. Vea [this thread](https://www.kubuntuforums.net/showthread.php?67599-Plasma-5-background-images&s=59832dc20e5bfc2948dbb591d8453f61) en los foros de Kubuntu.

Tenga en cuenta que la pantalla de inicio de sesión [SDDM](/index.php/SDDM "SDDM") no forma parte de este tema.

###### Apariencia de aplicaciones Qt y GTK +

**Sugerencia:** Para la coherencia de los temas de Qt y GTK, consulte Uniform look for Qt y GTK applications.

	Qt4

Para que las aplicaciones Qt4 tengan una apariencia consistente, hay dos opciones:

Instale [breeze-kde4](https://www.archlinux.org/packages/?name=breeze-kde4) y luego selecciona Breeze como estilo GUI en `qtconfig-qt4`; o instale [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) y seleccione GTK + como estilo GUI.

	GTK +

El tema recomendado para una apariencia agradable en aplicaciones GTK + es [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) o [gnome-breeze-git](https://aur.archlinux.org/packages/gnome-breeze-git/), un tema GTK + diseñado para imitar la aparición del tema Breeze de Plasma. Instale [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config) y seleccione el tema GTK instalado para GTK2/GTK3-Theme en *Configuración del sistema> Estilo de aplicaciones> Estilo de aplicación de GNOME*.

En algunos temas, las sugerencias de las aplicaciones GTK + tienen texto blanco sobre fondos blancos, por lo que es difícil de leer. Para cambiar los colores en las aplicaciones de GTK2, busque la sección de información sobre herramientas en el archivo `.gtkrc-2.0` y cámbiela. Para la aplicación GTK3 hay que cambiar dos archivos; `gtk.css` y `settings.ini`. También puede ayudar desmarcar la opción de *Aplicar colores a aplicaciones que no sean Qt* en *Configuración del sistema > Colores* .

Algunos programas de GTK2 como [vuescan-bin](https://aur.archlinux.org/packages/vuescan-bin/) todavía no se pueden utilizar debido a las casillas de verificación invisibles con el tema Breeze o Adwaita en una sesión de plasma. Para solucionar este problema, instale y seleccione, por ejemplo, la piel Numix-Frost-Light del tema [numix-frost-themes](https://aur.archlinux.org/packages/numix-frost-themes/) en *Configuración del sistema > Estilo de aplicación > Estilo de aplicación GNOME (GTK)* > *Seleccione un tema GTK2:*. Numix-Frost-Light similar a Breeze.

##### Widgets

Los plasmoides son pequeños scripts (plasmoid scripts) o codigos de (plasmoid binaries) aplicaciones KDE diseñados para mejorar la funcionalidad de su escritorio.

La forma más fácil de instalar scripts de plasmoides es haciendo clic con el botón derecho en un panel o en el escritorio y eligiendo *Añadir Widgets> Obtener nuevos Widgets> Descargar Widgets*. Esto mostrará un interfaz agradable de [https://store.kde.org/](https://store.kde.org/) que le permite instalar, desinstalar o actualizar scripts de plasmoides de terceros literalmente con un solo clic.

Muchos binarios Plasmoid están disponibles en la [available from the AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmoid&do_Search=Go&PP=25&SO=d&SB=v).

##### Applet de sonido en la bandeja del sistema

[Instale](/index.php/Install "Install") [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa) o [kmix](https://www.archlinux.org/packages/?name=kmix) (inicie Kmix desde el Lanzador de aplicaciones). [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa) ahora se instala por defecto con [plasma](https://www.archlinux.org/groups/x86_64/plasma/), no se necesita ninguna configuración adicional.

**Nota:** Para ajustar el tamaño [step size of volume increments/decrements](https://bugs.kde.org/show_bug.cgi?id=313579#c28), agregue por ejemplo `VolumePercentageStep=1` en la sección `[Global]` de `~/.config/kmixrc`.

##### Desactivar la sombra del panel

Cuando el panel de plasma está en la parte superior de otras ventanas, su sombra se dibuja sobre ellas. [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1228394#p1228394) Para deshabilitar este comportamiento sin afectar a otras sombras, [instale](/index.php/Install "Install") [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) y ejecute:

```
 $ Xprop -remove _KDE_NET_WM_SHADOW

```

A continuación, seleccione el panel con el boton de signo mas. [[2]](https://forum.kde.org/viewtopic.php?f=285&t=121592) Para automatizar dicha configuración, instale [xorg-xwininfo](https://www.archlinux.org/packages/?name=xorg-xwininfo) y cree la siguiente secuencia de comandos:

 `/usr/local/bin/kde-no-shadow` 
```
#!/bin/bash
for WID in $(xwininfo -root -tree | sed '/"Plasma": ("plasmashell" "plasmashell")/!d; s/^  *\([^ ]*\) .*/\1/g'); do
   xprop -id $WID -remove _KDE_NET_WM_SHADOW
done

```

El script se puede ejecutar en inicio de sesión con *Añadir script* en *Autoarranque*:

```
 $ Kcmshell5 autostart

```

#### Decoraciones para ventanas

Las [decoraciones de ventana](https://store.kde.org/browse/cat/114/) se pueden cambiar en *Configuración del sistema > Estilo de aplicación> Decoraciones de ventana*.

Allí también puede descargar e instalar directamente más temas con un solo clic, y algunos están disponibles en el [AUR](https://aur.archlinux.org/packages.php?O=0&K=kdestyle&do_Search=Go&PP=25&SO=d&SB=v).

#### Temas de iconos

Los temas de iconos se pueden instalar y cambiar en A*justes del sistema> Iconos*.

**Nota:** Aunque todos los modernos escritorios de Linux comparten el mismo formato de tema de iconos, los escritorios como [GNOME](/index.php/GNOME "GNOME") utilizan menos iconos (especialmente en los menús y las barras de herramientas). Los temas desarrollados para tales escritorios carecen generalmente de iconos requeridos por las aplicaciones de Plasma y KDE. En su lugar, se recomienda instalar temas de iconos compatibles con Plasma.

#### Fuentes

##### Las fuentes en una sesión de Plasma lucen pobres

Intente instalar los paquetes [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) y [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation).

Después de la instalación, asegúrese de cerrar y volver a iniciar sesión. No debería tener que modificar nada en *Configuración del sistema > Fuentes*. Si está utilizando [qt5ct](https://www.archlinux.org/packages/?name=qt5ct), la configuración de Qt5 Configuration Tool puede anular la configuración de fuente en Configuración del sistema.

Si ha configurado personalmente cómo se renderizan las [fuentes](/index.php/Fonts "Fonts"), tenga en cuenta que la configuración del sistema puede alterar su apariencia. Cuando vaya a *Configuración del sistema> Fuentes*, Configuración del sistema probablemente alterará el archivo de configuración de las fuentes (`fonts.conf`).

No hay manera de evitar esto, pero si establece los valores para que coincidan con el archivo `fonts.conf`, se devolverá el renderizado de fuentes esperado (requerirá reiniciar la aplicación o, en algunos casos, reiniciar el escritorio). Tenga en cuenta que las Preferencias de fuente de Gnome también lo hacen.

##### Las fuentes son enormes o parecen desproporcionadas

Intente forzar la fuente DPI a `**96**` en *Configuración del sistema> Fuentes*.

Si eso no funciona, intente establecer el DPI directamente en su configuración de Xorg como se documenta en [Xorg#Setting DPI manually](/index.php/Xorg#Setting_DPI_manually "Xorg").

##### Eficiencia del espacio

El Plasma Netbook shell ha sido eliminado del Plasma 5, vea lo siguiente [KDE forum post](https://forum.kde.org/viewtopic.php?f=289&t=126631&p=335947&hilit=plasma+netbook#p335899). Sin embargo, puede conseguir algo similar editando el archivo `~/.config/kwinrc` añadiendo `BorderlessMaximizedWindows=true` en la sección `[Windows]`.

##### Generación de miniaturas

Para permitir la generación de miniaturas de archivos multimedia o de documentos en el escritorio y en Dolphin, instale [kdegraphics-thumbnailers](https://www.archlinux.org/packages/?name=kdegraphics-thumbnailers), [ffmpegthumbs](https://www.archlinux.org/packages/?name=ffmpegthumbs) y [kde-thumbnailer-odf](https://aur.archlinux.org/packages/kde-thumbnailer-odf/).

A continuación, habilite las categorías de miniaturas para el escritorio mediante el *botón derecho* sobre el *fondo del escritorio > Configurar el escritorio > Iconos > Más opciones de vista previa ....*

En *Dolphin*, vaya a *Control > Configurar Dophin > General > Vistas previas*.

### Impresión

**Sugerencia:** Utilice la interfaz web de CUPS para una configuración más rápida. Las impresoras configuradas de esta manera pueden utilizarse en aplicaciones KDE.

También puede configurar impresoras en *Configuración del sistema> Impresoras*. Para utilizar este método, primero debe instalar [print-manager](https://www.archlinux.org/packages/?name=print-manager) y [cups](https://www.archlinux.org/packages/?name=cups). Consulte Configuración de CUPS [CUPS#Configuration](/index.php/CUPS#Configuration "CUPS").

### Soporte de Samba/Windows

Si desea tener acceso a los servicios de Windows, instale [Samba](/index.php/Samba "Samba") (paquete [samba](https://www.archlinux.org/packages/?name=samba)).

La funcionalidad de compartir de Dolphin requiere el paquete [kdenetwork-filesharing](https://www.archlinux.org/packages/?name=kdenetwork-filesharing) y usershares, que el archivo `smb.conf` no ha habilitado. Las instrucciones para agregarlas se encuentran en [Samba#Creating a share](/index.php/Samba#Creating_a_share "Samba"), después de lo cual compartir en Dolphin debería funcionar fuera del espacio de trabajo después de reiniciar Samba.

Sin embargo, las habilidades de Plasma para acceder a las acciones de las PYMES son limitadas. Escribir en las particiones de Windows es problemático y abrir archivos de dichas particiones, por ejemplo, vídeos de gran tamaño, hace que Plasma copie todo el archivo al sistema local primero. Para solucionar esto, puede instalar un explorador de archivos basado en GTK como [thunar](https://www.archlinux.org/packages/?name=thunar) con [gvfs](https://www.archlinux.org/packages/?name=gvfs) y [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) (y [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) para guardar las credenciales de inicio de sesión) para acceder a los recursos compartidos SMB de una manera más capaz. Otra posible solución consiste en [montar](/index.php/Mount "Mount") un recurso de Samba a través de [cifs-utils](https://www.archlinux.org/packages/?name=cifs-utils) para que le parezca a Plasma que el recurso compartido SMB fuera sólo una carpeta local normal y, por lo tanto, se puede acceder normalmente. El comando mount podría ser similar al siguiente para el acceso de escritura a un recurso compartido público:

1.  mount -t cifs -o username=*,password=*,uid=1000,gid=1000,file_mode=0660,dir_mode=0770 //networkhost/share/ /home/user/localmountpoint/

Make it permanent:

 `/etc/fstab` 
```
//networkhost/share/ /home/user/localmountpoint/ cifs defaults,username=*,password=*,uid=1000,gid=1000,file_mode=0660,dir_mode=0770 0 2

```

Es posible que no sea necesario añadir `.local` al nombre de host.

Una solución más fácil es usar [samba-mounter-git](https://aur.archlinux.org/packages/samba-mounter-git/), que ofrece básicamente la misma funcionalidad a través de una opción fácil de usar ubicada en *Configuración del sistema > Controladores de red*.

### Actividades de KDE Desktop

[KDE Desktop Activities|Las actividades de escritorio de KDE](https://userbase.kde.org/Plasma#Activities) son espacios de trabajo especiales donde puede seleccionar configuraciones específicas para cada actividad, que se aplican sólo cuando está utilizando dicha actividad.

### Ahorro de energía

[Instale](/index.php/Install "Install") [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) para integrar el servicio de ahorro de energía llamado "**Powerdevil Power Management**", que puede ajustar el perfil de ahorro de energía del sistema y / o el brillo de la pantalla (si está soportado).

**Nota:** Powerdevil no puede [inhibir](/index.php/Power_management#Power_managers "Power management") todos los ajustes de inicio de sesión (como la acción de cierre de la tapa para ordenadores portátiles). En estos casos, el ajuste de inicio de sesión tendrá que cambiarse - vea [Administración de energía con systemd.](/index.php/Power_management#Power_management_with_systemd "Power management")

### Aplicaciones de autoarranque

Plasma puede autoarrancar aplicaciones y ejecutar scripts en el inicio y apagado del sistema. Para iniciar automáticamente una aplicación, vaya a *Configuración del sistema> Inicio y apagado> Inicio automático* y agregue el programa o la secuencia de comandos de shell de su elección. Para las aplicaciones, se creará un archivo `.desktop`, para los scripts de shell, se creará un enlace simbólico.

**Nota:**

*   Los programas pueden autoarrancar en el inicio de sesión, mientras que los scripts de shell también se pueden ejecutar en el apagado o incluso antes de que el propio Plasma se inicie.
*   Los scripts de Shell sólo se ejecutarán si están marcados como ejecutables.

Coloque las [entradas del escritorio](/index.php/Desktop_entries "Desktop entries") (por ejemplo, archivos `.desktop`) aquí:

	`~/.config/autostart`

	Para iniciar las aplicaciones al inicio de sesión.

Coloque o escriba scripts de shell de enlace simbólico en uno de los siguientes directorios:

	`~/.config/plasma-workspace/env`

	Para ejecutar scripts en el inicio de sesión antes de iniciar Plasma.

	`~/.config/autostart-scripts`

	Para ejecutar scripts al iniciar sesión.

	`~/.config/plasma-workspace/shutdown`

	Para ejecutar scripts en el apagado.

### Phonon

De [Wikipedia](https://en.wikipedia.org/wiki/Phonon_(software) "wikipedia:Phonon (software)"):

	*“Phonon es la API multimedia proporcionada por KDE y es la abstracción estándar para manejar corrientes multimedia dentro del software de KDE y también utilizada por varias aplicaciones Qt.*

Phonon fue creado originalmente para permitir que el software KDE y Qt fuera independiente de cualquier framework multimedia como GStreamer o xine y proporcionar una API estable y mayor vida útil de una versión principal.”

**Phonon** se utiliza ampliamente en KDE, tanto para audio (por ejemplo, las notificaciones del sistema o las aplicaciones de audio de KDE) como para el vídeo (por ejemplo, las miniaturas de vídeo de Dolphin).

#### ¿Qué backend debo elegir?

Puede elegir entre backends basados en [GStreamer](/index.php/GStreamer "GStreamer") y [VLC](/index.php/VLC_(Espa%C3%B1ol) "VLC (Español)") – cada uno disponible en versiones para aplicaciones Qt4 y aplicaciones Qt5 ([phonon-qt4-gstreamer](https://aur.archlinux.org/packages/phonon-qt4-gstreamer/), [phonon-qt5-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt5-gstreamer) – [phonon-qt4-vlc](https://aur.archlinux.org/packages/phonon-qt4-vlc/), [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc)).

[Upstream prefers VLC|Upstream prefiere VLC](https://www.phoronix.com/scan.php?page=news_item&px=MTUwNDM), pero las distribuciones Linux destacadas (Kubuntu y Fedora-KDE por ejemplo) prefieren GStreamer porque eso les permite fácilmente descartar los codecs MPEG patentados de la instalación por defecto. Ambos backends tienen un conjunto de características ligeramente diferente. [features set](https://community.kde.org/Phonon/FeatureMatrix).

En el pasado, otros backends también se desarrollaron, pero ya no se mantienen y sus paquetes AUR han sido eliminados.

**Nota:**

*   Se pueden instalar múltiples backends a la vez y se priorizan en *Configuración del sistema> Multimedia> Backend*.
*   Según los [foros de KDE](https://forum.kde.org/viewtopic.php?f=250&t=126476&p=335080), el backend de VLC carece de soporte para [ReplayGain](https://en.wikipedia.org/wiki/ReplayGain "wikipedia:ReplayGain")
*   Si elige el backend de vlc, es posible que experimente fallos cada vez que kde quiera enviarle una advertencia audible (y en bastantes casos también, consulte [[3]](https://forum.kde.org/viewtopic.php?f=289&t=135956)).
*   Una posible solución es ejecutar

 `# /usr/lib/vlc/vlc-cache-gen -f /usr/lib/vlc/plugins` 

## Aplicaciones

El proyecto KDE proporciona un conjunto de aplicaciones que se integran con el escritorio de plasma. Consulte el grupo de aplicaciones kde para obtener una lista completa de las aplicaciones disponibles. Véase también Categoría: KDE para páginas de aplicación de KDE relacionadas. Aparte de los programas proporcionados en las aplicaciones de KDE, hay muchas otras aplicaciones disponibles que pueden complementar el escritorio de plasma. Algunas de ellas se discuten a continuación.

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