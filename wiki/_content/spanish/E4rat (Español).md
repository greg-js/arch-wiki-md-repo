En e4rat se encuentra e4 'reduce el tiempo de acceso' es un proyecto de Andreas Rid and Gundolf Kiefer. La herramienta de e4rat contiene las aplicaciones de e4rat-collect, e4rat-realloc y e4rat-preload.

La versión actual es 0.2.1

## Contents

*   [1 Proceso](#Proceso)
*   [2 Quien se beneficia,Quien no se beneficia](#Quien_se_beneficia.2CQuien_no_se_beneficia)
*   [3 Instalación](#Instalaci.C3.B3n)
*   [4 Manos a la obra](#Manos_a_la_obra)
    *   [4.1 e4rat-collect](#e4rat-collect)
    *   [4.2 e4rat-realloc](#e4rat-realloc)
    *   [4.3 e4rat-preload](#e4rat-preload)
*   [5 e4rat con diferentes init system](#e4rat_con_diferentes_init_system)
*   [6 Tips and Tricks](#Tips_and_Tricks)
    *   [6.1 El archivo startup.log no es creado](#El_archivo_startup.log_no_es_creado)
    *   [6.2 e4rat reporta erroneamente un sistema de archivos ext2](#e4rat_reporta_erroneamente_un_sistema_de_archivos_ext2)

## Proceso

Si miras un [bootchart](/index.php/Bootchart "Bootchart") podrás observar que tanto el disco duro como el procesador son utilizados durante el proceso de inicio del sistema operativo. e4rat cambia esto haciendo que tanto el disco duro como el cpu sean usados durante el proceso de inicio con lo que se reduce drásticamente el tiempo de inicio. Consiste en tres etapas:

*   e4rat-collect - recolecta archivos durante un tiempo especificado (por omisión son 120 segundos esto puede ser ajustado)
*   e4rat-realloc - mueve los archivos
*   e4rat-preload - precarga los archivos

## Quien se beneficia,Quien no se beneficia

e4rat ha demostrado ser muy eficaz para el usuario que tiene una configuración que inicia directamente a las X, incluso teniendo varias aplicaciones abiertas. Si tienes un servidor con inicio y Cli el tiempo de inicio no será tan drástico. Los usuarios con unidades SSD no se benefician ya que las unidades SSD no cuentan con partes movibles y por lo tanto sin (casi) latencia de disco - [ureadahead](/index.php/Ureadahead "Ureadahead") deberías observar.

**Nota:** (A los usuarios de ureadahead) [El manual oficial de e4rat](http://e4rat.sourceforge.net/wiki/index.php/Main_Page#Ubuntu_and_ureadahead) establece conflictos entre ureadahead y e4rat. Esto es cierto para Ubunto pero ureadahead y e4rat funcionan Arch Linux, aunque el proceso de inicio no se hace más rápido.

Siempre es mejor prevenir que curar. Realiza un copia de seguridad para prevenir cualquier perdida de datos en tu partición.

## Instalación

El paquete [e4rat](https://aur.archlinux.org/packages/e4rat/) está disponible en el repositorio [Official repositories](/index.php/Official_repositories "Official repositories"):

```
# pacman -S e4rat

```

## Manos a la obra

### e4rat-collect

e4rat collect contiene una lista de archivos necesitas agregar lo siguiente a tu kernel en tu archivo `/boot/grub/menu.lst` (grub legacy) o `/boot/grub/grub.cfg` (grub2):

```
init=/sbin/e4rat-collect

```

Esto tendrás que hacerlo una vez si prefieres agregarlo desde los la línea de comandos de grub.

Después de iniciar el e4rat-collect observará el sistema por un tiempo 120 segundos. Si inicias X, abrir tu navegador favorito y cliente de email te toma 2 minutos, cada una de estas actividades será grabada. Para cambiar el tiempo predefinido de 120 segundos edita el archivo `/etc/e4rat.conf`. Para detener e4rat-collect debes escribir lo siguiente:

```
e4rat-collect -k 

```

o

```
pkill e4rat-collect

```

Si tuvo éxito en el arranque y después de haber esperado el tiempo asignado podrás ver el archivo en **`/var/lib/e4rat/startup.log`**

No olvides quitar el comando e4rat-collect de tu archivo **`menu.lst`** o **`grub.cfg`** (no es necesario si lo agregaste directamente a la línea de comando del grub).

### e4rat-realloc

Para iniciar el proceso de re-colocación cambia cambia init 1

```
sudo init 1

```

Inicia como root y ejecuta:

```
e4rat-realloc  /var/lib/e4rat/startup.log

```

Esto tomará un tiempo dependiendo cuantos archivos tienes en tu archivo startup.log.

### e4rat-preload

Agrega la siguiente línea permanente en tu línea de kernel en tu archivo `/boot/grub/menu.lst` (grub legacy) o `/boot/grub/grub.cfg` (grub2):

```
init=/sbin/e4rat-preload

```

Reinicia y a disfrutar.

## e4rat con diferentes init system

e4rat-collect por default es reemplazado por `/sbin/init` después de finalizar. Si necesitas especificar otro PID 1, por ejemplo `/bin/systemd`, puedes cambiarlo en `/etc/e4rat.conf` ajustando el parámetro '*init* y recuerda descomentar la línea.

## Tips and Tricks

Si no funciona como esperabas intenta esto.

### El archivo startup.log no es creado

*   comenta auditd en tu **`rc.conf`**
*   Comprueba la salida con:

```
dmesg | grep e4rat

```

*   Intenta aumentando el nivel de información a 31 en el archivo **`e4rat.conf`**

### e4rat reporta erroneamente un sistema de archivos ext2

*   Agrega lo siguiente a tu línea del kernel en tu **`grub.cfg`** o **`menu.lst`**

```
rootfstype=ext4

```