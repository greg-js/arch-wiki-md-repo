**Estado de la traducción**
Este artículo es una traducción de [GTK+](/index.php/GTK%2B "GTK+"), revisada por última vez el **en fase de traducción**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GTK%2B&diff=0&oldid=545475) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

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