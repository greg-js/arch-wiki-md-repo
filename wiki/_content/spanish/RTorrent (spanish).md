RTorrent es un cliente de bittorrent muy sencillo, elegante y ultraligero. Está escrito en C++ y utiliza ncurses, está basado completamente por tanto en texto y corre enteramente en consola. RTorrent es ideal para sistemas poco potentes y con el añadido de GNU Screen y openssh es adecuado para utilizar como cliene de bittorrnt remoto.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Configuración recomendada](#Configuración_recomendada)
*   [3 Controles](#Controles)
*   [4 Usar RTorrent con Screen](#Usar_RTorrent_con_Screen)
*   [5 Consejos adicionales](#Consejos_adicionales)
*   [6 Conclusión](#Conclusión)
*   [7 Vea también](#Vea_también)

## Instalación

```
pacman -S rtorrent

```

## Configuración

Antes de ejecutar RTorrent, el primer paso debe ser copiar el archivo de configuración por defecto que está disponible en la [página del proyecto](http://libtorrent.rakshasa.no/browser/trunk/rtorrent/doc/rtorrent.rc?rev=1027&format=raw) RTorrent y grabarlo el archivo como .rtorrent.rc en su directorio de usuario.

Una vez que el archivo ha sido grabado, ábralo con editor de texto preferido y haga los cambios que sean necesarios. Simplemente tendrá que descomentar las opciones que desee hbilitar o utiizar. Para conseguir información más detallada de las opciones disponibles, visite [RTorrent Common Tasks](http://libtorrent.rakshasa.no/wiki/RTorrentCommonTasks)

### Configuración recomendada

Los valores que se presentan a continuación son completamente subjetivos y dependientes de su propio sistema. Para descubrir la configuración óptima para uso propio, visite el siguiente sitio web y siga las instrucciones: [Optimize Your BitTorrent Download Speed](http://torrentfreak.com/optimize-your-BitTorrent-download-speed)

```
# Máximo y mínimo númreo de pares por torrent.
#min_peers = 40
max_peers = 52

# Lo mismo de antes pero para las semillas ya completadas ("seeds") (-1 = tantos como los que lo estén bajando)
#min_peers_seed = 10
max_peers_seed = 52

# Máximo número de subidas simultáneas por torrent.
max_uploads = 8

# Ratio global de subida y bajada en KiB. "0" para si límite.
download_rate = 200
upload_rate = 28

```

La siguiente opción determinará donde se grabarán sus torrents. Cambie el directorio por defecto al que usted quiera utilizar. Asegúrese de introducir la ruta absoluta; hay un extraño error en RTorrent que hace que *a veces* no respete las rutas relativas (esto es, ~/torrents):

```
# Directorio por defecto para grabar los torrents bajados.
directory = /home/[user]/torrents/

```

Esta opción permitirá a RTorrent grabar el progreso de sus torrents. Asegúrese de crear un directorio llamado .session. Simplemente ejecute como un usuario normal:

```
mkdir ~/.session

```

```
# Directorio de sesión por defecto. Asegúrese de no ejecutar varias instancias
# de rtorrent que usen el mismo directorio de sesión. ¿Usando tal vez una ruta
# relativa?
session = /home/[user]/.session/

```

La siguiente opción hará que RTorrent "vigile" un directorio determinado por nuevos archivos .torrent. Utilizando su navegador, cuando encuentre un archivo torrent que quiera bajar, sólo tendrá que grabar el archivo en este directorio y RTorrent arrancará automáticamente el torrent. Asegúrese de crear el directorio que será puesto en vigilancia (simplemente ejecute como un usuario normal:*mkdir ~/watch*):

```
# Vigilar un directorio en busca de nuevos torrents, y parar aquellos que hayan sido 
# borrados.
#schedule = watch_directory,5,5,load_start=./watch/*.torrent
#schedule = untied_directory,5,5,stop_untied=
schedule = watch_directory,5,5,load_start=/home/[user]/watch/*.torrent
schedule = untied_directory,5,5,stop_untied=
schedule = tied_directory,5,5,start_tied=

```

La siguiente opción hará que RTorrent deje de bajar cuando sea bajo el espacio en disco. Esto es particularmente útil con [Seedbox](https://en.wikipedia.org/wiki/Seedbox "wikipedia:Seedbox") allí donde el espacio de disco sea muy limitad. Cambie el valor a su gusto:

```
# Cierre torrents cuando el espacio de disco sea bajo.
schedule = low_diskspace,5,60,close_low_diskspace=100M

```

Esta opción a continuación establecerá qué puerto será usado para la escucha. Se recomienda utilizar un puerto por encima de 49152\. RTorrent permite el uso de un único puerto en vez de un rango de elos; se recomienda utilizar un único puerto en vez de un rango real.

```
# Rango de puertos par usar en la escucha.
port_range = 49164-49164

```

La siguiente opción permite la comprobación del "hash" cuando se completa un torrent o cuando se rearranca RTorrent. Esto asegurará que no haya errores en sus archivos.

```
# Comprobación de "hash" para los torrents completados. Podría ser útil mientras no se 
# arregle el error que causa que la falta de espacio de disco no sea avisada convenientemente.
check_hash = yes

```

La siguiente opción permite la habilitación del cifrado. Esto es muy importante habilitar esto, si no ya por usted, por aquellos otros en la marea del torrent, que pudieran necesitar la ofuscación del uso del ancho de banda a su ISP. No le hace daño habilitarlo aunque usted no necesite tal protección. Más información: [Bittorrent Protocol Encryption](https://en.wikipedia.org/wiki/BitTorrent_protocol_encryption "wikipedia:BitTorrent protocol encryption")

```
# Opciones de cifrado, no establezca ninguna (situación por defecto) o establezca una combinación de las siguientes::
# allow_incoming, try_outgoing, require, require_RC4, enable_retry, prefer_plaintext
#
# El valor del ejemplo permite conexiones cifradas entrantes, arranca conexiones de salida
# no cifradas pero las reintenta con cifrado si fallan, prefiriendo
# texto plano a cifrado RC4 después del apretón de manos cifrado ("encrypted handshake")
#
# encryption = allow_incoming,enable_retry,prefer_plaintext
encryption = allow_incoming,try_outgoing,enable_retry

```

Lo siguiente es para utilizar DHT. Si usa trackers públicos, querrá habilitar DHT par adquirir más pares. Si únicamente utiliza trackers privados, **no habilite DHT** ya que esto reducirá sus velocidades y puede poner en riesgo su privacidad. Algunos trackers incluso le advertirán si usa DHT.

```
# Habilitar la posibilidad de DHT para torrents sin tracker o cuando todos los trackers están caidos.
# Puede ser configurado como "disable" (deshabilitación completa de DHT), "off" (no arrancar DHT),
# "auto" (arrancar y parar DHT según se necesite), o "on" (arrancar DHT inmediatamente).
# El valor por defecto es "off". Para que funcione DHT, hay que definir un directorio de sesión.
# 
# dht = auto

# Puerto UDP para ser tilizado por DHT. 
# 
# dht_port = 6881

# Permitir intercambio entre pares (para torrents no marcados como privados)
#
# peer_exchange = yes

```

Asegúrese de acomodar los puertos apropiados con su router si utiliza uno. Se puede encontrar una guía decente por fabricante/modelo del router [aquí](http://portforward.com/english/routers/port_forwarding/routerindex.htm).

## Controles

RTorrent recibe instrucciones exclusivamente por mdio del teclado. Hay disponible una completa guía en el sitio principal [RTorrent User Guide](http://libtorrent.rakshasa.no/wiki/RTorrentUserGuide)

Esto es lo básico para comenzar:

*   Control-q : cierra RTorrent al pulsarlo dos veces.
*   Left arrow : vuelve a la pantalla anterior.
*   Right arrow : va a la siguiente pantalla.
*   a|s|d : incrementa la velocidad de subida global unos 1|5|50 KB/s
*   A|S|D : incrementa la velocidad de bajada global unos 1|5|50 KB/s
*   z|x|c : decrementa la velocidad de subida global unos 1|5|50 KB/s
*   Z|X|C : decrementa la velocidad de bajada global unos 1|5|50 KB/s
*   Control-S : arranca la bajada de un torrent
*   Control-D : detiene y continua la bajada activa
*   + or - : cambia la prioridad de bajada del torrent seleccionado.
*   Backspace : añade el archivo .torrent especificado. Después de presionar este botón escriba la ruta completa o el URL del archivo .torrent file. Puede utilizar la tecla del tabulador u otros trucos como en bash.

## Usar RTorrent con Screen

Screen es un programa que permite pasar a segundo plano las aplicaciones en línea de comandos sin necesidad du utilizar X.

Para instalarlo:

```
pacman -S screen

```

y copie entonces, como un usuario normal, screenrc a su directorio personal:

```
cp /etc/screenrc ~/.screenrc

```

Para hacer que RTorrent arranque siempre con screen, añada lo siguiente a su archivo .screenrc:

```
screen -t rtorrent rtorrent 

```

Para arrancar screen + RTorrent, simplemente tiene que ejecutar *screen* desde un terminal. Control-D-A quitará screen y ejecutando *screen -raAd* abrirá screen de nuevo.

## Consejos adicionales

*   Para usar RTorrent con un tracker que utiliza https, haga lo siguiente como root:

```
cd /etc/ssl/certs
wget --no-check-certificate https://www.geotrust.com/resources/root_certificates/certificates/Equifax_Secure_Global_eBusiness_CA-1.cer
mv Equifax_Secure_Global_eBusiness_CA-1.cer Equifax_Secure_Global_eBusiness_CA-1.pem
c_rehash

```

Y de ahora en adelante ejecute RTorrent con:

```
rtorrent -o http_capath=/etc/ssl/certs

```

Asegúrese de cambiar .screenrc para que refleje este cambio si usa screen:

```
screen -t rtorrent rtorrent -o http_capath=/etc/ssl/certs

```

*   Para crear archivos .torrent, yo recomiendo [mktorrent](https://aur.archlinux.org/packages.php?do_Details=1&ID=10635&O=0&L=0&C=0&K=mktorrent&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd) para interfaz de línea de órdenes o [RubyTorrent](http://benclarke.ca/rubytorrent/) para interfaz gráfica de usuario.

## Conclusión

Rtorrent es un excelente cliente de bittorrent. Su rendimiento estelar, sus bajos requerimientos y excelente configurabilidad lo destaca frente a la competencia.

## Vea también

[Screen Tips](/index.php/Screen_Tips "Screen Tips")