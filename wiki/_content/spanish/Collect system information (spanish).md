**Nota:** Este artículo sólo es una copia de [Gulix.cl - Encontrar Información del Sistema](http://www.gulix.cl/wiki/Encontrar_Informaci%C3%B3n_del_Sistema#Leer_m.C3.A1s).

## Contents

*   [1 Cómo Encontrar Información del Sistema GNU/Linux](#C.C3.B3mo_Encontrar_Informaci.C3.B3n_del_Sistema_GNU.2FLinux)
    *   [1.1 Herramientas](#Herramientas)
    *   [1.2 Mi Distribución y Kernel](#Mi_Distribuci.C3.B3n_y_Kernel)
    *   [1.3 Hardware](#Hardware)
        *   [1.3.1 Procesador](#Procesador)
            *   [1.3.1.1 Temperatura del procesador](#Temperatura_del_procesador)
        *   [1.3.2 Memoria](#Memoria)
        *   [1.3.3 Tarjeta Madre](#Tarjeta_Madre)
            *   [1.3.3.1 Bios](#Bios)
            *   [1.3.3.2 Modelo de la Placa madre (Motherboard)](#Modelo_de_la_Placa_madre_.28Motherboard.29)
            *   [1.3.3.3 Capacidades del Bus de Datos](#Capacidades_del_Bus_de_Datos)
            *   [1.3.3.4 Sensores de Hardware](#Sensores_de_Hardware)
        *   [1.3.4 Almacenamiento](#Almacenamiento)
        *   [1.3.5 Interface Humana](#Interface_Humana)
            *   [1.3.5.1 Dispositivos USB](#Dispositivos_USB)
            *   [1.3.5.2 Dispositivos PCI](#Dispositivos_PCI)
            *   [1.3.5.3 Monitores Externos](#Monitores_Externos)
            *   [1.3.5.4 Aceleración gráfica y poder de cálculo gráfico](#Aceleraci.C3.B3n_gr.C3.A1fica_y_poder_de_c.C3.A1lculo_gr.C3.A1fico)
            *   [1.3.5.5 Información acerca del Teclado](#Informaci.C3.B3n_acerca_del_Teclado)
            *   [1.3.5.6 Idioma del sistema](#Idioma_del_sistema)
            *   [1.3.5.7 Controles para Pantallas de Notebook](#Controles_para_Pantallas_de_Notebook)
        *   [1.3.6 Bateria](#Bateria)
            *   [1.3.6.1 Carga actual de la bateria](#Carga_actual_de_la_bateria)
            *   [1.3.6.2 Carga full de la batería](#Carga_full_de_la_bater.C3.ADa)
            *   [1.3.6.3 Carga full según diseño de la bateria](#Carga_full_seg.C3.BAn_dise.C3.B1o_de_la_bateria)
            *   [1.3.6.4 Resumen de información de la batería](#Resumen_de_informaci.C3.B3n_de_la_bater.C3.ADa)
    *   [1.4 Software](#Software)
        *   [1.4.1 El Gestor de Paquetes](#El_Gestor_de_Paquetes)
        *   [1.4.2 Software Instalado](#Software_Instalado)
    *   [1.5 Meta](#Meta)
        *   [1.5.1 Permisos y privilegios del Usuario](#Permisos_y_privilegios_del_Usuario)
        *   [1.5.2 Otros usuarios conectados al sistema](#Otros_usuarios_conectados_al_sistema)
        *   [1.5.3 Últimos usuarios autentificados en el sistema](#.C3.9Altimos_usuarios_autentificados_en_el_sistema)
        *   [1.5.4 Usuarios validos del sistema](#Usuarios_validos_del_sistema)
        *   [1.5.5 Grupos validos del sistema](#Grupos_validos_del_sistema)
        *   [1.5.6 Passwords de usuarios del sistema](#Passwords_de_usuarios_del_sistema)
        *   [1.5.7 Conexión a la Red](#Conexi.C3.B3n_a_la_Red)
        *   [1.5.8 Puntos de Montaje](#Puntos_de_Montaje)
        *   [1.5.9 Carga](#Carga)
        *   [1.5.10 Mensaje de bienvenida en sesión de texto](#Mensaje_de_bienvenida_en_sesi.C3.B3n_de_texto)
        *   [1.5.11 Mensajes de Error Recientes](#Mensajes_de_Error_Recientes)
        *   [1.5.12 Presencia de otros Sistemas Operativos](#Presencia_de_otros_Sistemas_Operativos)
            *   [1.5.12.1 Archivo de configuración de grub](#Archivo_de_configuraci.C3.B3n_de_grub)
            *   [1.5.12.2 Archivo de configuración de lilo](#Archivo_de_configuraci.C3.B3n_de_lilo)
    *   [1.6 Servicios](#Servicios)
        *   [1.6.1 Escaneando los servicios de red activos en puertos públicos](#Escaneando_los_servicios_de_red_activos_en_puertos_p.C3.BAblicos)

# Cómo Encontrar Información del Sistema GNU/Linux

En este sencillo <u>tutorial</u>, vamos a ver cómo encontrar información acerca del sistema en una máquina con una distribución de GNU/Linux. Se usará más que nada la consola y se utilizará medios disponibles para usuarios normales cuando sea posible, para determinar información acerca de nuestra distro, kernel, hardware, software, etc.

Saber cómo obtener esta información es muy útil en el mundo del software libre, pues forma parte de la [ netiqueta] en muchos foros de GNU/Linux el *saber cómo hacer preguntas* para evitar ser ignorado o (peor) *flameado*.

--[Ryan.chappelle](/index.php?title=Usuario:Ryan.chappelle&action=edit&redlink=1 "Usuario:Ryan.chappelle (page does not exist)") 16:01 4 feb 2010 (UTC)

## Herramientas

Para este tutorial se utilizarán las siguientes herramientas:

*   Acceso a una consola
*   Teclado
*   [Cerebro](https://es.wikipedia.org/wiki/Cerebro)

## Mi Distribución y Kernel

¿Quieres saber qué **distribución** de GNU/Linux estás usando?

Una de las maneras más fáciles es consultar el archivo *issue*:

```
cat /etc/issue

```

En mi máquina esto entrega un resultado como el siguiente:

```
Fedora release 12 (Constantine)
Kernel \r on an \m (\l)

```

De aquí obtenemos la información importante: nombre de la distribución, versión y nombre código.

En una máquina con Trisquel (una distribución sólo-software-libre derivativa de Debian), el resultado es el siguiente:

*POR HACER*

*   Más información: `man issue`.

Para saber qué **kernel** se está usando, basta con utilizar el comando <tt>uname</tt>:

```
uname -r

```

Esto entrega el siguiente resultado:

```
2.6.31.5-127.fc12.i686.PAE

```

De aquí podemos obtener la siguiente información:

*   La versión *major* o principal del Kernel es la <tt>2.6</tt>. Esto es indicativo de qué rama de desarrollo y tecnologías tienes disponibles este kernel.
*   La versión *minor* es la <tt>.31</tt>.
*   El kernel está compilado para la arquitectura y máquina *Intel 686* o mejor conocido como Intel Pentium Pro (6), lo que equivale a las familias de procesadores Core y M, y a todos los procesadores Intel posteriores a Pentium II y AMD Athlon y posteriores. En términos básicos esto significa que el kernel está optimizado para correr en hardware Intel "moderno".
*   El kernel soporta la capacidad <tt>PAE</tt> o [Extensión de Dirección Física](https://es.wikipedia.org/wiki/Extensión_de_dirección_física) del procesador, que permite a procesadores de 32-bit obtener más de 4GiB de memoria RAM cuando esté disponible, además de habilitar el llamado "bit NX".

*   Más información: `man uname`.

Además el kernel cuando arranca mantiene un archivo llamado **/proc/version** donde se puede obtener información adicional sobre el kernel que se está usando actualmente.

```
$cat /proc/version
 Linux version 2.6.31-16-generic (buildd@rothera) (gcc version 4.4.1 (Ubuntu 4.4.1-4ubuntu8) ) #53-Ubuntu
 SMP Tue Dec 8 04:01:29 UTC 2009

```

## Hardware

*   **En general, es posible obtener toda la información del hardware con programas como <tt>lshw</tt>, <tt>lspci</tt>, <tt>hwinfo</tt> y <tt>dmidecode</tt>. Aquí veremos solamente cómo obtener información de partes y componentes específicos.**

### Procesador

El kernel Linux, mantiene un archivo en /proc/cpuinfo que contiene información del/los procesadores que utiliza la máquina:

```
cat /proc/cpuinfo

```

Aquí podemos encontrar información bastante interesante sobre nuestro procesador:

| Salida | Significado |
| processor : 0 | El número del procesador que tenemos (<tt>0</tt> = primer/único procesador, etc) |
| vendor_id : AuthenticAMD | Identificación del vendedor |
| model name : AMD Sempron(TM) 2400+ | Iddentificación del modelo |
| cpu MHz : 1666.725 | Velocidad del procesador |
| cache size : 256 KB | Caché |
| flags : ... | Banderas indicando qué características soporta el procesador. |

**Flags (Banderas)**:

*   fpu: el procesador tiene una Unidad de Aritmética de Punto Flotante
*   apic: el procesador soporta los controladores de interrupción programables
*   mmx: el procesador soporta multimedia por MMX
*   3dnow: el procesador soporta la tecnología 3DNow! de AMD.
*   *otros*...

#### Temperatura del procesador

El kernel Linux, mantiene un archivo en /proc/acpi/thermal_zone/THRM/temperature que contiene la información ACPI de la temperatura del procesador, para ello ACPI debe estar activado

```
cat /proc/acpi/thermal_zone/THRM/temperature

```

### Memoria

La información del uso de memoria está en el archivo <tt>/proc/meminfo</tt>. Un ejemplo de las líneas que pueden ser de interés:

```
MemTotal:         239492 kB
MemFree:           36700 kB
Buffers:            2120 kB
Cached:           117744 kB
SwapCached:          112 kB
Active:            48064 kB
Inactive:         141124 kB

```

Otra manera de ver esta información es con el comando <tt>free</tt>:

```
free -m # ver la información de memoria disponible, en MegaBytes.

```

La salida de *free* es una tabla con información de la memoria física y virtual, tanto libre como ocupada:

```
             total       used       free     shared    buffers     cached
Mem:           233        204         29          0          2        117
-/+ buffers/cache:         83        150
Swap:         1105          0       1105

```

*   `man free`

También es posible obtener la cantidad de memoria en la lista de procesos e información que entrega el comando `man top`

Al ejecutar **top** se desplegará la lista de procesos y consumos que está tomando cada uno, en la parte superior se podrá observar información sobre la memoria, cpu y otros

```
top - 22:36:22 up  5:32,  2 users,  load average: 0.07, 0.08, 0.02
Tasks: 178 total,   3 running, 175 sleeping,   0 stopped,   0 zombie
Cpu(s): 13.5%us,  3.9%sy,  0.0%ni, 82.5%id,  0.0%wa,  0.0%hi,  0.2%si,  0.0%st
Mem:   1931712k total,  1334444k used,   597268k free,    80248k buffers
Swap:   393584k total,        0k used,   393584k free,   540072k cached

```

### Tarjeta Madre

El programa <tt>dmidecode</tt> lee la información de los chips de la tarjeta madre, de esta forma es posible determinar qué atributos soporta el hardware o cómo está construido. Toda esta información es proporcionada por el estándar [Desktop Management Interface](https://en.wikipedia.org/wiki/Desktop_Management_Interface "wikipedia:Desktop Management Interface") que soportan las placas madres desde 1997.

#### Bios

**sudo dmidecode -t 0**

```
# dmidecode 2.9
SMBIOS 2.4 present.

Handle 0x0000, DMI type 0, 24 bytes
BIOS Information
	Vendor: Hewlett-Packard
	Version: F.21
	Release Date: 02/28/2008
	Address: 0xE7060
	Runtime Size: 102304 bytes
	ROM Size: 1024 kB
	Characteristics:
		ISA is supported
		PCI is supported
		PC Card (PCMCIA) is supported
		PNP is supported
		APM is supported
		BIOS is upgradeable
		BIOS shadowing is allowed
		ESCD support is available
		Boot from CD is supported
		ACPI is supported
		USB legacy is supported
		AGP is supported
		BIOS boot specification is supported
 		Targeted content distribution is supported
	BIOS Revision: 15.33
	Firmware Revision: 81.81

```

#### Modelo de la Placa madre (Motherboard)

**dmidecode -t 2**

```
# dmidecode 2.9
SMBIOS 2.4 present. 

Handle 0x0002, DMI type 2, 8 bytes
Base Board Information
	Manufacturer: Wistron
	Product Name: 30D6
	Version: 81.51
	Serial Number:           

```

#### Capacidades del Bus de Datos

#### Sensores de Hardware

### Almacenamiento

*   Comando **fdisk -l** -> `man fdisk`

Ejemplo de salida de **fdisk -l**: aquí se puede observar que la máquina posee 3 unidades de almacenamiento conectada, se puede observar la distribución de las particiones de cada una. Este comando debe ser ejecutado con niveles de root.

```
Disco /dev/sda: 122.9 GB, 122942324736 bytes
255 cabezas, 63 sectores/pista, 14946 cilindros
Unidades = cilindros de 16065 * 512 = 8225280 bytes
Identificador de disco: 0x83d5d8c9

Disposit. Inicio    Comienzo      Fin      Bloques  Id  Sistema
/dev/sda1   *           1       14946   120053713+  83  Linux

Disco /dev/sdb: 1000.2 GB, 1000204886016 bytes
255 cabezas, 63 sectores/pista, 121601 cilindros
Unidades = cilindros de 16065 * 512 = 8225280 bytes
Identificador de disco: 0xdf69df69

Disposit. Inicio    Comienzo      Fin      Bloques  Id  Sistema
/dev/sdb1   *           1        2550    20482843+   7  HPFS/NTFS
/dev/sdb2            2551       11060    68356575   83  Linux
/dev/sdb3           11061      121601   887920582+   5  Extendida
/dev/sdb5           11061       11184      995998+  82  Linux swap / Solaris
/dev/sdb6           11185      121601   886924521   83  Linux

Disco /dev/sdc: 1029 MB, 1029701632 bytes
8 cabezas, 32 sectores/pista, 7856 cilindros
Unidades = cilindros de 256 * 512 = 131072 bytes
Identificador de disco: 0x1926be76

Disposit. Inicio    Comienzo      Fin      Bloques  Id  Sistema
/dev/sdc1   *           1        7856     1005552    b  W95 FAT32

```

También es posible obtener la lista de particiones de las diferentes unidades revisando el archivo controlado por el kernel que contiene dicha información **/proc/partitions**:

```
$cat /proc/partitions

```

*   `man blkid`
*   `man df`
*   **Ver también: [Explicaciones Acerca de /dev](/index.php?title=Explicaciones_Acerca_de_/dev&action=edit&redlink=1 "Explicaciones Acerca de /dev (page does not exist)")**.

### Interface Humana

Se entiende usualmente por *inteface humana* a todos los dispositivos que pueden recibir y enviar información de/a un ser humano. En el sistema de eventos del kernel de Linux el significado está más acotado a aquellos dispositivos que cambian de estado cuando reciben interacción de un humano: teclado, mouse, joystick, etc.

La información de estado está almacenada en un árbol de directorios en <tt>/etc/input.d/</tt> para los kernels 2.6 en adelante.

#### Dispositivos USB

Utilizando el comando **lsusb** `man lsusb` Ejemplo de salida de **lsusb**

```
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 021: ID 1516:1603 CompUSA 1GB Flash Drive
Bus 001 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub

```

#### Dispositivos PCI

utilizando el comando **lspci** `man lspci`

Ejemplo de salida de **lspci**:

```
00:00.0 Host bridge: Intel Corporation 82945G/GZ/P/PL Memory Controller Hub (rev 02)
00:02.0 VGA compatible controller: Intel Corporation 82945G/GZ Integrated Graphics Controller (rev 02)
00:1b.0 Audio device: Intel Corporation 82801G (ICH7 Family) High Definition Audio Controller (rev 01)
00:1c.0 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 1 (rev 01)
00:1c.1 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 2 (rev 01)
00:1d.0 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #1 (rev 01)
00:1d.1 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #2 (rev 01)
00:1d.2 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #3 (rev 01)
00:1d.3 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #4 (rev 01)
00:1e.0 PCI bridge: Intel Corporation 82801 PCI Bridge (rev e1)
00:1f.0 ISA bridge: Intel Corporation 82801GB/GR (ICH7 Family) LPC Interface Bridge (rev 01)
00:1f.1 IDE interface: Intel Corporation 82801G (ICH7 Family) IDE Controller (rev 01)
00:1f.2 IDE interface: Intel Corporation 82801GB/GR/GH (ICH7 Family) SATA IDE Controller (rev 01)
00:1f.3 SMBus: Intel Corporation 82801G (ICH7 Family) SMBus Controller (rev 01)
02:00.0 Ethernet controller: 
        Realtek Semiconductor Co., Ltd. RTL8101E/RTL8102E PCI Express Fast Ethernet controller (rev 01)
03:01.0 Communication controller: Conexant Systems, Inc. HSF 56k Data/Fax Modem

```

#### Monitores Externos

Si tu computador tiene más de un monitor activado, o si tiene dos salidas de video activas (por ejemplo, un laptop conectado a una salida VGA o similar), es posible encontrar información de las salidas de video activas en <tt>/proc/video</tt> o <tt>/proc/acpi/video</tt>, dependiendo del kernel y la tarjeta madre.

#### Aceleración gráfica y poder de cálculo gráfico

Si el resultado del comando **glxinfo | grep rendering** retorna **Yes** entonces la sessión gráfica que está usando posee soporte para aceleración gráfica.

```
# glxinfo  | grep rendering
direct rendering: Yes

```

Para obtener un valor referencial del poder de cálculo de su tarjeta gráfica, puede someter a esta a una sesión de estrés con el siguiente test.

```
glxgears

```

salida esperada de **glxgears**

```
3229 frames in 5.0 seconds
3373 frames in 5.0 seconds
..
..

```

#### Información acerca del Teclado

-- **Ver también: [Emular_Teclas_Multimedia](/index.php?title=Emular_Teclas_Multimedia&action=edit&redlink=1 "Emular Teclas Multimedia (page does not exist)") para configurar habilidades especiales en tu teclado**.

#### Idioma del sistema

El idioma del sistema en curso está almacenado en el shell en un conjunto de variables, la más importante **LANG**:

comando:

```
echo $LANG

```

ejemplo de salida:

```
es_CL.UTF-8

```

Establecer un lenguaje diferente, por ejemplo inglés de US:

```
export LANG=US

```

#### Controles para Pantallas de Notebook

El brillo de la pantalla LCD del notebook se puede ver en el archivo /proc/acpi/video/IGPU/LCD0/brightness que retornará los tipos de brillo soportados y el brillo actual en que se encuentra el monitor

```
cat /proc/acpi/video/IGPU/LCD0/brightness

```

retornará algo similar a:

```
levels:  10 20 30 40 50 60 70 80 90 100
current: 60

```

En donde 60 es el brillo actual (**current**)

### Bateria

La información de la batería de un notebook está disponible en más de un lugar dependiendo de la versión del kernel, en kernels antiguos se encuentra en los archivos del directorio /proc/acpi/battery/BAT*n*, sin embargo, en kernels actuales se encuentra en /sys/class/power_supply/BAT*n* (en donde n es el numero de la batería)

#### Carga actual de la bateria

La información de la carga actual se encuentra en el archivo /sys/class/power_supply/BAT1/charge_now

```
cat /sys/class/power_supply/BAT1/charge_now

```

regresará algo similar a:

```
2647000

```

#### Carga full de la batería

La información de la carga actual se encuentra en el archivo /sys/class/power_supply/BAT1/charge_full

```
cat /sys/class/power_supply/BAT1/charge_full

```

regresará algo similar a:

```
2647000

```

#### Carga full según diseño de la bateria

La información de la carga actual se encuentra en el archivo /sys/class/power_supply/BAT1/charge_full_design

```
cat /sys/class/power_supply/BAT1/charge_full_design

```

regresará algo similar a:

```
4000000

```

#### Resumen de información de la batería

Un archivo que acompaña a los anteriores es un resumen de la información total de la batería, el cual se encuentra en /sys/class/power_supply/BAT1/uevent

```
cat /sys/class/power_supply/BAT1/uevent

```

regresará algo similar a:

```
POWER_SUPPLY_NAME=BAT1
POWER_SUPPLY_TYPE=Battery
POWER_SUPPLY_STATUS=Full
POWER_SUPPLY_PRESENT=1
POWER_SUPPLY_TECHNOLOGY=Li-ion
POWER_SUPPLY_VOLTAGE_MIN_DESIGN=11100000
POWER_SUPPLY_VOLTAGE_NOW=12086000
POWER_SUPPLY_CURRENT_NOW=0
POWER_SUPPLY_CHARGE_FULL_DESIGN=4000000
POWER_SUPPLY_CHARGE_FULL=2647000
POWER_SUPPLY_CHARGE_NOW=2647000
POWER_SUPPLY_MODEL_NAME=Chapala
POWER_SUPPLY_MANUFACTURER=SANYO
POWER_SUPPLY_SERIAL_NUMBER=29220

```

## Software

### El Gestor de Paquetes

El **Gestor de Paquetes** es un programa que se encarga de gestionar los programas y componentes instalados, y depende de cada distribución.

*   **Debian y similares**: Apt (apt-get, aptitude), Synaptic
*   **Redhat** y derivados: Pickup, Yum (yumex, etc...)
*   **OpenSUSE** y derivados: Smart

La configuración del gestor de paquetes está almacenada en un directorio en <tt>/etc</tt>. Por ejemplo, la configuración de Apt está en <tt>/etc/apt/</tt> mientras que la de Yum en <tt>/etc/yum.d/</tt>. La configuración de la caché de paquetes instalados y disponibles está en <tt>/var/cache/nombre_del_gestor</tt>.

### Software Instalado

## Meta

### Permisos y privilegios del Usuario

`man whoami` Ejemplo de salida de **whoami**

```
dalacost@urano:~$ whoami
dalacost

```

El comando **id** retorna la información de grupos y privilegios de un usuario. Se le pasa de parámetro el nombre de un usuario (opcional) y retorna una lista de los grupos (con sus GID) a los que pertenece ese usuario, y que en un sistema Linux determina de qué privilegios dispone ese usuario y qué operaciones puede realizar.

`man id` Ejemplo de salida de **id**

```
dalacost@urano:~$ id
uid=1000(dalacost) gid=1000(dalacost) gupos=4(adm),20(dialout),21(fax),24(cdrom),26(tape),
29(audio),30(dip),44(video),46(plugdev),103(fuse),104(lpadmin),
112(netdev),115(admin),120(sambashare),1000(dalacost)

```

En el ejemplo anterior, el usuario <tt>dalacost</tt> tiene los siguientes privilegios, entre otros:

*   ...puede leer registros de administración del sistema (grupo **adm**).
*   ...puede utilizar un módem u otra conexión PPP (o PPPoE) de manera directa (grupo **dialout**).
*   ...puede montar y desmontar imágenes o archivos de disco con FUSE (grupo **fuse**).
*   ...puede administrar la impresora del sistema directamente (grupo **lpadmin**).

### Otros usuarios conectados al sistema

El comando **who** `man who` permite obtener información sobre otros usuarios conectados al mismo sistema.

Ejemplo de salida del comando **who**

```
dalacost tty7         2010-01-13 12:04 (:0)
dalacost pts/0        2010-01-13 12:05 (:0.0)
dalacost pts/1        2010-01-13 12:06 (:0.0)
dalacost pts/3        2010-01-13 12:53 (:0.0)
dalacost pts/4        2010-01-13 13:02 (:0.0)
dalacost pts/5        2010-01-13 17:53 (:0.0)
dalacost pts/6        2010-01-14 13:27 (:0.0)
dalacost pts/7        2010-01-14 15:27 (:0.0)
dalacost pts/8        2010-01-28 12:04 (:0.0)
dalacost pts/9        2010-01-18 15:55 (:0.0)
dalacost pts/10       2010-01-20 16:01 (:0.0)
dalacost pts/11       2010-01-26 18:58 (:0.0)
dalacost pts/12       2010-01-27 11:36 (:0.0)
dalacost pts/13       2010-02-03 11:09 (:0.0)

```

### Últimos usuarios autentificados en el sistema

`man last`

Salida de ejemplo del comando **last**

```
dalacost pts/1        :0.0             Sun Jan 31 17:52   still logged in   
dalacost pts/0        :0.0             Sun Jan 31 17:52 - 17:53  (00:00)    
dalacost tty7         :0               Sun Jan 31 17:04   still logged in   
reboot   system boot  2.6.31-17-generi Sun Jan 31 17:04 - 22:51  (05:47)    
dalacost tty7         :0               Sat Jan 30 23:46 - down   (17:16)    
dalacost pts/2        :0.0             Sat Jan 30 20:53 - 23:46  (02:52)    
dalacost pts/1        :0.0             Sat Jan 30 13:17 - 23:46  (10:28)    
dalacost tty7         :0               Fri Jan 29 21:10 - 23:46 (1+02:35)   
reboot   system boot  2.6.31-17-generi Fri Jan 29 21:10 - 17:03 (1+19:52)

```

### Usuarios validos del sistema

Es posible indagar sobre usuarios válidos del sistema revisando los archivos de autenticación de usuarios **/ etc/passwd**.

Ejemplo del archivo

```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/bin/sh
sys:x:3:3:sys:/dev:/bin/sh
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
lp:x:7:7:lp:/var/spool/lpd:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
uucp:x:10:10:uucp:/var/spool/uucp:/bin/sh
proxy:x:13:13:proxy:/bin:/bin/sh
www-data:x:33:33:www-data:/var/www:/bin/sh
backup:x:34:34:backup:/var/backups:/bin/sh
list:x:38:38:Mailing List Manager:/var/list:/bin/sh
irc:x:39:39:ircd:/var/run/ircd:/bin/sh
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/bin/sh
nobody:x:65534:65534:nobody:/nonexistent:/bin/sh
libuuid:x:100:101::/var/lib/libuuid:/bin/sh
syslog:x:101:102::/home/syslog:/bin/false
messagebus:x:102:106::/var/run/dbus:/bin/false
hplip:x:103:7:HPLIP system user,,,:/var/run/hplip:/bin/false
avahi-autoipd:x:104:110:Avahi autoip daemon,,,:/var/lib/avahi-autoipd:/bin/false
avahi:x:105:111:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/bin/false
couchdb:x:106:113:CouchDB Administrator,,,:/var/lib/couchdb:/bin/bash
haldaemon:x:107:114:Hardware abstraction layer,,,:/var/run/hald:/bin/false
speech-dispatcher:x:108:29:Speech Dispatcher,,,:/var/run/speech-dispatcher:/bin/sh
kernoops:x:109:65534:Kernel Oops Tracking Daemon,,,:/:/bin/false
saned:x:110:116::/home/saned:/bin/false
pulse:x:111:117:PulseAudio daemon,,,:/var/run/pulse:/bin/false
gdm:x:112:119:Gnome Display Manager:/var/lib/gdm:/bin/false
polkituser:x:113:121:PolicyKit,,,:/var/run/PolicyKit:/bin/false
mysql:x:114:122:MySQL Server,,,:/var/lib/mysql:/bin/false
sshd:x:115:65534::/var/run/sshd:/usr/sbin/nologin

```

*   `man passwd`

### Grupos validos del sistema

Es posible indagar sobre grupos válidos del sistema revisando el archivo de configuracion de grupos **/etc/group** Ejemplo de contenido del arhivo **/etc/group**

```
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:usuario
tty:x:5:
disk:x:6:
lp:x:7:
mail:x:8:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:usuario
fax:x:21:
voice:x:22:
cdrom:x:24:usuario
floppy:x:25:
tape:x:26:
sudo:x:27:
audio:x:29:pulse
dip:x:30:
www-data:x:33:
backup:x:34:
operator:x:37:
list:x:38:
irc:x:39:
src:x:40:
gnats:x:41:

```

### Passwords de usuarios del sistema

Dependiendo de la distribución GNU/Linux que estés usando las passwords estarán almacenadas con un algoritmo de encriptación diferente.

Generalmente las passwords son almacenadas en el archivo **/ etc/passwd** , pero si en lugar de la password existe una letra **x**, estas estarán almacenadas en el archivo **/ etc/shadow**

ejemplo del contenido del archivo / etc/shadow

```
root:!:14589:0:99999:7:::
daemon:*:14545:0:99999:7:::
bin:*:14545:0:99999:7:::
sys:*:14545:0:99999:7:::
sync:*:14545:0:99999:7:::
games:*:14545:0:99999:7:::
man:*:14545:0:99999:7:::
lp:*:14545:0:99999:7:::
mail:*:14545:0:99999:7:::
uucp:*:14545:0:99999:7:::
proxy:*:14545:0:99999:7:::
www-data:*:14545:0:99999:7:::
backup:*:14545:0:99999:7:::
list:*:14545:0:99999:7:::
irc:*:14545:0:99999:7:::
gnats:*:14545:0:99999:7:::
nobody:*:14545:0:99999:7:::
libuuid:!:14545:0:99999:7:::
syslog:*:14545:0:99999:7:::
messagebus:*:14545:0:99999:7:::
hplip:*:14545:0:99999:7:::
avahi-autoipd:*:14545:0:99999:7:::
avahi:*:14545:0:99999:7:::
couchdb:*:14545:0:99999:7:::
haldaemon:*:14545:0:99999:7:::
speech-dispatcher:!:14545:0:99999:7:::
kernoops:*:14545:0:99999:7:::
saned:*:14545:0:99999:7:::
pulse:*:14545:0:99999:7:::
gdm:*:14545:0:99999:7:::
usuario:$6$3v2OQ05R$9gWOCo3Xdh6v2NIsfCtye7L.ag3b12Y3dsrfGs/:14589:0:99999:7:::
polkituser:*:14592:0:99999:7:::
mysql:!:14594:0:99999:7:::
sshd:*:14595:0:99999:7:::

```

### Conexión a la Red

*   `man ifconfig`

Listando las interfaces de red con el comando **ifconfig**

```
eth0      Link encap:Ethernet  direcciónHW 00:1d:72:56:dc:f0  
          ACTIVO DIFUSIÓN MULTICAST  MTU:1500  Métrica:1
          Paquetes RX:0 errores:0 perdidos:0 overruns:0 frame:0
          Paquetes TX:0 errores:0 perdidos:0 overruns:0 carrier:0
          colisiones:0 long.colaTX:1000 
          Bytes RX:0 (0.0 B)  TX bytes:0 (0.0 B)
          Interrupción:27 Dirección base: 0x2000 

eth2      Link encap:Ethernet  direcciónHW 00:21:00:1b:6b:ed  
          Direc. inet:192.168.0.20  Difus.:192.168.0.255  Másc:255.255.255.0
          Dirección inet6: fe80::221:ff:fe1b:6bed/64 Alcance:Enlace
          ACTIVO DIFUSIÓN FUNCIONANDO MULTICAST  MTU:1500  Métrica:1
          Paquetes RX:41635 errores:0 perdidos:0 overruns:0 frame:280694
          Paquetes TX:28206 errores:8 perdidos:0 overruns:0 carrier:0
          colisiones:0 long.colaTX:1000 
          Bytes RX:23854793 (23.8 MB)  TX bytes:4222659 (4.2 MB)
          Interrupción:20 

lo        Link encap:Bucle local  
          Direc. inet:127.0.0.1  Másc:255.0.0.0
          Dirección inet6: ::1/128 Alcance:Anfitrión
          ACTIVO LOOPBACK FUNCIONANDO  MTU:16436  Métrica:1
          Paquetes RX:478 errores:0 perdidos:0 overruns:0 frame:0
          Paquetes TX:478 errores:0 perdidos:0 overruns:0 carrier:0
          colisiones:0 long.colaTX:0 
          Bytes RX:38029 (38.0 KB)  TX bytes:38029 (38.0 KB)

```

*   `man iwconfig`

Listando interfaces de red con soporte inalámbrico con el comando **iwconfig** , en este ejemplo se puede ver que la interfaz llamada **eth2**, posee soporte para red inalábrica y está conectada a la red llamada **Lacosox.org**

```
lo        no wireless extensions.

eth0      no wireless extensions.

eth2      IEEE 802.11bg  ESSID:"Lacosox.org"  Nickname:""
          Mode:Managed  Frequency:2.427 GHz  Access Point: 00:14:78:53:43:98   
          Bit Rate=54 Mb/s   Tx-Power:32 dBm   
          Retry min limit:7   RTS thr:off   Fragment thr:off
          Power Managementmode:All packets received

pan0      no wireless extensions.

```

*   `man iwlist`

Con iwlist es posible lista las redes inalábricas disponibles ( esta es solo una de las cosas que puede hacer). para esto se debe usar el comando **iwlist interfaz scan**

```
dalacost@urano:~$ sudo iwlist eth2 scan
eth2      Scan completed :
          Cell 01 - Address: 00:14:78:53:43:98
                    ESSID:"Lacosox.org"
                    Mode:Managed
                    Frequency:2.427 GHz (Channel 4)
                    Quality:5/5  Signal level:-27 dBm  Noise level:-92 dBm
                    IE: IEEE 802.11i/WPA2 Version 1
                        Group Cipher : TKIP
                        Pairwise Ciphers (2) : TKIP CCMP
                        Authentication Suites (1) : PSK
                        Preauthentication Supported
                    IE: WPA Version 1
                        Group Cipher : TKIP
                        Pairwise Ciphers (2) : TKIP CCMP
                        Authentication Suites (1) : PSK
                    Encryption key:on
                    Bit Rates:1 Mb/s; 2 Mb/s; 5.5 Mb/s; 11 Mb/s; 6 Mb/s
                              12 Mb/s; 24 Mb/s; 36 Mb/s; 9 Mb/s; 18 Mb/s
                              48 Mb/s; 54 Mb/s

```

-- **Ver también: [Configuración_de_interfaces_de_red](/index.php?title=Configuraci%C3%B3n_de_interfaces_de_red&action=edit&redlink=1 "Configuración de interfaces de red (page does not exist)")**.

### Puntos de Montaje

`man df`

Salida de ejemplo del comando **df**

```
S.ficheros         Bloques de 1K   Usado    Dispon Uso% Montado en
/dev/sda6             25292348   9499996  14507556  40% /
udev                    965856       296    965560   1% /dev
none                    965856       188    965668   1% /dev/shm
none                    965856       224    965632   1% /var/run
none                    965856         4    965852   1% /var/lock
none                    965856         0    965856   0% /lib/init/rw
none                  25292348   9499996  14507556  40% /var/lib/ureadahead/debugfs
/dev/sda5             48229064  42094984   3684172  92% /opt
/dev/sr0               4298428   4298428         0 100% /media/cdrom0

```

También es posible obtener otro tipo de información sobre los puntos de montaje en el archivo de configuración de estos en **/etc/fstab**

```
cat /etc/fstab

```

### Carga

*   `man top`

Salida normal del comando **top**

```
top - 22:42:52 up  5:39,  2 users,  load average: 0.11, 0.08, 0.01
Tasks: 178 total,   1 running, 177 sleeping,   0 stopped,   0 zombie
Cpu(s): 11.4%us,  2.4%sy,  0.0%ni, 85.7%id,  0.5%wa,  0.0%hi,  0.0%si,  0.0%st
Mem:   1931712k total,  1330640k used,   601072k free,    80900k buffers
Swap:   393584k total,        0k used,   393584k free,   541492k cached

  PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND            
 2875 dalacost  20   0  332m 120m  30m S   18  6.4  15:15.57 firefox            
 1399 root      20   0 88484  64m  16m S    3  3.4  12:24.84 Xorg               
 4134 dalacost  20   0 30280 9.9m 8144 S    2  0.5   4:51.22 gkrellm            
10594 dalacost  20   0  2472 1200  884 R    1  0.1   0:02.56 top                
 2155 dalacost  20   0 97300 9416 7124 S    0  0.5   0:06.08 gnome-settings-    
 2177 dalacost  20   0 28460  11m 8888 S    0  0.6   0:32.31 metacity           
 2189 dalacost  20   0 52748  27m  16m S    0  1.4   0:37.62 gnome-panel        
 3077 dalacost  20   0 39288  14m  10m S    0  0.7   0:15.04 gnome-terminal     
    1 root      20   0  2664 1536 1128 S    0  0.1   0:01.19 init               
    2 root      15  -5     0    0    0 S    0  0.0   0:00.00 kthreadd           
    3 root      RT  -5     0    0    0 S    0  0.0   0:00.01 migration/0        
    4 root      15  -5     0    0    0 S    0  0.0   0:00.15 ksoftirqd/0        
    5 root      RT  -5     0    0    0 S    0  0.0   0:00.00 watchdog/0         
    6 root      RT  -5     0    0    0 S    0  0.0   0:00.01 migration/1        
    7 root      15  -5     0    0    0 S    0  0.0   0:04.45 ksoftirqd/1        
    8 root      RT  -5     0    0    0 S    0  0.0   0:00.00 watchdog/1         
    9 root      15  -5     0    0    0 S    0  0.0   0:00.05 events/0           
   10 root      15  -5     0    0    0 S    0  0.0   0:00.24 events/1           
   11 root      15  -5     0    0    0 S    0  0.0   0:00.00 cpuset             
   12 root      15  -5     0    0    0 S    0  0.0   0:00.00 khelper            
   13 root      15  -5     0    0    0 S    0  0.0   0:00.00 netns              
   14 root      15  -5     0    0    0 S    0  0.0   0:00.00 async/mgr          
   15 root      15  -5     0    0    0 S    0  0.0   0:00.00 kintegrityd/0      
   16 root      15  -5     0    0    0 S    0  0.0   0:00.00 kintegrityd/1      
   17 root      15  -5     0    0    0 S    0  0.0   0:00.00 kblockd/0          
   18 root      15  -5     0    0    0 S    0  0.0   0:00.02 kblockd/1          
   19 root      15  -5     0    0    0 S    0  0.0   0:00.00 kacpid             
   20 root      15  -5     0    0    0 S    0  0.0   0:00.12 kacpi_notify       
   21 root      15  -5     0    0    0 S    0  0.0   0:00.00 kacpi_hotplug      
   22 root      15  -5     0    0    0 S    0  0.0   0:00.01 ata/0              
   23 root      15  -5     0    0    0 S    0  0.0   0:00.99 ata/1              
   24 root      15  -5     0    0    0 S    0  0.0   0:00.00 ata_aux            
   25 root      15  -5     0    0    0 S    0  0.0   0:00.00 ksuspend_usbd      
   26 root      15  -5     0    0    0 S    0  0.0   0:00.00 khubd              
   27 root      15  -5     0    0    0 S    0  0.0   0:00.04 kseriod 

```

*   `man uptime`

Salida normal del comando **uptime**

```
 22:45:07 up  5:41,  2 users,  load average: 0.49, 0.20, 0.06

```

*   `man free`

Salida normal del comando **free**

```
            total       used       free     shared    buffers     cached
Mem:       1931712    1329772     601940          0      81328     541600
-/+ buffers/cache:     706844    1224868
Swap:       393584          0     393584

```

*   `man w`

Salida normal del comando **w**

```
 22:45:38 up  5:41,  2 users,  load average: 0,48, 0,23, 0,07
USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT
dalacost tty7     :0               17:04    8:41m 12:40   0.50s gnome-session
dalacost pts/1    :0.0             17:52    0.00s  0.25s  0.01s w

```

### Mensaje de bienvenida en sesión de texto

El archivo **motd** contiene el *Message of The Day* o Mensaje del Día, una tradición de los sistemas UNIX de mostrar un mensaje a un usuario al iniciar su sesión.

```
cat /etc/motd

```

### Mensajes de Error Recientes

```
cat /var/log/dmesg

```

```
cat /var/log/kern.log

```

### Presencia de otros Sistemas Operativos

Una Forma rápida de verificar si la máquina es capaz de arrancar con otros sistemas operativos instalados, es revisar los archivos de configuración del software encargado de arrancar el kernel.

#### Archivo de configuración de grub

```
cat /boot/grub/grub.cfg

```

#### Archivo de configuración de lilo

```
cat /etc/lilo.conf

```

## Servicios

### Escaneando los servicios de red activos en puertos públicos

Un excelente software para el verificar los puertos abiertos en tu máquina es **nmap**, aquí un ejemplo de como utilizarlo.

```
nmap localhost

```

Posible salida, se puede observar que esta máquina ejecuta servicios en los puertos 22, 80, 135, 139, 445, 631, 1024, 3306

```
Starting Nmap 5.00 ( [http://nmap.org](http://nmap.org) ) at 2010-02-01 18:24 CLST
Warning: Hostname localhost resolves to 2 IPs. Using 127.0.0.1.
Interesting ports on localhost (127.0.0.1):
Not shown: 992 closed ports
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
631/tcp  open  ipp
1024/tcp open  kdm
3306/tcp open  mysql

```