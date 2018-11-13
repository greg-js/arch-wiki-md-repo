[lm_sensors](http://www.lm-sensors.org/) (Linux-monitoring sensors o Monitor de sensores de Linux en español), una herramienta libre para linux, provee las herramientas y los drivers de control de las temperaturas, voltaje y ventiladores.

Este documento te dice como instalar, configurar y usar **lm_sensors** para que puedas monitorear tu CPU y/o la temperatura de tu placa madre y velocidad de los ventiladores.

## Contents

*   [1 Aviso para los Kernels >=2.6.31](#Aviso_para_los_Kernels_>=2.6.31)
*   [2 Uso](#Uso)
    *   [2.1 Instalación](#Instalación)
    *   [2.2 Configurando lm_sensors](#Configurando_lm_sensors)
    *   [2.3 Probando lm_sensors](#Probando_lm_sensors)
    *   [2.4 Leyendo los valores SPD desde los modulos de memoria (Opcional)](#Leyendo_los_valores_SPD_desde_los_modulos_de_memoria_(Opcional))
*   [3 Usando datos del sensor](#Usando_datos_del_sensor)
    *   [3.1 Frontends Graficos](#Frontends_Graficos)
    *   [3.2 Sensord](#Sensord)

## Aviso para los Kernels >=2.6.31

Un cambio en la versión 2.6.31 ha hecho que los sensores dejen de funcionar para algunos usuarios. Mira [este FAQ](http://www.lm-sensors.org/wiki/FAQ/Chapter3#Mysensorshavestoppedworkinginkernel2.6.31) para una explicación detallada y para algunos errores de ejemplo. Para arreglar los sensores, agrega lo siguiente a tu linea de booteo del kernel en /boot/grub/menu.lst y reinicia tu máquina

```
acpi_enforce_resources=lax

```

Ejemplo de mi computadora

```
title           Arch Linux
root            (hd0,1)
kernel          /boot/vmlinuz26 root=/dev/sda2 ro quiet acpi_enforce_resources=lax vga=773
initrd          /boot/kernel26.img

```

## Uso

### Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors), disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)")

### Configurando lm_sensors

Usa **sensors-detect** para detectar y generar una lista de los modulos del Kernel
 `# sensors-detect` Esto creará la configuración y la guardará en `/etc/conf.d/lm_sensors`. Asegurate de responder YES a las preguntas sobre la exploración de diversos sensores. Cuando el script haya finalizado, se le presentará un resumen de las pruebas, ejemplo de mi sistema
```
Now follows a summary of the probes I have just done.
Just press ENTER to continue:
Driver `it87':
  * ISA bus, address 0x290
     Chip `ITE IT8718F Super IO Sensors' (confidence: 9)
Driver `coretemp':
  * Chip `Intel Core family thermal sensor' (confidence: 9)
```
Carga automáticamente los modulos del Kernel al momento de bootear agergando **sensors** a la cadena **DAEMONS** en `/etc/rc.conf` `DAEMONS=(syslog-ng crond ... sensors ...)` Alternativamente, agregalos manualmente a **MODULES** en `/etc/rc.conf` `MODULES=(coretemp it87 acpi-cpufreq)` **NO** necesitas ambas configuraciones, la de DAEMONS y la de MODULES.

### Probando lm_sensors

PAra probar tu configuracion, carga los modulos del Kernel manualmente o usando el script de inicio de sensors. **NO** tenes que hacer ambos. Ejemplo agregandolos manualmente

```
# modprobe it87
# modprobe coretemp

```

Ejemplo usando el scritp

```
# /etc/rc.d/sensors start

```

Deberias ver algo como esto cuando cunado ejecutes sensors

```
$ sensors
coretemp-isa-0000
Adapter: ISA adapter
Core 0:      +30.0°C  (high = +76.0°C, crit = +100.0°C)  

coretemp-isa-0001
Adapter: ISA adapter
Core 1:      +30.0°C  (high = +76.0°C, crit = +100.0°C)  

coretemp-isa-0002
Adapter: ISA adapter
Core 2:      +32.0°C  (high = +76.0°C, crit = +100.0°C)  

coretemp-isa-0003
Adapter: ISA adapter
Core 3:      +30.0°C  (high = +76.0°C, crit = +100.0°C)  

it8718-isa-0290
Adapter: ISA adapter
in0:         +1.17 V  (min =  +0.00 V, max =  +4.08 V)   
in1:         +1.31 V  (min =  +1.28 V, max =  +1.68 V)   
in2:         +3.28 V  (min =  +2.78 V, max =  +3.78 V)   
in3:         +2.88 V  (min =  +2.67 V, max =  +3.26 V)   
in4:         +2.98 V  (min =  +2.50 V, max =  +3.49 V)   
in5:         +1.34 V  (min =  +0.58 V, max =  +1.34 V)   ALARM
in6:         +2.02 V  (min =  +1.04 V, max =  +1.36 V)   ALARM
in7:         +2.83 V  (min =  +2.67 V, max =  +3.26 V)   
Vbat:        +3.28 V
fan1:       1500 RPM  (min = 3245 RPM)  ALARM
fan2:          0 RPM  (min = 3245 RPM)  ALARM
fan3:          0 RPM  (min = 3245 RPM)  ALARM
temp1:       +18.0°C  (low  = +127.0°C, high = +64.0°C)  sensor = thermal diode
temp2:       +32.0°C  (low  = +127.0°C, high = +64.0°C)  sensor = thermistor
temp3:       +38.0°C  (low  = +127.0°C, high = +64.0°C)  sensor = thermistor
cpu0_vid:   +2.050 V

acpitz-virtual-0
Adapter: Virtual device
temp1:       +18.0°C  (crit = +64.0°C)
```

### Leyendo los valores SPD desde los modulos de memoria (Opcional)

Para leer los valores de tiempo SPD desde tus modulos de memoria, descarga este script en perl: [SPDdecodeScript](http://www.lm-sensors.org/browser/lm-sensors/branches/lm-sensors-2.10/prog/eeprom/decode-dimms.pl?format=raw) Una ves que lo hayas descargado, necesitaras cargar el modulo eeprom del kernel

```
# modprobe eeprom

```

Ahora podes hacer el decode-dimms.pl ejecutable y ejecutarlo

```
$ chmod +x decode-dimms.pl

```

Aqui un ejemplo de la salida de mi maquina

```
$ ./decode-dimms.pl 

Memory Serial Presence Detect Decoder
By Philip Edelbrock, Christian Zuckschwerdt, Burkart Lingner,
Jean Delvare and others
Version 2.10.8

Decoding EEPROM: /sys/bus/i2c/drivers/eeprom/0-0050
Guessing DIMM is in                             bank 1

---=== SPD EEPROM Information ===---
EEPROM Checksum of bytes 0-62                   OK (0x0D)
# of bytes written to SDRAM EEPROM              128
Total number of bytes in EEPROM                 256
Fundamental Memory type                         DDR2 SDRAM
SPD Revision                                    1.2

---=== Memory Characteristics ===---
Maximum module speed                            800MHz (PC2-6400)
Size                                            2048 MB
tCL-tRCD-tRP-tRAS                               5-5-5-18
Supported CAS Latencies                         5, 4
Minimum Cycle Time (CAS 5)                      2.5 ns
Maximum Access Time (CAS 5)                     0.4 ns
Minimum Cycle Time (CAS 4)                      3.7 ns
Maximum Access Time (CAS 4)                     0.5 ns

---=== Manufacturing Information ===---
Manufacturer                                    Corsair
Manufacturing Location Code                     0x01
Part Number                                     CM2X2048-8500C5D  
Revision Code                                   0x2020

Decoding EEPROM: /sys/bus/i2c/drivers/eeprom/0-0051
Guessing DIMM is in                             bank 2

---=== SPD EEPROM Information ===---
EEPROM Checksum of bytes 0-62                   OK (0x0D)
# of bytes written to SDRAM EEPROM              128
Total number of bytes in EEPROM                 256
Fundamental Memory type                         DDR2 SDRAM
SPD Revision                                    1.2

---=== Memory Characteristics ===---
Maximum module speed                            800MHz (PC2-6400)
Size                                            2048 MB
tCL-tRCD-tRP-tRAS                               5-5-5-18
Supported CAS Latencies                         5, 4
Minimum Cycle Time (CAS 5)                      2.5 ns
Maximum Access Time (CAS 5)                     0.4 ns
Minimum Cycle Time (CAS 4)                      3.7 ns
Maximum Access Time (CAS 4)                     0.5 ns

---=== Manufacturing Information ===---
Manufacturer                                    Corsair
Manufacturing Location Code                     0x01
Part Number                                     CM2X2048-8500C5D  
Assembly Serial Number                          0x00514458

Decoding EEPROM: /sys/bus/i2c/drivers/eeprom/0-0052
Guessing DIMM is in                             bank 3

---=== SPD EEPROM Information ===---
EEPROM Checksum of bytes 0-62                   OK (0x0D)
# of bytes written to SDRAM EEPROM              128
Total number of bytes in EEPROM                 256
Fundamental Memory type                         DDR2 SDRAM
SPD Revision                                    1.2

---=== Memory Characteristics ===---
Maximum module speed                            800MHz (PC2-6400)
Size                                            2048 MB
tCL-tRCD-tRP-tRAS                               5-5-5-18
Supported CAS Latencies                         5, 4
Minimum Cycle Time (CAS 5)                      2.5 ns
Maximum Access Time (CAS 5)                     0.4 ns
Minimum Cycle Time (CAS 4)                      3.7 ns
Maximum Access Time (CAS 4)                     0.5 ns

---=== Manufacturing Information ===---
Manufacturer                                    Corsair
Manufacturing Location Code                     0x01
Part Number                                     CM2X2048-8500C5D  
Revision Code                                   0x2020

Decoding EEPROM: /sys/bus/i2c/drivers/eeprom/0-0053
Guessing DIMM is in                             bank 4

---=== SPD EEPROM Information ===---
EEPROM Checksum of bytes 0-62                   OK (0x0D)
# of bytes written to SDRAM EEPROM              128
Total number of bytes in EEPROM                 256
Fundamental Memory type                         DDR2 SDRAM
SPD Revision                                    1.2

---=== Memory Characteristics ===---
Maximum module speed                            800MHz (PC2-6400)
Size                                            2048 MB
tCL-tRCD-tRP-tRAS                               5-5-5-18
Supported CAS Latencies                         5, 4
Minimum Cycle Time (CAS 5)                      2.5 ns
Maximum Access Time (CAS 5)                     0.4 ns
Minimum Cycle Time (CAS 4)                      3.7 ns
Maximum Access Time (CAS 4)                     0.5 ns

---=== Manufacturing Information ===---
Manufacturer                                    Corsair
Manufacturing Location Code                     0x01
Part Number                                     CM2X2048-8500C5D  
Assembly Serial Number                          0x00514458

Decoding EEPROM: /sys/bus/i2c/drivers/eeprom/0-0057
Guessing DIMM is in                             bank 8

---=== SPD EEPROM Information ===---
EEPROM Checksum of bytes 0-62                   Bad
                                                (found 0x20, calculated 0x0A)

Number of SDRAM DIMMs detected and decoded: 4
```

## Usando datos del sensor

### Frontends Graficos

Hay una variedad de front-ends para los datos del sensor. Algunos están listados abajo. El nombre en *cursiva* es el nombre del paquete en el repositorio, en otras palabras, podes instalarlo/s via pacman.

1.  *sensors-applet* - un applet para el panel de Gnome para visualizar lecturas desde los sensores, incluyendo la temperatura del CPU, velocidad de los ventiladores y voltajes.
2.  *ksensors* - ksensors es un agradable frontend para lm_sensors para KDE
3.  *xsensors* - interfaz X11 para lm_sensors
4.  *xfce4-sensors-plugin* - Un plugin de lm_sensors para el panel de Xfce
5.  *[conky](/index.php/Conky "Conky")* - Conky es un avanzado, y altamente configurable monitor de sistema para X basado en torsmo
6.  *kdeutils-superkaramba* - Superkaramba es una herramienta la cual te da la posibilidad de crear diferentes widgets para el entorno KDE. Mira la [sección karamba en kde-look.org](http://www.kde-look.org/index.php?xcontentmode=38) para ejemplos de frontends hechos en karamba para los ensores.

### Sensord

Hay un paquete opcional con un daemon llamado sensord que puede registrar tus datos a una base de datos rrd que vos podes visualizar graficamente. Marcador de posición para que alguien escriba una wiki sobre instalación/configuración de [sensord](/index.php?title=Sensord&action=edit&redlink=1 "Sensord (page does not exist)").