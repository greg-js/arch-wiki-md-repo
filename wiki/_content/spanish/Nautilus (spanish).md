[Nautilus](http://live.gnome.org/Nautilus) es el gestor de archivos predeterminado para [GNOME](https://live.gnome.org/). [Desde el sitio web de Gnome](http://library.gnome.org/users/user-guide/stable/gosnautilus-22.html.en): *El gestor de archivos Nautilus proporciona un modo sencillo e integrado para administrar sus archivos y aplicaciones. Se puede utilizar el gestor de archivos para hacer lo siguiente:*

*   Crear carpetas y documentos
*   Mostrar archivos y carpetas
*   Buscar y administrar sus archivos
*   Ejecutar secuencias de comandos y lanzar aplicaciones
*   Personalizar la apariencia de los archivos y carpetas
*   Abrir ubicaciones especiales en su ordenador
*   Escribir datos en un CD o DVD
*   Instalar y eliminar fuentes

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Administración del escritorio](#Administraci.C3.B3n_del_escritorio)
    *   [2.2 Cambiar la vista de elementos por defecto](#Cambiar_la_vista_de_elementos_por_defecto)
    *   [2.3 Eliminar las carpetas desde los lugares de la barra lateral](#Eliminar_las_carpetas_desde_los_lugares_de_la_barra_lateral)
    *   [2.4 Mostrar siempre la ubicación mediante entradas de texto](#Mostrar_siempre_la_ubicaci.C3.B3n_mediante_entradas_de_texto)
    *   [2.5 Plugins](#Plugins)
    *   [2.6 Crear un documento vacío con Nautilus 3.6](#Crear_un_documento_vac.C3.ADo_con_Nautilus_3.6)
    *   [2.7 Utilizar la tecla suprimir en Nautilis 3.6 para mover archivos a la papelera](#Utilizar_la_tecla_suprimir_en_Nautilis_3.6_para_mover_archivos_a_la_papelera)
*   [3 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [3.1 Nautilus no puede explorar mis recursos compartidos de red Windows](#Nautilus_no_puede_explorar_mis_recursos_compartidos_de_red_Windows)
    *   [3.2 Nautilus no puede ver los recursos compartidos de red de apple](#Nautilus_no_puede_ver_los_recursos_compartidos_de_red_de_apple)
    *   [3.3 Nautilus ya no es el administrador de archivos por defecto](#Nautilus_ya_no_es_el_administrador_de_archivos_por_defecto)

## Instalación

[Instale](/index.php/Pacman "Pacman") [nautilus](https://www.archlinux.org/packages/?name=nautilus) desde los [repositorios oficiales](/index.php/Official_repositories "Official repositories").

**Nota:** Nautilus no necesita el paquete completo [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell), pero sí requiere [gnome-desktop](https://www.archlinux.org/packages/?name=gnome-desktop). Algunos pueden encontrar este procedimiento interesante ya que instalar gnome-shell supone cierta complejidad.

Nautilus forma parte del grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

## Configuración

Nautilus es fácil de configurar gráficamente, pero no todas las configuraciones posibles se pueden hacer a través del menú de preferencias de nautilus. Hay más opciones disponibles con *dconf-editor* en `org.gnome.nautilus`.

### Administración del escritorio

Nautilus, por defecto, ya no controla fondos/escritorio en gnome-shell. No obstante, si le gusta tener iconos en el escritorio o disfrutar de la función de arrastrar y soltar, puede configurar fácilmente nautilus para manejar el escritorio.

Instale el paquete [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) y ejecútelo. Haga click en la opción "Escritorio" de la lista, y pinche en "Tener administrador de archivos para manejar el escritorio" deslizando la opción a "on". Puede que tenga que reiniciar nautilus ejecutando `killall nautilus;nautilus` o resetear [GNOME](/index.php/GNOME "GNOME"), presionando `ALT+F2`, escribiendo `r`, y pulsando `Intro`.

### Cambiar la vista de elementos por defecto

Puede cambiar la vista predeterminada de los objetos mediante el establecimiento de la variable `default-folder-viewer`, por ejemplo, para ver la lista:

```
$ gsettings set org.gnome.nautilus.preferences default-folder-viewer 'list-view'

```

### Eliminar las carpetas desde los lugares de la barra lateral

Las carpetas que se muestran están especificadas en `~/.config/user-dirs.dirs` y se pueden modificar con cualquier editor. La ejecución de `xdg-user-dirs-update` vuelve a cambiar los archivos visualizados, por lo que es aconsejable cambiar los permisos del archivo a sólo lectura.

### Mostrar siempre la ubicación mediante entradas de texto

La barra de herramientas estándar de Nautilus muestra una interfaz de barra de botones para la navegación por las rutas de los archivos. Para entrar en ubicaciones de ruta utilizando el *teclado*, debe exponer la ubicación de la ruta en el campo de navegación con entrada de texto. Ésto se logra pulsando `Ctrl+l`

Para hacer que esté siempre presente la ubicación de la ruta en el campo de navegación como entrada de texto, utilice GSettings como sigue:

```
$ gsettings set org.gnome.nautilus.preferences always-use-location-entry true

```

**Nota:** Después de cambiar a esta configuración, no tendrá la barra de botones. Sólo cuando el ajuste es **false** puede emplear ambas formas de navegación.

### Plugins

Algunos programas pueden añadir funcionalidad extra a Nautilus. Aquí hay algunos paquetes desde los repositorios oficiales que hacen precisamente éso.

*   **Nautilus Actions** — Programas configurados para ser lanzados cuando los archivos se seleccionan en Nautilus

	[http://gnome.org](http://gnome.org) || [nautilus-actions](https://www.archlinux.org/packages/?name=nautilus-actions)

*   **Nautilus Terminal** — Terminal integrado en Nautilus. Siempre está abierto en la carpeta actual, y sigue la navegación.

	[http://projects.flogisoft.com/nautilus-terminal/](http://projects.flogisoft.com/nautilus-terminal/) || [nautilus-terminal](https://www.archlinux.org/packages/?name=nautilus-terminal)

*   **Open in Terminal** — Un plugin de nautilus para abrir terminales en rutas locales arbitrarias

	[http://ftp.gnome.org/pub/GNOME/sources/nautilus-open-terminal](http://ftp.gnome.org/pub/GNOME/sources/nautilus-open-terminal) || [nautilus-open-terminal](https://www.archlinux.org/packages/?name=nautilus-open-terminal)

*   **Send to Menu** — Menú contextual de nautilus para enviar archivos

	[http://download.gnome.org/sources/nautilus-sendto/](http://download.gnome.org/sources/nautilus-sendto/) || [nautilus-sendto](https://www.archlinux.org/packages/?name=nautilus-sendto)

*   **Sound Converter** — Extensión de nautilus para convertir formatos de archivos de audio

	[http://code.google.com/p/nautilus-sound-converter/](http://code.google.com/p/nautilus-sound-converter/) || [nautilus-sound-converter](https://aur.archlinux.org/packages/nautilus-sound-converter/)

*   **Seahorse Nautilus** — Firma y cifrado PGP para nautilus

	[http://git.gnome.org/browse/seahorse-nautilus/](http://git.gnome.org/browse/seahorse-nautilus/) || [seahorse-nautilus](https://www.archlinux.org/packages/?name=seahorse-nautilus)

### Crear un documento vacío con Nautilus 3.6

Gnome 3.6 trae nuevos cambios para Nautilus. Algunas funciones se han abandonado en favor de un mantenimiento más fácil de Nautilus. La opción de crear un documento vacío se ha eliminado de forma predeterminada del menú de Nautilus. Hay que crear una carpeta `~/Templates/` en el directorio *home*, colocar un archivo vacío `touch ~/Templates/new` en el interior de dicho directorio con un Terminal o usando cualquier otro administrador de archivos. Reinicie nautilus para recuperar la función de crear un documento vacío desde el menú de Nautilus.

### Utilizar la tecla suprimir en Nautilis 3.6 para mover archivos a la papelera

Por defecto, Nautilus ahora ya no utiliza la tecla «Supr» para mover archivos a la papelera. Si quiere conseguir esta característica de nuevo, realice los siguientes cambios en `~/.config/nautilus/accels`:

```
- ; (gtk_accel_path "<Actions>/DirViewActions/Trash" "<Primary>Delete")
+ (gtk_accel_path "<Actions>/DirViewActions/Trash" "Delete")

```

## Solución de problemas

### Nautilus no puede explorar mis recursos compartidos de red Windows

Nautilus cuenta con el paquete [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) para esta funcionalidad; puede ser [instalado](/index.php/Pacman "Pacman") desde los [repositorios oficiales](/index.php/Official_repositories "Official repositories").

### Nautilus no puede ver los recursos compartidos de red de apple

Nautilus depende de [gvfs-afp](https://www.archlinux.org/packages/?name=gvfs-afp) y [avahi](https://www.archlinux.org/packages/?name=avahi) para esta funcionalidad, que puede ser [instalado](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Tenga en cuenta que, además de instalar [Avahi](/index.php/Avahi "Avahi"), necesita iniciarlo también, utilizando:

 `systemctl start avahi-daemon` 

y/o

 `systemctl enable avahi-daemon` 

### Nautilus ya no es el administrador de archivos por defecto

Si algunas aplicaciones como Firefox, entre otras, se niegan a tomar Nautilus como administrador de archivos por defecto, se puede solucionar agregando la siguiente línea en la sección [Default Applications] en `~/.local/share/applications/mimeapps.list`:

```
inode/directory=nautilus.desktop

```