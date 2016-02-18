**Advertencia:** Port knocking debe ser usado como parte de una estrategia de seguridad, no como la unica proteccion. Eso seria un fragil sistema de [Seguridad mediante obscuridad](https://en.wikipedia.org/wiki/Security_through_obscurity "wikipedia:Security through obscurity"). En caso de proteccion SSH, vea [SSH keys](/index.php/SSH_keys "SSH keys") por un metodo fuerte que se puede usar junto con port knocking.

Port knocking (Tocar puertos) es un metodo discreto de abrir puertos que, por default, el firewall mantiene cerrado. Funciona requiriendo intentos de conexion a una serie de puertos predefinidos cerrados. Cuando la sequencia correcta de "toquidos" a puertos (intentos de coneccion) es recibida, el firewall abre entonces cierto(s) puerto(s).

El beneficio es que, en un escaneo de puertos normal, pareceria que el servicio del puerto simplemente no esta disponible.

Una sesion con port knocking podria lucir asi:

```
$ ssh usuario@servidor # No hay respuesta (Ctrl+c para salir)
^C
$ nmap -PN --host_timeout 201 --max-retries 0  -p 1111 servidor #tocando el puerto 1111
$ nmap -PN --host_timeout 201 --max-retries 0  -p 2222 servidor #tocando el puerto 2222
$ ssh usuario@servidor # Ahore si esta permitido logearse
usuario@servidor's password:

```

## Contents

*   [1 Instalacion](#Instalacion)
*   [2 Metodo con daemon](#Metodo_con_daemon)
*   [3 Metodo con solo-iptables](#Metodo_con_solo-iptables)
    *   [3.1 reglas de iptables](#reglas_de_iptables)
    *   [3.2 Script de port knocking](#Script_de_port_knocking)
*   [4 Advertencia](#Advertencia)

## Instalacion

Necesitas tener [iptables](https://www.archlinux.org/packages/?name=iptables) instalado, lee la pagina de la wiki de [iptables](/index.php/Iptables "Iptables") para mas detalles.

[Instala](/index.php/Pacman "Pacman") el paquete [iptables](https://www.archlinux.org/packages/?name=iptables) desde los [repositorios oficiales](/index.php/Official_repositories "Official repositories").

A continuacion, agrega `iptables` a la [lista de DAEMONS](/index.php/Daemon "Daemon") en `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")` para que carge tu configuracion al inicio:

 `/etc/rc.conf` 
```
...

DAEMONS=(... **iptables** network ...)
```

## Metodo con daemon

Puedes usar un daemon para que haga todo el trabajo por ti. En **Simple stateful firewall**[[1]](https://wiki.archlinux.org/index.php/Simple_stateful_firewall#Port_Knocking) puedes leer un metodo para eso.

## Metodo con solo-iptables

### reglas de iptables

El modulo **recent** en iptables es usado para crear una lista dinamico de direcciones ip basadas en sus (existosas o no) conexiones a puertos.

Usando **recent** podemos averiguar si cierta IP a tocado los puertos correctos y, si el el caso, abrir cierto(s) puerto(s).

A continuacion se representa el contenido de un archivo `iptables.rules` . En este ejemplo, el puerto para ser abierto es el 22 (default para SSH) Este ejemplo tiene comentarios que explican como funciona.

 `/etc/iptables/iptables.rules` 
```
*filter
 :INPUT ACCEPT [0:0]
 :FORWARD ACCEPT [0:0]
 :OUTPUT ACCEPT [0:0]
 :TRAFFIC - [0:0]
 :SSH-INPUT - [0:0]
 :SSH-INPUTTWO - [0:0]
 -A INPUT -j TRAFFIC
 -A FORWARD -j TRAFFIC

 # Conexiones aceptadas por default

 -A TRAFFIC -i lo -j ACCEPT
 -A TRAFFIC -s 192.168.0.0/24 -j ACCEPT
 -A TRAFFIC -p icmp --icmp-type any -j ACCEPT
 -A TRAFFIC -m state --state ESTABLISHED,RELATED -j ACCEPT
 -A TRAFFIC -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT
 -A TRAFFIC -m state --state NEW -m tcp -p tcp --dport 443 -j ACCEPT

 # Port Knocking -- la secuencio correcta es 8881 -> 7777 -> 9991;  cualquier otra secuencia cerrara el puerto 22

 # Si la ip esta en la lista SSH2, el puerto 22 estara abierto por 30 segundos,
 # despues de eso, se cerrara de nuevo (pero solo para conexiones nuevos, las ya establecidas no se cerraran)
 -A TRAFFIC -m state --state NEW -m tcp -p tcp --dport 22 -m recent --rcheck --seconds 30 --name SSH2 -j ACCEPT

 # Ahora borramos la ip de la lista SSH2 (si esta presente)
 -A TRAFFIC -m state --state NEW -m tcp -p tcp -m recent --name SSH2 --remove -j DROP

 # Esto llama a SSH-INPUTTWO si la ip esta presente en la lista SSH1 y el puerto tocado es 9991
 -A TRAFFIC -m state --state NEW -m tcp -p tcp --dport 9991 -m recent --rcheck --name SSH1 -j SSH-INPUTTWO

 # Ahora borramos la ip de la lista SSH1 (si esta presente)
 -A TRAFFIC -m state --state NEW -m tcp -p tcp -m recent --name SSH1 --remove -j DROP

 # Esto llama a SSH-INPUT si la ip esta presente en la lista SSH0 y el puerto tocado es 7777
 -A TRAFFIC -m state --state NEW -m tcp -p tcp --dport 7777 -m recent --rcheck --name SSH0 -j SSH-INPUT

 # Ahora borramos la ip de la lista SSH0 (si esta presente)
 -A TRAFFIC -m state --state NEW -m tcp -p tcp -m recent --name SSH0 --remove -j DROP

 # Esto agrega la ip a la lista SSH0 si el puerto tocado es 8881
 -A TRAFFIC -m state --state NEW -m tcp -p tcp --dport 8881 -m recent --name SSH0 --set -j DROP

 # SSH-INPUT agrega la ip a la lista SSH1 
 -A SSH-INPUT -m recent --name SSH1 --set -j DROP

 # SSH-INPUTTWO agrega la ip a la lista SSH2
 -A SSH-INPUTTWO -m recent --name SSH2 --set -j DROP 

 # El resto del trafico es rechazado
 -A TRAFFIC -j DROP
 COMMIT
 # puedes agregar reglas nat, etc aqui
```

**Nota:** Por razones de seguridad, los puertos `8881`, `7777` y `9991` usados en el ejemplo anterior deben ser cambiados. Por favor, use un set unico de numeros de puertos.

### Script de port knocking

Ahora podemos usar un simple shell script (`knock.sh`) para que los toque:

 `knock.sh` 
```
#!/bin/bash
HOST=$1
shift
for ARG in "$@"
do
        nmap -PN --host_timeout 201 --max-retries 0 -p $ARG $HOST
done
```

Aqui esta como funcionaria el script:

```
$ ssh username@hostname # No hay respuesta (Ctrl+c para salir)
^C
$ sh knock.sh hostname 8881 7777 9991
$ history -r
$ ssh username@hostname # Ahora esta permitido logearse
username@hostname's password:

```

## Advertencia

La segurida obtenida por usar la informacion anterior, no puede ser garantizada. Esto solo es una forma de enmascarar en servicio en cierto puerto. Otras medidas de seguridad deben ser usadas. Si decide usar la informacion anterior para cualquier proposito, es bajo su propio riesgo.