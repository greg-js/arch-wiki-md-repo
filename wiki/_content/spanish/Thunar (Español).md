Desde la [página principal](http://docs.xfce.org/xfce/thunar/start) del proyecto:

	_Thunar es un nuevo administrador de archivos moderno para el entorno de escritorio Xfce. Thunar ha sido diseñado desde cero para ser rápido y fácil de usar. Su interfaz de usuario es limpia e intuitiva, y no incluye opciones confusas o inútiles por defecto. Thunar es rápido y sensible, con un buen tiempo de arranque y de carga de carpetas._

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Montaje automático](#Montaje_autom.C3.A1tico)
    *   [1.2 Plugins y addons](#Plugins_y_addons)
*   [2 Administrador del Volumen Thunar](#Administrador_del_Volumen_Thunar)
    *   [2.1 Instalación](#Instalaci.C3.B3n_2)
    *   [2.2 Configuración](#Configuraci.C3.B3n)
*   [3 Consejos y trucos](#Consejos_y_trucos)
    *   [3.1 Usar Thunar para explorar zonas remotas](#Usar_Thunar_para_explorar_zonas_remotas)
    *   [3.2 GVFS necesita D-Bus y polkit](#GVFS_necesita_D-Bus_y_polkit)
    *   [3.3 Iniciar en modo demonio](#Iniciar_en_modo_demonio)
    *   [3.4 Ajustar el tema de iconos](#Ajustar_el_tema_de_iconos)
    *   [3.5 Resolver problemas con el arranque lento "en frío"](#Resolver_problemas_con_el_arranque_lento_.22en_fr.C3.ADo.22)
*   [4 Acciones personalizadas](#Acciones_personalizadas)
    *   [4.1 Escanear virus](#Escanear_virus)
    *   [4.2 Enlace a Dropbox](#Enlace_a_Dropbox)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

[Instale](/index.php/Pacman "Pacman") el paquete [thunar](https://www.archlinux.org/packages/?name=thunar) disponible en los [repositorios oficiales](/index.php/Official_repositories "Official repositories"). Este paquete es parte del grupo [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/), por lo que al ejecutar [Xfce4](/index.php/Xfce4 "Xfce4"), es probable que ya tenga instalado Thunar.

### Montaje automático

Thunar utiliza [GVFS](/index.php/GVFS "GVFS") para el montaje automático, consulte [GVFS](/index.php/GVFS "GVFS") para más detalles para conseguir que funcione.

### Plugins y addons

*   **ffmpegthumbnailer** — Programa externo para generar imágenes en miniatura. Para que esto funcione, debe instalar [tumbler](https://www.archlinux.org/packages/?name=tumbler).

	[http://code.google.com/p/ffmpegthumbnailer/](http://code.google.com/p/ffmpegthumbnailer/) || [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer)

*   **Thunar Archive Plugin** — Plugin que permite crear y extraer archivos comprimidos utilizando los elementos del menú contextual. No crea o extraer directamente los archivos, sino que actúa como interfaz para otros programas como File Roller, Ark, o Xarchiver. Es parte de [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/).

	[http://goodies.xfce.org/projects/thunar-plugins/thunar-archive-plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-archive-plugin) || [thunar-archive-plugin](https://www.archlinux.org/packages/?name=thunar-archive-plugin)

*   **Thunar Media Tags Plugin** — PProgramas que le permite ver la información detallada acerca de los archivos multimedia. También tiene otras opciones como posibilidad de cambiar el nombre y permitir la edición de etiquetas de los archivos multimedia. Es compatible con ID3 (sistema de formato de archivo MP3) y etiquetas Ogg/Vorbis. Es parte de [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/).

	[http://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin) || [thunar-media-tags-plugin](https://www.archlinux.org/packages/?name=thunar-media-tags-plugin)

*   **Thunar Shares Plugin** — Programas que permite compartir rápidamente una carpeta con Samba desde Thunar sin necesidad de acceso como root. Véase también [how to configure directions](/index.php/Samba#Creating_user_share_path "Samba").

	[http://goodies.xfce.org/projects/thunar-plugins/thunar-shares-plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-shares-plugin) || [thunar-shares-plugin](https://aur.archlinux.org/packages/thunar-shares-plugin/)

*   **[Thunar Volume Manager](/index.php/Thunar#Thunar_Volume_Manager "Thunar")** — Gestión automática de los dispositivos extraibles en Thunar. Parte del grupo [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/).

	[http://foo-projects.org/~benny/projects/thunar-volman](http://foo-projects.org/~benny/projects/thunar-volman) || [thunar-volman](https://www.archlinux.org/packages/?name=thunar-volman)

*   **Tumbler** — Programa externo para generar imágenes en miniaturas. Instale también [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer) para activar la miniaturización de vídeo.

	[http://git.xfce.org/xfce/tumbler/tree/README](http://git.xfce.org/xfce/tumbler/tree/README) || [tumbler](https://www.archlinux.org/packages/?name=tumbler)

## Administrador del Volumen Thunar

Mientras Thunar soporta el montaje y desmontaje automático de medios extraíbles, el admnistrador de volúmenes Thunar permite funcionalidades extendidas, tales como la posibilidad de ejecutar comandos particulares para la conexión de un dispositivo periférico o abrir automáticamente una ventana de Thunar al montar el volumen.

### Instalación

Thunar Volume Manager se puede instalar con el paquete [thunar-volman](https://www.archlinux.org/packages/?name=thunar-volman) disponible en los [repositorios oficiales](/index.php/Official_repositories "Official repositories").

### Configuración

También se puede configurar para ejecutar ciertas acciones al conectar cámaras y reproductores de audio. Una vez instalado el plugin:

1.  Lance Thunar y abra Editar -> Preferencias
2.  Bajo la pestaña "Avanzado", marque la casilla "Habilitar la administración de volúmenes"
3.  Pinche en configurar y verifique los siguientes elementos:
    *   Montar unidades extraíbles (discos duros) cuando se enciendan.
    *   Montar medios extraíbles (USB) cuando se inserten.
4.  Haga adicionalmente también los cambios que desee (vea el ejemplo a continuación)

He aquí un ejemplo de ajuste para hacer que Amarok se abra para reproducir un CD de audio al insertarlo.

```
 Multimedia - CD Audio: `amarok --cdplay %d`

```

## Consejos y trucos

### Usar Thunar para explorar zonas remotas

Desde Xfce 4.8 (Thunar 1.2), es posible explorar carpetas en zonas remotas (como servidores FTP o Samba para compartir ficheros) directamente en Thunar, similar a la funcionalidad de GNOME y KDE. Los paquetes [gvfs](https://www.archlinux.org/packages/?name=gvfs) y [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) son necesarios para habilitar esta funcionalidad. Ambos paquetes están disponibles en los [repositorios oficiales](/index.php/Official_repositories "Official repositories").

Después de reiniciar Xfce se agrega un enlace de "Red" a la barra lateral de Thunar y las ubicaciones remotas se pueden abrir con los siguientes esquemas de URI en el campo de diálogo (abierto con `Ctrl+L`): smb://, ftp://, ssh://, sftp://

### GVFS necesita D-Bus y polkit

Si utiliza un gestor de ventanas independiente, asegúrese que [D-Bus](/index.php/D-Bus "D-Bus") es lanzado en el inicio de sesión, y que se está ejecutando un agente de autenticación de [polkit](/index.php/Polkit "Polkit"). De lo contrario, GVFS no estará activo. Véase [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") para obtener más detalles.

### Iniciar en modo demonio

Thunar puede ejecutarse en modo demonio. Este comportamiento tiene varias ventajas, incluyendo un inicio más rápido de Thunar, haciendo que Thunar se inicialice en segundo plano y sólo se abra una ventana cuando sea necesario (por ejemplo, cuando una unidad USB se inserta).

Asegúrese de que la orden `thunar --daemon` está [iniciada](/index.php/Autostarting_(Espa%C3%B1ol) "Autostarting (Español)") en el inicio de sesión.

### Ajustar el tema de iconos

Al usar Thunar fuera de Gnome o Xfce, ciertos paquetes y configuraciones que se utilizan para controlar los iconos pueden estar ausentes. Los gestores de ventanas como Awesome y Xmonad no vienen con el administrador XSETTINGS, que es donde Thunar busca primero su configuración de icono. Es posible instalar y ejecutar xfce-mcs-manager mediante un script de inicio si se va a utilizar Xfce4 conjuntamente con muchas aplicaciones de Gnome. La configuración de gtk-icon-theme-name para gtk2 se puede ajustar para un usuario mediante la adición de algo parecido a lo siguiente en `~/.gtkrc-2.0`:

```
 gtk-icon-theme-name = "Tango"

```

Por supuesto, al instalar el paquete [gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme) dará a Thunar un tema de iconos diferente a los iconos predeterminados para el resto de los elementos.

### Resolver problemas con el arranque lento "en frío"

Algunas usuarios todavía tienen problemas con Thunar que tarda mucho tiempo para iniciar la primera vez. Esto es debido a que gvfs verifica la red, impidiendo a Thunar que arranque hasta que gvfs finalice sus operaciones. Para cambiar este comportamiento, edite el archivo `usr/share/gvfs/mounts/network.mount` y modifique `automount=true` a `automount=false`.

## Acciones personalizadas

Esta sección trata de acciones personalizadas útiles que se pueden obtener a través del menú Editar -> Configuración de acciones personalizadas. Se enumeran más ejemplos en la [wiki de thunar](http://thunar.xfce.org/pwiki/documentation/custom_actions).

### Escanear virus

Para utilizar esta acción es necesario tener instalado clamav y clamtk.

| Nombre | Comando | Patrones de archivos | Aparecerá si está en la selección |
| Analizar en busca de virus | clamtk %F | * | Seleccionar todo |

### Enlace a Dropbox

| Nombre | Comando | Patrones de archivos | Aparecerá si está en la selección |
| Enlace a Dropbox | `ln -s %f /ruta/a/Carpeta_Dropbox` | * | Directorios, otros archivos |

Tenga en cuenta que cuando se utilizan muchos enlaces simbólicos de archivos y carpetas a un lugar particular, podría ser útil ponerlos en la carpeta `Enviar a` del menú contextual para evitar que el mismo menú se sobredimensione. Esto es bastante fácil de lograr y requiere un archivo .desktop en `~/.local/share/Thunar/sendto` para cada acción a realizar. Por ejemplo, si quiere un enlace simbólico a la carpeta dropbox en Enviar a, creamos un archivo `dropbox_folder.desktop` con el contenido de abajo. La nueva acción personalizada se activará después de reiniciar Thunar.

```
[Desktop Entry]
Type=Application
Version=1.0
Encoding=UTF-8
Exec=ln -s %f /percorso/alla/cartella/dropbox
Icon=/usr/share/icons/dropbox.png
Name=Dropbox

```

## Véase también

*   Página del proyecto [Thunar](http://thunar.xfce.org/index.html).
*   Página del proyecto [Thunar Volume Manager](http://goodies.xfce.org/projects/thunar-plugins/thunar-volman).
*   [Lista](http://goodies.xfce.org/projects/thunar-plugins/start) de plugins.