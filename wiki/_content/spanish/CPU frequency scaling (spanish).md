Artículos relacionados

*   [Power saving](/index.php/Power_saving "Power saving")
*   [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")
*   [PHC](/index.php/PHC "PHC")

## Contents

*   [1 Herramientas del espacio de usuario](#Herramientas_del_espacio_de_usuario)
    *   [1.1 thermald](#thermald)
    *   [1.2 cpupower](#cpupower)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Controlador de frecuencia de la UCP](#Controlador_de_frecuencia_de_la_UCP)
    *   [2.2 Reguladores de ajuste (Esquemas de potencia de la UCP)](#Reguladores_de_ajuste_.28Esquemas_de_potencia_de_la_UCP.29)
    *   [2.3 Modo demonio](#Modo_demonio)
*   [3 Otros recursos](#Otros_recursos)

## Herramientas del espacio de usuario

### thermald

[thermald](https://www.archlinux.org/packages/?name=thermald) es un demonio de Linux que previene el sobrecalentamiento del ordenador; controla y equilibra la temperatura utilizando los métodos de refrigeración disponibles en la máquina.

De manera predeterminada, monitorea la temperatura la UCP usando los sensores de temperatura digitales disponibles en la misma, y mantiene la temperatura de la UCP bajo control antes que la máquina tome una medida correctiva que resulte agresiva.

### cpupower

[cpupower](https://www.archlinux.org/packages/?name=cpupower) es un conjunto de utilidades diseñadas para ajustar la frecuencias de la UCP (tecnología usada principalmente en portátiles) y permite al sistema operativo el ajuste de la velocidad hacia arriba o hacia abajo, dependiendo de la carga actual del sistema o del esquema de potencia, p. ej. la frecuencia de la UCP puede ser reducida de 2 GHz a 1 GHz cuando el portátil funciona con la batería, conservando la duración de ésta, reduciendo el calor generado y el ruido del ventilador.

El fichero de configuración de *cpupower* se encuentra alojada en `/etc/default/cpupower`. Este fichero de configuración es leído por un script bash alojado en `/usr/lib/systemd/scripts/cpupower` y es activado con *systemd* a través del servicio `cpupower.service`. Si desea habilitarlo para que inicie al arrancar el sistema operativo, puede ejecutar la orden:

```
# systemctl start cpupower && systemctl enable cpupower

```

## Configuración

La configuración del ajuste de la UPC es un proceso de 3 partes:

1.  Cargar el controlador de frecuencia de la UPC apropiado
2.  Cargar el regulador (o reguladores) de ajuste deseado
3.  Configurar y cargar el demonio de ajuste de frecuencia (opcional)

### Controlador de frecuencia de la UCP

Para lograr que el ajuste de frecuencia funcione adecuadamente, el sistema operativo debe conocer en primer lugar los límites de su UCP (o unidades si tiene varias). Para hacer esto, cargamos un controlador del núcleo que pueda leer y gestionar las especificaciones de todas sus UPC.

La mayoría de los portátiles y sobremesas modernos pueden simplemente utilizar el controlador `acpi-cpufreq`; otras opciones incluyen sin embargo, los controladores, `p4-clockmod`, `powernow-k6`, `powernow-k7`, `powernow-k8`, y `speedstep-centrino`.

Para cargar manualmente el controlador de frecuencia de la UPC:

```
# modprobe acpi-cpufreq

```

Para cargar automáticamente en el arranque, añada el controlador apropiado al array `MODULES` del archivo `/etc/rc.conf`. Por ejemplo:

```
MODULES=( ***acpi-cpufreq*** vboxdrv fuse fglrx iwl3945 ... )

```

Una vez cargado el controlador cpufreq apropiado, se puede visualizar la información detallada acerca de la UCP ejecutando:

```
$ cpupower frequency-info

```

Ejemplo de salida de `frequency-info` (en un Intel Duo Core T4300):

```
 analyzing CPU 0:
 driver: acpi-cpufreq
 CPUs which run at the same hardware frequency: 0
 CPUs which need to have their frequency coordinated by software: 0
 maximum transition latency: 10.0 us
 hardware limits: 1.20 GHz - 2.10 GHz
 available frequency steps:  2.10 GHz, 1.60 GHz, 1.20 GHz
 available cpufreq governors: performance schedutil
 current policy: frequency should be within 1.20 GHz and 2.10 GHz.
                 The governor "schedutil" may decide which speed to use
                 within this range.
 current CPU frequency: 2.10 GHz (asserted by call to hardware)
 boost state support:
   Supported: no
   Active: no

```

### Reguladores de ajuste (Esquemas de potencia de la UCP)

Se puede considerar a los reguladores como esquemas de potencia de la UCP preconfigurados. Para que los programas tales como kpowersave o gnome-power-manager puedan captarlos, estos reguladores deben ser cargados como módulos del núcleo. Usted puede cargar tantos reguladores como desee, pero solamenete uno de ellos estará activo en un momento dado.

Reguladores disponibles:

	Schedutil *(Por defecto, ha estado incorporado desde el kernel 4.7 al día de hoy)*

	Ya que aprovecha los datos de utilización del planificador del núcleo en un intento de tomar mejores decisiones sobre el ajuste del estado de frecuencia / rendimiento del CPU.

	Performance

	El regulador de rendimiento esta empotrado en el núcleo y hace que las UCP funcionen a la máxima velocidad de reloj.

	Ondemand *(recomendado para AMD)*

	Incrementa/Decrementa dinámicamente la velocidad de reloj de la UCP en base a la carga del sistema.

	Conservative

	Similar a ondemand, pero más conservador (los cambios de velocidad son más suaves)

	Powersave

	Hacer funcionar la UPC a la velocidad mínima.

	Userspace

	Velocidades de reloj configuradas manualmente por el usuario.

Alternativamente, puede establecer el regulador manualmente ejecutando (como root) la orden `cpupower frequency-set`, pero esto no se conservará después de un rearranque/apagado. Por ejemplo:

```
# cpupower frequency-set -r -g powersave

```

Ejecute **`cpupower frequency-set--help`** o **`man cpupower frequency-set`** para más información.

	También puede usar el siguiente script para modificar los esquemas de **`cpupower frequency-set`** ejemplo

```
##!/bin/bash
clear
echo " *** SCRIPT CPU-FREQ SCALING  *** "
echo " SELECCIONA UNA OPCIÓN. "
echo " 0.-Frecuencia actual del procesador"
echo " 1.-Powersave"
echo " 2.-Schedutil"
echo " 3.-Ondemand----(Recomendado para AMD)"
echo " 4.-Performance"
echo " 5.-Conservative"
echo " 6.-Userspace----(Asigna una frecuencia de forma manual)"
echo " 7.-¿Qué frecuencia tengo?"
echo " 8.-CPU frequency-info---(Ver frecuencias a las que se puede alcanzar"
echo "****************************************"
echo " 9.-Cambiar de forma permanente governor"
echo "*****************************************" 
echo " 10.-Salir"
echo ""
read -p "OPCIÓN: " OPCIÓN
case $OPCION in
0) watch grep \"cpu MHz\" /proc/cpuinfo;;
1) sudo cpupower frequency-set  -r -g powersave;;
2) sudo cpupower frequency-set  -r -g schedutil;;
3) sudo cpupower frequency-set  -r -g ondemand;;
4) sudo cpupower frequency-set  -r -g performance;;
5) sudo cpupower frequency-ser  -r -g conservative;;
6) echo -n " *** Ingresa de forma manual la frecuencia *** "
read freq
sudo cpupower frequency-set -f $freq;;
7) echo "**** Frecuencia actual ****: "
echo "****************************** "
cat /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor ;;
8) cpupower frequency-info ;;
9) sudo nano /etc/default/cpupower ;;
10) exit;;
*) echo " OPCIÓN NO VÁLIDA "
exit 1;;
esac

```

### Modo demonio

`cpupower` instala también un demonio que le permitirá establecer el regulador de juste deseado y velocidades de reloj maximas/mínimas en tiempo de arranque, sin necesidad de herramienta adicional alguna tal como kpowersave. Esta es una solución perfecta para aquellos que utilizan un escritorio ligero tal como Openbox.

Antes de arrancar el demonio, edite `/etc/default/cpupower` como root, seleccionando el regulador deseado y estableciendo las velocidades de reloj mínima y máxima para sus UPC, por ejemplo:

```
#configuración para el control de cpufreq
# reguladores válidos:
#  ondemand, performance, powersave,
#  conservative, userspace
governor="ondemand"

# sufijos válidos: Hz, kHz (default), MHz, GHz, THz
min_freq="1GHz"
max_freq="2GHz"

```

**Nota:** Los valores de la velocidad de reloj mínimo y máximo para sus UPC pueden ser leídos ejecutando `cpupower frequency-info` después de cargar el controlador de la CPU como se vió anteriormente (p.ej. `modprobe acpi-cpufreq`). Estos valores son opcionales, no obstante. Usted podría omitirlos completamente borrando o comentando las líneas min/max_freq. Todo funcionará automáticamente.

Habiéndose ocupado del archivo de configuración, puede usted ahora arrancar el demonio mediante la siguiente orden:

```
# /etc/rc.d/cpufreq start

```

Para arrancar el demonio autómaticamente en el arranque, añada `cpufreq` al array `DAEMONS` en `/etc/rc.conf`, por ejemplo:

```
DAEMONS=(syslog-ng hal ***cpufreq*** network netfs @alsa @crond @cupsd @fam @ntpd @sshd)

```

## Otros recursos

[CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") - Más información útil para los usuarios de entornos de escritorio (Entrada de Arch Wiki)