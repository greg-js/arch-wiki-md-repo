Artículos relacionados

*   [Mirroring](/index.php/Mirroring "Mirroring")
*   [pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")
*   [reflector (Español)](/index.php/Reflector_(Espa%C3%B1ol) "Reflector (Español)")

Esta guía esta orientada a ayudarle a seleccionar y configurar los mejores mirrors para su equipo, y mostrarle un listado de los mirrors actuales disponibles.

## Contents

*   [1 Habilitar un mirror especifico](#Habilitar_un_mirror_especifico)
    *   [1.1 Forzar a pacman para actualizar la lista de paquetes](#Forzar_a_pacman_para_actualizar_la_lista_de_paquetes)
*   [2 Estado de los mirrors](#Estado_de_los_mirrors)
*   [3 Clasificar y seleccionar los mirrors](#Clasificar_y_seleccionar_los_mirrors)
    *   [3.1 Listado por velocidad](#Listado_por_velocidad)
    *   [3.2 Listado combinado por velocidad y estatus](#Listado_combinado_por_velocidad_y_estatus)
    *   [3.3 Script de shell para automatizar el uso de Pacman Mirrorlist Generator](#Script_de_shell_para_automatizar_el_uso_de_Pacman_Mirrorlist_Generator)
    *   [3.4 Usar Reflector](#Usar_Reflector)
    *   [3.5 Elegir un mirror local](#Elegir_un_mirror_local)
*   [4 Mirrors oficiales](#Mirrors_oficiales)
    *   [4.1 IPv6-ready mirrors](#IPv6-ready_mirrors)
*   [5 Mirrors no oficiales](#Mirrors_no_oficiales)
    *   [5.1 Global](#Global)
    *   [5.2 TOR Network](#TOR_Network)
    *   [5.3 Singapur](#Singapur)
    *   [5.4 Bulgaria](#Bulgaria)
    *   [5.5 Vietnam](#Vietnam)
    *   [5.6 China](#China)
    *   [5.7 Francia](#Francia)
    *   [5.8 Alemania](#Alemania)
    *   [5.9 Indonesia](#Indonesia)
    *   [5.10 Kazakhstan](#Kazakhstan)
    *   [5.11 Malasia](#Malasia)
    *   [5.12 Nueva Zelanda](#Nueva_Zelanda)
    *   [5.13 Polonia](#Polonia)
    *   [5.14 Rusia](#Rusia)
    *   [5.15 Sudáfrica](#Sudáfrica)
    *   [5.16 Estados Unidos](#Estados_Unidos)
    *   [5.17 Hyperboria](#Hyperboria)
*   [6 Solución de problemas](#Solución_de_problemas)
    *   [6.1 Mirrors fuera de sincronización: paquetes corruptos/archivo no encontrado](#Mirrors_fuera_de_sincronización:_paquetes_corruptos/archivo_no_encontrado)
        *   [6.1.1 Utilizar todos los mirrors](#Utilizar_todos_los_mirrors)
*   [7 Véase también](#Véase_también)

## Habilitar un mirror especifico

Para habilitar los mirrors, edite el archivo `/etc/pacman.d/mirrorlist` y localice la región geográfica más cercana a su ubicación. Descomente los mirrors que desee utilizar.

**Nota:** El ancho de banda disponible en archlinux.org [está limitado a 50KB/s](https://www.archlinux.org/news/302/)

Ejemplo:

```
# Any
# Server = ftp://mirrors.kernel.org/archlinux/$repo/os/$arch
**Server = http://mirrors.kernel.org/archlinux/$repo/os/$arch**

```

Véanse los apartados [#Estado de los mirrors](#Estado_de_los_mirrors) y [#Listado por velocidad](#Listado_por_velocidad) para obtener ayuda sobre cómo escoger los mejores mirrors.

**Sugerencia:** Descomente sus 5 mirrors preferidos y ubíquelos al inicio de la lista de mirrors. De esa forma tendrán prioridad dentro de la lista de mirrors. También hace mas fácil la inclusión de actualizaciones de la lista del mirrorlist.

También es posible especificar mirrors directamente en el archivo `/etc/pacman.conf`. Para el repositorio *[core]* la configuración predifinida es:

```
[core]
Include = /etc/pacman.d/mirrorlist

```

Para utilizar el mirror *HostEurope* como el mirror predeterminado, hay que agregar su dirección antes de la linea `Include`:

```
[core]
**Server = ftp://ftp.hosteurope.de/mirror/ftp.archlinux.org/core/os/i686**
Include = /etc/pacman.d/mirrorlist

```

Ahora pacman tratara de conectarse primero a este mirror. El mismo procedimiento es válido para *[testing]*, *[extra]* y *[community]*.

**Nota:** Si los mirrors fueron especificados manualmente en el archivo `pacman.conf`, recuerde también utilizar el mismo mirror para todos los repositorios. De otra forma, puede que paquetes que son incompatibles entre sí sean instalados, como linux desde *[core]* y un modulo viejo del kernel desde *[extra]*.

### Forzar a pacman para actualizar la lista de paquetes

Después de crear/editar el archivo `/etc/pacman.d/mirrorlist`, (manualmente o utilizando `rankmirrors`) ejecute la siguiente orden:

```
# pacman -Syy

```

**Sugerencia:** Pasar dos flags `--refresh` o `-y` fuerzan a pacman a refrescar todas las listas de paquetes incluso si se considera que ya están actualizados. Ejecutar `pacman -Syy` *cada vez que cambie un mirror* es una buena práctica para evitar posibles problemas.

## Estado de los mirrors

Puede verificar el estado de los Mirrors y su nivel de actualización visitando [http://www.archlinux.de/?page=MirrorStatus](http://www.archlinux.de/?page=MirrorStatus) o [https://www.archlinux.org/mirrors/status/](https://www.archlinux.org/mirrors/status/).

Puede generar una lista de mirrors nueva y actualizada desde [aquí](https://www.archlinux.org/mirrorlist/), y automatizar el proceso con un [script](#Script_de_shell_para_automatizar_el_uso_de_Pacman_Mirrorlist_Generator), o puede instalar [Reflector](/index.php/Reflector_(Espa%C3%B1ol) "Reflector (Español)"), una herramienta que puede generar mirrors utilizando la lista de Mirrorcheck; también se puede verificar el nivel de actualización de los mirrors de la siguiente forma:

1.  elija un server y navegue por «extra/os/»;
2.  acceda a [https://www.archlinux.org/](https://www.archlinux.org/) en otro navegador o pestaña del navegador; y,
3.  compare la última fecha de modificación del directorio `i686` del mirror con la fecha del mirror en la página principal de ArchLinux, en el área de *Package Repositories* a la derecha.

## Clasificar y seleccionar los mirrors

Si no utiliza Reflector, que tiene la habilidad de clasificar los mirrors por ambos criterios: por velocidad de descarga y por última fecha de actualización, siga esta demostración de cómo clasificar los mirrors manualmente.

**Nota:** Esto no se aplica a [powerpill](/index.php/Pacman/Tips_and_tricks_(Espa%C3%B1ol)#Powerpill "Pacman/Tips and tricks (Español)"), que se conecta a varios servidores simultáneamente para aumentar la velocidad de descarga. La velocidad de las conexiones individuales se vuelve menos relevante, y powerpill-light puede ser configurado para requerir velocidades mínimas por conexión.

### Listado por velocidad

Puede sacar provecho de utilizar el mirror local mas rápido, y esto puede ser determinado por el script de bash, `/usr/bin/rankmirrors`.

Utilice la orden `cd`para moverse al directorio `/etc/pacman.d`:

```
# cd /etc/pacman.d

```

Respalde el existente `/etc/pacman.d/mirrorlist`:

```
# cp mirrorlist mirrorlist.backup

```

Edite el archivo `mirrorlist.backup` y descomente los mirrors que van a ser probados con rankmirrrors:

```
# nano mirrorlist.backup

```

Opcionalmente, puede utilizar la siguiente línea `sed` para descomentar (y probar) todos los mirrors:

```
# sed '/^#\S/ s|#||' -i mirrorlist.backup

```

Finalmente, clasifique los mirrors. El parámetro `-n 6` significa que dejará habilitados solo los 6 mirrors con mejor respuesta:

```
# rankmirrors -n 6 mirrorlist.backup > mirrorlist

```

### Listado combinado por velocidad y estatus

No es una buena idea utilizar solo los mirrrors solo por el más rápido, dado a que posiblemente el mirror mas rápido para su zona puede estar desactualizado. La forma predilecta es [#Listado por velocidad](#Listado_por_velocidad), luego ordenar esos mirrors por [su estado](#Estado_de_los_mirrors).

Simplemente visite uno o los dos links de [#Estado de los mirrors](#Estado_de_los_mirrors) y ordénelos primero por los que están más actualizados. Luego, mueva los más actualizados al principio del archivo de configuración `/etc/pacman.d/mirrorlist` y los mirrors que estén muy desactualizados simplemente no los utilize; repita el proceso hasta que elimine los mirrors mas desactualizados. Continue este proceso hasta que queden solo 6 mirrors que estén ordenados por velocidad de descarga y por nivel de actualización, dejando fuera los mirrors desactualizados o lentos.

Si se presentan problemas con los mirrors, se deben repetir los pasos de más arriba. O repetirlos, incluso, cada tanto, aunque no se estén experimentando problemas con los mirrors, para mantener un archivo `/etc/pacman.d/mirrorlist` actualizado.

### Script de shell para automatizar el uso de Pacman Mirrorlist Generator

Puede usar el siguiente script de shell para actualizar los propios mirrors en base a las clasificaciones proporcionadas por [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) (si no vive en los Estados Unidos, puede cambiar la variable del país (`country`). Se puede descargar invocando: `curl http://pastebin.ca/raw/2404700 -o pacmrr`, ([ver script](http://pastebin.ca/2404700)).

### Usar Reflector

Como alternativa, es posible utilizar [Reflector](/index.php/Reflector_(Espa%C3%B1ol) "Reflector (Español)") para recuperar los últimos mirrorlist de la página [MirrorStatus](https://www.archlinux.org/mirrors/status/), filtrar los mirror más actualizados, ordenarlos en base a la velocidad y sobreescribir el archivo `/etc/pacman.d/mirrorlist`.

### Elegir un mirror local

La forma más sencilla es editar el archivo mirrorlist y cologar un mirror local en la parte superior de la lista. Entonces pacman usará este mirror preferentemente.

Como alternativa, se puede editar el archivo pacman.conf para colocar un mirror local antes de la línea que suministra el archivo mirrorlist, es decir, donde dice "add your preferred servers here" (*«ponga aquí sus servidores preferidos»*). Es más seguro si se utiliza el mismo servidor para cada repositorio.

## Mirrors oficiales

La lista oficial de mirrors de pacman se puede obtener del paquete [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist). Para obtener una lista de mirrors aun más actualizada puede consultar la pagina de [[https://www.archlinux.org/mirrorlist/](https://www.archlinux.org/mirrorlist/) Pacman Mirrorlist Generator en la página principal. En el muy improbable escenario de que no tenga un mirrorlist configurado o `pacman-mirrorlist` no este instalado, escriba:

 `# wget -O /etc/pacman.d/mirrorlist [https://www.archlinux.org/mirrorlist/all/](https://www.archlinux.org/mirrorlist/all/)` 

Asegúrese de descomentar los mirrors preferidos como se mencionó más arriba y luego ejecute:

```
# pacman -Syy
# pacman -S --force pacman-mirrorlist

```

Si desea que su mirror sea incluido en la lista oficial, puede hacer una solicitud. Mientras tanto, puede agregarlo a la lista de [#Mirrors no oficiales](#Mirrors_no_oficiales) al final de esta página.

Si obtiene un error diciendo que la variable `$arch` es utilizada pero no definida, agregue lo siguiente al archivo de configuración `/etc/pacman.conf`:

```
 Architecture = x86_64

```

**Nota:** También puede agregar las variables `auto` y `i686` para `Architecture`.

### IPv6-ready mirrors

[Pacman mirror list generator](https://www.archlinux.org/mirrorlist/?country=all&protocol=http&ip_version=6) puede ser usado para generar una lista de mirrors IPv6.

## Mirrors no oficiales

Estos mirrors *no* están listados en el archivo de configuración `/etc/pacman.d/mirrorlist`.

### Global

*   [http://prdownloads.sourceforge.net/archlinux/](http://prdownloads.sourceforge.net/archlinux/) - *No contiene ISO recientes, utilícelo solo para obtener ISO viejos.*

### TOR Network

*   [http://cz2jqg7pj2hqanw7.onion/archlinux](http://cz2jqg7pj2hqanw7.onion/archlinux)
*   [ftp://mirror:mirror@cz2jqg7pj2hqanw7.onion/archlinux](ftp://mirror:mirror@cz2jqg7pj2hqanw7.onion/archlinux)

### Singapur

*   [http://mirror.nus.edu.sg/archlinux/](http://mirror.nus.edu.sg/archlinux/)

### Bulgaria

*   [http://mirror.telepoint.bg/archlinux/](http://mirror.telepoint.bg/archlinux/)
*   [ftp://mirror.telepoint.bg/archlinux/](ftp://mirror.telepoint.bg/archlinux/)

### Vietnam

**FPT TELECOM**

*   [http://mirror-fpt-telecom.fpt.net/archlinux/](http://mirror-fpt-telecom.fpt.net/archlinux/)

### China

**CHINA TELECOM**

*   [http://mirror.lupaworld.com/archlinux/](http://mirror.lupaworld.com/archlinux/)

**CHINA UNICOM**

*   [http://mirrors.sohu.com/archlinux/](http://mirrors.sohu.com/archlinux/)

**Cernet**

*   [http://mirrors.zju.edu.cn/archlinux/](http://mirrors.zju.edu.cn/archlinux/) - *Universidad de Zhejian*
*   [http://ftp.sjtu.edu.cn/archlinux/](http://ftp.sjtu.edu.cn/archlinux/) - *Universidad Shanghai Jiaotong*
*   [ftp://ftp.sjtu.edu.cn/archlinux/](ftp://ftp.sjtu.edu.cn/archlinux/)
*   [http://mirrors.ustc.edu.cn/archlinux/](http://mirrors.ustc.edu.cn/archlinux/) - *Universidad de Ciencia y Tecnología de China*
*   [ftp://mirrors.ustc.edu.cn/archlinux/](ftp://mirrors.ustc.edu.cn/archlinux/)
*   [http://mirrors.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.tuna.tsinghua.edu.cn/archlinux/) - *Universidad de Tsinghua*
*   [http://mirrors.4.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.4.tuna.tsinghua.edu.cn/archlinux/) *(solo ipv4)*
*   [http://mirrors.6.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.6.tuna.tsinghua.edu.cn/archlinux/) *(solo ipv6)*
*   [http://mirror.lzu.edu.cn/archlinux/](http://mirror.lzu.edu.cn/archlinux/) - *Universidad de Lanzhou*

### Francia

*   [http://delta.archlinux.fr/](http://delta.archlinux.fr/) - *Apoyo al paquete Delta. Es necesario el paquete xdelta3 disponible desde [extra].*
*   [http://mirror.soa1.org/archlinux](http://mirror.soa1.org/archlinux)
*   [ftp://mirror:mirror@mirror.soa1.org/archlinux](ftp://mirror:mirror@mirror.soa1.org/archlinux)

### Alemania

*   [http://ftp.uni-erlangen.de/mirrors/archlinux/](http://ftp.uni-erlangen.de/mirrors/archlinux/)
*   [ftp://ftp.uni-erlangen.de/mirrors/archlinux/](ftp://ftp.uni-erlangen.de/mirrors/archlinux/)
*   [http://ftp.u-tx.net/archlinux/](http://ftp.u-tx.net/archlinux/)
*   [ftp://ftp.u-tx.net/archlinux/](ftp://ftp.u-tx.net/archlinux/)
*   [http://mirror.michael-eckert.net/archlinux/](http://mirror.michael-eckert.net/archlinux/)
*   [http://linux.rz.rub.de/archlinux/](http://linux.rz.rub.de/archlinux/)

### Indonesia

*   [http://mirror.kavalinux.com/archlinux/](http://mirror.kavalinux.com/archlinux/) - *Solo para Indonesia*
*   [http://kambing.ui.ac.id/archlinux/](http://kambing.ui.ac.id/archlinux/)
*   [http://repo.ukdw.ac.id/archlinux/](http://repo.ukdw.ac.id/archlinux/)

### Kazakhstan

*   [http://archlinux.kz/](http://archlinux.kz/)
*   [http://mirror.neolabs.kz/archlinux/](http://mirror.neolabs.kz/archlinux/)
*   [http://mirror-kt.neolabs.kz/archlinux/](http://mirror-kt.neolabs.kz/archlinux/)

### Malasia

*   [http://mirror.oscc.org.my/archlinux/](http://mirror.oscc.org.my/archlinux/)
*   [http://mirrors.inetutils.net/archlinux/](http://mirrors.inetutils.net/archlinux/) - *ISO y Core*

### Nueva Zelanda

*   [http://mirror.ihug.co.nz/archlinux/](http://mirror.ihug.co.nz/archlinux/)
*   [http://mirror.ece.auckland.ac.nz/archlinux/](http://mirror.ece.auckland.ac.nz/archlinux/) *Solo NZ*

### Polonia

*   [ftp://ftp.icm.edu.pl/pub/Linux/dist/archlinux/](ftp://ftp.icm.edu.pl/pub/Linux/dist/archlinux/) - ICM UW
*   [http://ftp.icm.edu.pl/pub/Linux/dist/archlinux/](http://ftp.icm.edu.pl/pub/Linux/dist/archlinux/) - ICM UW
*   rsync://ftp.icm.edu.pl/pub/Linux/dist/archlinux/ - ICM UW

### Rusia

*   [http://hatred.homelinux.net/archlinux/](http://hatred.homelinux.net/archlinux/) - *Vladivostok, sin iso, con repositorios del proyecto <sub>[3SPY](http://hatred.homelinux.net/wiki/proekty:3spy:start)</sub> y del repositorio [**mingw32**](http://hatred.homelinux.net/archlinux/mingw32/os/i686)*
*   [http://mirrors.krasinfo.ru/archlinux/](http://mirrors.krasinfo.ru/archlinux/) - *Krasnoyarsk, Classica-Service Ltd*

### Sudáfrica

*   [http://ftp.sun.ac.za/ftp/pub/mirrors/archlinux/](http://ftp.sun.ac.za/ftp/pub/mirrors/archlinux/) - *Universidad de Stellenbosch*
*   [ftp://ftp.sun.ac.za/pub/mirrors/archlinux/](ftp://ftp.sun.ac.za/pub/mirrors/archlinux/)
*   [http://ftp.leg.uct.ac.za/pub/linux/arch/](http://ftp.leg.uct.ac.za/pub/linux/arch/) - *Universidad de Cape Town*
*   [ftp://ftp.leg.uct.ac.za/pub/linux/arch/](ftp://ftp.leg.uct.ac.za/pub/linux/arch/)
*   [http://mirror.ufs.ac.za/archlinux/](http://mirror.ufs.ac.za/archlinux/) - *Universidad de Free State*
*   [ftp://mirror.ufs.ac.za/os/linux/distros/archlinux/](ftp://mirror.ufs.ac.za/os/linux/distros/archlinux/)
*   [http://ftp.wa.co.za/pub/archlinux/](http://ftp.wa.co.za/pub/archlinux/) - *Web Africa Networks*
*   [ftp://ftp.wa.co.za/pub/archlinux/](ftp://ftp.wa.co.za/pub/archlinux/)
*   [http://archlinux.mirror.ac.za](http://archlinux.mirror.ac.za) - *TENET - Tertiary Education and Research Network of South Africa*
*   [ftp://archlinux.mirror.ac.za](ftp://archlinux.mirror.ac.za)

### Estados Unidos

*   [http://archlinux.linuxfreedom.com](http://archlinux.linuxfreedom.com) - *Contiene numerosas imágenes ISO pero no la última ISO de fecha 2011.08.19*
*   [http://mirror.pointysoftware.net/archlinux/](http://mirror.pointysoftware.net/archlinux/)

### Hyperboria

*   [http://[fc7b:5f90:01f8:2b33:7c3e:f94b:00f3:0bed]/archlinux/](http://[fc7b:5f90:01f8:2b33:7c3e:f94b:00f3:0bed]/archlinux/)

## Solución de problemas

### Mirrors fuera de sincronización: paquetes corruptos/archivo no encontrado

Los problemas con mirrors fuera de sincronización fueron ya apuntados en [este post](https://www.archlinux.org/news/482), por lo que, probablemente, ya fue solucionado para la mayoría de los usuarios, pero en el caso de que este evento se presente de nuevo, trate de verificar si los paquetes se encuentran en el repositorio [testing].

Después de sincronizar con `pacman -Sy`, utilize esta orden:

```
# pacman -Ud $(pacman -Sup | tail -n +2 | sed -e 's,/\(core\|extra\)/,/testing/,' \
                                              -e 's,/\(community\)/,/\1-testing/,')

```

Hacer esto ayudara en cualquier ocasión, cuando los paquetes en un mirror no hayan sido sincronizados en [core/extra], y residan ahora en [testing]. Es perfectamente seguro instalar desde [testing] en el caso de que los paquetes sean coincidentes por versión y fecha de liberación. En cualquier caso, es mejor cambiar los mirrors y sincronizar con `pacman -Syy`, que recurrir a un repositorio. De cualquier modo puede suceder que uno o todos los mirrors, en algún grado, estén fuera de sincronización.

#### Utilizar todos los mirrors

Para emular el comportamiento de `pacman -Su`, para que revise toda la lista de mirrors, utilize el siguiente scrpit:

 `~/bin/pacup` 
```
#!/bin/bash

# Pacman will not exit on the first error. Comment the line below to
# try from [testing] directly.
pacman -Su "$@" && exit

while read -r pkg; do
  if pacman -Ud "$pkg"; then
    continue
  else
    while read -r mirror; do
      pacman -Ud $(sed "s,.*\(/\(community-\)*testing/os/\(i686\|x86_64\)/\),$mirror\1," <<<"$pkg") &&
      break
    done < <(sed -ne 's,^ *Server *= *\|/$repo/os/\(i686\|x86_64\).*,,gp' \
           </etc/pacman.d/mirrorlist | tail -n +2 )
  fi
done < <(pacman -Sup | tail -n +2 | sed -e 's,/\(core\|extra\)/,/testing/,' \
                                        -e 's,/\(community\)/,/\1-testing/,')

```

## Véase también

*   [MirUp](http://wiki.gotux.net/code/bash/mirup) – pacman mirrorlist downloader/checker