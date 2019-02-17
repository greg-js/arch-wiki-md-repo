**Estado de la traducción**
Este artículo es una traducción de [Honeyd](/index.php/Honeyd "Honeyd"), revisada por última vez el **2019-02-15**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Honeyd&diff=0&oldid=566653) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Honeyd](http://www.honeyd.org/) es un programa de código abierto que permite a un usuario configurar y ejecutar múltiples hosts virtuales en una red informática. Estos hosts virtuales pueden configurarse para imitar varios tipos de servidores diferentes, lo que permite al usuario simular un número infinito de configuraciones de red. Honeyd se utiliza principalmente en el ámbito de la seguridad informática tanto por profesionales como por aficionados por igual.

Este artículo le explicará cómo poner en marcha una configuración sencilla. Para este ejemplo, el servidor utiliza la dirección IP 192.168.1.10\. El daemon Honeyd escuchará en 10.0.0.1.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [honeyd](https://aur.archlinux.org/packages/honeyd/).

## Configuración

Cree los siguientes archivos

 `/root/default.conf` 
```
create host
set host default tcp action reset
add host tcp port 23 "/tmp/hello.sh"

bind 10.0.0.1 host

```
 `/tmp/hello.sh` 
```
#!/bin/sh
echo "Led Zeppelin, great band or greatest band?"
while read data
do
        echo "$data"
done

```

En su firewall, agregue la siguiente ruta:

```
Destination IP 	Netmask 	Gateway
10.0.0.0	        255.0.0.0	192.168.1.10

```

Abra 2 shells en su servidor. En el primer shell, inicie Honeyd. En el segundo shell, utilize la orden `nc` para conectarse a Honeyd. Debería ver la salida que se muestra a continuación:

 `$ honeyd -d -p /usr/share/honeyd/nmap.prints -f default.conf 10.0.0.0/8` 
```
Honeyd V1.5c Copyright (c) 2002-2007 Niels Provos
honeyd[3985]: started with -d -p /usr/share/honeyd/nmap.prints -f default.conf 10.0.0.0/8
Warning: Impossible SI range in Class fingerprint "IBM OS/400 V4R2M0"
Warning: Impossible SI range in Class fingerprint "Microsoft Windows NT 4.0 SP3"
honeyd[3985]: listening promiscuously on eth0: (arp or ip proto 47 or (udp and src port 67 and dst port 68) or (ip and (net 10.0.0.0/8))) and not ether src MAC_ADDY_HERE
honeyd[3985]: Demoting process privileges to uid 99, gid 99
honeyd[3985]: Connection request: tcp (192.168.1.10:60109 - 10.0.0.1:23)
honeyd[3985]: Connection established: tcp (192.168.1.10:60109 - 10.0.0.1:23) <-> /tmp/hello.sh
honeyd[3985]: Connection dropped by reset: tcp (192.168.1.10:60109 - 10.0.0.1:23)
^Choneyd[3985]: exiting on signal 2
```
 `$ nc 10.0.0.1 23` 
```
Led Zeppelin, great band or greatest band?
greatest
greatest

^C
```

He aquí una configuración básica, sencilla, de Honeyd. Para matar Honeyd, ejecute la orden

```
killall honeyd

```

Véase el libro "Virtual Honeypots: From Botnet Tracking to Intrusion Detection" de Niels Provos para obtener más información.

## Véase también

[http://www.honeyd.org/faq.php](http://www.honeyd.org/faq.php)

[Wikipedia:Honeyd](https://en.wikipedia.org/wiki/Honeyd "wikipedia:Honeyd")

[http://ulissesaraujo.wordpress.com/2008/12/08/deploying-honeypots-with-honeyd/](http://ulissesaraujo.wordpress.com/2008/12/08/deploying-honeypots-with-honeyd/)