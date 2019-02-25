Related articles

*   [File manager functionality (Español)](/index.php/File_manager_functionality_(Espa%C3%B1ol) "File manager functionality (Español)")
*   [KDE (Español)](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)")
*   [udisks](/index.php/Udisks "Udisks")

[Dolphin](https://www.kde.org/applications/system/dolphin/) es el administrador de archivos por defecto de [KDE](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)"). Para el emulador de vídeojuego de consola, vea [Emulador Dolphin](/index.php?title=Dolphin_emulator_(Espa%C3%B1ol)&action=edit&redlink=1 "Dolphin emulator (Español) (page does not exist)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
    *   [1.1 Comparar archivos](#Comparar_archivos)
    *   [1.2 Previsualización de archivos](#Previsualización_de_archivos)
    *   [1.3 Vista CDs de audio](#Vista_CDs_de_audio)
*   [2 Uso](#Uso)
    *   [2.1 Abrir terminal](#Abrir_terminal)
    *   [2.2 KIO Slaves](#KIO_Slaves)
*   [3 Solución de Problemas](#Solución_de_Problemas)
    *   [3.1 Nombre de dispositivos mostrados como "X GiB Harddrive"](#Nombre_de_dispositivos_mostrados_como_"X_GiB_Harddrive")
    *   [3.2 Fuentes transparentes](#Fuentes_transparentes)
    *   [3.3 Bloqueos en compartición SMB montada](#Bloqueos_en_compartición_SMB_montada)
    *   [3.4 Iconos sin mostrarse](#Iconos_sin_mostrarse)
    *   [3.5 Colores de fondo incompatibles en vista de carpeta](#Colores_de_fondo_incompatibles_en_vista_de_carpeta)
*   [4 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [dolphin](https://www.archlinux.org/packages/?name=dolphin).

Para la versión de control y soporte de [Dropbox](/index.php?title=Dropbox_(Espa%C3%B1ol)&action=edit&redlink=1 "Dropbox (Español) (page does not exist)"), instale [dolphin-plugins](https://www.archlinux.org/packages/?name=dolphin-plugins). Para habilitar el plugin pertinente vaya a *Control > Configurar Dolphin... > Servicios*.

### Comparar archivos

El cuadro de diálogo *Comparar archivos* depende de [kompare](https://www.archlinux.org/packages/?name=kompare). Alternativamente, puede comparar archivos en cualquier herramienta de diferencias (como meld) seleccionando dos archivos, clic derecho, seleccione abrir con, y luego la herramienta de diferencias.

### Previsualización de archivos

*   [kdegraphics-thumbnailers](https://www.archlinux.org/packages/?name=kdegraphics-thumbnailers): Archivos de imagen y PDFs
*   [kimageformats](https://www.archlinux.org/packages/?name=kimageformats): Archivos Gimp *.xcf*
*   [resvg](https://aur.archlinux.org/packages/resvg/): Miniaturas de imágenes SVG rápido y preciso
*   [kdesdk-thumbnailers](https://www.archlinux.org/packages/?name=kdesdk-thumbnailers): Plugins para las miniaturas de sistema
*   [ffmpegthumbs](https://www.archlinux.org/packages/?name=ffmpegthumbs): Archivos de vídeo (Basado en ffmpeg)
*   [raw-thumbnailer](https://www.archlinux.org/packages/?name=raw-thumbnailer): Archivos *.raw*
*   [taglib](https://www.archlinux.org/packages/?name=taglib) : Archivos de audio
*   [kde-thumbnailer-apk](https://aur.archlinux.org/packages/kde-thumbnailer-apk/): Archivos **A**ndroid **a**pplication **p**ackage
*   [kde-thumbnailer-blender](https://aur.archlinux.org/packages/kde-thumbnailer-blender/): Archivos de aplicación Blender
*   [kde-thumbnailer-epub](https://aur.archlinux.org/packages/kde-thumbnailer-epub/): Archivos de libro de electrónico

Habilite la previsualización del tipo de archivo requerido en *Control > Configurar Dolphin... > General > Vistas previas*.

### Vista CDs de audio

El soporte para CDs de audio es provisto por la extensión [audiocd-kio](https://www.archlinux.org/packages/?name=audiocd-kio).

## Uso

### Abrir terminal

Dolphin y otras aplicaciones KDE usan [konsole](https://www.archlinux.org/packages/?name=konsole) por defecto. Para cambiar el emulador de terminal por defecto, ejecute `kcmshell5 componentchooser` y seleccione *Emulador de Terminal > Utilice un programa de terminal diferente*

### KIO Slaves

Dolphin utiliza *KIO slaves* para acceder a la red, papelera y otras funcionalidades, a diferencia de los administradores de archivos [GTK+](/index.php/GTK%2B "GTK+") quienes utilizan [GVFS](/index.php/GVFS "GVFS"). Los protocolos disponibles son mostrados en la barra de ubicación (modo editable) [[1]](https://docs.kde.org/stable/en/applications/dolphin/location-bar.html#location-bar-editable). Para marcarlos rápidamente, clic derecho en el espacio de trabajo, y seleccione "Añadir a Lugares".

## Solución de Problemas

### Nombre de dispositivos mostrados como "X GiB Harddrive"

Al crear una etiqueta de sistema, o etiqueta de partición, y Dplphin mostrará ésta etiquta en la lista de dispositivos en lugar del tamaño. Vea [Persistent block device naming#by-label](/index.php/Persistent_block_device_naming#by-label "Persistent block device naming").

### Fuentes transparentes

Las fuentes en marcos de selección pueden llegar a ser transparentes cuando usen [Estilos GTK+ Qt](/index.php/Uniform_look_for_Qt_and_GTK_applications_(Espa%C3%B1ol)#QGtkStyle "Uniform look for Qt and GTK applications (Español)"). Los estilos Qt nativos como *Cleanlooks* y *Oxygen* no son afectados.

### Bloqueos en compartición SMB montada

Vea [Samba#Unable to overwrite files](/index.php/Samba#Unable_to_overwrite_files.2C_permissions_errors "Samba").

### Iconos sin mostrarse

Si los iconos no se están mostrando en Dolphin, y aparece un error similar a "Pixmap es un Pixmap nulo" en la consola, pruebe poniendo ésta línea en su `~/.profile`

```
[ "$XDG_CURRENT_DESKTOP" = "KDE" ] || [ "$XDG_CURRENT_DESKTOP" = "GNOME" ] || export QT_QPA_PLATFORMTHEME="qt5ct"

```

### Colores de fondo incompatibles en vista de carpeta

Cuando se ejecuta Dolphin en algo diferente de Plasma, es posible que el color de fondo en panel de la vista de carpeta no coincida con el tema Qt de sistema. Esto es debido a que Dolphin lee el color de fondo de vista de carpeta desde la sección `[Colors:View]` en `~/.config/kdeglobals`. Cambie la siguiente línea a los valores R,G,B que prefiera:

 `~/.config/kdeglobals` 
```
...
[Colors:View]
BackgroundNormal=23,24,24
...

```

Alternativamente, use Alternatively, use [kvantum-qt5](https://www.archlinux.org/packages/?name=kvantum-qt5) para administrar sus temas Qt5\. Para instrucciones de uso vea la página de inicio de proyecto [Kvantum](https://github.com/tsujan/Kvantum/blob/master/Kvantum/README.md)

## Véase también

*   [Wikipedia:Dolphin (file manager)](https://en.wikipedia.org/wiki/Dolphin_(file_manager) "wikipedia:Dolphin (file manager)")
*   [KDE userbase: Dolphin](https://userbase.kde.org/Dolphin)
*   [Dolphin Handbook](https://docs.kde.org/stable/en/applications/dolphin/index.html)