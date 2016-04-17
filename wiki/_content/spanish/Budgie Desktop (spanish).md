Budgie es el escritorio por defecto del sistema operativo Solus, escrito desde cero. Además de un diseño más moderno, Budgie puede simular la apariencia del escritorio GNOME 2.

En este momento Budgie está fuertemente en fase de desarrollo, por lo que se puede esperar pequeños errores y nuevas características con el paso del tiempo.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Comenzando](#Comenzando)
*   [3 Uso](#Uso)
*   [4 Ver también](#Ver_tambi.C3.A9n)

## Instalación

[Instalar](/index.php/Install "Install") la última version estable de [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop) o [budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/) desde los repositorios git. Se recomienda instalar sus dependencias opcionales también para obtener un entorno de escritorio más completo, cómo así también instalar el grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/), que contiene las aplicaciones necesarias para la experiencia GNOME estándar.

## Comenzando

Elegimos la sesión *Budgie Desktop* de nuestro [display manager (Español)](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)") o editamos nuestro [xinitrc (Español)](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") para incluir Budgie Desktop:

 `~/.xinitrc` 
```
export XDG_CURRENT_DESKTOP=Budgie:GNOME
exec budgie-desktop

```

## Uso

Puedes ver las notificaciones, ajustes de volumen y modificar la apariencia del escritorio con la barra lateral llamada "Raven". Podemos acceder a ella con las teclas `Super+N` o haciendo clic en el indicador de estado.

## Ver también

*   [Web Oficial del Proyecto Solus](https://solus-project.com/)
*   [Repositorios git oficiales de Solus](https://git.solus-project.com/)
*   [Estado de las versiones del proyecto Solus](https://build.solus-project.com/)