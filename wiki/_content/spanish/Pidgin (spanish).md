## Contents

*   [1 Preface](#Preface)
*   [2 Instalación](#Instalación)
*   [3 Corrector ortográfico](#Corrector_ortográfico)
*   [4 Corregir el sonido](#Corregir_el_sonido)
*   [5 Corregir el Error de Navegador](#Corregir_el_Error_de_Navegador)
*   [6 IRC](#IRC)
*   [7 Xfire](#Xfire)
*   [8 Privacy](#Privacy)
*   [9 Other Packages](#Other_Packages)
*   [10 Links externos](#Links_externos)

## Preface

**Pidgin** (anteriormente GAIM) es un cliente de mensajería instantanea para Linux que puede conectar a varias diferentes redes de mensajería, como Live Messenger, Yahoo, IRC, AIM, etc. Lo lindo acerca de pidgin es que puedes usar varias redes al mismo tiempo.

## Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [pidgin](https://www.archlinux.org/packages/?name=pidgin) disponible desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Variantes notables son:

*   **Pidgin Light** — Light Pidgin sin soporte de GStreamer, Tcl/Tk, XScreenSaver, video/audio.

	[http://pidgin.im/](http://pidgin.im/) || [pidgin-light](https://aur.archlinux.org/packages/pidgin-light/)

Puede que también desee instalar plugins extras de [pidgin-plugin-pack](https://www.archlinux.org/packages/?name=pidgin-plugin-pack).

## Corrector ortográfico

Aspell será bajado como una dependencia, pero para prevenir todo su texto de ser mostrado como incorrecto deberá instalar un diccionario aspell.

```
# pacman -S aspell-es

```

Para el diccionario en Español. Use <tt>pacman -Ss aspell</tt> para una lista de los lenguajes disponibles.

*Nota: El **seleccionador ortográfico**-plugin está incluido en el purple-plugin-pack (ver arriba). Le permte seleccionar entre múltiples idiomas.*

## Corregir el sonido

Si el sonido no funciona con la configuración automática: configure ALSA, entonces use 'Command' como método de reproducción con el siguiente comando

```
aplay %s

```

## Corregir el Error de Navegador

Si al clickear en un hipervínculo dentro de pidgin crea un mensaje de error acerca de intentar usar 'sensible-browser' para abrir un hipervínculo, intente editando ~/.purple/prefs.xml. Busque la línea referenciando 'sensible-browser', y cambiela a esto:

```
<pref name='command' type='path' value='firefox'/>

```

Este ejemplo asume que usa firefox.

## IRC

Por supuesto quiere usar pidgin para que también sea su cliente de IRC y preguntar/ responder preguntas en el IRC de Arch. Así es como se establece el IRC para pidgin.

Ir a Cuentas -> Gestionar Cuentas -> Añadir -> Llenar/seleccionar las siguientes opciones:

```
        #Protocolo: IRC 
 Nombre de usuario: <tu nombre de usuario>

```

Y cierre la ventana

Ahora vaya a Amigos -> Mensae instantáneo nuevo ( o presione ctrl + m) escriba 'freenode.net' en el cuadro de texto y <nombre de usuario>@irc.freenode.net -> luego toque ok Ahora escriba:

```
# /join #archlinux (o simplemente cualquier otro canal que quiera)

```

Ahora está en el canal de IRC de Arch Linux y ahora registremos su apodo, tipee:

```
#/msg nickserv register <contraseña> <dirección de email>

```

Ahora recibirá un correo electrónico en su bandeja de entrada, ejecute el comandoque está en el correo y será registrado. Para cualquier ayuda tipee:

```
#/msg nickserv help
 /msg nickserv help <comando>

```

El último paso agregará su canal a sus amigos. Vaya a Amigos -> Añadir un chat -> escriba el canal correcto en el campo de texto llamado sala (#archlinux).

## Xfire

Pidgin tiene soporte Xfire, para obtener este soporte instale este paquete de AUR:

```
#pidgin-gfire 

```

Ahora simplemente agregue una cuenta y seleccione el protocolo xfire y llene su nombre de usuario + contraseña

## Privacy

Pidgin tiene algunas reglas de privacidad, así todo el mundo no pueda hablarle sino sólo sus amigos o personas seleccionadas de una lista. Simplemente vaya a:

```
#Herramientas -> Privacidad

```

## Other Packages

Arch (Repositorio Comunitario) tiene otros paquetes relacionados a Pidgin. Estos están listados aquí (incompletamente, haga una búsqueda en AUR)

*   pidgin-libnotify - Soporte libnotify, para notificaciones consistentes con el theme
*   pidgin-facebookchat - Para usar el chat de facebook
*   pidgin-guifications - Popup de notificaciones con el estilo "Toaster"
*   microblog-purple - Agregado de libpurple para soportar servicios de microblog como Twitter

## Links externos

*   [Página de inicio de Pidgin](http://pidgin.im)