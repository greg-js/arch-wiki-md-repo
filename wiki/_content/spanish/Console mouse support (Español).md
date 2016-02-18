#### ¿Como configuro un mouse para que sea usado en la consola?

Para usar su mouse en la consola, necesita el paquete **gpm**. Si no está instalado, consígalo con:

 `pacman -S gpm` 

Para usarlo, puede cargar gpm desde el archivo /etc/rc.conf, agregándolo a la línea de DAEMONS. Aquí hay un ejemplo de esta línea, incluyendo gpm:

```
DAEMONS=(syslog-ng !hotplug !pcmcia network netfs openntpd crond cups gpm)

```

El paquete gpm necesita ser inicializado con unos pocos parámetros. Estos parámetros pueden ser agregados en el archivo */etc/conf.d/gpm*. Aquí hay un ejemplo del contenido del archivo:

```
#
# Parameters to be passed to gpm
#
GPM_ARGS="-m /dev/psaux -t imps2"

```

El parámetro -m precede a la declaración del mouse que va a ser usado. El parámetro -t precede el tipo de mouse que está usando (un mouse PS2 en este caso). Para obtener una lista de los tipos disponibles para la opción -t, ejecute gpm con -t help

 `$ gpm -m /dev/psaux -t help` 

Para más información vea `man gpm`.