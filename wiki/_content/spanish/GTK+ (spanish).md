**Estado de la traducción:** este artículo es una versión traducida de [GTK+](/index.php/GTK%2B "GTK+"). Fecha de la última traducción/revisión: **en fase de traducción**. Puede ayudar a actualizar la traducción, si advierte que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=GTK%2B&diff=0&oldid=535659).

Artículos relacionados

*   [Uniformidad en aplicaciones Qt y GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications_(Espa%C3%B1ol) "Uniform look for Qt and GTK applications (Español)")
*   [Qt](/index.php/Qt "Qt")
*   [GNU](/index.php/GNU_(Espa%C3%B1ol) "GNU (Español)")
*   [GTK+/Development](/index.php/GTK%2B/Development "GTK+/Development")

De la [web de GTK+](http://www.gtk.org):

	GTK+, o GIMP Toolkit, es un conjunto de herramientas multiplataforma para crear interfaces gráficas de usuario. Al ofrecer un conjunto completo de widgets, GTK+ es adecuado para proyectos que van desde pequeñas herramientas con funcionalidad reducida hasta completas suites de aplicaciones.

GTK+ (GIMP Toolkit) fue originalmente creado por el [Proyecto GNU](/index.php/GNU_(Espa%C3%B1ol) "GNU (Español)") para [GIMP](/index.php/GIMP "GIMP"), pero ahora es un conjunto de herramientas popular con conectores a múltiples lenguajes de programación. Este artículo explora las herramientas utilizadas para configurar el tema GTK+, el estilo, los iconos, las fuentes y sus tamaños, y también detalla la configuración manual.

## Instalación

Dos versiones de GTK+ estan disponibles en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Se pueden [instalar](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") con los siguientes paquetes:

*   **GTK+ 3.x** disponible con el paquete [gtk3](https://www.archlinux.org/packages/?name=gtk3).
*   **GTK+ 2.x** disponible con el paquete [gtk2](https://www.archlinux.org/packages/?name=gtk2).
*   **GTK+ 1.x** disponible con el paquete [gtk](https://aur.archlinux.org/packages/gtk/).

## Temas

En GTK+ 2, el tema predeterminado es *Raleigh*, pero Arch Linux tiene un archivo de configuración personalizado en `/usr/share/gtk-2.0/gtkrc`, que establece *Adwaita* como el tema predeterminado. En GTK+ 3, el tema predeterminado es *Adwaita*, pero también se incluyen *HighContrast*, *HighContrastInverse* y *Raleigh*.

Para forzar un tema específico, puede establecer variables de entorno.

*   Para GTK+ 2, utilice la variable de entorno `GTK2_RC_FILES`, por ejemplo:

```
$ GTK2_RC_FILES=/usr/share/themes/Industrial/gtk-2.0/gtkrc gimp

```

	lanzará GIMP con el tema Industrial.

*   Para GTK+ 3, utilice la variable de entorno `GTK_THEME`, por ejemplo:

```
$ GTK_THEME=Adwaita:dark gnome-calculator

```

	lanzará la calculadora de GNOME con la variante oscura del tema Adwaita.

Se pueden instalar más temas desde los repositorios oficiales o desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

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

Hay una serie de temas GTK+ adicionales en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"): [búsqueda de gtk-theme](https://aur.archlinux.org/packages.php?K=gtk-theme), [búsqueda de gtk2-theme](https://aur.archlinux.org/packages.php?K=gtk2-theme).

**Nota:** Debido a que GTK+ 3 cambia rápidamente, los temas GTK+ 3 a menudo requieren una revisión después de una nueva versión GTK+ 3\. Por esta razón, no todos los temas de GTK+ 3 se muestran como se pretendía cuando se utilizó con la última versión de GTK+ 3.

### GTK+ y Qt

Si tiene aplicaciones GTK+ y Qt (KDE) en su escritorio, entonces sabe que sus apariencias no combinan bien. Si desea que los estilos GTK+ coincidan con los estilos Qt, véase [unificación de aspectos para las palicaciones Qt y GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications_(Espa%C3%B1ol) "Uniform look for Qt and GTK applications (Español)").