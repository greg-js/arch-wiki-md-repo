Artículos relacionados

*   [fail2ban](/index.php/Fail2ban "Fail2ban")
*   [Secure Shell (Español)](/index.php/Secure_Shell_(Espa%C3%B1ol) "Secure Shell (Español)")

**Estado de la traducción**
Este artículo es una traducción de [Sshguard](/index.php/Sshguard "Sshguard"), revisada por última vez el **2018-09-03**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Sshguard&diff=0&oldid=513055) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

**Advertencia:** Utilizar de una lista negra de IP detendrá ataques triviales, pero esto le supondrá el uso de un demonio adicional y de un registro fiable (la partición donde esté /var puede llenarse, especialmente si un atacante está golpeando el servidor). Además, con el conocimiento de su dirección IP, el atacante puede enviar paquetes con un encabezado de fuente falsificado y bloquearlo fuera del servidor. [SSH keys](/index.php/SSH_keys "SSH keys") le ofrece una solución elegante al problema del ataque de fuerza bruta, sin tantos inconvenientes.

[sshguard](http://www.sshguard.net) es un demonio que protege a [SSH](/index.php/SSH "SSH") y otros servicios contra los ataques de fuerza bruta, similar a [fail2ban](/index.php/Fail2ban "Fail2ban").

sshguard es diferente de este último en cuanto que está escrito en C, es más ligero y más simple de usar y con menos características, mientras realiza la función que se espera de él igual de bien.

sshguard no es vulnerable a la mayoría (o, tal vez, a ninguno) de los análisis de registros, [vulnerabilidades](https://web.archive.org/web/20120625102244/http://www.ossec.net/main/attacking-log-analysis-tools) que han causado problemas para aplicaciones similares.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Ajustes](#Ajustes)
    *   [2.1 FirewallD](#FirewallD)
    *   [2.2 UFW](#UFW)
    *   [2.3 iptables](#iptables)
    *   [2.4 nftables](#nftables)
*   [3 Utilización](#Utilizaci.C3.B3n)
    *   [3.1 systemd](#systemd)
    *   [3.2 syslog-ng](#syslog-ng)
*   [4 Configuración](#Configuraci.C3.B3n)
    *   [4.1 Umbral de la lista negra](#Umbral_de_la_lista_negra)
    *   [4.2 Ejemplo moderado de baneado](#Ejemplo_moderado_de_baneado)
    *   [4.3 Baneado agresivo](#Baneado_agresivo)
*   [5 Consejos y trucos](#Consejos_y_trucos)
    *   [5.1 Desbloquear](#Desbloquear)
        *   [5.1.1 iptables](#iptables_2)
        *   [5.1.2 nftables](#nftables_2)
    *   [5.2 Registro](#Registro)

## Instalación

[Instale](/index.php/Install "Install") el paquete [sshguard](https://www.archlinux.org/packages/?name=sshguard).

## Ajustes

sshguard funciona monitorizando `/var/log/auth.log`, syslog-ng o el [journal de systemd](/index.php/Systemd_journal "Systemd journal") para intentos fallidos de inicio de sesión. Para cada intento fallido, el servidor infractor tiene prohibido continuar comunicándose con nuestro equipo durante un tiempo limitado. La cantidad de tiempo predeterminada que el atacante está baneado comienza en 120 segundos, y se incrementa en un factor de 1,5 cada vez que falla en otro intento de iniciar sesión. sshguard se puede configurar para prohibir permanentemente un servidor del que se tienen registrados demasiados intentos fallidos.

Las prohibiciones temporales y permanentes se realizan añadiendo una entrada en la cadena («*chain*») «sshguard» en iptables que descarta todos los paquetes del atacante. La prohibición se registra en syslog y termina en `/var/log/auth.log`, o en el journal de systemd, si se está utilizando este último.

Debe configurar uno de los siguientes cortafuegos para usarlo con sshguard para que funcione el bloqueo.

#### FirewallD

sshguard puede funcionar con Firewalld. Asegúrese, primero, de activar y configurar Firewalld. Para hacer que sshguard escriba en su zona de preferencia, emita las siguientes órdenes:

```
# firewallctl zone "<nombre_de_la_zona>" --permanent add rich-rule "rule source ipset=sshguard4 drop"

```

Si usa ipv6, puede emitir la misma orden pero sustituyendo sshguard4 con sshguard6\. Se terminaría con:

```
# firewall-cmd --reload

```

Puede verificar lo anterior con:

```
# firewall-cmd --info-ipset=sshguard4

```

Finalmente, en /etc/sshguard.conf, busque la línea para BACKEND y cámbiela de la siguiente manera

```
BACKEND="/usr/lib/sshguard/sshg-fw-firewalld"

```

#### UFW

Si UFW está instalado y activado, se le debe dar la capacidad de pasar el control de DROP a sshguard. Esto se logra modificando `/etc/ufw/before.rules` para que contenga las líneas de abajo, que se deben insertar justo después de la sección para los dispositivos loopback.
**Nota:** Los usuarios que ejecuten sshd en un puerto no estándar, deben sustituir el mismo en la línea final anterior (donde 22 es el estándar).
 `/etc/ufw/before.rules` 
```
# permitir todo en loopback
-A ufw-before-input -i lo -j ACCEPT
-A ufw-before-output -o lo -j ACCEPT

# entregar el control de sshd a sshguard
-N sshguard
-A ufw-before-input -p tcp --dport 22 -j sshguard

```

[Reinicie](/index.php/Restart "Restart") ufw después de hacer esta modificación.

#### iptables

**Nota:** Consulte primero [iptables](/index.php/Iptables "Iptables") y [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall") para configurar un cortafuegos.

Lo principal que requiere la configuración es crear una cadena llamada `sshguard`, donde sshguard inserta automáticamente reglas para descartar paquetes de red provenientes de servidores peligrosos:

```
# iptables -N sshguard

```

A continuación, hay que agregar una regla para saltar desde la cadena `INPUT` a la cadena `sshguard`. Esta regla debe añadirse **antes** de cualquier otra regla que procese los puertos que sshguard protege. Utilice la siguiente línea para proteger FTP y SSH, o vea [esta documentación](http://www.sshguard.net/docs/setup/#netfilter-iptables) para más ejemplos.

```
# iptables -A INPUT -m multiport -p tcp --destination-ports 21,22 -j sshguard

```

Para guardar las reglas:

```
# iptables-save > /etc/iptables/iptables.rules

```

**Nota:** Para IPv6, repita los mismos pasos con *ip6tables* y guarde las reglas con *ip6tables-save* en `/etc/iptables/ip6tables.rules`.

#### nftables

Edite `/etc/sshguard.conf` y cambie el valor de `BACKEND` como sigue:

 `/etc/sshguard.conf`  `BACKEND="/usr/lib/sshguard/sshg-fw-nft-sets"` 

Además, necesitará [editar](/index.php/Edit "Edit") el servicio `sshguard.service` para que [iptables](/index.php/Iptables_(Espa%C3%B1ol) "Iptables (Español)") no se ejecute:

```
[Service]
ExecStartPre= 

```

Cuando [inicie/active](/index.php/Start/enable "Start/enable") el servicio `sshguard.service`, se agregararán dos nuevas tablas llamadas `sshguard` en las familias de direcciones `ip` y `ip6`, que filtran el tráfico entrante a través de la lista de direcciones IP de sshguard. Las cadenas en la tabla `sshguard` tienen una prioridad de -10 y, por tanto, se procesarán antes que otras reglas de menor prioridad. Consulte [7 sshguard-setup( 7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sshguard-setup.) y [nftables](/index.php/Nftables "Nftables") para obtener más información.

## Utilización

### systemd

[Active](/index.php/Enable "Enable") e [inicie](/index.php/Start "Start") `sshguard.service`.

### syslog-ng

Si tiene [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng) instalado, puede iniciar sshguard directamente desde la línea de órdenes.

```
/usr/sbin/sshguard -l /var/log/auth.log -b /var/db/sshguard/blacklist.db

```

## Configuración

La configuración se realiza en el archivo `/etc/sshguard.conf`, necesario para que *sshguard* se inicie. Un ejemplo comentado se encuentra en `/usr/share/doc/sshguard/sshguard.conf.sample`.

**Nota:** Las órdenes de tuberías y los indicadores de tiempo de ejecución en las unidades de systemd para *sshguard* [no son compatibles](https://sourceforge.net/p/sshguard/mailman/message/35709860/). Tales indicadores se pueden modificar en el archivo de configuración.

### Umbral de la lista negra

De forma predeterminada, en el archivo de configuración proporcionado por Arch, los atacantes quedan permanentemente prohibidos una vez que alcanzan un nivel de «peligro» de 120 (o 12 intentos de inicios de sesión fallidos —consulte [attack dangerousness](https://www.sshguard.net/docs/terminology/#attack-dangerousness) para más detalles—). Este comportamiento puede modificarse anteponiendo un nivel de peligro distinto en el archivo de la lista negra.

```
BLACKLIST_FILE=200:/var/db/sshguard/blacklist.db

```

El nivel `200:` en este ejemplo, le dice a sshguard que bloquee permanentemente un servidor después de alcanzar un nivel de peligro de 200.

Finalmente [reinicie](/index.php/Restart "Restart") `sshguard.service`.

### Ejemplo moderado de baneado

He aquí una regla de prohibición ligeramente más agresiva que la predefinida, para ilustrar otras opciones. Fiscalizamos [sshd](/index.php/Sshd "Sshd") y [vsftpd](/index.php/Vsftpd "Vsftpd") a través de los registros del *journal de systemd*. Bloqueamos a los atacantes después de 2 intentos durante 180 segundos y el tiempo de bloqueo posterior aumentará en un factor de 1,5\. Tenga en cuenta que esta función de retraso multiplicativo es interna y no está controlada por la configuración siguiente. Los atacantes son recordados durante 3600 segundos y permanecen en la lista negra después de 10 intentos (10 intentos con un costo de 10 cada uno, lo que explica el parámetro «100» en la configuración de la lista negra). Bloqueamos no solo la IP del atacante, sino también toda la subred IPv4 24 (notación [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing "wikipedia:Classless Inter-Domain Routing")).

```
BACKEND="/usr/lib/sshguard/sshg-fw-iptables"
LOGREADER="LANG=C /usr/bin/journalctl -afb -p info -n1 -t sshd -t vsftpd -o cat"
THRESHOLD=20
BLOCK_TIME=180
DETECTION_TIME=3600
BLACKLIST_FILE=100:/var/db/sshguard/blacklist.db
IPV4_SUBNET=24

```

### Baneado agresivo

Para algunos usuarios sometidos a ataques constantes, se puede adoptar una política de prohibición más agresiva. Si está seguro de que los intentos de inicios de sesión fallidos son poco probables que sean accidentales, puede indicar a SSHGuard que prohíba permanentemente los servidores después de un solo intento de inicio de sesión fallido. Modifique los parámetros en el archivo de configuración de la siguiente manera:

```
THRESHOLD=10
BLACKLIST_FILE=10:/var/db/sshguard/blacklist.db

```

Finalmente [reinicie](/index.php/Restart "Restart") `sshguard.service`.

Además, para evitar múltiples intentos de autenticación durante una sola conexión, es posible que desee cambiar `/etc/ssh/sshd_config` definiendo:

```
MaxAuthTries 1

```

[Reinicie](/index.php/Restart "Restart") `sshd.service` para que este cambio surta efecto.

## Consejos y trucos

### Desbloquear

Si la prohibición de una IP la realiza *usted mismo*, puede esperar a que se desbloquee automáticamente o puede utilizar iptables o nftables para destrabarla.

#### iptables

Primero compruebe si la IP está baneada por sshguard:

```
# iptables --list sshguard --line-numbers --numeric

```

A continuación, utilice la siguiente orden para desbloquearla, con el número de línea obtenido de la orden anterior:

```
# iptables --delete sshguard *line-number*

```

También deberá eliminar la dirección IP de `/var/db/sshguard/blacklist.db` para que el desbloqueo sea persistente.

#### nftables

Elimine la dirección IP del conjunto de `attackers`:

```
# nft delete element *family* sshguard attackers { *ip_address* }

```

donde `*family*` es `ip` o `ip6`.

### Registro

Para ver qué se pasa a través de sshguard, examine el script en `/usr/lib/systemd/scripts/sshguard-journalctl` y el servicio de systemd `sshguard.service`. Puede utilizar una orden equivalente para ver los registros en el terminal:

```
$ journalctl -afb -p info SYSLOG_FACILITY=4 SYSLOG_FACILITY=10

```