## Contents

*   [1 ¿Que es deluge?](#¿Que_es_deluge?)
*   [2 Instalación](#Instalación)
*   [3 Configuración](#Configuración)
    *   [3.1 Demonio e interfaz web](#Demonio_e_interfaz_web)
    *   [3.2 SSL](#SSL)

### ¿Que es deluge?

Deluge es un cliente BitTorrent, creado usando Python y GTK+ (a través de PyGTK). Deluge se puede utilizar en cualquier sistema operativo que respete el estándar POSIX. Su objetivo es brindar un nativo y completo cliente a entornos de escritorio GTK como son GNOME y Xfce. Desde el 13 de marzo de 2009 está disponible una versión oficial para Microsoft Windows. El programa utiliza la librería libtorrent escrita en C++ por medio de los bindings oficiales en Python.

## Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [deluge](https://www.archlinux.org/packages/?name=deluge) de los repositorios oficiales. El cliente con GTK+ tambien necesita el paquete [pygtk](https://www.archlinux.org/packages/?name=pygtk).

## Configuración

### Demonio e interfaz web

El usuario por defecto para deluged, el demonio de Deluge, es “deluge”. Se puede cambiar en este archivo `/etc/conf.d/deluged`. Claro que el usuario debe existir, en el caso d usar el de por defecto, este se crea automáticamente.

En el resto de esta guia se asumira que uso el usuario “deluge”. La carpeta de este usuario se encuentra en “/srv/deluge”. Advierta que no es la carpeta de descarga por defecto, allí solo se guarda la configuración, y los certificados SSL. La carpeta de descarga la puede configurar una vez que haya iniciado el cliente, en sus respectivas opciones.

Luego, iniciamos el demonio para generar la configuración por defecto en el directorio del usuario:

```
# /etc/rc.d/deluged start

```

Finalmente iniciamos la interfaz web:

```
# /etc/rc.d/deluge-web start

```

E ingresamos en “[http://maquina_con_deluge:8112”](http://maquina_con_deluge:8112”). Donde 'maquina_con_deluge' es la IP o el nombre DNS de su servidor de deluge. Cuando pregunte por un password, ingrese “deluge”, que es el password por defecto.

Las preferencias de la interfaz web están bien explicadas y la primera acción que debe realizas es cambiar el password.

Deberia agregar el demonio a `/etc/rc.conf`, para que inicie automaticamente:

```
DAEMONS=( ... network deluged deluge-web ... )

```

Solo asegúrese que su conexión este bien, y que agrego los dos demonios.

### SSL

En el caso que desee SSL para la interfaz web, necesitara generar una nueva llave/certificado. Para hacer esto pare el demonio de la interfaz web:

```
# /etc/rc.d/deluge-web stop

```

Luego valla a */srv/deluge/.config/deluge/ssl/* y ejecute:

```
# openssl req -new -x509 -nodes -out deluge.cert.pem -keyout deluge.key.pem

```

Luego edite `/srv/deluge/.config/deluge/web.conf` y modifique las directivas de **pkey** y **cert** para usar tu propia firma en los certificados y también habilitar SSL: t

```
...
"pkey": "ssl/deluge.key.pem",
...
"cert": "ssl/deluge.cert.pem",
...
"https": true,

```

Para finalizar vuelva a iniciar el demonio de la interfaz web de deluge:

```
# /etc/rc.d/deluge-web start

```