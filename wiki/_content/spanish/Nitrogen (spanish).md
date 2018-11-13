Related articles

*   [feh (Español)](/index.php/Feh_(Espa%C3%B1ol) "Feh (Español)")

[Nitrogen](http://l3ib.org/nitrogen/) es un navegador/colocador de fondos de escritorio rapido y ligero para X.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Uso](#Uso)
    *   [2.1 Seleccionando un fondo de escritorio](#Seleccionando_un_fondo_de_escritorio)
    *   [2.2 Restaurando imagen de fondo](#Restaurando_imagen_de_fondo)
*   [3 Solución de problemas](#Solución_de_problemas)
    *   [3.1 Congelamiento con dos monitores](#Congelamiento_con_dos_monitores)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [nitrogen](https://www.archlinux.org/packages/?name=nitrogen).

## Uso

Ejecute `nitrogen --help` para una lista completa de opciones. Los siguientes ejemplos le serán útil:

### Seleccionando un fondo de escritorio

Para ver y seleccionar una imagen desde un directorio recursivamente, ejecute:

```
$ nitrogen /ruta/al/directorio/de/las/imágenes/

```

Para ver y seleccionar una imagen desde un directorio en modo no recursivo, ejecute:

```
$ nitrogen --no-recurse /ruta/al/directorio/de/las/imágenes/

```

### Restaurando imagen de fondo

Para restaurar el fondo de escritorio en sesiones subsecuentes, [autoarranque](/index.php/Autostarting_(Espa%C3%B1ol) "Autostarting (Español)") el siguiente comando: `nitrogen --restore &`

## Solución de problemas

### Congelamiento con dos monitores

Remueva la configuracion actual de nitrogen: [[1]](https://bbs.archlinux.org/viewtopic.php?id=46245)

```
$ rm -r ~/.config/nitrogen/

```