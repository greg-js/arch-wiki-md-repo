Un disco RAM (ramdisk) es un área de memoria utilizada como disco. Muchas distribuciones usan /dev/ram para esto, pero en Arch no están disponibles de los dispositivos /dev/ram, por lo que hay que usar [/etc/fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") para crear un disco RAM. Es extremadamente importante acordarse de que los discos RAM se almacenan en memoria y, por consiguiente, son volátiles. Cualquier cosa almacenada en un disco RAM, se perderá si apaga el equipo o se interrumpe la alimentación de la memoria. Por lo tanto, es necesario guardar el contenido de tu disco RAM en un soporte persistente, si quieres conservarlo.

## Contents

*   [1 ¿Por qué usar uno?](#¿Por_qué_usar_uno?)
*   [2 Cómo crear un disco RAM](#Cómo_crear_un_disco_RAM)
*   [3 Ejemplo de uso](#Ejemplo_de_uso)
*   [4 Enlaces de interés](#Enlaces_de_interés)

## ¿Por qué usar uno?

Un disco RAM se almacena en RAM y, en consecuencia, es mucho más rápido que un disco o dispositivo de almacenamiento convencional. Así pues, si necesitas manipular ficheros a alta velocidad, un disco RAM puede resultar ser una solución ideal. Algunos usos relativamente comunes incluyen /tmp, /var/cache/pacman o /var/lib/pacman, aunque estoy convencido de que se te han venido a la cabeza muchos más.

## Cómo crear un disco RAM

Para crear un disco RAM, debes proceder igual que para montar cualquier otro dispositivo de almacenamiento. En primer lugar, debes elegir el punto de montaje deseado (directorio) y, a continuación, añadirlo a /etc/fastab, tal como se indica seguidamente:

```
none     /directorio/punto/montaje     ramfs  defaults   0     0

```

Si no dispones de una gran cantidad de memoria RAM, se recomienda usar 'tmpfs' en lugar de 'ramfs', dado que tmpfs usará Swap (memoria de intercambio; disco) cuando la memoria RAM se agote, mientras que ramfs no. Por supuesto, es lógico pensar que el acceso a Swap echará por tierra todo el beneficio de los discos RAM, por lo que no parece muy lógico usarse a menos que tengas mucha o suficiente memoria libre.

## Ejemplo de uso

Los ficheros que a editar son /etc/fstab, /etc/rc.local y /etc/rc.local.shutdown para almacenar /tmp, /var/cache/pacman y /var/lib/pacman en RAM y copiarlos a disco antes de apagar el equipo. Las partes irrelevantes de los ficheros han sido eliminadas para ahorrar espacio.

**/etc/fstab:**

```
none        /tmp         ramfs   defaults              0 0
none        /mnt/ramdisk ramfs   defaults              0 0

```

**/etc/rc.local:**

```
chmod 777 /tmp
touch /etc/ramdisk.sh

/bin/cat - >> /etc/ramdisk.sh << EOT
#!/bin/sh

cd /var/ && /bin/tar cf abs.tar abs/
cd /var/cache/ && /bin/tar cf pacman.tar pacman/
cd /var/lib/ && /bin/tar cf pacman.tar pacman/

/bin/mkdir /mnt/ramdisk/var/
/bin/mkdir /mnt/ramdisk/var/cache/
/bin/mkdir /mnt/ramdisk/var/lib/

/bin/mv /var/abs /mnt/ramdisk/var && /bin/ln -s /mnt/ramdisk/var/abs /var/abs
/bin/mv /var/cache/pacman /mnt/ramdisk/var/cache &&  /bin/ln -s /mnt/ramdisk/var/lib/pacman /var/lib/pacman
/bin/mv /var/lib/pacman /mnt/ramdisk/var/lib && /bin/ln -s /mnt/ramdisk/var/cache/pacman /var/cache/pacman

/bin/ln -s /tmp /mnt/ramdisk/tmp
/bin/chmod 777 /mnt/ramdisk/tmp
EOT

/etc/ramdisk.sh &

```

**/etc/rc.local.shutdown:**

```
echo "Guardando el contenido de memoria a disco"
rm /var/abs
rm /var/cache/pacman
rm /var/lib/pacman
mv /mnt/ramdisk/var/abs /var
mv /mnt/ramdisk/var/cache/pacman /var/cache
mv /mnt/ramdisk/var/lib/pacman /var/lib

```

## Enlaces de interés

*   [How to mount Ramdisk](https://bbs.archlinux.org/viewtopic.php?id=50893)
*   [Ramdrive setup](https://bbs.archlinux.org/viewtopic.php?pid=326269)
*   [Official tmpfs documentation](http://www.kernel.org/doc/Documentation/filesystems/tmpfs.txt)
*   [Official ramfs documentation](http://www.kernel.org/doc/Documentation/filesystems/ramfs-rootfs-initramfs.txt)