[Reflector](http://xyne.archlinux.ca/projects/reflector/) es un _script_ que es capaz de obtener la lista más reciente de _[mirrors](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)")_ desde la página [MirrorStatus](https://www.archlinux.org/mirrors/status/), filtrar los _mirrors_ más actualizados, ordenarlos en base a su velocidad, y sobrescribir el archivo `/etc/pacman.d/mirrorlist`.

## Instalación

[Instala](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") el paquete [reflector](https://www.archlinux.org/packages/?name=reflector), disponible en los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)").

## Uso

**Advertencia:** Por favor haz una copia de seguridad de tu archivo `/etc/pacman.d/mirrorlist` antes de continuar.

Primero, respalda tu archivo `/etc/pacman.d/mirrorlist`:

```
# cp -vf /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup

```

El siguiente comando filtrará los primeros cinco _mirrors,_ los ordenará en base a su velocidad, y sobrescribirá el archivo `/etc/pacman.d/mirrorlist`:

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

**Advertencia:** Asegúrate de que la lista de _mirrors_ no contiene entradas extrañas antes de sincronizar o actualizar con pacman.

### Actualizar la lista de paquetes

Siempre que se hagan modificaciones al arhivo `/etc/pacman.d/mirrorlist` es recomendable forzar a pacman a actualizar la lista de paquetes. Para esto ejecuta:

```
# pacman -Syy

```