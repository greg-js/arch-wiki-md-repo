Desde el sitio web awesome:

"*[awesome](http://awesome.naquadah.org/) es altamente configurable y es la próxima generación para administradores de ventanas para el X. Es muy rápido, extensible y está bajo la licencia GNU GPLv2.*

Esta pensado principalmente para usuarios con experiencia, desarrolladores y personas que lidian cada día con tareas computacionales y que desean un control detallado de su entorno gráfico.*"*

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Usando awesome](#Usando_awesome)
    *   [2.1 Iniciando Awesome sin un Gestor de inicio](#Iniciando_Awesome_sin_un_Gestor_de_inicio)
    *   [2.2 Iniciando Awesome con un Gestor de Inicio](#Iniciando_Awesome_con_un_Gestor_de_Inicio)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Creando el archivo de configuración](#Creando_el_archivo_de_configuraci.C3.B3n)
    *   [3.2 Mas recursos de configuración](#Mas_recursos_de_configuraci.C3.B3n)
    *   [3.3 Depurando rc.lua usando Xephyr](#Depurando_rc.lua_usando_Xephyr)
*   [4 Temas](#Temas)
    *   [4.1 Creación de su fondo de escritorio](#Creaci.C3.B3n_de_su_fondo_de_escritorio)
    *   [4.2 Imagen de Fondo Aleatoria](#Imagen_de_Fondo_Aleatoria)
*   [5 Consejos & Trucos](#Consejos_.26_Trucos)
    *   [5.1 Expose efecto como compiz](#Expose_efecto_como_compiz)
    *   [5.2 Esconder / mostrar wibox en awesome 3](#Esconder_.2F_mostrar_wibox_en_awesome_3)
    *   [5.3 Activar printscreens](#Activar_printscreens)
    *   [5.4 Etiquetado dinámico utilizando Eminent](#Etiquetado_din.C3.A1mico_utilizando_Eminent)
    *   [5.5 Invasores del Espacio](#Invasores_del_Espacio)
    *   [5.6 Vistosa notificación emergente](#Vistosa_notificaci.C3.B3n_emergente)
    *   [5.7 Ventanas Emergentes en los Menus](#Ventanas_Emergentes_en_los_Menus)
    *   [5.8 Mas Widgets en awesome](#Mas_Widgets_en_awesome)
    *   [5.9 Transparencia](#Transparencia)
    *   [5.10 Ejecutar automáticamente programas](#Ejecutar_autom.C3.A1ticamente_programas)
    *   [5.11 Pasando contenido a un widget con awesome-client](#Pasando_contenido_a_un_widget_con_awesome-client)
*   [6 Solución de Problemas](#Soluci.C3.B3n_de_Problemas)
    *   [6.1 Tecla Mod4](#Tecla_Mod4)
        *   [6.1.1 Tecla Mod4 vs. usuario de IBM ThinkPad](#Tecla_Mod4_vs._usuario_de_IBM_ThinkPad)
    *   [6.2 Disminución de Memoria en Cairo](#Disminuci.C3.B3n_de_Memoria_en_Cairo)
*   [7 Enlaces Externos](#Enlaces_Externos)

## Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [awesome](https://www.archlinux.org/packages/?name=awesome) de los repositorios oficiales. La versión en desarrollo via Git está disponible en AUR, instalando [awesome-git](https://aur.archlinux.org/packages/awesome-git/). Nótese que esta versión no es estable y su sintaxis de configuración puede diferir con la versión estable.

## Usando awesome

### Iniciando Awesome sin un Gestor de inicio

Para ejecutar awesome sin un manejador de sesión, sólo agregue `exec awesome` a el script de inicio de su elección (ej. `~/.xinitrc`.)

Véase [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") para mas información, como por ejemplo mantener la sesión logind (y/o consolekit).

Sin embargo, se puede también iniciar awesome como usuario preestablecido sin ningún manejador de sesión y sin una contraseña, después que edite ~/.xinitrc y /etc/inittab adecuadamente. Véase [arrancar X al iniciar sesión](/index.php/Start_X_at_login_(Espa%C3%B1ol) "Start X at login (Español)").

### Iniciando Awesome con un Gestor de Inicio

Para iniciar awesome desde un manejador de sesión, vea [este artículo](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)").

## Configuración

Awesome incluye una buena configuración inicial, pero temprano o tarde tendrá que cambiar algo. El archivo de configuración basado en lua se encuentra en `~/.config/awesome/rc.lua`.

### Creando el archivo de configuración

Primero, crea el siguiente directorio donde se alojará el archivo de configuración:

```
$ mkdir -p ~/.config/awesome/

```

Siempre que sea compilado, awesome intentará utilizar cualquier configuración personalizada que se encuentre en ~/.config/awesome/rc.lua. Este archivo no se crea por defecto, por lo tanto, es necesario copiar el archivo primero:

```
$ cp /etc/xdg/awesome/rc.lua ~/.config/awesome/rc.lua

```

La sintaxis para configurar el archivo usualmente cambia cuando se realiza una actualización de awesome. Por lo tanto, recuerde repetir el comando de arriba cuando obtenga un comportamiento extraño o quiera modificar la configuración.

Para mayor información sobre la configuración de awesome, observe [configuración de awesome en el wiki](http://awesome.naquadah.org/wiki/Awesome_3_configuration)

### Mas recursos de configuración

**Nota:** La sintaxis de awesome cambia regularmente, por lo tanto, probablemente tendrán que modificar cualquier archivo que se descargue.

Varios buenos ejemplos de rc.lua son los siguientes:

*   [http://git.sysphere.org/awesome-configs/tree/](http://git.sysphere.org/awesome-configs/tree/) - Awesome 3.4 configuración por Adrian C. (anrxc)
*   [http://pastebin.com/f6e4b064e](http://pastebin.com/f6e4b064e) - Darthlukan's awesome 3.4 configuración.
*   [http://www.calmar.ws/dotfiles/dotfiledir/dot_awesomerc.lua](http://www.calmar.ws/dotfiles/dotfiledir/dot_awesomerc.lua)
*   [http://github.com/wolgri/wolgri.config/tree/master/.config/awesome/rc.lua](http://github.com/wolgri/wolgri.config/tree/master/.config/awesome/rc.lua)
*   [http://oxmoz.no-ip.org/awesome/rc.lua](http://oxmoz.no-ip.org/awesome/rc.lua)
*   [http://www.ugolnik.info/downloads/awesome/rc.lua](http://www.ugolnik.info/downloads/awesome/rc.lua) (screen) - Awesome 3 con una pequeña barra de titulo y barra de estado.
*   [http://github.com/bash/dotfiles/blob/master/.config/awesome/rc.lua](http://github.com/bash/dotfiles/blob/master/.config/awesome/rc.lua)
*   [http://github.com/nblock/config/blob/master/.config/awesome/rc.lua](http://github.com/nblock/config/blob/master/.config/awesome/rc.lua)
*   User Configuration Files [http://awesome.naquadah.org/wiki/User_Configuration_Files](http://awesome.naquadah.org/wiki/User_Configuration_Files)

### Depurando rc.lua usando Xephyr

Esta es la forma que prefiero depurar rc.lua, sin la necesidad de cerrar mi escritorio actual. Primero copio mi rc.lua en un nuevo archivo, rc.lua.new, y lo modifico si es necesario. Luego, ejecuto la nueva instancia de awesome en Xephyr (permitiendo ejecutar un X adjunto a otro cliente X), reemplazando rc.lua.new como el archivo de configuración, de esta forma:

```
$ Xephyr -ac -br -noreset -screen 1152x720 :1 &
$ DISPLAY=:1.0 awesome -c ~/.config/awesome/rc.lua.new

```

La gran ventaja de esta enfoque es que si se rompe el rc.lua.new, no se necesita cerrar el escritorio awesome actual (y probablemente dañe todas las aplicaciones X, perdiendo las cosas que no se salvaron...). Una vez que este satisfecho con los nuevos cambios, mover el rc.lua.new a rc.lua y reiniciar awesome. Y puede estar seguro de que el trabajo de configuración y reinicio de la nueva configuración no dañe las cosas.

Actualmente [awmtt](https://aur.archlinux.org/packages/awmtt/) provee la funcionalidad antes descrita.

## Temas

Beautiful es la biblioteca de lua que le permite cambiar de tema en awesome usando un archivo externo, de manera que es muy fácil cambiar dinamicamente todo los colores de awesome y el fondo de escritorio sin la necesidad de cambiar el archivo rc.lua.

El tema por defecto está en /usr/share/awesome/themes/default. Cópielo ~/.config/awesome/themes/default y cambie la ruta_del_tema en rc.lua.

Para más detalles [aquí](http://awesome.naquadah.org/wiki/Beautiful)

Algunos ejemplos [temas](http://awesome.naquadah.org/wiki/Beautiful_themes)

### Creación de su fondo de escritorio

Beautiful puede manejar su fondo de escritorio, de manera que no tenga que agregarlo en su archivo .xinitrc o .xsession. Este le permite tener un fondo de escritorio especifico por cada tema. Si observa el tema por defecto observará una entrada llamada wallpaper_cmd, este comando es ejecutado cuando el beautiful.init("ruta_archivo_del_tema") este corriendo. Usted puede colocar allí su propio comando o eliminar/comentar la entrada si no quiere que Beautiful interfiera con el fondo de escritorio.

Para una instancia, si usa awsetbg para establecer su fondo de escritorio, usted puede escribir:

wallpaper_cmd = { "awsetbg -f .config/awesome/themes/awesome-wallpaper.png" }

### Imagen de Fondo Aleatoria

Para rotar el fondo de escritorio aleatoriamente, necesita comentar la línea wallpaper_cmd, y agregar un script en su .xinitrc con el código siguiente:

```
while true;
do
  awsetbg -r <path/to/the/directory/of/your/wallpapers>
  sleep 15m
done &

```

## Consejos & Trucos

Siéntete libre de agregar cualquier consejo o truco que te gustaría compartir con otros usuarios de awesome.

### Expose efecto como compiz

Revelar el resultado de todos sus clientes abiertos; clic-izquierdo en un cliente abrirá una ventana emergente con la primera etiqueta visible que le permite obtener el foco del cliente. Además, la tecla Enter desplegara una ventana emergente que se enfocará en el cliente actual, y la tecla Escape es para abortar.

[http://awesome.naquadah.org/wiki/Revelation](http://awesome.naquadah.org/wiki/Revelation)

### Esconder / mostrar wibox en awesome 3

La tecla ModKey-b le permite esconder/mostrar la barra de estado en una pantalla activa (por defecto en awesome 2.3), agregue a su *clientkeys* en rc.lua:

```
awful.key({ modkey }, "b", function ()
    mywibox[mouse.screen].visible = not mywibox[mouse.screen].visible
end),

```

### Activar printscreens

Para habilitar prinscreens en awesome desde el tecla PrtScr necesita tener un programa de captura de pantalla. Scrot es la utilidad más fácil de utilizar para este propósito y esta disponible en los repositorios de Arch.

Sólo escriba:

```
# pacman -S scrot

```

e instale las dependencias opcionales si cree que las necesitará.

Lo siguiente que necesitamos obtener es el nombre para el tecla PrtScr, en muchos casos se llama "Print" pero no se puede estar seguro.

Ejecute:

```
# xev

```

Y presione la tecla PrtScr, la salida debería ser algo como esto:

```
 KeyPress event ....
     root 0x25c, subw 0x0, ...
     state 0x0, keycode 107 (keysym 0xff61, **Print**), same_screen YES,
     ....

```

En mi caso como observan, el nombre de la tecla es Print.

Ahora la configuración de awesome!

En algún lado de su conjunto de teclas globales (no importa donde) escriba:

Lua código:

```
 awful.key({ }, "Print", function () awful.util.spawn("scrot -e 'mv $f ~/screenshots/ 2>/dev/null'") end),

```

Un buen lugar para colocar esto es debajo del keyhook para el spawning un terminal. Para encontrar esta línea busque por: awful.util.spawn(terminal) en su editor de texto favorito.

También, esta función guarda el screenshots dentro de ~/screenshots/, editelo para ajustarlo a sus necesidades.

### Etiquetado dinámico utilizando Eminent

TODO... [[1]](http://awesome.naquadah.org/wiki/index.php?title=Eminent)

Observación: Eminent es un poco antiguo y desactualizado. Nosotros tenemos una nueva biblioteca llamada: Shifty. No ha sido incluida aun, pero es bastate prometedora. Yo recomiendo esperar por y después escribir su respectiva sección. [Shifty Video (.ogv)](http://garoth.com/awesome/shifty.ogv)

Observación2: Hay actualmente otra implementación para esta funcionalidad. Estoy esperando que se integre con Shifty, y estoy dirigiendo a los desarrolladores en esa dirección.

### Invasores del Espacio

Invasores del Espacio es un demo que muestra las posibilidades de awesome Lua API. [[2]](http://awesome.naquadah.org/wiki/Space_Invaders)

Por favor, tenga en cuenta que no esta incluido en los paquetes de Awesome desde la versión 3.4-rc1.

### Vistosa notificación emergente

TODO [[3]](http://awesome.naquadah.org/wiki/index.php?title=Naughty)

### Ventanas Emergentes en los Menus

Hay un solo menu por defecto en awesome3, y personalizarlo es muy fácil ahora. Sin embargo, si esta utilizando la versión 2.x de awesome, tiene que ver *[awful.menu](http://awesome.naquadah.org/wiki/index.php?title=Awful.menu)*.

Un ejemplo para awesome3:

```
myawesomemenu = {
   { "lock", "xscreensaver-command -activate" },
   { "manual", terminal .. " -e man awesome" },
   { "edit config", editor_cmd .. " " .. awful.util.getdir("config") .. "/rc.lua" },
   { "restart", awesome.restart },
   { "quit", awesome.quit }
}

mycommons = {
   { "pidgin", "pidgin" },
   { "OpenOffice", "soffice-dev" },
   { "Graphic", "gimp" }
}

mymainmenu = awful.menu.new({ items = { 
                                        { "terminal", terminal },
                                        { "icecat", "icecat" },
                                        { "Editor", "gvim" },
                                        { "File Manager", "pcmanfm" },
                                        { "VirtualBox", "VirtualBox" },
                                        { "Common App", mycommons, beautiful.awesome_icon },
                                        { "awesome", myawesomemenu, beautiful.awesome_icon }
                                       }
                             })

```

### Mas Widgets en awesome

*Los Widgets en awesome son objetos que se pueden agregar a cualquier contenedor-widget (barra de estado y barra de títulos), ellos pueden proveer de varias informaciones sobre el sistema, y son muy útiles para tener acceso a esa información desde la manejador de ventanas. Los Widgets son fáciles de utilizar y comúnmente proporcionan mucha flexibilidad.* -- Fuente [Awesome Wiki: Widgets](http://awesome.naquadah.org/wiki/Widgets_in_awesome).

Existe una biblioteca para widgets mayormente utilizada llamada **Wicked** (compatible con las versiones **superiores a 3.4** de awesome), que proveen de muchos widgets, como MPD widget, uso del CPU, uso de la memoria, etc. Para más detalles ver [la página de Wicked](http://awesome.naquadah.org/wiki/index.php?title=Wicked).

Un reemplazo para Wicked en awesome v3.4 es **[Vicious](http://awesome.naquadah.org/wiki/Vicious)**, **[Obvious](http://awesome.naquadah.org/wiki/Obvious)** y **[Bashets](http://awesome.naquadah.org/wiki/Bashets)**. Si elige vicious, se le recomienda ver [vicious documentación](http://git.sysphere.org/vicious/tree/README).

### Transparencia

Awesome tiene soporte para transparencias (2D) con xcompmgr. Observe que probablemente querrá utilizar la versión git de xcompmgr, la cual es [disponible en AUR](https://aur.archlinux.org/packages.php?ID=16554).

Agregue esto a su ~/.xinitrc:

```
exec xcompmgr &

```

Vea *man xcompmgr* o [xcompmgr](/index.php/Xcompmgr "Xcompmgr") para más opciones.

En awesome 3.4, la transparencia de la ventana puede ser establecida dinamicamente usandos señales. Por ejemplo, su rc.lua podría contener lo siguiente:

```
client.add_signal("focus", function(c)
                              c.border_color = beautiful.border_focus
                              c.opacity = 1
                           end)
client.add_signal("unfocus", function(c)
                                c.border_color = beautiful.border_normal
                                c.opacity = 0.7
                             end)

```

Observe que si no esta usando conky, necesita establecerlo para crear su propia ventana en vez de usar la del escritorio. Para hacer esto, edite ~/.conkyrc para que contenga:

```
own_window yes
own_window_transparent yes
own_window_type desktop

```

De lo contrario se comportará extrañamente, que todas las ventanas tengan toda la transparencia. Observe también que desde que conky va a crear transparencias en las ventanas de su escritorio, toda acción definida en el archivo de awesome rc.lua no funcionará para el escritorio actual.

A partir de Awesome 3.1, está incorporada la pseudo-transparencia para los wiboxes. Para habilitarlo, agregue dos dígitos hexadecimales a los colores en el archivo del tema (~/.config/awesome/themes/default, el cual es usualmente una copia de /usr/share/awesome/themes/default), como se muestra abajo:

```
bg_normal = #000000AA

```

donde "AA" es el valor de transparencia.

### Ejecutar automáticamente programas

Solo agregue el siguiente código en el archivo rc.lua, y reemplace las aplicaciones en la sección autorunsApps con cualquier cosa que le guste. Por ejemplo:

```
-- Autorun programs
autorun = true
autorunApps = 
{ 
   "swiftfox",
   "mutt",
   "consonance",
   "linux-fetion",
   "weechat-curses",
}
if autorun then
   for app = 1, #autorunApps do
       awful.util.spawn(autorunApps[app])
   end
end

```

or like this:

```
os.execute("mutt &"),
os.execute("weechat-curses &"),

```

Para ejecutar una aplicación solo una vez, e.g. para reiniciar awesome, utilice esta función (tomado de [awesome wiki](http://awesome.naquadah.org/wiki/Autostart)):

```
function run_once(prg)
	if not prg then
		do return nil end
	end
	awful.util.spawn_with_shell("pgrep -u $USER -x " .. prg .. " || (" .. prg .. ")")
end

```

```
-- AUTORUN APPS!
run_once("parcellite")

```

### Pasando contenido a un widget con awesome-client

Fácilmente se puede enviar texto a un widget de awesome. Solo cree un nuevo widget:

```
 mywidget = widget({ type = "textbox", name = "mywidget" })
 mywidget.text = "initial text"

```

Para actualizar el texto desde una fuente externa, use awesome-client:

```

 echo -e 'mywidget.text = "new text"' | awesome-client

```

No olvide agregar el widget a su wibox.

## Solución de Problemas

### Tecla Mod4

La tecla Mod4 es por defecto la **tecla Window**. Si no está funcional por defecto, por alguna razón, usted puede verificar el código de la tecla de su tecla Mod4 con:

```
$ xev

```

Debería ser 115 como mínimo. Luego agréguela a su ~/.xinitrc

```
xmodmap -e "keycode 115 = Super_L" -e "add mod4 = Super_L"
exec awesome

```

#### Tecla Mod4 vs. usuario de IBM ThinkPad

IBM ThinkPads no vienen equipadas con la tecla Window (sin embargo Lenovo cambio esta tradición para sus ThinkPads). Como se ha escrito, la tecla Alt no está en uso para las combinaciones por defecto en rc.lua (vea el wiki de Awesome para la lista de comandos), pero puede utilizarse como reemplazo para la teclas Super/Mod 4/Win. Para hacer esto, edite su rc.lua y sustituya:

```
modkey = "Mod4"

```

by:

```
modkey = "Mod1"

```

Observación: Awesome tiene varias comandos que le permiten utilizar la tecla Mod4 en combinación con una simple letra. Cambiando Mod4 a Mod1/Alt podría causar choques para algunas combinaciones de teclas. La menor cantidad de instancias donde esto ocurre pueden ser cambiada en el archivo rc.lua.

Si usted no le agrada cambiar los estándares de awesome, debe remapear una tecla. A veces la tecla de caps lock es inútil (para mi), por lo tanto, agrego lo siguiente al contenido de ~/.Xmodmap

```
clear lock 
add mod4 = Caps_Lock

```

y [(re)cargo](/index.php/Xmodmap#Custom_table "Xmodmap") el archivo.

Se debe cambiar la tecla caps lock a la tecla mod4 y funciona bastante bien con el estándar de configuración de awesome. Además, si es necesario, la tecla mod4 es proporcionada por otros programas también.

### Disminución de Memoria en Cairo

Si está experimentando [disminución de memoria](http://awesome.naquadah.org/bugs/index.php?do=details&task_id=396) entonces pruebe [cairo-git](https://aur.archlinux.org/packages/cairo-git/) en AUR. [Tema en el Foro](https://bbs.archlinux.org/viewtopic.php?pid=462021).

**Actualización**: La versión actual de Cairo 1.8.6 se puede utilizar sin problemas, parece que la versión git soluciona el error.

## Enlaces Externos

*   [http://awesome.naquadah.org/wiki/FAQ](http://awesome.naquadah.org/wiki/FAQ) - FAQ
*   [http://www.lua.org/pil/](http://www.lua.org/pil/) - Programando en Lua (primera edición)
*   [http://awesome.naquadah.org/](http://awesome.naquadah.org/) - Página oficial de Awesome
*   [http://awesome.naquadah.org/wiki/Main_Page](http://awesome.naquadah.org/wiki/Main_Page) - El wiki de Awesome
*   [http://www.penguinsightings.org/desktop/awesome/](http://www.penguinsightings.org/desktop/awesome/) - Un Análisis