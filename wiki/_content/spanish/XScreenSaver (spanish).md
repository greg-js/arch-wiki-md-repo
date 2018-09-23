## Contents

*   [1 Configuración](#Configuraci.C3.B3n)
*   [2 Arrancando Xscreensaver](#Arrancando_Xscreensaver)
    *   [2.1 Ejemplo de ~/.xinitrc](#Ejemplo_de_.7E.2F.xinitrc)
*   [3 bloquear pantalla](#bloquear_pantalla)

## Configuración

## Arrancando Xscreensaver

En algunas máquinas, el simple hecho de instalar el programa xscreensaver no es suficiente para que funcione correctamente. El programa de xscreensaver tiene que ser arrancado, tarea de la que se ocupa habitualmente el gestor de escritorio.

Sin embargo, algunos gestores no lo hacen (p.ej.: IceWM).

Para arrancar manualmente el programa xscreensaver, sólo tiene que teclear

```
<tt>xscreensaver</tt> 

```

en un terminal.

O bien, para arrancarlo automáticamente cada vez que entre al entorno X11, escriba lo siguiente en su archivo '~/.xinitrc' por encima de la línea que especifica qué gestor se va a cargar.

```
<tt>xscreensaver -no-splash &</tt>

```

### Ejemplo de ~/.xinitrc

```
#!/bin/sh

```

```
#
# ~/.xinitrc
#
# Ejecutado mediante startx (lance su gestor de ventanas a partir de aquí)
#

xscreensaver -no-splash &
# exec wmaker
# exec startkde
# exec icewm
# exec blackbox
# exec fluxbox
exec xfce4-session

```

## bloquear pantalla

tu puedes bloquear la pantalla si se esta ejecutando `xscreensaver`, con el siguiente comando:

```
$ xscreensaver-command --lock

```