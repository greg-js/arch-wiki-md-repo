En esta página, trataré de hacer que la instalación de Arch en su máquina HP Pavillion, series dv1000, sea lo más sencilla posible. Si tiene algo que añadir, no dude en contribuir con esta página.

## Contents

*   [1 ¿Qué funciona?](#¿Qué_funciona?)
*   [2 ¿Qué es lo que no funciona?](#¿Qué_es_lo_que_no_funciona?)
*   [3 Instalación](#Instalación)
*   [4 Configuración](#Configuración)
    *   [4.1 Xorg y la tarjeta gráfica](#Xorg_y_la_tarjeta_gráfica)
*   [5 Módulos](#Módulos)
    *   [5.1 Conexión inhalámbrica ("Wireless")](#Conexión_inhalámbrica_("Wireless"))
    *   [5.2 Sonido](#Sonido)
*   [6 Enlaces externos](#Enlaces_externos)

## ¿Qué funciona?

La conexión Wifi utilizando los controladortes ipw2200

El control táctil ("Touchpad") utilizando los controladores synaptics

El control remoto, cuando funcionen sus teclas multimedia. El control remoto funciona desde el primer momento.

Suspensión a ram/swap

## ¿Qué es lo que no funciona?

Lector de tarjetas Texas Instruments, existe hoy día un desarrollo para hacer que funcione [aquí](http://developer.berlios.de/projects/tifmxx/) y [aquí](http://openfacts.berlios.de/index-en.phtml?title=Pcixx21_flash_media_module)

# Instalación

Arranque con el CD de Arch sin añadir ninguna opción, no necesita "acpi=off"" para este portátil. Particione a su gusto pero reserve algo más de 204 MB de espacio libre de disco **que no pertenezca a ninguna partición** para instalar más tarde Quickplay. Puede que tenga que seguir alguna guía de instalación de las quue hay en la wiki.

# Configuración

## Xorg y la tarjeta gráfica

See [Intel graphics](/index.php/Intel_graphics "Intel graphics").

# Módulos

## Conexión inhalámbrica ("Wireless")

Tiene que usar ipw2200 para hacer que su conexión wifi funcione... Así que veamos primero si su kernel puede utilizarlo

 `zcat /proc/config.gz | grep IPW2200` 

la salida debería ser algo como

 `CONFIG_IPW2200=m` 

o como

 `CONFIG_IPW2200=y` 

El kernel predeterminado de Arch puede trabajar con ipw2200

Ahora instale el paquete `ipw2200` y añada al archivo /etc/modprobe.d/modprobe.conf la siguiente línea

```
options ipw2200 led=1

```

## Sonido

El sonido funcionará desde el primer momento, asegúrese de tener instalados los paquetes `alsa-lib alsa-utils alsa-oss`, añada su usuario al grupo audio, y ya está...

--[Gandalf](/index.php/User:Gandalf "User:Gandalf") 19:30, 16 March 2006 (EST)

# Enlaces externos

*   [A Linux compatibility guide to the HP Pavillion DV1000 series](http://www.linlap.com/wiki/HP+Pavilion+dv1000)
*   Este informe aparece listado en la [Linux Laptop and Notebook Installation Guides Survey: Hewlett-Packard - HP](http://tuxmobil.org/hp.html).