**badblocks** es una utilidad disponible para Linux que permite localizar y aislar los sectores o bloques defectuosos de una unidad de disco. Este programa genera una lista de los sectores dañados en el disco que puede ser leída por otros programas, como *mkfs*, a fin de evitar su uso y prevenir así problemas de corrupción y pérdida de datos. Es parte del proyecto [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs), y está disponible una versión portada a sistemas BSD.2​.

Un sector defectuoso en el disco duro representa una parte de la unidad en el cual los datos no se pueden leer o escribir debido a daños físicos o inconsistencias en la comprobación de los bits de paridad en el disco (CRC o error de comprobación de redundancia cíclica), es decir que está funcionando incorrectamente porque se dañaron permanentemente (un sector defectuoso puede tener efectos adversos, desde cambiar una letra en un archivo de texto hasta causar que un programa binario tiene un error de segmentación). Todos los sistemas operativos actuales realizan un mapa de los sectores defectuosos a fin de evitarlos al realizar algún proceso.

Ejecutado como programa independiente, **badblocks** devuelve una lista de bloques defectuosos, si los hubiera.Se trata de una buena opción a la hora de chequear problemas en un disco duro, con independencia de otras tecnologías de control de errores como [S.M.A.R.T.](/index.php/S.M.A.R.T. "S.M.A.R.T.") o las incluidas en el propio sistema de archivos.

**S.M.A.R.T.** (Self-Monitoring, Analysis, and Reporting Technology) está disponible en casi todos los discos duros que se utilizan en la actualidad y, en algunos casos, puede retirar automáticamente los sectores de disco duro defectuosos. De todos modos, S.M.A.R.T. sólo espera pasivamente los errores mientras que *badblocks* escribe patrones simples en cada bloque de un dispositivo y luego los lee y comprueba en busca de áreas dañadas. (Igual que [memtest86+](https://en.wikipedia.org/wiki/es:Memtest86%2B "wikipedia:es:Memtest86+") hace con la [RAM](https://en.wikipedia.org/wiki/es:Memoria_de_acceso_aleatorio "wikipedia:es:Memoria de acceso aleatorio").)

Esto se puede hacer en un modo de escritura destructivo que efectivamente [borre](/index.php/Securely_wipe_disk "Securely wipe disk") el dispositivo (¡haga una copia de seguridad!) o en modo de lectura-escritura no destructiva (¡también es recomendable la copia de seguridad!) y los modos de solo lectura.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Fidelidad de los dispositivos de almacenamiento](#Fidelidad_de_los_dispositivos_de_almacenamiento)
*   [3 Comparación con otros programas](#Comparación_con_otros_programas)
*   [4 Pruebas para sectores defectuosos](#Pruebas_para_sectores_defectuosos)
    *   [4.1 Prueba de lectura-escritura (advertencia: destructiva)](#Prueba_de_lectura-escritura_(advertencia:_destructiva))
        *   [4.1.1 Definir un patrón de prueba específico](#Definir_un_patrón_de_prueba_específico)
            *   [4.1.1.1 Patrón aleatorio](#Patrón_aleatorio)
    *   [4.2 Prueba de lectura-escritura (no destructiva)](#Prueba_de_lectura-escritura_(no_destructiva))
*   [5 El sistema de archivos tiene bloques defectuosos](#El_sistema_de_archivos_tiene_bloques_defectuosos)
    *   [5.1 Durante la comprobación del sistema de archivos](#Durante_la_comprobación_del_sistema_de_archivos)
    *   [5.2 Antes de la creación del sistema de archivos](#Antes_de_la_creación_del_sistema_de_archivos)
        *   [5.2.1 Ext4](#Ext4)
        *   [5.2.2 Tamaño de bloque](#Tamaño_de_bloque)
*   [6 Ver también](#Ver_también)

## Instalación

El paquete [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) es parte de [base group](/index.php/Base_group "Base group"). Vea [badblocks(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/badblocks.8) para su uso.

## Fidelidad de los dispositivos de almacenamiento

Aunque no hay una regla firme, es lógico pensar que una nueva unidad debe tener cero sectores defectuosos. Con el tiempo, los sectores defectuosos se desarrollarán y, aunque pueden definirse en el sistema de archivos para evitarlos, el uso continuo de la unidad generalmente puede dar lugar a la formación de sectores defectuosos adicionales y, por lo general, es el presagio de su muerte final. Se recomienda reemplazar el dispositivo.

## Comparación con otros programas

La práctica recomendada típica para probar un dispositivo de almacenamiento en busca de sectores defectuosos es utilizar el programa de pruebas del fabricante. La mayoría de los fabricantes tienen programas que hacen esto. El principal razonamiento para esto es que los fabricantes generalmente tienen sus estándares incorporados en los programas de prueba que le dirán si la unidad necesita ser reemplazada o no. La advertencia aquí es que algunos programas de prueba de los fabricantes no muestran los resultados completos de las pruebas y permiten que un cierto número de sectores defectuosos sean mostrados o no. Los programas de los fabricantes, sin embargo, son generalmente más rápidos que los "badblocks", a veces mucho más.

## Pruebas para sectores defectuosos

Para probar los sectores defectuosos en Linux, se usa normalmente. *badblocks* . *badblocks* tiene varios modos diferentes para poder detectar sectores defectuosos.

### Prueba de lectura-escritura (advertencia: destructiva)

Esta prueba es principalmente para probar nuevas unidades de disco y es una prueba de lectura y escritura. A medida que el patrón se escribe en cada bloque accesible, el dispositivo se [borra](/index.php/Securely_wipe_disk "Securely wipe disk") de manera efectiva. Por defecto es una prueba extensiva con cuatro pasadas usando cuatro patrones diferentes: 0xaa (10101010), 0x55 (01010101), 0xff (11111111) y 0x00 (00000000). En el caso de algunos dispositivos, esto tardará un par de días en completarse.

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

	`-o */path/to/output-file*`: imprimime sectores defectuosos en *archivo-salida* en lugar de la salida estándar

	`-t *test_pattern*`: Especifiqua un patrón. Ver abajo.

#### Definir un patrón de prueba específico

**Desde la página de manual:** El "patrón_prueba" puede ser un valor numérico entre 0 y ULONG_MAX-1 inclusive, o la palabra *random* (aleatorio), que especifica que el bloque debe rellenarse con un patrón de bits aleatorio. Para los modos de lectura/escritura (-w) y no destructivo (-n), se pueden especificar uno o más patrones de prueba especificando la opción -t para cada patrón de prueba deseado.

Para el modo de sólo lectura sólo se puede especificar un patrón único y no puede ser "aleatorio". Las pruebas de sólo lectura , con un patrón asumen que el patrón especificado ha sido escrito previamente en el disco, si no, un gran número de bloques fallarán en la verificación. Si se especifican múltiples patrones, todos los bloques se probarán con un patrón antes de proceder al siguiente.

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

**Advertencia:** Esto no es seguro para fines criptográficos. Un "patrón aleatorio" es una contradicción en sí misma. Como *badblocks* no aplica (como [/dev/urandom](https://en.wikipedia.org/wiki//dev/random "wikipedia:/dev/random")) procedimientos sofisticados para reutilizar la entropía, sino que simplemente repite un "patrón aleatorio", no debería utilizarse cuando se necesiten datos aleatorios, por ejemplo para la [encriptación de dispositivos de bloques.](/index.php/Securely_wipe_disk#Preparations_for_block_device_encryption "Securely wipe disk").

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

### Antes de la creación del sistema de archivos

Alternativamente, esto se puede hacer antes de la creación del sistema de archivos.

Si se ejecuta *badblocks* sin la opción `-o`, los sectores defectuosos solo se imprimirán en la salida estándar.

Ejemplo de salida para errores de lectura al principio del disco:

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

Para pasar cómodamente la salida de error *badblocks* al sistema de archivos, debe escribirse en un archivo.

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

Despues (re) crea el sistema de archivos con la información:

```
# mkfs.*filesystem-type* **-l** /root/*badblocks.txt* /dev/*device*

```

**Nota:** El significado de los errores `0/0/527405` es *número_de_errores_de_lectura* / *número_de_errores_de_escritura* / *número_de_errores_de_corrupción*.

#### Ext4

De la página de manual [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8):

	Tenga en cuenta que los números de bloque de la lista de bloques defectuosos deben generarse utilizando el mismo tamaño de bloque que el utilizado por *mke2fs*. Como resultado, la opción `-c` de *mke2fs* es un método mucho más simple y menos propenso a errores para comprobar si un disco tiene bloques defectuosos antes de formatearlo.

Así que el método recomendado es usar:

```
# mkfs.ext4 -c /dev/*device*

```

Utilice `-cc` para realizar una prueba de lectura y escritura de bloques defectuosos..

#### Tamaño de bloque

En primer lugar, busque los sistemas de archivos **tamaño de bloque**. Por ejemplo para sistemas de archivos ext#:

```
# dumpe2fs /dev/*device-PARTITION* | grep 'Block size'

```

Añada esto a *badblocks*:

```
# badblocks -b *block size*

```

## Ver también

*   [Mi disco duro tiene sectores defectuosos o está desarrollando sectores defectuosos con el paso del tiempo](http://www.pcguide.com/ts/x/comp/hdd/errorsBadSectors-c.html) -**Inglés**

*   [badblocks(8) - Linux man page](https://linux.die.net/man/8/badblocks) -**Inglés**

*   [Badblocks - Wikipedia](https://en.wikipedia.org/wiki/es:Badblocks "wikipedia:es:Badblocks") - **Español**