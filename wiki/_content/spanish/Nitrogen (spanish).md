## Contents

*   [1 Introduccion](#Introduccion)
*   [2 Instalacion](#Instalacion)
*   [3 Uso](#Uso)
    *   [3.1 Colocando un fondo de escritorio](#Colocando_un_fondo_de_escritorio)
    *   [3.2 Restaurando imagen de fondo](#Restaurando_imagen_de_fondo)

# Introduccion

[Nitrogen](http://l3ib.org/nitrogen/) es un navegador/colocador de fondos de escritorio rapido y ligero para X.

# Instalacion

Nitrogen esta disponible en los repositorios standar:

```
# pacman -S nitrogen

```

# Uso

Ejecute **nitrogen --help** para los una lista completa de detalles. Los siguientes ejemplos le setan util:

## Colocando un fondo de escritorio

Para ver y colocar una imagen desde un directorio ( recursivamente, esto significa que revisara las carpetas contenidas en el interior de la especificada), ejecute:

```
$ nitrogen /ruta/al/directorio/de/las/imagenes/

```

Para ver y colocar una imagen desde un directorio ( no recursivamente), ejecute:

```
$ nitrogen --no-recurse /ruta/al/directorio/de/las/imagenes/

```

## Restaurando imagen de fondo

Para restaurar el fondo de escritorio en las sesiones subsecuentes, debe agregar esta linea a su archivo de inicio (ej: ~/.xinitrc, ~/.config/openbox/autostart.sh, etc.):

```
nitrogen --restore &

```

**Note:** En versiones menores o iguales a la 1.5.2-1, al hacer doble click sobre la imagen esta se pone como vista previa, los cambios no se guradan, uno debe clickear sobre el boton aplicar para que la imagen se ponga como fondo y se restaure correctamente.