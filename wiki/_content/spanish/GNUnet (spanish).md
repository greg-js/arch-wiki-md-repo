**Estado de la traducción**
Este artículo es una traducción de [GNUnet](/index.php/GNUnet "GNUnet"), revisada por última vez el **2018-11-03**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GNUnet&diff=0&oldid=552757) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Tor](/index.php/Tor "Tor")

[GNUnet](https://gnunet.org/) es un framework para conexión segura entre redes P2P (peer-to-peer) que no utiliza ningún servicio centralizado o de confianza. Actualmente, el servicio implementado en el framework sirve para realizar intercambio de archivos resistentes a la censura.

Véase también [Wikipedia:GNUnet](https://en.wikipedia.org/wiki/es:GNUnet "wikipedia:es:GNUnet").

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
*   [3 Utilización](#Utilizaci.C3.B3n)
    *   [3.1 Descargar](#Descargar)
    *   [3.2 Subir](#Subir)
        *   [3.2.1 Para indexar un archivo/directorio](#Para_indexar_un_archivo.2Fdirectorio)
        *   [3.2.2 Para desindexar un archivo/directorio](#Para_desindexar_un_archivo.2Fdirectorio)
        *   [3.2.3 Modificar y eliminar archivos indexados](#Modificar_y_eliminar_archivos_indexados)
*   [4 Interfaz de usuario Web](#Interfaz_de_usuario_Web)

## Instalación

GNUnet puede ser [Instalado](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") con el paquete [gnunet](https://www.archlinux.org/packages/?name=gnunet). Si también desea utilizar la interfaz gráfica, instale [gnunet-gtk](https://www.archlinux.org/packages/?name=gnunet-gtk). Alternativamente, para la versión experimental más reciente, las versiones git están disponibles también en AUR, bajo [gnunet-git](https://aur.archlinux.org/packages/gnunet-git/) y [gnunet-gtk-git](https://aur.archlinux.org/packages/gnunet-gtk-git/) respectivamente.

## Configuración

[Inicie](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") y posiblemente [habilite](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") el servicio `gnunet`.

Alternativamente, para iniciar el par inmediatamente en un terminal ejecute:

```
# gnunet-arm -s

```

Véase también [cómo iniciar y detener un par GNUnet](https://GNUnet.org/how-Start-and-STOP-GNUnet-peer).

## Utilización

### Descargar

Para utilizar *gnunet-gtk* para descargar un archivo, sólo tiene que buscar el archivo en la pestaña *Filesystem*. Cuando vea el archivo que desea, sólo tiene que descargarlo como lo haría con cualquier otro programa de intercambio de archivos P2P. Inícielo con:

```
# gnunet-fs-gtk

```

### Subir

Subir archivos a la red gnunet es más complicado. GNUnet diferencia entre *indexar* un archivo e *insertar* un archivo. Los detalles se pueden leer en la [página web del framework](https://GNUnet.org). Los siguientes pasos explican cómo compartir datos con la red, y son una forma abreviada de las instrucciones encontradas en [esta página](https://GNUnet.org/File-Sharing).

Los siguientes pasos pueden ser hechos manualmente. Un módulo, llamado [gnunet-fuse](https://aur.archlinux.org/packages/gnunet-fuse/), ha sido desarrollado para hacer este proceso más fácil para el usuario.

#### Para indexar un archivo/directorio

```
gnunet-insert [-n] [-k palabraclave1] [-k palabraclave2] [-m TYPE:VALOR] nombredelarchivo

```

No es necesario añadir palabras clave, pero se recomienda. Esto se debe a que GNUnet no permite buscar por nombre de archivo, sino por palabras clave. Libextractor, que es una dependencia de gnunet, extraerá palabras clave del archivo, pero es posible que desee introducir palabras clave propias. La opción `-m` es para los metadatos. Se trata de datos (sobre el archivo) que otros usuarios de gnunet verán cuando sus archivos aparezcan durante sus búsquedas. Para obtener más información, consulte la documentación en línea de gnunet.org. La opción `-n` se utiliza para insertar un archivo/directorio en la base de datos de gnunet MySQL/sqlite, en lugar de simplemente indexarlo.

#### Para desindexar un archivo/directorio

```
gnunet-unindex

```

Suponga que ha olvidado los archivos que ha indexado, puede buscar los punteros en el directorio `/var/lib/gnunet/data/shared`, donde `GNUNET_HOME=/var/lib/gnunet` (definido por `gnunet-setup -d`).

**Warning:** No edite este directorio usted mismo, utilice gnunet-insert y gnunet-unindex para realizar cambios. Esto se debe a que gnunet utiliza una base de datos para almacenar la información del archivo, y eliminar (o modificar) el contenido del directorio no eliminará las entradas de la base de datos gnunet.

#### Modificar y eliminar archivos indexados

*   Al modificar un archivo, el URI del archivo cambia. Por lo tanto, GNUnet considera que este es un archivo completamente distinto. Por lo tanto, asegúrese de que el archivo original no está indexado (utilizando el comando gnunet-unindex), modifique el archivo y, a continuación, indexe el nuevo archivo para que sea accesible a través de la red.
*   Si desea mover/quitar un archivo de su sistema, entonces debe desindexarlo primero.

## Interfaz de usuario Web

Existe una interfaz web para GNUnet y está disponible en AUR como [gnunet-webui-git](https://aur.archlinux.org/packages/gnunet-webui-git/).