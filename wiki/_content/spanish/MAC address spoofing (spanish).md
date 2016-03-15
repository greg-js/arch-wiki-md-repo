Existen dos métodos para falsear una dirección MAC (Media Access Control) en Arch. Ambas se describen a continuación

**Warning:** Cambiar las opciones de red usualmente requiere privilegios especiales. Así que necesitaras trabajar como root

## Contents

*   [1 Método 1: macchanger](#M.C3.A9todo_1:_macchanger)
*   [2 Método 2: Manual](#M.C3.A9todo_2:_Manual)
*   [3 Spoofing MAC On Boot](#Spoofing_MAC_On_Boot)
*   [4 Enlaces y Referencias](#Enlaces_y_Referencias)

## Método 1: macchanger

Este método usa [macchanger](http://www.alobbs.com/macchanger) (a.k.a., the GNU MAC Changer), escrito por Alvaro Lopez Ortega. Provee una variedad de características como cambiar la dirección para que coincida con un determinado proveedor o completamente aleatoria. El primer paso es descargarlo desde [extra]

```
# pacman -S macchanger

```

Después de esto, la MAC puede ser falseado con una dirección aleatoria. La sintaxis de uso es "macchanger -r <device>". Los nombres estándar para los dispositivos son eth0 (para Ethernet) y wlan0 (para inalámbrica), si solo un dispositivo de cada tipo esta conectado. Para un dispositivo secundario, se llamaría eth1 o wlan1.

Este es un comando de ejemplo para falsear una dirección MAC en un dispositivo llamado eth0

```
# macchanger -r eth0

```

Para aleatorizar la dirección excepto los bytes del proveedor (esto es, si la dirección MAC fuera revisada, esta seguiría siendo registrada del mismo proveedor), debes utilizar el comando:

```
# macchanger -e eth0

```

Finalmente, para cambiar la dirección MAC a un valor especifico:

```
# macchanger --mac=XX:XX:XX:XX:XX:XX

```

Donde 'XX:XX:XX:XX:XX:XX' es la dirección MAC que deseas utilizar.

**Note:** Un dispositivo no puede estar en uso mientras se realiza el cambio de dirección MAC.

## Método 2: Manual

Este método también asume que el nombre dispositivo es eth0\. Para clarificación, lea el segundo párrafo del Método 1.

Primero, puedes comprobar tu dirección MAC con el siguiente comando:

```
# ip link show eth0

```

La sección que nos interesa en este momento es la que tiene por nombre "HWaddr" seguido por un número de 6-bytes. Probablemente se vea así:

```
link/ether 00:1d:98:5a:d1:3a

```

El primer paso para falsear la dirección MAC es detener la interfaz. Debes estar logeado como root o utilizar sudo.

```
# ip link set dev eth0 down

```

Ahora podremos realmente falsear nuestra MAC. Cualquier valor hexadecimal nos es útil, pero algunas redes pueden estar configuradas para no entregar direcciones IP a clientes cuyas MAC no coincidan con algún proveedor. Finalmente, a menos que controles la red a la que te conectarás, es una buena idea probar con una dirección MAC conocida en vez de utilizar una al azar.

Para cambiar la MAC utilizamos el siguiente comando:

```
# ip link set dev eth0 address XX:XX:XX:XX:XX:XX

```

Donde 'XX:XX:XX:XX:XX:XX'. cualquier valor de 6-bytes nos sirve.

El paso final es activar la red, para esto:

```
# ip link set dev eth0 up

```

Si quiere verificar el cambio de MAC, simplemente ejecuta 'ifconfig eth0' nuevamente y revisa el valor para HWaddr.

## Spoofing MAC On Boot

Te darás cuenta que ambos métodos no son definitivos, al reiniciar, tu MAC retorna a su valor por defecto. Para modificar tu MAC al momento de iniciar tu computador, ubica el comando utilizado para falsear tu MAC en el script rc.multi antes de la linea #Start Daemons loop. Esto modificar tu MAC antes de que la interfaz de red se inicie.

## Enlaces y Referencias

*   [macchanger](http://www.alobbs.com/macchanger) página del proyecto.
*   [Article on DebianAdmin](http://www.debianadmin.com/change-your-network-card-mac-media-access-control-address.html) con mas opciones para macchanger.