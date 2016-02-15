**Note:** Esta es una artículo complementario del artículo [Openbox (Español)](/index.php/Openbox_(Espa%C3%B1ol) "Openbox (Español)").

Aquí se trata la personalización de la aparencia de Openbox en Arch Linux, así también sobre paneles y áreas de notificación.

.

## Contents

*   [1 Temas y Aparencia](#Temas_y_Aparencia)
    *   [1.1 Temas KDE](#Temas_KDE)
    *   [1.2 Temas GTK](#Temas_GTK)
        *   [1.2.1 GTK2/GTK+](#GTK2.2FGTK.2B)
        *   [1.2.2 GTK1](#GTK1)
    *   [1.3 Tipos GTK](#Tipos_GTK)
    *   [1.4 Iconos GTK](#Iconos_GTK)
    *   [1.5 Temas para el cursor del ratón](#Temas_para_el_cursor_del_rat.C3.B3n)
    *   [1.6 Iconos del escritorio](#Iconos_del_escritorio)
*   [2 Programas Recomendados](#Programas_Recomendados)
    *   [2.1 Gestores de sesiones](#Gestores_de_sesiones)
    *   [2.2 Utilizar "Composite" en el escritorio](#Utilizar_.22Composite.22_en_el_escritorio)
    *   [2.3 Lanzadores de aplicaciones](#Lanzadores_de_aplicaciones)
        *   [2.3.1 dmenu](#dmenu)
        *   [2.3.2 Gmrun](#Gmrun)
    *   [2.4 Gestores de archivos](#Gestores_de_archivos)
    *   [2.5 Paneles, bandejas, y seleccionadores ("Pagers")](#Paneles.2C_bandejas.2C_y_seleccionadores_.28.22Pagers.22.29)

## Temas y Aparencia

### Temas KDE

Las aplicaciones KDE pueden utilizar temas y ser coloreadas para que coincidan perfectamente con sus aplicaciones GTK2 invocando al programa kcontrol, que forma parte del paquete **kdeadmin**.

### Temas GTK

##### GTK2/GTK+

Los temas GTK+ pueden ser fácilmente gestionados con las utilidades _gtk-chtheme_ o _switch2_. Para instalarlas, ejecute:

```
# pacman -S gtk-chtheme

```

y/o

```
# pacman -S gtk-theme-switch2

```

Ejecute entonces **gtk-chtheme** o bien **switch2** y establezca el tema que desee.

##### GTK1

Para los temas GTK1 antiguos, instale el paquete **gtk-theme-switch**:

```
# pacman -S gtk-theme-switch

```

Ejecute entonces _**switch**_ para seleccionar el tema deseado.

### Tipos GTK

Si quiere cambiar el tipo o el tamaño de sus fuente tipográficas, añada lo siguiente a **~/.gtkrc.mine**:

```
style "user-font"
{
font_name = "[font-name] [size]"
}
widget_class "*" style "user-font"
gtk-font-name = "[font-name] [size]"

```

donde [font-name] [size] es el tipo deseado y su tamaño en puntos. Por ejemplo:

```
style "user-font"
{
font_name = "DejaVu Sans 8"
}
widget_class "*" style "user-font"
gtk-font-name = "DejaVu Sans 8"

```

Se requieren ambos campos **font_name** y **gtk-font-name** para tener compatibilidad hacia atrás.

### Iconos GTK

Extraiga el temas de iconos deseado a **/usr/share/icons** (para acceso global del sistema) o **~/.icons** (para acceso local de cada usuario).

Añada lo siguiente a **~/.gtkrc.mine**:

```
gtk-icon-theme-name = "[name-of-icon-theme]"

```

donde [name-of-icon-theme] es el nombre del directorio de temsa de icono. Por ejemplo:

```
gtk-icon-theme-name = "Tango"

```

Asegúrese de que **~/.gtkrc-2.0** está configurado para revisar **~/.gtkrc.mine**:

```
# ~/.gtkrc-2.0
# -- THEME AUTO-WRITTEN DO NOT EDIT
include "/usr/share/themes/Rezlooks-Gilouche/gtk-2.0/gtkrc"
include "/home/username/.gtkrc.mine"
# -- THEME AUTO-WRITTEN DO NOT EDIT

```

### Temas para el cursor del ratón

Extraiga el tema para Xcursor deseado a **/usr/share/icons** (para acceso global del sistema) o a **~/.icons** (para acceso local de cada usuario).

Añada esto a **~/.Xdefaults**:

```
Xcursor.theme:   [name-of-cursor-theme]

```

Donde [name-of-cursor-theme] es el nombre del directorio de temas de cursor. Por ejemplo:

```
Xcursor.theme:	Vanilla-DMZ-AA

```

### Iconos del escritorio

Openbox no proporciona medios para mostrar iconos en el escritorio. [PCManFM](/index.php/PCManFM "PCManFM"), [Rox](/index.php?title=Rox&action=edit&redlink=1 "Rox (page does not exist)"), [Idesk](/index.php/Idesk "Idesk"), o incluso Nautilus (y el demonio gnome-settings-daemon) pueden proporcionar esta función.

ROX y PCmanFM tienen la ventaja adicional de ser gestores de ficheros ligeros.

## Programas Recomendados

### Gestores de sesiones

[SLiM](http://slim.berlios.de/) propordiona una solución ligera y elegante para el ingreso gráfico en configuraciones de Openbox en solitario. Consulte la entrada de [SLiM](/index.php/SLiM "SLiM") en la wiki de Arch ver las instrucciones en detalle. También puedes visitar [Display Manager (Español)](/index.php/Display_Manager_(Espa%C3%B1ol) "Display Manager (Español)") si deseas mas información sobre gestores de sesiones, como así también si deseas no instalar alguno.

### Utilizar "Composite" en el escritorio

[Xcompmgr](/index.php/Xcompmgr "Xcompmgr") es un gestor de composición ligero capaz de renderizar sombras, degradados y sencillas transparencias de las ventanas en Openbox y en otros gestores de ventanas.

### Lanzadores de aplicaciones

#### dmenu

Configure dmenu como se describe en la entrada [dmenu](/index.php/Dmenu "Dmenu") de la wiki.

Añada entonces la siguiente entrada , en la sección <keyboard> de **~/.config/openbox/rc.xml** para habilitar un atajo de teclazo que lance dmenu:

```
   <keybind key="W-p">
     <action name="Execute">
       <command>~/path/to/your/dmenu-script</command>
     </action>
   </keybind>

```

#### Gmrun

[gmrun](http://sourceforge.net/projects/gmrun) proporciona una excelente caja de diálogo para ejecutar órdenes, similar a la combinación de teclas Alt+F2 que se tiene en Gnome o KDE:

```
pacman -S gmrun

```

Añada la siguiente entrada a la sección <keyboard> de **~/.config/openbox/rc.xml** para habilitar la funcionalidad Alt+F2:

```
<keybind key="A-F2">
<action name="execute"><execute>gmrun</execute></action>
</keybind>

```

### Gestores de archivos

Hay muchas posibilidades, pero los gestores de ficheros ligeros más populares son:

*   [Thunar](/index.php/Thunar "Thunar"). Thunar tiene capacidad de automontaje y otros plugins.
*   [ROX](http://rox.sourceforge.net) (ROX proporciona iconos de escritorio)
*   [PCMan](http://pcmanfm.sourceforge.net) (pcmanfm también proporciona iconos de escritorio)

Considere [Gentoo](http://www.obsession.se/gentoo/) o [emelFM](http://emelfm.sourceforge.net/) para soluciones aún más ligeras, ambas utilizan la típica disposición de doble panel de 'Midnight Commander' (ambas requieren gtk 1.2.x).

Por supuesto, puede utilizar el gestor de GNOME, Nautilus. Aunque es un poco más lento que las soluciones anteriores, presenta la ventaja adicional de su capacidad VFS support (p.ej. SSH remoto, FTP y conexiones Samba).

### Paneles, bandejas, y seleccionadores ("Pagers")

Existe un gran número de utilidades que proporcionan un panel (barra de tareas), una bandeja de sistema, y un seleccionador de escritorios virtuales ("Pager") para Openbox. Los más comunes son:

**Paneles**

*   [PyPanel](https://wiki.archlinux.org/index.php/PyPanel)
*   [bmpanel](http://nsf.110mb.com/bmpanel/)
*   [Tint](http://code.google.com/p/ttm/)
*   [LXPanel](http://sourceforge.net/projects/lxpanel)
*   [fbpanel](http://fbpanel.sourceforge.net)
*   [PerlPanel](http://perlpanel.org/)
*   [fspanel](http://www.chatjunkies.org/fspanel/)
*   [xfce4-panel](http://www.xfce.org/projects/xfce4-panel/)
*   [gnome-panel](http://developer.gnome.org/arch/gnome/corecomponents/panel/)
*   [avant-window-navigator](http://code.google.com/p/avant-window-navigator/)
*   [cairo-dock](http://developer.berlios.de/projects/cairo-dock/)

**Bandejas**

*   [Stalonetray](http://stalonetray.sourceforge.net/)
*   [Trayer](http://download.gna.org/fvwm-crystal/trayer/1.0/)

**Seleccionadores**

*   [Visibility](http://projects.l3ib.org/trac/visibility)
*   [bbpager](http://bbtools.sourceforge.net/)
*   [netwmpager](https://aur.archlinux.org/packages.php?ID=970)
*   [IPager](http://useperl.ru/ipager/index.en.html)

Elija alguno y añádalo a su archivo de arranque.