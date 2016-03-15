Este modem es de fácil instalación con la última imágen del Cd 2009.08 . Lo primero que se debe hacer es instalar el paquete linux-atm que puede ser obtenido del ftp de Arch.Ingresa al navegador la dirección [ftp://ftp.archlinux.org/core/os](ftp://ftp.archlinux.org/core/os), allí selecciona la arquitectura que corresponda y descarga el paquete, esta forma es si no tienes conexión a internet; en caso contrario puedes instalar el paquete diréctamente con el gestor pacman con la siguiente instrucción:

```
# pacman -S linux-atm

```

esto descargará el paquete y completará la instalación del mismo.

## Firmware

El driver existe. pero falta el firmware. Por lo tanto, habrá que bajarlo, descomprimirlo y luego copiarla a la carpeta /lib/firmware/ueagle-atm. El firmware se obtiene de: [http://eagle-usb.org/ueagle-atm/non-free/ueagle-data-1.1.tar.gz](http://eagle-usb.org/ueagle-atm/non-free/ueagle-data-1.1.tar.gz). En modo root crear la ueagle-atm en /lib/firmware/:

```
# mkdir /lib/firmware/ueagle-atm

```

Ahora descomprimimos el archivo recién descargado:

```
# tar -xvf ueagle-data-1.1.tar.gz

```

esto nos creará una carpeta llamada ueagle-data, ingresamos a ella:

```
# cd ueagle-data

```

y ahora copiamos todo su contenido a la carpeta que hemos creado:

```
# cp * /lib/firmware/ueagle-atm

```

Ahora debemos activar el nuevo driver, para eso escribimos:

```
# modprobe ueagle-atm

```

Hecho esto las luces del modem deberían empezar a prender y apagar, esto quiere decir que el modem se está sincronizando. Con esto ya está el modem instalado, ahora falta configurar la conexión.

Primero creamos la interfaz de red para nuestro modem:

```
# modprobe br2684

```

```
# br2684ctl -c 0 -b -a <VPI>.<VCI>

```

Si todo sale bien, aparecerá esto en pantalla:

```
RFC1483/2684 bridge: Interface "nas0" created sucessfully

```

```
RFC1483/2684 bridge: Communicating over ATM 0.0.33, encapsulation: LLC

```

```
RFC1483/2684 bridge: Interface configured

```

Por último, tecleamos:

```
# ifconfig nas0 up

```

## Asistente para configurar la conexión

Ahora debemos ingresar al asistentes de conexión donde tendremos que completar con los datos de nuestra conexión.

```
# pppoe-setup

```

Ahora para iniciar la conexión tecleamos:

```
# pppoe-start

```

Y para terminar la conexión:

```
# pppoe-stop

```

Se puede realizar un script o ejecutable para realizar todos estos pasos en una sola vez. Creamos un archivo con el nombre, por ejemplo, conectar.sh, lo editamos con el editor nano:

```
# nano conectar.sh

```

y pegamos los datos:

```
# sudo modprobe br2684

```

```
# sudo br2684ctl -c 0 -b -a <VPI>.<VCI>

```

```
# sudo ifconfig nas0 up

```

```
# sudo pppoe-start

```

guardamos, y lo marcamos como ejecutable en la propiedades del archivo.