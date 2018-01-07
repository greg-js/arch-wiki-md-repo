[Powerpill](https://xyne.archlinux.ca/projects/powerpill/) es una envoltura de [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") que usa descarga paralela y segmentada para acelerar las descargas de Pacman. Internamente usa [Aria2](/index.php/Aria2 "Aria2") y [Reflector](/index.php/Reflector_(Espa%C3%B1ol) "Reflector (Español)"). Powerpill también puede usar [rsync](/index.php/Rsync_(Espa%C3%B1ol) "Rsync (Español)") para mirrors que son compatibles con este. Esto puede ser beneficioso para usuarios que usan todo el ancho de banda al descargar de un mirror. [Pacserve](/index.php/Pacserve "Pacserve") también es compatible al modificar el archivo de configuración y será usado antes de buscar en mirrors externos.

Ejemplo: al actualizar un sistema con *pacman -Syu* existe una lista de 20 paquetes con opción de actualización que en total suman 200 MB. Si el usuario los descarga con Pacman, estos descargaran uno a la vez. Si el usuario los descarga con Powerpill, se descargaran simultáneamente y en muchos casos bastante más rápido (depende de la velocidad de ancho de banda, disponibilidad de paquetes en los servidores, velocidad del servidor, etc.)

Examinando Pacman vs. Powerpill en un sistema revela una aceleración de hasta 4 veces, en el escenario del ejemplo donde la descarga de Pacman tenia una velocidad en promedio de 300kB/seg y las descargas de Powerpill tenia una velocidad en promedio de 1.2MB/seg.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
*   [3 Usando Reflector](#Usando_Reflector)
*   [4 Usando rsync](#Usando_rsync)
*   [5 Uso básico](#Uso_b.C3.A1sico)
    *   [5.1 Actualización del sistema](#Actualizaci.C3.B3n_del_sistema)
    *   [5.2 Instalación de paquetes](#Instalaci.C3.B3n_de_paquetes)
*   [6 Solución de problemas](#Soluci.C3.B3n_de_problemas)
*   [7 Vea también](#Vea_tambi.C3.A9n)

## Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [powerpill](https://aur.archlinux.org/packages/powerpill/).

## Configuración

Powerpill tiene un solo archivo de configuración `/etc/powerpill/powerpill.json`, el cual se puede modificar como se prefiera. Revise el manual [powerpill.json(1)](https://xyne.archlinux.ca/projects/powerpill/#powerpill.json1) para más detalles.

## Usando Reflector

Por defecto, Powerpill esta configurado para usar [Reflector](/index.php/Reflector_(Espa%C3%B1ol) "Reflector (Español)") al descargar la lista actual de mirrors disponibles desde el API de Arch Linux, para usarlos en la descarga paralela de paquetes. Así se asegura que hay suficientes servidores en la lista para una aceleración significativa en la descarga.

## Usando rsync

La compatibilidad de [Rsync](/index.php/Rsync "Rsync") depende del mirror. Cuando esta disponible, la sincronización de las bases de datos (`pacman -Sy`), y otras operaciones pueden ser mucho mas rápidas porque una sola conexión es usada. El protocolo Rsync también acelera la verificación de actualizaciones y a veces la transferencia de archivos.

Para encontrar un servidor compatible, use `reflector`:

```
$ reflector -p rsync

```

Alternativamente se pueden encontrar la cantidad de servidores `*n*` mas rápidos con el parámetro `-f *n*`, y la cantidad de servidores `*m*` que han sido actualizados mas recientemente con el parámetro `-l *m*`:

```
$ reflector -p rsync -f *n* -l *m*

```

Seleccione el/los mirror(s) que desee usar. El parámetro `-c` también puede ser usado para filtrar por país, (`reflector --list-countries` para ver una lista completa, use comillas alrededor del nombre y se distingue mayúsculas de minúsculas). Una vez terminado, modifique `/etc/powerpill/powerpill.json`, en la parte baja del archivo donde `rsync` aparece, y agregue tantos servidores como quiera en el campo de servidores.

Después de hacer estas modificaciones, todas las actualizaciones de bases de datos y paquetes se descargaran con un servidor rsync si esta disponible.

## Uso básico

Para la mayoría de operaciones *powerpill* funciona como pacman, ya que es un script que envuelve a *pacman*.

### Actualización del sistema

Para actualizar su sistema (sincronización y actualización de paquetes) usando powerpill, simplemente pase los parámetros `-Syu`, como se ejecutaría con *pacman*:

```
# powerpill -Syu

```

### Instalación de paquetes

Para instalar un paquete y sus dependencias usando powerpill, simplemente use el parámetro `-S`, como se ejecutaría en *pacman*:

```
# powerpill -S *paquete*

```

También se puede pasar una lista de paquetes de la misma manera que con *pacman*:

```
# powerpill -S *paquete1* *paquete2* *paquete3*

```

## Solución de problemas

En caso de tener un error [err] con los archivos de repositorio <repo>.db.sig:

```
   b5d7d7|ERR |       0B/s|/var/lib/pacman/sync/extra.db.sig
   899e91|ERR |       0B/s|/var/lib/pacman/sync/multilib.db.sig
   8fcc32|ERR |       0B/s|/var/lib/pacman/sync/core.db.sig
   85eb3d|ERR |       0B/s|/var/lib/pacman/sync/community.db.sig

```
Es causado por la ausencia de las firmas para ese repositorio, y no se ha configurado el parámetro `SigLevel = PackageRequired` explicitamente en el archivo `/etc/pacman.conf`, como se explica en este [post del forum](https://bbs.archlinux.org/viewtopic.php?pid=1254940#p1254940).

## Vea también

*   [Powerpill](http://xyne.archlinux.ca/projects/powerpill/) - Página oficial de proyecto
*   [powerpill reborn](https://bbs.archlinux.org/viewtopic.php?id=153818) - powerpill esta de vuelta :)