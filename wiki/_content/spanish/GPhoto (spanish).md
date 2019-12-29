Este documento procura configurar hotplug de modo que los miembros del grupo de usuarios puedan tener acceso a una cámara fotográfica digital USB. Este documento es simple y no se cubren casos especiales. Sin embargo, el contenido de éste documento es principalmente un resumen de gphoto y la gente que necesite información adicional puede consultar éste sitio: Recuerda fijar tu cámara digital en modo p-t-p (algunas quizás usen el modo de almacenamiento?) . La lista de cámaras fotográficas que libgphoto2 soporta las pueden encontrar en gphoto. Si tu cámara digital no se enumera dentro de la lista podría funcionar de todos modos como medio de almacenamiento USB. Hay otro artículo en éste wiki que lo explica, Dispositivos de Almacenamiento USB.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalar hotplug y libgphoto2](#Instalar_hotplug_y_libgphoto2)
*   [2 Configurando hotplug](#Configurando_hotplug)
*   [3 Testeamos la instalación](#Testeamos_la_instalación)
*   [4 Usa la cámara con tu aplicación favorita](#Usa_la_cámara_con_tu_aplicación_favorita)

## Instalar hotplug y libgphoto2

Verificar que tengamos instalados los paquetes necesarios en nuestro sistema.

```
# pacman -Q hotplug libgphoto2

```

También podemos instalar gtkam, (un front-end de gphoto2 ) a menos que desees aprender otra aplicación desde la línea de comandos.

```
# pacman -S gtkam

```

Si debes instalar los demás paquetes lo haces:

```
# pacman -S hotplug
# pacman -S libgphoto2

```

## Configurando hotplug

Abrimos una Terminal y nos logueamos como root: Creamos o añadimos al archivo usbcam.usermap tipeando:

```
# /usr/lib/libgphoto2/print-usb-usermap >> /etc/hotplug/usb/usbcam.usermap

```

libgphoto2 ofrece scripts listos para usar para hotplug. Copia el script para el acceso del grupo a la ubicación correcta.

```
# cp `locate /usr/share/libgphoto2/*/linux-hotplug/usbcam.group` /etc/hotplug/usb/usbcam

```

Puedes necesitar cambiar el path según versiones más recientes de libgphoto2\. Abrimos el nuevo archivo copiado con nuestro editor de texto favorito, por ejemplo:

```
# vi /etc/hotplug/usb/usbcam

```

Y cambiamos la línea:

```
GROUP=camera

```

A

```
GROUP=users

```

Guardamos y cerramos el fichero. Alternativamente puedes dejar el grupo fijo en camera. Solo necesitas crear el grupo:

```
# groupadd camera

```

Y los usuarios de sistema que tendrán acceso al grupo cámara.

```
# gpasswd -a username camera

```

Haces el script ejecutable:

```
# chmod +x /etc/hotplug/usb/usbcam

```

## Testeamos la instalación

Testeamos la instalación enchufando y encendiendo la cámara. Si estaba enchufada apágala y enciéndela nuevamente. Lista el contenido de /proc/bus/usb tipeando:

1.  ls -lR /proc/bus/usb

Debe haber por lo menos un dispositivo que no debe decir dos veces /root. En mi máquina, la salida muestra algo así:

```
/proc/bus/usb/004:
 total 0
 -rw-r--r--  1 root root   43 Apr 12 16:05 001
 -rw-r--r--  1 root root   43 Apr 12 16:05 002
 -rw-r--r--  1 root root   59 Apr 12 16:05 003
 -rw-r--r--  1 root root  211 Apr 12 16:05 004
 -rw-rw----  1 root users  57 Apr 12 17:58 007

```

Nótese la última línea.

## Usa la cámara con tu aplicación favorita

Puedes usar ahora gphoto2 o la reciente versión de gthumb para descargar las imágenes desde tu cámara.