**Estado de la traducción**
Este artículo es una traducción de [KDE](/index.php/KDE "KDE"), revisada por última vez el **2019-01-28**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=KDE&diff=0&oldid=564820) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Entornos de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)")
*   [Gestor de pantallas](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)")
*   [Gestor de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)")
*   [Qt](/index.php/Qt "Qt")
*   [SDDM](/index.php/SDDM "SDDM")
*   [Dolphin](/index.php/Dolphin "Dolphin")
*   [KDE Wallet](/index.php/KDE_Wallet_(Espa%C3%B1ol) "KDE Wallet (Español)")
*   [KDevelop](/index.php/KDevelop "KDevelop")
*   [Trinity](/index.php/Trinity "Trinity")
*   [Apariencia uniforme para aplicaciones Qt y GTK](/index.php/Uniform_Look_for_Qt_and_GTK_Applications_(Espa%C3%B1ol) "Uniform Look for Qt and GTK Applications (Español)")

KDE es un proyecto de software que actualmente comprende un [entorno de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)") conocido como Plasma, una colección de librerías y frameworks (KDE Frameworks) y también varias aplicaciones (KDE Applications). El anterior KDE tiene un [UserBase wiki](https://userbase.kde.org/) bien mantenido. Allí se puede encontrar información detallada sobre la mayoría de las aplicaciones KDE.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
    *   [1.1 Plasma](#Plasma)
    *   [1.2 Aplicaciones KDE](#Aplicaciones_KDE)
    *   [1.3 Lanzamientos inestables](#Lanzamientos_inestables)
*   [2 Iniciar Plasma](#Iniciar_Plasma)
    *   [2.1 Usar un gestor de pantallas](#Usar_un_gestor_de_pantallas)
    *   [2.2 Desde la consola](#Desde_la_consola)
*   [3 Configuración](#Configuración)
    *   [3.1 Personalización](#Personalización)
        *   [3.1.1 Escritorio Plasma](#Escritorio_Plasma)
            *   [3.1.1.1 Temas](#Temas)
                *   [3.1.1.1.1 Apariencia de las aplicaciones Qt y GTK+](#Apariencia_de_las_aplicaciones_Qt_y_GTK+)
            *   [3.1.1.2 Caras](#Caras)
            *   [3.1.1.3 Widgets](#Widgets)
            *   [3.1.1.4 Applet de sonido en la bandeja del sistema](#Applet_de_sonido_en_la_bandeja_del_sistema)
            *   [3.1.1.5 Deshabilitar la sombra del panel](#Deshabilitar_la_sombra_del_panel)
        *   [3.1.2 Decoraciones de las ventanas](#Decoraciones_de_las_ventanas)
        *   [3.1.3 Temas de iconos](#Temas_de_iconos)
        *   [3.1.4 Eficiencia de espacio](#Eficiencia_de_espacio)
        *   [3.1.5 Generación de miniaturas](#Generación_de_miniaturas)
    *   [3.2 Imprimir](#Imprimir)
    *   [3.3 Soporte Samba/Windows](#Soporte_Samba/Windows)
    *   [3.4 Actividades de KDE Desktop](#Actividades_de_KDE_Desktop)
    *   [3.5 Administración de energía](#Administración_de_energía)
    *   [3.6 Inicio automático](#Inicio_automático)
    *   [3.7 Phonon](#Phonon)
        *   [3.7.1 ¿Qué backend debo elegir?](#¿Qué_backend_debo_elegir?)
*   [4 Aplicaciones](#Aplicaciones)
    *   [4.1 Administración del sistema](#Administración_del_sistema)
        *   [4.1.1 Detener Xorg server a través de las preferencias del sistema KDE](#Detener_Xorg_server_a_través_de_las_preferencias_del_sistema_KDE)
        *   [4.1.2 KCM](#KCM)
    *   [4.2 Búsqueda de escritorio](#Búsqueda_de_escritorio)
    *   [4.3 Navegadores web](#Navegadores_web)
    *   [4.4 PIM](#PIM)
        *   [4.4.1 Akonadi](#Akonadi)
            *   [4.4.1.1 PostgreSQL](#PostgreSQL)
            *   [4.4.1.2 SQLite](#SQLite)
            *   [4.4.1.3 Deshabilitar Akonadi](#Deshabilitar_Akonadi)
    *   [4.5 KDE Telepathy](#KDE_Telepathy)
        *   [4.5.1 Utilizar Telegram con KDE Telepathy](#Utilizar_Telegram_con_KDE_Telepathy)
    *   [4.6 KDE Connect](#KDE_Connect)
*   [5 Consejos y trucos](#Consejos_y_trucos)
    *   [5.1 Usar un gestor de ventanas diferente](#Usar_un_gestor_de_ventanas_diferente)
        *   [5.1.1 Sesión KDE/Openbox](#Sesión_KDE/Openbox)
        *   [5.1.2 Rehabilitar efectos de composición](#Rehabilitar_efectos_de_composición)
    *   [5.2 Configurar la resolución del monitor / múltiples monitores](#Configurar_la_resolución_del_monitor_/_múltiples_monitores)
    *   [5.3 Deshabilitar la apertura del lanzador de aplicaciones con la tecla Super (tecla Windows)](#Deshabilitar_la_apertura_del_lanzador_de_aplicaciones_con_la_tecla_Super_(tecla_Windows))
    *   [5.4 Deshabilitar que los marcadores se muestren en el menú de aplicaciones](#Deshabilitar_que_los_marcadores_se_muestren_en_el_menú_de_aplicaciones)
*   [6 Solución de problemas](#Solución_de_problemas)
    *   [6.1 Fuentes tipográficas](#Fuentes_tipográficas)
        *   [6.1.1 Las fuentes en una sesión Plasma se ven mal](#Las_fuentes_en_una_sesión_Plasma_se_ven_mal)
        *   [6.1.2 Las fuentes son enormes o parecen desproporcionadas](#Las_fuentes_son_enormes_o_parecen_desproporcionadas)
    *   [6.2 Configuración relacionada](#Configuración_relacionada)
        *   [6.2.1 El escritorio Plasma se comporta de manera extraña](#El_escritorio_Plasma_se_comporta_de_manera_extraña)
        *   [6.2.2 Limpiar la caché para resolver problemas de actualización](#Limpiar_la_caché_para_resolver_problemas_de_actualización)
    *   [6.3 Problemas gráficos](#Problemas_gráficos)
        *   [6.3.1 Obtener el estado actual de KWin para fines de soporte y depuración](#Obtener_el_estado_actual_de_KWin_para_fines_de_soporte_y_depuración)
        *   [6.3.2 Deshabilitar los efectos del escritorio manualmente o automáticamente para aplicaciones definidas](#Deshabilitar_los_efectos_del_escritorio_manualmente_o_automáticamente_para_aplicaciones_definidas)
        *   [6.3.3 Deshabilitar la composición](#Deshabilitar_la_composición)
        *   [6.3.4 Parpadeo en pantalla completa cuando la composición está habilitada](#Parpadeo_en_pantalla_completa_cuando_la_composición_está_habilitada)
        *   [6.3.5 Screen tearing con NVIDIA](#Screen_tearing_con_NVIDIA)
        *   [6.3.6 El cursor de Plasma a veces se muestra incorrectamente](#El_cursor_de_Plasma_a_veces_se_muestra_incorrectamente)
        *   [6.3.7 Se ha establecido una resolución de pantalla inutilizable](#Se_ha_establecido_una_resolución_de_pantalla_inutilizable)
    *   [6.4 Problemas de sonido](#Problemas_de_sonido)
        *   [6.4.1 No hay sonido después de suspender](#No_hay_sonido_después_de_suspender)
        *   [6.4.2 Los archivos MP3 no se pueden reproducir cuando se utiliza el backend GStreamer Phonon](#Los_archivos_MP3_no_se_pueden_reproducir_cuando_se_utiliza_el_backend_GStreamer_Phonon)
    *   [6.5 Administración de energía](#Administración_de_energía_2)
        *   [6.5.1 No hay opciones de Suspender/Hibernar](#No_hay_opciones_de_Suspender/Hibernar)
    *   [6.6 KMail](#KMail)
        *   [6.6.1 Limpie la configuración de akonadi para arreglar KMail](#Limpie_la_configuración_de_akonadi_para_arreglar_KMail)
        *   [6.6.2 Vaciar la bandeja de entrada IMAP en KMail](#Vaciar_la_bandeja_de_entrada_IMAP_en_KMail)
    *   [6.7 Conexión](#Conexión)
        *   [6.7.1 Se congela cuando se usa montaje automático en un volumen NFS](#Se_congela_cuando_se_usa_montaje_automático_en_un_volumen_NFS)
    *   [6.8 Registro agresivo del diario QXcbConnection](#Registro_agresivo_del_diario_QXcbConnection)
    *   [6.9 Las aplicaciones KF5/Qt 5 no muestran iconos en i3/FVWM/awesome](#Las_aplicaciones_KF5/Qt_5_no_muestran_iconos_en_i3/FVWM/awesome)
    *   [6.10 Problemas al guardar las credenciales y los diálogos de KWallet se muestran de manera persistente](#Problemas_al_guardar_las_credenciales_y_los_diálogos_de_KWallet_se_muestran_de_manera_persistente)
    *   [6.11 Discover no muestra ninguna aplicación](#Discover_no_muestra_ninguna_aplicación)
    *   [6.12 kscreenlocker_greet usa mucha CPU con controladores de NVIDIA](#kscreenlocker_greet_usa_mucha_CPU_con_controladores_de_NVIDIA)
    *   [6.13 Error 22 del SO cuando se ejecuta Akonadi en ZFS](#Error_22_del_SO_cuando_se_ejecuta_Akonadi_en_ZFS)
    *   [6.14 Algunos programas no pueden desplazarse cuando sus ventanas están inactivas](#Algunos_programas_no_pueden_desplazarse_cuando_sus_ventanas_están_inactivas)
*   [7 Véase también](#Véase_también)

## Instalación

### Plasma

Antes de instalar Plasma, asegúrese de tener una instalación [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") en funcionamiento en su sistema.

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el metapaquete [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) o el grupo [plasma](https://www.archlinux.org/groups/x86_64/plasma/). Para conocer las diferencias entre [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) y [plasma](https://www.archlinux.org/groups/x86_64/plasma/) véase [grupo de paquetes](/index.php/Package_group_(Espa%C3%B1ol) "Package group (Español)"). Alternativamente, para una instalación de Plasma más minimalista, instale el paquete [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop).

Para habilitar el soporte para [Wayland](/index.php/Wayland_(Espa%C3%B1ol) "Wayland (Español)") en Plasma, instale también el paquete [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session).

### Aplicaciones KDE

Para instalar el conjunto completo de aplicaciones KDE, instale el grupo [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) o el metapaquete [kde-applications-meta](https://www.archlinux.org/packages/?name=kde-applications-meta). Tenga en cuenta que esto solo instalará aplicaciones, no instalará ninguna versión de Plasma.

### Lanzamientos inestables

Véase [Repositorios oficiales#kde-inestable](/index.php/Official_repositories#kde-unstable "Official repositories")

## Iniciar Plasma

**Nota:** Aunque es posible iniciar Plasma en [Wayland](/index.php/Wayland_(Espa%C3%B1ol) "Wayland (Español)"), faltan algunas características y hay algunos problemas conocidos a partir de Plasma 5.13\. Véase la [Plasma 5.13 Errata](https://community.kde.org/Plasma/5.13_Errata#Wayland) para ver una lista de problemas y la [Plasma on Wayland workboard](https://phabricator.kde.org/project/board/99/) para observar el estado actual de desarrollo. Utilize [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") para una experiencia más completa y estable.

Plasma puede iniciarse usando o bien un [gestor de pantallas](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)"), o bien desde la consola.

### Usar un gestor de pantallas

*   Seleccione *Plasma* para iniciar una nueva sesión en [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)").
*   [Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session) y seleccione *Plasma (Wayland)* para iniciar una nueva sesión en [Wayland](/index.php/Wayland_(Espa%C3%B1ol) "Wayland (Español)").

**Nota:** La implementación del controlador propietario [NVIDIA](/index.php/NVIDIA_(Espa%C3%B1ol) "NVIDIA (Español)") para Wayland requiere EGLStreams. KDE no ha implementado EGLStreams en su [implementación](https://blog.martin-graesslin.com/blog/2016/09/to-eglstream-or-not) de Wayland. Las siguientes soluciones están disponibles:

*   Utilizar el controlador [Nouveau](/index.php/Nouveau_(Espa%C3%B1ol) "Nouveau (Español)").
*   Utilizar la sesión de (por defecto) Xorg.

### Desde la consola

Para iniciar Plasma con [xinit/startx](/index.php/Xinit_(Espa%C3%B1ol) "Xinit (Español)"), agregue `exec startkde` a su archivo `.xinitrc`. Si desea iniciar Xorg al iniciar sesión, véase [iniciar X al iniciar sesión](/index.php/Xinit_(Espa%C3%B1ol)#Inicio_automático_de_X_al_inicio_de_sesión "Xinit (Español)"). Para iniciar una sesión de Plasma en Wayland desde una consola, ejecute `XDG_SESSION_TYPE=wayland dbus-run-session startplasmacompositor`.[[1]](https://community.kde.org/KWin/Wayland#Start_a_Plasma_session_on_Wayland)

## Configuración

La mayoría de las configuraciones para las aplicaciones KDE se almacenan en `~/.config/`. Sin embargo, la configuración de KDE se realiza principalmente a través de la aplicación **Preferencias del sistema**. Se puede iniciar desde un terminal ejecutando `systemsettings5`.

### Personalización

#### Escritorio Plasma

##### Temas

Los [temas de Plasma](https://store.kde.org/browse/cat/104/) definen el aspecto de los paneles y los plasmoides. Para facilitar la instalación en todo el sistema, algunos temas están disponibles tanto en los repositorios oficiales como en [AUR](https://aur.archlinux.org/packages.php?K=plasma+theme).

Los temas de Plasma también se pueden instalar a través de *Preferencias del sistema > Tema del espacio de trabajo > Tema de escritorio > Obtener nuevos temas*.

La [KDE-Store](https://store.kde.org/) ofrece más personalizaciones de Plasma, como temas [SDDM](/index.php/SDDM "SDDM") y pantallas de bienvenida.

###### Apariencia de las aplicaciones Qt y GTK+

**Sugerencia:** Para la coherencia de los temas Qt y GTK, véase [aspecto uniforme para aplicaciones Qt y GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications_(Espa%C3%B1ol) "Uniform look for Qt and GTK applications (Español)")

	Qt4

Breeze no está disponible directamente para Qt4 ya que no se puede compilar sin los paquetes de KDE 4, que se han eliminado del repositorio adicional en agosto de 2018 ([FS#59784](https://bugs.archlinux.org/task/59784)). Sin embargo, puede instalar [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) y elegir GTK+ como estilo de interfaz gráfica ejecutando `qtconfig-qt4`.

	GTK+

El tema recomendado para una apariencia agradable en aplicaciones GTK+ es [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) o [gnome-breeze-git](https://aur.archlinux.org/packages/gnome-breeze-git/), un tema GTK+ diseñado para imitar la apariencia del tema de Plasma Breeze. Instale [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config) (parte del grupo [plasma](https://www.archlinux.org/groups/x86_64/plasma/)) y seleccione el tema GTK instalado para GTK2/GTK3-Theme en *Preferencias del sistema > Estilo de las aplicaciones > Estilo de aplicaciones de GNOME*.

En algunos temas, la descripción emergente en aplicaciones GTK+ tiene texto blanco sobre fondos blancos, lo que dificulta su lectura. Para cambiar los colores en las aplicaciones GTK2, busque la sección de descripciones emergentes en el archivo `.gtkrc-2.0` y cámbiela. Para la aplicación GTK3 se deben cambiar dos archivos, `gtk.css` y `settings.ini`. También puede ayudar el desmarcar la opción *Aplicar colores a aplicaciones no Qt* en *Preferencias del sistema > Colores*.

Algunos programas de GTK2 como [vuescan-bin](https://aur.archlinux.org/packages/vuescan-bin/) todavía parecen difíciles de usar debido a casillas de verificación invisibles con el aspecto Breeze o Adwaita en una sesión Plasma. Para solucionar esto, instale y seleccione, por ejemplo, el aspecto Numix-Frost-Light de [numix-frost-themes](https://aur.archlinux.org/packages/numix-frost-themes/) en *Preferencias del sistema > Estilo de las aplicaciones > Estilo de aplicaciones de GNOME (GTK) > Seleccione un tema de GTK2:*. Numix-Frost-Light se parece a Breeze.

##### Caras

La cara del usuario se puede configurar a través de *Preferencias del sistema > Detalles de cuentas > Gestor de usuarios*.

Si no se encuentra *Gestor de usuarios*, instale [user-manager](https://www.archlinux.org/packages/?name=user-manager) para obtenerlo.

##### Widgets

Los plasmoides son pequeñas aplicaciones KDE scripteadas (scripts plasmoides) o codificadas (binarios plasmoides) diseñadas para mejorar la funcionalidad de su escritorio.

La forma más fácil de instalar scripts plasmoides es haciendo clic derecho en un panel o en el escritorio y seleccionando *Añadir elementos gráficos > Obtener nuevos elementos gráficos > Descargar nuevos elementos gráficos de plasma*. Esto le mostratá una bonita interfaz para [https://store.kde.org/](https://store.kde.org/) que le permite instalar, desinstalar o actualizar scripts plasmoides de terceros con un solo clic.

Muchos binarios de Plasmoid están disponibles en [AUR](https://aur.archlinux.org/packages.php?K=plasmoid).

##### Applet de sonido en la bandeja del sistema

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa) o [kmix](https://www.archlinux.org/packages/?name=kmix) (inicie Kmix desde el lanzador de aplicaciones). [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa) ahora se instala de manera predeterminada con [plasma](https://www.archlinux.org/groups/x86_64/plasma/), no se necesita ninguna configuración.

**Nota:** Para ajustar el [tamaño del cambio de los incrementos/decrementos de volumen](https://bugs.kde.org/show_bug.cgi?id=313579#c28), agregue, por ejemplo. `VolumePercentageStep=1` en la sección `[Global]` de `~/.config/kmixrc`

##### Deshabilitar la sombra del panel

Cuando el panel de plasma esté encima de otras ventanas, su sombra se mostrará encima de ellas. [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1228394#p1228394) Para deshabilitar este comportamiento sin afectar a otras sombras, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) y ejecute:

```
$ xprop -remove _KDE_NET_WM_SHADOW

```

a continuación, seleccione el panel con el cursor de tamaño ampliado. [[3]](https://forum.kde.org/viewtopic.php?f=285&t=121592) Para su automatización, instale [xorg-xwininfo](https://www.archlinux.org/packages/?name=xorg-xwininfo) y cree el siguiente script:

 `/usr/local/bin/kde-no-shadow` 
```
#!/bin/bash
for WID in $(xwininfo -root -tree | sed '/"Plasma": ("plasmashell" "plasmashell")/!d; s/^  *\([^ ]*\) .*/\1/g'); do
   xprop -id $WID -remove _KDE_NET_WM_SHADOW
done

```

Establezca permisos de ejecución para el script:

```
# chmod 755 /usr/local/bin/kde-no-shadow

```

El script se puede ejecutar al iniciar sesión con *Agregar script* en *Inicio automático*:

```
$ kcmshell5 autostart

```

#### Decoraciones de las ventanas

Las [decoraciones de las ventanas](https://store.kde.org/browse/cat/114/) se pueden cambiar en *Preferencias del sistema > Estilo de las aplicaciones > Decoración de ventanas*.

Allí también puede descargar e instalar directamente más temas con un solo clic, y algunos están disponibles en [AUR](https://aur.archlinux.org/packages.php?K=kde+window+decoration).

#### Temas de iconos

Los temas de iconos se pueden instalar y cambiar en *Preferencias del sistema > Iconos*.

**Nota:** Aunque todos los escritorios de Linux modernos comparten el mismo formato de tema de iconos, los escritorios como [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)") usan menos iconos (especialmente en menús y barras de herramientas). Los temas desarrollados para tales escritorios generalmente carecen de los iconos requeridos por las aplicaciones Plasma y KDE. Se recomienda en su lugar instalar temas de iconos compatibles con Plasma.

**Sugerencia:** Dado que algunos temas de iconos no se heredan del tema de iconos predeterminado, es posible que falten algunos iconos. Para heredarlo de Breeze, agregue `breeze` al vector `Inherits=` en `/usr/share/icon/*nombre-del-tema*/index.theme`, por ejemplo: `Inherits=breeze,hicolor`. Debe volver a aplicar este parche después de cada actualización del tema de iconos; considere usar [Pacman hooks](/index.php/Pacman_(Espa%C3%B1ol)#Hooks "Pacman (Español)") para automatizar el proceso.

#### Eficiencia de espacio

El shell del Plasma Netbook se ha eliminado de Plasma 5, véase la siguiente [publicación en el foro de KDE](https://forum.kde.org/viewtopic.php?f=289&t=126631&p=335947&hilit=plasma+netbook#p335899). Sin embargo, puede lograr algo similar editando el archivo `~/.config/kwinrc` agregando `BorderlessMaximizedWindows=true` en la sección `[Windows]`.

#### Generación de miniaturas

Para permitir la generación de miniaturas para archivos de media o de documentos en el escritorio y en Dolphin, instale [kdegraphics-thumbnailers](https://www.archlinux.org/packages/?name=kdegraphics-thumbnailers) y [ffmpegthumbs](https://www.archlinux.org/packages/?name=ffmpegthumbs).

Luego, habilite las categorías de las miniaturas para el escritorio haciendo clic con el botón derecho en el *fondo de escritorio > Configurar escritorio > Iconos > Más opciones de vista previa...*

En *Dolphin*, vaya a *Control > Configurar Dolphin... > General > Vistas previas*.

### Imprimir

**Sugerencia:** Use la interfaz web [CUPS](/index.php/CUPS_(Espa%C3%B1ol) "CUPS (Español)") para una configuración más rápida. Las impresoras configuradas de esta manera se pueden utilizar en aplicaciones KDE.

También puede configurar impresoras en *Preferencias del sistema > Impresoras*. Para usar este método, primero debe instalar [print-manager](https://www.archlinux.org/packages/?name=print-manager) y [cups](https://www.archlinux.org/packages/?name=cups). Véase [CUPS#Configuration](/index.php/CUPS_(Espa%C3%B1ol)#Configuración "CUPS (Español)").

### Soporte Samba/Windows

Si desea tener acceso a los servicios de Windows, instale [Samba](/index.php/Samba_(Espa%C3%B1ol) "Samba (Español)") (paquete [samba](https://www.archlinux.org/packages/?name=samba)).

La funcionalidad de compartir con Dolphin requiere el paquete [kdenetwork-filesharing](https://www.archlinux.org/packages/?name=kdenetwork-filesharing) y los recursos compartidos, que el stock `smb.conf` no los tiene habilitados. Las instrucciones para agregarlos se encuentran en [Samba#Habilitar los recursos compartidos](/index.php/Samba#Enable_usershares "Samba"), después de lo cual la compartición en Dolphin debería funcionar sin necesidad de configuración después de reiniciar Samba.

**Sugerencia:** Utilice `*` (asterisco) tanto para el nombre de usuario como para la contraseña cuando acceda a un recurso compartido de Windows sin autenticación en la pantalla de solicitud de Dolphin.

A diferencia de los exploradores de archivos GTK que también utilizan GVfs para el programa lanzado, abrir archivos desde recursos compartidos de Samba en Dolphin a través de KIO hace que Plasma copie primero todo el archivo al sistema local con la mayoría de los programas (VLC es una excepción). Para solucionar esto, puede usar un navegador de archivos basado en GTK como [thunar](https://www.archlinux.org/packages/?name=thunar) con [gvfs](https://www.archlinux.org/packages/?name=gvfs) y [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) (y [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) para guardar las credenciales de inicio de sesión) para acceder a los recursos compartidos SMB de una manera más capaz.

Otra posibilidad es [montar](/index.php/Mount "Mount") un recurso compartido Samba a través de [cifs-utils](https://www.archlinux.org/packages/?name=cifs-utils) para hacer creer a Plasma que el recurso compartido SMB es solo una carpeta local normal y, por lo tanto, se pueda acceder a él normalmente. Véase [Samba#Montaje manual](/index.php/Samba#Manual_mounting "Samba") y [Samba#Montaje automático](/index.php/Samba#Automatic_mounting "Samba").

Una solución con interfaz gráfica está disponible en [samba-mounter-git](https://aur.archlinux.org/packages/samba-mounter-git/), que ofrece básicamente la misma funcionalidad a través de una opción fácil de utilizar ubicada en *Preferencias del sistema > Controladores de red*. Sin embargo, podría romperse con las nuevas versiones de KDE Plasma.

### Actividades de KDE Desktop

[KDE Desktop Activities](https://userbase.kde.org/Plasma#Activities) son espacios de trabajo especiales en los que puede seleccionar configuraciones específicas para cada actividad que se aplican solamente cuando se está utilizando dicha actividad.

### Administración de energía

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) para obtener un servicio integrado de administración de energía en Plasma. Este servicio ofrece funciones adicionales de ahorro de energía, control de brillo del monitor (si es compatible) e informes de batería, incluidos dispositivos periféricos.

[powerdevil-light](https://aur.archlinux.org/packages/powerdevil-light/) proporciona un paquete alternativo sin las dependencias de [NetworkManager](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)") y [Bluez](/index.php/Bluetooth_(Espa%C3%B1ol) "Bluetooth (Español)").

**Nota:** Powerdevil podría no [inhibir](/index.php/Power_management#Power_managers "Power management") todas las configuraciones de logind (como la acción de cierre de la tapa para ordenadores portátiles). En estos casos, será necesario cambiar la configuración de logind - véase [Administración de energía#Administración de energía con systemd](/index.php/Power_management_(Espa%C3%B1ol)#Administración_de_energía_con_systemd "Power management (Español)").

### Inicio automático

Plasma puede iniciar aplicaciones automáticamente y ejecutar scripts en el arranque y el apagado. Para iniciar automáticamente una aplicación, vaya a *Preferencias del sistema > Arranque y apagado > Autoarranque* y agregue el programa o el script de shell que desee. Para las aplicaciones, se creará un archivo *.desktop*, para los scripts de shell, se creará un enlace simbólico.

**Nota:**

*   Los programas pueden iniciarse automáticamente solo con el inicio de sesión, mientras que los scripts de shell también se pueden ejecutar en el apagado o incluso antes de que se inicie Plasma.
*   Los scripts de shell solo se ejecutarán si están marcados como [ejecutables](/index.php/Help:Reading_(Espa%C3%B1ol)#Hacer_ejecutable "Help:Reading (Español)").

*   Coloque [entradas del escritorio](/index.php/Desktop_entries "Desktop entries") (es decir, archivos *.desktop*) en el directorio [XDG Autostart](/index.php/XDG_Autostart_(Espa%C3%B1ol) "XDG Autostart (Español)") apropiado.

*   Coloque o guarde los scripts de shell en uno de los siguientes directorios:

	`~/.config/plasma-workspace/env/`

	para ejecutar scripts al iniciar sesión antes de iniciar Plasma.

	`~/.config/autostart-scripts/`

	para ejecutar scripts al iniciar sesión.

	`~/.config/plasma-workspace/shutdown/`

	para ejecutar scripts en el apagado.

### Phonon

De [Wikipedia](https://en.wikipedia.org/wiki/es:Phonon_(KDE) "wikipedia:es:Phonon (KDE)"):

	Phonon es el framework multimedia estándar de KDE 4, también parte de Qt desde la versión 4.4.

	El objetivo de Phonon es facilitar a los programadores el uso de tecnologías multimedia en sus programas, así como asegurar que las aplicaciones que usen Phonon funcionen en diversas plataformas y arquitecturas de sonido.

Phonon está siendo ampliamente utilizando en KDE, tanto para audio (por ejemplo, las notificaciones del sistema o aplicaciones de audio de KDE) como para vídeo (por ejemplo, las miniaturas de video de [Dolphin](/index.php/Dolphin "Dolphin")).

#### ¿Qué backend debo elegir?

Puede elegir entre backends basados en [GStreamer](/index.php/GStreamer_(Espa%C3%B1ol) "GStreamer (Español)") y [VLC](/index.php/VLC_media_player_(Espa%C3%B1ol) "VLC media player (Español)") - cada uno disponible en versiones para aplicaciones Qt4 y aplicaciones Qt5 ([phonon-qt4-gstreamer](https://aur.archlinux.org/packages/phonon-qt4-gstreamer/), [phonon-qt5-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt5-gstreamer) - [phonon-qt4-vlc](https://aur.archlinux.org/packages/phonon-qt4-vlc/), [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc)).

[El anterior (Phonon) prefiere VLC](https://www.phoronix.com/scan.php?page=news_item&px=MTUwNDM), pero algunas distribuciones de Linux más prominentes (Kubuntu y Fedora-KDE por ejemplo) prefieren GStreamer porque les permite dejar fácilmente de lado los códecs patentados MPEG de la instalación por defecto. Ambos backends tienen un [conjunto de características](https://community.kde.org/Phonon/FeatureMatrix) ligeramente diferentes. El backend de Gstreamer tiene alguna dependencias de códecs opcionales, instálelos según sea necesario:

*   [gst-libav](https://www.archlinux.org/packages/?name=gst-libav) - códecs de Libav.
*   [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good) - Soporte de PulseAudio y códecs adicionales.
*   [gst-plugins-ugly](https://www.archlinux.org/packages/?name=gst-plugins-ugly) - códecs adicionales.
*   [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad) - códecs adicionales.

En el pasado, también se desarrollaron otros backends, pero ya no se mantienen y sus paquetes AUR se han eliminado.

**Nota:**

*   Se pueden instalar varios backends a la vez y priorizarlos en *Preferencias del sistema > Multimedia > Audio y vídeo > Motor*.
*   Según los [foros de KDE](https://forum.kde.org/viewtopic.php?f=250&t=126476&p=335080), el backend de VLC carece de soporte para [ReplayGain](https://en.wikipedia.org/wiki/ReplayGain "wikipedia:ReplayGain").
*   Si usa el backend VLC, puede experimentar cuelgues cada vez que Plasma quiera enviarle una advertencia sonora y en muchos otros casos también [[4]](https://forum.kde.org/viewtopic.php?f=289&t=135956). Una posible solución es reconstruir la caché de los plugins de VLC:

 `# /usr/lib/vlc/vlc-cache-gen /usr/lib/vlc/plugins` 

## Aplicaciones

El proyecto KDE proporciona un conjunto de aplicaciones que se integran con el escritorio Plasma. Véase el grupo [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) para obtener una lista completa de las aplicaciones disponibles. Véase también [Category:KDE (Español)](/index.php/Category:KDE_(Espa%C3%B1ol) "Category:KDE (Español)") para los artículos relacionados con las aplicaciones KDE .

Aparte de los programas provistos en KDE Applications, hay muchas otras aplicaciones disponibles que pueden complementar el escritorio Plasma. Algunas de éstas se tratan a continuación.

### Administración del sistema

#### Detener Xorg server a través de las preferencias del sistema KDE

Navegue al submenú *Preferencias del sistema > Dispositivos de entrada > Teclado > Avanzado (pestaña) > "Key Sequence to kill the X server"* y asegúrese de que la casilla esté marcada.

#### KCM

KCM significa **KC**onfig **M**odule. Los KCM pueden ayudarle a configurar su sistema al proporcionar interfaces en preferencias del sistema, o a través de la línea de comandos con *kcmshell5*.

*   **kde-gtk-config** — Configurador GTK2 y GTK3 para KDE.

	[https://cgit.kde.org/kde-gtk-config.git](https://cgit.kde.org/kde-gtk-config.git) || [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)

*   **Políticas del sistema** — Conjunto de módulos de configuración que permite al administrador cambiar la configuración de [PolicyKit](/index.php/PolicyKit "PolicyKit").

	[https://cgit.kde.org/polkit-kde-kcmodules-1.git](https://cgit.kde.org/polkit-kde-kcmodules-1.git) || [kcm-polkit-kde-git](https://aur.archlinux.org/packages/kcm-polkit-kde-git/)

*   **wacom tablet** — Interfaz gráfica de KDE para los controladores Linux Wacom.

	[https://www.linux-apps.com/p/1127862/](https://www.linux-apps.com/p/1127862/) || [kcm-wacomtablet](https://www.archlinux.org/packages/?name=kcm-wacomtablet)

*   **Kcmsystemd** — módulo de control systemd para KDE.

	[https://github.com/rthomsen/kcmsystemd](https://github.com/rthomsen/kcmsystemd) || [systemd-kcm](https://aur.archlinux.org/packages/systemd-kcm/)

Puede encontrar más KCMs en [linux-apps.com](https://www.linux-apps.com/search?projectSearchText=KCM).

### Búsqueda de escritorio

KDE implementa la búsqueda de escritorio con un software llamado [Baloo](/index.php/Baloo "Baloo"), una solución de indexación y de búsqueda de archivos.

### Navegadores web

Los siguientes navegadores web pueden integrarse con Plasma:

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — Parte del proyecto KDE, es compatible con dos motores de renderización - KHTML y Qt WebEngine basado en [Chromium](/index.php/Chromium_(Espa%C3%B1ol) "Chromium (Español)").

	[https://konqueror.org/](https://konqueror.org/) || [konqueror](https://www.archlinux.org/packages/?name=konqueror)

*   **[Falkon](https://en.wikipedia.org/wiki/Falkon "wikipedia:Falkon")** — Un navegador web Qt con funciones de integración Plasma, anteriormente conocido como Qupzilla. Utiliza Qt WebEngine.

	[https://userbase.kde.org/Falkon/](https://userbase.kde.org/Falkon/) || [falkon](https://www.archlinux.org/packages/?name=falkon)

*   **[Chromium](/index.php/Chromium "Chromium")** — Chromium y su variante patentada Google Chrome tienen una integración de Plasma limitada. [Pueden usar KWallet](/index.php/KDE_Wallet_(Espa%C3%B1ol)#KDE_Wallet_para_Chromium "KDE Wallet (Español)") y las ventanas de KDE Abrir/Guardar.

	[https://www.chromium.org/](https://www.chromium.org/) || [chromium](https://www.archlinux.org/packages/?name=chromium)

*   **[Firefox](/index.php/Firefox "Firefox")** — Firefox puede configurarse para integrarse mejor con Plasma. Véase [Integración de Firefox KDE](/index.php/Firefox_(Espa%C3%B1ol)#Mejorar_la_integración_de_Firefox_con_KDE "Firefox (Español)") para obtener más información.

	[https://mozilla.org/firefox](https://mozilla.org/firefox) || [firefox](https://www.archlinux.org/packages/?name=firefox)

**Sugerencia:** A partir de Plasma 5.13, uno puede integrar [Firefox](/index.php/Firefox_(Espa%C3%B1ol) "Firefox (Español)") o [Chrome](/index.php/Chromium_(Espa%C3%B1ol) "Chromium (Español)") con Plasma: proporcione el control de reproducción de medios desde la bandeja de Plasma, descargue notificaciones y encuentre pestañas abiertas en KRunner. [Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [plasma-browser-integration](https://www.archlinux.org/packages/?name=plasma-browser-integration) y el complemento del navegador correspondiente. El soporte de Chrome/Chromium ya debería estar incluido, para el complemento de Firefox véase [Integración de Firefox KDE](/index.php/Firefox_(Espa%C3%B1ol)#Mejorar_la_integración_de_Firefox_con_KDE "Firefox (Español)").

### PIM

KDE ofrece su propia pila para la gestión de información personal. Esto incluye emails, contactos, calendario, etc. Para instalar todos los paquetes PIM, puede usar el metapaquete [kdepim-meta](https://www.archlinux.org/packages/?name=kdepim-meta).

#### Akonadi

Akonadi es un sistema destinado a actuar como caché local para datos PIM, independientemente de su origen, para que luego pueda ser utilizado por otras aplicaciones. Esto incluye los emails, contactos, calendarios, eventos, diarios, alarmas, notas, etc. del usuario. Akonadi no almacena ningún dato por sí mismo: el formato de almacenamiento depende de la naturaleza de los datos (por ejemplo, los contactos pueden almacenarse en formato vCard).

Instale [akonadi](https://www.archlinux.org/packages/?name=akonadi). Para obtener complementos adicionales, instale [kdepim-addons](https://www.archlinux.org/packages/?name=kdepim-addons).

**Nota:** Si desea usar un motor de base de datos que no sea [MariaDB](/index.php/MariaDB "MariaDB"), al instalar el paquete [akonadi](https://www.archlinux.org/packages/?name=akonadi), use el siguiente comando para omitir la instalación de las dependencias [mariadb](https://www.archlinux.org/packages/?name=mariadb):
```
# pacman -S akonadi --assume-installed mariadb

```

Véase también [FS#32878](https://bugs.archlinux.org/task/32878).

##### PostgreSQL

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [postgresql](https://www.archlinux.org/packages/?name=postgresql).

Para usar [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") edite el archivo de configuración de Akonadi para que tenga el siguiente contenido:

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
Driver=QPSQL

[QPSQL]
Host=
InitDbPath=/usr/bin/initdb
Name=akonadi
ServerPath=/usr/bin/pg_ctl
StartServer=true

```

**Nota:** El valor `Host=` será establecido por Akonadi cuando se inicie por primera vez.

Inicie Akonadi con `akonadictl start`, y verifique su estado: `akonadictl status`.

##### SQLite

Para usar [SQLite](/index.php/SQLite "SQLite") edite el archivo de configuración de Akonadi para que coincida con la configuración que se muestra a continuación:

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
Driver=QSQLITE3

[QSQLITE3]
Name=/home/*username*/.local/share/akonadi/akonadi.db
```

##### Deshabilitar Akonadi

Véase esta [sección en la base de usuarios de KDE](https://userbase.kde.org/Akonadi#Disabling_the_Akonadi_subsystem).

### KDE Telepathy

[KDE Telepathy](https://community.kde.org/KTp) es un proyecto con el objetivo de integrar estrechamente la mensajería instantánea con el escritorio KDE. Utiliza el framework Telepathy como backend y está destinado a reemplazar a Kopete.

Para instalar todos los protocolos de Telepathy, instale el grupo [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). Para utilizar el cliente KDE Telepathy, instale el paquete [telepathy-kde-meta](https://www.archlinux.org/packages/?name=telepathy-kde-meta) que incluye todos los paquetes contenidos en el grupo [telepathy-kde](https://www.archlinux.org/groups/x86_64/telepathy-kde/).

#### Utilizar Telegram con KDE Telepathy

El protocolo [Telegram](/index.php/Telegram "Telegram") está disponible usando [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), instalando [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) o [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/) y [telepathy-morse-git](https://aur.archlinux.org/packages/telepathy-morse-git/). El nombre de usuario es el número de teléfono de la cuenta de Telegram (complételo con el prefijo nacional `+*xx*`, por ejemplo, `+34` para España).

La configuración a través de la interfaz gráfica puede ser complicada: si el número de teléfono no se acepta al configurar una nueva cuenta en el cliente KDE Telepathy (con un mensaje de error quejándose de un parámetro inválido que impide la creación de la cuenta), insértelo entre comillas simples y luego elimine las comillas manualmente del archivo de configuración (`~/.local/share/telepathy/mission-control/accounts.cfg`) después de la creación de la cuenta (si las comillas no se eliminan posteriormente, debería salir un error de autenticación).

**Nota:** El archivo de configuración debería editarse manualmente cuando KDE Telepathy no se esté ejecutando, por ejemplo, cuando no hay una sesión de escritorio KDE activa, de lo contrario, el software puede sobrescribir los cambios realizados manualmente.

### KDE Connect

[KDE Connect](https://community.kde.org/KDEConnect) proporciona varias características para conectar su teléfono [Android](/index.php/Android_(Espa%C3%B1ol) "Android (Español)") con su escritorio Linux:

*   Comparta archivos y URLs a/desde KDE desde/a cualquier aplicación, sin cables.
*   Emulación de panel táctil: use la pantalla de su teléfono como si fuera el panel táctil de su ordenador.
*   Sincronización de notificaciones (4.3+): lea sus notificaciones Android desde el escritorio.
*   Portapapeles compartido: copie y pegue entre su teléfono y su ordenador.
*   Control remoto multimedia: utilize su teléfono como un control remoto para reproductores multimedia en Linux.
*   Conexión WiFi: no necesita cable usb ni bluetooth.
*   Cifrado RSA: su información está segura.

Deberá instalar KDE Connect tanto en su ordenador como en Android. Para el PC, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect). Para Android, instale KDE Connect desde [Google Play](https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp) o desde [F-Droid](https://f-droid.org/packages/org.kde.kdeconnect_tp/).

Es posible usar KDE Connect incluso si no usa el escritorio Plasma. Para los entornos de escritorio que utilizan AppIndicators, como Unity, instale también el paquete [indicator-kdeconnect](https://aur.archlinux.org/packages/indicator-kdeconnect/). Para los usuarios de GNOME, se puede lograr una mejor integración instalando [gnome-shell-extension-gsconnect](https://aur.archlinux.org/packages/gnome-shell-extension-gsconnect/) en vez de [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect).

Si usa un [cortafuegos](/index.php/Firewalls_(Espa%C3%B1ol) "Firewalls (Español)"), necesita abrir los puertos UDP y TCP `1714` a través de `1764`. Véase [https://community.kde.org/KDEConnect#Troubleshooting](https://community.kde.org/KDEConnect#Troubleshooting).

## Consejos y trucos

### Usar un gestor de ventanas diferente

La configuración del selector de componentes en Plasma ya no permite cambiar el gestor de ventanas. [[5]](https://github.com/KDE/plasma-desktop/commit/2f83a4434a888cd17b03af1f9925cbb054256ade) Para cambiar el gestor de ventanas utilizado, debe establecer la [variable de entorno](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") `KDEWM` antes del inicio de KDE. [[6]](https://wiki.haskell.org/Xmonad/Using_xmonad_in_KDE) Para ello, puede crear un script llamado `set_window_manager.sh` en `~/.config/plasma-workspace/env/` y exportar la variable `KDEWM` allí. Por ejemplo, para utilizar el gestor de ventanas i3:

 `~/.config/plasma-workspace/env/set_window_manager.sh`  `export KDEWM=/usr/bin/i3` 

Y luego hacerlo ejecutable:

 `$ chmod +x ~/.config/plasma-workspace/env/set_window_manager.sh` 

#### Sesión KDE/Openbox

El paquete [openbox](https://www.archlinux.org/packages/?name=openbox) proporciona una sesión para usar KDE con [Openbox](/index.php/Openbox_(Espa%C3%B1ol) "Openbox (Español)"). Para hacer uso de esta sesión, seleccione *KDE/Openbox* en el menú [gestor de pantallas](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)").

Para aquellos que inician sesión manualmente, agregue la siguiente línea a su configuración [xinit](/index.php/Xinit_(Espa%C3%B1ol) "Xinit (Español)"):

 `~/.xinitrc` 
```
exec openbox-kde-session

```

#### Rehabilitar efectos de composición

Al reemplazar Kwin con un gestor de ventanas que no proporciona un Compositor (como Openbox), se perderá cualquier efecto de composición del escritorio, por ejemplo, la transparencia. En este caso, instale y ejecute un gestor de Composite separado para proporcionar los efectos como [Xcompmgr](/index.php/Xcompmgr_(Espa%C3%B1ol) "Xcompmgr (Español)") o [Compton](/index.php/Compton "Compton").

### Configurar la resolución del monitor / múltiples monitores

Para habilitar la gestión de resolución de pantalla y múltiples monitores en Plasma, instale [kscreen](https://www.archlinux.org/packages/?name=kscreen). Esto agrega las opciones adicionales a *Preferencias del sistema > Pantalla y monitor*.

### Deshabilitar la apertura del lanzador de aplicaciones con la tecla Super (tecla Windows)

Para deshabilitar esta característica, actualmente puede ejecutar el siguiente comando:

```
$ kwriteconfig5 --file kwinrc --group ModifierOnlyShortcuts --key Meta ""

```

### Deshabilitar que los marcadores se muestren en el menú de aplicaciones

Si tiene instalada la integración del navegador de Plasma, KDE mostrará marcadores en el lanzador de aplicaciones.

Para deshabilitar esta característica, ejecute las siguientes órdenes:

```
$ mkdir ~/.local/share/kservices5
$ sed 's/EnabledByDefault=true$/EnabledByDefault=false/' /usr/share/kservices5/plasma-runner-bookmarks.desktop > ~/.local/share/kservices5/plasma-runner-bookmarks.desktop

```

## Solución de problemas

### Fuentes tipográficas

#### Las fuentes en una sesión Plasma se ven mal

Pruebe a instalar los paquetes [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) y [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation).

Después de la instalación, asegúrese de cerrar sesión y volver a iniciarla. No debería tener que modificar nada en *Preferencias del sistema > Tipos de letra*. Si está utilizando [qt5ct](https://www.archlinux.org/packages/?name=qt5ct), la preferencias de la Herramienta de Configuración Qt5 pueden anular los ajustes de los tipos de letra en las preferencias del sistema.

Si ha configurado personalmente el renderizado de sus [Fuentes](/index.php/Fonts_(Espa%C3%B1ol) "Fonts (Español)"), tenga en cuenta que las preferencias del sistema pueden alterar su apariencia. Cuando vaya a *Preferencias del sistema > Tipos de letra*, las preferencias del sistema probablemente alterarán el archivo de configuración de las fuentes (`fonts.conf`).

No hay forma de evitar esto, pero, si configura los valores para que coincidan con su archivo `fonts.conf`, el renderizado esperado de las fuentes volverá (se requerirá que reinicie su aplicación o, en algunos casos, que reinicie su escritorio). Tenga en cuenta que las preferencias de las fuentes de Gnome también hacen esto.

#### Las fuentes son enormes o parecen desproporcionadas

Intente forzar la fuente DPI a `**96**` en *Preferencias del sistema > Tipos de letra*.

Si eso no funciona, intente establecer el DPI directamente en su configuración de Xorg como se documenta en [Xorg#Configuración manual de DPI](/index.php/Xorg_(Espa%C3%B1ol)#Configuración_manual_de_DPI "Xorg (Español)").

### Configuración relacionada

Muchos problemas en KDE están relacionados con su configuración.

#### El escritorio Plasma se comporta de manera extraña

Los problemas en Plasma son generalmente causados por *widgets de Plasma* inestables (llamados coloquialmente *plasmoides*) o *temas de Plasma*. Primero, encuentre cuál fue el último widget o tema que instaló y deshabilítelo o desinstálelo.

Por lo tanto, si su escritorio muestra repentinamente un «bloqueo», es probable que esto se deba a un widget instalado defectuoso. Si no puede recordar qué widget instaló antes de que comenzara el problema (a veces puede ser un problema irregular), intente localizarlo eliminando cada widget hasta que el problema cese. Luego, puede desinstalar el widget y presentar un informe de error en el [seguimiento de errores de KDE](https://bugs.kde.org/) **solo si es un widget oficial**. Si no lo es, se recomienda buscar la entrada en la [KDE Store](https://store.kde.org/) e informar al desarrollador de ese widget sobre el problema (detallando los pasos para reproducirlo, etc.).

Si no puede encontrar el problema, pero no quiere que se pierdan *todos* los ajustes, vaya a `~/.config/` y ejecute el siguiente comando:

```
$ for j in plasma*; do mv -- "$j" "${j%}.bak"; done

```

Este comando renombrará **todos** los archivos de configuración relacionados con Plasma de su usuario a **.bak* (por ejemplo, `plasmarc.bak`) y cuando vuelva a iniciar sesión en Plasma, tendrá la configuración predeterminada de nuevo. Para deshacer esa acción, elimine la extensión de archivo *.bak*. Si ya tiene archivos **.bak*, renómbrelos, muévalos o elimínelos primero. Se recomienda encarecidamente que se creen regularmente copias de seguridad de todos modos. Véase [sincronización y programas de copia de seguridad](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs") para obtener una lista de posibles soluciones.

#### Limpiar la caché para resolver problemas de actualización

El [problema](https://bbs.archlinux.org/viewtopic.php?id=135301) puede ser causado por un caché antiguo. A veces, después de una actualización, la memoria caché antigua podría presentar un comportamiento extraño y difícil de depurar, como shells no detenibles, cuelgues al cambiar varias configuraciones, que Ark no pueda extraer archivos o que Amarok no reconozca ninguna de sus canciones. Esta solución también puede resolver problemas con aplicaciones KDE y Qt que se ven mal después de una actualización.

Reconstruya la caché usando los siguientes comandos:

```
$ rm ~/.config/Trolltech.conf
$ kbuildsycoca5 --noincremental

```

Opcionalmente, vacíe los contenidos de la carpeta `~/.cache/`, sin embargo, esto también borrará la caché de otras aplicaciones:

```
$ rm -rf ~/.cache/*

```

### Problemas gráficos

Asegúrese de tener instalado el controlador adecuado para su GPU. Véase [Xorg#Instalación del controlador](/index.php/Xorg_(Espa%C3%B1ol)#Instalación_del_controlador "Xorg (Español)") para obtener más información. Si tiene una tarjeta más antigua, podría ayudar el [#Deshabilitar los efectos del escritorio manualmente o automáticamente para aplicaciones definidas](#Deshabilitar_los_efectos_del_escritorio_manualmente_o_automáticamente_para_aplicaciones_definidas) o [#Deshabilitar la composición](#Deshabilitar_la_composición).

#### Obtener el estado actual de KWin para fines de soporte y depuración

Este comando muestra un resumen del estado actual de KWin, incluidas las opciones utilizadas, el backend de composición utilizado y las capacidades relevantes del controlador OpenGL. Véase más en [el blog de Martin](https://blog.martin-graesslin.com/blog/2012/03/on-getting-help-for-kwin-and-helping-kwin/).

```
$ qdbus org.kde.KWin /KWin supportInformation

```

#### Deshabilitar los efectos del escritorio manualmente o automáticamente para aplicaciones definidas

Plasma tiene habilitados los efectos del escritorio de manera predeterminada y no todas las aplicaciones los deshabilitarán automáticamente, por ejemplo, los juegos. Puede deshabilitar los efectos del escritorio en *Preferencias del sistema > Comportamiento del escritorio > Efectos del escritorio* y alternar los efectos del escritorio con `Alt+Shift+F12`.

Adicionalmente, puede crear reglas KWin personalizadas para deshabilitar/habilitar automáticamente la composición cuando cierta aplicación/ventana se inicie en *Preferencias del sistema > Gestión de ventanas > Reglas de la ventana*.

#### Deshabilitar la composición

En *Preferencias del sistema > Pantalla y monitor > Compositor*, desmarque *Activar el compositor durante el inicio* y reinicie Plasma.

#### Parpadeo en pantalla completa cuando la composición está habilitada

En *Preferencias del sistema > Pantalla y monitor > Compositor*, desmarque *Permitir que las aplicaciones bloqueen la composición*. Esto puede afectar al rendimiento.

#### Screen tearing con NVIDIA

Véase [NVIDIA/Solución de problemas#Evitar screen tearing en KDE (KWin)](/index.php/NVIDIA/Troubleshooting#Avoid_screen_tearing_in_KDE_(KWin) "NVIDIA/Troubleshooting").

#### El cursor de Plasma a veces se muestra incorrectamente

Cree el directorio `~/.icons/default`, y dentro de él un archivo llamado `index.theme` con el siguiente contenido:

 `~/.icons/default/index.theme` 
```
[Icon Theme]
Inherits=breeze_cursors
```

Ejecute el siguiente comando:

```
$ ln -s /usr/share/icons/breeze_cursors/cursors ~/.icons/default/cursors

```

#### Se ha establecido una resolución de pantalla inutilizable

Sus ajustes de configuración locales para kscreen pueden anular aquellos establecidos en `xorg.conf`. Busque los archivos de configuración de kscreen en `~/.local/share/kscreen/` y revise si el modo está establecido en una resolución que no es compatible con su monitor.

### Problemas de sonido

**Nota:** Primero asegúrese de tener [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) instalado.

#### No hay sonido después de suspender

Si no hay sonido después de la suspensión y si KMix no muestra dispositivos de audio los cuales deberían estar ahí, reiniciar plasmashell y pulseaudio podría ayudar:

```
$ killall plasmashell
$ systemctl --user restart pulseaudio.service
$ plasmashell

```

Es posible que algunas aplicaciones también deban reiniciarse para que el sonido se reproduzca de nuevo.

#### Los archivos MP3 no se pueden reproducir cuando se utiliza el backend GStreamer Phonon

Esto se puede resolver instalando el complemento libav de GStreamer (paquete [gst-libav](https://www.archlinux.org/packages/?name=gst-libav)). Si aún tiene problemas, puede intentar cambiar el backend de Phonon utilizado instalando otro como [phonon-qt4-vlc](https://aur.archlinux.org/packages/phonon-qt4-vlc/) o [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc).

Luego, asegúrese de que se prefiera el backend vía *Preferencias del sistema > Multimedia > Audio y vídeo > Motor*.

### Administración de energía

#### No hay opciones de Suspender/Hibernar

Si su sistema puede suspender o hibernar usando [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") pero estas opciones no se muestran en KDE, asegúrese de que [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) esté instalado.

### KMail

#### Limpie la configuración de akonadi para arreglar KMail

En primer lugar, asegúrese de que KMail no se está ejecutando. Después, haga una copia de seguridad de la configuración:

```
$ cp -a ~/.local/share/akonadi ~/.local/share/akonadi-old
$ cp -a ~/.config/akonadi ~/.config/akonadi-old

```

Inicie *Preferencias del sistema > Personal* y elimine todos los medios. Vuelva a Dolphin y elimine el `~/.local/share/akonadi/` original y `~/.config/akonadi/` - las copias que hizo aseguran que pueda revertir los cambios en caso de ser necesario.

Ahora vuelva a la página de preferencias del sistema y agregue cuidadosamente los medios necesarios. Debería ver la lectura de medios en sus carpetas de correo. A continuación, inicie Kontact/KMail para ver si funciona correctamente.

#### Vaciar la bandeja de entrada IMAP en KMail

Para algunas cuentas IMAP, KMail mostrará la bandeja de entrada como un contenedor de nivel superior (por lo que no será posible leer los mensajes allí) con todas las demás carpetas de esta cuenta dentro. [[7]](https://bugs.kde.org/show_bug.cgi?id=284172). Para resolver este problema, simplemente deshabilite las suscripciones del lado del servidor en la configuración de la cuenta KMail.

### Conexión

#### Se congela cuando se usa montaje automático en un volumen NFS

El uso de [Fstab#Montaje automático con systemd](/index.php/Fstab_(Espa%C3%B1ol)#Montaje_automático_con_systemd "Fstab (Español)") en un volumen [NFS](/index.php/NFS_(Espa%C3%B1ol) "NFS (Español)") puede provocar bloqueos, véase [informe de errores previos](https://bugs.kde.org/show_bug.cgi?id=354137).

### Registro agresivo del diario QXcbConnection

Véase [Qt#Deshabilitar/Cambiar el comportamiento de registro del diario Qt](/index.php/Qt#Disable/Change_Qt_journal_logging_behaviour "Qt").

### Las aplicaciones KF5/Qt 5 no muestran iconos en i3/FVWM/awesome

Véase [Qt#Configuración de aplicaciones Qt5 en entornos que no sean KDE Plasma](/index.php/Qt#Configuration_of_Qt5_apps_under_environments_other_than_KDE_Plasma "Qt").

### Problemas al guardar las credenciales y los diálogos de KWallet se muestran de manera persistente

No se recomienda desactivar el sistema de guardado de contraseñas de [KWallet](/index.php/KDE_Wallet_(Espa%C3%B1ol) "KDE Wallet (Español)") en las preferencias del usuario, ya que es necesario para guardar credenciales cifradas como las frases de contraseñas WiFi de cada usuario. La persistencia de los diálogos de KWallet puede ser consecuencia de desactivarlo.

En caso de que encuentre molestos los diálogos para desbloquear la cartera cuando las aplicaciones deseen acceder a ella, puede permitir que los [gestores de pantallas](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)") [SDDM](/index.php/SDDM "SDDM") y [LightDM](/index.php/LightDM_(Espa%C3%B1ol) "LightDM (Español)") desbloqueen la cartera al iniciar sesión automáticamente, véase [KDE Wallet#Desbloquear KDE Wallet automáticamente al iniciar sesión](/index.php/KDE_Wallet_(Espa%C3%B1ol)#Desbloquear_KDE_Wallet_automáticamente_al_iniciar_la_sesión "KDE Wallet (Español)"). La primera cartera debe ser generada por KWallet (y no por el usuario) para poder ser utilizada por las credenciales del programa del sistema.

En caso de que desee que las credenciales de la cartera no se abran en la memoria para cada aplicación, puede restringir su acceso a las aplicaciones con [kwalletmanager](https://www.archlinux.org/packages/?name=kwalletmanager) en la configuración de KWallet.

Si no le interesa para nada el cifrado de credenciales, simplemente puede dejar los formularios de contraseñas en blanco cuando KWallet le pida la contraseña mientras crea una cartera. En este caso, las aplicaciones pueden acceder a las contraseñas sin tener que desbloquear primero la cartera.

### Discover no muestra ninguna aplicación

Esto se puede resolver instalando [packagekit-qt5](https://www.archlinux.org/packages/?name=packagekit-qt5).

### kscreenlocker_greet usa mucha CPU con controladores de NVIDIA

Tal y como se describe en [KDE Bug 347772](https://bugs.kde.org/show_bug.cgi?id=347772) los controladores OpenGL de NVIDIA y QML pueden no funcionar bien con Qt 5\. Esto puede llevar a `kscreenlocker_greet` a utilizar mucha CPU después de desbloquear la sesión. Para resolver este problema, establezca la [variable de entorno](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") `QSG_RENDERER_LOOP` a `basic`.

A continuación, elimine las instancias anteriores del greeter con `killall kscreenlocker_greet`.

### Error 22 del SO cuando se ejecuta Akonadi en ZFS

Si su directorio de inicio está en un grupo [ZFS](/index.php/ZFS "ZFS"), cree un archivo `~/.config/akonadi/mysql-local.conf` con el siguiente contenido:

```
[mysqld]
innodb_use_native_aio = 0

```

Véase [MariaDB#OS error 22 when running on ZFS](/index.php/MariaDB#OS_error_22_when_running_on_ZFS "MariaDB").

### Algunos programas no pueden desplazarse cuando sus ventanas están inactivas

Esto se debe a la problemática manera en que GTK3 maneja los eventos de desplazamiento del ratón. Una solución para esto es establecer la [variable de entorno](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") `GDK_CORE_DEVICE_EVENTS=1`. Sin embargo, esta solución también rompe el desplazamiento suave del panel táctil y el desplazamiento de la pantalla táctil.

## Véase también

*   [Página web de KDE](https://www.kde.org/)
*   [Seguimiento de errores de KDE](https://bugs.kde.org/)
*   [Blog de Martin Graesslin](https://blog.martin-graesslin.com/blog/kategorien/kde/)