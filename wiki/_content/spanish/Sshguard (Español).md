[sshguard](http://www.sshguard.net) es un demonio que para prteger [SSH](/index.php/SSH "SSH") y otros servicios contra ataques de fuerza bruta, es similiar a [fail2ban](/index.php/Fail2ban "Fail2ban").

Sshguard es diferente, por que esta escrito en C, es liviano y simple de usar, tiene varias caracteristicas. No es vulnerable a la mayoria de los analisis de logs [vulnerabilidades de analisis de logs](http://www.ossec.net/main/attacking-log-analysis-tools), que les han causado problemas a herramientas similares.

## Contents

*   [1 Instalacion](#Instalacion)
*   [2 Configuracion](#Configuracion)
*   [3 Informacion general](#Informacion_general)
*   [4 Lea tambien](#Lea_tambien)

## Instalacion

Primero, instale [iptables](/index.php/Iptables "Iptables") para que sshguard pueda bloquear host remotos:

```
# pacman -S iptables

```

Luego, instale [sshguard](https://www.archlinux.org/packages/?name=sshguard):

```
# pacman -S sshguard

```

## Configuracion

Sshguard no tiene un archivo de configuracion. Toda configuracion que se debe hacer es crear una cadena llamada "sshguard" en la ENTRADA de cadenas de iptables donde sshguard es agregado automaticamente a las reglas, para deshacerse de los paquetes provenientes de host ofensivos:

```
# iptables -N sshguard
# iptables -A INPUT -j sshguard
# /etc/rc.d/iptables save

```

Si no usa iptables regularmente y solo quiere correr sshguard sin algun impacto adicional en su equipo, estos comandos crearan y guardaran una configuracion para iptables que solo habilitaran a sshguard para trabajar:

```
# iptables -F
# iptables -X
# iptables -P INPUT ACCEPT
# iptables -P FORWARD ACCEPT
# iptables -P OUTPUT ACCEPT
# iptables -N sshguard
# iptables -A INPUT -j sshguard
# /etc/rc.d/iptables save

```

Para mas informacion sobre el uso de iptables y la creacion de un buen firewall, revise [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall").

Finalmente, agregue iptables y sshguard a los DEMONIOS en `/etc/rc.conf`:

```
DAEMONS=(... iptables sshguard ...)

```

## Informacion general

Sshguard funciona observando los cambios en `/var/log/auth.log`, verifica si alguien esta fallando al autentificarse varias veces.Tambien se puede configurar para que obtenga la informacion directamente de syslog-ng. Luego de varios errores de autentificacion (por defecto son 14) el host ofensivo sera proscripto por un tiempo limitado. El tiempo es de 7 minutos y se duplica cada vez que el host ofensivo es repita el ataque. Por defecto en el paquete de archlinux, el host ofensivo es proscripto en el primer ataque.

Las proscripciones se realizan agregando una entrada en la cadena "sshguard" dentro de iptables, y rechazan todo paquete del atacante. Para hacer que la proscripcion solo al puerto 22, simplemente no en cargue otros puertos en la cadena "sshguard"

Cuando sshguard proscribe a alguien, la proscripcion es cargada en syslog y termina en `/var/log/auth.log`.

Desde que dejo de haber archivo de configuracion, todas las configuracions se hacen via linea de comandos donde sshguard se ah iniciado. En archlinux podemos modificar este comportamiento, editando `/etc/rc.d/sshguard`. Por defecto, la linea donde se inicia el programa es:

```
tail -n0 -F /var/log/auth.log | /usr/sbin/sshguard -b /var/db/sshguard/blacklist.db &> /dev/null &

```

En la configuracion origina, _tail_ lee la informacion de las autentificaciones y se las envia a sshguard. Otro cosa a tener en cuenta es que la opcion -b esta seindo usada, lo que hace las proscripciones permamentes. Los registros de las proscripciones permanentes se guardan en `/var/db/sshguard/blacklist.db` para ser recordadas en cada inicio.

Esta linea habilita el lector de autentificaciones integrado (llamado _Log Sucker_) en vez de _tail_, pero no guardara las proscripciones permanentes:

```
/usr/sbin/sshguard -l /var/log/auth.log &> /dev/null &

```

## Lea tambien

*   [fail2ban](/index.php/Fail2ban "Fail2ban")