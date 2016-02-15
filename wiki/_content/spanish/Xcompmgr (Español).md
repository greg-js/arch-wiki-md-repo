## Contents

*   [1 Introducción](#Introducci.C3.B3n)
    *   [1.1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Transparencia de Ventanas](#Transparencia_de_Ventanas)
*   [3 Problemas](#Problemas)
    *   [3.1 Las ventanas de Fluxbox no se levantan](#Las_ventanas_de_Fluxbox_no_se_levantan)
    *   [3.2 Mozilla Firefox se tranca al entrar a un sitio con Flash](#Mozilla_Firefox_se_tranca_al_entrar_a_un_sitio_con_Flash)
*   [4 Recursos adicionales](#Recursos_adicionales)

# Introducción

Xcompmgr es un simple manejador de ventanas capaz de renderizar sombras y junto a la utilidad <tt>transset</tt> transparencia sencilla de ventanas. Diseñado solo como un concepto de prueba, xcompmgr es una alternativa liviana a Compiz Fusion y similares.

Debido a que no reemplaza ningun manejador de ventanas, es la solución ideal para usuarios de [Openbox](/index.php/Openbox "Openbox") y [Fluxboxque](/index.php/Fluxbox "Fluxbox") buscan un escritorio mas elegante.

## Instalación

Instala los paquetes [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr) y [transset-df](https://www.archlinux.org/packages/?name=transset-df), que están disponibles en los repositorios oficiales.

```
# pacman -S xcompmgr transset-df

```

# Configuración

Para cargar xcompmgr, simplemente ejecuta:

```
$ xcompmgr -c

```

Para cargarlo cada vez que las X se inicien, agrega lo siguiente a tu `~/.xinitrc`:

```
xcompmgr -c &

```

En vez de `-c` puedes experimentar con otros parametras para modificar los efectos de sombras o incluso la aparición. Lo siguiente es un ejemplo de ello:

```
xcompmgr -c -t-5 -l-5 -r4.2 -o.55 &

```

Para obtener la lista completa de opciones, ejecuta:

```
$ xcompmgr --help

```

## Transparencia de Ventanas

Aunque su uso práctico es limitado, debido a su lento rendimiento, la utilidad <tt>transset</tt> puede ser usada para controlar la transparencia de una ventana.

Para controlar la transparencia de una ventana, asegurate que el programa deseado esta corriendo, entonces ejecuta:

```
transset _n_

```

.. donde _n_ es un número de 0 a 1, cero es transparente y 1 es opaco.

Una vez ejecutado, el cursor del mouse se transformará en una cruz. Simplemente haz click en la ventana deseada y la transparencia cambiará al valor especificado. Por ejemplo, `transset .25` colocará la ventana a un 75% de transpariencia.

# Problemas

## Las ventanas de Fluxbox no se levantan

Esto es arreglado en fluxbox CVS después de 0.9.10\. Mira [[1]](http://freedesktop.org/bugzilla/show_bug.cgi?id=1264) para mas información.

## Mozilla Firefox se tranca al entrar a un sitio con Flash

Puedes hacerlo bien sea creando un ejecutable en /etc/profile.d llamado _flash.sh_ que contenga esta línea:

```
export XLIB_SKIP_ARGB_VISUALS=1

```

O agregándoselo a la línea 184 de /opt/mozilla/bin/firefox.

¡Advertencia! esto deshabilitará los efectos de composición, podría causar que kwin no funcionara y cairo-compmgr se bloquee.

# Recursos adicionales

*   [Compiz](/index.php/Compiz "Compiz")