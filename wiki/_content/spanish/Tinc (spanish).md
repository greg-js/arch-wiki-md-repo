**Estado de la traducción**
Este artículo es una traducción de [Tinc](/index.php/Tinc "Tinc"), revisada por última vez el **2019-10-06**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Tinc&diff=0&oldid=584511) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

**Advertencia:** se han descubierto vulnerabilidades en la versión 1.0.34 [[1]](http://tinc-vpn.org/security/). Ya hay una versión más nueva disponible en el repositorio, ¡asegúrese de actualizarla!

[tinc](http://tinc-vpn.org/) es un demonio de red privada virtual (siglas en inglés VPN) que utiliza túneles y cifrado para crear una red privada segura entre equipos en Internet.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configurar una red privada](#Configurar_una_red_privada)
    *   [2.1 Configuración de alfa](#Configuración_de_alfa)
    *   [2.2 Configuración de beta](#Configuración_de_beta)
    *   [2.3 Configuración de los equipos](#Configuración_de_los_equipos)
*   [3 Iniciar una red privada](#Iniciar_una_red_privada)
*   [4 Utilizar dispositivos TAP y puentes de red](#Utilizar_dispositivos_TAP_y_puentes_de_red)
*   [5 Iniciar Tinc automáticamente en el arranque](#Iniciar_Tinc_automáticamente_en_el_arranque)
*   [6 Solución de problemas](#Solución_de_problemas)
    *   [6.1 He actualizado mi sistema y ahora tinc no se inicia](#He_actualizado_mi_sistema_y_ahora_tinc_no_se_inicia)
    *   [6.2 Estoy ejecutando un kernel personalizado y tinc no se inicia](#Estoy_ejecutando_un_kernel_personalizado_y_tinc_no_se_inicia)
*   [7 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [tinc](https://www.archlinux.org/packages/?name=tinc).

## Configurar una red privada

En este ejemplo, crearemos una red privada virtual, *vpnname*, entre dos equipos, *alpha* y *beta*, donde el primero es el punto de entrada para el segundo, de modo que beta intente conectarse a alpha en el arranque.

Para cada red privada virtual, debe crear un directorio separado `/etc/tinc/*network*`.

También puede comenzar copiando la configuración de muestra:

```
# cp -r /usr/share/tinc/examples/* /etc/tinc/*vpnname*

```

En /etc/tinc/*vpnname*/tinc.conf especifique el nombre de la máquina del equipo (que puede diferir del nombre de equipo real del sistema) y la ubicación del dispositivo tun/tap.

### Configuración de alfa

 `/etc/tinc/*vpnname*/tinc.conf` 
```
Name = alpha
Device = /dev/net/tun
```
 `/etc/tinc/*vpnname*/tinc-up` 
```
#!/bin/sh
ip link set $INTERFACE up
ip addr add  192.168.0.1/24 dev $INTERFACE

```
 `/etc/tinc/*vpnname*/tinc-down` 
```
#!/bin/sh
ip addr del 192.168.0.1/24 dev $INTERFACE
ip link set $INTERFACE down

```

`tinc-up` y `tinc-down` deben hacerse [ejecutables](/index.php/Executable "Executable").

### Configuración de beta

 `/etc/tinc/*vpnname*/tinc.conf` 
```
Name = beta
Device = /dev/net/tun
ConnectTo = alpha
```
 `/etc/tinc/*vpnname*/tinc-up` 
```
#!/bin/sh
ip link set $INTERFACE up
ip addr add 192.168.0.2/24 dev $INTERFACE

```
 `/etc/tinc/*vpnname*/tinc-down` 
```
#!/bin/sh
ip addr del 192.168.0.2/24 dev $INTERFACE
ip link set $INTERFACE down

```

`tinc-up` y `tinc-down` deben hacerse [ejecutables](/index.php/Executable "Executable").

### Configuración de los equipos

Los archivos de configuración para los diferentes equipos se almacenan en el directorio /etc/tinc/*vpnname*/hosts/. En este ejemplo, necesitamos los dos archivos en cada máquina.

 `/etc/tinc/*vpnname*/hosts/alpha` 
```
Address = 10.0.0.1
Port = 655
Subnet = 192.168.0.1/32
```
 `/etc/tinc/*vpnname*/hosts/beta` 
```
Port = 655
Subnet = 192.168.0.2/32
```

Después de crear un archivo para cada equipo, debe generar un par de claves, utilizando:

```
# tincd -n *vpnname* -K

```

que crea la clave privada en /etc/tinc/*vpnname*/tinc.rsa_key.priv y la clave pública en el archivo del equipo correspondiente.

En el último paso, deberá intercambiar los archivos de configuración de los equipos, de modo que tanto alfa como beta en /etc/tinc/*vpnname*/hosts/ estén en cada equipo.

## Iniciar una red privada

Después de haber creado la configuración adecuada en /etc/tinc/*vpnname*, puede probar la nueva red privada con:

```
# tincd -n *vpnname*

```

Si desea activarla al inicio, debe activar el servicio apropiado:

```
# systemctl enable tinc@*vpnname*

```

## Utilizar dispositivos TAP y puentes de red

A veces es razonable usar dispositivos [TAP](https://en.wikipedia.org/wiki/es:TAP "wikipedia:es:TAP") en lugar de dispositivos [TUN](https://en.wikipedia.org/wiki/TUN/TAP "wikipedia:TUN/TAP"). Por ejemplo, si desea añadir el dispositivo tinc a un [puente de red](https://en.wikipedia.org/wiki/es:Puente_de_red "wikipedia:es:Puente de red") ya existente. Simplemente añada la opción «Mode» a tinc.conf.

Recuerde hacer esto en **cada** equipo.

 `/etc/tinc/*vpnname*/tinc.conf` 
```
Name = *node*
Mode = switch
Device = /dev/net/tun
ConnectTo = *other*
```

Los posibles archivos tinc-up/down podrían verse así:

 `/etc/tinc/*vpnname*/tinc-up` 
```
#!/bin/sh
ip link set $INTERFACE up
brctl addif *br0* $INTERFACE

```
 `/etc/tinc/*vpnname*/tinc-down` 
```
#!/bin/sh
brctl delif *br0* $INTERFACE
ip link set $INTERFACE down

```

Y finalmente [reinicie](/index.php/Restart "Restart") su demonio tinc: `tinc@*vpnname*`.

## Iniciar Tinc automáticamente en el arranque

Tinc se puede configurar para iniciarse automáticamente en el momento del arranque utilizando unidades de systemd.

Si desea poder iniciar, detener o recargar todas sus redes a la vez, debe activar el servicio tinc:

```
# systemctl enable tinc

```

Luego, para cada red que desee iniciar automáticamente, debe activarla individualmente:

```
# systemctl enable tinc@*vpnname*
# systemctl enable tinc@*another_vpnname*
...

```

## Solución de problemas

### He actualizado mi sistema y ahora tinc no se inicia

En caso de una actualización del kernel de Linux, debe reiniciar el sistema o reinstalar el paquete del kernel en ejecución.

### Estoy ejecutando un kernel personalizado y tinc no se inicia

Asegúrese de que tiene el [soporte TUN/TAP](/index.php/OpenVPN#Kernel_configuration "OpenVPN") activado.

## Véase también

*   [tincd(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tincd.8)
*   [tinc documentation](https://tinc-vpn.org/docs/)