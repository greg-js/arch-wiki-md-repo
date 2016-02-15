## Contents

*   [1 Mejorar la velocidad de acceso a la base de datos](#Mejorar_la_velocidad_de_acceso_a_la_base_de_datos)
*   [2 Mejorar la velocidad de las descargas](#Mejorar_la_velocidad_de_las_descargas)
    *   [2.1 Usar Powerpill](#Usar_Powerpill)
    *   [2.2 Usar powerpill-light (en desuso)](#Usar_powerpill-light_.28en_desuso.29)
    *   [2.3 Usar wget](#Usar_wget)
    *   [2.4 Usar aria2](#Usar_aria2)
        *   [2.4.1 Instalación](#Instalaci.C3.B3n)
        *   [2.4.2 Configuración](#Configuraci.C3.B3n)
        *   [2.4.3 Detalles de las opciones](#Detalles_de_las_opciones)
        *   [2.4.4 Notas adicionales](#Notas_adicionales)
    *   [2.5 Script para el mirror pacget (aria2)](#Script_para_el_mirror_pacget_.28aria2.29)
    *   [2.6 Utilizar otras aplicaciones](#Utilizar_otras_aplicaciones)
*   [3 Seleccionar el mirror más rápido](#Seleccionar_el_mirror_m.C3.A1s_r.C3.A1pido)
*   [4 Compartir paquetes a través de una red LAN](#Compartir_paquetes_a_trav.C3.A9s_de_una_red_LAN)

## Mejorar la velocidad de acceso a la base de datos

Pacman almacena toda la información relativa a los paquetes en una colección de archivos pequeños, uno por cada paquete. Mejorar la velocidad de acceso a la base de datos, reduce el tiempo necesario para completar las operaciones para las que aquellas se utilizan, por ejemplo, buscar paquetes y resolver las dependencias de los mismos. El método más seguro y rápido es ejecutar la siguiente orden, como root:

```
# pacman-optimize

```

De este modo, el sistema intentará reagrupar todos los archivos pequeños con la información de los paquetes en un ubicación (física) del disco duro, evitando que la cabeza del disco duro tenga que moverse en exceso cuando tenga que acceder a todos los paquetes. Este método es seguro, pero no es infalible. Su eficacia dependerá de factores como el sistema de archivos utilizado, del uso que se haga del disco y de la fragmentación del espacio vacío. Otra opción más agresiva sería quitar primero, de la caché, los paquetes desinstalados y eliminar los repositorios no utilizados, antes de optimizar la bases de datos:

```
# pacman -Sc && pacman-optimize

```

## Mejorar la velocidad de las descargas

**Nota:** Si las velocidades de descarga son mínimas, asegúrese de que está utilizando uno de los [mirrors](/index.php/Mirrors "Mirrors"), y no ftp.archlinux.org, cuyo ancho de banda está [reducido desde marzo de 2007](https://www.archlinux.org/news/302/).

La velocidad con que pacman descarga los paquetes se puede mejorar mediante el uso de una aplicación diferente para descargarlos, en lugar del descargador de archivos compilados de pacman.

En todos los casos, asegúrese de tener instalada la última versión de pacman antes de realizar cualquier modificación.

```
# pacman -Syu

```

### Usar Powerpill

PowerPill es un wrapper completo para Pacman que utiliza descargas paralelas y fragmentadas para acelerar el proceso de descarga. Normalmente Pacman descargará un paquete a la vez, y esperará a que se complete antes de comenzar la próxima descarga. PowerPill adopta un enfoque diferente: trata de acceder a la vez a tantos paquetes como sea posible.

La [página wiki de Powerpill](/index.php/Powerpill "Powerpill") proporciona una configuración básica y ejemplos de uso, junto con el paquete y enlaces upstream.

### Usar powerpill-light (en desuso)

[pacman2aria2](http://xyne.archlinux.ca/projects/pacman2aria2/) proporcina un script llamado «powerpill-light», que era un recurso provisional creado tras el desuso de powerpill original escrito en Perl. Ahora que [Powerpill](/index.php/Powerpill "Powerpill") se ha vuelto a publicar, powerpill-light está desatendido.

### Usar wget

Esta opción es muy útil si necesita configuraciones más avanzadas para el proxy respecto a las capacidades incorporadas en pacman.

Para usar `wget`, primero instálelo con `pacman -S wget` y, luego, modifique el archivo `/etc/pacman.conf`, para agregar la siguiente línea a la sección `[options]`:

```
XferCommand = /usr/bin/wget -c --passive-ftp -c %u

```

En lugar de poner los parámetros de `wget` en el archivo `/etc/pacman.conf`, puede modificar el archivo de configuración de `wget` directamente (el archivo que afecta a todo el sistema es `/etc/wgetrc`, mientras que los archivos que afectan únicamente a los usuarios están contenidos en `$HOME/.wgetrc`).

### Usar aria2

[aria2](/index.php/Aria2 "Aria2") es una utilidad ligera de descarga con apoyo para descargas fragmentadas y reanudables desde HTTP/HTTPS y FTP. [aria2](http://aria2.sourceforge.net/) permite conexiones HTTP/HTTPS y FTP mútiples y simultáneas a un mirror de Arch, que debería traducirse en un aumento en la velocidad de descarga de los archivos y la posibilidad de recuperación de los paquetes.

**Nota:** El uso de aria2c en el parámetro XferCommand de pacman **no** da como resultado descargas paralelas de varios paquetes. Pacman invoca la orden XferCommand con respecto a un único paquete a la vez y espera a que se complete antes de invocar el siguiente. Para descargar varios paquetes al mismo tiempo, véase cómo usar [powerpill-light](/index.php/Improve_pacman_performance#Usar_powerpill-light "Improve pacman performance") en la siguiente sección.

#### Instalación

Descargue e instale [aria2](https://www.archlinux.org/packages/?name=aria2) y sus dependencias:

```
# pacman -S aria2

```

#### Configuración

Modifique el archivo `/etc/pacman.conf` agregando la siguiente línea a la sección `[options]`:

 `XferCommand = /usr/bin/aria2c --allow-overwrite=true -c --file-allocation=none --log-level=error -m2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=60 -t5 -d / -o %o %u` 

#### Detalles de las opciones

	`/usr/bin/aria2c`

	La ruta completa al ejecutable aria2.

	`--allow-overwrite=true`

	Reinicia la descarga si el archivo de control correspondiente no existe. (Por defecto: false).

	`-c, --continue`

	Continua la descarga de un archivo descargado parcialmente, si el archivo de control correspondiente existe.

	`--file-allocation=none`

	No preasigna al archivo un espacio en el disco antes de que comience la descarga. (Por defecto: prealloc) 

	`--log-level=error`

	Establece el nivel de salida del registro solamente en caso de error. (Por defecto: debug).

	`-m2, --max-tries=2`

	Hace 2 intentos como máximo por mirror para descargar el archivo(s) especificado. (Por defecto: 5).

	`--max-connection-per-server=2`

	Establece un máximo de 2 conexiones para cada mirror por archivo. (Por defecto: 1).

	`--max-file-not-found=5`

	Fuerza la descarga al ser considerada como fallida si no se recibe un solo byte después de 5 intentos. (Por defecto: 0).

	`--min-split-size=5M`

	Divide el archivo si el tamaño es mayor que 2; 5 MB = 10 MB. (Por defecto: 20M).

	`--no-conf`

	Desactiva la carga si es que existe un archivo `aria2.conf`. (Por defecto: `~/.aria2/aria2.conf`)

	`--remote-time=true`

	Aplica marcas de tiempo de los archivos remotos a los archivo locales. (Por omisión: false).

	`--summary-interval=60`

	Muestra la salida del resumen del progreso de descarga cada 60 segundos. (Por defecto: 60) 

	`-t5, --timeout=5`

	Permite definir un tiempo de espera de 5 segundos por mirror después de establecer la conexión. (Por defecto: 60).

	`-d, --dir`

	El directorio para guardar el archivo(s) descargado como se especifica en [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)").

	`-o, --output`

	Salida del nombre del archivo(s) descargado.

	`%o`

	Variable que representa el nombre del archivo(s) local, según lo especificado por pacman.

	`%u`

	Variable que representa la dirección URL de descarga, según lo especificado por pacman.

#### Notas adicionales

	 `--file-allocation=falloc`

	Se recomienda para los sistemas de archivos más recientes, como ext4 (con soporte a las extensiones habilitadas), btrfs o xfs, ya que asigna la ubicación de archivos grandes (GB) casi al instante. No utilice falloc, para la preubicación, con sistemas de archivos antiguos como ext3, que consumen aproximadamente la misma cantidad de tiempo que la que consumiría la asignación estándar, bloqueando entre tanto el proceso de aria2 para realizar la descarga.

	 `--summary-interval=0`

	Suprime la salida del resumen del proceso de descarga y puede mejorar el rendimiento general. Los registros seguirán siendo escritos, de acuerdo con el valor especificado en la opción `log-level`.

	 `XferCommand = /usr/bin/printf 'Downloading ' && echo %u | awk -F/ '{printf $NF}' && printf '...' && /usr/bin/aria2c -q --allow-overwrite=true -c --file-allocation=none --log-level=error -m2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=0 -t5 -d / -o %o %u && echo ' Complete!'`

	El uso de la orden XferCommand proporciona una salida menos útil, pero mucho más fácil de leer.

### Script para el mirror pacget (aria2)

Este script mejora notablemente la velocidad de descarga para los usuarios de banda ancha. Utilice los servidores en `/etc/pacman.d/mirrorlist` como mirrors en aria2\. Lo que hace aria2 es descargar desde múltiples servidores al mismo tiempo, lo que le da un gran impulso a la velocidad de descarga.

**Nota:** Es necesario insertar «exec» antes de /usr/bin/pacget en XferCommand, de modo que al terminar pacget o aria2 (proceso utilizado por pacget), pacman también termine. Esto evitará inconvenientes, porque Pacman no insistirá en la descarga de un archivo cuando se le ordene interrumpirla.

**Advertencia:** Se pueden experimentar algunos problemas si los mirrors utilizados no están sincronizados o simplemente no están al día. Solo tiene que usar el script [Reflector](/index.php/Reflector_(Espa%C3%B1ol) "Reflector (Español)") para generar una lista de mirrors actualizados y _rápidos_. Además, ftp.archlinux.org viene resuelta con dos IPs. Es posible que desee elegir solo una de ellas y forzar al sistema a utilizar ftp.archlinux.org y la dirección IP elegida mediante `/etc/hosts`.

 `/usr/bin/pacget` 

```
#!/bin/bash

msg() {
  echo ""
  echo -e "   \033[1;34m->\033[1;0m \033[1;1m${1}\033[1;0m" >&2
}

error() {
  echo -e "\033[1;31m==> ERROR:\033[1;0m \033[1;1m$1\033[1;0m" >&2
}

CONF=/etc/pacget.conf
STATS=/etc/pacget.stats
ARIA2=$(which aria2c 2> /dev/null)

# ----- do some checks first -----
if [ ! -x "$ARIA2" ]; then
  error "aria2c was not found or isn't executable."
  exit 1
fi

if [ $# -ne 2 ]; then
  error "Incorrect number of arguments"
  exit 1
fi

filename=$(basename $1)
server=${1%/$filename}
arch=$(grep ^Architecture /etc/pacman.conf | cut -d '=' -f2 | sed 's/ //g')
if [[ $arch = "auto" ]]; then
  arch=$(uname -m)
fi
# Determine qué repositorio se está utilizando
repo=$(awk -F'/' '$(NF-2)~/^(community|core|extra|testing|comunity-testing|multilib)$/{print $(NF-2)}' <<< $server)
[ -z $repo ] && repo="custom"

# Para los archivos db, o cuando se utiliza un repositorio personalizado (que muy probablemente no tiene ningún mirror),
# Use solo la URL que le ha facilitado pacman, de lo contrario, extraiga la lista de servidores (desde el archivo «include» del repositorio) para la descarga desde
url=$1
if ! [[ $filename = *.db || $repo = "custom" ]]; then
  mirrorlist=$(awk -F' *= *' '$0~"^\\["r"\\]",/Include *= */{l=$2} END{print l}' r=$repo /etc/pacman.conf)
  if [ -n mirrorlist ]; then
    num_conn=$(grep ^split $CONF | cut -d'=' -f2)
    url=$(sed -r '/^Server *= */!d; s/Server *= *//; s/\$repo'"/$repo/"'; s/\$arch'"/$arch/; s/$/\/$filename/" $mirrorlist | head -n $(($num_conn *2)) )
  fi
fi

msg "Downloading $filename"
cd /var/cache/pacman/pkg/

touch $STATS

$ARIA2 --conf-path=$CONF --max-tries=1 --max-file-not-found=5 \
  --uri-selector=adaptive --server-stat-if=$STATS --server-stat-of=$STATS \
  --allow-overwrite=true --remote-time=true --log-level=error --summary-interval=0 \
  $url --out=${filename}.pacget && [ ! -f ${filename}.pacget.aria2 ] && mv ${filename}.pacget $2 && chmod 644 $2

exit $?

```

 `/etc/pacget.conf` 

```
# El archivo de registro
log=/var/log/pacget.log
# El número de servidores para la descarga
split=5
# Tamaño mínimo del archivo a partir del cual justifica su división, es decir descarga simultánea (default 20M)
min-split-size=1M
# Velocidad máxima de descarga (0 = sin restricciones)
max-download-limit=0
# Velocidad mínima de descarga (0 = no importa)
lowest-speed-limit=0
# Período de tiempo de espera del servidor
timeout=5
# «none» (ninguno) o «falloc» (preubicación)
file-allocation=none

```

Guarde este script como /usr/bin/pacget.

```
# chmod 755 /usr/bin/pacget

```

La orden anterior hace que el script sea ejecutable.

En la sección [options], del archivo /etc/pacman.conf, añada lo siguiente:

```
XferCommand = exec /usr/bin/pacget %u %o

```

**Nota:** Si utiliza ftp.archlinux.org como el primer servidor listado en los archivos _«include»_ (/etc/pacman.d/*), pueden ocurrir algunos problemas cuando los otros mirror que utiliza no se hayan sincronizado. Para hacer un mejor uso de este script, elija un mirror (que sincronice de manera oportuna) que sea el más apropiado para su caso, y colóquelo en la parte superior de la lista de servidores. Esto es para evitar descargar de ftp.archlinux.org, y hacer uso de este último solo para cuando los otros mirrors no han sido sincronizados aún. El script rankmirrors puede ser útil en este caso.

### Utilizar otras aplicaciones

Existen otras aplicaciones para realizar las descargas, que se pueden utilizar con Pacman. Vienen presentadas a continuación, con sus correspondientes ajustes en XferCommand:

*   `snarf`: `XferCommand = /usr/bin/snarf -N %u`
*   `lftp`: `XferCommand = /usr/bin/lftp -c pget %u`
*   `axel`: `XferCommand = /usr/bin/axel -n 2 -v -a -o %o %u`

## Seleccionar el mirror más rápido

Cuando pacman descarga paquetes utiliza los mirrors en el orden en que aparecen en `/etc/pacman.d/mirrorlist`. El primer mirror puede no ser el más rápido de la lista por defecto. Para seleccionar un mirror más rápido, véase [Mirrors](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)").

## Compartir paquetes a través de una red LAN

Si se dispone de más de una máquina con Arch Linux conectadas a una red local, se pueden compartir paquetes para disminuir los tiempos de descarga. Tenga presente que no se pueden compartir paquetes entre diferentes arquitecturas (es decir, i686 y x86_64) o generarán problemas.

Véase [Pacman tips#Network_shared_pacman_cache](/index.php/Pacman_tips#Network_shared_pacman_cache "Pacman tips").