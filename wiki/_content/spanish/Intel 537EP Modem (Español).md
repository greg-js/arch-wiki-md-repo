El módem Intel 537EP es en realidad un winmodem, por lo que parte del trabajo lo hace el sistema operativo.

Originalmente esta pensado para ser usado en Sistemas con Microsoft Windows (MR), por lo que la gente de Intel (MR) diseño los drivers respectivos para otros Sistemas Operativos, incluido GNU/Linux(MR). Esto nos permite tener una serie de herramientas creadas desde fabrica y disponibles con su código fuente.

Es importante aclarar que estos drivers para linux no son GPL, sino Propietarios.

Entre los paquetes disponibles para Arch Linux existen cuatro ( son seis en realidad), que permiten disponer de drivers necesarios y utilidades para el Intel 536EP y el Intel 537 que no nos sirven para este módem en particular, Para eso he escrito esta Guia.

## Contents

*   [1 A tener en cuenta](#A_tener_en_cuenta)
*   [2 Principios de funcionamiento del driver](#Principios_de_funcionamiento_del_driver)
*   [3 Que nos provee el driver descargado](#Que_nos_provee_el_driver_descargado)
*   [4 Como Gestiona Todo Arch Linux](#Como_Gestiona_Todo_Arch_Linux)
*   [5 Compilar e Instalar Todo](#Compilar_e_Instalar_Todo)
*   [6 Algunos Detalles](#Algunos_Detalles)

## A tener en cuenta

La gente de Intel ha diseñado [un driver](http://downloadfinder.intel.com/scripts-df/filter_results.asp?strOSs=39&strTypes=DRV&ProductID=1230&OSFullName=Linux*&submit=Go!) , que permite su uso en kernels 2.4 o 2.6, pero en este ultimo tendremos algunos inconvenientes en varias versiones, es decir 2.6.9, 2.6.10, 2.6.11, 2.6.16\. Para ello podríamos aplicar distintos parches.

Existe además una web muy buena para configurar winmodems que [es aqui](http://linmodems.org), esta web posee una lista de correo en ingles que suele contar con el aporte de distintos usuarios que proveen los parches o correcciones al driver original. Entre estas correcciones un usuario generó un driver modificado que podemos encontrar en [este sitio](http://linmodems.technion.ac.il/packages/Intel/Philippe.Vouters/), nos interesa el que dice secure, el driver si bien no es la última versión respecto a la publicada en Intel, funciona en el kernel 2.6.16.9 que estoy usando.

Si usamos el kernel original de Arch Linux, es decir el 2.6.15-arch, podemos usar el de Intel, si usamos el current, el 2.6.16.9 conviene usar el de Phiilippe Vouters.

Dentro de los paquetes de Arch Linux hay uno llamados intel-537-utils.pkg.tar.gz, si bien no nos sirven, podemos usarlo, personalmente no los uso, y la idea de esta guia es explicar el funcionamiento de manera independiente de estos paquetes.

Si tenemos duda sobre el módem en particular, podemos descargar desde linmodems una utilidad llamada scanmodem y correrla en nuestra máquina linux que nos proveerá de mucha información que puede servirnos.

## Principios de funcionamiento del driver

El driver crea un módulo llamado Intel537 que nos permite trabajar con nuestro módem. luego de levantarse debemos crear un dispositivo /dev/537 o /dev/5370 en el sistema, podemos crear los dos inclusive, este último lo crea el udevd. Creamos el link a /dev/modem y configuramos nuestra conexión. Así de simple es todo.

## Que nos provee el driver descargado

Cuando descargamos el driver, tendremos el código fuente necesario para construir nuestro /dev/537 y una serie de utilidades como hamregistry, o usrsound ( en la versión de Vouters), además de tres scripts, uno llamado 537_boot, otro 537_inst y el config_check. Además un archivo que nos hará falta ver, el readme.txt.

De los archivos provistos, el único que deberemos usar es el readme.txt, el resto es opcional y básicamente nos permite: hamregistry, sirve para indicarle al módem algunos detalles como el tipo del módem, el usrsound es una aplicación que nos permite escuchar los ruidos de conexión del módem, esta aplicación causa muchos problemas por ello en las nuevas versiones del driver de Intel, no se agrega; el 537_boot provee un script que se añade en el directorio de demonios ( /etc/rc.d, por ejemplo) en algunos sistemas como Slackware, Red Hat, y demás. En nuestro caso no nos sirve, hay un archivo en el paquete utils de los otros módems ( Intel 537, Intel 536EP) pero sirve para inicializar el hamregistry. Podemos usarlo también. Otro archivo es 537_inst que suele instalar el módulo y configurar todo automáticamente, al ser Arch Linux una distribución que no esta incluida en este script suele dar error. En realidad no nos sirve mucho. La otra es config_check que verifica que las fuentes del kernel existan. En Arch Linux las fuentes o elementos necesarios forman parte del kernel instalado asi que....

## Como Gestiona Todo Arch Linux

En el caso particular de Arch Linux, el método usado por el sistema es muy simple.

Lo fundamental es que para agregar el módulo en /etc/rc.conf, y si vamos a usar el intel-537 de las utils en la sección de daemons ( del paquete intel-537-utils.pkg.tar.gz). luego de copiar este archivo ( intel-537) a /etc/rc.d. Cualquier comando para crear el /dev/537 o el link se agrega a /etc/rc.local. La herramienta udev suele crear un dispositivo llamado /dev/5370 por lo que todo se resume a crear el link a /dev/modem. Si usamos wvdial para conectarnos a nuestro ISP, deberemos crear un link a /dev/ttyS4 o similar ( ver directorio /dev), ya que no reconoce ni el /dev/537, /dev/5370 o /dev/modem.

## Compilar e Instalar Todo

Sabiendo lo referente a que hay en el driver y como gestiona todo Arch Linux vamos a lo realmente importante.

Según el readme.txt el proceso se hace en tres pasos, pero nosotros solo usaremos dos. El readme.txt indica:

```
make clean
make 537
make install

```

El primero borra si hay compilación anterior, el make 537 crea el Intel537 y el make install instalará todo, este lo obviaremos por que suele dar error y en realidad lo hacemos a nuestra manera.

El más importante aquí es el make 537 que será quien construya el módulo respectivo, el proceso es simple, verifica que este la fuente del kernel y luego construye el módulo. Suele pasar que el driver de Intel indique algunos mensajes que suelen deberse a temas simplemente sintácticos del código, el de Vouters, no indica mensajes. Lo importante es que no detenga todo por algún error. Si usamos el de Intel en el kernel 2.6.16.x nos dará error por una variable que fue eliminada en los kernels desde el 2.6.16-rc2, el driver de Vouters soluciona este detalle.

Para instalar todo simplemente copiamos Intel537.ko a /lib/modules/<version-kernel>/kernel/drivers/net/ y luego hacemos depmod -a para actualizar la base de datos de módulos. Si queremos ver si se levanta el módulo sin error, ponemos:

```
#insmod ./Intel537.ko

```

en el directorio de las fuentes del módem y vemos si está con lsmod, si hay error lo indica. Después solo lo agregamos en /etc/rc.conf.

El módulo admite opciones, es decir si queremos habilitar los sonidos ( sin usrsound, no tendría sentido, pero...) podemos agregar en /etc/modprobe.conf la línea:

```
options Intel537 sound_enabled=1

```

Si leemos el 537_boot en las fuentes del módem, veremos que luego de levantar el módulo suele crear el dispositivo, esto se hace en nuestro caso añadiendo la línea:

```
mknod /dev/537 c 240 1

```

al /etc/rc.local para que el dispositivo sea creado al inicio de nuestro sistema. El udev suele crear el dispositivo llamándolo /dev/5370\. Dentro del /etc/rc.local agregamos la creación de los links y estará listo para configurar nuestra conexión a Internet.

El driver también provee una utilidad llamada hamregistry, esta utilidad permite pasarle al módem algunos datos, podemos usarla agregándola a /etc/rc.local, pero primero debemos copiarla a /usr/sbin y crear el archivo de configuración en /etc/hamregistry.bin, para ello en readme.txt esta muy bien documentado, por ejemplo use:

```
hamregistry & 

```

esto creo un archivo /etc/hamregistry.bin por defecto.

Luego agregamos a /etc/rc.local la línea hamregistry & y listo.

## Algunos Detalles

El módem suele tener una velocidad de descarga de 5,0 k/b en promedio, funciona muy bien, pero hay casos en que no logra velocidades muy altas, suele tener un promedio de 2,9 k/s. La solución proveida en la lista de linmodems, fue parchear el archivo coredrv/rts.c de los drivers del módem.

El parche es:

```
diff -urN Intel-536.orig/coredrv/rts.c Intel-536/coredrv/rts.c
--- Intel-536.orig/coredrv/rts.c 2005-07-26 17:59:33.000000000
+0200
+++ Intel-536/coredrv/rts.c 2005-09-22 09:59:27.000000000 +0200
@@ -220,7 +220,7 @@
#if LINUX_VERSION_CODE <= KERNEL_VERSION(2,6,0)
rs_timer.expires = jiffies + 1;
#else
- rs_timer.expires = jiffies + 10;
+ rs_timer.expires = jiffies + CONFIG_HZ/100;
#endif
add_timer(&rs_timer);
}

```

Como se observa es para el módem 536EP, pero puede aplicarse en nuestro caso con algunos detalles a considerar, primeramente se ve que se modifica una línea del código, por lo que esta puede hacerse directamente en el código de nuestro driver. En el caso de la versión de Intel, la modificación se aplica en la línea 223, en la versión de Vouters está en la 224\. Luego tendremos nuestro módem normal.

El readme.txt también comenta algunos detalles con el uso del wvdial que debemos tener presente si usamos esta aplicación.

Para lograr nuestra conexión debemos indicarle a módem el país desde donde nos conectamos, estos datos están en el readme.txt y se usa entre los script de inicio del módem el comando AT+GCI=<nº-país>. Por ejemplo, para la Republica Argentina sería:

```
AT+GCI=07

```

Como modo normal para verificar el proceso de conexión, suelo ver la salida de /var/log/messages.log.

Tengo una web donde se explica como configuré el módem en Slackware que quizás sirva, en [este sitio](http://ar.geocities.com/javara2305/config_modem.html), por si hace falta.