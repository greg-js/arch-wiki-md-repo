Aquí dejo un pequeño TIP que me ayudó a pasar un AVI a MPEG y preparado para verlo en DVD.

**NOTA:** Sin menú.

# Usando tovid

```
# pacman -S tovid 

```

```
$ tovid -pal -dvd -in archivo_avi -out nombre_pelicula_salida [b]sin extension[/b]

```

```
$ makexml -dvd video.mpg -out mydvd [b]sin extension[/b]

```

```
$ makedvd -burn -device /dev/hdX mydvd.xml //donde hdx corresponde a la grabadora.

```

# Usando encode2mpeg

- Instalar encode2mpeg:

[https://aur.archlinux.org/packages.php?do_Details=1&ID=3248&O=0&L=0&C=0&K=encode2&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd](https://aur.archlinux.org/packages.php?do_Details=1&ID=3248&O=0&L=0&C=0&K=encode2&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd)

Para saber como instalarlo, nos vamos a:

[http://www.archlinux.com.ar/wiki/index.php/Instalando_desde_AUR](http://www.archlinux.com.ar/wiki/index.php/Instalando_desde_AUR)

```
$encode2mpeg pelicula.avi -dvd -imageonly -n p -vfr 3 -o pelicula-dvd

```

Aquí se convierte un divx a dvd, el programa crea los directorios del dvd, que después solamente tienes que grabar con el k3b o similar.