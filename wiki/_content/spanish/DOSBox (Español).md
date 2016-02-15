## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Configuración](#Configuraci.C3.B3n)
*   [4 Uso](#Uso)

# Introducción

DOSBox es un emulador de PC con soporte para MS-DOS para correr juegos y programas de DOS.

# Instalación

La instalación es simple:

```
# pacman -S dosbox

```

# Configuración

No se necesita una configuración inicial. Sin embargo, el manual oficial de DOSBox dice que debe existir un archivo llamado
"dosbox.conf".
Por defecto para recrear el archivo:

Simplemente ejecuta DOSBox sin parámetros:

```
$ dosbox

```

Entonces en la linea de comandos de DOS:

```
Z:\> config -wc dosbox.conf

```

Y el archivo de configuración "dosbox.conf" se grabará en el actual directorio.

# Uso

Primero coloca tus juegos/programas en un directorio, entonces corre DOSBox con un parámetro para que monte el directorio:

```
$ dosbox ./directorio/

```

Eso es todo. Estas en la línea de comandos de DOS y puedes empezar a jugar tu juegos antiguos.

Para mas información visita: [http://dosbox.sourceforge.net/](http://dosbox.sourceforge.net/)