[Reflector](http://xyne.archlinux.ca/projects/reflector/) es un *script* que es capaz de obtener la lista más reciente de *[mirrors](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)")* desde la página [MirrorStatus](https://www.archlinux.org/mirrors/status/), filtrar los *mirrors* más actualizados, ordenarlos en base a su velocidad, y sobrescribir el archivo `/etc/pacman.d/mirrorlist`.

## Instalación

[Instala](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [reflector](https://www.archlinux.org/packages/?name=reflector), disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

## Uso

**Advertencia:** Por favor haz una copia de seguridad de tu archivo `/etc/pacman.d/mirrorlist` antes de continuar.

Primero, respalda tu archivo `/etc/pacman.d/mirrorlist`:

```
# cp -vf /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup

```

El siguiente comando filtrará los primeros cinco *mirrors,* los ordenará en base a su velocidad, y sobrescribirá el archivo `/etc/pacman.d/mirrorlist`:

```
# reflector --verbose -l 5 --sort rate --save /etc/pacman.d/mirrorlist

```

Este comando evaluará de manera verbosa los 200 servidores HTTP sincronizados más recientemente, los ordenará por su tasa de descarga, y sobrescribirá el archivo `/etc/pacman.d/mirrorlist`:

```
# reflector --verbose -l 200 -p http --sort rate --save /etc/pacman.d/mirrorlist

```

Para ver todos las opciones disponibles, utiliza:

```
# reflector --help

```

**Advertencia:** Asegúrate de que la lista de *mirrors* no contiene entradas extrañas antes de sincronizar o actualizar con pacman.

### Actualizar la lista de paquetes

Siempre que se hagan modificaciones al archivo `/etc/pacman.d/mirrorlist` es recomendable forzar a pacman a actualizar la lista de paquetes. Para esto ejecuta:

```
# pacman -Syy

```