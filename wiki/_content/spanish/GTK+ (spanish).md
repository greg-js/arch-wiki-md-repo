**Estado de la traducción**
Este artículo es una traducción de [GTK+](/index.php/GTK%2B "GTK+"), revisada por última vez el **2018-10-10**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GTK%2B&diff=0&oldid=545475) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Uniformidad en aplicaciones Qt y GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications_(Espa%C3%B1ol) "Uniform look for Qt and GTK applications (Español)")
*   [Qt](/index.php/Qt "Qt")
*   [GNU](/index.php/GNU_(Espa%C3%B1ol) "GNU (Español)")
*   [GTK+/Development](/index.php/GTK%2B/Development "GTK+/Development")

De la [web de GTK+](http://www.gtk.org):

	GTK+, o GIMP Toolkit, es un conjunto de herramientas multiplataforma para crear interfaces gráficas de usuario. Al ofrecer un conjunto completo de widgets, GTK+ es adecuado para proyectos que van desde pequeñas herramientas con funcionalidad reducida hasta completas suites de aplicaciones.

GTK+ (GIMP Toolkit) fue originalmente creado por el [Proyecto GNU](/index.php/GNU_(Espa%C3%B1ol) "GNU (Español)") para [GIMP](/index.php/GIMP "GIMP"), pero ahora es un conjunto de herramientas popular con conectores a múltiples lenguajes de programación. Este artículo explora las herramientas utilizadas para configurar el tema GTK+, el estilo, los iconos, las fuentes y sus tamaños, y también detalla la configuración manual.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Temas](#Temas)
    *   [2.1 GTK+ y Qt](#GTK.2B_y_Qt)
*   [3 Herramientas de configuración](#Herramientas_de_configuraci.C3.B3n)
*   [4 Configuración](#Configuraci.C3.B3n)
    *   [4.1 Configuración básica del tema](#Configuraci.C3.B3n_b.C3.A1sica_del_tema)
    *   [4.2 Variante oscura del tema](#Variante_oscura_del_tema)
    *   [4.3 Atajos de teclado](#Atajos_de_teclado)
        *   [4.3.1 Combinaciones de teclas Emacs](#Combinaciones_de_teclas_Emacs)
    *   [4.4 Retraso del menú de GNOME](#Retraso_del_men.C3.BA_de_GNOME)
    *   [4.5 Reducir el tamaño de los widgets](#Reducir_el_tama.C3.B1o_de_los_widgets)
    *   [4.6 Ocultar los botones CSD](#Ocultar_los_botones_CSD)
    *   [4.7 Desactivar pegar desde el ratón](#Desactivar_pegar_desde_el_rat.C3.B3n)
    *   [4.8 Posición inicial del selector de archivos](#Posici.C3.B3n_inicial_del_selector_de_archivos)
    *   [4.9 Comportamiento de desplazamiento heredado](#Comportamiento_de_desplazamiento_heredado)
    *   [4.10 Deshabilitar las barras de desplazamiento superpuestas](#Deshabilitar_las_barras_de_desplazamiento_superpuestas)
        *   [4.10.1 Eliminar indicadores de la barra de desplazamiento de superposición](#Eliminar_indicadores_de_la_barra_de_desplazamiento_de_superposici.C3.B3n)
*   [5 GDK backends](#GDK_backends)

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

**Sugerencia:** `gtkrc` puede ser también un archivo personalizado en su directorio de inicio creado por cualquiera de las [#Herramientas de configuración](#Herramientas_de_configuraci.C3.B3n).

*   Para GTK+ 3, utilice `GTK_THEME`. Por ejemplo para lanzar la calculadora de GNOME con la variante oscura de *Adwaita*:

```
$ GTK_THEME=Adwaita:dark gnome-calculator

```

Se pueden instalar más temas desde los repositorios oficiales o desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"). Los temas extraídos manualmente van en el directorio `~/.themes/` o `~/.local/share/themes/`.

**Compatibles con GTK+ 2 y GTK+ 3.20 o posterior:**

*   **Adapta** — Un tema Gtk+ adaptativo basado en las guías de diseño de Material Design. Incluye: *Adapta*, *Adapta-Eta*, *Adapta-Nokto*, *Adapta-Nokto-Eta*

	[https://github.com/tista500/Adapta](https://github.com/tista500/Adapta) || [adapta-gtk-theme](https://www.archlinux.org/packages/?name=adapta-gtk-theme)

*   **Arc** — Un tema plano con un aspecto moderno y elementos transparentes. Incluye: *Arc*, *Arc-Dark*, *Arc-Darker*

	[https://github.com/horst3180/arc-theme](https://github.com/horst3180/arc-theme) || con transparencia: [arc-gtk-theme](https://www.archlinux.org/packages/?name=arc-gtk-theme), sin transparencia: [arc-solid-gtk-theme](https://www.archlinux.org/packages/?name=arc-solid-gtk-theme)

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

Otras herramientas del GUI generalmente sobrescriben los [archivos de configuración](#Configuraci.C3.B3n).

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

Para obtener combinaciones de teclas similares a Emacs en aplicaciones gtk:

Para GTK2, añada `gtk-key-theme-name="Emacs"` en `~/.gtkrc-2.0`.

Para GTK3 añada lo siguiente al archivo anotado:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-key-theme-name = Emacs
```

Entonces ejecute:

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

Para eliminar los botones minimizar y maximizar. [[3]](https://developer.gnome.org/gtk3/3.22/GtkSettings.html#GtkSettings--gtk-decoration-layout)

```
gtk-decoration-layout=menu:close

```

### Desactivar pegar desde el ratón

Para desactivar el pegado al pulsar el botón central del ratón (también conocido como PRIMARIO):

```
gtk-enable-primary-paste=false

```

### Posición inicial del selector de archivos

Abra el selector de archivos dentro del **directorio de trabajo actual** y no en la ubicación **reciente**. Normalmente, el **directorio de trabajo actual** es el **directorio personal**.

**GTK+ 3**

Modifique DConf con *gsettings*, ya que el archivo de base de datos ($XDG_CONFIG_HOME/dconf/users) es binario:

```
$ gsettings set org.gtk.Settings.FileChooser startup-mode cwd

```

**GTK+ 2**

Modifique el archivo de configuración `~/.config/gtk-2.0/gtkfilechooser.ini`:

 `~/.config/gtk-2.0/gtkfilechooser.ini`  `StartupMode=cwd` 

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

Desde GTK+ 3.15, las barras de desplazamiento superpuestas están habilitadas de forma predeterminada, lo que significa que las barras de desplazamiento se mostrarán solo al pasar el ratón en las aplicaciones de GTK+ 3\. Este comportamiento se puede revertir configurando la siguiente variable de entorno: `GTK_OVERLAY_SCROLLING=0`. Véase [Variables de entorno # aplicaciones gráficas](/index.php/Environment_variables_(Espa%C3%B1ol)#Graphical_applications "Environment variables (Español)").

GTK+ 4 ya no admitirá `GTK_OVERLAY_SCROLLING`. Ya ha sido [eliminado](https://github.com/GNOME/gtk/commit/e49615184a9d85bb0bb4e289b3ee8252adee3813#diff-3cf94c6e1eb009e20985034bc2210bfd) de la rama principal de desarrollo. A partir de GTK+ 4, la naturaleza de superposición de las barras de desplazamiento es parte del kit de herramientas. Se ha eliminado el conmutador general para evitar que los desarrolladores rompan aplicaciones que no han sido probadas con ambas combinaciones. Para permitir que los desarrolladores de aplicaciones decidan qué aspecto deberían tener sus aplicaciones, en su lugar, el kit de herramientas proporciona un mecanismo para excluir o añadir una configuración para los usuarios. La función [gtk_scrolled_window_set_overlay_scrolling()](https://developer.gnome.org/gtk3/stable/GtkScrolledWindow.html#gtk-scrolled-window-setlay-scrolling) se puede usar para habilitar/deshabilitar las barras de desplazamiento superpuestas *por cada usuario*. Los desarrolladores de aplicaciones pueden utilizar opcionalmente [GSettings](https://blog.gtk.org/2017/05/01/first-steps-with-gsettings/) para que el usuario tenga una configuración vinculada a esta propiedad.

#### Eliminar indicadores de la barra de desplazamiento de superposición

Las posiciones de las barras de desplazamiento de superposición se indican mediante líneas finas discontinuas en la ventana de la aplicación. Estas líneas discontinuas estarán presentes incluso cuando la barra de desplazamiento de superposición se deshabilite utilizando la variable de entorno que se analiza en la sección anterior. Para eliminar las líneas indicadoras, cree el siguiente archivo:

 `~/.config/gtk-3.0/gtk.css` 
```
/* Remove dotted lines from GTK+ 3 applications */
undershoot.top, undershoot.right, undershoot.bottom, undershoot.left { background-image: none; }

```

## GDK backends