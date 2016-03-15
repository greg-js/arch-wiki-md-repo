**Warning:** Esta documentación esta en proceso de traducción por lo que habrá partes sin terminar de traducir

	*Esta es una guia de las distintas etiquetas para editar un fichero theme.cfg*

	*Este archivo consta de dos partes: la primera explica cada uno de los elementos y la segunda es una lista completa que puede ser pegada en un archivo theme.cfg para que puedas comenzar.*

	*Esta estructurado para explicar los elementos mas relevantes*

## Contents

*   [1 Como trabajan los elementos](#Como_trabajan_los_elementos)
    *   [1.1 {texture type}](#.7Btexture_type.7D)
    *   [1.2 {color}](#.7Bcolor.7D)
    *   [1.3 {archivo}](#.7Barchivo.7D)
    *   [1.4 {entero}](#.7Bentero.7D)
    *   [1.5 {boleano}](#.7Bboleano.7D)
    *   [1.6 {alpha}](#.7Balpha.7D)
    *   [1.7 {redondeo}](#.7Bredondeo.7D)
    *   [1.8 {justificar}](#.7Bjustificar.7D)
    *   [1.9 {bullet}](#.7Bbullet.7D)
    *   [1.10 {string}](#.7Bstring.7D)
    *   [1.11 {fuente}](#.7Bfuente.7D)
    *   [1.12 Explanation of items that are a little confusing](#Explanation_of_items_that_are_a_little_confusing)
    *   [1.13 Notes for getting started](#Notes_for_getting_started)
*   [2 structured items](#structured_items)
    *   [2.1 La barra de herramientas](#La_barra_de_herramientas)
        *   [2.1.1 opciones generales](#opciones_generales)
        *   [2.1.2 Area del reloj](#Area_del_reloj)
        *   [2.1.3 The workspace title area](#The_workspace_title_area)
        *   [2.1.4 La barra de iconos](#La_barra_de_iconos)
        *   [2.1.5 Empty - when no windows are shown as icons](#Empty_-_when_no_windows_are_shown_as_icons)
        *   [2.1.6 Focused window icon](#Focused_window_icon)
        *   [2.1.7 Unfocused window icon](#Unfocused_window_icon)
        *   [2.1.8 The toolbar buttons for prevworkspace, nextworkspace, prevwindow and next window](#The_toolbar_buttons_for_prevworkspace.2C_nextworkspace.2C_prevwindow_and_next_window)
    *   [2.2 The windows](#The_windows)
        *   [2.2.1 general](#general)
    *   [2.3 focused and unfocused window](#focused_and_unfocused_window)
        *   [2.3.1 titlebar](#titlebar)
        *   [2.3.2 label](#label)
        *   [2.3.3 handle](#handle)
        *   [2.3.4 grips](#grips)
        *   [2.3.5 button](#button)
        *   [2.3.6 window buttons](#window_buttons)
        *   [2.3.7 close](#close)
        *   [2.3.8 max](#max)
        *   [2.3.9 icon](#icon)
        *   [2.3.10 stick](#stick)
        *   [2.3.11 stuck](#stuck)
    *   [2.4 The menu](#The_menu)
        *   [2.4.1 general settings](#general_settings)
        *   [2.4.2 title - top of each menu](#title_-_top_of_each_menu)
        *   [2.4.3 frame - menu body](#frame_-_menu_body)
        *   [2.4.4 hilite](#hilite)
        *   [2.4.5 details](#details)
        *   [2.4.6 set the wallpaper with an app...](#set_the_wallpaper_with_an_app...)
        *   [2.4.7 The slit](#The_slit)

## Como trabajan los elementos

Cada elemento se divide en main*object.sub*object.item: valor p.e. toolbar.clock.pixmap: valor

El valor depende del elemento p.e. .pixmap: {archivo}

El elemento pixmaps requiere del valor {fichero} para indicar el archivo de imagen que se usara p.e. toolbar.clock.pixmap: clock.xpm

¡Esto es todo! Lo unico que necesitas saber son las opciones de cada valor. Ahora se explicaran las opciones de cada valor del elemento. La segunda parte contiene la lista entera de elementos con sus valores, así como ejemplos que puedes copiar en un fichero para trabajar con ellos.

### {texture type}

pixmap options: requires a filename in *.pixmap

```
 pixmap
   tiled

```

non-pixmap options: uses **.color to color the objects, use** .colorTo for gradients and highlights

```
 flat
   gradient
     vertical
     horizontal
     diagonal
     crossdiagonal
     pipecross
     elliptic
     rectangle
     pyramid

```

e.g menu.frame: Flat Gradient Vertical
or

```
   raised
   sunken
     bevel1
     bevel2
       gradient
         vertical
         horizontal
         diagonal
         crossdiagonal
         pipecross
         elliptic
         rectangle
         pyramid

```

e.g. menu.title: Raised Bevel1 Gradient Vertical

### {color}

Cualquier color en hexadecimal:

```
 #ffffff
 #000000

```

p.e menu.title.textColor: #ffffff

cualquier color rgb mostrado en /usr/X11R6/lib/X11/rgb.txt

```
rgb:4/3/2

```

p.e menu.title.textColor: rgb:4/3/2

cualquier color

```
white
black

```

p.e menu.title.textColor: white

### {archivo}

el nombre de un fichero de imagen en pixmaps (.xpm o .png), deben de colocarse en la carpeta pixmaps, la cual debe de estar en la misma carpeta que el archivo theme.cfg p.e. menu.title.pixmap: iconbarf.xpm

### {entero}

el numero que determinara el ancho/alto de algo en pixels p.e window.title.height: 22

### {boleano}

Activara o desactivara algo

```
true
false

```

p.e .toolbar.shaped: true

### {alpha}

la transparencia - debiendo ser un entero entre 0 y 255 donde 0 is invisible/transparente
y 255 es solido/opaco - 150 suele ser el mas usado

p.e .window.alpha: 255

### {redondeo}

opcion para redondear las esquinas

```
TopLeft
TopRight
BottomLeft
BottomRight

```

p.e .window.roundCorners: TopLeft TopRight

### {justificar}

donde se posicionara una imagen o texto

```
Center
Left
Right

```

p.e .window.justify: Center

### {bullet}

solo usado en la opcion menu.bullet. solo para temas sin imagenes.

```
triangle
square
diamond
empty

```

p.e .menu.bullet: triangle

### {string}

only used for the root.command: option. lets you set the path to a wallapaper image and which application to display it

```
fbsetbg -f wallpaper.png

```

e.g.root.command: fbsetbg -a mywallpaper.png

### {fuente}

la fuente que se usara

```
font-size

```

p.e .menu.frame.font: trebuchet-10

estas opciones se pueden combinar como quieras

```
bold
shadow
italic

```

deben de estar separados por dos punto o punto y coma

```
font-size:bold:shadow:italic

```

p.e .menu.title.font: trebuchet-10:shadow:bold

### Explanation of items that are a little confusing

.colorTo - if you use a gradient setting then the belnd is between .color and .colorTo

.borderWidth - gives a border of {integer} width. 0 will give no border

.bevelwidth - the bevel is between the border and the object e.g. in the menu, menu.bevelWidth increases the space between menu entries

.picColor - sets the color of a default fluxbox image that is added on top of an item e.g. toolbar.button.picColor

.alpha - a transparency setting

### Notes for getting started

1\. using window.label and window.title with window.bevelWidth

When you use window.label this will overlay window.title. however, if you set window.bevelWidth the window.title will show as a "border" around window.label i.e. window.label floats over window.title This allows some quite simple but cool effects but does restrict window buttons (see below)

2\. using toolbar and toolbar.iconbar.*, toolbar.clock, toolbar.workspace, toolbar.button

As with 1\. above. toolbar is overlayed by toolbar.iconbar.*, toolbar.clock, toolbar.workspace and toolbar.button. Again setting toolbar.bevelWidth allows all of the these to float over toolbar, giving a border/layer effect

3\. using window buttons

If window.bevelWidth is **not** used then all window.* buttons (close, icon, etc) may be any size but must be **square** and all have the **same dimensions**. This allows some very creative button designs and most styles at Fluxmod use this method

However, if window.bevelWidth **is** used then the buttons are restricted in size by the **font** used for window.label. Here the best thing to do is choose the font size you want for window.label then make your pixmaps to the correct size. Or, in this case, you could set the window.button options to give a background and allow fluxbox to overlay with the default pixmaps (you can choose the colour with window.button.*.picColor) or create your own to the correct dimensions.

4\. using * (wildcards)

## structured items

a theme.cfg template, laid out as below, is available for you to download and edit here [http://dtw.jiwe.org/share/StyleItems.txt](http://dtw.jiwe.org/share/StyleItems.txt)

```
 This work is licensed under the Creative Commons
 Attribution-NonCommercial-ShareAlike License.
 To view a copy of this license, visit
 http://creativecommons.org/licenses/by-nc-sa/1.0/
 or send a letter to Creative Commons,
 559 Nathan Abbott Way, Stanford, California 94305, USA.

---------------------------------------------
 FluxMOD http://www.fluxmod.dk
 Style Name:
 Style Author:
 Style Date:
---------------------------------------------

```

### La barra de herramientas

#### opciones generales

toolbar.borderWidth: {entero}
toolbar.borderColor: {color}

toolbar.shaped: {boleano}
toolbar.alpha: {alpha}
toolbar.height: {entero}

#### Area del reloj

toolbar.clock.font: {fuente}
toolbar.clock.textColor: {color}
toolbar.clock.justify: {justificacion}

toolbar.clock: {textura}
toolbar.clock.pixmap: {archivo}
toolbar.clock.color: {color}
toolbar.clock.colorTo: {color}
toolbar.clock.borderWidth: {entero}
toolbar.clock.borderColor: {color}

#### The workspace title area

toolbar.workspace.font: {fuente}
toolbar.workspace.textColor: {color}
toolbar.workspace.justify: {justificación}

toolbar.workspace: {textura}
toolbar.workspace.pixmap: {archivo}
toolbar.workspace.color: {color}
toolbar.workspace.colorTo: {color}
toolbar.workspace.borderWidth: {entero}
toolbar.workspace.borderColor: {color}

#### La barra de iconos

where windows are shown depending on Iconbar Mode which is set by right-clicking on the fluxbox toolbar

toolbar.iconbar.borderWidth: {integer}
toolbar.iconbar.borderColor: {color}

#### Empty - when no windows are shown as icons

toolbar.iconbar.empty: {texture type}
toolbar.iconbar.empty.pixmap: {filename}
toolbar.iconbar.empty.color: {color}
toolbar.iconbar.empty.colorTo: {color}

#### Focused window icon

toolbar.iconbar.focused.font: {font}
toolbar.iconbar.focused.textColor: {color}
toolbar.iconbar.focused.justify: {justify}
toolbar.iconbar.focused: {texture type}
toolbar.iconbar.focused.pixmap: {filename}
toolbar.iconbar.focused.color: {color}
toolbar.iconbar.focused.colorTo: {color}
toolbar.iconbar.focused.borderWidth: {integer}
toolbar.iconbar.focused.borderColor: {color}

#### Unfocused window icon

toolbar.iconbar.unfocused.font: {font}
toolbar.iconbar.unfocused.textColor: {color}
toolbar.iconbar.unfocused.justify: {justify}
toolbar.iconbar.unfocused: {texture type}
toolbar.iconbar.unfocused.pixmap: {filename}
toolbar.iconbar.unfocused.color: {color}
toolbar.iconbar.unfocused.colorTo: {color}
toolbar.iconbar.unfocused.borderWidth: {integer}
toolbar.iconbar.unfocused.borderColor: {color}

#### The toolbar buttons for prevworkspace, nextworkspace, prevwindow and next window

toolbar.button {texture type}
toolbar.button.pixmap: {filename}
toolbar.button.color: {color}
toolbar.button.colorTo: {color}
toolbar.button.picColor: {color}
toolbar.button.pressed: {texture type}
toolbar.button.pressed.pixmap: {filename}
toolbar.button.pressed.color: {color}
toolbar.button.pressed.colorTo: {color}
toolbar.button.pressed.picColor: {color}

### The windows

focus is the currently selected window - unfocus is in the background

#### general

window.font: {font}
window.justify: {justify}
window.roundCorners: {round}
window.alpha: {alpha}
window.bevelWidth: {integer}
window.borderWidth: {integer}
window.borderColor: {color}

### focused and unfocused window

#### titlebar

the "background" of the window title. This is layered under window.label - see the note in part one

window.title.height: {integer}
window.title.focus: {texture type}
window.title.focus.pixmap: {filename}
window.title.focus.color: {color}
window.title.focus.colorTo: {color}
window.title.unfocus: {texture type}
window.title.unfocus.pixmap: {filename}
window.title.unfocus.color: {color}
window.title.unfocus.colorTo: {color}

#### label

the text background. This is layered over window.title - see the note in part one

window.label.focus: {texture type}
window.label.focus.pixmap: {filename}
window.label.focus.color: {color}
window.label.focus.colorTo: {color}
window.label.focus.textColor: {color}
window.label.unfocus: {texture type}
window.label.unfocus.pixmap: {filename}
window.label.unfocus.color: {color}
window.label.unfocus.colorTo: {color}
window.label.unfocus.textColor: {color}

#### handle

the bar along the bottom of the window for resizing vertically

window.handleWidth: {integer}
window.handle.focus: {texture type}
window.handle.focus.pixmap: {filename}
window.handle.focus.color: {color}
window.handle.focus.colorTo: {color}
window.handle.unfocus: {texture type}
window.handle.unfocus.pixmap: {filename}
window.handle.unfocus.color: {color}
window.handle.unfocus.colorTo: {color}

#### grips

either side of the handle for resizing in horizontally and vertically

window.grip.focus: {texture type}
window.grip.focus.pixmap: {filename}
window.grip.focus.color: {color}
window.grip.focus.colorTo: {color}
window.grip.unfocus: {texture type}
window.grip.unfocus.pixmap: {filename}
window.grip.unfocus.color: {color}
window.grip.unfocus.colorTo: {color}

#### button

sets the background for the window buttons - not visible if window buttons (below) are used

window.button.focus: {texture type}
window.button.focus.pixmap: {filename}
window.button.focus.color: {color}
window.button.focus.colorTo: {color}
window.button.focus.picColor: {color}
window.button.unfocus: {texture type}
window.button.unfocus.pixmap: {filename}
window.button.unfocus.color: {color}
window.button.unfocus.colorTo: {color}
window.button.unfocus.picColor: {color}
window.button.pressed: {texture type}
window.button.pressed.pixmap: {filename}
window.button.pressed.color: {color}
window.button.pressed.colorTo: {color}

#### window buttons

close, max and min, shade, stick and stuck

#### close

window.close.pixmap: {filename}
window.close.unfocus.pixmap: {filename}
window.close.pressed.pixmap: {filename}

#### max

window.maximize.pixmap: {filename}
window.maximize.unfocus.pixmap: {filename}
window.maximize.pressed.pixmap: {filename}

#### icon

window.iconify.pixmap: {filename}
window.iconify.unfocus.pixmap: {filename}
window.iconify.pressed.pixmap: {filename}

#### stick

window.stick.pixmap: {filename}
window.stick.unfocus.pixmap: {filename}
window.stick.pressed.pixmap: {filename}

#### stuck

window.stuck.pixmap: {filename}
window.stuck.unfocus.pixmap: {filename}

### The menu

#### general settings

menu.borderWidth: {integer}
menu.bevelWidth: {integer}
menu.borderColor: {color}

#### title - top of each menu

menu.title.font: {font}
menu.title.textColor: {color}
menu.title.justify: {justify}
menu.title: {texture type}
menu.title.pixmap: {filename}
menu.title.color: {color}
menu.title.colorTo: {color}

#### frame - menu body

menu.frame.font: {font}
menu.frame.textColor: {color}
menu.frame.disableColor: {color}
menu.frame.justify: {justify}
menu.frame: {texture type}
menu.frame.pixmap: {filename}
menu.frame.color: {color}
menu.frame.colorTo: {color}

#### hilite

how the options are highlighted when mouse is over them

menu.hilite.textColor: {color}
menu.hilite: {texture type}
menu.hilite.pixmap: {filename}
menu.hilite.color: {color}
menu.hilite.colorTo: {color}

#### details

menu.roundCorners: {round}
menu.bullet.position: {justify}
menu.bullet: {bullet}
menu.submenu.pixmap: {filename}
menu.selected.pixmap: {filename}
menu.unselected.pixmap: {filename}

#### set the wallpaper with an app...

rootCommand: {string}

#### The slit

settings for the slit - not applicable if slit alpha is set to 0

slit: {texture type}
slit.pixmap: {filename}
slit.color: {color}
slit.colorTo: {color}
slit.borderWidth: {integer}
slit.bevelWidth: {integer}
slit.borderColor: {color}