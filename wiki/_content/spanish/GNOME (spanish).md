**Estado de la traducción**
Este artículo es una traducción de [GNOME](/index.php/GNOME "GNOME"), revisada por última vez el **2018-11-20**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GNOME&diff=0&oldid=556231) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Related articles

*   [GTK+](/index.php/GTK%2B_(Espa%C3%B1ol) "GTK+ (Español)")
*   [GDM](/index.php/GDM_(Espa%C3%B1ol) "GDM (Español)")
*   [GNOME/Tips and tricks](/index.php/GNOME/Tips_and_tricks "GNOME/Tips and tricks")
*   [GNOME/Troubleshooting](/index.php/GNOME/Troubleshooting "GNOME/Troubleshooting")
*   [GNOME/Files](/index.php/GNOME/Files "GNOME/Files")
*   [GNOME/Gedit](/index.php/GNOME/Gedit "GNOME/Gedit")
*   [GNOME/Web](/index.php/GNOME/Web "GNOME/Web")
*   [GNOME/Evolution](/index.php/GNOME/Evolution "GNOME/Evolution")
*   [GNOME/Flashback](/index.php/GNOME/Flashback "GNOME/Flashback")
*   [GNOME/Keyring](/index.php/GNOME/Keyring "GNOME/Keyring")
*   [GNOME/Document viewer](/index.php/GNOME/Document_viewer "GNOME/Document viewer")
*   [Official repositories#gnome-unstable](/index.php/Official_repositories#gnome-unstable "Official repositories")

[GNOME](https://en.wikipedia.org/wiki/es:GNOME que pretende ser simple y fácil de utilizar. Está diseñado por [el Proyecto GNOME](https://en.wikipedia.org/wiki/The_GNOME_Project en lugar de [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)").

## Contents

*   [1 Instalación](#Instalación)
*   [2 Sesiones de GNOME](#Sesiones_de_GNOME)
*   [3 Inicio](#Inicio)
    *   [3.1 Gráficamente](#Gráficamente)
    *   [3.2 Manualmente](#Manualmente)
        *   [3.2.1 Sesiones de Xorg](#Sesiones_de_Xorg)
        *   [3.2.2 Sesiones de Wayland](#Sesiones_de_Wayland)
    *   [3.3 Aplicaciones de GNOME en Wayland](#Aplicaciones_de_GNOME_en_Wayland)
*   [4 Navegación](#Navegación)
*   [5 Nombres heredados](#Nombres_heredados)
*   [6 Configuración](#Configuración)
    *   [6.1 Configuración del sistema](#Configuración_del_sistema)
        *   [6.1.1 Color](#Color)
        *   [6.1.2 Luz nocturna](#Luz_nocturna)
        *   [6.1.3 Fecha y hora](#Fecha_y_hora)
        *   [6.1.4 Aplicaciones predeterminadas](#Aplicaciones_predeterminadas)
        *   [6.1.5 Ratón y panel táctil](#Ratón_y_panel_táctil)
        *   [6.1.6 Red](#Red)
        *   [6.1.7 Cuentas en línea](#Cuentas_en_línea)
        *   [6.1.8 Buscador](#Buscador)
    *   [6.2 Configuración avanzada](#Configuración_avanzada)
        *   [6.2.1 Apariencia](#Apariencia)
            *   [6.2.1.1 Temas](#Temas)
            *   [6.2.1.2 Altura de la barra de título](#Altura_de_la_barra_de_título)
            *   [6.2.1.3 Orden de los botones de la barra de título](#Orden_de_los_botones_de_la_barra_de_título)
            *   [6.2.1.4 Ocultar la barra de título cuando está maximizado](#Ocultar_la_barra_de_título_cuando_está_maximizado)
            *   [6.2.1.5 Temas de GNOME Shell](#Temas_de_GNOME_Shell)
            *   [6.2.1.6 Iconos en el menú](#Iconos_en_el_menú)
        *   [6.2.2 Carpetas de la rejilla de aplicaciones](#Carpetas_de_la_rejilla_de_aplicaciones)
        *   [6.2.3 Inicio automático](#Inicio_automático)
        *   [6.2.4 Escritorio](#Escritorio)
            *   [6.2.4.1 Iconos en el escritorio](#Iconos_en_el_escritorio)
            *   [6.2.4.2 Fondo de pantalla y de bloqueo](#Fondo_de_pantalla_y_de_bloqueo)
            *   [6.2.4.3 Desactivar la esquina activa superior izquierda](#Desactivar_la_esquina_activa_superior_izquierda)
        *   [6.2.5 Extensiones](#Extensiones)
        *   [6.2.6 Tipografía](#Tipografía)
        *   [6.2.7 Métodos de entrada](#Métodos_de_entrada)
        *   [6.2.8 Energía](#Energía)
            *   [6.2.8.1 Configurar el comportamiento del cierre de la tapa](#Configurar_el_comportamiento_del_cierre_de_la_tapa)
            *   [6.2.8.2 Cambiar la acción del nivel crítico de batería](#Cambiar_la_acción_del_nivel_crítico_de_batería)
    *   [6.3 Utilizar un gestor de ventanas diferente](#Utilizar_un_gestor_de_ventanas_diferente)
*   [7 Véase también](#Véase_también)

## Instalación

Hay disponibles dos grupos:

*   [gnome](https://www.archlinux.org/groups/x86_64/gnome/) contiene el escritorio base de GNOME y un subconjunto de aplicaciones [[1]](https://wiki.gnome.org/Apps) bien integradas;
*   [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/) contiene aplicaciones GNOME adicionales, incluido un gestor de archivos, gestor de discos, [editor de texto](/index.php/Gedit "Gedit") y un conjunto de juegos. Tenga en cuenta que este grupo se basa en el grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

El escritorio base consiste en [GNOME Shell](https://en.wikipedia.org/wiki/es:GNOME_Shell "wikipedia:es:GNOME Shell"), un complemento para el gestor de ventanas [Mutter](https://en.wikipedia.org/wiki/es:Mutter_(software) "wikipedia:es:Mutter (software)"). Se puede instalar por separado con [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell).

**Nota:** *mutter* actúa como un compositor para el escritorio, utilizando aceleración gráfica por hardware para proporcionar efectos dirigidos a reducir el desorden de la pantalla. El gestor de sesión de GNOME detecta automáticamente si su controladora gráfica es capaz de ejecutar GNOME Shell y, de no ser así, recurre al renderizado software utilizando *llvmpipe* .

## Sesiones de GNOME

GNOME tiene tres sesiones disponibles, todas utilizan GNOME Shell.

*   **GNOME** es el valor predeterminado que utiliza Wayland. Las aplicaciones X tradicionales se ejecutan a través de Xwayland.
*   **GNOME Classic** es un diseño de escritorio tradicional con una interfaz similar a GNOME 2, que utiliza extensiones y parámetros preactivados. [[2]](http://worldofgnome.org/welcome-to-gnome-3-8-flintstones-mode/) Por lo tanto, es más un GNOME Shell personalizado que un modo verdaderamente distinto.
*   **GNOME en Xorg** ejecuta GNOME shell utilizando Xorg.

## Inicio

GNOME puede iniciarse gráficamente con un [gestor de pantalla](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)") o manualmente desde la consola (pueden faltar algunas funciones).

**Nota:** El soporte para el bloqueo de pantalla (y demás) en GNOME lo proporciona GDM. Si GNOME no se inicia con GDM, se puede utilizar otro bloqueador de pantalla. Véase [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security").

### Gráficamente

Seleccione la sesión: *GNOME*, *GNOME Classic* o *GNOME en Xorg* desde el menú de sesión del gestor de pantalla.

### Manualmente

#### Sesiones de Xorg

*   Para la sesión de GNOME en Xorg, añada al archivo `~/.xinitrc`:
    ```
    export GDK_BACKEND=x11
    exec gnome-session
    ```

*   Para la sesión de GNOME Classic, añada al archivo `~/.xinitrc`:
    ```
    export XDG_CURRENT_DESKTOP=GNOME-Classic:GNOME
    export GNOME_SHELL_SESSION_MODE=classic
    exec gnome-session --session=gnome-classic
    ```

Después de editar el archivo `~/.xinitrc`, se puede iniciar GNOME con el comando `startx` (véase [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") para obtener detalles adicionales, como preservar la sesión de logind). Después de configurar el archivo `~/.xinitrc`, también se puede organizar en [Inicio automático de X al inicio de sesión](/index.php/Start_X_at_login_(Espa%C3%B1ol) "Start X at login (Español)").

#### Sesiones de Wayland

**Nota:**

*   Todavía es necesario un servidor X, proporcionado por el paquete [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland), para ejecutar aplicaciones que aún no se han portado a [Wayland](/index.php/Wayland_(Espa%C3%B1ol) "Wayland (Español)").
*   Wayland con el controlador propietario [NVIDIA](/index.php/NVIDIA_(Espa%C3%B1ol) "NVIDIA (Español)") tiene actualmente un rendimiento muy bajo: [FS#53284](https://bugs.archlinux.org/task/53284).

Es posible iniciar manualmente una sesión de Wayland con `XDG_SESSION_TYPE=wayland dbus-run-session gnome-session`.

Para iniciar la sesión en tty1, añada lo siguiente a su `.bash_profile`:

```
if [[ -z $DISPLAY ]] && [[ $(tty) = /dev/tty1 ]] && [[ -z $XDG_SESSION_TYPE ]]; then
  XDG_SESSION_TYPE=wayland exec dbus-run-session gnome-session
fi

```

### Aplicaciones de GNOME en Wayland

Cuando se utiliza la sesión *GNOME*, las aplicaciones GNOME se ejecutarán utilizando Wayland. Para la depuración, el [manual de GTK+](https://developer.gnome.org/gtk3/stable/gtk-running.html) lista las opciones y las variables de entorno.

## Navegación

Para aprender a utilizar GNOME Shell, lea [GNOME Shell Cheat Sheet](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet); destaca las características de GNOME Shell y los atajos de teclado. Las funciones incluyen el cambio de tareas, el uso del teclado, el control de la ventana, el panel, el modo de vista general y demás. Algunos de los atajos son:

*   `Super` + `m`: muestra la bandeja de mensajes
*   `Super` + `a`: muestra el menú de aplicaciones
*   `Alt` + `Tab`: cambia entre las aplicaciones activas
*   `Alt` + `º` (la tecla sobre `Tab` en las distribuciones de teclado en español): cambia entre las ventanas de la aplicación en primer plano
*   `Alt` + `F2`, luego introduzca `r` o `restart`: reinicia el intérprete de órdenes en caso de problemas con el intérprete gráfico (solo en el modo X/legacy, no en el modo Wayland).

## Nombres heredados

**Nota:** Algunos programas de GNOME han sufrido cambios de nombre en los que se ha cambiado el nombre de la aplicación en la documentación y sobre los diálogos, pero no el nombre del ejecutable. Algunas de estas aplicaciones se listan en la tabla siguiente.

**Sugerencia:** La búsqueda del nombre heredado de una aplicación en la barra de búsqueda de GNOME Shell devolverá con éxito la aplicación en cuestión. Por ejemplo, la búsqueda de *nautilus* devolverá *Archivos*.

| Actual | Antiguo |
| [Archivos](/index.php?title=Archivos&action=edit&redlink=1 "Archivos (page does not exist)") | Nautilus |
| [Web](/index.php/GNOME/Web "GNOME/Web") | Epiphany |
| Vídeos | Tótem |
| Menú principal | Alacarte |
| Visor de documentos | Evince |
| Analizador de uso de disco | Baobab |
| Visor de imágenes | EoG (Ojo de GNOME) |
| [Contraseñas y claves](/index.php/GNOME/Keyring "GNOME/Keyring") | Seahorse |

## Configuración

El panel de configuración del sistema GNOME (*gnome-control-center*) y las aplicaciones GNOME utilizan el sistema de configuración [dconf](https://en.wikipedia.org/wiki/Dconf "wikipedia:Dconf") para almacenar sus configuraciones.

Puede acceder directamente a la base de datos dconf utilizando las herramientas de línea de comando `gsettings` o `dconf`. Esto también le permite configurar ajustes no expuestos por las interfaces de usuario.

Hasta antes de GNOME 3.24 la configuración era aplicada por el demonio de configuración de GNOME, que podría ejecutarse fuera de una sesión de GNOME utilizando:

```
$ nohup /usr/lib/gnome-settings-daemon/gnome-settings-daemon > /dev/null &

```

Sin embargo, GNOME 3.24 reemplazó el demonio de configuración de GNOME con varios complementos de configuración separados `/usr/lib/gnome-settings-daemon/gsd-*`. Estos complementos ahora se controlan mediante archivos de escritorio en `/etc/xdg/autostart` (org.gnome.SettingsDaemon.*.desktop). Para ejecutar estos complementos fuera de una sesión de GNOME, ahora deberá copiar/editar las [entradas de escritorio](/index.php/Desktop_entries "Desktop entries") correspondientes a `~/.config/autostart`.

La configuración generalmente se realiza según el usuario, esta sección no trata sobre cómo crear plantillas de configuración para múltiples usuarios.

### Configuración del sistema

#### Color

El demonio `colord` lee el EDID de la pantalla y extrae el perfil de color apropiado. La mayoría de los perfiles de color son precisos y no se requiere configuración; sin embargo, para aquellos que no son precisos, o para pantallas más antiguas, los perfiles de color se pueden colocar en `~/.local/share/icc/`.

#### Luz nocturna

GNOME viene con un filtro de luz azul incorporado similar a [Redshift](/index.php/Redshift "Redshift"). Puede activar y personalizar la hora en que desea activar la luz nocturna desde el menú de configuración de pantalla. Además, puede ajustar la temperatura de color (en grados kelvin) con la siguiente configuración [dconf](https://www.archlinux.org/packages/?name=dconf), donde 5000 es un valor de ejemplo:

```
$ gsettings set org.gnome.settings-daemon.plugins.color night-light-temperature 5000

```

**Sugerencia:** Para cambiar la temperatura diurna en una sesión de Wayland, instale [esta extensión](https://extensions.gnome.org/extension/1276/night-light-slider/).

#### Fecha y hora

Si el sistema tiene configurado un [demonio de protocolo de tiempo de red](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon"), también será efectivo para GNOME. La sincronización se puede configurar manualmente desde el menú, si es necesario.

Para mostrar la fecha en la barra superior, ejecute:

```
$ gsettings set org.gnome.desktop.interface clock-show-date true

```

Además, para mostrar los números de semana en el calendario desplegado de la barra superior, ejecute:

```
$ gsettings set org.gnome.desktop.calendar show-weekdate true

```

#### Aplicaciones predeterminadas

Al instalar GNOME por primera vez, es posible que las aplicaciones incorrectas estén manejando ciertos protocolos. Por ejemplo, *totem* abre los vídeos en lugar de [VLC](/index.php/VLC_(Espa%C3%B1ol) "VLC (Español)") utilizado anteriormente. Algunas de las asociaciones se pueden configurar desde la configuración del sistema a través de: *Detalles* > *Aplicaciones predeterminadas*.

Para otros protocolos y métodos, véase [Aplicaciones predeterminadas](/index.php/Default_applications "Default applications") para la configuración.

#### Ratón y panel táctil

La mayoría de las configuraciones del panel táctil se pueden establecer desde la configuración del sistema a través de: *Dispositivos* > *Ratón y «touchpad»*.

Dependiendo de su dispositivo, pueden estar disponibles otros ajustes de configuración, pero no expuestos a través de la GUI predeterminada. Por ejemplo, un `click-method` del touchpad diferente

 `$ gsettings range org.gnome.desktop.peripherals.touchpad click-method` 
```

enum
'default'
'none'
'areas'
'fingers'
```

para ser configurado manualmente:

```
$ gsettings set org.gnome.desktop.peripherals.touchpad click-method 'fingers'

```

o mediante [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).

**Nota:** El controlador [synaptics](/index.php?title=Synaptics_(Espa%C3%B1ol)&action=edit&redlink=1 "Synaptics (Español) (page does not exist)") no es compatible con GNOME. En su lugar debe utilizar [libinput](/index.php/Libinput_(Espa%C3%B1ol) "Libinput (Español)"). Véase [este informe de error](https://bugzilla.gnome.org/show_bug.cgi?id=764257#c12).

#### Red

[NetworkManager](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)") es la herramienta nativa del proyecto GNOME para controlar la configuración de red desde el intérprete. [Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) y [active](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") la unidad systemd `NetworkManager.service`.

Si bien también se puede utilizar cualquier otro [gestor de red](/index.php/Network_manager "Network manager"), NetworkManager proporciona la integración completa a través de la configuración de red del intérprete y un applet indicador de estado [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) (no requerido para GNOME).

#### Cuentas en línea

Los backends para la aplicación de mensajería de GNOME [empathy](https://www.archlinux.org/packages/?name=empathy), así como la sección de Cuentas en línea de GNOME del panel de configuración del sistema se proporcionan en un grupo separado: [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). Véase [No se pueden añadir cuentas en las cuentas en línea de Empathy y GNOME](/index.php/GNOME/Troubleshooting#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts "GNOME/Troubleshooting"). Algunas cuentas en línea, como [ownCloud](/index.php/OwnCloud "OwnCloud"), requieren que [gvfs-goa](https://www.archlinux.org/packages/?name=gvfs-goa) esté instalado para una funcionalidad completa en aplicaciones GNOME como [Archivos GNOME](/index.php/GNOME_Files_(Espa%C3%B1ol) "GNOME Files (Español)") y Documentos GNOME [https: //wiki.gnome .org / ThreePointSeven / Features / Owncloud].

#### Buscador

GNOME Shell tiene una búsqueda a la que se puede acceder rápidamente presionando la tecla `Super` y comenzando a escribir. El paquete [tracker](https://www.archlinux.org/packages/?name=tracker) se instala de forma predeterminada como parte del grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/) y proporciona una aplicación de indexación y una base de datos de metadatos. Se puede configurar con el elemento de menú *Buscar*; controle el estado con *tracker-control*. Se inicia automáticamente con *gnome-session* cuando el usuario inicia sesión. La indexación se puede iniciar manualmente con `tracker-control -s`. Los ajustes de búsqueda también se puede configurar en el panel *Configuración del sistema*.

La base de datos del rastreador se puede consultar utilizando el comando *tracker-sparql*. Véase su página de manual [tracker-sparql(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tracker-sparql.1) para más información.

### Configuración avanzada

Como se indicó anteriormente, muchas opciones de configuración, como cambiar el tema [GTK+](/index.php/GTK%2B_(Espa%C3%B1ol) "GTK+ (Español)") o del [gestor de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") no están expuestas en el panel de configuración del sistema GNOME (*gnome-control-center*). Es posible que aquellos usuarios que deseen configurar estos ajustes deseen utilizar Retoques de GNOME ([gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks)), una herramienta gráfica que expone muchos de estos ajustes.

La configuración de GNOME (que se almacena en la base de datos DConf) también se puede configurar utilizando [*dconf-editor*](https://developer.gnome.org/dconf/unstable/dconf-editor.html) (una herramienta de configuración gráfica de DConf) o la herramienta de línea de órdenes [*gsettings*](https://developer.gnome.org/gio/stable/GSettings.html). Retoques de GNOME no hacen nada más tras la GUI; tenga en cuenta que no encontrará todas las configuraciones descritas en las siguientes secciones.

#### Apariencia

##### Temas

GNOME utiliza Adwaita por defecto. Para aplicar Adwaita en oscuro solo a aplicaciones GTK+ 2 utilice el siguiente enlace simbólico:

```
$ ln -s /usr/share/themes/Adwaita-dark ~/.themes/Adwaita

```

Para seleccionar nuevos temas (muévalos al directorio apropiado y) utilice Retoques de GNOME o las siguientes órdenes de configuración de GSOME:

Para el tema GTK+:

```
$ gsettings set org.gnome.desktop.interface gtk-theme *nombre-tema*

```

Para el tema del icono:

```
$ gsettings set org.gnome.desktop.interface icon-theme *nombre-tema*

```

**Nota:** El tema del gestor de ventanas sigue al tema GTK+. El uso de `org.gnome.desktop.wm.preferences theme` está en desuso y se ignora.

Véase [Temas de GTK+](/index.php/GTK%2B_(Espa%C3%B1ol)#Temas "GTK+ (Español)") e [Icons#Manually](/index.php/Icons#Manually "Icons").

##### Altura de la barra de título

**Nota:** La aplicación de esta configuración reduce la barra de título de GNOME-terminal y Chromium, pero no parece afectar a la altura de la barra de título de Nautilus.
 `~/.config/gtk-3.0/gtk.css` 
```
headerbar.default-decoration {
 padding-top: 0px;
 padding-bottom: 0px;
 min-height: 0px;
 font-size: 0.6em;
}

headerbar.default-decoration button.titlebutton {
 padding: 0px;
 min-height: 0px;
}

```

Véase [[3]](https://ask.fedoraproject.org/en/question/10035/shrink-title-bar/?answer=86149#post-id-86149) para más información.

##### Orden de los botones de la barra de título

Para establecer el orden para el gestor de ventanas de GNOME (Mutter, Metacity):

```
$ gsettings set org.gnome.desktop.wm.preferences button-layout ':minimize,maximize,close'

```

**Sugerencia:** Los dos puntos indican en qué lado de la barra de título aparecerán los botones de la ventana.

##### Ocultar la barra de título cuando está maximizado

*   [Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [gnome-shell-extension-no-title-bar](https://aur.archlinux.org/packages/gnome-shell-extension-no-title-bar/) o [gnome-shell-extension-no-title-bar](https://aur.archlinux.org/packages/gnome-shell-extension-no-title-bar/). Las ventanas maximizadas obtienen la barra de título fusionada en la barra de actividad.

*   [Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [mutter-hide-legacy-decorations](https://aur.archlinux.org/packages/mutter-hide-legacy-decorations/). Cambia una configuración predeterminada en el gestor de ventanas, a fin de ocultar automáticamente la barra de título en aplicaciones heredadas (sin barra de encabezado) cuando están maximizadas o en mosaico en el lateral.

*   [Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [gnome-shell-extension-pixel-saver-git](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver-git/) o [gnome-shell-extension-pixel-saver](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver/). Las ventanas maximizadas obtienen la barra de título fusionada en la barra de actividad, ahorrando píxeles valiosos.

##### Temas de GNOME Shell

El tema de GNOME Shell en sí es configurable. Para utilizar un tema de Shell, primero asegúrese de tener el paquete [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) instalado. Luego active la extensión *Temas de usuario*, ya sea a través de Retoques de GNOME o a través de la página web [GNOME Shell Extensions](https://extensions.gnome.org). Los temas de Shell se pueden cargar y seleccionar mediante Retoques de GNOME.

Hay una serie de temas de GNOME Shell disponibles [en AUR](https://aur.archlinux.org/packages.php?O=0&K=gnome-shell-theme&do_Search=Go&PP=50&SB=v&SO=d). Los temas de shell también se pueden descargar desde [gnome-look.org](http://gnome-look.org/).

##### Iconos en el menú

El esquema predeterminado de GNOME no muestra ningún icono en los menús. Para mostrar iconos en los menús, ejecute el siguiente comando.

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

```

#### Carpetas de la rejilla de aplicaciones

**Sugerencia:** El script [gnome-catgen](https://github.com/prurigro/gnome-catgen) ([gnome-catgen-git](https://aur.archlinux.org/packages/gnome-catgen-git/)) le permite administrar carpetas a través de la creación de archivos en `~/.local/share/applications-categories` nombradas tras cada categoría y conteniendo una lista de los archivos de escritorio que pertenecen a las aplicaciones que le gustaría tener dentro. Opcionalmente, puede hacer que recorra cada aplicación sin una carpeta e introducir la categoría deseada hasta que pulse `Ctrl-c` o se quede sin aplicaciones.

En **dconf-editor** navegue a `org.gnome.desktop.app-folder` y establezca el valor `folder-children` a una matriz de nombres de carpetas separados por comas:

```
['Utilities', 'Sundry']

```

Añada aplicaciones utilizando `gsettings`:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ apps "['alacarte.desktop', 'dconf-editor.desktop']"

```

Esto añade las aplicaciones `alacarte.desktop` y `dconf-editor.desktop` a la carpeta Sundry. También se creará la carpeta `org.gnome.desktop.app-folder.folders.Sundry`.

Para nombrar la carpeta (si no tiene un nombre que aparezca en la parte superior de las aplicaciones):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ name "Sundry"

```

Las aplicaciones también se pueden ordenar por su categoría (especificada en su archivo *.desktop*):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ categories "['Office']"

```

Si ciertas aplicaciones que coinciden con una categoría no se quieren en una carpeta determinada, se pueden establecer exclusiones:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ excluded-apps "['libreoffice-draw.desktop']"

```

Para más información, véase [[4]](https://git.gnome.org/browse/gsettings-desktop-schemas/tree/schemas/org.gnome.desktop.app-folders.gschema.xml.in) y [[5]](https://wiki.gentoo.org/wiki/Gnome_Applications_Folders).

#### Inicio automático

GNOME implementa [XDG Autostart](/index.php/XDG_Autostart_(Espa%C3%B1ol) "XDG Autostart (Español)").

El paquete [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) permite administrar las entradas de inicio automático.

**Sugerencia:** Si el botón del signo más en la sección Aplicaciones de inicio de Retorques no responde, intente iniciar Retoques desde el terminal utilizando la siguiente orden: `gnome-tweaks`. Véase el siguiente [hilo del foro](https://bbs.archlinux.org/viewtopic.php?pid=1413631#p1413631).

**Nota:** El diálogo en desuso *gnome-session-properties* se puede añadir [instalando](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [gnome-session-properties](https://aur.archlinux.org/packages/gnome-session-properties/).

#### Escritorio

##### Iconos en el escritorio

Hasta GNOME 3.28, los iconos en el escritorio eran proporcionados por [Archivos](/index.php/GNOME/Files_(Espa%C3%B1ol) "GNOME/Files (Español)") que dibujaba una ventana transparente sobre el escritorio que contenía los iconos. A partir de GNOME 3.28, esta funcionalidad se ha eliminado y los iconos del escritorio ya no están disponibles. Entre las posibles soluciones se encuentra el uso de [Nemo](/index.php/Nemo "Nemo") (una bifurcación de Archivos que aún tiene la funcionalidad de los iconos del escritorio) o la instalación de [gnome-shell-extension-desktop-icons](https://aur.archlinux.org/packages/gnome-shell-extension-desktop-icons/) que replica parcialmente la funcionalidad del icono del escritorio disponible en GNOME 3.26 y anteriores. Para obtener más información, véase el siguiente [hilo del foro](https://bbs.archlinux.org/viewtopic.php?id=235633).

##### Fondo de pantalla y de bloqueo

Al configurar el fondo de la pantalla de Escritorio o Bloqueo, es importante tener en cuenta que la pestaña Imágenes solo mostrará las imágenes ubicadas en la carpeta `/home/*usuario*/Imágenes`. Si desea usar una imagen que no se encuentra en esta carpeta, utilice las órdenes que se indican a continuación.

Para el fondo del escritorio:

```
$ gsettings set org.gnome.desktop.background picture-uri 'file:///path/to/my/picture.jpg'

```

Para el fondo de pantalla de bloqueo:

```
$ gsettings set org.gnome.desktop.screensaver picture-uri 'file:///path/to/my/picture.jpg'

```

##### Desactivar la esquina activa superior izquierda

Puede desactivar la esquina activa superior izquierda con el paquete [gnome-shell-extension-no-topleft-hot-corner](https://aur.archlinux.org/packages/gnome-shell-extension-no-topleft-hot-corner/).

#### Extensiones

El catálogo de extensiones está disponible en [extensions.gnome.org](https://extensions.gnome.org). Se pueden instalar y activar en un navegador configurando el interruptor en la parte superior izquierda de la pantalla en **ON** y pulsando en **Instalar** en la ventana emergente (si la extensión en cuestión no está instalada). Las extensiones instaladas se pueden ver en [extensions.gnome.org/local](https://extensions.gnome.org/local/), donde se pueden consultar las actualizaciones disponibles. Las extensiones instaladas también se pueden activa o desactivas con [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).

**Nota:** Las extensiones de [extensions.gnome.org](https://extensions.gnome.org) se pueden instalar de inmediato con [GNOME/Web](/index.php/GNOME/Web "GNOME/Web"). Para otros navegadores, es necesario instalar [chrome-gnome-shell](https://www.archlinux.org/packages/?name=chrome-gnome-shell) y la extensión de navegador apropiada.

GNOME Shell se puede personalizar con extensiones por cada usuario o para todo el sistema. La instalación de extensiones con [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") hace que estén disponibles para todos los usuarios del sistema y automatiza el proceso de actualización. El paquete [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) proporciona un conjunto de extensiones mantenidas como parte del proyecto de GNOME (la sesión clásica de GNOME usa muchas de las extensiones incluidas). Los usuarios que desean una barra de tareas pero no quieren utilizar la sesión de GNOME Classic deben activar la extensión *Window list* (*Lista de ventana*, proporcionada por el paquete [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions)).

Para listar las extensiones actualmente habilitadas:

```
$ gsettings get org.gnome.shell enabled-extensions

```

Para obtener más información sobre las extensiones de GNOME Shell, véase [[6]](https://extensions.gnome.org/about/).

#### Tipografía

**Sugerencia:** Si establece el *Factor de escala* en un valor superior a 1.00, el menú Accesibilidad se activará automáticamente.

La tipografía se pueden configurar para títulos de Ventanas, Interfaz (aplicaciones), Documentos y Monoespacio. Véase la pestaña Tipografías en Retoques para las opciones relevantes.

Para las sugerencias, es probable que se desee RGBA ya que esto se ajusta a la mayoría de los tipos de monitores, y si la tipografía aparece demasiado obstruida, reduzca la sugerencia a *Ligero* o *Ninguno*.

#### Métodos de entrada

GNOME tiene soporte integrado para los [métodos de entrada](/index.php/Input_method "Input method") a través de [IBus](/index.php/IBus "IBus"), solo se necesita instalar [ibus](https://www.archlinux.org/packages/?name=ibus) y el motor del método de entrada deseado (por ejemplo, [ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin) para el Pinyin inteligente), después de la instalación, el motor del método de entrada se puede añadir como un diseño de teclado en la Configuración regional y de idioma de GNOME.

#### Energía

Cuando está utilizando una computadora portátil, es posible que desee modificar la siguiente configuración:

```
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-timeout *3600*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type *hibernate*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-timeout *1800*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-type *hibernate*
$ gsettings set org.gnome.settings-daemon.plugins.power power-button-action *suspend*
$ gsettings set org.gnome.desktop.lockdown disable-lock-screen *true*

```

Para mantener el monitor activo cuando la tapa está cerrada:

```
$ gsettings set org.gnome.settings-daemon.plugins.xrandr default-monitors-setup do-nothing

```

GNOME 3.24 desaprobó las siguientes configuraciones:

```
org.gnome.settings-daemon.plugins.power button-hibernate
org.gnome.settings-daemon.plugins.power button-power
org.gnome.settings-daemon.plugins.power button-sleep
org.gnome.settings-daemon.plugins.power button-suspend
org.gnome.settings-daemon.plugins.power critical-battery-action

```

##### Configurar el comportamiento del cierre de la tapa

Retoques de GNOME pueden *inhibir* opcionalmente la configuración de *systemd* para el evento ACPI de cierre de la tapa. [[7]](Http://ftp.gnome.org/pub/GNOME/sources/gnome-tweak-tool/3.17/gnome-tweak-tool-3.17.1.news) Para *inhibir* la configuración, inicie la herramienta Retoques y, debajo de la pestaña General, desmarque la opción *Suspender al cerrar la tapa del portátil*. Esto significa que el sistema no hará nada al cerrar la tapa en lugar de suspenderlo, que es el comportamiento predeterminado. Al desmarcar la opción se crea `~/.config/autostart/ignore-lid-switch-tweak.desktop` que iniciará automáticamente el inhibidor de Retoques.

Si no desea que el sistema se suspenda o que no haga nada con la tapa cerrada, deberá asegurarse de que la configuración descrita anteriormente esté marcada y luego configure *systemd* con `HandleLidSwitch=*preferred_behaviour*` como se describe en [Eventos de ACPI](/index.php/Power_management_(Espa%C3%B1ol)#Eventos_de_ACPI "Power management (Español)").

##### Cambiar la acción del nivel crítico de batería

El panel de configuración no proporciona una opción para cambiar la acción del nivel crítico de batería. Estas configuraciones también se han eliminado de dconf. Ahora son gestionados por upower. Edite la configuración de upower en `/etc/UPower/UPower.conf`. Encuentre estas configuraciones y ajústelos a sus necesidades.

 `/etc/UPower/UPower.conf` 
```
PercentageLow=10
PercentageCritical=3
PercentageAction=2
CriticalPowerAction=HybridSleep
```

### Utilizar un gestor de ventanas diferente

GNOME Shell no admite el uso de un [gestor de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") diferente, sin embargo [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback") proporciona sesiones para Metacity y [Compiz](/index.php/Compiz "Compiz"). Además, es posible definir sus propias [sesiones personalizadas de GNOME](/index.php/GNOME/Tips_and_tricks#Custom_GNOME_sessions "GNOME/Tips and tricks") que utilizan componentes alternativos.

## Véase también

*   [Sitio web oficial](https://www.gnome.org/)
*   [Artículo de Wikipedia](https://en.wikipedia.org/wiki/es:GNOME "wikipedia:es:GNOME")
*   [Extensiones de GNOME-Shell](https://extensions.gnome.org/)
*   [GNOME Shell Cheat Sheet](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet)
*   Personalización (temas, iconos...):
    *   [Personalice GNOME](https://wiki.gnome.org/Personalization)
    *   [GNOME Look](https://www.gnome-look.org/)
*   Aplicaciones GNOME:
    *   [Índice de aplicaciones GNOME](https://wiki.gnome.org/Apps)
    *   [Wikipedia:GNOME Core Applications](https://en.wikipedia.org/wiki/GNOME_Core_Applications "wikipedia:GNOME Core Applications")
*   Fuentes/Espejos GNOME:
    *   [Repositorio Git de GNOME](https://git.gnome.org/browse/)
    *   [Espejo Github de GNOME](https://github.com/GNOME)