**Nota:** Este artículo trata únicamente sobre la configuración básica, sin modificar diseños, asignación de teclas extras, etc. Véase [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") para conocer más sobre estos temas avanzados.

Las asignaciones del teclado (keymaps) para la [consola virtual](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console"), tipos de letras de la consola y mapas de la consola son proporcionados por el paquete [kbd](https://www.archlinux.org/packages/?name=kbd) (paquete que ya debería estar instalado), que también proporciona muchas herramientas de bajo nivel para la gestión de la consola virtual.

## Contents

*   [1 Visualizar la configuración del teclado](#Visualizar_la_configuraci.C3.B3n_del_teclado)
*   [2 Configurar la distribución del teclado](#Configurar_la_distribuci.C3.B3n_del_teclado)
    *   [2.1 Configuración permanente](#Configuraci.C3.B3n_permanente)
    *   [2.2 Configuración temporal](#Configuraci.C3.B3n_temporal)
*   [3 Otras opciones](#Otras_opciones)
    *   [3.1 Cambiar el tipo de letra de la consola](#Cambiar_el_tipo_de_letra_de_la_consola)
    *   [3.2 Ajustar el retardo y la velocidad de typematic](#Ajustar_el_retardo_y_la_velocidad_de_typematic)

## Visualizar la configuración del teclado

Puede utilizar la orden siguiente para ver la configuración del teclado presente en su equipo:

 `$ localectl status` 

```
   System Locale: LANG=es_ES.utf8
                  LC_NUMERIC=es_ES.UTF-8
                  LC_TIME=es_ES.UTF-8
                  LC_MONETARY=es_ES.UTF-8
                  LC_PAPER=es_ES.UTF-8
                  LC_MEASUREMENT=es_ES.UTF-8
       VC Keymap: es
      X11 Layout: es

```

## Configurar la distribución del teclado

A diferencia del teclado [XKB](/index.php/XKB "XKB"), que se integra por varios componentes, la distribución del teclado para la consola virtual tiene solo un componente. Por lo general, un archivo keymap se corresponde con una distribución de teclado (la declaración _include_ se puede utilizar para compartir partes comunes y un archivo keymap puede contener varios diseños con alguna combinación de tecla que se utiliza para la conmutación). Los archivos keymap se almacenan en el árbol de directorio `/usr/share/kbd/keymaps/`. Puede utilizar la siguiente orden para listar todos los mapas de teclado disponibles:

```
$ localectl list-keymaps

```

Las convenciones de los nombres de los mapas de teclado de la consola no son muy estrictas, pero, por lo general, el nombre consta de [2-letras del código del país](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements "wikipedia:ISO 3166-1 alpha-2") y una variante, separados por un guión (`-`) o un guión bajo (`_`).

### Configuración permanente

La configuración de alto nivel puede realizarse en `/etc/vconsole.conf`, que es leído por [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") en el arranque. La variable `KEYMAP` se utiliza para especificar la distribución de teclado. Si la variable está vacía o no se establece, la distribución del teclado usada por defecto es `us`. Véase `man 5 vconsole.conf` para obtener más ejemplos. Por ejemplo:

 `/etc/vconsole.conf` 

```
KEYMAP=es
...

```

Para mayor comodidad, la orden _localectl_ puede ser usada para establecer la distribución del teclado de la consola. Con esta orden se cambia la variable `KEYMAP` en `/etc/vconsole.conf` y fija la distribución del teclado en la sesión en curso. Por ejemplo:

```
$ localectl set-keymap --no-convert _mapa_de_teclas_

```

Véase `man 1 localectl` para obtener más detalles.

### Configuración temporal

Es posible establecer un distribución de teclado solo para la sesión actual. Esto es útil para probar diferentes mapas de teclado, resolución de problemas, etc.

La utilidad _loadkeys_ se utiliza para este propósito, utilizado internamente por [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") al cargar la distribución del teclado configurado en `/etc/vconsole.conf`. Su utilización a este fin es muy sencilla:

```
# loadkeys _mapa_de_teclas_

```

Véase `man 1 loadkeys` para obtener más detalles.

## Otras opciones

### Cambiar el tipo de letra de la consola

El paquete [kbd](https://www.archlinux.org/packages/?name=kbd) proporciona herramientas para cambiar el tipo de letras de la consola virtual y el mapa de caracteres. Los tipos de letras se guardan en el directorio `/usr/share/kbd/consolefonts/`.

La configuración se realiza en `vconsole.conf` usando las variables `FONT` y `FONT_MAP`:

 `/etc/vconsole.conf` 

```
...
FONT=Lat2-Terminus16
FONT_MAP=8859-15

```

Si la variable `FONT` está vacía o no se establece, se utiliza, por defecto, el tipo de letra incorporado en el kernel. Véase `man 5 vconsole.conf` para conocer más detalles.

### Ajustar el retardo y la velocidad de typematic

La opción _typematic delay_ indica la cantidad de tiempo (normalmente en milisegundos) que una tecla necesita ser presionada para que el proceso de repetición comience. Después que el proceso de repetición ha sido activado, el carácter se repite con una frecuencia determinada (por lo general en Hz dado) especificado por la opción _typematic rate_. Estos valores se pueden cambiar usando la orden _kbdrate_:

```
# kbdrate [-d _delay_] [-r _rate_]

```

Por ejemplo, para establecer una cadencia typematic de 200ms y una tasa typematic de 30Hz, utilice la siguiente orden:

```
# kbdrate -d 200 -r 30

```

Al emitir la orden sin especificar el retardo y la tasa, se ​restablecerá typematic a sus respectivos valores por defecto: un retardo de 250ms y una frecuencia de 11Hz:

```
# kbdrate

```