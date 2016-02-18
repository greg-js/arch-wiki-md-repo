El archivo `rc.conf` (`/etc/rc.conf`) es archivo de configuración del sistema de ArchLinux. Contiene varias configuraciones editables para el usuario como zona horaria, mapa de teclado, módulos del kernel, demonios a cargar en el inicio, etcétera, en un archivo de texto editable para facilitar la administración del sistema.

## Contents

*   [1 Resumen](#Resumen)
*   [2 Localización](#Localizaci.C3.B3n)
*   [3 Hardware](#Hardware)
*   [4 Redes](#Redes)
*   [5 Demonios](#Demonios)

## Resumen

Este es un tipo archivo `rc.conf` sin alteraciones después de una instalación limpia de Arch Linux:

 `/etc/rc.conf` 
```
#
# /etc/rc.conf - Main Configuration for Arch Linux
#

# -----------------------------------------------------------------------
# LOCALIZATION
# -----------------------------------------------------------------------
#
# LOCALE: available languages can be listed with the 'locale -a' command
#   LANG in /etc/locale.conf takes precedence
# DAEMON_LOCALE: If set to 'yes', use $LOCALE as the locale during daemon
# startup and during the boot process. If set to 'no', the C locale is used.
# HARDWARECLOCK: set to "", "UTC" or "localtime", any other value will result
#   in the hardware clock being left untouched (useful for virtualization)
#   Note: Using "localtime" is discouraged, using "" makes hwclock fall back
#   to the value in /var/lib/hwclock/adjfile
# TIMEZONE: timezones are found in /usr/share/zoneinfo
#   Note: if unset, the value in /etc/localtime is used unchanged
# KEYMAP: keymaps are found in /usr/share/kbd/keymaps
# CONSOLEFONT: found in /usr/share/kbd/consolefonts (only needed for non-US)
# CONSOLEMAP: found in /usr/share/kbd/consoletrans
# USECOLOR: use ANSI color sequences in startup messages
#
LOCALE="en_US.UTF-8"
DAEMON_LOCALE="no"
HARDWARECLOCK="UTC"
TIMEZONE="Canada/Pacific"
KEYMAP="us"
CONSOLEFONT=
CONSOLEMAP=
USECOLOR="yes"

# -----------------------------------------------------------------------
# HARDWARE
# -----------------------------------------------------------------------
#
# MODULES: Modules to load at boot-up. Blacklisting is no longer supported.
#   Replace every !module by an entry as on the following line in a file in
#   /etc/modprobe.d:
#     blacklist module
#   See "man modprobe.conf" for details.
#
MODULES=()

# Udev settle timeout (default to 30)
UDEV_TIMEOUT=30

# Scan for FakeRAID (dmraid) Volumes at startup
USEDMRAID="no"

# Scan for BTRFS volumes at startup
USEBTRFS="no"

# Scan for LVM volume groups at startup, required if you use LVM
USELVM="no"

# -----------------------------------------------------------------------
# NETWORKING
# -----------------------------------------------------------------------
#
# HOSTNAME: Hostname of machine. Should also be put in /etc/hosts
#
HOSTNAME="myhost"

# Use 'ip addr' or 'ls /sys/class/net/' to see all available interfaces.
#
# Wired network setup
#   - interface: name of device (required)
#   - address: IP address (leave blank for DHCP)
#   - netmask: subnet mask (ignored for DHCP) (optional, defaults to 255.255.255.0)
#   - broadcast: broadcast address (ignored for DHCP) (optional)
#   - gateway: default route (ignored for DHCP)
# 
# Static IP example
# interface=eth0
# address=192.168.0.2
# netmask=255.255.255.0
# broadcast=192.168.0.255
# gateway=192.168.0.1
#
# DHCP example
# interface=eth0
# address=
# netmask=
# gateway=

interface=
address=
netmask=
broadcast=
gateway=

# Setting this to "yes" will skip network shutdown.
# This is required if your root device is on NFS.
NETWORK_PERSIST="no"

# Enable these netcfg profiles at boot-up. These are useful if you happen to
# need more advanced network features than the simple network service
# supports, such as multiple network configurations (ie, laptop users)
#   - set to 'menu' to present a menu during boot-up (dialog package required)
#   - prefix an entry with a ! to disable it
#
# Network profiles are found in /etc/network.d
#
# This requires the netcfg package
#
#NETWORKS=(main)

# -----------------------------------------------------------------------
# DAEMONS
# -----------------------------------------------------------------------
#
# Daemons to start at boot-up (in this order)
#   - prefix a daemon with a ! to disable it
#   - prefix a daemon with a @ to start it up in the background
#
# If you are sure nothing else touches your hardware clock (such as ntpd or
# a dual-boot), you might want to enable 'hwclock'. Note that this will only
# make a difference if the hwclock program has been calibrated correctly.
#
# If you use a network filesystem you should enable 'netfs'.
#
DAEMONS=(syslog-ng network crond)

```

## Localización

*   `[LOCALE](/index.php/LOCALE "LOCALE")`:Esto establece el idioma del sistema, será utilizado por todas las aplicaciones con interfaz a base i18n. Puede revisar la lista de soportes de idiomas disponibles ejecutando el comando `locale -a`. Esta variable esta puesta por default en el idioma Ingles de los estados unidos.
*   `HARDWARECLOCK`: Especifica si el reloj del sistema, que es sincronizado tanto al inicio como al apagado del sistema, se maneja por tiempo `UTC` o por `localtime`, el uso más común es el formato `UTC` por que simplifica el cambiar de hora al cambiar de zona horaria o con el sistema de horario de verano/invierno, sin embargo si el sistema está instalado en un equipo con arranque dual con otro sistema operativo que maneje localtime (como es el caso de Microsoft Windows) la opción a utilizar debe ser `localtime`.

**Nota:** GNU/Linux cambiara automáticamente a DST cuando la configuración de HARDWARECLOCK este puesta en UTC, sin importar si el sistema está corriendo en el momento que se entra en la configuración de DST. Cuando HARDWARECLOCK este puesto en localtime, el sistema no tratara de ajustar el reloj del sistema asumiendo que se encuentra en un sistema de doble arranque (dual boot) y que el otro sistema se hace cargo del cambio DST. Si ese no fuera el caso, el cambio DST debe ser hecho manualmente.

*   `TIMEZONE`: Especifica la zona horaria. Las zonas horarias posibles son las rutas relativas a los archivos de zona horaria encontrados en el directorio `/usr/share/zoneinfo`. Por ejemplo, una zona horaria alemana seria `Europe/Berlin`, que hace referencia al archivo `/usr/share/zoneinfo/Europe/Berlin`.
*   `[KEYMAP](/index.php/KEYMAP "KEYMAP")`: El mapa de teclado que se quiere utilizar. Si usted es de los estados unidos tal vez el mapa de teclado qwerty US (que es la configuración default) sea suficiente. Los mapas de teclado disponibles se encuentran listados en el directorio `/usr/share/kbd/keymaps`. Recuerde que esta configuración de teclado solo es válida para su TTY y no para su sus sistema de ventas o de escritorio.
*   `[CONSOLEFONT](/index.php/Fonts#Console_fonts "Fonts")` Define la fuente o tipo de letra a utilizar dentro de la TTY, las tipografías disponibles se encuentran listadas en el directorio `/usr/share/kbd/consolefonts`. Para mayor informacion ver: [Fonts_(Español)#Console fonts](/index.php/Fonts_(Espa%C3%B1ol)#Console_fonts "Fonts (Español)")
*   `[CONSOLEMAP](/index.php/Fonts#Console_fonts "Fonts")`: Define el mapa de caracteres de la consola que se va a cargar al inicio (por ejemplo 8859-1_to_uni). Los posibles mapas de consola están listados en el directorio `/usr/share/kbd/consoletrans`. Deberá encontrar un mapa de caracteres útil para su locale (por ejemplo 8859-1 para Latin1) si utiliza un sistema local basado en el estándar tuf8 o utiliza programas que generan salidas de 8 bits. Si utiliza X11 para su trabajo diario, recuerde que esta configuración solo afectara a la consola TTY.
*   `USECOLOR`: Habilita o deshabilita el uso de salidas de mensajes a color durante el arranque de sistema.

## Hardware

*   `MOD_AUTOLOAD`: Si esta puesto en “yes” Archlinux escaneara su hardware durante el arranque para intentar cargar automáticamente los módulos del kernel necesarios, esto utilizando [udev](/index.php/Udev "Udev").

**Tip:** El modulo auto-loading puede ser deshabilitado para acelerar el proceso de arranque, pero el usuario debe estar seguro que todos los módulos necesarios están listados en la lista de la sección `MODULES`. La utilería [hwdetect](/index.php/Hwdetect "Hwdetect") de detección de hardware puede ser utilizada para averiguar que módulos son necesarios por el sistema, lshwd es una opción disponible en el AUR[lshwd](https://aur.archlinux.org/packages/lshwd/)

*   `MOD_BLACKLIST`: Depreciado. Equivalente a listar los módulos con el signo (!) en la lista `MODULES` para bloquear que sean cargados al inicio.
*   `MODULES`: En esta lista se pueden listar manualmente los módulos a cargar durante el inicio de sistema sin necesidad de utilizar el método de auto detección de MOD_AUTOLOAD. Simplemente hay que agregar el nombre del modulo aquí, separando cada nombre de modulo con un espacio en blanco y poniendo opciones necesarias en el archivo `modprobe.conf`, los módulos que sean antecedidos por un signo de exclamación (!) se bloqueara su carga durante el inicio de sistema.

**Tip:** Un beneficio de especificar módulos de red es que las tarjetas de Ethernet serán detectadas en el orden que los módulos son listados. Esto previene una confusión a la hora de nombrar interfaces que a veces sucede con las interfaces de red, otro modo de evitar esto es utilizar nombres de interface estáticos configurando udev apropiadamente.

*   `USELVM`: Escanea por grupos de volúmenes LVM al inicio, requerido si maneja LVM en su sistema.

## Redes

*   `[HOSTNAME](/index.php/HOSTNAME "HOSTNAME")`: Es el nombre del equipo en la red (sin el nombre de dominio). Esto es totalmente personal siempre y cuando el nombre se centre en letras y números y algunos pocos caracteres especiales, en caso de cualquier duda se recomienda dejar el nombre default
*   `INTERFACES`: Aquí se agregan las configuraciones para las interfaces de red, las líneas comentadas incluyen una clara explicación de su configuración. SI no utiliza DHCP en su dispositivo de red, tenga en cuenta que el valor de la variable (cuyo nombre debe ser igual al nombre del dispositivo que se está configurando) equivaldrá a la salida del comando `ifconfig` si usted estuviera configurando el dispositivo de red manualmente desde la terminal.
*   `ROUTES`: Se pueden definir las rutas a redes estáticas aquí. Puede definir su propia red estática con sus propias reglas de ruteo. Vea el ejemplo ahí descrito de una ruta de salida default. Básicamente las partes encerradas en comentarios son idénticas a las que usted pasa con el comando route add, por eso el leer el manpage de route es recomendado, si no sabe que escribir aquí, deje esta parte tal como esta.
*   `NETWORKS`: Esto habilita ciertos perfiles de red al inicio. Los perfiles de red son una manera conveniente de manejar múltiples configuraciones de red, y su intención es remplazar la configuración estándar de `INTERFACES`/`ROUTES` (que sigue siendo la configuración recomendada para sistemas con solo una configuración de red). Si su equipo va a ser conectado a varias redes y varias veces (por ejemplo, una Laptop) entonces usted puede configurar perfiles en el directorio /etc/network.d. Hay plantillas de configuraciones en `/etc/network.d/examples` que pueden ser utilizados para crear perfiles.

## Demonios

*   `[DAEMONS](/index.php/DAEMONS "DAEMONS")`: Este arreglo contiene una sencilla lista de scripts almacenados en `/etc/rc.d/` que se ejecutaran durante el proceso de arranque. Las entradas a la lista son separadas por un espacio en blanco. Si las entradas a la lista son precedidas por un símbolo de exclamación (!), este no será ejecutado, si la entrada esta procedida por un símbolo de arroba (@) este será ejecutado en el background, por ejemplo la secuencia de inicio no esperara hasta el correcto inicio de un script para pasar al siguiente del arreglo de demonios. Generalmente no hay que cambiar la lista default para obtener un sistema funcional, pero si va a editar o modificar esta lista cada vez que instale programas o servicios (como `sshd`) seguramente necesitara que inicien con el arranque del sistema. Básicamente esta es la forma en que ArchLinux maneja los servicios de sistema, similar a lo que otros sistemas manejan con enlaces simbólicos al directorio `init.d`.

```
   Nota: El orden de inicio de los demonios  están listados en orden de importancia y de esa manera son cargados al inicio del sistema.

```