*badblocks* es un programa para probar dispositivos de almacenamiento en busca de bloques defectuosos.

En caso de un disco duro, todo el sector debería retirarse. Un sector es una subdivisión de una pista en un dispositivo de almacenamiento y los sectores que se han deteriorado no se pueden usar porque se dañaron permanentemente (un sector defectuoso puede tener efectos adversos, desde cambiar una letra en un archivo de texto hasta causar que un programa binario tiene una falla de segmentación).

[S.M.A.R.T.](/index.php/S.M.A.R.T. "S.M.A.R.T.") (Self-Monitoring, Analysis, and Reporting Technology) está disponible en casi todos los discos duros que se utilizan en la actualidad y, en algunos casos, puede retirar automáticamente los sectores de disco duro defectuosos. De todos modos, S.M.A.R.T. sólo espera pasivamente los errores mientras que *badblocks* escribe patrones simples en cada bloque de un dispositivo y luego los lee y comprueba en busca de áreas dañadas. (Igual que [memtest86+](https://en.wikipedia.org/wiki/es:Memtest86%2B "wikipedia:es:Memtest86+") hace con la [RAM](https://en.wikipedia.org/wiki/es:Memoria_de_acceso_aleatorio "wikipedia:es:Memoria de acceso aleatorio").)

Esto se puede hacer en un modo de escritura destructivo que efectivamente [limpie](/index.php/Securely_wipe_disk "Securely wipe disk") el dispositivo (¡haga una copia de seguridad!) o en modo de lectura-escritura no destructiva (¡también es recomendable la copia de seguridad!) y los modos de solo lectura.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Fidelidad de los dispositivos de almacenamiento](#Fidelidad_de_los_dispositivos_de_almacenamiento)
*   [3 Comparaciones con otros programas](#Comparaciones_con_otros_programas)
*   [4 Pruebas para sectores defectuosos](#Pruebas_para_sectores_defectuosos)
    *   [4.1 Prueba de lectura-escritura (advertencia: destructiva)](#Prueba_de_lectura-escritura_(advertencia:_destructiva))
        *   [4.1.1 Definir un patrón de prueba específico](#Definir_un_patrón_de_prueba_específico)
            *   [4.1.1.1 Patrón aleatorio](#Patrón_aleatorio)
    *   [4.2 Prueba de lectura-escritura (no destructiva)](#Prueba_de_lectura-escritura_(no_destructiva))
*   [5 El sistema de archivos tiene bloques defectuosos](#El_sistema_de_archivos_tiene_bloques_defectuosos)
    *   [5.1 Durante la comprobación del sistema de archivos](#Durante_la_comprobación_del_sistema_de_archivos)
    *   [5.2 Before filesystem creation](#Before_filesystem_creation)
        *   [5.2.1 Ext4](#Ext4)
        *   [5.2.2 Block size](#Block_size)
*   [6 See also](#See_also)

## Instalación

El paquete [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) es parte de [base group](/index.php/Base_group "Base group"). Vea [badblocks(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/badblocks.8) para su uso.

## Fidelidad de los dispositivos de almacenamiento

Aunque no hay una regla firme, es común pensar que una nueva unidad debe tener cero sectores defectuosos. Con el tiempo, los sectores defectuosos se desarrollarán y, aunque pueden definirse en el sistema de archivos para evitarlos, el uso continuo de la unidad generalmente resultará en la formación de sectores defectuosos adicionales y, por lo general, es el presagio de su muerte final. Se recomienda reemplazar el dispositivo.

## Comparaciones con otros programas

La práctica recomendada típica para probar un dispositivo de almacenamiento en busca de sectores defectuosos es utilizar el programa de pruebas del fabricante. La mayoría de los fabricantes tienen programas que hacen esto. El principal razonamiento para esto es que los fabricantes generalmente tienen sus estándares incorporados en los programas de prueba que le dirán si la unidad necesita ser reemplazada o no. La advertencia aquí es que algunos programas de prueba de los fabricantes no imprimen los resultados completos de las pruebas y permiten que un cierto número de sectores defectuosos digan solo si pasan o no. Los programas de los fabricantes, sin embargo, son generalmente más rápidos que los "badblocks", a veces mucho más.

## Pruebas para sectores defectuosos

Para probar los sectores defectuosos en Linux, el programa "badblocks" se usa normalmente. *badblocks* tiene varios modos diferentes para poder detectar sectores defectuosos.

### Prueba de lectura-escritura (advertencia: destructiva)

Esta prueba es principalmente para probar nuevas unidades de disco y es una prueba de lectura y escritura. A medida que el patrón se escribe en cada bloque accesible, el dispositivo obtiene una [limpieza](/index.php/Securely_wipe_disk "Securely wipe disk"). Por defecto es una prueba extensiva con cuatro pasadas usando cuatro patrones diferentes: 0xaa (10101010), 0x55 (01010101), 0xff (11111111) y 0x00 (00000000). En el caso de algunos dispositivos, esto tardará un par de días en completarse.

 `# badblocks -wsv /dev/*device*` 
```
Checking for bad blocks in read-write mode
From block 0 to 488386583
Testing with pattern **0xaa**: done
Reading and comparing: done
Testing with pattern **0x55**: done
Reading and comparing: done
Testing with pattern **0xff**: 22.93% done, 4:09:55 elapsed. (0/0/0 errors)
[...]
Testing with pattern **0x00**: done
Reading and comparing: done
Pass completed, 0 bad blocks found. (0/0/0 errors)
```

Opciones:

	`-w`: hace una prueba de escritura destructiva

	`-s`: muestra barra de progreso

	`-v`: detalla y muestra los sectores defectuosos detectados en la salida estándar

Opciones adicionales a considerar:

	`-p *number*`: ejecuta una extensa prueba de cuatro pasadas *número* de iteraciones secuenciales

	`-o */path/to/output-file*`: imprimime sectores defectuosos en *archivo-salida* en lugar de stdout

	`-t *test_pattern*`: Especifiqua un patrón. Ver abajo.

#### Definir un patrón de prueba específico

**Desde la página de manual:** El "patrón_prueba" puede ser un valor numérico entre 0 y ULONG_MAX-1 inclusive". [...]."

##### Patrón aleatorio

*Badblocks* puede hacer que los bloques defectuosos se escriban repetidamente en un único "patrón aleatorio" con la opción `-t random`.

 `# badblocks -wsv -t random /dev/*device*` 
```
Checking for bad blocks in read-write mode
From block 0 to 488386583
Testing with **random pattern**: done                                                 
Reading and comparing: done                                                 
Pass completed, 0 bad blocks found. (0/0/0 errors)
```

**Advertencia:** Esto no es seguro para fines criptográficos. Un "patrón aleatorio" es una contradicción en sí misma. Como *badblocks* no aplica (similar [/dev/urandom](https://en.wikipedia.org/wiki//dev/random "wikipedia:/dev/random")) procedimientos sofisticados para reutilizar la entropía, sino que simplemente repiten un "patrón aleatorio", no debería utilizarse cuando se necesiten datos aleatorios, por ejemplo [cifrar dispositivo de bloqueo](/index.php/Securely_wipe_disk#Preparations_for_block_device_encryption "Securely wipe disk").

### Prueba de lectura-escritura (no destructiva)

Esta prueba está diseñada para los dispositivos que ya tienen datos en ellos. Una prueba de lectura y escritura no destructiva realiza una copia de seguridad del contenido original de un sector antes de probar con un único patrón aleatorio y luego restaurar el contenido de la copia de seguridad. Esta es una prueba de un solo paso y es útil como prueba de mantenimiento general..

 `# badblocks -nsv /dev/*device*` 
```
Checking for bad blocks in non-destructive read-write mode
From block 0 to 488386583
Checking for bad blocks (non-destructive read-write test)
Testing with **random pattern**: done                                                 
Pass completed, 0 bad blocks found. (0/0/0 errors)
```

La opción `-n` significa prueba no destructiva de lectura-escritura.

## El sistema de archivos tiene bloques defectuosos

Para no utilizar los sectores defectuosos , estos tienen que ser reconocidos por el sistema de ficheros.

### Durante la comprobación del sistema de archivos

La incorporación de sectores defectuosos se puede hacer usando la utilidad de comprobación del sistema de ficheros (`fsck`).Se le puede decir a `fsck` que use *badblocks* durante una comprobación. Para hacer una prueba de "lectura-escritura" (no destructiva) y hacer que los sectores defectuosos se den a conocer al sistema de archivos:

```
# fsck -vcck /dev/*device-PARTITION*

```

La opción `-cc` le dice a `fsck` que ejecute en modo de prueba "no destructivo", la `-v` le dice a `fsck` que muestre la salida, y la opción `-k` conserva los viejos sectores defectuosos que se detectaron..

Para hacer una prueba de "solo lectura" (no se recomienda):

```
# fsck -vck /dev/*device-PARTITION*

```

### Before filesystem creation

Alternately, this can be done before filesystem creation.

If *badblocks* is run without the `-o` option bad sectors will only be printed to stdout.

Example output for read errors in the beginning of the disk:

 `# badblocks -wsv /dev/*drive*` 
```
[...]
Testing with pattern **0xff**: done                                                 
Reading and comparing:
[...]
37584
37585 0.84% done, 7:31:08 elapsed. (0/0/527405 errors)
37586
[...]
done
Testing with pattern **0x00**:
Reading and comparing:
[...]
37584
37585
[...]
done
Pass completed, 527405 bad blocks found. (0/0/527405 errors)
```

For comfortably passing *badblocks* error output to the filesystem it has to be written to a file.

 `# badblocks -wsv **-o** /root/*badblocks.txt* /dev/*device*` 
```
Checking for bad blocks in read-write mode
From block 0 to 488386583
Testing with pattern **0xaa**: done
Reading and comparing:   6.36% done, 0:51 elapsed. (0/0/14713 errors)
[...]
Testing with pattern **0x00**: done
Reading and comparing: done
Pass completed, 527405 bad blocks found. (0/0/527405 errors)
```

Then (re-)create the file system with the information:

```
# mkfs.*filesystem-type* **-l** /root/*badblocks.txt* /dev/*device*

```

**Note:** The meaning of `0/0/527405` errors is *number_of_read_errors* / *number_of_write_errors* / *number_of_corruption_errors*.

#### Ext4

From the [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) manual page:

	Note that the block numbers in the bad block list must be generated using the same block size as used by *mke2fs*. As a result, the `-c` option to *mke2fs* is a much simpler and less error-prone method of checking a disk for bad blocks before formatting it.

So the recommended method is to use:

```
# mkfs.ext4 -c /dev/*device*

```

Use `-cc` to do a read-write bad block test.

#### Block size

First find the file systems **block size**. For example for ext# filesystems:

```
# dumpe2fs /dev/*device-PARTITION* | grep 'Block size'

```

Feed this to *badblocks*:

```
# badblocks -b *block size*

```

## See also

*   [My hard disk has bad sectors or is developing bad sectors over time](http://www.pcguide.com/ts/x/comp/hdd/errorsBadSectors-c.html)