**Nota:** Este artículo trata únicamente sobre la configuración básica, sin modificar los diseños, asignación de teclas extras, etc. Véase [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") para conocer más sobre estos temas avanzados.

Xorg utiliza [X KeyBoard extension](/index.php/X_KeyBoard_extension "X KeyBoard extension") (XKB) para gestionar la distribución del teclado. Por otra parte, [xmodmap](/index.php/Xmodmap "Xmodmap") se puede utilizar para acceder al mapa del teclado interno directamente. Por lo general, no se recomienda el uso de _xmodmap_, excepto, tal vez, para tareas simples.

En este artículo se describe la configuración de bajo nivel usando XKB, que es eficaz en la mayoría de los casos, aunque algunos entornos de escritorios como [GNOME (Español)](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)") la sobrescriben con su propia configuración.

## Contents

*   [1 Visualizar la configuración del teclado](#Visualizar_la_configuraci.C3.B3n_del_teclado)
    *   [1.1 Utilidades de terceros](#Utilidades_de_terceros)
*   [2 Configurar la distribución del teclado](#Configurar_la_distribuci.C3.B3n_del_teclado)
    *   [2.1 Utilizar setxkbmap](#Utilizar_setxkbmap)
    *   [2.2 Utilizar los archivos de configuración de X](#Utilizar_los_archivos_de_configuraci.C3.B3n_de_X)
    *   [2.3 Utilizar localectl](#Utilizar_localectl)
*   [3 Opciones XKB usadas frecuentemente](#Opciones_XKB_usadas_frecuentemente)
    *   [3.1 Alternar entre distintas distribuciones de teclado](#Alternar_entre_distintas_distribuciones_de_teclado)
    *   [3.2 Terminar Xorg con Ctrl+Alt+Retroceso](#Terminar_Xorg_con_Ctrl.2BAlt.2BRetroceso)
    *   [3.3 Intercambiar Bloq Mayús con Control Izquierdo](#Intercambiar_Bloq_May.C3.BAs_con_Control_Izquierdo)
    *   [3.4 mouse keys](#mouse_keys)
    *   [3.5 Configurar tecla compose](#Configurar_tecla_compose)
        *   [3.5.1 Combinaciones de teclas](#Combinaciones_de_teclas)
*   [4 Otros ajustes](#Otros_ajustes)
    *   [4.1 Ajustar el retardo y la velocidad de typematic](#Ajustar_el_retardo_y_la_velocidad_de_typematic)

## Visualizar la configuración del teclado

Se puede utilizar la siguiente orden para ver la configuración vigente de XKB :

 `$ setxkbmap -print -verbose 10` 

```
Setting verbose level to 10
locale is C
Trying to load rules file ./rules/evdev...
Trying to load rules file /usr/share/X11/xkb/rules/evdev...
Success.
Applied rules from evdev:
rules:      evdev
model:      pc104
layout:     es,us
variant:    ,
options:    keypad:pointerkeys,terminate:ctrl_alt_bksp
Trying to build keymap using the following components:
keycodes:   evdev+aliases(qwerty)
types:      complete
compat:     complete
symbols:    pc+es+us:2+inet(evdev)+terminate(ctrl_alt_bksp)+keypad(pointerkeys)
geometry:   pc(pc104)
xkb_keymap {
	xkb_keycodes  { include "evdev+aliases(qwerty)"	};
	xkb_types     { include "complete"	};
	xkb_compat    { include "complete"	};
	xkb_symbols   { include "pc+es+us:2+inet(evdev)+terminate(ctrl_alt_bksp)+keypad(pointerkeys)"	};
	xkb_geometry  { include "pc(pc104)"	};
};

```

### Utilidades de terceros

Hay algunas utilidades «no oficiales» que permiten imprimir información específica acerca de la distribución del teclado que se está utilizando.

*   [xkb-switch-git](https://aur.archlinux.org/packages/xkb-switch-git/):

 `$ xkb-switch`  `us` 

*   [xkblayout-state](https://aur.archlinux.org/packages/xkblayout-state/):

 `$ xkblayout-state print "%s"`  `de` 

## Configurar la distribución del teclado

La distribución del teclado en Xorg puede configurarse de múltiples maneras. He aquí una explicación de las opciones usadas :

*   `XkbModel` selecciona el modelo de teclado. No tiene mucha relevancia, salvo que se cuente con un teclado con teclas extras. Los parámetros seguros son `pc104` o `pc105`. Pero para algunos portátiles con teclas adicionales, la simple definición del modelo adecuado puede hacer que funcionen dichas teclas.
*   `XkbLayout` selecciona la distribución del teclado. Se pueden especificar varias distribuciones en una lista separada por comas, para el caso, por ejemplo, de que desee cambiar rápidamente entre tales distribuciones.
*   `XkbVariant` selecciona una variante de la distribución específica. Por ejemplo, la variante, por defecto, del teclado `sk` es `qwertz`, pero se pueden especificar otras distintas manualmente tal como `qwerty`, etc.

**Advertencia:** Se deben especificar tantas variantes como número de distribuciones de teclados haya especificado. Si desea utilizar la variante por defecto de dichos teclados, especifique como _«xkbvariant»_ una cadena vacía (la coma debe permanecer). Por ejemplo, si se tiene la distribución de teclado `us` como primario que queremos usar con la variante predeterminada y una distribución de teclado secundaria `us` que queremos utilizar con la variante `dvorak`, especifique `us,us` como `XkbLayout` y `,dvorak` como `XkbVariant`.

*   `XkbOptions` contiene algunas opciones adicionales. Se utiliza para especificar la forma de alternar, el LED de notificación, el modo de compose, etc.

El nombre de la distribución, [_layout_], es normalmente un [código de dos letras por país](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements "wikipedia:ISO 3166-1 alpha-2"). Puede ver una lista completa de los modelos de teclado, distribuciones, variantes y opciones, con su correspondiente descripción, abriendo `/usr/share/X11/xkb/rules/base.lst`. Del mismo modo, pueden usarse las órdenes de abajo para ver los listados sin más:

*   `localectl list-x11-keymap-models`
*   `localectl list-x11-keymap-layouts`
*   `localectl list-x11-keymap-variants [_layout_]`
*   `localectl list-x11-keymap-options`

Los ejemplos de las secciones siguientes producirán el mismo resultado, esto es, se definirá el modelo `pc104`, `es` como teclado primario, `us` como teclado secundario, las variantes `deadtilde` para el teclado `es` y `dvorak` para `us`, y la combinación de teclas `Alt+Mayús` para alternar los teclados.

### Utilizar setxkbmap

La herramienta _setxkbmap_ establece la distribución del teclado para un servidor X activo y mantiene la configuración solo durante la sesión en curso. No obstante, puede utilizarse [xinitrc](/index.php/Xinitrc "Xinitrc") para hacer que la configuración se mantenga después de los reinicios. Esto último es útil para establecer una configuración específica para nuestra sesión de usuario distinta de la establecida para todo el sistema por los [archivos de configuración de X](#Using_X_configuration_files).

Su uso es como sigue:

```
$ setxkbmap [-model _modelo_xkb_] [-layout _distribución_xkb_] [-variant _variantes_xkb_] [-option _opciones_xkb_]

```

No es necesario especificar todas las opciones, por ejemplo, se puede cambiar solo una distribución:

```
$ setxkbmap -layout _distribución_xkb_

```

Véase `man 1 setxkbmap` para conocer un listado completo de los argumentos que se pueden pasar a la línea de órdenes.

Por ejemplo:

```
$ setxkbmap -model pc104 -layout es,us -variant deadtilde,dvorak -option grp:alt_shift_toggle

```

### Utilizar los archivos de configuración de X

La sintaxis de los archivos de configuración de X se explica en [Xorg#Configuration](/index.php/Xorg#Configuration "Xorg"). Este método crea la configuración para todo el sistema, que se mantiene después de los reinicios.

He aquí un ejemplo:

 `/etc/X11/xorg.conf.d/10-keyboard.conf` 

```
Section "InputClass"
        Identifier "system-keyboard"
        MatchIsKeyboard "on"
        Option "XkbLayout"  "es,us"
        Option "XkbModel"   "pc104"
        Option "XkbVariant" "deadtilde,dvorak"
        Option "XkbOptions" "grp:alt_shift_toggle"
EndSection

```

### Utilizar localectl

Por conveniencia, la herramienta _localectl_ puede ser utilizada en lugar de editar manualmente el archivo de configuración de X. Se guardará la configuración en `etc/X11/xorg.conf.d/00-keyboard.conf`. Este archivo no debe modificarse manualmente, porque _localectl_ sobrescribirá los cambios en el siguiente inicio.

Su uso es como sigue:

```
$ localectl set-x11-keymap [_distribución_] [_modelo_] [_variantes_] [_opciones_]

```

La siguiente órden creará un archivo `/etc/X11/xorg.conf.d/00-keyboard.conf` con el mismo contenido que el del ejemplo de arriba:

```
$ localectl set-x11-keymap es,us pc104 deadtilde,dvorak grp:alt_shift_toggle

```

## Opciones XKB usadas frecuentemente

### Alternar entre distintas distribuciones de teclado

Para ser capaz de cambiar fácilmente la distribución del teclado, primero especifique varias distribuciones entre las que desea alternar (la primera de ellas será la predeterminada). A continuación, especifique una tecla (o combinación de teclas), que utilizará para alternar las distribuciones. Por ejemplo, para cambiar entre una distribución US y otra Sueca, utilizando la tecla `Bloq Mayús`, use `us,se` como un argumento de `XkbLayout` y `grp:caps_toggle` como un argumento de `XkbOptions`.

Puede utilizar otras combinaciones de teclas distintas de `Bloq Mayús`, las cuales se enumeran en `/usr/share/X11/xkb/rules/base.lst`, que son las que comienzan con `grp:` y terminan en `_toggle`. Para obtener la lista completa de opciones disponibles, ejecute la orden siguiente:

```
$ grep "grp:.*_toggle" /usr/share/X11/xkb/rules/base.lst

```

### Terminar Xorg con Ctrl+Alt+Retroceso

Por defecto, la combinación de teclas `Ctrl+Alt+Retroceso` está desactivada. Puede activarla haciendo pasar el argumento `terminate:ctrl_alt_bksp` a `XkbOptions`.

### Intercambiar Bloq Mayús con Control Izquierdo

Para cambiar Bloq Mayús con la tecla Control izquierda, añada `ctrl:swapcaps` a `XkbOptions`. Ejecute la orden siguiente para ver opciones similares, junto con sus descripciones:

```
$ grep -E "(ctrl|caps):" /usr/share/X11/xkb/rules/base.lst

```

### mouse keys

[Mouse keys](https://en.wikipedia.org/wiki/Mouse_keys "wikipedia:Mouse keys") está desactivada por defecto y tiene que ser activada manualmente haciendo pasar el argumento `keypad:pointerkeys` a `XkbOptions`. Esto hará que al teclear `Mayús+BloqNum` alternemos entre el teclado numérico y mousekeys.

### Configurar tecla compose

La [tecla compose](https://en.wikipedia.org/wiki/Compose_key "wikipedia:Compose key"), cuando se pulsa en secuencia con otras teclas, produce un carácter Unicode. Por ejemplo, en la mayoría de configuraciones pulsando `_tecla_compose_ ' e` produce `é`. Esto es especialmente útil si se necesita escribir en un idioma diferente a aquel para el cual la distribución del teclado fue diseñado (como escribir en francés, italiano y alemán en un teclado americano).

Por ejemplo, para que la tecla `Alt` derecha funcione como una tecla compose, pase el argumento `compose:ralt` a `XkbOptions`.

Se pueden utilizar otras teclas como teclas compose, su listado figura en `/usr/share/X11/xkb/rules/base.lst` y comienzan con `compose:`. Para obtener la lista completa de las opciones disponibles, ejecute la orden siguiente :

```
$ grep "compose:" /usr/share/X11/xkb/rules/base.lst

```

#### Combinaciones de teclas

Las combinaciones predeterminadas para las teclas compose dependen de la configuración regional y se almacenan en `/usr/share/X11/locale/_locale_usado_/Compose`, donde `_locale_usado_` es, por ejemplo, `es_ES.UTF-8`.

Puede definir sus propias combinaciones de la tecla compose copiando el archivo predeterminado a `~/.XCompose` y modificándolo. La tecla compose funciona con cualquiera de los miles de caracteres Unicode válidos, incluyendo aquellos fuera del Basic Multilingual Plane.

No obstante lo anterior, GTK no utiliza [XIM](https://en.wikipedia.org/wiki/X_Input_Method "wikipedia:X Input Method") de forma predeterminada, por lo que no lee las teclas de `~/.XCompose`. Esto se puede solucionar obligando a GTK a utilizar XIM añadiendo `export GTK_IM_MODULE=xim` y/o `export XMODIFIERS="@im=none"` a `~/.xprofile`.

**Sugerencia:** XIM es muy antiguo, es posible que tenga más suerte con otros métodos de entrada: [SCIM](https://en.wikipedia.org/wiki/Smart_Common_Input_Method "wikipedia:Smart Common Input Method"), [uim](https://en.wikipedia.org/wiki/Uim "wikipedia:Uim"), [IBus](https://en.wikipedia.org/wiki/Intelligent_Input_Bus "wikipedia:Intelligent Input Bus") etc. Véase [Internationalization#Input methods in Xorg](/index.php/Internationalization#Input_methods_in_Xorg "Internationalization") para conocer más detalles.

## Otros ajustes

### Ajustar el retardo y la velocidad de typematic

La opción _typematic delay_ («retardo para la automatización de escritura») indica la cantidad de tiempo (normalmente en milisegundos) que una tecla necesita ser presionada para que el proceso de repetición comience. Después que el proceso de repetición ha sido activado, el carácter se repite con una frecuencia determinada (por lo general en Hz dado) especificado por la opción _typematic rate_ («velocidad de la automatización de escritura»). Estos valores se pueden cambiar usando la orden _xset_:

```
$ xset r rate _delay_ [_rate_]

```

Por ejemplo, para establecer una cadencia typematic de 200ms y una tasa typematic de 30Hz, utilice la siguiente orden (use [xinitrc](/index.php/Xinitrc "Xinitrc") para mantener permanente la configuración):

```
$ xset r rate 200 30

```

Al emitir la orden sin especificar el retardo y la tasa, se ​restablecerá typematic a sus respectivos valores por defecto: un retardo de 660ms y una frecuencia de 25Hz:

```
$ xset r rate

```