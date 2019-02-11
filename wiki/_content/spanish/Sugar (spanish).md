**Estado de la traducción**
Este artículo es una traducción de [Sugar](/index.php/Sugar "Sugar"), revisada por última vez el **2019-02-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Sugar&diff=0&oldid=556430) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Producto de la iniciativa de [OLPC](https://en.wikipedia.org/wiki/es:OLPC es un entorno de escritorio similar a [KDE](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)") y [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"), pero orientado hacia los niños y la educación.

Sugar tiene una [taxonomía](http://wiki.sugarlabs.org/go/Taxonomy) especial para nombrar las partes de su sistema. La interfaz gráfica en sí misma constituye el grupo **Glucose**. Este es el sistema central y cabe esperar que esté presente cuando se instale Sugar. Pero para usar realmente el entorno, necesita actividades (alguna clase de aplicaciones). Las actividades base son parte de **Fructose**. Luego, **Sucrose** está constituido por glucose y fructose y representa lo que debería distribuirse como un entorno de escritorio básico Sugar. Las actividades extra son parte de **Honey**. Tenga en cuenta que Ribose (el sistema operativo subyacente) se reemplaza aquí por Arch.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
    *   [1.1 Desde la biblioteca de actividades](#Desde_la_biblioteca_de_actividades)
*   [2 Iniciar Sugar](#Iniciar_Sugar)
*   [3 Véase también](#Véase_también)

## Instalación

*   Para el sistema central (*Glucose*), instale [sugar](https://www.archlinux.org/packages/?name=sugar). Proporciona la interfaz gráfica y una sesión de escritorio, pero no es muy útil por sí sola.
*   El grupo [sugar-fructose](https://www.archlinux.org/groups/x86_64/sugar-fructose/) contiene las actividades básicas (*Fructose*) que incluyen un navegador web, un editor de texto, un reproductor multimedia y un emulador de terminal.
*   El paquete [sugar-runner](https://www.archlinux.org/packages/?name=sugar-runner) proporciona un script de ayuda que hace posible lanzar Sugar dentro de otro entorno de escritorio, o directamente desde la línea de comandos.

### Desde la biblioteca de actividades

La [Biblioteca de Actividades Sugar](http://wiki.sugarlabs.org/go/Activity_Library) proporciona muchos [paquetes de actividades](http://wiki.sugarlabs.org/go/Development_Team/Almanac/Activity_Bundles) empaquetados como archivos zip con la extensión ".xo". Estos paquetes se pueden descargar e instalar en el directorio del usuario desde Sugar, pero la instalación no garantiza que se cumplan las dependencias. Por lo tanto, no es la forma recomendada de instalar actividades, ya que es probable que no se inicien debido a las dependencias faltantes. Dependencias comúnmente utilizadas:

*   Para las actividades web, instale [webkit2gtk](https://www.archlinux.org/packages/?name=webkit2gtk) desde los repositorios oficiales.
*   Para actividades basadas en GTK+ 2, instale [sugar-toolkit-gtk2](https://aur.archlinux.org/packages/sugar-toolkit-gtk2/) desde AUR.

Para comprobar por qué la actividad no se inicia, consulte el archivo de registro ubicado en `~/.sugar/default/logs/[app_id]-1.log`.

## Iniciar Sugar

Sugar puede iniciarse gráficamente usando un [gestor de pantalla](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)"), o manualmente desde la consola.

**Gráficamente**

Seleccione la sesión *Sugar* en el menú de sesión del gestor de pantalla.

**Manualmente**

Si [sugar-runner](https://www.archlinux.org/packages/?name=sugar-runner) está instalado, Sugar se puede iniciar con el comando `sugar-runner`.

Un método alternativo es agregar `exec sugar` al archivo `~/.xinitrc`. Después de eso, Sugar se puede iniciar con el comando `startx` (véase [xinitrc](/index.php/Xinit_(Espa%C3%B1ol)#xinitrc "Xinit (Español)") para detalles adicionales). Después de configurar el archivo `~/.xinitrc`, también se puede configurar para que se [inicie automáticamente X al inicio de sesión](/index.php/Xinit_(Espa%C3%B1ol)#Inicio_automático_de_X_al_inicio_de_sesión "Xinit (Español)").

## Véase también

*   [Página web oficial de Sugar](http://sugarlabs.org/)
*   [Actividades para Sugar](http://activities.sugarlabs.org/)