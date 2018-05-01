Fluxbox es un gestor de ventanas para X. Esta basado en el código del abandonado Blackbox 0.61.1, pero con continuas mejoras y desarrollo. Fluxbox es muy ligero, consume pocos recursos y rápido, provee de varias herramientas útiles como tabulación y agrupación, ademas es fácil de configurar.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Comenzando con Fluxbox](#Comenzando_con_Fluxbox)
    *   [2.1 Método 1: KDM/GDM Login/Session Managers](#M.C3.A9todo_1:_KDM.2FGDM_Login.2FSession_Managers)
    *   [2.2 Metodo 2: ~/.xinitrc](#Metodo_2:_.7E.2F.xinitrc)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Mantenimiento del menú](#Mantenimiento_del_men.C3.BA)
        *   [3.1.1 fluxbox-generate_menu](#fluxbox-generate_menu)
        *   [3.1.2 MenuMaker](#MenuMaker)
        *   [3.1.3 Arch Linux Xdg menu](#Arch_Linux_Xdg_menu)
        *   [3.1.4 Crear/editar manualmente el menú](#Crear.2Feditar_manualmente_el_men.C3.BA)
    *   [3.2 Teclas de acceso rápido](#Teclas_de_acceso_r.C3.A1pido)
    *   [3.3 Espacios de trabajo](#Espacios_de_trabajo)
    *   [3.4 Tabulación y agrupación](#Tabulaci.C3.B3n_y_agrupaci.C3.B3n)
    *   [3.5 Fondos de pantalla](#Fondos_de_pantalla)
        *   [3.5.1 Cambiar fondos de pantalla fácilmente](#Cambiar_fondos_de_pantalla_f.C3.A1cilmente)
        *   [3.5.2 Usando Feh en FluxBox](#Usando_Feh_en_FluxBox)
    *   [3.6 Temas](#Temas)
    *   [3.7 La Slit](#La_Slit)
    *   [3.8 Auto arrancar aplicaciones](#Auto_arrancar_aplicaciones)
    *   [3.9 Terminales rxvt-unicode transparente](#Terminales_rxvt-unicode_transparente)
    *   [3.10 La vida después de xorg.conf](#La_vida_despu.C3.A9s_de_xorg.conf)
        *   [3.10.1 Configurar el teclado correctamente](#Configurar_el_teclado_correctamente)
        *   [3.10.2 Deshabilitar ahorro de energia](#Deshabilitar_ahorro_de_energia)
*   [4 Recursos adicionales](#Recursos_adicionales)

## Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [fluxbox](https://www.archlinux.org/packages/?name=fluxbox) de los repositorios oficiales.

## Comenzando con Fluxbox

### Método 1: KDM/GDM Login/Session Managers

Si usas [KDM](/index.php/KDM "KDM") o [GDM](/index.php/GDM "GDM") se añadirá automáticamente una entrada para Fluxbox. Simplemente escoge Fluxbox en el menú de sesiones antes de iniciar sesión.

### Metodo 2: ~/.xinitrc

Abre el fichero `~/.xinitrc` y añade el siguiente código:

```
exec startfluxbox 

```

**Nota:** Solo se puede tener una linea `exec` en tu fichero `~/.xinitrc`.

## Configuración

Los archivos de configuración de Fluxbox del sistema se encuentran en la carpeta `/usr/share/fluxbox` y los del usuario en `~/.fluxbox`. Los archivos de configuración del usuario son:

*   init: El archivo principal de configuración. Mira [Editing the init file](http://fluxbox-wiki.org/index.php?title=Editing_the_init_file)
*   menu: la configuración del menú. Mira mas abajo y en [Editing the menu file](http://fluxbox-wiki.org/index.php?title=Editing_the_menu)
*   keys: los atajos de teclado de fluxbox (hotkeys). Mira mas abajo y [aquí](http://fluxbox-wiki.org/index.php?title=Keyboard_shortcuts)
*   startup: las aplicaciones que se iniciaran al arrancar fluxbox. Mira abajo para .xinitrc y/o [aquí](http://fluxbox-wiki.org/index.php?title=Editing_the_startup_file)
*   overlay: un archivo de configuración para anular los elementos de los estilos. Mirar [aquí](http://fluxbox-wiki.org/index.php?title=Style_overlay).
*   apps: guarda configuraciones especificas para las aplicaciones (posición en la pantalla, tamaño de la venta, etc). Mira [aquí](http://fluxbox-wiki.org/index.php?title=Editing_the_apps_file)
*   windowmenu: fichero de configuración para cambiar el menú de las ventanas. Mira en [[2]](http://fluxbox-wiki.org/index.php?title=Editing_the_windowmenu)

En el directorio hay otros archivos de configuración menos importantes. Los archivos mas importantes son init, menu, keys y tal vez startup.

### Mantenimiento del menú

Cuando instalas por primera vez Fluxbox este genera una configuración básica para el menú en ~/.fluxbox/menu. Para acceder a el pulsa con el botón derecho del ratón en una zona libre del escritorio. Para mejorar el menú y editar/añadir entradas existen cuatro formas de hacerlo:

#### fluxbox-generate_menu

Este comando viene de serie con Fluxbox:

```
$ fluxbox-generate_menu

```

Este comando auto-genera el archivo `~/.fluxbox/menu/` basándose en los programas que tengas instalados. Sin embargo, no es tan exhaustivo como el generador por "menumaker" (ver debajo).

#### MenuMaker

[MenuMaker](http://menumaker.sourceforge.net) es una poderosa herramienta que genera menús basados en XML para una variedad de gestores de ventanas, Fluxbox incluido. MenuMaker busca ejecutables en el sistema y genera el menú basándose en los resultados. Puede configurarse para excluir aplicaciones de Legacy X, GNOME, KDE o Xfce.

Para instalar MenuMaker:

```
# pacman -S menumaker

```

Una vez instalado, para generar el menú o sobrescribir el existente:

```
$ mmaker -f FluxBox

```

Para ver las opciones de MenuMaker:

```
$ mmaker --help

```

#### Arch Linux Xdg menu

Para instalar [XdgMenu](/index.php/XdgMenu "XdgMenu"):

```
# pacman -S archlinux-xdg-menu

```

Para generar el menú para Fluxbox:

```
$ xdg_menu --fullmenu --format fluxbox --root-menu /etc/xdg/menus/arch-applications.menu >~/.fluxbox/menu

```

Mas información:

```
$ xdg_menu --help

```

#### Crear/editar manualmente el menú

Usa tu editor de texto favorito para modificar: "~/.fluxbox/menu" . La sintaxis básica para añadir una entrada en el menú es:

```
[exec] (nombre) {comando}

```

...donde "nombre" es el titulo que aparecera en la entrada y "comando" es el ejecutable, p.e.:

```
[exec] (Firefox) {/usr/bin/firefox}

```

Si quieres crear un submenú escribe:

```
[submenu] (Nombre)
...
...
[end]

```

Guarda el archivo, cierra el editor y ya tienes el nuevo menú. No es necesario reiniciar Fluxbox para ver los cambios. Para mas información lee [editing the fluxbox menu](http://fluxbox-wiki.org/index.php?title=Editing_the_menu).

### Teclas de acceso rápido

Fluxbox ofrece funciones básicas de atajos de teclado. El archivo con la configuración esta en `~/.fluxbox/keys`. La tecla Control esta representada con al palabra "Control". Mod1 corresponda a la tecla Alt y Mod4 corresponde a Meta (no es una tecla estándar pero muchos usuarios mapean Meta con la tecla "Win"). Cuando se instala y ejecuta Fluxbox por primera vez provee una muy útil y casi completa configuración de teclas de acceso rápido. Debería de leer y aprende r del archivo ~/.fluxbox/keys para mejorar su experiencia con Fluxbox.

Ejemplo: una manera rápida de controlar el volumen principal:

```
Control Mod1 Up :Exec amixer set Master,0 5%+  
Control Mod1 Down :Exec amixer set Master,0 5%-

```

### Espacios de trabajo

Fluxbox tiene por defecto con 4 escritorios. Puedes cambiar entre ellos usando la combinación de teclas Ctrl+F1-F4, pulsando sobre las flechas en la barra de tareas o con la rueda del ratón. Si pulsa con el botón central se abrirá un menú con los escritorios, una lista de los programas que se están ejecutando en el y unas pocas opciones.

### Tabulación y agrupación

Si tienes 2 ventanas abiertas pulsa sobre una de ellas con el botón central del ratón ya arrástrala a la otra. Las dos ventanas han sido agrupadas y puedes cambiar entre ellas pulsando en las pestañas situadas arriba de la ventana. Las operaciones sobre la ventana afectaran a todo el "grupo".

### Fondos de pantalla

Históricamente configurar el fondo de pantalla en Fluxbox a sido complicado, especialmente si se trabajaba con transparencias. En la Wiki de Fluxbox hay una entrada al respecto [Poner un fondo](http://fluxbox-wiki.org/index.php?title=Poner_un_fondo).

La via mas rápida para saber si en Arch tenemos instalado algún programa para configurar el fondo de pantalla:

```
 $ fbsetbg -i

```

Si no es así, instala feh, esetroot o wmsetbg con pacman. Luego añade lo siguiente en ~/.xinitrc o en ~/.fluxbox/startup , p.e.:

```
 fbsetbg /ruta/a/mi/imagen.imagen

```

#### Cambiar fondos de pantalla fácilmente

Añade lo siguiente en tu menú de Fluxbox:

```
[submenu] (Backgrounds)
[wallpapers] (~/.fluxbox/backgrounds)
[wallpapers] (/usr/share/fluxbox/backgrounds)
[end]

```

Mete las imágenes que usaras de fondo en `~/.fluxbox/backgrounds` u otra carpeta que especifiques, Estos saldrán como en el menú de Estilos.\

#### Usando Feh en FluxBox

Instala feh usando:

```
# pacman -S feh

```

Puedes añadir un submenu en `~/.fluxbox/menu` para cambiar el fondo de pantalla:

```
[submenu] (Fondos)
[wallpapers] (/ruta/a/tus/fondos) {feh --bg-scale}
[end]

```

Para estar seguro de que Fluxbox cargara el fondo de pantalls:

**1.** Añade permisos de ejecución a `.fehbg`:

```
$ chmod 770 ~/.fehbg

```

**2.** Añade o modifica la siguiente linea en `~/.fluxbox/init`:

```
session.screen0.rootCommand:	~/.fehbg

```

**3.** o añade o modifica la siguiente linea en `~/.fluxbox/startup`:

```
~/.fehbg

```

### Temas

Para instalar temas en Fluxbox, descomprime los archivos en la carpeta styles. Los directorios por defecto son:

*   global - `/usr/share/fluxbox/styles`
*   usuario - `~/.fluxbox/styles`

Actualmente en [AUR](/index.php/AUR "AUR") hay varias compilaciones de buenos temas para Fluxbox llamados "fluxbox-styles". Descarga uno desde [aquí](https://aur.archlinux.org/packages.php?ID=28743) e instala el paquete para obtener varios temas. Una vez instalados correctamente aparecerán en la sección Styles dentro de Fluxbox en el menú .

Para crear tus temas de Fluxbox lee [Fluxbox Style Guide](/index.php/Fluxbox_Style_Guide "Fluxbox Style Guide") y esto [guía de estilo](http://tenr.de/howto/style_fluxbox/style_fluxbox.html).

### La Slit

Fluxbox, WindowMaker y algunos gestores de ventanas ligeros tienen un "Slit". En ella se acoplan pequeños programas llamados "docks" que se verán en todos los espacios de trabajo. Estos no se pueden mover libremente y no les afecta el manipula miento de las ventanas. Son básicamente pequeñas aplicaciones. Una dock son utiles en varias situaciones como relojes, monitores de sistema, etc. Visita [Dockapps.org](http://dockapps.org) para ver varias de estas pequeñas aplicaciones

### Auto arrancar aplicaciones

La manera de Archlinux de auto arrancar es poner el código en el archivo `~/.xinitrc`. Por favor, mire [Xinitrc](/index.php/Xinitrc "Xinitrc"). Sin embargo, fluxbox provee un metodo para hacerlo al arrancar. El archivo `~/.fluxbox/startup` es un script para auto arrancar programas cuando lo hace el. tambien se puede usar para editar variables del sistema, etc. El símbolo # sirve para escribir un comentario.

Un ejemplo:

```
fbsetbg -l # establece el ultimo fondo de pantalla definido, muy útil y recomendable.
# In the below commands the ampersand symbol (&) is required on all applications that do not terminate immediately. 
# failure to provide them will cause fluxbox not to start.
idesk & 
xterm &
# exec is for starting fluxbox itself, don't put an ampersand (&) after this or fluxbox will exit immediately
exec /usr/bin/fluxbox
# or if you want to keep a log, uncomment the below command and comment out the above command:
# exec /usr/bin/fluxbox -log ~/.fluxbox/log

```

**Nota:** Cada linea debe de acabar con el símbolo &, de lo contrario los programas no terminaran correctamente y provocar que Fluxbox no arranque.

### Terminales rxvt-unicode transparente

Instalar urxvt:

```
 # pacman -S rxvt-unicode

```

Lanza urxvtcon estas opciones:

```
 $ urxvt -depth 32 -bg rgba:0000/0000/0000/bbbb -tint grey

```

O edita el archivo ~/.Xdefaults y escribe los comandos equivalentes de urxvt en el archivo. Mira [Xdefaults](/index.php/Xdefaults "Xdefaults") para infotmación.

### La vida después de xorg.conf

Xorg ya no requiere del archivo xorg.conf. Tradicionalmente se usaba para configurar el teclado y el ahorro de energía. Por suerte hay maneras elegantes de hacerlo sin el archivo xorg.conf.

#### Configurar el teclado correctamente

Añade esto en el archivo `~/.fluxbox/startup`:

```
setxkbmap es -variant intl& # para habilitar el teclado español y poder usar la tecla Ñ y los caracteres especiales del idioma.

```

Después de 'es' también puede pasar el código del lenguaje y quitar la opción de la variante (ej.: 'es_intl', hace lo mismo que el comando anterior). Mira man setxkbmap para ver mas opciones.

Para poder cambiar el teclado, añade lo siguiente en `~/.fluxbox/menu`:

```
[submenu] (Teclado)
      [exec] (Por defecto) {setxkbmap us}
      [exec] (Español) {setxkbmap es}
[end]

```

#### Deshabilitar ahorro de energia

¿Reconoce ese problema cuando estas jugando o viendo algún vídeo y se pone la pantalla en negro? Felicidades, justo Xorg a detectado que no estas haciendo nada :). Si no necesitas los ejercicios de movimiento, puedes deshabilitarlo. Recuerda apagar el monitor si no vas a usarlo durante un tiempo.

Añade esto al principio de `~/.fluxbox/startup`:

```
xset s off -dpms &

```

## Recursos adicionales

*   [Pagina de Fluxbox](http://fluxbox.org/)
*   [Fluxbox Wiki](http://fluxbox-wiki.org/)
*   [Howtos de Fluxbox en español](http://fluxbox-wiki.org/index.php?title=Category:Espa%C3%83%C2%B1ol_/_Spanish_howtos)
*   [Manual de Fluxbox en la Wiki de Gentoo](http://wiki.gentoo.org/wiki/Fluxbox)
*   [Temas para Fluxbox](http://box-look.org/)
*   [Guía de estilo para Fluxbox (ingles)](/index.php/Fluxbox_Style_Guide "Fluxbox Style Guide")
*   [Guía de Fluxbox por Narada](https://bbs.archlinux.org/viewtopic.php?id=77729)