**Estado de la traducción**
Este artículo es una traducción de [GTK+](/index.php/GTK%2B "GTK+"), revisada por última vez el **2018-10-24**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GTK%2B&diff=0&oldid=550627) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Uniformidad en aplicaciones Qt y GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications_(Espa%C3%B1ol) "Uniform look for Qt and GTK applications (Español)")
*   [Qt](/index.php/Qt "Qt")
*   [GNU](/index.php/GNU_(Espa%C3%B1ol) "GNU (Español)")
*   [GTK+/Development](/index.php/GTK%2B/Development "GTK+/Development")

De la [web de GTK+](http://www.gtk.org):

	GTK+, o GIMP Toolkit, es un conjunto de herramientas multiplataforma para crear interfaces gráficas de usuario. Al ofrecer un conjunto completo de widgets, GTK+ es adecuado para proyectos que van desde pequeñas herramientas con funcionalidad reducida hasta completas suites de aplicaciones.

GTK+ (GIMP Toolkit) fue originalmente creado por el [Proyecto GNU](/index.php/GNU_(Espa%C3%B1ol) "GNU (Español)") para [GIMP](/index.php/GIMP "GIMP"), pero ahora es un conjunto de herramientas popular con conectores a múltiples lenguajes de programación. Este artículo explora las herramientas utilizadas para configurar el tema GTK+, el estilo, los iconos, las fuentes y sus tamaños, y también detalla la configuración manual.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Temas](#Temas)
    *   [2.1 GTK+ y Qt](#GTK+_y_Qt)
*   [3 Herramientas de configuración](#Herramientas_de_configuración)
*   [4 Configuración](#Configuración)
    *   [4.1 Configuración básica del tema](#Configuración_básica_del_tema)
    *   [4.2 Variante oscura del tema](#Variante_oscura_del_tema)
    *   [4.3 Atajos de teclado](#Atajos_de_teclado)
        *   [4.3.1 Combinaciones de teclas Emacs](#Combinaciones_de_teclas_Emacs)
    *   [4.4 Retraso del menú de GNOME](#Retraso_del_menú_de_GNOME)
    *   [4.5 Reducir el tamaño de los widgets](#Reducir_el_tamaño_de_los_widgets)
    *   [4.6 Ocultar los botones CSD](#Ocultar_los_botones_CSD)
    *   [4.7 Desactivar pegar desde el ratón](#Desactivar_pegar_desde_el_ratón)
    *   [4.8 Posición inicial del selector de archivos](#Posición_inicial_del_selector_de_archivos)
    *   [4.9 Comportamiento de desplazamiento heredado](#Comportamiento_de_desplazamiento_heredado)
    *   [4.10 Deshabilitar las barras de desplazamiento superpuestas](#Deshabilitar_las_barras_de_desplazamiento_superpuestas)
        *   [4.10.1 Eliminar indicadores de la barra de desplazamiento de superposición](#Eliminar_indicadores_de_la_barra_de_desplazamiento_de_superposición)
*   [5 Backends de GDK](#Backends_de_GDK)
    *   [5.1 Backend de Broadway](#Backend_de_Broadway)
    *   [5.2 Backend de Wayland](#Backend_de_Wayland)
*   [6 Solución de problemas](#Solución_de_problemas)
    *   [6.1 Diferentes temas entre aplicaciones GTK+ 2 y GTK+ 3](#Diferentes_temas_entre_aplicaciones_GTK+_2_y_GTK+_3)
    *   [6.2 Tema no aplicado en aplicaciones del superusuario](#Tema_no_aplicado_en_aplicaciones_del_superusuario)
    *   [6.3 Decoraciones del lado del cliente](#Decoraciones_del_lado_del_cliente)
    *   [6.4 Cedilla ç/Ç en lugar de ć/Ć](#Cedilla_ç/Ç_en_lugar_de_ć/Ć)
    *   [6.5 Suprimir advertencia referente al bus de accesibilidad](#Suprimir_advertencia_referente_al_bus_de_accesibilidad)
    *   [6.6 Falta de coincidencia del color de fondo de la barra de título](#Falta_de_coincidencia_del_color_de_fondo_de_la_barra_de_título)
    *   [6.7 Eventos de enfoque incorrecto con administradores de ventanas de mosaico](#Eventos_de_enfoque_incorrecto_con_administradores_de_ventanas_de_mosaico)
    *   [6.8 Soporte de miniaturas para el diálogo del archivo GTK+ 2](#Soporte_de_miniaturas_para_el_diálogo_del_archivo_GTK+_2)
    *   [6.9 Iconos de botón/menú en algunas aplicaciones en la sesión Wayland de GNOME](#Iconos_de_botón/menú_en_algunas_aplicaciones_en_la_sesión_Wayland_de_GNOME)
    *   [6.10 GTK+ 3 sin polkit](#GTK+_3_sin_polkit)
    *   [6.11 Algunos temas de GTK+ 2 solo cambian la paleta de colores de la interfaz de usuario](#Algunos_temas_de_GTK+_2_solo_cambian_la_paleta_de_colores_de_la_interfaz_de_usuario)
*   [7 Ejemplos](#Ejemplos)
*   [8 Véase también](#Véase_también)

## Instalación

Dos versiones de GTK+ estan disponibles en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Se pueden [instalar](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") con los siguientes paquetes:

*   **GTK+ 3.x** disponible con el paquete [gtk3](https://www.archlinux.org/packages/?name=gtk3).
*   **GTK+ 2.x** disponible con el paquete [gtk2](https://www.archlinux.org/packages/?name=gtk2).
*   **GTK+ 1.x** disponible con el paquete [gtk](https://aur.archlinux.org/packages/gtk/).

## Temas

En GTK+ 2, el tema predeterminado es *Raleigh*, pero Arch Linux tiene un archivo de configuración personalizado en `/usr/share/gtk-2.0/gtkrc`, que establece *Adwaita* como el tema predeterminado. En GTK+ 3, el tema predeterminado es *Adwaita*, pero también se incluyen *HighContrast*, *HighContrastInverse* y *Raleigh*.

Para forzar un tema específico, establezca las siguientes [variables de entorno](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)").

*   Para GTK+ 2, utilice `GTK2_RC_FILES`. Por ejemplo para lanzar [GIMP](/index.php/GIMP "GIMP") con el tema *Industrial*:

```
$ GTK2_RC_FILES=/usr/share/themes/Industrial/gtk-2.0/gtkrc gimp

```

**Sugerencia:** `gtkrc` puede ser también un archivo personalizado en su directorio de inicio creado por cualquiera de las [#Herramientas de configuración](#Herramientas_de_configuración).

*   Para GTK+ 3, utilice `GTK_THEME`. Por ejemplo para lanzar la calculadora de GNOME con la variante oscura de *Adwaita*:

```
$ GTK_THEME=Adwaita:dark gnome-calculator

```

Se pueden instalar más temas desde los repositorios oficiales o desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"). Los temas extraídos manualmente van en el directorio `~/.themes/` o `~/.local/share/themes/`.

**Compatibles con GTK+ 2 y GTK+ 3.20 o posterior:**

*   **Adapta** — Un tema Gtk+ adaptativo basado en las guías de diseño de Material Design. Incluye: *Adapta*, *Adapta-Eta*, *Adapta-Nokto*, *Adapta-Nokto-Eta*

	[https://github.com/tista500/Adapta](https://github.com/tista500/Adapta) || [adapta-gtk-theme](https://www.archlinux.org/packages/?name=adapta-gtk-theme)

*   **Arc** — Un tema plano con un aspecto moderno y elementos transparentes. Incluye: *Arc*, *Arc-Dark*, *Arc-Darker*

	[https://github.com/nicohood/arc-theme](https://github.com/nicohood/arc-theme) || con transparencia: [arc-gtk-theme](https://www.archlinux.org/packages/?name=arc-gtk-theme), sin transparencia: [arc-solid-gtk-theme](https://www.archlinux.org/packages/?name=arc-solid-gtk-theme)

*   **Breeze** — Versión GTK+ del tema predeterminado de KDE. Incluye: *Breeze*, *Breeze-Dark*

	[https://cgit.kde.org/breeze-gtk.git](https://cgit.kde.org/breeze-gtk.git) || [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk)

*   **Deepin** — Tema predeterminado del escritorio Deepin. Incluye: *deepin*, *deep-dark*

	[https://github.com/linuxdeepin/deepin-gtk-theme](https://github.com/linuxdeepin/deepin-gtk-theme) || [deepin-gtk-theme](https://www.archlinux.org/packages/?name=deepin-gtk-theme)

*   **Temas extra de GNOME** — Temas extra para el escritorio GNOME. Incluye: *Adwaita*, *Adwaita-dark*, *HighContrast*

	[https://gitlab.gnome.org/GNOME/gnome-themes-extra](https://gitlab.gnome.org/GNOME/gnome-themes-extra) || [gnome-themes-extra](https://www.archlinux.org/packages/?name=gnome-themes-extra)

*   **Temas de MATE** — Temas predeterminados del escritorio MATE. Incluye: *BlackMATE*, *Blue-Submarine*, *BlueMenta*, *ContrastHighInverse*, *Green-Submarine*, *GreenLaguna*, *Menta*, *TraditionalGreen*, *TraditionalOk*

	[https://github.com/mate-desktop/mate-themes](https://github.com/mate-desktop/mate-themes) || [mate-themes](https://www.archlinux.org/packages/?name=mate-themes)

*   **Tema Materia** — Un tema plano parecido a Material Design para GTK3, GTK2 y GNOME-Shell.

	[Https://github.com/nana-4/materia-theme](Https://github.com/nana-4/materia-theme) || [materia-gtk-theme](https://www.archlinux.org/packages/?name=materia-gtk-theme)

*   **Numix** — Un tema plano y ligero con un aspecto moderno (GNOME, Openbox, Unity, Xfce). Incluye: *Numix*

	[https://github.com/shimmerproject/Numix](https://github.com/shimmerproject/Numix) || [numix-gtk-theme](https://www.archlinux.org/packages/?name=numix-gtk-theme)

*   **Blackbird** — Tema oscuro para Xfce.

	[Https://github.com/shimmerproject/Blackbird](Https://github.com/shimmerproject/Blackbird) || [xfce-theme-blackbird](https://aur.archlinux.org/packages/xfce-theme-blackbird/)

*   **Greybird** — Un tema de Xfce gris y azul, utilizado por defecto en Xubuntu 12.04.

	[Https://github.com/shimmerproject/Greybird](Https://github.com/shimmerproject/Greybird) || [xfce-theme-greybird](https://aur.archlinux.org/packages/xfce-theme-greybird/)

*   **Vertex** — Tema para GTK3, GTK2, Gnome-Shell y Cinnamon.

	[Https://github.com/horst3180/vertex-theme](Https://github.com/horst3180/vertex-theme) || [vertex-themes](https://aur.archlinux.org/packages/vertex-themes/)

*   **Zuki** — Temas para GTK, gnome-shell y más.

	[Https://github.com/lassekongo83/zuki-themes](Https://github.com/lassekongo83/zuki-themes) || [zuki-themes-git](https://aur.archlinux.org/packages/zuki-themes-git/)

**Solo compatibles con GTK+ 2:**

*   **Motores GTK+** — Motores de temas para GTK+ 2\. Incluye: *Clearlooks*, *Crux*, *Industrial*, *Mist*, *Redmond*, *ThinIce*

	[https://github.com/GNOME/gtk-engines](https://github.com/GNOME/gtk-engines) || [gtk-engines](https://www.archlinux.org/packages/?name=gtk-engines)

*   **Motor Xfce Gtk+** — Motor y temas de Xfce Gtk+-2.0

	[http://git.xfce.org/xfce/gtk-xfce-engine/](http://git.xfce.org/xfce/gtk-xfce-engine/) || [gtk-xfce-engine](https://www.archlinux.org/packages/?name=gtk-xfce-engine)

*   **Oxygen-Gtk** — Adaptación del tema predeterminado de KDE (Oxygen) a GTK2

	[https://cgit.kde.org/oxygen-gtk.git](https://cgit.kde.org/oxygen-gtk.git) || [oxygen-gtk2](https://www.archlinux.org/packages/?name=oxygen-gtk2)

*   **QtCurve** — Un conjunto configurable de estilos para KDE y Gtk.

	[Https://cgit.kde.org/qtcurve.git](Https://cgit.kde.org/qtcurve.git) || [qtcurve-gtk2](https://www.archlinux.org/packages/?name=qtcurve-gtk2)

Hay una serie de temas GTK+ adicionales en AUR, por ejemplo: [búsqueda de gtk-theme](https://aur.archlinux.org/packages.php?K=gtk-theme), [búsqueda de gtk2-theme](https://aur.archlinux.org/packages.php?K=gtk2-theme).

**Nota:** Debido a que GTK+ 3 cambia rápidamente, los temas GTK+ 3 a menudo requieren una revisión después de una nueva versión GTK+ 3\. Por esta razón, no todos los temas de GTK+ 3 se muestran como se pretendía cuando se utilizó con la última versión de GTK+ 3.

### GTK+ y Qt

Si tiene aplicaciones GTK+ y Qt (KDE) en su escritorio, entonces sabe que sus apariencias no combinan bien. Si desea que los estilos GTK+ coincidan con los estilos Qt, véase [unificación de aspectos para las aplicaciones Qt y GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications_(Espa%C3%B1ol) "Uniform look for Qt and GTK applications (Español)").

## Herramientas de configuración

La mayoría de los [entornos de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)") proporcionan herramientas para configurar el tema GTK+, los iconos, la tipografía y el tamaño de la misma, y administrar estas configuraciones a través de [XSettings](http://standards.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html):

*   Si utiliza [Cinnamon](/index.php/Cinnamon "Cinnamon"), emplee la herramienta Temas (*cinnamon-settings themes*): diríjase a *Configuración del sistema > Temas*.
*   Si utiliza [Enlightenment](/index.php/Enlightenment_(Espa%C3%B1ol) "Enlightenment (Español)"): diríjase a *Configuración > Todos > Aspecto > Tema de aplicación*.
*   Si utiliza [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"), emplee los ajustes de GNOME (*gnome-tweaks*): instale [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).
*   Si utiliza [MATE](/index.php/MATE_(Espa%C3%B1ol) "MATE (Español)"), emplee la herramienta de Preferencias de apariencia (*mate-apariencia-propiedades*): diríjase a *Sistema > Configuración > Apariencia*.
*   Si utiliza [Xfce](/index.php/Xfce_(Espa%C3%B1ol) "Xfce (Español)"), emplee la herramienta Apariencia: diríjase a *Configuración > Apariencia*.

Otras herramientas del GUI generalmente sobrescriben los [archivos de configuración](#Configuración).

**Compatibles con GTK+ 2 y GTK+ 3:**

*   **KDE GTK Configurator** — Aplicación que le permite cambiar el estilo y la tipografía de las aplicaciones GTK+ 2 y Gtk+ 3.

	[Https://cgit.kde.org/kde-gtk-config.git](Https://cgit.kde.org/kde-gtk-config.git) || [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)

	Después de la instalación, `kde-gtk-config` se puede encontrar también en *Configuración del sistema > Estilo de aplicación > GTK*.

*   **LXAppearance** — Herramienta independiente del escritorio de configuración de estilo GTK+ 2 y GTK+ 3 del proyecto LXDE (no requiere otras partes del escritorio LXDE).

	[Http://wiki.lxde.org/en/LXAppearance](Http://wiki.lxde.org/en/LXAppearance) || [lxappearance](https://www.archlinux.org/packages/?name=lxappearance)

*   **Oo-mox** — Aplicación gráfica para generar diferentes variaciones de color de los temas Numix y Flat-Plat (GTK+ 2 y 3), Archdroid y Gnome-Colors. También permite generar temas GTK+ 2 pre-escalados para pantallas HiDPI.

	[https://github.com/actionless/oomox](https://github.com/actionless/oomox) || [oomox](https://aur.archlinux.org/packages/oomox/)

**Compatible solo con GTK+ 2:**

*   **GTK+ Change Theme** — Pequeño programa que le permite cambiar su tema GTK+ 2.0 (considerada una mejor alternativa a *switch2*).

	[Http://plasmasturm.org/code/gtk-chtheme/](Http://plasmasturm.org/code/gtk-chtheme/) || [gtk-chtheme](https://www.archlinux.org/packages/?name=gtk-chtheme)

*   **GTK+ Preference Tool** — Selector de temas GTK+ y cambio de tipografía.

	[Http://gtk-win.sourceforge.net/home/index.php/Main/GTKPreferenceTool](Http://gtk-win.sourceforge.net/home/index.php/Main/GTKPreferenceTool) || [gtk2_prefs](https://aur.archlinux.org/packages/gtk2_prefs/)

*   **GTK+ Theme Switch** — Intercambiador simple de temas GTK+.

	[http://muhri.net/nav.php3?node=gts](http://muhri.net/nav.php3?node=gts) || [gtk-theme-switch2](https://www.archlinux.org/packages/?name=gtk-theme-switch2)

## Configuración

Los ajustes de GTK+ se puede especificar manualmente en los archivos de configuración, pero los entornos de escritorio y las aplicaciones pueden anular esta configuración. Dependiendo de la versión GTK+, estos archivos se encuentran en:

*   GTK+ 2 específico del usuario: `~/.gtkrc-2.0`
*   GTK+ 2 en todo el sistema: `/etc/gtk-2.0/gtkrc`
*   GTK+ 3 específico del usuario: `$XDG_CONFIG_HOME/gtk-3.0/settings.ini`, o `$HOME/.config/gtk-3.0/settings.ini` si `$XDG_CONFIG_HOME` no está establecido
*   GTK+ 3 en todo el sistema: `/etc/gtk-3.0/settings.ini`

**Nota:**

*   Véase [Propiedades *GtkSettings* de GTK+ 3](http://library.gnome.org/devel/gtk3/stable/GtkSettings.html#GtkSettings.properties) (y [Propiedades de GTK+ 2](http://library.gnome.org/devel/gtk2/stable/GtkSettings.html#GtkSettings.properties)) en el manual de referencia de programación de GTK+ para ver la lista completa de las opciones de configuración actualmente admitidas de GTK+.
*   Algunas de las configuraciones que se describen a continuación (como `gtk-icon-size`) están en desuso y se ignoran desde GTK+ 3.10.
*   Si edita sus archivos de configuración GTK+, solo las aplicaciones recién iniciadas mostrarán los cambios.

### Configuración básica del tema

Para cambiar manualmente el tema, los iconos, la tipografía y el tamaño de la fuente GTK+, añada lo siguiente a los archivos de configuración, por ejemplo:

**GTK+ 2:**

 `~/.gtkrc-2.0` 
```
gtk-icon-theme-name = "Adwaita"
gtk-theme-name = "Adwaita"
gtk-font-name = "DejaVu Sans 11"
```

**GTK+ 3:**

 `$XDG_CONFIG_HOME/gtk-3.0/settings.ini` 
```
[Settings]
gtk-icon-theme-name = Adwaita
gtk-theme-name = Adwaita
gtk-font-name = DejaVu Sans 11
```

**Nota:** El nombre del tema del icono es el nombre definido en el archivo de índice del tema, *no* el nombre de su directorio.

### Variante oscura del tema

Algunos temas de GTK+ 3 contienen una variante oscura del tema, pero solo se usa de forma predeterminada cuando la aplicación lo solicita explícitamente. Para usar la variante oscura del tema con todas las aplicaciones GTK+ 3, establezca:

```
gtk-application-prefer-dark-theme = true

```

### Atajos de teclado

Los atajos de teclado (también conocidos como "aceleradores" en GTK+ o métodos abreviados de teclado) se pueden cambiar al colocar el ratón sobre el elemento del menú correspondiente y presionar la combinación de teclas deseada. Para habilitar esta característica, establezca:

```
gtk-can-change-accels = 1

```

#### Combinaciones de teclas Emacs

Para tener combinaciones de teclas similares a Emacs en aplicaciones GTK+, añada lo siguiente:

 `~/.gtkrc-2.0`  `gtk-key-theme-name = "Emacs"`  `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-key-theme-name = Emacs
```

Para GTK+3 ejecute también:

```
$ gsettings set org.gnome.desktop.interface gtk-key-theme "Emacs"

```

XFCE tiene una configuración similar:

```
$ xfconf-query -c xsettings -p /Gtk/KeyThemeName -s Emacs

```

Los archivos de configuración en `/usr/share/themes/Emacs/` determinan cuáles son los enlaces de Emacs, y se pueden cambiar. Copiar secciones en el archivo `~/.gtkrc-2.0` de los usuarios permite realizar cambios para cada usuario.

### Retraso del menú de GNOME

Esta configuración controla el retraso entre apuntar el ratón hacia un menú y la apertura del mismo. Este retraso se mide en milisegundos.

```
gtk-menu-popup-delay = 0

```

### Reducir el tamaño de los widgets

Si tiene una pantalla pequeña o simplemente no le gustan los iconos y widgets grandes, puede cambiarles el tamaño fácilmente.

Para tener iconos sin texto en las barras de herramientas ([valores válidos](https://developer.gnome.org/gtk3/stable/gtk3-Standard-Enumerations.html#GtkToolbarStyle)), utilice:

```
gtk-toolbar-style = GTK_TOOLBAR_ICONS

```

Para tener iconos más pequeños, utilice una línea como esta:

```
gtk-icon-sizes = "panel-menu=16,16:panel=16,16:gtk-menu=16,16:gtk-large-toolbar=16,16\
:gtk-small-toolbar=16,16:gtk-button=16,16"

```

O bien, para eliminar los iconos de los botones por completo:

```
gtk-button-images = 0

```

También puede eliminar los iconos de los menús:

```
gtk-menu-images = 0

```

Véase también [[1]](http://martin.ankerl.com/2008/10/10/how-to-make-a-compact-gnome-theme/) y [[2]](http://gnome-look.org/content/show.php/Simple+eGTK?content=119812).

### Ocultar los botones CSD

Para eliminar los botones minimizar y maximizar de las ventanas *gtk3*:

```
gtk-decoration-layout=menu:close

```

Véase [[3]](https://developer.gnome.org/gtk3/3.22/GtkSettings.html#GtkSettings--gtk-decoration-layout).

### Desactivar pegar desde el ratón

Para desactivar el pegado al pulsar el botón central del ratón (también conocido como PRIMARIO):

```
gtk-enable-primary-paste=false

```

### Posición inicial del selector de archivos

Abra el selector de archivos dentro del **directorio de trabajo actual** y no en la ubicación **reciente**. Normalmente, el **directorio de trabajo actual** es el **directorio personal**.

**GTK+ 3**

Cambie el [ajuste](/index.php/GNOME#Configuration "GNOME") con la orden siguiente:

```
$ gsettings set org.gtk.Settings.FileChooser startup-mode cwd

```

**GTK+ 2**

Añada lo siguiente a `~/.config/gtk-2.0/gtkfilechooser.ini`:

```
StartupMode=cwd

```

### Comportamiento de desplazamiento heredado

**Nota:** Esta configuración no es obedecida por todas las aplicaciones GTK+.

**Sugerencia:** El comportamiento de desplazamiento heredado se puede lograr de manera segura pulsando simplemente con el botón derecho en lugar de pulsar con el botón izquierdo.

Antes de GTK+ 3.6, pulsando a cada lado del control deslizante en la barra de desplazamiento movía la barra de desplazamiento aproximadamente una página en la dirección donde pulsaba. Desde GTK+ 3.6, el control deslizante se mueve directamente a la posición donde se pulsa. Este comportamiento se puede revertir en algunas aplicaciones creando el archivo con el contenido siguiente:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-primary-button-warps-slider = false

```

### Deshabilitar las barras de desplazamiento superpuestas

Desde GTK+ 3.15, las barras de desplazamiento superpuestas están habilitadas de forma predeterminada, lo que significa que las barras de desplazamiento se mostrarán solo al pasar el ratón en las aplicaciones de GTK+ 3\. Este comportamiento se puede revertir configurando la siguiente variable de entorno: `GTK_OVERLAY_SCROLLING=0`. Véase [Aplicaciones gráficas](/index.php/Environment_variables_(Espa%C3%B1ol)#Aplicaciones_gráficas "Environment variables (Español)").

GTK+ 4 ya no admitirá `GTK_OVERLAY_SCROLLING`. Ya ha sido [eliminado](https://github.com/GNOME/gtk/commit/e49615184a9d85bb0bb4e289b3ee8252adee3813#diff-3cf94c6e1eb009e20985034bc2210bfd) de la rama principal de desarrollo. A partir de GTK+ 4, la naturaleza de superposición de las barras de desplazamiento es parte del kit de herramientas. Se ha eliminado el conmutador general para evitar que los desarrolladores rompan aplicaciones que no han sido probadas con ambas combinaciones. Para permitir que los desarrolladores de aplicaciones decidan qué aspecto deberían tener sus aplicaciones, en su lugar, el kit de herramientas proporciona un mecanismo para excluir o añadir una configuración para los usuarios. La función [gtk_scrolled_window_set_overlay_scrolling()](https://developer.gnome.org/gtk3/stable/GtkScrolledWindow.html#gtk-scrolled-window-setlay-scrolling) se puede usar para habilitar/deshabilitar las barras de desplazamiento superpuestas *por cada usuario*. Los desarrolladores de aplicaciones pueden utilizar opcionalmente [GSettings](https://blog.gtk.org/2017/05/01/first-steps-with-gsettings/) para que el usuario tenga una configuración vinculada a esta propiedad.

#### Eliminar indicadores de la barra de desplazamiento de superposición

Las posiciones de las barras de desplazamiento de superposición se indican mediante líneas finas discontinuas en la ventana de la aplicación. Estas líneas discontinuas estarán presentes incluso cuando la barra de desplazamiento de superposición se deshabilite utilizando la variable de entorno que se analiza en la sección anterior. Para eliminar las líneas indicadoras, cree el siguiente archivo:

 `~/.config/gtk-3.0/gtk.css` 
```
/* Remove dotted lines from GTK+ 3 applications */
undershoot.top, undershoot.right, undershoot.bottom, undershoot.left { background-image: none; }

```

## Backends de GDK

GDK (la capa de abstracción subyacente de GTK+) admite varios backends para mostrar aplicaciones de GTK+. El backend predeterminado es *x11*.

### Backend de Broadway

El backend de GDK Broadway proporciona soporte para mostrar aplicaciones GTK+ en un navegador web, utilizando HTML5 y sockets web. [[4]](https://developer.gnome.org/gtk3/3.8/gtk-broadway.html)

Cuando use broadwayd, especifique el número de pantalla a emplear, con el prefijo de dos puntos, similar a X. El número de pantalla predeterminado es 1.

```
$ display_number=:5

```

Inícielo:

```
$ broadwayd $display_number

```

El puerto utilizado por defecto es:

```
port = 8080 + $display_number

```

Apunte su navegador a [http://127.0.0.1:port](http://127.0.0.1:port).

Para iniciar aplicaciones:

```
$ GDK_BACKEND=broadway BROADWAY_DISPLAY=$display_number *<<aplicación>>*

```

Alternativamente, puede configurar la dirección y el puerto

```
$ broadwayd --port $port_number --address $address $display_number

```

### Backend de Wayland

El backend de GDK [Wayland](/index.php/Wayland_(Espa%C3%B1ol) "Wayland (Español)") se puede habilitar configurando la variable de entorno `GDK_BACKEND=wayland`.

**Sugerencia:** Para deshabilitar las decoraciones de la ventana GTK en Wayland, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [gtk3-optional-csd](https://aur.archlinux.org/packages/gtk3-optional-csd/) y establezca la variable de entorno `GTK_CSD=0`.

## Solución de problemas

### Diferentes temas entre aplicaciones GTK+ 2 y GTK+ 3

En general, si un tema seleccionado es compatible con GTK+ 2 y GTK+ 3, este se aplicará a todas las aplicaciones GTK+ 2 y GTK+ 3\. Si un tema seleccionado solo es compatible con GTK+ 2, se utilizará para las aplicaciones de GTK+ 2 y el tema predeterminado de GTK+ se utilizará para las aplicaciones de GTK+ 3\. Si el tema seleccionado solo es compatible con GTK+ 3, se utilizará para las aplicaciones de GTK+ 3 y el tema predeterminado de GTK+ se utilizará para las aplicaciones de GTK+ 2\. Por lo tanto, para la consistencia del tema de la aplicación, es mejor utilizar un tema que sea compatible con GTK+ 2 y GTK+ 3.

Puede encontrar qué temas instalados en su sistema tienen las versiones GTK+ 2 y GTK+ 3 mediante esta orden (no funciona con nombres que contengan espacios):

```
find $(find ~/.themes /usr/share/themes/ -wholename "*/gtk-3.0" | sed -e "s/^\(.*\)\/gtk-3.0$/\1/") -wholename "*/gtk-2.0" | sed -e "s/.*\/\(.*\)\/gtk-2.0/\1"/

```

### Tema no aplicado en aplicaciones del superusuario

Como los archivos de temas del usuario (`$XDG_CONFIG_HOME/gtk-3.0/settings.ini`, `~/.gtkrc-2.0`) no son leídos por otras cuentas, el tema seleccionado no se aplicará a [las aplicaciones X ejecutadas como superusuario](/index.php/Running_X_apps_as_root "Running X apps as root"). Las posibles soluciones incluyen:

*   Crear enlaces simbólicos, por ejemplo:

```
# ln -s /home/[username]/.gtkrc-2.0 /etc/gtk-2.0/gtkrc
# ln -s /home/[username]/.config/gtk-3.0/settings.ini /etc/gtk-3.0/settings.ini

```

*   Configurar los archivos de temas en todo el sistema: `/etc/gtk-3.0/settings.ini` (GTK+ 3) o `/etc/gtk-2.0/gtkrc` (GTK+ 2)
*   Ajustar el tema como superusuario:

```
# sudo lxappearance

```

*   Utilizar un demonio de configuración (esto es lo que hacen la mayoría de los entornos de escritorio). Una variante agnóstica de escritorio que utiliza [XSettings](http://standards.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html) está disponible en [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)") bajo [xsettingsd-git](https://aur.archlinux.org/packages/xsettingsd-git/).

### Decoraciones del lado del cliente

GTK 3.12 introdujo las [decoraciones del lado del cliente](http://blogs.gnome.org/mclasen/2013/12/05/client-side-decorations-in-themes/), que separa la barra de título del administrador de ventanas. Esto puede presentar problemas como las [dobles barras de títulos](http://redmine.audacious-media-player.org/boards/1/topics/1135), la no existencia de estas o las [sombras dobles](https://github.com/chjj/compton/issues/189) con la composición habilitada.

Para eliminar la sombra y la brecha alrededor de las ventanas (por ejemplo, en combinación con un administrador de ventanas de mosaico), cree el siguiente archivo:

 `~/.config/gtk-3.0/gtk.css` 
```
.window-frame, .window-frame:backdrop {
 box-shadow: 0 0 0 black;
 border-style: none;
 margin: 0;
 border-radius: 0;
}

.titlebar {
 border-radius: 0;
}

.window-frame.csd.popup {
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2), 0 0 0 1px rgba(0, 0, 0, 0.13);
}

.header-bar {
  background-image: none;
  background-color: #ededed;
  box-shadow: none;
}
/* You may want to use this if you don't like the double title.
GtkLabel.title {
    opacity: 0;
}*/

```

Para ajustar los botones en la barra superior, utilice la configuración `gtk-decoration-layout`. [[5]](https://developer.gnome.org/gtk3/stable/GtkSettings.html#GtkSettings--gtk-decoration-layout) El siguiente ejemplo eliminan todos los botones:

 `~/.config/gtk-3.0/settings.ini`  `gtk-decoration-layout=menu:` 

### Cedilla ç/Ç en lugar de ć/Ć

Véase [[6]](https://bugs.launchpad.net/ubuntu/+source/ibus/+bug/518056), y [[7]](https://bugs.launchpad.net/ubuntu/+source/ibus/+bug/518056/comments/37) para una solución utilizando Xcompose (disposición internacional de EE.UU.).

### Suprimir advertencia referente al bus de accesibilidad

Si no utiliza ninguna de las funciones de [accesibilidad de Gnome](https://wiki.gnome.org/Accessibility), puede recibir advertencias en inglés como:

```
WARNING **: Couldn't connect to accessibility bus:

```

O en español:

```
ADVERTENCIA **: No se pudo conectar al bus de accesibilidad:

```

Para suprimir estas advertencias, ejecute los programas con `NO_AT_BRIDGE=1` o configúrelo como una [variable de entorno](/index.php/Environment_variable_(Espa%C3%B1ol) "Environment variable (Español)") global.

### Falta de coincidencia del color de fondo de la barra de título

Si está utilizando un [administrador de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") que utiliza un tema de decoración de ventanas que imita el color de fondo del tema GTK+, es posible que el color de la barra de título ya no coincida completamente con el color de la aplicación en algunas aplicaciones GTK+ 3\. Como solución, cree el siguiente archivo:

 `~/.config/gtk-3.0/gtk.css` 
```
/* Always use background color */
GtkWindow {
    background-color: @theme_bg_color;
}

/* Fix tooltip background override */
.tooltip {
    background-color: rgba(0, 0, 0, 0.8);
}

.tooltip * {
    background-color: transparent;
}

/* Fix Nautilus desktop window background override */
NautilusWindow {
     background-color: transparent; 
}

```

### Eventos de enfoque incorrecto con administradores de ventanas de mosaico

**Nota:** Esto deshabilita el soporte de la pantalla táctil para aplicaciones GTK+ 3\. [[8]](https://bugzilla.gnome.org/show_bug.cgi?id=677329#c14)

[Defina](/index.php/Define "Define") `GDK_CORE_DEVICE_EVENTS=1` para utilizar la entrada de estilo GTK+ 2, en lugar de xinput2\. [[9]](https://bugzilla.gnome.org/show_bug.cgi?id=677329#c10)

### Soporte de miniaturas para el diálogo del archivo GTK+ 2

Instale [gtk2-patched-filechooser-icon-view](https://aur.archlinux.org/packages/gtk2-patched-filechooser-icon-view/) para tener la opción de ver los archivos como miniaturas en lugar de la lista en el selector de archivos de GTK+.

### Iconos de botón/menú en algunas aplicaciones en la sesión Wayland de GNOME

Su archivo `~/.config/gtk-3.0/settings.ini` está mal configurado. Esto puede ocurrir si prueba otros entornos de escritorio basados ​​en GTK+. Estos son los valores afectados:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-button-images=1
gtk-menu-images=1
```

Simplemente cámbielos a 0 o elimine todo el archivo para usar los valores predeterminados de GNOME.

### GTK+ 3 sin polkit

GTK+ 3 depende del polkit a través de colord, que es requerido para imprimir. Sin embargo, la impresión funciona bien sin polkit instalado; al menos con una impresora monocromática y versiones de paquete gtk3-print-backends=3.22.19-2 y colord=1.4.1-1.

### Algunos temas de GTK+ 2 solo cambian la paleta de colores de la interfaz de usuario

Según el tema elegido compatible con GTK+ 2, los controles de la interfaz de usuario pueden tener la apariencia predeterminada de Raleigh, posiblemente con una paleta de colores diferente. Esto se debe a que estos temas requieren el motor Murrine de GTK+ 2, que no está disponible (los programas GTK+ 2 deben avisar de ello en su salida de error estándar). Instale el paquete [gtk-engine-murrine](https://www.archlinux.org/packages/?name=gtk-engine-murrine).

## Ejemplos

Ejemplo de configuración de GTK+ 2:

 `~/.gtkrc-2.0` 
```
# GTK theme
include "/usr/share/themes/Clearlooks/gtk-2.0/gtkrc"

# Font
style "myfont" {
    font_name = "DejaVu Sans 8"
}
widget_class "*" style "myfont"
gtk-font-name = "DejaVu Sans 8"

# Icon theme
gtk-icon-theme-name = "Tango"

# Toolbar style
gtk-toolbar-style = GTK_TOOLBAR_ICONS
```

Ejemplo de GTK+ 3 de una configuración convertida de GTK+ 2.x a GTK+ 3.x por [lxappearance](https://www.archlinux.org/packages/?name=lxappearance):

 `$XDG_CONFIG_HOME/gtk-3.0/settings.ini` 
```
[Settings] 
gtk-theme-name=TraditionalOk
gtk-icon-theme-name=Fog
gtk-font-name=Luxi Sans 12
gtk-cursor-theme-name=mate
gtk-cursor-theme-size=24
gtk-toolbar-style=GTK_TOOLBAR_BOTH_HORIZ
gtk-toolbar-icon-size=GTK_ICON_SIZE_LARGE_TOOLBAR
gtk-button-images=1
gtk-menu-images=1
gtk-enable-event-sounds=0
gtk-enable-input-feedback-sounds=0
gtk-xft-antialias=1
gtk-xft-hinting=1
gtk-xft-hintstyle=hintslight
gtk-xft-rgba=rgb
```

## Véase también

*   [Web oficial de GTK+](http://www.gtk.org/)
*   [Artículo en Wikipedia sobre GTK+](https://en.wikipedia.org/wiki/es:GTK%2B "wikipedia:es:GTK+")
*   [Tutorial de GTK+ 2.0](http://developer.gnome.org/gtk-tutorial/stable/)
*   [Manual de referencia de GTK+ 3](http://developer.gnome.org/gtk3/stable/)
*   [Tutorial de gtkmm](http://developer.gnome.org/gtkmm-tutorial/stable/)
*   [Manual de referencia de gtkmm](http://developer.gnome.org/gtkmm/stable/)