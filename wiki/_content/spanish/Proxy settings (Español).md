## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Variables de entorno](#Variables_de_entorno)
    *   [2.1 Mantener el proxy a través de sudo](#Mantener_el_proxy_a_trav.C3.A9s_de_sudo)
    *   [2.2 Automatización con los administradores de red](#Automatizaci.C3.B3n_con_los_administradores_de_red)
*   [3 Acerca de libproxy](#Acerca_de_libproxy)
*   [4 Opciones proxy web](#Opciones_proxy_web)
    *   [4.1 Proxy simple con SSH](#Proxy_simple_con_SSH)
*   [5 Utilizar un proxy SOCKS](#Utilizar_un_proxy_SOCKS)
*   [6 Configuración de proxy en GNOME3](#Configuraci.C3.B3n_de_proxy_en_GNOME3)
*   [7 Proxy NTLM de Microsoft](#Proxy_NTLM_de_Microsoft)
    *   [7.1 Configuración](#Configuraci.C3.B3n)
    *   [7.2 Utilización](#Utilizaci.C3.B3n)

## Introducción

Un proxy es *una interfaz para un servicio, especialmente para uno que está a distancia, utilización intensiva de recursos o, de otra manera, difícil de usar directamente*. Fuente: [Proxy - Wiktionary](http://en.wiktionary.org/wiki/proxy).

## Variables de entorno

Algunos programas (como [wget](/index.php/Wget "Wget")) utilizan variables de entorno con el formato «protocol_proxy» para determinar el proxy para un protocolo determinado (por ejemplo, HTTP, FTP, ...).

A continuación se muestra un ejemplo sobre cómo configurar estas variables en una shell:

```
 export http_proxy=http://10.203.0.1:5187/
 export https_proxy=$http_proxy
 export ftp_proxy=$http_proxy
 export rsync_proxy=$http_proxy
 export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com"

```

Algunos programas buscan la versión en mayúsculas de las variables de entorno.

Si las variables de entorno del proxy son aplicables a todos los usuarios y a todas las aplicaciones, las órdenes de exportación arriba mencionadas se pueden añadir a un script, por ejemplo «proxy.sh», colocado dentro del directorio /etc/profile.d/. El script ha de marcarse como ejecutable. Este método es útil cuando se utiliza un entorno de escritorio como [Xfce](/index.php/Xfce "Xfce") que no proporciona una opción para la configuración del proxy. Por ejemplo, el navegador [Chromium](/index.php/Chromium "Chromium") hará uso de las variables establecidas, usando este método mientras se ejecuta XFCE.

Alternativamente, se puede automatizar la alternancia de las variables mediante la adición de una función al archivo .bashrc (gracias a Alan Pope por la idea del script original)

```
function proxy_on() {
    export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com"

    if (( $# > 0 )); then
        valid=$(echo $@ | sed -n 's/\([0-9]\{1,3\}.\)\{4\}:\([0-9]\+\)/&/p')
        if [[ $valid != $@ ]]; then
            >&2 echo "Invalid address"
            return 1
        fi

        export http_proxy="http://$1/"
        export https_proxy=$http_proxy
        export ftp_proxy=$http_proxy
        export rsync_proxy=$http_proxy
        echo "Proxy environment variable set."
        return 0
    fi

    echo -n "username: "; read username
    if [[ $username != "" ]]; then
        echo -n "password: "
        read -es password
        local pre="$username:$password@"
    fi

    echo -n "server: "; read server
    echo -n "port: "; read port
    export http_proxy="http://$pre$server:$port/"
    export https_proxy=$http_proxy
    export ftp_proxy=$http_proxy
    export rsync_proxy=$http_proxy
    export HTTP_PROXY=$http_proxy
    export HTTPS_PROXY=$http_proxy
    export FTP_PROXY=$http_proxy
    export RSYNC_PROXY=$http_proxy
}

function proxy_off(){
    unset http_proxy
    unset https_proxy
    unset ftp_proxy
    unset rsync_proxy
    echo -e "Proxy environment variable removed."
}

```

Si no necesitamos el nombre de usuario y la contraseña, los omitimos.

Como alternativa, es posible que desee utilizar el siguiente script. Cambie las cadenas «YourUserName», «ProxyServerAddress:Port», «LocalAddress» y «LocalDomain» para ajustarlos con sus propios datos, luego, edite el archivo `~/.bashrc` para incluir las funciones modificadas. Cualquier nueva ventana bash tendrá operativa las nuevas funciones. En las ventanas de bash existentes, escriba `source ~/.bashrc` para poder utilizar dichas funciones. Es posible que prefiera poner la definición de dichas funciones en un archivo separado, como por ejemplo `functions`, y añadir `source functions` a `.bashrc`, en vez de poner todo en `.bashrc`. También es posible que desee cambiar el nombre de «myproxy» por algo más fácil y corto de escribir.

```
 #!/bin/bash

 assignProxy(){
   PROXY_ENV="http_proxy ftp_proxy https_proxy all_proxy HTTP_PROXY HTTPS_PROXY FTP_PROXY ALL_PROXY"
   for envar in $PROXY_ENV
   do
     export $envar=$1
   done
   for envar in "no_proxy NO_PROXY"
   do
      export $envar=$2
   done
 }

 clrProxy(){
   assignProxy "" # This is what 'unset' does.
 }

 myProxy(){
   user=YourUserName
   read -p "Password: " -s pass &&  echo -e " "
   proxy_value="http://$user:$pass@ProxyServerAddress:Port"
   no_proxy_value="localhost,127.0.0.1,LocalAddress,LocalDomain.com"
   assignProxy $proxy_value $no_proxy_value
 }

```

### Mantener el proxy a través de sudo

Si se establecen las variables de entorno del proxy solo para el usuario (por ejemplo, usando órdenes manuales o .bashrc) estas se pierden cuando se ejecutan órdenes con [sudo](/index.php/Sudo "Sudo") (o cuando programas como [yaourt](/index.php/Yaourt "Yaourt") utilizan sudo internamente).

Una manera de evitarlo es añadir la siguiente línea al archivo de configuración de sudo (accesible con visudo):

```
Defaults env_keep += "http_proxy https_proxy ftp_proxy"

```

También puede añadir cualquier otra variable de entorno, como rsync_proxy, o no_proxy.

### Automatización con los administradores de red

*   [NetworkManager](/index.php/NetworkManager "NetworkManager") no puede cambiar las variables de entorno.
*   [netctl](/index.php/Netctl "Netctl") podría programar estas variables de entorno, pero no serían vistas por otras aplicaciones ya que no descienden de netctl.

## Acerca de libproxy

[libproxy](http://code.google.com/p/libproxy/) (que está disponible en el repositorio extra) es una biblioteca de abstracción que puede ser utilizada por todas las aplicaciones que deseen acceder a un recurso de red. Todavía está en desarrollo, pero podría llegar a ser a un gestor unificado y automatizado de proxies en GNU/Linux si es ampliamente adoptado.

La función de libproxy es leer la configuración del proxy desde las diferentes fuentes y ponerla a disposición de las aplicaciones que utilizan la biblioteca. La parte interesante de libproxy es que ofrece una implementación de la [Web Proxy Autodiscovery Protocol](https://en.wikipedia.org/wiki/Web_Proxy_Autodiscovery_Protocol "wikipedia:Web Proxy Autodiscovery Protocol") y una implementación de [Proxy Auto-Config](https://en.wikipedia.org/wiki/Proxy_auto-config "wikipedia:Proxy auto-config") que va con ella.

El binario `/usr/bin/proxy` toma URL(s) como argumento(s) y devuelve el proxy/proxies que podría ser usado para obtener este/estos recurso(s) de red.

**Nota:** La versión 0.4.11 no soporta http_proxy='wpad:' dado que `{ pkg-config 'mozjs185 >= 1.8.5'; }` falla.

Desde 06/04/2009, libproxy es requerido por libsoup. Este se utiliza indirectamente por el navegador [Midori](https://www.archlinux.org/packages/extra/i686/midori/).

## Opciones proxy web

*   [Squid](/index.php/Squid "Squid") es un popular proxy almacenador/optimizador.
*   [Privoxy](/index.php/Privoxy "Privoxy") es un proxy para el anonimato y el bloqueo de anuncios.
*   Para un proxy simple, puede utilizarse ssh con el redireccionamiento de puertos.

### Proxy simple con SSH

Conéctese a un servidor (HOST) en el que tenga una cuenta (USER) de la siguiente manera:

```
ssh -D PORT USER@HOST

```

Para PORT, seleccione un número que no sea un puerto IANA registrado. Esto especifica que el tráfico en el puerto local se enviará al equipo remoto. ssh actuará como un servidor [SOCKS](https://en.wikipedia.org/wiki/SOCKS "wikipedia:SOCKS"). El sotfware da soporte a los servidores proxy SOCKS que permite una configuración simple para conectar con el puerto (PORT) en el servidor local.

## Utilizar un proxy SOCKS

Hay dos casos:

*   la aplicación que desea utilizar maneja proxies [SOCKS5](https://en.wikipedia.org/wiki/SOCKS#SOCKS5 "wikipedia:SOCKS") (por ejemplo [Firefox](/index.php/Firefox "Firefox")), por tanto, solo hay que configurarla para utilizar el proxy.
*   la aplicación que desea utilizar no maneja proxies SOCKS, con lo que puede probar utilizando una aplicación intermedia como [tsocks](https://www.archlinux.org/packages/?name=tsocks) o [proxychains-ng](https://www.archlinux.org/packages/?name=proxychains-ng).

En Firefox, puede utilizar el proxy SOCKS en las Preferencias del menú> Avanzado> Red> Configuración de conexión. Seleccione la opción «Configuración manual del proxy», y establezca el Servidor SOCKS (y solo este, asegúrese de que los otros campos, como el proxy HTTP o SSL queden vacíos). Por ejemplo, si un proxy SOCKS5 se ejecuta en el puerto 8080 de localhost, escriba «127.0.0.1» en el campo Servidor SOCKS, «8080» en el campo Puerto, y Aceptar. localhost, 127.0.0.1

Si usa *proxychains-ng*, la configuración se realiza en `/etc/proxychains.conf`. Puede que tenga que anular el comentario de la última línea (establecido por defecto para utilizar [Tor](/index.php/Tor "Tor")), y reemplazarlo con los parámetros del proxy SOCKS. Por ejemplo, si está utilizando el mismo proxy SOCKS5 que el anterior, tendrá que reemplazar la última línea por:

```
socks5 127.0.0.1 8080

```

Entonces, *proxychains-ng* puede ser lanzado con:

```
proxychains <programa>

```

donde <programa> puede ser cualquier programa ya instalado en el sistema (por ejemplo, xterm, gnome-terminal, etc.).

## Configuración de proxy en GNOME3

Algunos programas como [Chromium](/index.php/Chromium "Chromium") prefieren utilizar las configuraciones almacenadas por Gnome. Estos ajustes se pueden modificar a través de la interfaz gnome-control-center o a través de gsettings.

```
gsettings set org.gnome.system.proxy mode 'manual' 
gsettings set org.gnome.system.proxy.http host 'proxy.localdomain.com'
gsettings set org.gnome.system.proxy.http port 8080
gsettings set org.gnome.system.proxy.ftp host 'proxy.localdomain.com'
gsettings set org.gnome.system.proxy.ftp port 8080
gsettings set org.gnome.system.proxy.https host 'proxy.localdomain.com'
gsettings set org.gnome.system.proxy.https port 8080
gsettings set org.gnome.system.proxy ignore-hosts "['localhost', '127.0.0.0/8', '10.0.0.0/8', '192.168.0.0/16', '172.16.0.0/12' , '*.localdomain.com' ]"

```

Esta configuración también se puede ajustar para ejecutarse automáticamente cuando [Network Manager](/index.php/NetworkManager#Proxy_settings "NetworkManager") se conecte a redes específicas, utilizando el paquete [proxydriver](https://aur.archlinux.org/packages/proxydriver/) disponible en [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

## Proxy NTLM de Microsoft

En una red de Windows, se utiliza NT LAN Manager (NTLM) que es un conjunto de protocolos de seguridad de Microsoft que proporciona autenticación, integridad y confidencialidad a los usuarios.

[cntlm](https://aur.archlinux.org/packages/cntlm/) disponible en [AUR](/index.php/AUR "AUR") se interpone entre las aplicaciones y el proxy NTLM, añadiendo autenticación NTLM sobre la marcha. Puede especificar varios proxies «jerarquicamente» y Cntlm sondeará uno tras otro hasta que uno funcione. Todas las conexiones autenticadas se almacenan en caché y vuelven a ser utilizadas para lograr una alta eficiencia.

```
(NTLM PROXY IP:PORT + CREDENTIALS + OTHER INFO) -----> **(127.0.0.1:PORT)**

```

### Configuración

Cambie la configuración en `/etc/cntlm.conf`, según sus necesidades, a excepción de la contraseña. A continuación, ejecute:

```
$ cntlm -H

```

Esto va a generar [hashes](https://en.wikipedia.org/wiki/es:Funci%C3%B3n_hash "wikipedia:es:Función hash") de contraseñas encriptadas de acuerdo al nombre del equipo del proxy, nombre del usuario y la contraseña.

**Advertencia:** [ettercap](https://www.archlinux.org/packages/?name=ettercap) puede fácilmente [sniffar](https://en.wikipedia.org/wiki/es:Detecci%C3%B3n_de_sniffer "wikipedia:es:Detección de sniffer") su contraseña a través de una LAN si utiliza contraseñas en texto plano en lugar de hashes cifrados.

Edite `/etc/cntlm.conf` de nuevo e incluya los tres valores hash generados y, a continuación, [active](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") `cntlm.service`.

Para probar la configuración, ejecute:

```
$ cntlm -v

```

### Utilización

Utilice esta dirección como un proxy:

```
127.0.0.1:PORT

```

o

```
localhost:PORT

```

`PORT` coincide con el parámetro `Listen` en `/etc/cntlm.conf`, que por defecto es `3128`.