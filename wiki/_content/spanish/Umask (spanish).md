El modo de creación de archivos de la máscara de usuario ([umask](https://en.wikipedia.org/wiki/es:Umask "wikipedia:es:Umask")) se utiliza para determinar el permiso de un archivo para los archivos recién creados. Se puede utilizar para controlar el permiso predeterminado del archivo para los nuevos archivos. Es un número [octal](https://en.wikipedia.org/wiki/es:Octal "wikipedia:es:Octal") de cuatro dígitos.

## Configurar UMASK

Se puede configurar el valor umask en `/etc/bashrc` o `/etc/profile` (este último para todos los usuarios). Por defecto, la mayoría de las distribuciones Linux establecen el valor en 0022 (022) o 0002 (002).

Abra el archivo `/etc/profile` (global) o `~/.bashrc`

```
# vi /etc/profile

```

o

```
$ vi ~/.bashrc

```

Añada/modifique la línea siguiente para configurar una nueva umask:

```
umask 022

```

Guarde y cierre el archivo. Los cambios tendrán efecto después del siguiente inicio de sesión.

Pero, ¿qué es 0022 y 0002?

El umask por defecto `0002` se utiliza para los usuarios regulares. Con esta máscara, los permisos predeterminados de los directorios son 775, y los permisos predeterminados de los archivos son 664.

El umask por defecto para el usuario root es `0022` , y como resultado, los permisos predeterminados de los directorios son 755, y los permisos predeterminados de los archivos son 644.

Para los directorios, los permisos de base son 0777 (rwxrwxrwx) y para los archivos son 0666 (rw-rw-rw).

Para calcular los permisos de los directorios para un valor umask de 022 (usuario root):

```
Default permission: 777
Subtract umask value: 022 (-)
Directory permission: 755

```

Para calcular los permisos de los archivos para un valor umask de 022 (usuario root):

```
Default permission: 666
Subtract umask value: 022 (-)
File permission: 644

```

En el ejemplo siguiente se exponen los pasos necesarios para establecer un valor umask que resultará en valores de permisos para los directorios de 700 y para los archivos de usuario de 600\. La idea muy simple es que solo el usuario podrá leer o escribir el archivo, o acceder a los contenidos del directorio.

```
Default permissions:777 / 666    # Permisos por defecto
Subtract umask value: 077 (-)    # Reste el valor umask
Resulting permissions:700 / 600  # Permisos resultantes

```

```
$ umask 077
$ touch file.txt
$ mkdir directory
$ ls -ld file.txt directory

```

Salida:

```
drwx------ 2 vivek vivek 4096 2007-02-01 02:21 directory
-rw------- 1 vivek vivek    0 2007-02-01 02:21 file.txt

```

```
Muestra de valores umask y permisos
valor umask 	Usuario Grupo 	Otros
0000 		all 	all 	all
0007 		all 	all 	none
0027 		all 	read 	none

```

Para obtener más información, véase 'man bash' y 'help umask'.

## Véase también

[http://www.cyberciti.biz/tips/understanding-linux-unix-umask-value-usage.html](http://www.cyberciti.biz/tips/understanding-linux-unix-umask-value-usage.html) (fuente de este artículo)