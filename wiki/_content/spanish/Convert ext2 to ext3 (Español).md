_Si has instalado Arch en un sistema de archivos ext2, es una buena idea activar journal y convertirlo en un sistema de archivos ext3._

Solo es necesario ejecutar:

```
tune2fs -j DISCO 

```

Donde DISCO es /dev/discs/disc0/part1 o /dev/hda1 por ejemplo.

Una vez realizada la operación **tu tienes que editar**

```
/etc/fstab 

```

y cambiar

```
ext2

```

a

```
ext3

```

para la partición del disco que se cambió el sistema de archivos.