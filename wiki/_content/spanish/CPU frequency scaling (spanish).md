## Contents

*   [1 Resumen](#Resumen)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Controlador de frecuencia de la UCP](#Controlador_de_frecuencia_de_la_UCP)
    *   [3.2 Reguladores de ajuste (Esquemas de potencia de la UCP)](#Reguladores_de_ajuste_.28Esquemas_de_potencia_de_la_UCP.29)
    *   [3.3 Modo demonio](#Modo_demonio)
*   [4 Otros recursos](#Otros_recursos)

## Resumen

[cpufrequtils](https://www.archlinux.org/packages/?name=cpufrequtils) es un conjunto de utilidades diseñadas para ayudar al ajuste de frecuencias de la UCP, una tecnología usada principalmente en portátiles que permite al sistema operativo el ajuste de la velocidad hacia arriba o hacia abajo, dependiendo de la carga actual del sistema o del esquema de potencia. Por poner un ejemplo, el ajuste de frecuencia de la UCP puede reducir un procesador de 2 GHz a uno de 1 GHz cuando el portátil funciona con la batería, conservando la duración de ésta, reduciendo el calor generado y reduciendo el ruido del ventilador.

Cuando es usado en conjunción com [pm-utils](/index.php/Pm-utils "Pm-utils"), los propietarios de portátiles están provistos de un conjunto completo de programas para la gestión de la potencia.

## Instalación

El paquete [cpufrequtils](https://www.archlinux.org/packages/?name=cpufrequtils) está disponible en los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)").

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
$ cpufreq-info

```

Ejemplo de salida de `cpufreq-info` (en un Intel Duo Core T2500):

```
analyzing CPU 0:
 driver: acpi-cpufreq
 CPUs which need to switch frequency at the same time: 0 1
 hardware limits: 1000 MHz - 2.00 GHz
 available frequency steps: 2.00 GHz, 1.67 GHz, 1.33 GHz, 1000 MHz
 available cpufreq governors: ondemand, performance
 current policy: frequency should be within 1000 MHz and 2.00 GHz.
                 The governor "performance" may decide which speed to use
                 within this range.
 current CPU frequency is 2.00 GHz.
analyzing CPU 1:
 driver: acpi-cpufreq
 CPUs which need to switch frequency at the same time: 0 1
 hardware limits: 1000 MHz - 2.00 GHz
 available frequency steps: 2.00 GHz, 1.67 GHz, 1.33 GHz, 1000 MHz
 available cpufreq governors: ondemand, performance
 current policy: frequency should be within 1000 MHz and 2.00 GHz.
                 The governor "performance" may decide which speed to use
                 within this range.
 current CPU frequency is 2.00 GHz.

```

### Reguladores de ajuste (Esquemas de potencia de la UCP)

Se puede considerar a los reguladores como esquemas de potencia de la UCP preconfigurados. Para que los programas tales como kpowersave o gnome-power-manager puedan captarlos, estos reguladores deben ser cargados como módulos del núcleo. Usted puede cargar tantos reguladores como desee, pero solamenete uno de ellos estará activo en un momento dado.

Reguladores disponibles:

	performance **(por defecto)**

	El regulador de rendimiento esta empotrado en el núcleo y hace que las UCP funcionen a la máxima velocidad de reloj

	cpufreq_ondemand *(recomendado)*

	Incrementa/Decrementa dinámicamente la velocidad de reloj de la UCP en base a la carga del sistema

	cpufreq_conservative

	Similar a ondemand, pero más conservador (los cambios de velocidad son más suaves)

	cpufreq_powersave

	Hacer funcionar la UPC a la velocidad mínima

	cpufreq_userspace

	Velocidades de reloj configuradas manualmente por el usuario

Añada el regulador (o reguladores) al array `MODULES` en `/etc/rc.conf`:

```
MODULES=(acpi-cpufreq ***cpufreq_ondemand cpufreq_powersave*** vboxdrv fuse fglrx iwl3945 ... )

```

Alternativamente, puede establecer el regulador manualmente ejecutando (como root) la orden `cpufreq-set`, pero esto no se conservará después de un rearranque/apagado. Por ejemplo:

```
# cpufreq-set -g ondemand

```

Ejecute **`cpufreq-set --help`** o **`man cpufreq-set`** para más información.

### Modo demonio

`cpufrequtils` instala también un demonio que le permitirá establecer el regulador de juste deseado y velocidades de reloj maximas/mínimas en tiempo de arranque, sin necesidad de herramienta adicional alguna tal como kpowersave. Esta es una solución perfecta para aquellos que utilizan un escritorio ligero tal como Openbox.

Antes de arrancar el demonio, edite `/etc/conf.d/cpufreq` como root, seleccionando el regulador deseado y estableciendo las velocidades de reloj mínima y máxima para sus UPC, por ejemplo:

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

**Nota:** Los valores de la velocidad de reloj mínimo y máximo para sus UPC pueden ser leídos ejecutando `cpufreq-info` después de cargar el controlador de la CPU como se vió anteriormente (p.ej. `modprobe acpi-cpufreq`). Estos valores son opcionales, no obstante. Usted podría omitirlos completamente borrando o comentando las líneas min/max_freq. Todo funcionará automáticamente.

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
[pm-utils](/index.php/Pm-utils "Pm-utils") - Utilería Hibernate/Suspend proporcionada por la comunidad de OpenSUSE (Entrada de Arch Wiki)