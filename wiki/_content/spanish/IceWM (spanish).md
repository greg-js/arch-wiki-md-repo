Artículos relacionados

*   [Window Manager (Español)](/index.php/Window_Manager_(Espa%C3%B1ol) "Window Manager (Español)")

Deacuerdo a [Wikipedia](https://en.wikipedia.org/wiki/Icewm "wikipedia:Icewm"), "IceWM es un gestor de ventanas para el sistema gráfico X Window, utilizado en sistemas Unix y derivados. Fue escrito por Marko Maček desde cero en C++ y está disponible bajo los términos de la licencia GPL en unos 20 idiomas. Es relativamente ligero en cuanto a uso de memoria RAM y CPU, y viene con temas que imitan las interfaces de usuario de sistemas como Windows 95, OS/2, Motif, etc.".

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 IceWM en Solitario](#IceWM_en_Solitario)
*   [3 IceWM como WM para Escritorios](#IceWM_como_WM_para_Escritorios)
*   [4 Configuración](#Configuraci.C3.B3n)
    *   [4.1 Menú](#Men.C3.BA)
    *   [4.2 Temas](#Temas)
*   [5 Gestores de Archivos](#Gestores_de_Archivos)
*   [6 See also](#See_also)

## Instalación

IceWM se puede instalar desde los repositorios oficiales con el paquete [icewm](https://www.archlinux.org/packages/?name=icewm).

Alternativamente, La última versión de pruebas esta en ([icewm-testing](https://aur.archlinux.org/packages/icewm-testing/)) y la última versión CVS en ([icewm-cvs](https://aur.archlinux.org/packages/icewm-cvs/)) disponibles en [AUR](/index.php/AUR "AUR"). Estas versiones corrigen Bugs y dan nuevas funcionalidades (Debido al lentísimo desarrollo de IceWM es posible que las versiones de AUR sean las mismas que las oficiales de Arch).

## IceWM en Solitario

Para correr IceWM como un WM unicamente agregue esto a su **`~/.xinitrc`**:

```
exec icewm

```

icewm-session correrá icewm, icewmbg y icewmtray, así que agregue esto a su **`~/.xinitrc`** para implementar el manejo de sesión básico:

```
exec icewm-session

```

Vea [xinitrc](/index.php/Xinitrc "Xinitrc") para mas información.

## IceWM como WM para Escritorios

Las acciones requeridas para que IceWM corra junto a un DE son basicamente las mismas que para [OpenBox](/index.php/Openbox_(Espa%C3%B1ol)#Openbox_como_WM_junto_a_otros_entornos_de_escritorio "Openbox (Español)") (y probablemente para otros gestores de ventanas también).

## Configuración

Aunque la configuración de IceWM esta basada an archivos de texto, esta disponible una herramienta gráfica mediante el paquete [icewm-utils](https://aur.archlinux.org/packages/icewm-utils/) en [community]. De todas maneras, estas herramientas son relativamente viejas y muchos usuarios prefieren simplemente editar los archivos de configuración. Estos cambios pueden aplicarse al sistema en general (en /etc/icewm/) o a un usuario en específico (en ~/.icewm/).

Para cambiar la configuración por defecto, simplemente copia los archivos de configuración por defecto de `/usr/share/icewm/` a `~/.icewm/`, por ejemplo:

**Note:** Haz esto como usuario normal, no como root.

```
$ mkdir ~/.icewm/
$ cp -R /usr/share/icewm/* ~/.icewm/

```

*   `preferences` es el archivo principal de configuración de IceWM.
*   `menu` controla el contenido del menú de aplicaciones de IceWM.
*   `keys` permite personalizar los atajos de teclado.
*   `toolbar` indica los lanzadores en la barra de tareas.
*   `winoptions` comportamiento de aplicaciones especificas.
*   `theme` directorio de temas.
*   `startup` script para aplicaciones al inicio.
*   `shutdown` para apagar el equipo.

### Menú

*   [menumaker](https://www.archlinux.org/packages/?name=menumaker) disponible en [community] es un script escrito en python que automáticamente crea las entradas del menú de aplicaciones instaladas en tu sistema. Aunque esto talvez resulte en un menú lleno de programas no deseados, sigue siendo mas rápido que editar manualmente el archivo de configuración del menú. al utilizar MenuMaker, usa la opción -f para sobreescribir el menú existente:

```
# mmaker -f icewm

```

*   Otra herramienta escrita en Perl es [archlinux-xdg-menu](https://www.archlinux.org/packages/?name=archlinux-xdg-menu):

```
# xdg_menu --format icewm --fullmenu --root-menu /etc/xdg/menus/arch-applications.menu > ~/.icewm/menu

```

### Temas

Algunos temas son incluidos por defecto, muchos otros estan disponibles con el paquete [icewm-themes](https://aur.archlinux.org/packages/icewm-themes/) pero incluso los mejores de ellos tienen una aparencia arcaica al mejor estilo de un "viejo windows", hay mejores y más atractivos ejemplos (como estos por ejemplo: [[1]](http://box-look.org/content/show.php/Carbonit+Ice?content=146421%7Ceste), [[2]](http://box-look.org/content/show.php/IceBuntu?content=62935%7Cthis) or [[3]](http://box-look.org/content/show.php/IceClearlooks?content=96346%7Cthis)) muchos mas pueden ser encontrados en [box-look.org](http://www.box-look.org/index.php?xcontentmode=7311).

## Gestores de Archivos

Se debe señalar que IceWM es un gestor de ventanas y por lo tanto no incluye un Gestor de Archivos.[spacefm](https://aur.archlinux.org/packages/spacefm/), [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm), y [rox](https://www.archlinux.org/packages/?name=rox) pueden gestionar los íconos del escritorio, aunque [iDesk](/index.php/Idesk "Idesk") también puede ser usado para lograr dicha funcionalidad.

**Note:** Para una mejor lista de Gestores de Archivos, vea [File managers](/index.php/Category:File_managers "Category:File managers").

## See also

*   [Xinitrc](/index.php/Xinitrc "Xinitrc")
*   [Sitio Oficial de IceWM](http://www.icewm.org/)
*   [IceWM - The Cool Window Manager](http://www.osnews.com/story.php/7774/IceWM--The-Cool-Window-Manager/) - Detallada introducción en OSNews
*   [IceWM - A desktop for Windows emigrants](http://polishlinux.org/apps/window-managers/icewm-a-desktop-for-windows-emmigrants/) - Intoducción y tutorial en polishlinux.org