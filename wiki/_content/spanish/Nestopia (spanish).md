**Estado de la traducción**
Este artículo es una traducción de [Nestopia](/index.php/Nestopia "Nestopia"), revisada por última vez el **2019-01-25**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Nestopia&diff=0&oldid=564708) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Nestopia](https://github.com/0ldsk00l/nestopia) es un emulador de la NES de código abierto que intenta emular su hardware con la mayor precisión posible. Está disponible para Windows, macOS, Linux y BSD. También hay un port para Libretro, véase [RetroArch](/index.php/RetroArch_(Espa%C3%B1ol) "RetroArch (Español)") para obtener más información.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Solución de problemas](#Solución_de_problemas)
    *   [2.1 No hay audio con el backend libao](#No_hay_audio_con_el_backend_libao)
*   [3 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [nestopia](https://aur.archlinux.org/packages/nestopia/) del [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)"). Alternativamente, instale [nestopia-git](https://aur.archlinux.org/packages/nestopia-git/) para la versión de desarrollo.

## Solución de problemas

### No hay audio con el backend libao

Actualmente, el backend libao está roto. Se recomienda cambiar la API de audio a *SDL* en *Emulador -> Configuración -> Audio*.

## Véase también

*   [Página web oficial](http://0ldsk00l.ca/nestopia/)
*   [Página de GitHub](https://github.com/0ldsk00l/nestopia)
*   [Lista de juegos de la NES](https://nesdir.github.io/)