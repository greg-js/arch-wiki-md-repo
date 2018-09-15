**Estado de la traducción:** este artículo es una versión traducida de [GTK+](/index.php/GTK%2B "GTK+"). Fecha de la última traducción/revisión: **en fase de traducción**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=GTK%2B&diff=0&oldid=535659).

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

**GTK+ 2 y GTK+ 3.20 o posterior son compatibles:**

### GTK+ y Qt