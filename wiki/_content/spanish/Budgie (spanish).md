**Estado de la traducción**
Este artículo es una traducción de [Budgie](/index.php/Budgie "Budgie"), revisada por última vez el **2018-11-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Budgie&diff=0&oldid=534157) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Entornos de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)")
*   [Gestor de pantallas](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)")
*   [Gestor de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)")
*   [GTK+](/index.php/GTK%2B_(Espa%C3%B1ol) "GTK+ (Español)")

[Budgie](https://budgie-desktop.org/home/) es el escritorio predeterminado de Solus Operating System, escrito desde cero. Además de un diseño más moderno, Budgie puede emular la apariencia y la sensación del escritorio GNOME 2.

En este momento, Budgie está fuertemente en desarrollo, por lo que es de esperar que haya pequeños errores y que se vayan agregando nuevas características a medida que pase el tiempo.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Puesta en marcha](#Puesta_en_marcha)
*   [3 Utilización](#Utilización)
*   [4 Configuración](#Configuración)
    *   [4.1 Cambiar la distribución de los botones](#Cambiar_la_distribución_de_los_botones)
    *   [4.2 Usar un gestor de ventanas distinto](#Usar_un_gestor_de_ventanas_distinto)
*   [5 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop) para la última versión estable o [budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/) para el git master actual. También se recomienda instalar las dependencias opcionales para obtener un entorno de escritorio aún más completo. Así mismo, también se recomienda instalar el grupo de paquetes [gnome](https://www.archlinux.org/groups/x86_64/gnome/), que contiene las aplicaciones necesarias para una experiencia estándar de GNOME.

## Puesta en marcha

Elija la sesión *Budgie Desktop* en el [gestor de pantallas](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)") de su elección, o modifique [xinitrc](/index.php/Xinit_(Espa%C3%B1ol)#xinitrc "Xinit (Español)") para incluir Budgie Desktop:

 `~/.xinitrc` 
```
export XDG_CURRENT_DESKTOP=Budgie:GNOME
exec budgie-desktop

```

## Utilización

Puede ver los mensajes de notificación, configurar el volumen y modificar la apariencia y sensación del escritorio con la barra lateral llamada "Raven". Se puede acceder a ella con la combinación `Super+N` o haciendo clic en el applet de indicador de estado.

## Configuración

La configuración de Budgie Desktop se realiza a través de la barra lateral, y los cambios en la configuración del sistema se realizan a través de [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center)

### Cambiar la distribución de los botones

La distribución de los botones de las ventanas se pueden cambiar utilizando [dconf](https://www.archlinux.org/packages/?name=dconf), [dconf-editor](https://www.archlinux.org/packages/?name=dconf-editor) o gsettings.

Por ejemplo:

```
gsettings set com.solus-project.budgie-wm button-layout 'close,minimize,maximize:appmenu'
gsettings set com.solus-project.budgie-helper.workarounds fix-button-layout 'close,minimize,maximize:menu'

```

### Usar un gestor de ventanas distinto

Es posible utilizar un [gestor de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") alternativo con Budgie. O bien defina una [sesión personalizada de GNOME](/index.php/GNOME/Tips_and_tricks#Custom_GNOME_sessions "GNOME/Tips and tricks") que reemplaze a *budgie-wm* con otro gestor de ventanas o bien [autoinicie](/index.php/GNOME_(Espa%C3%B1ol)#Inicio_automático "GNOME (Español)") `*my-wm* --replace` donde *my-wm* es el nombre ejecutable del gestor de ventanas que desea usar.

## Véase también

*   [Wikipedia:Budgie (entorno de escritorio)](https://en.wikipedia.org/wiki/Budgie_(desktop_environment) "wikipedia:Budgie (desktop environment)")
*   [Página web oficial de Budgie Desktop](https://budgie-desktop.org/)
*   [repositorios oficiales de git para el desarrollo de Solus](https://git.solus-project.com/)
*   [Estado de compilación para el proyectos Solus](https://build.solus-project.com/)