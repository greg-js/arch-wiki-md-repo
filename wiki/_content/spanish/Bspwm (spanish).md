Artículos relacionados

*   [bspwm/Example configurations](/index.php/Bspwm/Example_configurations "Bspwm/Example configurations")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers")

*bspwm* es un [gestor de ventanas tipo mosaico](https://es.wikipedia.org/wiki/Gestor_de_ventanas#Gestores_de_ventanas_de_mosaico) que organiza las ventanas en un [árbol binario completo](https://es.wikipedia.org/wiki/%C3%81rbol_binario). Tiene soporte para [EWMH](http://standards.freedesktop.org/wm-spec/wm-spec-1.3.html) y múltiples monitores, y se configura y controla a través de mensajes.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Para múltiples monitores](#Para_múltiples_monitores)
    *   [2.2 Reglas](#Reglas)
    *   [2.3 Paneles](#Paneles)
    *   [2.4 Scratchpad](#Scratchpad)
    *   [2.5 *bspwmrc* como script](#bspwmrc_como_script)
*   [3 Solución de problemas](#Solución_de_problemas)
    *   [3.1 Aparece una pantalla negra y las combinaciones de teclas no funcionan](#Aparece_una_pantalla_negra_y_las_combinaciones_de_teclas_no_funcionan)
    *   [3.2 Una aplicación no ocupa todo el espacio de su ventana](#Una_aplicación_no_ocupa_todo_el_espacio_de_su_ventana)
    *   [3.3 Problemas con aplicaciones Java](#Problemas_con_aplicaciones_Java)
*   [4 Véase también](#Véase_también)

## Instalación

Instale [bspwm](https://www.archlinux.org/packages/?name=bspwm) y [sxhkd](https://www.archlinux.org/packages/?name=sxhkd), o las versiones en desarrollo: [bspwm-git](https://aur.archlinux.org/packages/bspwm-git/) y [sxhkd-git](https://aur.archlinux.org/packages/sxhkd-git/). **sxhkd** es un simple servicio de combinaciones de teclas usables dentro de [X](https://es.wikipedia.org/wiki/Sistema_de_ventanas_X), requerido para comunicarse con bspwm y lanzar aplicaciones a elección.

Para comenzar bspwm al iniciar sesión, añada lo siguiente a `~/.xinitrc` o `~/.xprofile` (dependiendo de [cómo ha escogido iniciar X](/index.php/Xorg_(Espa%C3%B1ol)#Ejecuci.C3.B3n "Xorg (Español)")):

```
sxhkd &
exec bspwm

```

## Configuración

Puede encontrar ejemplos de configuración en `/usr/share/doc/bspwm/examples/` y en [GitHub](https://github.com/baskerville/bspwm/blob/master/examples/).

Cree los directorios `~/.config/bspwm/` y `~/.config/sxhkd/`, y luego copie `/usr/share/doc/bspwm/examples/bspwmrc` a `~/.config/bspwm/` y `/usr/share/doc/bspwm/examples/sxhkdrc` a `~/.config/sxhkd/`. En estos dos archivos se definirán las configuraciones y las combinaciones de teclas, respectivamente. Por último, haga que el archivo bspwmrc sea ejecutable, con `chmod +x ~/.config/bspwm/bspwmrc`.

**Note:** Asegúrese de que su variable de entorno $XDG_CONFIG_HOME esté indicada en el sistema, o su bspwmrc no será tomado en cuenta. Para indicarla, escriba `XDG_CONFIG_HOME="$HOME/.config"` y `export XDG_CONFIG_HOME` en ~/.profile, en líneas aparte.

Las opciones de configuración para cada archivo se encuentran enlistadas y descritas en [bspwm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bspwm.1) y [sxhkd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sxhkd.1).

#### Para múltiples monitores

El ejemplo de bspwmrc configura diez escritorios para un sólo monitor:

```
bspc monitor -d I II III IV V VI VII VIII IX X

```

Esa línea tendría que ser dividida para cada monitor:

```
bspc monitor DVI-I-1 -d I II III IV
bspc monitor DVI-I-2 -d V VI VII
bspc monitor DP-1 -d VIII IX X

```

Para averiguar el nombre de sus monitores, puede escribir `xrandr -q` o `bspc query -M` en su terminal.

En el ejemplo anterior, el número total de escritorios fue limitado a diez. Esto es para que cada escritorio pueda ser invocado con 'super + {1-9,0}', de acuerdo a al ejemplo de sxhkdrc. La tecla de inicio de Windows es denominada universalmente como 'super', y es la más utilizada en el ejemplo de sxhkdrc.

### Reglas

Hay dos formas de definir reglas para el comportamiento de ventanas (a partir de [cd97a32](https://github.com/baskerville/bspwm/commit/cd97a3290aa8d36346deb706fa307f5f8faa2f34)).

La primera consiste en usar el comando de regla *integrado* (bspc), como se muestra en el ejemplo de bspwmrc:

```
bspc rule -a Gimp desktop=^8 follow=on state=floating
bspc rule -a Chromium desktop=^2
bspc rule -a mplayer2 state=floating
bspc rule -a Kupfer.py focus=on
bspc rule -a Screenkey manage=off

```

La segunda opción consiste en usar un comando de regla *externo*. Esto es más complejo, pero permite diseñar reglas más específicas. Vea [estos ejemplos](https://github.com/baskerville/bspwm/tree/master/examples/external_rules).

Si alguna ventana desobedece a bspwmrc, asegúrese de que la regla correspondiente invoque al programa con el sinónimo ejecutable de su nombre oficial. Puede averiguar dicho sinónimo, ejecutando: `xprop | grep WM_CLASS` (requiere tener [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) instalado).

### Paneles

Aparte de los ejemplos de bspwmrc y de sxhkdrc, en la carpeta *examples* se encuentra un ejemplo para integrar un panel [lemonbar](https://aur.archlinux.org/packages/lemonbar/). Para aprender más acerca de su uso, visite nuestra entrada de [lemonbar](/index.php/Lemonbar "Lemonbar"). Revise las dependencias opcionales que pueda necesitar para su configuración deseada.

El panel se ejecuta incluyendo la línea `panel &` en su bspwmrc.

Para visualizar información del sistema en la barra de estado, se puede usar diversas [llamadas al sistema](https://es.wikipedia.org/wiki/Llamada_al_sistema). El siguiente ejemplo le enseñará a conseguir que su panel muestre el estado del volumen de audio:

```
panel_volume()
{
        volStatus=$(amixer get Master | tail -n 1 | cut -d '[' -f 4 | sed 's/].*//g')
        volLevel=$(amixer get Master | tail -n 1 | cut -d '[' -f 2 | sed 's/%.*//g')
        # ¿está alsa en mute o no?:
        if [ "$volStatus" == "on" ]
        then
                echo "%{Fyellowgreen} $volLevel %{F-}"
        else
                # si está en mute, que la fuente sea roja:
                echo "%{Findianred} $volLevel %{F-}"
        fi
}
```

Luego, verificaremos que es invocado y redirigido a `$PANEL_FIFO`:

```
while true; do
echo "S" "$(panel_volume) $(panel_clock) > "$PANEL_FIFO"
        sleep 1s
done &

```

### Scratchpad

Se puede emular un *scratchpad* (un terminal invocado en cualquier lugar del escritorio para ejecutar un comando específico), añadiendo una combinación de teclas para su invocación con [xdotool](https://www.archlinux.org/packages/?name=xdotool):

```
xdotool search --onlyvisible --classname scratchpad windowunmap \
|| xdotool search --classname scratchpad windowmap \
|| st -c scratchpad -g 1000x400+460 &

```

y añadiendo esta regla:

```
bspc rule -a scratchpad sticky=on state=floating

```

Véase [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1338582#p1338582) y [[2]](http://yuri-rage.github.io/geekery/2015/01/26/bleeding-edge-bspwm/).

Para un scratchpad que prescinda de reglas pre-definidas, véase: [[3]](https://www.reddit.com/r/bspwm/comments/3xnwdf/i3_like_scratch_for_any_window_possible/cy6i585)

Para un scratchpad con más sofisticación de comportamiento, instale [tdrop-git](https://aur.archlinux.org/packages/tdrop-git/).

### *bspwmrc* como script

Dado que `bspwmrc` es un [script](http://ovtoaster.com/introduccion-los-scripts-en-linux/) (guión de comandos), usted puede hacer con él cosas como éstas:

Configuraciones diferentes para cada monitor:

```
#! /bin/sh

 if [[ $(hostname) == 'myhost' ]]; then
     bspc monitor eDP1 -d I II III IV V VI VII VIII IX X
 elif [[ $(hostname) == 'otherhost' ]]; then
     bspc monitor VGA-0 -d I II III IV V
     bspc monitor VGA-1 -d VI VII VIII IX X
 elif [[ $(hostname) == 'yetanotherhost' ]]; then
     bspc monitor DVI-I-3 -d VI VII VIII IX X
     bspc monitor DVI-I-2 -d I II III IV V
 fi

```

Que todas las ventanas sean flotantes:

```
#!/bin/bash

 # change the desktop number here
 FLOATING_DESKTOP_ID=$(bspc query -D -d '^3')

 bspc subscribe node_manage | while read -a msg ; do
    desk_id=${msg[2]}
    wid=${msg[3]}
    [ "$FLOATING_DESKTOP_ID" = "$desk_id" ] && bspc node "$wid" -t floating
 done

```

([fuente](https://github.com/baskerville/bspwm/issues/428#issuecomment-199985423))

## Solución de problemas

### Aparece una pantalla negra y las combinaciones de teclas no funcionan

Primero que todo, una pantalla negra significa que bspwm está funcionando. Respecto a las combinaciones de teclas, verifique que usted haya seguido los pasos correctamente. Si lo había hecho así, entonces incluya la ejecución de un emulador de terminal en `~/.xinitrc`:

```
sxhkd &
[su terminal de preferencia] &
exec bspwm

```

Habiendo iniciado X con `startx`, usted tendrá su emulador de terminal dispuesto. Ahora, tipee `pidof sxhkd`. Si el comando no devuelve un número, inténtelo de nuevo asociando sxhkd con sxhkdrc explícitamente, ejecutando `pidof sxhkd -c ~/.config/sxhkd/sxhkdrc`.

También puede intentar cambiando la tecla 'super' por 'Alt', en sxhkdrc.

### Una aplicación no ocupa todo el espacio de su ventana

Esto puede pasar si está usando aplicaciones GTK3, y especialmente en el caso de los cuadros de diálogo. Si se trata de eso, añada lo siguiente a ~/.config/gtk-3.0/gtk.css:

```
.window-frame, .window-frame:backdrop {
  box-shadow: 0 0 0 black;
  border-style: none;
  margin: 0;
  border-radius: 0;
}

.titlebar {
  border-radius: 0;
}

```

(fuente: [foro de bspwm](https://bbs.archlinux.org/viewtopic.php?pid=1404973#p1404973))

### Problemas con aplicaciones Java

Si, por ejemplo, las aplicaciones Java no pueden cambiar de tamaño o sus menús se cierran espontáneamente, véase [Java#Gray window, applications not resizing with WM, menus immediately closing](/index.php/Java#Gray_window,_applications_not_resizing_with_WM,_menus_immediately_closing "Java").

## Véase también

*   Mailing List: bspwm en librelist.com.
*   `#bspwm` - canal IRC en irc.freenode.net
*   [https://bbs.archlinux.org/viewtopic.php?id=149444](https://bbs.archlinux.org/viewtopic.php?id=149444) - Tema en el foro Arch BBS
*   [https://github.com/baskerville/bspwm](https://github.com/baskerville/bspwm) - GitHub
*   [https://github.com/windelicato/dotfiles/wiki/bspwm-for-dummies](https://github.com/windelicato/dotfiles/wiki/bspwm-for-dummies) - Un "bspwm para tontos"