## Instalación

Para instalar, lanzamos el siguiente comando:

```
# pacman -S minidlna

```

## Configuración

Para la configuarción del servicio tenemos: /etc/minidlna.conf. A continuación explicamos lo mínimo para que MiniDLNA funcione:

```
media_dir=/path/to/media

```

Con este parámetro especificamos a MiniDLNA donde tenemos los archivos de audio/vídeo. Se pueden crear varias rutas dependiendo si contiene vídeo, fotos o audio.

Por defecto, el nombre que se mostrará a todos los clientes será My Media Server o algo parecido, puedes modificar este nombre en el parámetro:

```
friendly_name="My Media Server"

```

Aunque no es necesario, es una buena idea habilitar el caché de MiniDLNA's (esto afectará a las carátulas y no será necesario reiniciar el servicio cada vez). Para ello, creamos los directorios y aplicamos "chown" para nobody:nobody.

```
# mkdir /var/{cache,log}/minidlna
# chown nobody:nobody /var/{cache,log}/minidlna

```

Ahora,debemos crear los archivos:

```
db_dir=/var/cache/minidlna
log_dir=/var/log/minidlna

```

Es posible que se experimenten problemas si tiene dos (o más) interfaces de red (incluyendo puentes), la opción network_interface debe establecerse de acuerdo a su configuración específica.

Puedes arrancar MiniDLNA usando el initscript en /etc/rc.d/, o si quieres que se inicie al arrancar el sistema, editamos y añadimos "miniDLNA" a DAEMONS dentro de /etc/rc.conf.