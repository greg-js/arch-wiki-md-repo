[Ntop](http://www.ntop.org/products/ntop/) es una herramienta de monitorización de tráfico de red basada en [libcap](http://www.tcpdump.org/), que ofrece estadísticas de red estilo RMON mediante a través del navegador de red.

## Contents

*   [1 Instalación y configuración](#Instalaci.C3.B3n_y_configuraci.C3.B3n)
*   [2 Trucos y consejos](#Trucos_y_consejos)
    *   [2.1 Interfaz web](#Interfaz_web)
    *   [2.2 Usuario y grupo](#Usuario_y_grupo)
*   [3 Resolución de problemas](#Resoluci.C3.B3n_de_problemas)
    *   [3.1 **ERROR** RRD: Disabled - unable to create base directory (err 13, /var/lib/ntop/rrd)](#.2A.2AERROR.2A.2A_RRD:_Disabled_-_unable_to_create_base_directory_.28err_13.2C_.2Fvar.2Flib.2Fntop.2Frrd.29)
    *   [3.2 Please enable make sure that the ntop html/ directory is properly installed](#Please_enable_make_sure_that_the_ntop_html.2F_directory_is_properly_installed)

## Instalación y configuración

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [ntop](https://www.archlinux.org/packages/?name=ntop) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). En la primera ejecución de ntop, debe configurar la contraseña de administrador:

```
# ntop

```

Seguidamente, tiene que editar el archivo de configuración (`/etc/conf.d/ntop`) y adaptarlo a sus necesidades. A continuación tiene un ejemplo de archivo de configuración, enfocándose en el host para conseguir tanta información de las conexiones de hosts como sea posible:

 `/etc/conf.d/ntop` 
```
# Parameters que se suministrarán a ntop.
NTOP_ARGS="-K -W 2323 -i enp1s0,wlp2s0 -M -s -4 -6 -s -u ntop -c -r 30 --w3c -t 3 -a /var/log/ntop/http.log -O /var/log/ntop/ -q --skip-version-check 0"

# ubicación del archivo de log.
NTOP_LOG="/var/log/ntop/ntop.log"

```

Inicie el servicio *ntop* de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") y si desea iniciar *ntop* en el arranque, habilítelo.

## Trucos y consejos

### Interfaz web

Para acceder a la interfaz web de ntop, Introduzca [http://127.0.0.1:3000/](http://127.0.0.1:3000/) en su navegador. Para efectuar cambios en el servidor, tendrá que introducir su usuario (por defecto = *admin*) y su contraseña.

Si usa ntop no solo en su máquina local, sino también con múltiples usuarios en la red, lo más indicado es que **solo** permita conexiones SSL (http**s**).

```
# ntop -W 4223

```

Se permite el uso de parámetros adicionales. Vaya ahora a la siguiente dirección en el navegador [https://127.0.0.1:4223/](https://127.0.0.1:4223/).

También puede suministrar a ntop su propio certificado SSL. Tan solo debe colocarlo en el directorio de configuración de ntop y nombrarlo como **ntop-cert.pem**

```
# cd /etc/ntop/
# openssl req -x509 -nodes -days 365 
  \-subj '/C=US/L=Portland/CN=swim' 
  \-newkey rsa:1024 -keyout ntop-cert.pem -out ntop-cert.pem

```

### Usuario y grupo

Para que el parámetro *-u* funcione correctamente y para asegurar un poco más su instalación de ntop, debería crear un usuario y grupo dedicados.

```
# useradd -M -s /usr/bin/false ntop
# passwd -l ntop

```

**Nota:** El comando `passwd` aquí es opcional pero recomendado, ya que redundará en un sistema más seguro con respecto a su demonio ssh.

## Resolución de problemas

### **ERROR** RRD: Disabled - unable to create base directory (err 13, /var/lib/ntop/rrd)

El directorio `/var/lib/ntop/rrd/` puede no existir. Créelo y asegúrese que pertence al usuario nobody.

### Please enable make sure that the ntop html/ directory is properly installed

Si recibe este aviso mientras trata de acceder a la interfaz web, edite `/etc/conf.d/ntop` incluyendo su IP y reinicie el demonio. Por ejemplo:

```
NTOP_ARGS="-i enp1s0 -w 127.0.0.1:3000"

```

Esta es la IP que usará para acceder a la interfaz web.