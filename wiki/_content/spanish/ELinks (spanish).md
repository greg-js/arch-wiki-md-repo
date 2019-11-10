**Estado de la traducción**
Este artículo es una traducción de [ELinks](/index.php/ELinks "ELinks"), revisada por última vez el **2019-11-04**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=ELinks&diff=0&oldid=587733) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[ELinks](http://elinks.or.cz/) es un navegador web avanzado y bien establecido de modo de texto rico en funciones (HTTP/FTP/...). ELinks puede representar tanto frames como tablas, es altamente personalizable y puede ampliarse mediante scripts de Lua o Guile. Cuenta con pestañas y algo de soporte para CSS.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
    *   [2.1 Navegación](#Navegación)
*   [3 Configuración](#Configuración)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Definir manejadores de URL](#Definir_manejadores_de_URL)
    *   [4.2 Utilización de Tor](#Utilización_de_Tor)
    *   [4.3 Pasar URL a órdenes externas](#Pasar_URL_a_órdenes_externas)
        *   [4.3.1 Guardar enlace al portapapeles X](#Guardar_enlace_al_portapapeles_X)
        *   [4.3.2 Pasar enlaces de YouTube a través de un reproductor externo](#Pasar_enlaces_de_YouTube_a_través_de_un_reproductor_externo)
*   [5 Solución de problemas](#Solución_de_problemas)
    *   [5.1 ELinks se congeló y no puede iniciarse sin que se congele nuevamente](#ELinks_se_congeló_y_no_puede_iniciarse_sin_que_se_congele_nuevamente)
*   [6 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [elinks](https://www.archlinux.org/packages/?name=elinks).

## Utilización

Vea [elinks(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/elinks.1).

### Navegación

Navegar por la web con un navegador de texto es más o menos lo mismo que un navegador gráfico, solo que sin «distracciones». Una vez que haya comenzado *elinks*, puede presionar `g` y escribir la página web que desea solicitar. Luego puede navegar por la página con las teclas de flecha para navegar por línea, la barra espaciadora para navegar por páginas o las teclas `j` y `k` para navegar por enlaces.

**Sugerencia:** para mantener la sesión en el terminal original, *elinks* puede ejecutarse en una [consola virtual](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") (alternable con `Alt+arrow`) o con un [multiplexor terminal](https://en.wikipedia.org/wiki/Terminal_multiplexer "wikipedia:Terminal multiplexer") como [tmux](/index.php/Tmux "Tmux").

## Configuración

ELinks proporciona dos menús, accesibles a través de ELinks, para personalizar opciones y combinaciones de teclas respectivamente.

Se recomienda utilizar estas herramientas en lugar de editar manualmente los archivos de configuración (que se colocan en `~/.elinks`) Es mucho más fácil y seguro de esta manera.

Por defecto, la tecla `o` abre el administrador de opciones y la tecla `k` el administrador de teclas.

## Consejos y trucos

### Definir manejadores de URL

ELinks es capaz de usar programas externos para diversas tareas.

Definir manejadores de URL a través del menú de opciones puede ser un poco confuso al principio, pero una vez que lo domine, le resultará fácil.

Para hacer esto, vaya al administrador de opciones y navegue hasta *MIME*. Todos los submenús tienen páginas **I**nfo para ayudarlo.

Este es uno de los pocos casos en los que podría ser más fácil editar el archivo conf.

Por ejemplo, para hacer que ELinks inicie automáticamente su visor de imágenes cuando haga clic en un archivo jpeg, puede añadir lo siguiente a su archivo `~/.elinks/elinks.conf`:

 `~/.elinks/elinks.conf` 
```
set mime.extension.jpg="image/jpeg"
set mime.extension.jpeg="image/jpeg"
set mime.extension.png="image/png"
set mime.extension.gif="image/gif"
set mime.extension.bmp="image/bmp"

set mime.handler.image_viewer.unix.ask = 1
set mime.handler.image_viewer.unix-xwin.ask = 0

set mime.handler.image_viewer.unix.block = 1
set mime.handler.image_viewer.unix-xwin.block = 0 

set mime.handler.image_viewer.unix.program = "*pictureviewer* %"
set mime.handler.image_viewer.unix-xwin.program = "*pictureviewer* %"

set mime.type.image.jpg = "image_viewer"
set mime.type.image.jpeg = "image_viewer"
set mime.type.image.png = "image_viewer"
set mime.type.image.gif = "image_viewer"
set mime.type.image.bmp = "image_viewer"
```

### Utilización de [Tor](/index.php/Tor "Tor")

ELinks no es compatible con SOCKS directamente. Las alternativas son invocar ELinks a través de`torify elinks`, o [instalar](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [privoxy](https://www.archlinux.org/packages/?name=privoxy) para reenviarlo al proxy SOCKS de Tor. Añada primero la siguiente línea a su archivo de configuración `/etc/privoxy/config`:

```
forward-socks5 / localhost:9050 .

```

[Reinicie](/index.php/Restart "Restart") `privoxy.service`, luego ingrese las siguientes líneas al archivo `~/.elinks/elinks.conf`:

```
set protocol.http.proxy.host = "127.0.0.1:8118"
set protocol.https.proxy.host = "127.0.0.1:8118"

```

**Nota:** lo anterior supone que *Tor* está usando el puerto **9050** y que *privoxy* está escuchando en el puerto **8118**

### Pasar URL a órdenes externas

Puede definir órdenes que ELinks pasará a la URL actual.

Para hacer esto, vaya al menú de opciones, navegue a **Document**, luego a **URI-passing**. Luego presione `a` para agregar un nuevo nombre de la orden. Luego navegue hasta el nuevo nombre de la orden y presione `e` para editar. Escriba el nombre de la orden, ingrese y guarde.

Asumiendo que la orden «tab-external-command» está asignada a **KEY**, cada vez que presione **KEY**, un menú que contiene sus órdenes aparecerá. Seleccione la que desee y ELinks pasará la URL actual a esa orden.

**Nota:** Elinks le permite definir sus propias asignaciones para navegar por este menú.

#### Guardar enlace al portapapeles X

```
echo -n %c | xclip -i 

```

#### Pasar enlaces de YouTube a través de un reproductor externo

Para enlaces estrictamente de YouTube, [mpv](https://www.archlinux.org/packages/?name=mpv) tiene soporte incorporado. Basta utilizar lo siguiente:

```
mpv %c 

```

Para un enfoque más general que pueda manejar muchos sitios «tube», necesitará [youtube-dl](https://www.archlinux.org/packages/?name=youtube-dl). Luego añada la siguiente orden:

```
youtube-dl -o - %c | mplayer -

```

## Solución de problemas

### ELinks se congeló y no puede iniciarse sin que se congele nuevamente

Por defecto, cada vez que ELinks se inicia, este se conecta a una instancia existente. Por lo tanto, si esa instancia se congela, todas las instancias actuales y futuras también se congelarán.

Puede evitar que ELinks se conecte a una instancia existente al iniciarlo, procediendo así:

```
$ elinks -no-connect

```

Si esto sucede mucho, puede considerar hacer de este su inicio predeterminado, creando un alias en su [intérprete de órdenes](https://en.wikipedia.org/wiki/es:Shell_(inform%C3%A1tica) "wikipedia:es:Shell (informática)"):

```
alias elinks="elinks -no-connect"

```

## Véase también

*   [Sitio web oficial](http://elinks.or.cz/)
*   [Howto: utilizar elinks como un profesional](http://kmandla.wordpress.com/2007/05/06/howto-use-elinks-like-a-pro/)