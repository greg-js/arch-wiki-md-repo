Artículos relacionados

*   [ccache](/index.php/Ccache "Ccache")
*   [Improve pacman performance](/index.php/Improve_pacman_performance "Improve pacman performance")
*   [SSH#Speeding up SSH](/index.php/SSH#Speeding_up_SSH "SSH")
*   [LibreOffice#Speed up Libreoffice](/index.php/LibreOffice#Speed_up_Libreoffice "LibreOffice")
*   [Openoffice#Speed up OpenOffice](/index.php/Openoffice#Speed_up_OpenOffice "Openoffice")
*   [Laptop](/index.php/Laptop "Laptop")
*   [Swap#Swappiness](/index.php/Swap#Swappiness "Swap")
*   [Preload](/index.php/Preload "Preload")
*   [Improve boot performance](/index.php/Improve_boot_performance "Improve boot performance")

## Contents

*   [1 Lo básico](#Lo_b.C3.A1sico)
*   [2 Conoce tu sistema](#Conoce_tu_sistema)
*   [3 Lo primero a hacer](#Lo_primero_a_hacer)
    *   [3.1 Compromiso](#Compromiso)
    *   [3.2 Test de rendimiento](#Test_de_rendimiento)
*   [4 Dispositivos de almacenamiento](#Dispositivos_de_almacenamiento)
    *   [4.1 Eligiendo y optimizando el sistema de archivos](#Eligiendo_y_optimizando_el_sistema_de_archivos)
        *   [4.1.1 Sumario](#Sumario)
        *   [4.1.2 Opciones de montaje](#Opciones_de_montaje)
        *   [4.1.3 Ext3](#Ext3)
        *   [4.1.4 Ext4](#Ext4)
        *   [4.1.5 JFS](#JFS)
        *   [4.1.6 XFS](#XFS)
        *   [4.1.7 Reiserfs](#Reiserfs)
        *   [4.1.8 BTRFS](#BTRFS)
            *   [4.1.8.1 mkinitcpio.conf para btrfs](#mkinitcpio.conf_para_btrfs)
    *   [4.2 Comprimiendo /usr](#Comprimiendo_.2Fusr)
    *   [4.3 Optimizando un disco SSD](#Optimizando_un_disco_SSD)
*   [5 CPU](#CPU)
    *   [5.1 VeryNice](#VeryNice)
*   [6 Red](#Red)
*   [7 Graficos](#Graficos)
    *   [7.1 Xorg.conf configuration](#Xorg.conf_configuration)
    *   [7.2 Driconf](#Driconf)
    *   [7.3 Overclock del GPU](#Overclock_del_GPU)
*   [8 RAM y swap](#RAM_y_swap)
    *   [8.1 valor de Intercambio](#valor_de_Intercambio)
    *   [8.2 Compcache](#Compcache)
    *   [8.3 Montando /tmp en RAM](#Montando_.2Ftmp_en_RAM)
    *   [8.4 Usando la RAM de la placa de video](#Usando_la_RAM_de_la_placa_de_video)
    *   [8.5 Precarga](#Precarga)
        *   [8.5.1 Go-preload](#Go-preload)
        *   [8.5.2 Preload](#Preload)
    *   [8.6 Suspender a RAM](#Suspender_a_RAM)
    *   [8.7 Opciones del kernel para el inicio](#Opciones_del_kernel_para_el_inicio)
    *   [8.8 Kernel modificado](#Kernel_modificado)
*   [9 Trucos específicos de las aplicaciones](#Trucos_espec.C3.ADficos_de_las_aplicaciones)
    *   [9.1 Firefox](#Firefox)
    *   [9.2 Gcc/Makepkg](#Gcc.2FMakepkg)
    *   [9.3 Mkinitcpio](#Mkinitcpio)
    *   [9.4 LibreOffice](#LibreOffice)
    *   [9.5 Pacman](#Pacman)
    *   [9.6 SSH](#SSH)
*   [10 Laptops](#Laptops)

## Lo básico

## Conoce tu sistema

La mejor manera de optimizar el sistema es encontrar los cuellos de botella, son subsistemas que limitan el desempeño general. Usualmente pueden ser identificados conociendo las especificaciones del sistema, pero hay algunas indicaciones básicas:

*   Si la computadora se vuelve lenta cuando grandes aplicaciones corren. Como cuando LibreOffice y Firefox, son corridas a la vez, es probable que la cantidad de RAM es insuficiente. Para verificar la RAM disponible, use este comando, y observe la linea que comienza con +/-buffers:

```
$free -m

```

*   Si el inicio es realmente lento, y si las aplicaciones toman demasiado tiempo en cargar la primera vez, pero cargan bien luego, probablemente el disco rígido sea demasiado lento. La velocidad de un disco rígido puede ser medidas usando el comando hdparam:

```
$ hdparm -t /dev/harddrive

```

Esa es la velocidad pura de lectura, definitivamente no es una prueba de rendimiento valida, pero un valor superior a los 40MB/s ( asumiendo que el dispositivo fue testeado mientras estaba ocupado) debe ser considerado un valor decente en el desempeño del sistema.

*   Si la carga del CPU es consistente aunque haya RAM disponible, entonces disminuir el uso del CPU debería ser una de las prioridades. La carga del CPU puede ser monitoreada de varias maneras, por ejemplo usando el comando top:

```
$top

```

*   Si las únicas aplicaciones que demoran son las que usan Direct Rendering, significa que están usando la placa de video, como los reproductores de video y los juegos, mejorar la performance de video debería ayudar. Para esto debemos verificar si el Direct Rendering esta activado. No ayudara el comando glxinfo:

```
$ glxinfo | grep direct

```

## Lo primero a hacer

La manera mas simple y eficiente de mejorar el desempeño general es correr aplicaciones y un entorno liviano.

*   Use un [administrador de ventanas](/index.php/Window_manager "Window manager") en vez de un [entorno de escritorio](/index.php/Desktop_environment "Desktop environment").
*   Use un [entorno de escritorio](/index.php/Desktop_environment "Desktop environment") minimalista en vez de [GNOME](/index.php/GNOME "GNOME") y [KDE](/index.php/KDE "KDE"). La elección puede incluir [LXDE](/index.php/LXDE "LXDE") o [Xfce](/index.php/Xfce "Xfce").
*   Use aplicaciones livianas. Revise la [lista de aplicaciones](/index.php/List_of_applications "List of applications") y las que los usuarios del foro recomiendan[2007](https://bbs.archlinux.org/viewtopic.php?id=41168), [2008](https://bbs.archlinux.org/viewtopic.php?id=67951), [2009](https://bbs.archlinux.org/viewtopic.php?id=78490),[2010](https://bbs.archlinux.org/viewtopic.php?id=88515), and [2011](https://bbs.archlinux.org/viewtopic.php?id=111878).
*   Remueva los DEMONIOS innecesarios y mande a segundo plano todos los que pueda en el archivo `/etc/rc.conf`.

### Compromiso

Casi toda optimización acarrea inconvenientes. Las aplicaciones livianas usualmente vienen con menos características, algunos ajustes pueden desencadenar en un sistema inestable o simplemente requerir tiempo para implementarlos y mantenerlos. Esta pagina tratara de resaltar esos inconvenientes, pero el juicio final lo debe hacer el usuario.

### Test de rendimiento

Los efectos de la optimización son en su mayoría difíciles de juzgar. Sin embargo pueden ser medidos con [tests de rendimiento](/index.php/Benchmarking "Benchmarking")

## Dispositivos de almacenamiento

### Eligiendo y optimizando el sistema de archivos

Elegir el mejor sistema de archivos para un sistema especifico es muy importante por que cada uno tiene su fuerte.

#### Sumario

*   XFS: Excelente performance con archivos grandes. Lento con archivos pequeños. Una buena elección para /home
*   Resiserfs: Excelente performance con archivos pequeños. Una buena elección para /var
*   Ext3: Una performance media, pero seguro.
*   Ext4: Buen rendimiento general. Seguro, tiene algunos problemas con sqlite y algunas otras bases de datos.
*   JFS: Buen desempeño general, muy poco uso del CPU, luego de fallas eléctricas, se recupera muy rápido
*   Btrfs: Gran desempeño general (mejor que ext4), seguro (una vez que pase a ser estable). Gran cantidad de características Aun se mantiene bajo un intenso desarrollo, se lo considera inestable. No use este sistema de archivos si no sabe bien lo que esta haciendo, se arriesga a una probable perdida de datos.

#### Opciones de montaje

Las opciones de montaje le ofrecen una manera sencilla de aumentar la velocidad sin formatear. Pueden ser usadas por medio del comando mount:

```
$ mount -o opcion1,opcion2 /dev/partición /mnt/partición

```

Para hacerlas permanentes, debe modificar /etc/fstab y hacer que queden de esta manera;

```
/dev/partición /mnt/partición tipo_de_partición opcion1,opcion2 0 0

```

Un par de opciones que mejoran el rendimiento en casi todo sistema de archivos es {Codeline|noatime,nodiratime}}. El primero es parte del conjunto de la ultima (el cual se aplica solo a los directorios. `noatime` se aplica tanto a carpetas como a directorios, en algunos casos raros, por ejemplo si usa mutt puede causar problemas menores. En vez se puede usar `realtime`, (realtime esta por defecto en kernels >2.6.30)

#### Ext3

Mire [Ext3 Filesystem Tips](/index.php/Ext3_Filesystem_Tips "Ext3 Filesystem Tips").

#### Ext4

Mire [Ext4 wiki page](/index.php/Ext4#Impact_on_performance "Ext4").

#### JFS

Mire [JFS Filesystem](/index.php/JFS_Filesystem#Optimizations "JFS Filesystem").

#### XFS

Para una velocidad optima, cree un sistema de archivos XFS con estas opciones:

```
$ mkfs.xfs -l internal,lazy-count=1,size=128m -d agcount=2 /dev/partición

```

Una opción especifica de XFS que aumentara el rendimiento es `logbufs=8`.

```
#/etc/fstab
LABEL=XFSHOME /home xfs noatime,logbufs=8 0 1

```

#### Reiserfs

La opción de montaje {{Codelinedata=writeback}} aumenta la velocidad, pero puede ocasionar que los datos se corrompan durante un fallo eléctrico. La opción `notail` incrementa el espacio usado por el sistema de archivos en aproximadamente un 5%, pero también aumenta el desempeño general. También se puede reducir el uso del disco poniendo el registro(journal) y los datos en discos separados. Esto se debe hacer cuando se crea el sistema de archivos:

```
$ mkreiserfs –j /dev/hda1 /dev/hdb1

```

Reemplace /dev/hda1 con la particion reservada para el registro, y /dev/dhb1 para los datos. Puede aprender mas sobre reiserfs en este [articulo](http://www.funtoo.org/en/articles/linux/ffg/2/).

#### BTRFS

Btrfs is un nuevo sistema de archivos que ofrece desfragmentacion en linea (en el momento que se usa), modo optimizado para discos SDD, edición de snapshots, cambio del tamaño de la particion sin perdida de datos y otras características mas. Btrfs todavía esta en etapa de desarrollo y esta disponible en el kernel (posee la marca de experimental). Puede ver m,as información en la [pagina de btrfs](http://btrfs.wiki.kernel.org/index.php/Main_Page).

##### mkinitcpio.conf para btrfs

Cuando btrfs se no se usa como raíz, los módulos y las dependencias son cargadas cuando son requeridas. Para un sistema raíz, debe asegurarse de cargarlas en la ramdisk de inicio. El modulo de btrfs depende del modulo libcrc32c. Puede agregar crc32c en la linea de modulos de /etc/mkinitcpio.conf, de esta manera:

```
MODULES="crc32c libcrc32c zlib_deflate btrfs"

```

Para evitar los errores como "unknown symbol" cuando carga el modulo de btrfs. Mire tambien [mkinitcpio-btrfs](https://aur.archlinux.org/packages/mkinitcpio-btrfs/).

### Comprimiendo /usr

Una manera de aumentar la velocidad de lectura de los discos es comprimiendo los datos, lo que deriva en menos datos a leer, pero también significa un aumento del uso del CPU. Algunos sistemas de archivos soportan una compresión transparente, es lo mas notable de btrfs y reiserfs4, pero el radio de compresión esta limitado por los bloques de 4k. Una buena alternativa es comprimir /usr en un archivo squashfs. Con bloques de 64K(128k), como se explica en este [hilo del foro de Gentoo](http://forums.gentoo.org/viewtopic-t-646289.html). Lo que este tutorial explica básicamente es como comprimr /usr dentro de un sistema de archivos squashfs comprimido. Para luego montado con aufs. De esta manera se ahora mucho espacio, usualmente dos tercios del tamaño original de /usr y las aplicaciones cargan rápido. Sin embargo, cada vez que una aplicación es instalada o reinstalada, esta se escribe descomprimida, entonces /usr debe ser recomprimido periódicamente. Squashfs se encuentra en el kernel y aufs2 esta en el repositorio extra, así que no se necesita una recompilacion del kernel lo que hace util al kernel por defecto. Dado que la guia esta vinculada a Gentoo, los siguientes comandos describen los pasos para Arch. Básicamente debemos instalar dos paquetes para hacerlo funcionar:

```
# pacman -S aufs2 squashfs-tools

```

Esto nos instalara los módulos de aufs y algunas herramientas para el manejo de squashfs. Ahora necesitamos algunos directorios extra donde almacenar los archivos de /usr como solo-lectura y otro directorio para almacenar los datos que cambien respecto a la ultima compresión, con permisos de escritura:

```
# mkdir -p /squashed/usr/{ro,rw}

```

Siempre se debe hacer una actualización del sistema antes de comprimir /usr. Si usa prelink, debe hacer un prelink completo antes de crear el archivo. Ahora es momento de comprimir /usr:

```
# mksquashfs /usr /squashed/usr/usr.sfs -b 65536

```

Estos parámetros son los sugeridos por el tutorial de Gentoo, pero puede haber un cierto margen de mejor con las opciones descriptas en [aquí](http://www.tldp.org/HOWTO/SquashFS-HOWTO/mksqoverview.html#mksqusing). Para que se monte junto con la carpeta( que tenia permisos de escritura) es necesario editar fstab:

```
# nano /etc/fstab

```

Agregue estas lineas:

```
/squashed/usr/usr.sfs   /squashed/usr/ro   squashfs   loop,ro   0 0 
usr    /usr    aufs    udba=reval,br:/squashed/usr/rw:/squashed/usr/ro 0 0

```

Ya debería ser posible reiniciar. El autor original sugiere eliminar todo el contenido del viejo directorio de /usr, pero podría causar algunos problemas si algo se estropea luego de la compresión. Es mas seguro dejar los viejos archivos para tener un respaldo.

Hay un [bash script](https://bbs.archlinux.org/viewtopic.php?pid=714052) que se diseño para automatizar el proceso de recompresion. Algunas opciones pueden ser no correlativas para Arch.

### Optimizando un disco SSD

[Trucos para maximizar el rendimiento de discos SSD](/index.php/SSD#Tips_for_maximizing_SSD_performance "SSD")

## CPU

La única manera directa de aumentar el rendimiento del CPU es aumentar la velocidad del reloj (Overclock). Esto es complicado y riesgoso, y no se recomienda a nadie exceptuando a los expertos. La mejor manera de acelerar el reloj es desde la BIOS.

Una manera de modificar la performance es usar [ [http://lkml.org/lkml/2009/9/6/136%7C](http://lkml.org/lkml/2009/9/6/136%7C) los parches de conl kolivas' para el kernel], reemplazan completamente al Completely Fair Scheduler (CFS) por el Brain Fuck Scheduler (BFS).

Los PKGBUILDS del kernel que incluyen el parche BFS pueden ser instalados desde [AUR](/index.php/AUR "AUR") o desde [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories"). Revise respectivamente las paginas de [linux-ck](https://aur.archlinux.org/packages/linux-ck/) y [linux-ck wiki](/index.php/Linux-ck "Linux-ck") , [kernel26-bfs](https://aur.archlinux.org/packages.php?ID=36384) o [kernel26-pf](https://aur.archlinux.org/packages.php?ID=40191) para mas información sobre los parches adicionales.

**Note:** BFS/CK fue diseñado para escritorios/laptops, no pasa servidores. Bajaran la latencia y funcionan bien con CPUs o menos. Con Kolivas siguiere configurar los Hertz a 1000\. Para mas información, revise [http://ck.kolivas.org/patches/bfs/bfs-faq.txt](http://ck.kolivas.org/patches/bfs/bfs-faq.txt) BFS FAQ] y [ck patches](http://www.kernel.org/pub/linux/kernel/people/ck/patches/2.6/2.6.37/2.6.37-ck1/patches/).

### [VeryNice](/index.php/VeryNice "VeryNice")

[Verynice](http://thermal.cnde.iastate.edu/~sdh4/verynice/) es un DEMONIO, disponible en [https://aur.archlinux.org/packages.php?ID=6403](https://aur.archlinux.org/packages.php?ID=6403) AUR], para ajuste dinámico de los niveles de prioridad en los ejecutables. Esto representa cuan favorecido sera por los recursos del CPU. Simplemente defina a los ejecutables por cuan importante es su respuesta, como X o las aplicaciones multimedia, como l“goodexe” en `/etc/verynice.conf`. Los ejecutables que se les quiera dar baja prioridad, deben ser definidos como “badexe”. Estas priorizaciones le darán grandes beneficios cuando el sistema este muy cargado.

## Red

Revise estas [recomendaciones generales](/index.php/General_recommendations#Networking "General recommendations").

## Graficos

### Xorg.conf configuration

El rendimiento gráfico depende en gran medida de la configuración del archivo `/etc/X11/xorg.conf`. Hay tutoriales para placas [NVIDIA](/index.php/NVIDIA "NVIDIA"), [ATI](/index.php/ATI "ATI") e [Intel](/index.php/Intel "Intel"). Configuraciones erróneas harán que Xorg deje de funcionar.

### Driconf

Driconf es una pequeña utilidad que le permitirá cambiar la configuración de direct rendering para los drivers de codigo abierto. Habilitar HyperZ aumentara el desempeño drásticamente.

### Overclock del GPU

Realizar un overclock sobre las tarjetas gráficas esta mucho mas documentado que sobre CPU, hay buena cantidad de aplicaciones que le premitiran ajustar el reloj del GPU al vuelo. Para los usuarios de ATI [rovclock](https://aur.archlinux.org/packages/rovclock/), para los de Nvidia, nvclock puede ser encontrado en el repositorio extra. Los usuarios de Intel pueden instalar [GMABooster](http://www.gmabooster.com/) desde [AUR](https://aur.archlinux.org/packages.php?ID=28197).

Los cambios pueden hacerse permanentes ejecutando los comandos apropiados luego de que X inicie, por ejemplo agregándolos al archivo `~/.xinitrc`. Por seguridad se recomienda aplicar estos cambios solo cuando sean necesarios.

## RAM y swap

### valor de Intercambio

El valor de intercambio representa cuando el kernel prefiere la swap a la RAM. Configurarlo a un valor muy bajo, significa que el kernel casi siempre usara la RAM. Lo que mejorara el desempeño, para hacer esto debemos agregar estas lineas al archivo `/etc/sysctl.d/99-sysctl.conf`:

```
vm.swappiness=20
vm.vfs_cache_pressure=50

```

Para probarlo, revisa este [articulo(ingles)](http://rudd-o.com/en/linux-and-free-software/tales-from-responsivenessland-why-linux-feels-slow-and-how-to-fix-that).

### Compcache

[Compcache](http://code.google.com/p/compcache/), también es conocido como el modulo zram, su función es crear un dispositivo swap en RAM y comprimirlo. Significa que esa parte de la ram podrá almacenar mayor información, pero usara mas CPU. Pero es muchísimo mas rápido que cualquier swap de disco rigido. Si el sistema usa a menudo la swap, ésto mejorará su desempeño de manera drástica. Zram es considerado estable desde la version Linux 3.14.

```
 modprobe zram

```

También es posible (y se recomienda) decirle a compache que vuelva a usar la swap del disco rígido, cuando la de la RAM este completa. Para esto hay que definir un dispositivo en el archivo de configuración, este no debe estar en uso cuando zram es iniciado, debe ser removido de /etc/fstab !

Tambien es una buena manera para reducir los ciclos de lectura/escritura del disco, hacer que la swap este en un disco SSD.

### Montando /tmp en RAM

Esto hará el sistema un poquito mas rápido, pero consumirá algo de RAM. Esto también reduce los ciclos de lectura/escritura, y es una buena opción usar un SSD o si tiene demasiada RAM. Simplemente agregue estas lineas al archivo `/etc/fstab` y reinicie:

```
tmpfs /tmp tmpfs defaults,noatime,nodev,nosuid,mode=1777 0 0

```

### Usando la RAM de la placa de video

En el desagradable caso de que tenga poca RAM y buena RAM de video, puede usar la ultima como swap. Revise [Swap on video ram](/index.php/Swap_on_video_ram "Swap on video ram").

### Precarga

Precargar es seleccionar y mantener determinados archivos en RAM. El uso practico es precargar aplicaciones para que estar carguen rápido, por que leerlas de la RAM es siempre mas rápido que desde el disco rígido. Sin embargo, parte de su RAM sera dedicada a esta tarea, pero no mas de la que utilizaría la aplicación abierta. Por lo tanto la precarga es optima para cargar las aplicaciones que usa con mas frecuencia, como Firefox o Libreoffice.

#### Go-preload

[Go-preload](https://aur.archlinux.org/packages.php?ID=34207) es un pequeño DEMONIO creado en el [| Foro de Gentoo.](http://forums.gentoo.org/viewtopic-t-789818-view-next.html?sid=5457cff93039fc7d4a3e445ef90f9821). Para usarlo, debe ejecutar este comando por cada programa que se desee precargar, en un terminal:

```
# gopreload-prepare program

```

Luego, como dice, presione enter cuando el programa este completamente cargado. Esto agregara una lista de archivos necesitados por el programa en `/usr/share/gopreload/enabled`. Para cargar todas las listas al iniciop, simplemente agregue gopreload a la lista de DEMONIOS en `/etc/rc.conf`. Para deshabilitar la carga de un programa, remueva la lista apropiada en `/usr/share/gopreload/enabled`, o muevala a `/usr/share/gopreload/disabled`.

#### Preload

Una manea mas automatizada, aunque menos KISS, que se enfoca en [Preload](/index.php/Preload "Preload"). Todo lo que debe hacer es agregarlo a la lista de DEMONIOS en `/etc/rc.conf`. Hará que monitoree los archivos mas usados en el sistema, e ira creando su propia lista para la precarga al inicio.

### Suspender a RAM

La mejor manera de reducir el tiempo de inicio del sistema es... no iniciar el sistema. Considere [suspender su sistema en la ram](/index.php/Suspend_to_RAM "Suspend to RAM").

### Opciones del kernel para el inicio

Algunas opciones le permitirán reducir el tiempo en que se carga el kernel. La opción `fastboot` usualmente le quitaran aproximadamente un segundo. También, si ve un mensaje como Waiting 8s for device XXX", puede agregar `rootdelay=1` para que se reduzca el tiempo de espera, pero debera tener cuidado, puede dañar el inicio del sistema. Estas opciones se especifican en `/boot/grub/menu.lst` o `/etc/lilo.conf`, dependido que cargador use.

### Kernel modificado

Compilar un kernel modificado reducirá el tiempo de inicio y el uso de memoria, pero puede ser largo, complicado y hasta aveces doloroso. Usualmente no vale la pena. Pero es muy interesante y una buena experiencia de aprendizaje. Si realmente le interesa, puede revisar [esto](/index.php/Kernel_Compilation "Kernel Compilation").

## Trucos específicos de las aplicaciones

### Firefox

```
El articulo sobre [Firefox](/index.php/Firefox "Firefox") ofrece algunos buenos trucos; los mas notables son [Firefox Tips and Tweaks#Improve rendering by disabling pango |deshabilitar pango]], [Limpiar la base de datis SQLite](/index.php/Firefox_Tips_and_Tweaks#Defragment_the_profile.27s_SQLite_databases "Firefox Tips and Tweaks"), y usar  [firefox-pgo](/index.php/Firefox#Firefox_customized_for_speed "Firefox"). Revise cambien: [Aumentar la velocidad de Firefox usando tmpfs](/index.php?title=Aumentar_la_velocidad_de_Firefox_usando_tmpfs&action=edit&redlink=1 "Aumentar la velocidad de Firefox usando tmpfs (page does not exist)"), and [Apagando el ati-pishing](/index.php/Firefox_Tips_and_Tweaks#Turn_off_anti-phishing "Firefox Tips and Tweaks").

```

### Gcc/Makepkg

Revisar [Ccache](/index.php/Ccache "Ccache").

### Mkinitcpio

El usuario josh_ del foro realizo algunos cambios en el script de mkinitcpio, haciéndolo dos o tres veces mas rapido. Mientras que esperamos que estos cambios sean implementados, podes obtenerlos desde [aquí](https://bbs.archlinux.org/viewtopic.php?id=79898).

### LibreOffice

Revise [Aumentando la velocidad de libreoffice](/index.php/LibreOffice#Speed_up_LibreOffice "LibreOffice").

### Pacman

Revise [Mejorando el rendimiento de pacman](/index.php/Improve_pacman_performance "Improve pacman performance").

### SSH

Revise [Aumentando la velocidad de SSH](/index.php/SSH#Speeding_up_SSH "SSH").

## Laptops

Revise [Laptop](/index.php/Laptop "Laptop").