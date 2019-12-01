**Estado de la traducción**
Este artículo es una traducción de [Guake](/index.php/Guake "Guake"), revisada por última vez el **2019-11-29**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Guake&diff=0&oldid=590476) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [GNOME](/index.php/GNOME "GNOME")

[Guake](http://guake-project.org/) es un terminal despleable desde la parte superior de la pantella para [GNOME](/index.php/GNOME "GNOME") (al estilo de [Yakuake](/index.php/Yakuake "Yakuake") para [KDE](/index.php/KDE "KDE"), [Tilda](/index.php/Tilda "Tilda") o el terminal utilizado en Quake).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
*   [3 Inicio automático](#Inicio_automático)
*   [4 Realizar script para Guake](#Realizar_script_para_Guake)
*   [5 Solución de problemas](#Solución_de_problemas)
    *   [5.1 En gestores de ventanas flotantes](#En_gestores_de_ventanas_flotantes)
    *   [5.2 Alternar la visibilidad de Guake no funciona (Wayland)](#Alternar_la_visibilidad_de_Guake_no_funciona_(Wayland))
*   [6 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [guake](https://www.archlinux.org/packages/?name=guake), disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

## Utilización

Una vez instalado, puede iniciar Guake desde un terminal con:

```
$ guake

```

Después de que Guake se haya iniciado, puede hacer clic con el botón secundario del ratón sobre la interfaz y seleccionar *Preferencias* para cambiar la tecla de acceso rápido y descartar el terminal automáticamente, que de forma predeterminada está configurada en `F12`.

## Inicio automático

Es posible que desee cargar Guake al iniciar el entorno de escritorio. Para hacer esto, necesita:

```
# cp /usr/share/applications/guake.desktop /etc/xdg/autostart/

```

Consulte [Autostarting](/index.php/Autostarting "Autostarting") para obtener más información.

## Realizar script para Guake

Al igual que [Yakuake](/index.php/Yakuake "Yakuake"), Guake permite controlarse en tiempo de ejecución enviando los mensajes del servicio [D-Bus](/index.php/D-Bus "D-Bus"). Por lo tanto, se puede utilizar para iniciar Guake en una sesión definida por el usuario. Puede crear pestañas, asignarles nombres y también solicitar ejecutar cualquier orden específica en cualquier pestaña abierta o simplemente mostrar/ocultar la ventana de Guake, manualmente en un terminal o creando un script personalizado para ello.

Ejemplo de tal script se proporciona debajo de esta sección.

Puede utilizar el ejecutable *guake* para enviar mensajes D-Bus. Aquí está la lista de opciones disponibles que le pueden interesar:

*   `-t`, `--toggle-visibility` — alterna la visibilidad de la ventana del terminal. En realidad, puede escribir `guake`, y alternará la visibilidad de la instancia que ya se está ejecutando.
*   `-f`, `--fullscreen` — pone Guake en modo de pantalla completa.
*   `--show` — muestra la ventana principal de Guake.
*   `--hide` — oculta la ventana principal de Guake.
*   `-n *CUR_DIR*`, `--new-tab=*CUR_DIR*` — crea una nueva pestaña y la selecciona. El valor de `CUR_DIR` es utilizado para establecer un directorio actual para la pestaña, si se especifica.
*   `-s *INDEX*`, `--select-tab=*INDEX*` — selecciona la pestaña con el índice `INDEX`. Las pestañas indexadas comienzan con 0.
*   `-g`, `--selected-tab` — imprime el índice de la pestaña seleccionada actualmente.
*   `-e *CMD*`, `--execute-command=*CMD*` — ejecuta una orden arbitraria `CMD` en la pestaña seleccionada .
*   `-i *INDEX*`, `--tab-index=*INDEX*` — utilizada con `--rename-tab` para especificar el índice `INDEX` de una pestaña para renombrarla. El valor predeterminado es 0.
*   `--rename-tab=*TITLE*` — establece el nombre de la pestaña en `TITLE`. Puede restablecer el título de la pestaña al valor predeterminado pasando un solo guión (`"-"`). Utilice la opción `-i` para especificar qué pestaña cambiar de nombre.
*   `--bgcolor=*RGB*` — establece el color de fondo `RGB` en términos hexadecimales (`#rrggbb`) de la pestaña seleccionada.
*   `--fgcolor=*RGB*` — establece el color del primer plano `RGB` en términos hexadecimales (`#rrggbb`) de la pestaña seleccionada.
*   `-r *TITLE*`, `--rename-current-tab=*TITLE*` — igual que `--rename-tab`, pero cambia el nombre de la pestaña seleccionada actualmente.
*   `-q`, `--quit` — cierra la instancia de Guake en funcionamiento.

Se pueden combinar varias opciones en una sola llamada. Si no se está ejecutando una instancia de Guake, todas las opciones especificadas se aplicarán a la instancia recién creada.

Para mostrar la lista de todas las opciones disponibles, escriba `guake --help`.

Hay 2 formas de iniciar Guake mientras aplica estos scripts:

*   copiando el siguiente ejemplo en un archivo como `guake-init.sh` haciéndolo ejecutable y lanzando ese archivo en lugar de guake;
*   haciendo clic con el botón secundario del ratón en `Terminal de Guake > Preferencias > General` y añadir la ruta al script `guake-init.sh` en la sección «Path to script executed on Guake start:» mientras se asegura para comentar `/usr/bin/guake &` del script siguiente.

La segunda opción es preferible si desea que el script se ejecute independientemente de cómo se inicie Guake y aún puede indicarle a Guake que no ejecute el script con `guake --no-startup-script`, si es necesario.

Ejemplo:

```
#!/bin/bash

/usr/bin/guake &
sleep 5 # deja que comience el proceso Guake principal e inicialice la sesión de D-Bus

# pestaña de ajuste que se abrirá por defecto
guake --rename-tab="iotop" --execute="/usr/bin/iotop"

# crea nueva pestaña, e inicia sesión bash en ella
guake --new-tab --execute="/usr/bin/bash"
# y luego ejecuta htop, renombrando la pestaña a «htop»
guake --execute="/usr/bin/htop" --rename-current-tab="htop"

# ...
guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/atop" --rename-current-tab="atop"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="~/.iptables.sh" --rename-current-tab="iptables -nvL"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/journalctl --follow --full" --rename-current-tab="journalctl"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/irssi" --rename-current-tab="irssi"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/sudo -i" --rename-current-tab="rootshell0"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/sudo -i" --rename-current-tab="rootshell1"

guake --new-tab --execute="/usr/bin/bash"
guake --rename-current-tab="shell0"

guake --new-tab --execute="/usr/bin/bash"
guake --rename-current-tab="shell1"

```

Tenga en cuenta que debemos esperar un tiempo que se denomina *sleep* para evitar condiciones de solapamiento entre instancias en ejecución.

La opción

**Advertencia:** `--execute` puede causar daños en una pestaña que ejecuta un programa de interfaz de texto, como `fdisk` o `innotop`. Úselo con precaución. Hay un error en github al respecto: [guake#921](https://github.com/Guake/guake/issues/921).

## Solución de problemas

### En gestores de ventanas flotantes

Si está utilizando Tilda y un gestor de ventanas flotante, puede descubrir que puede utilizar la cadena class de «Tilda» para establecer que la ventana siga flotando. Pero la salida de WM_CLASS(STRING) de Guake es «Main.py», por lo que debe utilizar «Main.py» para hacer esto. Por ejemplo, en i3wm, añada esto a su .i3/config:

```
for_window [class="Main.py"] floating enable

```

### Alternar la visibilidad de Guake no funciona (Wayland)

Si está utilizando Wayland, la tecla de acceso rápido de alternancia de visibilidad de Guake puede no funcionar en algunas aplicaciones. Esto se debe a que Guake utiliza una biblioteca global de teclas rápidas para entornos X y no hay una interfaz global de teclas rápidas equivalente para Wayland. Muchas aplicaciones (por ejemplo, Firefox) se ejecutan en Wayland a través de XWayland, donde funcionará la alternatividad de Guake, pero otras que ejecutan de forma nativa Wayland (por ejemplo, aplicaciones GNOME) desactivan la función de alternar Guake.

Si no desea cambiar a un entorno X, una solución simple requiere configurar un acceso directo con su gestor de ventanas/entorno de escritorio para la orden `guake-toggle`.

Consulte [github issue](https://github.com/Guake/guake/issues/994) para obtener más detalles.

**Nota:** el uso de `guake-toggle` es [recomendado](https://github.com/Guake/guake/blob/master/docs/source/user/faq.rst#manual-keybinding) frente `guake -t`. Es mucho más rápido ya que va directamente sobre D-Bus sin inicializar completamente Guake.

## Véase también

*   [guake(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/guake.1)